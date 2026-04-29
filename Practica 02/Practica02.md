# Escuela Politécnica Nacional

# Business Intelligence

## Práctica 2

**Integrantes:** Doménica J. Cárdenas, Salma Morales, Danna Morales, Gabriel Del Valle, Belén Cholango

---

## Ferretería El Tornillo Feliz

### Resolución del caso de estudio

#### Creación tabla de Datos de la Ferretería 
Primero, se creó el esquema staging dentro de la base de datos Datawarehouse1 en PostgreSQL / pgAdmin. Posteriormente, se definió la tabla staging.productos_ferreteria_raw, la cual contiene los datos originales provenientes de las distintas sucursales de la ferretería. Esta tabla almacena información sin procesar, incluyendo inconsistencias en categorías, unidades de medida y formatos de precios, lo cual representa la situación del caso de estudio.

<img width="523" height="368" alt="image" src="https://github.com/user-attachments/assets/f2d72bc3-3097-4f0a-a2ee-9439802ea49c" />

#### Extracción de Datos de la Ferretería en Pentaho
Una vez tenemos esto, procedemos a ir a Pentaho para poder realizar la extracción y limpieza de estos datos.
Primero debemos crear un nuevo archivo de transformación, en donde para extraer los datos del pgAdmin usaremos un Table Input, dentro de este configuraremos y conectaremos la base de datos. Antes de esto, deberemos conectar la base de datos al archivo.  

<img width="464" height="374" alt="image" src="https://github.com/user-attachments/assets/1bd6afca-a659-444d-8651-c7d468359df4" />

Al ya estar conectada la base de datos, se empleó el componente Table Input para obtener los datos desde la tabla staging.productos_ferreteria_raw, permitiendo visualizar y trabajar con la información original dentro del flujo de transformación. 

<img width="478" height="472" alt="image" src="https://github.com/user-attachments/assets/d59f3a13-47e9-463d-b46f-5acf6e58242e" />

#### Transformación de datos 

Durante esta etapa se realizarón varias transformaciones con el objetivo de limpiar y estandarizar la información: 

1. Se utilizó el componente `Replace in String` para eliminar el simbolo `$` que estaba presente en el campo `precio_unitario`, permitiendo convertir los valores a un formato numerico limpio.

<img width="396" height="214" alt="image" src="https://github.com/user-attachments/assets/f1757d3e-4988-47d9-8c36-691f82595069" />

2. Se aplicó el componente `String Operations` para eliminar espacios en blanco innecesarios en los campos `categoria`, `unidad_medida` y `precio_unitario`, asegurando consistencia en los datos.

<img width="543" height="305" alt="image" src="https://github.com/user-attachments/assets/2f3530d5-4bc2-4124-adad-6c780eefff58" />









