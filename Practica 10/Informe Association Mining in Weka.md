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

-----------
#### **Ejercicio 10.8**
-----------
#### **Ejercicio 10.9**
-----------

#### Resultados 




















