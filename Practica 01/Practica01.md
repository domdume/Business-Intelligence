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

Descripción:

Resultados:

---

## Ejemplo 3

Descripción: 

Resultados:

---

## Ejemplo 4

Descripción:

Resultados :

---

## Ejemplo 5

Descripción:

Resultados :

