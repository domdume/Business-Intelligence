# Escuela Politécnica Nacional

# Business Intelligence

## Práctica 1

**Integrantes:** Doménica J. Cárdenas, Salma Morales, Danna Morales, Gabriel Del Valle, Belén Cholango

---

## Ejemplo 1

Descripción:

Resultados :

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

### Descripción: Uso de Input "CSV File Input", Transformación "String Operations" y Output "Text File Output"

#### 1. Entrada de Datos (CSV file input)
Se configuró la extracción de los datos del archivo. Se definió la coma (`,`) como delimitador y se utilizaron comillas dobles (`"`) como calificador de texto (Enclosure) para evitar conflictos con los paréntesis y comas de la columna RGB.

<img width="100%" src="https://github.com/user-attachments/assets/e1167563-442b-4f8a-8364-1006adff22b9" alt="Configuracion Input 1" />

Se utilizó el botón **Get Fields** para mapear automáticamente las columnas `Name`, `HEX` y `RGB`.

<img width="100%" src="https://github.com/user-attachments/assets/68681770-17dd-4528-9f06-5d5a9ae7f822" alt="Configuracion Input 2" />

#### 2. Transformación (String operations)
Se añadió el componente **String operations**. Se configuró específicamente el campo `Name` para que todos los registros se conviertan a **Upper case** y se aplicó un **Trim type: both** para eliminar cualquier espacio en blanco accidental al inicio o final de las cadenas.

<img width="100%" src="https://github.com/user-attachments/assets/f6fbf5a9-17f8-4e2b-a343-e4ea121781b2" alt="Transformacion" />

#### 3. Previsualización de Datos (Preview)
Antes de procesar la carga final, se ejecutó una vista previa mediante el botón **Preview rows** en el nodo de transformación. Esto permitió validar que los nombres de los colores cambiaron exitosamente a mayúsculas (ej. "White" a "WHITE") sin alterar los códigos hexadecimales.

<img width="100%" src="https://github.com/user-attachments/assets/a9ea2033-babb-49b0-b4e1-bcddcb11c9a1" alt="Preview datos" />

#### 4. Salida de Datos (Text file output)
Se conectó el flujo a un componente de salida para generar el archivo final procesado. Se definió el nombre del archivo de salida y la ubicación haciendo clic en **Browse**.

<img width="100%" src="https://github.com/user-attachments/assets/e66c97f2-fbc4-48e8-b4cc-7c426ff4d29c" alt="Configuracion Output 1" />

En la pestaña **Content** se aseguró que la codificación fuera **UTF-8** en Encoding.

<img width="100%" src="https://github.com/user-attachments/assets/cf2388dc-0a08-4afd-884d-fdfb338fe543" alt="Configuracion Output 2" />

En la pestaña **Fields** se hizo clic en **Get Fields** para confirmar las columnas de salida.

<img width="100%" src="https://github.com/user-attachments/assets/4728a9fc-8d47-464c-8dbe-a63172d7311a" alt="Configuracion Output 3" />

### Resultados:

El proceso finalizó exitosamente, mostrando los indicadores visuales (checks verdes) en todos los pasos del flujo de trabajo dentro de Spoon.

<img width="100%" src="https://github.com/user-attachments/assets/fca29cd2-2250-4922-814d-7b3d07f3f618" alt="Resultado 1" />

El resultado del archivo procesado en comparación con el original permite observar la correcta transformación de los datos a mayúsculas:

<img width="100%" src="https://github.com/user-attachments/assets/7380ac9d-5874-4ce1-9344-30d2dc84b38b" alt="Resultado 2" />

---

## Ejemplo 5

Descripción:

Resultados :

