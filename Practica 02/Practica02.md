# Escuela Politécnica Nacional

# Business Intelligence

## Práctica 2

**Integrantes:** Doménica J. Cárdenas, Salma Morales, Danna Morales, Gabriel Del Valle, Belén Cholango

---

## Ferretería El Tornillo Feliz

### Resolución del caso de estudio

#### Creación tabla de Datos de la Ferretería 
Primero, se creó el esquema staging dentro de la base de datos Datawarehouse1 en PostgreSQL / pgAdmin. Posteriormente, se definió la tabla staging.productos_ferreteria_raw, la cual contiene los datos originales provenientes de las distintas sucursales de la ferretería. Esta tabla almacena información sin procesar, incluyendo inconsistencias en categorías, unidades de medida y formatos de precios, lo cual representa la situación del caso de estudio.

<img width="723" height="568" alt="image" src="https://github.com/user-attachments/assets/f2d72bc3-3097-4f0a-a2ee-9439802ea49c" />

#### Extracción de Datos de la Ferretería en Pentaho
Una vez tenemos esto, procedemos a ir a Pentaho para poder realizar la extracción y limpieza de estos datos.
Primero debemos crear un nuevo archivo de transformación, en donde para extraer los datos del pgAdmin usaremos un Table Input, dentro de este configuraremos y conectaremos la base de datos. Antes de esto, deberemos conectar la base de datos al archivo.  

<img width="664" height="574" alt="image" src="https://github.com/user-attachments/assets/1bd6afca-a659-444d-8651-c7d468359df4" />
