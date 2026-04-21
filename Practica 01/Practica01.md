# Escuela Politécnica Nacional

# Business Intelligence

## Práctica 1

**Integrantes:** Doménica J. Cárdenas, Salma Morales, Danna Morales, Gabriel Del Valle, Belén Cholango

---

## Ejemplo 1

Descripción: Data Grid y transformación Split fields
Para iniciar el flujo, se utilizó el componente **Data Grid**, el cual permite generar datos estáticos dentro de la misma transformación sin depender de fuentes externas.
<img width="403" height="194" alt="image" src="https://github.com/user-attachments/assets/f7bbc3aa-3dfa-49f6-a6d1-209068ab7edd" />

Se definió un único campo de entrada de tipo cadena:
* **Campo:** `datos_combinados`
* **Tipo:** `String`
<img width="654" height="188" alt="image" src="https://github.com/user-attachments/assets/90180497-83a5-4c30-8c48-3ae160a57d11" />

Se cargaron filas de prueba siguiendo el formato `Nombre,Apellido,Edad`, utilizando la coma (`,`) como delimitador interno:
1. `Juan,Perez,25`
2. `Maria,Lopez,30`
3. `Carlos,Ruiz,22`
<img width="658" height="183" alt="image" src="https://github.com/user-attachments/assets/a4e22440-3a8c-4de9-9c10-69abd40b6299" />

Una vez obtenidos los datos, se aplicó la transformación **Split fields** para separar la cadena original en columnas estructuradas.
* **Campo a dividir:** `datos_combinados`
* **Delimitador:** `,` (coma)
  
<img width="479" height="433" alt="image" src="https://github.com/user-attachments/assets/0df70732-5069-4fbc-9072-0f25a907b72a" />

Se mapearon los fragmentos de la cadena a los siguientes campos de salida:
* **Nombre:** String
* **Apellido:** String
* **Edad:** Integer (Asegurando que no existan caracteres no numéricos para evitar errores de conversión).
  
<img width="649" height="244" alt="image" src="https://github.com/user-attachments/assets/2e959219-a44f-4ccc-8396-b45b45ceca74" />

Resultados :
Para finalizar el proceso, los datos transformados se enviaron a un componente **Microsoft Excel writer**. La transformación se ejecutó exitosamente, como se observa en el panel de **Logging**, donde no se reportaron errores y se confirmó el procesamiento de las 3 filas iniciales.

<img width="428" height="370" alt="image" src="https://github.com/user-attachments/assets/7f3b218f-4b78-4801-ba86-8611e96febaa" />

El archivo de salida generado muestra los datos perfectamente organizados en columnas independientes:
* Columna A: **Nombre**
* Columna B: **Apellido**
* Columna C: **Edad**
  
<img width="503" height="271" alt="image" src="https://github.com/user-attachments/assets/4bb5eb97-2885-4262-bc46-3e2fff3ea7a5" />

---

## Ejemplo 2

Descripción: Json Input, Select Values, Sort Rows y Json out
 
Se seleccionó el componente **Json Input**. 
<img width="435" height="157" alt="image" src="https://github.com/user-attachments/assets/06229da5-bb49-48df-a053-0b5528cf510a" />

Para los datos, se ha descargado datoos de prueba de una pagina y guardado en un archivo `.json` llamado DatosJson.  
1. Se seleccionó browse, para buscar el archivo de prueba. 
2. Se añadió el archivo DatosJson. 

<img width="500" height="272" alt="image" src="https://github.com/user-attachments/assets/c605284f-a48a-447e-a06b-efbc22d87c28" />

Se cargaron todas las columnas de los datos del json utilizando el select field 

<img width="705" height="309" alt="image" src="https://github.com/user-attachments/assets/e2647c1f-f195-43f4-a820-111054fffc13" />

Lo que se hara a continuación es transformar esos datos en información, eliminando las columnas de la ubicación geográfica exacta, ordenar por nombre de la compania, con el objetivo de ordenar y cargar esa información en una tabla.

<img width="642" height="102" alt="image" src="https://github.com/user-attachments/assets/43e2eab6-4436-411a-9a5d-4ce4cce97b54" />

En **Select values**  

1. Seleccionar remove
2. Escribimos las columnas que queremos eliminar, en este caso lat, lng, zipecode, bs y catchPhrase. 

<img width="395" height="159" alt="image" src="https://github.com/user-attachments/assets/70692b3c-5ee2-48d9-b8c9-3c4a8d5417a1" />

**Sort Rows** 
Para ordenar por companias seleccionamos en la fieldname a `company.name` y ponemos `Y` en Ascending. 

<img width="622" height="292" alt="image" src="https://github.com/user-attachments/assets/23b79581-b584-49ce-bd83-9d4ca54fa0e4" />

**Resultados:**

Para finalizar con el proceso, los datos analizados se mandaron a un componente llamado **Json out**, donde agregamos que la información nos 
aparezca en un bloque llamado data donde agregaremos 10 usuarios. 

<img width="536" height="200" alt="image" src="https://github.com/user-attachments/assets/a7e4a6bb-bac7-483f-b5ab-b01ed3eb17f4" />

además en la pestaña de fields, debemos de seleccionar todas las columnas del json que queremos, en este caso se selecciono todas las columnas que ya se procesaron, como se observa se ha eliminado la columna de geo y el resultado mostrata los usuarios ordenados alfabeticamente por el nombre de la compania. 

<img width="265" height="110" alt="image" src="https://github.com/user-attachments/assets/d44b1adb-8914-4588-9bd2-a5a348bc0db7" />

Ahora podemos observar como se ordenó los usuarios por orden alfabético mediante el nombre de la compania. 

Esto es importante cuando debemos de presnetar datos ordenados en orden alfabético y más a futuro podemos agrupar por companias, ver cuantos usuarios hay por cada una, etc. 

<img width="1481" height="342" alt="image" src="https://github.com/user-attachments/assets/6eeedb2f-5bc8-4d20-950a-74117af21fe5" />


---

## Ejemplo 3

Descripción:

Resultados:

---

## Ejemplo 4

### Descripción: Uso de Input "CSV File Input", Transformación "String Operations" y Output "Text File Output"

#### 1. Entrada de Datos (CSV file input)
Se configuró la extracción de los datos del archivo. Se definió la coma (`,`) como delimitador y se utilizaron comillas dobles (`"`) como calificador de texto (Enclosure) para evitar conflictos con los paréntesis y comas de la columna RGB.

<img width="1337" height="721" alt="Image" src="https://github.com/user-attachments/assets/e1610eaf-4889-4f6a-93a3-ef39204a2b7e" />

Se utilizó el botón **Get Fields** para mapear automáticamente las columnas `Name`, `HEX` y `RGB`.

<img width="850" height="564" alt="Image" src="https://github.com/user-attachments/assets/07f0bc1c-51c5-4264-aa73-ec8fdb2ba327" />

#### 2. Transformación (String operations)
Se añadió el componente **String operations**. Se configuró específicamente el campo `Name` para que todos los registros se conviertan a **Upper case** y se aplicó un **Trim type: both** para eliminar cualquier espacio en blanco accidental al inicio o final de las cadenas.

<img width="1318" height="280" alt="Image" src="https://github.com/user-attachments/assets/0d0de99f-e75a-482a-a1ee-f6a080c4555f" />

#### 3. Previsualización de Datos (Preview)
Antes de procesar la carga final, se ejecutó una vista previa mediante el botón **Preview rows** en el nodo de transformación. Esto permitió validar que los nombres de los colores cambiaron exitosamente a mayúsculas (ej. "White" a "WHITE") sin alterar los códigos hexadecimales.

<img width="978" height="593" alt="Image" src="https://github.com/user-attachments/assets/51bb9f66-7ed8-4641-8819-1eea79c6a108" />

#### 4. Salida de Datos (Text file output)
Se conectó el flujo a un componente de salida para generar el archivo final procesado. Se definió el nombre del archivo de salida y la ubicación haciendo clic en **Browse**.

<img width="1091" height="574" alt="Image" src="https://github.com/user-attachments/assets/60e97a89-91e3-49b7-af82-9256fa7063a4" />

En la pestaña **Content** se aseguró que la codificación fuera **UTF-8** en Encoding.

<img width="1093" height="572" alt="Image" src="https://github.com/user-attachments/assets/0263aa6a-a41d-446a-9e40-a17a23db5d53" />

En la pestaña **Fields** se hizo clic en **Get Fields** para confirmar las columnas de salida.

<img width="1079" height="563" alt="Image" src="https://github.com/user-attachments/assets/3009aae5-1e72-4735-acb5-0650d508f70a" />

### Resultados:

El proceso finalizó exitosamente, mostrando los indicadores visuales (checks verdes) en todos los pasos del flujo de trabajo dentro de Spoon.

<img width="769" height="801" alt="Image" src="https://github.com/user-attachments/assets/b04f5658-29c1-4f55-a950-4e6335fe49f2" />


El resultado del archivo procesado en comparación con el original permite observar la correcta transformación de los datos a mayúsculas:

<img width="734" height="794" alt="Image" src="https://github.com/user-attachments/assets/211b04d0-588a-4801-ad8e-55f8f5da30d8" />

---

## Ejemplo 5

Descripción:

Resultados :

