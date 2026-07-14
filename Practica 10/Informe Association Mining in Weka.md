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

En la pestaña "Associate", se selecciona el algoritmo Apriori desde el menú correspondiente. Al hacer clic sobre el nombre del algoritmo, se abre el Editor Genérico de Objetos, donde se configuran los valores y se confirma haciendo clic en "OK"..
<img width="937" height="872" alt="image" src="https://github.com/user-attachments/assets/063fb3e9-6b60-4ab6-a3e5-9daf02d7c2c3" />

Se activa el algoritmo presionando el botón "Start". Weka procesa los datos y muestra en el panel de salida las reglas de asociación generadas conforme a los parámetros establecidos.
<img width="1251" height="868" alt="image" src="https://github.com/user-attachments/assets/8dba7292-f3da-48b6-8e28-f51afb58f06a" />

Se examinan las reglas generadas, verificando que coinciden con las obtenidas en el capítulo anterior mediante la aplicación manual del algoritmo Apriori. Se destaca la presencia de reglas como Pan → Mermelada y Cornflakes → Mermelada, entre otras, todas con niveles de confianza iguales o superiores al 75%.

**Análisis**
Los resultados obtenidos tras ejecutar el algoritmo Apriori sobre el conjunto de datos DailyItem Dataset permitieron identificar cuatro reglas de asociación principales: Pan → Mermelada, Mermelada → Pan, Cornflakes → Mermelada y Mermelada → Cornflakes. La confianza de cada regla se calcula dividiendo el soporte conjunto de ambos productos entre el soporte del producto que aparece en el lado izquierdo de la regla, obteniéndose valores del 75% para tres de ellas (Pan → Mermelada, Mermelada → Pan y Mermelada → Cornflakes) y un 100% para la regla Cornflakes → Mermelada. Dado que todas superan el umbral mínimo de confianza establecido (75%), son consideradas reglas válidas.

-----------
#### **Ejercicio 10.8**
-----------
#### **Ejercicio 10.9**

1. Primero empezamos creando el Dataset dentro de Excel. En total 60 registros.

<img width="515" height="702" alt="image" src="https://github.com/user-attachments/assets/c0d56cb5-1304-49c8-994a-b32871fd735f" />

2. Reemplazar los primeros 12 registros de la columna MST (filas 2 a 13) por la letra H.

3. Reemplace los últimos 12 registros (filas 50 a 61) por la letra L.

4. Reemplace los 36 registros restantes por la letra M.
-----------

#### Resultados 




















