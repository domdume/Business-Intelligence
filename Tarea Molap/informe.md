# <center> **ESCUELA POLITÉCNICA NACIONAL** </center>
# <center> **Business Intelligence** </center>
# <center> **Tarea Molap** </center>

**Integrantes**
* Doménica J. Cárdenas
* Danna Morales
* Salma Morales
* Belén Cholango
* Gabriel del Valle

## **Índice de Contenidos**

1. [Introducción](#introducción)
2. [Desarrollo](#desarrollo)
    - [Modelo Estrella](#modelo-estrella)
    - [Dimensiones](#dimensiones)
    - [Tabla de hechos](#tabla-de-hechos)
    - [Vista materializada](#vista-materializada)
3. [Consultas MOLAP](#consultas-molap)
4. [Referencias bibliográficas](#referencias-bibliográficas)
5. [Declaración de uso de IA](#declaración-de-uso-de-ia)
## Introducción

En el entorno actual de la gestión de la salud, las instituciones médicas generan masivos volúmenes de datos transaccionales diariamente. Sin embargo, transformar estos registros operativos en conocimiento estratégico representa un desafío crítico. El Business Intelligence (BI) surge como la disciplina fundamental para abordar esta problemática, proveyendo herramientas y metodologías capaces de consolidar, procesar y analizar la información para optimizar la toma de decisiones clínicas, financieras y administrativas.

El presente informe documenta el desarrollo práctico de una Tarea MOLAP aplicada al sector sanitario. El proyecto aborda el diseño e implementación de un Modelo en Estrella, el cual utiliza una tabla de hechos central operativa (`fact_visitas_salud`) con un conjunto de dimensiones que capturan la demografía de los pacientes, las especialidades médicas, los diagnósticos y las temporalidades. Asimismo, se detalla la configuración de una vista materializada como estrategia de optimización física, y se exponen diversas consultas analíticas orientadas a resolver interrogantes críticas de negocio, tales como la distribución de costos institucionales y el comportamiento geográfico de las emergencias médicas. 
## Desarrollo
### Modelo estrella
### Dimensiones
Para la construcción del modelo en estrella, se definieron y crearon diversas tablas de dimensiones mediante sentencias SQL (`CREATE TABLE`). Estas tablas tienen el objetivo de otorgar el contexto necesario a los eventos médicos analizados, permitiendo responder a las preguntas de negocio. A continuación, se detalla la estructura implementada para cada dimensión:

* **Dimensión Ciudad (`dim_ciudad`):** Almacena la ubicación geográfica donde se realizó la atención médica. Contiene la clave primaria autonumérica `ciudad_key` y el nombre de la ciudad (`city`).
    
   <img width="556" height="567" alt="dim ciudad" src="https://github.com/user-attachments/assets/0f9ce648-6695-4384-837e-b3e763bef9b5" />
    <p align="center"><i>Figura 1: Sentencia SQL y registros de la dimensión Ciudad (dim_ciudad).</i></p>

* **Dimensión Diagnóstico (`dim_diagnostico`):** Categoriza el motivo médico o patología de la visita. Se compone de su llave primaria `diagnostico_key` y el grupo de diagnóstico (`diagnosis_group`, p. ej., Covid-19, Diabetes, Neumonía).
    
  <img width="503" height="575" alt="dim diagnostico" src="https://github.com/user-attachments/assets/e27fffc8-e7f3-4041-a407-d81f073e57e3" />
    <p align="center"><i>Figura 2: Sentencia SQL y registros de la dimensión Diagnóstico (dim_diagnostico).</i></p>

* **Dimensión Doctor (`dim_doctor`):** Identifica al personal médico que atendió al paciente. Incluye la llave `doctor_key`, el identificador operativo del médico (`doctor_id`) y el departamento del hospital al que pertenece (`hospital_department`).
    
   <img width="585" height="887" alt="dim doctor" src="https://github.com/user-attachments/assets/82e88822-02ec-4048-80e1-ac3850241ff6" />
   <p align="center"><i>Figura 3: Sentencia SQL y registros de la dimensión Doctor (dim_doctor).</i></p>


* **Dimensión Especialidad (`dim_especialidad`):** Clasifica la rama de la medicina bajo la cual se catalogó la visita. Utiliza `especialidad_key` como clave principal y almacena el nombre de la especialidad (`specialty`).
    
   <img width="527" height="546" alt="dim especialidad" src="https://github.com/user-attachments/assets/7c9caa11-5de0-4143-aabc-a0e8a706e3a0" />
   <p align="center"><i>Figura 4: Sentencia SQL y registros de la dimensión Especialidad (dim_especialidad).</i></p>


* **Dimensión Fecha (`dim_fecha`):** Es la dimensión de tiempo que permite el análisis cronológico y la detección de tendencias. Su llave primaria es un identificador numérico inteligente (`fecha_key`), desglosando la fecha exacta (`fecha`), año (`anio`), mes numérico (`mes`), nombre del mes (`nombre_mes`) y el periodo (`periodo_mes`).
    
    <img width="867" height="877" alt="dim_fecha" src="https://github.com/user-attachments/assets/185d2c7f-5fdc-4456-accd-d2120193694c" />
	<p align="center"><i>Figura 5: Sentencia SQL y registros de la dimensión Fecha (dim_fecha).</i></p>

* **Dimensión Paciente (`dim_paciente`):** Contiene la información demográfica de los usuarios del sistema de salud. Se estructura con `paciente_key` (PK), el identificador del paciente (`patient_id`), su edad (`patient_age`) y su género (`patient_gender`).
    
    <img width="617" height="892" alt="dim paciente" src="https://github.com/user-attachments/assets/9ec1624c-e387-4390-bd73-65dae6024cfa" />
	<p align="center"><i>Figura 6: Sentencia SQL y registros de la dimensión Paciente (dim_paciente).</i></p>

* **Dimensión Procedimiento (`dim_procedimiento`):** Describe la acción médica realizada durante la visita. Utiliza `procedimiento_key` como llave principal e incluye el tipo de procedimiento (`procedure_type`, p. ej., Cirugía mayor, Consulta).
    
   <img width="527" height="520" alt="dim procedimiento" src="https://github.com/user-attachments/assets/d32b9873-7784-420d-8559-73353dad0e14" />
	<p align="center"><i>Figura 7: Sentencia SQL y registros de la dimensión Procedimiento (dim_procedimiento).</i></p>

* **Dimensión Resultado (`dim_resultado`):** Registra el estado final o evolución del paciente tras la atención. Su estructura incluye `resultado_key` y la descripción del resultado (`outcome`).
    
    <img width="480" height="468" alt="dim resultado" src="https://github.com/user-attachments/assets/53908141-221d-411c-b0aa-58fa74f3e8c5" />
	<p align="center"><i>Figura 8: Sentencia SQL y registros de la dimensión Resultado (dim_resultado).</i></p>

* **Dimensión Seguro (`dim_seguro`):** Clasifica la cobertura financiera del paciente. Consta de `seguro_key` como clave primaria y el tipo de seguro médico (`insurance_type`).
    
    <img width="481" height="481" alt="dim seguro" src="https://github.com/user-attachments/assets/9ee34037-0144-4e4f-950c-fdb541aa32ec" />
	<p align="center"><i>Figura 9: Sentencia SQL y registros de la dimensión Seguro (dim_seguro).</i></p>
	
### Tabla de hechos
La tabla de hechos centraliza las transacciones y las métricas cuantitativas del modelo multidimensional. En este caso, la tabla **`fact_visitas_salud`** registra cada evento único de atención médica, consolidando el contexto a través de llaves foráneas e incorporando las métricas clave para el análisis financiero y operativo de la institución de salud.

La estructura construida mediante SQL se compone de la siguiente manera:

* **Llave Primaria:** `visit_id`, que identifica de forma única cada visita registrada.
* **Llaves Foráneas (FK):** Columnas que garantizan la integridad referencial conectando el hecho con sus respectivas dimensiones: `fecha_key`, `paciente_key`, `ciudad_key`, `doctor_key`, `especialidad_key`, `diagnostico_key`, `procedimiento_key`, `seguro_key` y `resultado_key`.
* **Métricas (Hechos):** Almacena los valores numéricos y booleanos que serán objeto de agregación (sumas, promedios, conteos). Incluye un indicador de emergencia (`is_emergency`), los días de estancia hospitalaria (`length_of_stay_days`), el costo de las medicinas (`cost_medicine`), el costo del procedimiento (`cost_procedure`) y la métrica financiera principal: el costo total (`total_cost`).

<img width="1267" height="887" alt="fact viistas salud" src="https://github.com/user-attachments/assets/3798dea0-3884-4c47-b7e9-66f56cfea955" />
<p align="center"><i>Figura 10: Estructura DDL de creación y muestra de registros de la Tabla de Hechos (fact_visitas_salud).</i></p>

### Vista materializada
Con el propósito de optimizar el rendimiento de las consultas analíticas y reducir los tiempos de procesamiento , se procedió a diseñar e implementar una **vista materializada**. A diferencia de una vista convencional, la vista materializada calcula y almacena físicamente el resultado de la consulta en el disco. Evita la necesidad de ejecutar costosas operaciones de unión (`JOIN`) entre la tabla de hechos y las múltiples dimensiones cada vez que se realiza un análisis multidimensional.

La vista materializada consolida los datos de la tabla central `fact_visitas_salud` junto con los atributos descriptivos más relevantes de las dimensiones circundantes, tales como:

* **Campos de Agrupación y Filtrado:** La especialidad (`specialty`), la ubicación (`city`), el periodo temporal (`nombre_mes`/`anio`), el género del paciente (`patient_gender`), el diagnóstico (`diagnosis_group`) y la cobertura (`insurance_type`).
* **Métricas Pre-consolidadas:** Hechos numéricos y lógicos clave como el costo total de la atención (`total_cost`) y la condición de emergencia (`is_emergency`).


<img width="1262" height="912" alt="vista materializada" src="https://github.com/user-attachments/assets/f4bc761a-3450-4c17-af01-a6de6cb57b9c" />
<p align="center"><i>Figura 11: Definición y creación de la Vista Materializada para la optimización de consultas analíticas.</i></p>

## Consultas MOLAP
### ¿Cuál es el costo total de atención por especialidad,ciudad y mes?
Se ejecutó una consulta analítica multidimensional extrayendo los datos consolidados. La consulta utiliza una función de agregación para sumar la métrica del costo total (`SUM(total_cost)`) y agrupa los resultados cruzando tres dimensiones clave: Especialidad (`specialty`), Ubicación Geográfica (`city`) y la dimensión Temporal (`nombre_mes`).

* A nivel macro, se identifica el costo total facturado por cada rama de la medicina (por ejemplo, Cardiología o Medicina General).
* Al profundizar en la granularidad, los resultados revelan el comportamiento geográfico, indicando en qué ciudades una especialidad específica genera mayores gastos.
* Finalmente, la apertura por mes permite detectar estacionalidades o picos de atención que influyen directamente en los costos operativos de la institución durante ciertos periodos del año.
<img width="878" height="892" alt="primera pregunta 1" src="https://github.com/user-attachments/assets/9e9a5809-5088-4251-baa0-19fec0752ee7" />
<p align="center"><i>Figura 12: Sentencia SQL y primeros resultados para el costo total por especialidad, ciudad y mes.</i></p>
<img width="812" height="842" alt="primera pregunta 2 de verdad" src="https://github.com/user-attachments/assets/96f60eb0-1ae6-4cfb-95bf-a4ba2bb853d9" />
<p align="center"><i>Figura 13: Vista extendida de los resultados agregados (subtotales) de la primera consulta analítica.</i></p>
<img width="817" height="847" alt="primera pregunta 2" src="https://github.com/user-attachments/assets/ee00fa03-06cb-456a-ac1f-8f741c5f1c5e" />
<p align="center"><i>Figura 14: Continuación y cierre de los registros obtenidos en la consulta analítica de costos totales.</i></p>


### ¿Qué ciudad tuvo más emergencias por mes y género?
Quito es la ciudad que aparece con mayor frecuencia liderando las emergencias en los distintos meses y géneros (destacando especialmente en febrero para el género masculino con 5 casos), mientras que ciudades como Guayaquil, Loja y Ambato lideran en meses o géneros específicos. 

*Consulta ejecutada* 
```
WITH emergencias AS (
    SELECT 
        periodo_mes,
        patient_gender,
        city,
        COUNT(*) AS total_emergencias
    FROM mv_salud_visitas
    WHERE is_emergency = TRUE
    GROUP BY 
        periodo_mes,
        patient_gender,
        city
),
ranking AS (
    SELECT 
        periodo_mes,
        patient_gender,
        city,
        total_emergencias,
        RANK() OVER (
            PARTITION BY periodo_mes, patient_gender
            ORDER BY total_emergencias DESC
        ) AS posicion
    FROM emergencias
)
SELECT 
    periodo_mes,
    patient_gender,
    city,
    total_emergencias
FROM ranking
WHERE posicion = 1
ORDER BY 
    periodo_mes,
    patient_gender;
``` 
<img width="800" height="286" alt="image" src="https://github.com/user-attachments/assets/6d4b9456-0090-4de2-a1b4-2afa876f5ee8" />
<p align="center"><i>Figura 15: Vista extendida de los resultados de la segunda consulta analítica.</i></p>


### ¿Por diagnóstico, tipo de seguro,  cuál es el costo promedio por visita y en qué ciudad es más alto?

Esta consulta devolvió 24 combinaciones, donde cáncer con seguro mixto registra el costo promedio más alto ($2.315 00) y siendo Ambato la ciudad con mayor gasto individual
($4.350,00).

La fractura con seguros tanto privado como público también destaca con costos elevados, mientras que la hipertensión y la diabetes presentan los valores más bajos, coherente con su naturaleza ambulatoria.

<img width="1102" height="868" alt="Image" src="https://github.com/user-attachments/assets/1ddd7069-5df5-49c9-a093-7ce8ccf38c4c" />
<p align="center"><i>Figura 16: Sentencia SQL para el costo promedio por diagnóstico, tipo de seguro y ciudad más alta.</i></p>

<img width="1188" height="811" alt="Image" src="https://github.com/user-attachments/assets/7ca98805-2b0d-4cff-af7c-42a062d8a2fa" />
<p align="center"><i>Figura 17: Vista extendida de los 24 resultados obtenidos para la tercera consulta analítica.</i></p>

## Referencias Bibliográficas

[1] Escuela Politécnica Nacional, "Clase 6: Business Intelligence — OLAP," material de clase, Quito, Ecuador, 2025.

[3] Escuela Politécnica Nacional, "Guía para Implementar una Vista Multidimensional de Datos en PostgreSQL," *Aulas Virtuales EPN*, 2025. [Online]. Available:
https://aulasvirtuales.epn.edu.ec/pluginfile.php/16280755/mod_resource/content/2/guia_olap_postgresql.html

[2] PostgreSQL Global Development Group, "PostgreSQL 16 Documentation," 2024.
[Online]. Available: https://www.postgresql.org/docs/current/

## Declaración de uso de IA
