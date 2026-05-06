# Escuela Politécnica Nacional

# Business Intelligence

## Práctica 3

**Integrantes:** Doménica J. Cárdenas, Salma Morales, Danna Morales, Gabriel Del Valle, Belén Cholango.

## Caso de estudio

Una empresa desea analizar el rendimiento de sus ventas según productos, clientes y fechas. Se necesita crear un esquema estrella identificando:
•	Tabla de hechos
•	Dimensiones

El objetivo es responder a preguntas comerciales clave mediante tablas dinámicas basadas en Power Pivot
1. ¿Cuántas ventas se realizaron por categoría de producto y mes?
2.	¿Cuál es el ingreso total (ventas) por cliente y género?
3.	¿Cuál es la cantidad total vendida por producto?
4.	¿Cuál fue la cantidad enviada por mes de envío?
5.	¿Cuánto se vendió por tamaño de producto y por estado civil del cliente?

### Resolución del caso de estudio

#### CREACIÍON DEL MODELO ESTRELLA 
Primero, se identificaron las tablas de hechos y de dimensiones, las cuales quedaron distribuidas de la siguiente manera: 

**fact_sales**                  
- `OrderNumber`
- `OrderLineNumber`
- `Quantity`
- `UnitPrice`
- `ProductCost`
- `SalesAmount`
- `ProductKey (FK)`
- `CustomerKey (FK)`
- `OrderDateKey (FK)`
- `ShipDateKey`
  
**dim_product**
- `ProductKey (PK)`
- `Product Code`
- `Product Name`
- `List Price`
- `Color`
- `Size`
- `Category`
- `Subcategory`

**dim_customer** 
- `CustomerKey (PK)`
- `Birth Date`
- `Marital Status`
- `Gender`
- `Income`
- `Children`
- `Home Owner`
- `Cars`

**dim_date**
- `DateKey (PK)`
- `Year`
- `Month`
- `Year`

Una vez con las tablas definidas, se creó una hoja de excel por cada tabla dentro del mismo libro 
<img width="1083" height="271" alt="image" src="https://github.com/user-attachments/assets/e0c9cdca-cbe2-411b-bf80-8e09e9c247bb" />

A continuación se seleccionaron las columnas que formaran parte de la tabla dim_product, se presionó c `ctrl` + `T`, se selecciono "Mi tabla tiene encabezados", se les puso el nombre de dim_producto y en Inicio se selecicono guardar y cerrar donde se convirtió en una tabla de excel. 

<img width="332" height="183" alt="image" src="https://github.com/user-attachments/assets/7ed97b53-f189-4751-8ffd-3d610cc97411" />

Lo mismo se realizó con las demás tablas. 

<img width="218" height="174" alt="image" src="https://github.com/user-attachments/assets/19220489-a4fb-404e-9add-551eb56fbcd4" />

Se eliminaron los duplicados de las tablas de dimensiones por la PK. 

Ejemplo: **dim_customer** 

<img width="426" height="300" alt="image" src="https://github.com/user-attachments/assets/4d65cc9d-4224-419e-80c5-8bf4c5dbca04" />

Luego se agregaron los datos al modelo. 

<img width="482" height="205" alt="image" src="https://github.com/user-attachments/assets/8e79d570-6b8d-4bf2-8961-ed57e8686586" />

Finalmente, se crearon las relaciones de las tablas y se visualizo el diagrama. 

<img width="546" height="546" alt="image" src="https://github.com/user-attachments/assets/b9a25ca1-cbc6-4748-af5b-e76dc591f842" />








