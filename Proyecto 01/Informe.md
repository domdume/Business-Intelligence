# <center> **ESCUELA POLITÉCNICA NACIONAL** </center>
# <center> **Proyecto I Bimestre** </center>

**Integrantes**
* Doménica J. Cárdenas
* Danna Morales
* Salma Morales
* Belén Cholango
* Gabriel del Valle

## **Índice de Contenidos**

1. [Problema y solución](#problema-y-solución)
2. [Justificación del diseño](#justificación-del-diseño)
3. [Proceso ETL](#proceso-etl)
	- [DIM_TIENDA](#dim_tienda)
    - [DIM_FERIADO](#dim_feriado)
	- [DIM_TIEMPO](#dim_tiempo)
	- [DIM_PRODUCTO](#dim_producto)
	- [FACT_VENTAS](#fact_ventas)
	- [FACT_TRANSACCIONES](#fact_transacciones)
    - [JOB](#job)
4. [Análisis de insights clave obtenidos (OLAP)](#análisis-de-insights-clave-obtenidos-olap)
5. [Recomendaciones al negocio](#recomendaciones-al-negocio)

## Problema y solución
### Problema:

**Corporación Favorita** es una de las cadenas de supermercados más grandes del Ecuador, con presencia en múltiples provincias y ciudades del país. La corporación maneja un volumen masivo de datos operacionales generados diariamente: transacciones de clientes, ventas por producto, movimientos por tienda y fechas de operación, incluyendo feriados nacionales.

Sin embargo, esta información se encontraba dispersa en múltiples tablas de un sistema transaccional (OLTP) sin una estructura analítica unificada. Esto generaba los siguientes problemas críticos para la toma de decisiones:

- **Falta de visibilidad consolidada**: Los gerentes no contaban con una vista centralizada de los KPIs principales (ventas totales, ticket promedio, número de transacciones) en un único panel de control.
- **Imposibilidad de análisis multidimensional**: No era posible cruzar variables como ciudad, tipo de tienda, familia de productos y período de tiempo de manera eficiente desde el sistema fuente.
- **Desconocimiento del impacto de feriados**: No existía un mecanismo que permitiera relacionar los días festivos con el comportamiento de ventas y transacciones, impidiendo planificar inventario y personal.
- **Análisis geográfico limitado**: La empresa no podía visualizar con rapidez cuáles provincias y ciudades representaban la mayor concentración de ingresos ni cómo se distribuían las ventas por tipo de tienda (A, B, C, D, E).
- **Análisis de portafolio de productos deficiente**: No había forma de identificar qué familias de productos y categorías (perecederos vs. no perecederos) generaban mayor rentabilidad ni su participación porcentual en las ventas totales.

### Solución:

Se diseñó e implementó un **Data Warehouse (DWH)** bajo el modelo de **Esquema de Constelación**, utilizando **Pentaho Data Integration (PDI/Kettle)** para el proceso ETL y **Power BI** para la capa de visualización y análisis OLAP.

La solución contempla:

1. **Proceso ETL automatizado en Pentaho**: Se crearon transformaciones independientes para cada tabla dimensional y de hechos, orquestadas por un Job maestro que garantiza la carga en el orden correcto respetando las dependencias de claves sustitutas (surrogate keys).

2. **Modelo dimensional Constelación**: Se construyeron dos tablas de hechos (`FACT_VENTAS` y `FACT_TRANSACCIONES`) que comparten las dimensiones `DIM_TIEMPO` y `DIM_TIENDA`, permitiendo análisis comparativos y cruzados entre ventas y comportamiento de transacciones.

3. **Tres dashboards en Power BI**:
   - **Dashboard General**: KPIs globales (191.15M en ventas, ticket promedio de 5.26, 36M de transacciones), análisis temporal y por ciudad.
   - **Dashboard de Productos**: Análisis por familia y categoría, diferenciando productos perecederos de no perecederos.
   - **Dashboard Geográfico**: Distribución de ventas por provincia y tipo de tienda, con análisis de dispersión entre transacciones y ventas por ciudad.


## Justificación del diseño

### Modelo Constelación (Galaxy Schema)

Para este proyecto se adoptó el **Modelo de Constelación** como arquitectura del Data Warehouse. 

La corporación necesita analizar simultáneamente dos procesos diferentes: las **ventas** (monto de ingresos generados, con o sin promoción) y las **transacciones** (conteo de operaciones realizadas en caja). Ambos tienen granularidades y métricas propias, lo que justifica la existencia de dos tablas de hechos separadas:
- `FACT_VENTAS`: almacena el importe de ventas y si hubo promoción (`onpromotion`, `sales`).
- `FACT_TRANSACCIONES`: almacena el número de transacciones (`transactions`).

La integración de `FACT_VENTAS` y `FACT_TRANSACCIONES` mediante **dimensiones conformadas** (`DIM_TIEMPO` y `DIM_TIENDA`) define nuestro esquema constelación, un diseño estratégico que elimina la redundancia y garantiza la coherencia analítica. 
Al compartir estas claves, un mismo filtro de fecha o ciudad se aplica simultáneamente a ambas tablas de hechos, habilitando análisis cruzados y comparativos directos y precisos, como evaluar el volumen de transacciones frente al ticket promedio en distintas ubicaciones.

La dimensión de feriados ayuda a `DIM_TIEMPO` con un atributo `es_feriado` que permite segmentar el comportamiento de compra en días festivos versus días ordinarios, una variable estratégica para planificación de inventario y staffing.

**Diagrama del modelo dimensional implementado en Power BI:**

<img width="983" height="655" alt="image" src="https://github.com/user-attachments/assets/f4a6fac6-7e2c-41b3-9192-183e1c571f22" />


## PROCESO ETL
El proceso ETL fue implementado en **Pentaho**. 
La fuente de datos es una base de datos de staging que contiene las tablas operacionales de Corporación Favorita. Las transformaciones siguen el patrón: **leer desde staging → transformar → cargar al DWH**.

##  DIM_TIENDA

La transformación `dim_tienda` carga la dimensión de tiendas desde la tabla de staging `stores` hacia el DWH.

### Pasos:
1. **Leer stores staging**: Se conecta a la base de datos de staging y extrae todos los registros de la tabla de tiendas, incluyendo los campos `store_nbr`, `city`, `state`, `type` (tipo de tienda: A, B, C, D, E).

2. **User defined Java expression** *(User Defined Java Expression)*: Se aplica lógica de derivación de campo. Concretamente, se genera el campo `Ciudad_Ecuador` a partir del campo `city`, realizando una normalización o mapeo de nombres de ciudades al estándar ecuatoriano para consistencia en los dashboards geográficos.

3. **Select values**: Se seleccionan y renombran únicamente los campos necesarios para la dimensión (`store_nbr`, `city`, `Ciudad_Ecuador`, `state`, `region`, `cluster`, `type`), eliminando cualquier campo innecesario proveniente del staging.

4. **Add sequence** : Se genera la **clave sustituta** `sk_tienda` como un entero autoincremental. Esta clave desvincula el DWH del identificador operacional (`store_nbr`) y es la que se usará como llave foránea en las tablas de hechos.

5. **Table output** : Se insertan los registros procesados en la tabla `dwh.dim_tienda` del Data Warehouse. 

<img width="921" height="238" alt="image" src="https://github.com/user-attachments/assets/4f81fe16-b168-4186-8cd8-c0f1dfd59842" />


## DIM_FERIADO

La transformación `dim_feriado` carga la dimensión de feriados nacionales ecuatorianos desde la tabla staging `holidays`. 

### Pasos:

1. **Leer holidays staging**: Extrae los registros de la tabla de feriados desde staging, con campos como `date`, `type`, `locale`, `locale_name` y `description`.

2. **User defined Java expression**: Se deriva el campo `es_feriado` (booleano o flag) basado en el tipo y ámbito del feriado. También se pueden generar campos de contexto como `tipo_feriado` o `ambito` (Nacional, Regional, Local) para análisis segmentado.

3. **Select values**: Se seleccionan los atributos definitivos de la dimensión —`fecha`, `descripcion`, `tipo`, `locale`, `locale_name`— eliminando columnas redundantes.

4. **Add sequence**: Se genera la clave sustituta `sk_feriado` como entero secuencial para referenciar esta dimensión desde las tablas de hechos.

5. **Table output**: Se carga la dimensión procesada en la tabla `dwh.dim_feriado` del Data Warehouse.

<img width="921" height="181" alt="image" src="https://github.com/user-attachments/assets/316da9f1-d70c-47d3-b5fe-4768272e7f07" />

## DIM_TIEMPO

La transformación `dim_tiempo` es una de las más importantes del proyecto, ya que genera la dimensión de tiempo enriquecida con atributos analíticos derivados de las fechas presentes en los datos de ventas.

### Pasos

1. **Leer fechas staging**: Se leen las fechas únicas presentes en la tabla de staging de transacciones/ventas. Se obtiene el campo `date` como fecha base para construir toda la dimensión.

2. **Calculator**: Se calculan de manera automática múltiples atributos derivados de la fecha utilizando las funciones integradas del paso Calculator de Pentaho.

3. **User defined Java expression** *(User Defined Java Expression)*: Se derivan los atributos textuales que el Calculator no proporciona directamente:
   - `nombre_dia`: nombre del día en español ("Lunes", "Martes", etc.) mediante lógica condicional.
   - `nombre_mes`: nombre del mes en español ("Enero", "Febrero", etc.).
   - `es_feriado`: se cruza con la tabla de feriados para marcar si la fecha corresponde a un día festivo (join lógico o lookup).

4. **Add sequence**: Se genera la clave sustituta `sk_tiempo` como entero secuencial, que servirá de llave foránea en `FACT_VENTAS` y `FACT_TRANSACCIONES`.

5. **Cargar dim_tiempo**: Se insertan todos los registros con sus atributos derivados en la tabla `dwh.dim_tiempo` del Data Warehouse.
   
<img width="921" height="184" alt="image" src="https://github.com/user-attachments/assets/eb355ab6-e457-43da-bcca-7027eea7165a" />

## DIM_PRODUCTO

La transformación `dim_producto` carga la dimensión de productos (ítems) con sus atributos de clasificación desde la tabla de familias de productos en staging.

### Pasos

1. **Leer familias staging**: Se extrae la tabla de artículos/familias desde el staging. Los campos de origen incluyen `family` (familia de producto, ej. GROCERY I, BEVERAGES, CLEANING) y `category` (categoría), así como el indicador de perecedero.

2. **User defined Java expression**: Se genera el campo `perishable_label` como etiqueta legible del indicador de perecedero: si `perishable = 1` → `"Perecedero"`, si `perishable = 0` → `"No perecedero"`. Esta transformación enriquece la dimensión para facilitar filtros y leyendas en Power BI sin necesidad de lógica adicional en DAX.

3. **Select values**: Se seleccionan y confirman los campos finales de la dimensión: `family`, `category`, `perishable`, `perishable_label`, descartando columnas de staging no necesarias.

4. **Add sequence**: Se genera la clave sustituta `sk_producto` como entero secuencial único por registro de producto.

5. **Table output**: Se carga la dimensión en la tabla `dwh.dim_producto` del Data Warehouse.

<img width="921" height="202" alt="image" src="https://github.com/user-attachments/assets/72278e1f-1498-49d0-8836-465ca897628e" />

## FACT_VENTAS

La transformación `fact_ventas` carga la tabla de hechos de ventas integrando las claves sustitutas de las dimensiones mediante lookups.

### Pasos

1. **Leer stg_train**: Se leen los registros de la tabla `stg_train`, que contiene el historial de ventas de Corporación Favorita. Los campos clave son `date`, `store_nbr`, `item_nbr` (o `family`), `sales` y `onpromotion`.

2. **Lookup sk_tiempo**: Se consulta `dwh.dim_tiempo` para obtener `sk_tiempo` a partir de la `date` del registro de origen. Esto sustituye la fecha operacional por la clave sustituta de la dimensión de tiempo.

3. **Lookup sk_tienda**: Se consulta `dwh.dim_tienda` para obtener `sk_tienda` a partir de `store_nbr`. Esto vincula cada venta con su tienda correspondiente en el DWH.

4. **Lookup sk_producto**: Se consulta `dwh.dim_producto` para obtener `sk_producto` a partir del identificador de familia/ítem del producto. Este lookup es el tercero en cadena, garantizando que la fila de hecho tenga todas las foreign keys necesarias.

5. **Dummy (do nothing)**: Paso conector utilizado para manejar los registros que no encontraron match en alguno de los lookups (filas rechazadas). Recibe el flujo de error de los lookups y lo redirige al Filter rows.

6. **Filter rows**: Filtra y separa los registros válidos (con todas las claves encontradas) de los registros con lookups fallidos. Solo los registros con `sk_tiempo`, `sk_tienda` y `sk_producto` no nulos avanzan hacia la carga final.

7. **Select values**: Se seleccionan únicamente las columnas que conformarán la tabla de hechos: `sk_tiempo`, `sk_tienda`, `sk_producto`, `sales`, `onpromotion`, descartando los campos operacionales originales.

8. **If field value is null**: Se aplica una verificación adicional de calidad de datos: si alguna clave sustituta llegara como nulo (caso borde), se reemplaza con un valor por defecto (p. ej., `-1`, correspondiente a un registro "desconocido" en la dimensión) para mantener integridad referencial.

9. **Table output**: Se insertan los registros en la tabla `dwh.fact_ventas` del Data Warehouse, con las métricas `sales` y `onpromotion` y las tres claves foráneas. 

<img width="692" height="471" alt="image" src="https://github.com/user-attachments/assets/36c55296-d89c-4b0b-a07a-fffee8597ccf" />

## FACT_TRANSACCIONES

La transformación `fact_transacciones` carga la tabla de hechos de transacciones de caja, vinculando cada registro con sus dimensiones de tiempo y tienda.

### Pasos

1. **Leer stg_transactions**: Se leen los registros de la tabla de staging `stg_transactions`, que contiene el número de transacciones realizadas por tienda y fecha. Los campos fuente son `date`, `store_nbr` y `transactions`.

2. **Lookup sk_tiempo**: Se consulta `dwh.dim_tiempo` para reemplazar `date` por la clave sustituta `sk_tiempo`. Se utiliza la fecha como clave de búsqueda, garantizando que cada transacción quede vinculada al registro correcto de la dimensión de tiempo.

3. **Lookup sk_tienda**: Se consulta `dwh.dim_tienda` para reemplazar `store_nbr` por `sk_tienda`. De este modo, el número operacional de tienda queda sustituido por la llave sustituta del DWH.

4. **Filter rows**: Se filtran únicamente los registros donde ambas claves (`sk_tiempo` y `sk_tienda`) hayan sido encontradas exitosamente en sus respectivos lookups. Los registros huérfanos (sin match en las dimensiones) son descartados o enviados a un log de errores.

5. **Select values**: Se seleccionan los tres campos finales de la tabla de hechos: `sk_tiempo`, `sk_tienda` y `transactions`, descartando los identificadores operacionales originales.

6. **Cargar fact_transacciones**: Se insertan los registros procesados en la tabla `dwh.fact_transacciones` del Data Warehouse, completando la carga de la segunda tabla de hechos.

<img width="617" height="533" alt="image" src="https://github.com/user-attachments/assets/e90a0246-810e-496c-96df-256a56dc49e6" />

## JOB

El Job orquesta la ejecución de todas las transformaciones en el orden correcto, garantizando que las dimensiones estén completamente cargadas antes de ejecutar las tablas de hechos (que dependen de sus claves sustitutas).

### Pasos

1. **Start**: Punto de entrada del Job. Inicia la ejecución del pipeline ETL completo. Puede configurarse para ejecución manual o programada (scheduling).

2. **SQL** *(Execute SQL Script)*: Ejecuta un script SQL de preparación antes de la carga. Típicamente incluye sentencias como `TRUNCATE TABLE` sobre las tablas del DWH para limpiar cargas anteriores y garantizar idempotencia (el mismo job ejecutado múltiples veces produce el mismo resultado). También puede incluir la creación de índices o la desactivación temporal de constraints para acelerar la carga masiva.

3. **dim_tiempo**: Ejecuta la transformación de la dimensión de tiempo. Es la primera en cargarse porque es referenciada por ambas tablas de hechos. La secuencia es estricta: las dimensiones deben existir antes que los hechos.

4. **dim_tienda**: Ejecuta la transformación de la dimensión de tiendas. Se carga en segundo lugar ya que tanto `fact_ventas` como `fact_transacciones` requieren el `sk_tienda` para sus lookups.

5. **dim_producto**: Ejecuta la transformación de la dimensión de productos. Se carga en tercer lugar porque solo es requerida por `fact_ventas` (no por `fact_transacciones`).

6. **dim_feriado**: Ejecuta la transformación de la dimensión de feriados. Se carga en cuarto lugar. Aunque en el modelo de Power BI el atributo `es_feriado` está integrado en `dim_tiempo`, esta dimensión puede ser utilizada para enriquecer análisis históricos o como tabla de referencia de calendarios fiscales.

7. **fact_ventas** *(Transformation)*: Ejecuta la transformación de la tabla de hechos de ventas. En este punto todas las dimensiones requeridas (`dim_tiempo`, `dim_tienda`, `dim_producto`) ya están cargadas, por lo que los lookups de claves sustitutas resolverán correctamente.

8. **fact_transacciones**: Ejecuta la transformación de la tabla de hechos de transacciones. Es la última transformación en el pipeline, ya que depende de `dim_tiempo` y `dim_tienda` para sus lookups.

9. **Success**: Marca la finalización exitosa del Job. Puede configurarse para enviar notificaciones por correo o activar pipelines de actualización en Power BI Service (vía API o Gateway).

<img width="921" height="640" alt="image" src="https://github.com/user-attachments/assets/2d8b14ad-e301-4b0f-b243-4d2663583eb6" />

## Análisis de insights clave obtenidos (OLAP)

### Dashboard General

El **Dashboard General** presenta los KPIs corporativos de más alto nivel para Corporación Favorita en el período 2013–2014:

| KPI | Valor |
|-----|-------|
| Ventas Totales | **$191.15 millones** |
| Ticket Promedio | **$5.26** |
| Total Transacciones | **36 millones** |

**Análisis temporal**: Se observa una **tendencia descendente en ventas** entre 2013 y 2014, pasando de aproximadamente $140M a $50M en el gráfico de líneas. Este comportamiento puede estar asociado a factores macroeconómicos del Ecuador en ese período (variación del precio del petróleo, reformas tributarias) o a efectos estacionales específicos de los meses seleccionados.

**Análisis por ciudad**: **Quito** lidera ampliamente las ventas totales con valores superiores a $100M, seguida de **Guayaquil** con aproximadamente $30M. Las ciudades medianas (Ambato, Cuenca, Santo Domingo) se ubican entre $5M y $15M. Esto refleja la alta concentración de la actividad comercial en las dos principales urbes del país.

**Análisis por familia de productos**: **GROCERY I** es la familia de mayor volumen de ventas, seguida por **BEVERAGES** y **CLEANING**. Las familias de productos frescos (DAIRY, MEATS, PRODUCE) tienen ventas relevantes, siendo consistentes con la naturaleza de un supermercado de consumo masivo.

---

### Dashboard de Productos

**Por familia**: El mapa de árbol (*treemap*) confirma que **GROCERY I** y **BEVERAGES** dominan el portafolio, concentrando la mayor área visual. Familias como BREAD/BAKERY, MEATS y PRODUCE tienen participaciones intermedias, mientras que categorías especializadas (DELI, LIQUOR/WINE, FROZEN FOODS) tienen menor representación.

**Por tipo de producto (perecedero vs. no perecedero)**:
- **Alimentos básicos (no perecedero)**: 40.2%
- **Frescos y perecederos**: 21.33%
- **Bebidas**: 17.72%
- **Cuidado y limpieza**: 14.68%
- **Hogar y electrodomésticos**: 0.11%
- **Alimentos básicos perecederos**: 5.73%

Este análisis revela que el **60% de las ventas proviene de productos no perecederos**, lo que tiene implicaciones directas en la gestión de inventario y cadena de frío.

---

### Dashboard Geográfico

El análisis geográfico desagrega las ventas a nivel de provincia y tipo de tienda. 
**Por provincia**: **Pichincha** es la provincia líder con **$105.7M** en ventas totales, representando más del 55% del total corporativo. **Guayas** es la segunda con **$29.4M**. Las provincias de la Sierra (Azuay, Tungurahua, Imbabura) tienen participaciones intermedias. Provincias amazónicas y del litoral sur presentan los menores volúmenes.

**Por tipo de tienda**: Las tiendas **tipo A y D** concentran los mayores volúmenes de ventas, superando los $60M cada una. Las tiendas **tipo C** (~$30M), **tipo B** (~$25M) y **tipo E** (~$8M) muestran volúmenes decrecientes. Esto sugiere que los formatos A y D corresponden a hipermercados o supermercados grandes, mientras que B y E serían tiendas de proximidad o express.

**Dispersión Transacciones vs. Ventas por ciudad**: El gráfico de dispersión muestra que la mayoría de ciudades se agrupan en el cuadrante de bajas transacciones y bajas ventas. Solo Quito se destaca con una posición muy superior (~15M de transacciones), mientras que Guayaquil aparece en una posición intermedia. 

---

## Recomendaciones al negocio

- Dado que Pichincha concentra más del 55% de las ventas, se recomienda evaluar la saturación del mercado capitalino y priorizar la expansión en provincias con alto potencial subatendido: **Manabí** ($2M), **Bolivar** ($2.4M) y **Imbabura** ($2.3M) muestran ventas relativamente bajas a pesar de ser provincias con poblaciones considerables.

- La categoría de frescos y perecederos representa el 21.33% de ventas pero implica los mayores costos de gestión (cadena de frío, merma, fechas de vencimiento). Se recomienda implementar un modelo predictivo de demanda basado en la dimensión de tiempo del DWH (considerando feriados, estacionalidad mensual y trimestral) para reducir el desperdicio de perecederos en tiendas tipo B y E.
- Se recomienda construir un reporte de feriados vs. variación de ventas para identificar qué categorías de productos muestran mayor incremento de demanda en fechas clave (Navidad, Carnaval, feriados nacionales) y así adelantar el abastecimiento correspondiente.

