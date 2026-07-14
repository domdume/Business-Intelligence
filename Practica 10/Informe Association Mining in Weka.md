# <center> **ESCUELA POLITÉCNICA NACIONAL** </center>
# <center> **Business Intelligence** </center>
# <center> **Practica 10** </center>

**Integrantes**
* Doménica J. Cárdenas
* Danna Morales
* Salma Morales
* Belén Cholango
* Gabriel Del Valle

### Introducción
El presente informe documenta el proceso de aplicación de algoritmos de minería de asociación utilizando la herramienta Weka, un software ampliamente reconocido en el ámbito académico y profesional por su facilidad de uso y su amplia gama de algoritmos de aprendizaje automático.
El trabajo se centra en la implementación práctica de los conceptos teóricos presentados en el Capítulo 10 del libro "Data Mining and Data Warehousing", específicamente en los ejercicios 10.6, 10.7, 10.8 y 10.9, los cuales abordan diferentes escenarios y niveles de complejidad en la minería de asociación.

### Desarrollo
#### **Ejercicio 10.6**

Primero empezamos creando el Dataset dentro de Excel.

<img width="592" height="197" alt="image" src="https://github.com/user-attachments/assets/f7f656ec-45f8-4c13-817a-65f7612b5a8d" />

Luego se guarda como archivo CSV con el nombre de DailyItem Dataset.

<img width="702" height="202" alt="image" src="https://github.com/user-attachments/assets/536c0467-54d1-460c-9387-6aa30d1f0715" />

Una vez tengamos esto, procedemos a ejecutar el Algoritmo Apriori en Weka.
Para esto, se abre la interfaz gráfica de Weka y se accede al módulo "Explorer". 

<img width="598" height="418" alt="image" src="https://github.com/user-attachments/assets/8f8f6f7f-da32-4565-a885-8e47ffd65979" />

Dentro de la pestaña "Preprocess", se utiliza el botón "Open file" para localizar y cargar el archivo CSV previamente guardado. Una vez cargado, la plataforma muestra todos los atributos que componen el conjunto de datos.

<img width="1261" height="937" alt="image" src="https://github.com/user-attachments/assets/483394d7-fb80-4719-8d20-9f2dc39a81e3" />

Dado que el algoritmo Apriori requiere datos de tipo nominal, se aplica un filtro de transformación. Para ello, se selecciona la opción "Choose" y se navega por la ruta: filters → unsupervised → Numeric to Nominal. Tras seleccionar este filtro, se hace clic en "Apply" para ejecutar la conversión sobre todas las columnas del conjunto de datos.

<img width="627" height="143" alt="image" src="https://github.com/user-attachments/assets/d1ab31fe-e102-4402-9a62-78c7d5bf8e19" />

Debido a que el atributo "Transaction" no aporta información relevante para el análisis de asociación, se procede a su eliminación. Esto se realiza seleccionándolo en el panel izquierdo y presionando el botón "Remove".

<img width="643" height="587" alt="image" src="https://github.com/user-attachments/assets/787dc6d9-1aad-438b-b64c-b9b8d3295885" />

Se cambia a la pestaña "Associate" y se elige el algoritmo Apriori desde el menú desplegable. A continuación, se hace clic en el campo del algoritmo para abrir el Editor Genérico de Objetos, donde se establecen varios parámetros, los cuales hay que configurarlos. 

<img width="1261" height="868" alt="image" src="https://github.com/user-attachments/assets/d6de866f-7a44-4212-a967-b2fa0450e006" />

Una vez configurados estos valores, se confirma la operación presionando "OK".

<img width="1250" height="873" alt="image" src="https://github.com/user-attachments/assets/1d47a3f6-c25a-4aba-b5d3-cbfa4b1a5475" />

Se inicia el proceso haciendo clic en el botón "Start". Weka procesa los datos y muestra los resultados en el panel derecho, correspondiente a la salida del asociador.

<img width="545" height="162" alt="image" src="https://github.com/user-attachments/assets/1233cd4f-22ce-4f9d-8c93-47024ba6a427" />

Finalmente, se analizan las reglas de asociación generadas, identificando aquellas con mayor relevancia según los umbrales establecidos.

<img width="1533" height="867" alt="image" src="https://github.com/user-attachments/assets/95f76158-ecea-453e-b2df-132ffa404b00" />

**Análisis**
La regla Jam (**Cornflake**) resulta ser la más relevante dentro del conjunto de datos analizado, con una confianza del 100% y un soporte del 50%. Esto significa que, en este pequeño conjunto de transacciones, todos los clientes que compraron mermelada también compraron cornflakes, lo cual representa un patrón de compra claramente identificable.

-----------
#### **Ejercicio 10.7**
Primero empezamos creando el Dataset dentro de Excel y se tabulan los datos.

<img width="772" height="197" alt="image" src="https://github.com/user-attachments/assets/aba3e729-9dff-45e0-9d2b-2a0922198feb" />

Luego se guarda como archivo CSV con el nombre de DailyItem2 Dataset.

<img width="931" height="193" alt="image" src="https://github.com/user-attachments/assets/ad2f09f6-b323-4161-b4b7-5e8ba8c4d1d0" />

Desde la interfaz principal de Weka, se ingresa al módulo "Explorer" y, en la pestaña "Preprocess", se emplea el botón "Open file" para seleccionar y cargar el archivo CSV recién creado. Una vez cargado, la herramienta muestra la lista completa de atributos presentes.

<img width="597" height="417" alt="image" src="https://github.com/user-attachments/assets/19c03a35-c950-4618-96d8-2b3662e771d3" />

<img width="1262" height="938" alt="image" src="https://github.com/user-attachments/assets/497bcecb-6707-4b78-9622-768ed9547022" />

Debido a que el algoritmo Apriori no opera directamente con valores numéricos, se aplica un filtro de conversión. Se hace clic en "Choose" y se sigue la ruta: filters → unsupervised → Numeric to Nominal. Luego, se presiona "Apply" para efectuar la transformación sobre todas las variables del conjunto.

<img width="1252" height="767" alt="image" src="https://github.com/user-attachments/assets/b513dae7-c142-46b6-b296-263138419bed" />

El campo "Transaction" se elimina del análisis, ya que no representa un elemento de interés para la minería de asociaciones. Para ello, se selecciona en el panel izquierdo y se pulsa el botón "Remove".

<img width="631" height="567" alt="image" src="https://github.com/user-attachments/assets/156c0e60-c743-4ac2-a76f-f696fd66a0d4" />

En la pestaña "Associate", se selecciona el algoritmo Apriori desde el menú correspondiente. Al hacer clic sobre el nombre del algoritmo, se abre el Editor Genérico de Objetos, donde se configuran los valores y se confirma haciendo clic en "OK".

<img width="937" height="872" alt="image" src="https://github.com/user-attachments/assets/063fb3e9-6b60-4ab6-a3e5-9daf02d7c2c3" />

Se activa el algoritmo presionando el botón "Start". Weka procesa los datos y muestra en el panel de salida las reglas de asociación generadas conforme a los parámetros establecidos.

<img width="1251" height="868" alt="image" src="https://github.com/user-attachments/assets/8dba7292-f3da-48b6-8e28-f51afb58f06a" />

Se examinan las reglas generadas, verificando que coinciden con las obtenidas en el capítulo anterior mediante la aplicación manual del algoritmo Apriori. Se destaca la presencia de reglas como Pan → Mermelada y Cornflakes → Mermelada, entre otras, todas con niveles de confianza iguales o superiores al 75%.

**Análisis**
Los resultados obtenidos tras ejecutar el algoritmo Apriori sobre el conjunto de datos DailyItem Dataset permitieron identificar cuatro reglas de asociación principales: Pan → Mermelada, Mermelada → Pan, Cornflakes → Mermelada y Mermelada → Cornflakes. La confianza de cada regla se calcula dividiendo el soporte conjunto de ambos productos entre el soporte del producto que aparece en el lado izquierdo de la regla, obteniéndose valores del 75% para tres de ellas (Pan → Mermelada, Mermelada → Pan y Mermelada → Cornflakes) y un 100% para la regla Cornflakes → Mermelada. Dado que todas superan el umbral mínimo de confianza establecido (75%), son consideradas reglas válidas.

-----------
#### **Ejercicio 10.8**

Inicialmente, se construyó el conjunto de datos DailyItem_Marks_Dataset en formato CSV a partir de los registros de calificaciones. Tras cargar el archivo en el entorno Explorer de Weka (pestaña Preprocess), se procedió a eliminar las variables identificadoras que no aportan valor predictivo para las reglas de asociación. Específicamente, se eliminaron los atributos "Roll No" y "Name", conservando únicamente las variables numéricas correspondientes a las notas y la variable categórica "Grade" (como se observa en la primera y segunda imagen de referencia).
<img width="975" height="717" alt="image" src="https://github.com/user-attachments/assets/77b73846-2f2e-4fef-92e3-bed49f50e35a" />
<img width="797" height="398" alt="image" src="https://github.com/user-attachments/assets/b15d396d-33eb-442e-ada8-6dec5a7eb514" />

##### Proceso de Discretización
Dado que los algoritmos de asociación como Apriori requieren que todos los datos sean nominales (categóricos) y no continuos, fue necesario transformar las calificaciones numéricas.

Para ello, se aplicó el filtro no supervisado Discretize (ruta: weka.filters.unsupervised.attribute.Discretize). Se configuró el filtro a través del Generic Object Editor con los siguientes parámetros clave:

<img width="975" height="913" alt="image" src="https://github.com/user-attachments/assets/abe96821-211c-4dd1-8b87-758e2d920109" />

- bins = 3: Para dividir las calificaciones numéricas en tres categorías (que pueden interpretarse como bajo, medio y alto).

- useEqualFrequency = True: Para garantizar que cada categoría contenga aproximadamente la misma cantidad de estudiantes (un tercio del total por rango), evitando sesgos hacia un grupo específico.

<img width="751" height="956" alt="image" src="https://github.com/user-attachments/assets/89ecb488-ea49-4807-9c0a-ef4194885727" />

Al aplicar el filtro, Weka transformó con éxito los valores continuos en rangos. Por ejemplo, la variable MST(20.0) quedó dividida en los siguientes intervalos nominales: (-inf-12.5], (12.5-16.5] y (16.5-inf).

<img width="975" height="506" alt="image" src="https://github.com/user-attachments/assets/d94acb59-21c2-456a-b693-b6abe159d332" />

Con los datos discretizados, se procedió a la pestaña Associate para generar las reglas de asociación. Se utilizó el algoritmo Apriori con su configuración por defecto.

<img width="975" height="407" alt="image" src="https://github.com/user-attachments/assets/f1ca8c89-977b-4193-844d-41827d057847" />


El algoritmo generó un modelo basado en el conjunto de entrenamiento completo, identificando patrones con alta consistencia. Todas las reglas del "Top 10" devueltas por Weka presentan una métrica de confianza (conf) de 1 (100%), lo que indica una asociación determinista dentro de este conjunto de datos.

A continuación, se interpretan las principales asociaciones encontradas:

- Regla 1 y Regla 2 (Asociación Fuerte Bidireccional):

Quiz(15)='(-inf-5.25]' 11 ==> MST(20.0)='(-inf-12.5]' 11

MST(20.0)='(-inf-12.5]' 11 ==> Quiz(15)='(-inf-5.25]' 11

Interpretación: Existe una correspondencia directa en el rendimiento bajo. Los 11 estudiantes que obtuvieron una calificación baja en el Quiz (5.25 o menos) también obtuvieron una calificación baja en el examen parcial MST (12.5 o menos), y viceversa.

- Regla 4 y Regla 5 (Correspondencia de Rendimiento Alto):

Total(100.0)='(66.25-inf)' 10 ==> MST(20.0)='(16.5-inf)' 10

MST(20.0)='(16.5-inf)' 10 ==> Total(100.0)='(66.25-inf)' 10

Interpretación: Existe una relación perfecta entre obtener una alta calificación total y un alto rendimiento en el parcial. Los 10 estudiantes que alcanzaron un puntaje total alto (mayor a 66.25) también obtuvieron una nota alta en su examen MST (mayor a 16.5), y viceversa.

- Regla 9 (Asociación de Múltiples Condiciones):

Quiz(15)='(-inf-5.25]' ENDSEM(45.0)='(-inf-18.5]' 10 ==> MST(20.0)='(-inf-12.5]' 10

Interpretación: Si un estudiante presenta un bajo rendimiento combinado en el Quiz (menor o igual a 5.25) y en el examen final ENDSEM (menor o igual a 18.5), se asocia indefectiblemente a un rendimiento bajo en el parcial MST (menor o igual a 12.5).

En general, las reglas extraídas por el algoritmo demuestran que el rendimiento académico de los estudiantes analizados es altamente consistente a lo largo del periodo; es decir, las calificaciones bajas en componentes específicos (como el Quiz o el MST) son fuertes predictores de calificaciones bajas en otras evaluaciones o en el total acumulado, de la misma forma que ocurre con las calificaciones altas.

-----------
#### **Ejercicio 10.9**

Detalles iniciales del archivo:

- Contiene las columnas: MST(20.0), Quiz (15), Lab(20.0), y ENDSEM(45.0).
- Datos ordenados: Los registros de la columna MST se encuentran ordenados de mayor a menor.

1. Primero empezamos creando el Dataset dentro de Excel. En total 60 registros.

<img width="535" height="661" alt="image" src="https://github.com/user-attachments/assets/719df5c3-e886-4556-99f9-8622dcd6be8b" />

2. Reemplazar los primeros 12 registros de la columna MST (filas 2 a 13) por la letra H. (20%)

<img width="570" height="331" alt="image" src="https://github.com/user-attachments/assets/10805809-b30a-40a8-87ca-4162f9964d84" />

3. Reemplace los últimos 12 registros (filas 50 a 61) por la letra L. (20%)

<img width="552" height="293" alt="image" src="https://github.com/user-attachments/assets/aa6ec915-32fe-464a-9c80-a67961f91dd5" />

4. Reemplace los 36 registros restantes por la letra M. (60%)

<img width="572" height="312" alt="image" src="https://github.com/user-attachments/assets/071c9020-ca60-4219-a0be-d99be5357033" />

Problema: Se tiene dos estudiantes con la misma nota exacta (16.5), pero uno tiene H y el otro M. Esto es un error en minería de datos porque el valor numérico no puede pertenecer a dos clases distintas al mismo tiempo. Como el corte original fue en la fila 13, y la fila 14 repite el mismo valor, la regla obliga a desplazar el corte hacia abajo para incluir a todos los que tengan 16.5 en el grupo superior.

5. Corregir cortes de acuerdo a la regla de minería de datos.
- Cambiar el valor de la celda A14 de M a H. Ahora se tendrá 13 registros con H en total (del registro 2 al 14).

<img width="292" height="346" alt="image" src="https://github.com/user-attachments/assets/6163332f-d2a6-42f2-9283-d59ed0bda1d5" />

- Cambiar las celdas A50 y A51 de L a M. De esta forma, el grupo L comenzará recién en la fila 52 (donde la nota de MST baja a 10.5), quedándote exactamente 10 registros con L (de la fila 52 a la 61).

<img width="407" height="247" alt="image" src="https://github.com/user-attachments/assets/52ee86ab-ad1b-4974-979a-9a969824fd18" />

Repetir desde el paso 2 al 5 para las siguientes columnas. De este modo se obtendrá una tabla con valores nominales:

<img width="725" height="661" alt="image" src="https://github.com/user-attachments/assets/ac79734a-af5f-4b2b-8f88-4ed3b4b68dc8" />





-----------

#### Resultados 




















