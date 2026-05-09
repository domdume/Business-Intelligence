# Escuela Politécnica Nacional

# Business Intelligence

## Práctica 3

**Integrantes:** Doménica J. Cárdenas, Salma Morales, Danna Morales, Gabriel Del Valle, Belén Cholango.

## Caso de estudio

Una empresa desea analizar el rendimiento de sus ventas según productos, clientes y fechas. Se necesita crear un esquema estrella identificando:

•	Tabla de hechos.
•	Dimensiones.

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
- `Day`
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


### Preguntas

1. ¿Cuántas ventas se realizaron por categoría de producto y mes?

Se utilizaron las tablas `fact_sales`, `dim_product` y `dim_date`, como también las relaciones definidas en el modelo estrella:

- `fact_sales[ProductKey]` → `dim_product[ProductKey]`
- `fact_sales[OrderDateKey]` → `dim_date[DateKey]`

En la tabla dinámica de Power Pivot se configuró:

| Campo       | Valor                          |
|-------------|--------------------------------|
| **Filas**   | `dim_product[Category]`        |
| **Columnas**| `dim_date[Month]`              |
| **Valores** | `COUNT(fact_sales[OrderNumber])` |

De este modo se puede identificar fácilmente las tendencias y picos de demanda por categoría.

<img width="911" height="127" alt="Image" src="https://github.com/user-attachments/assets/9fc90a3b-c9be-4404-b986-6816ca2a8181" />

2.	¿Cuál es el ingreso total (ventas) por cliente y género?

Se utilizaron las tablas `fact_sales` y `dim_customer`, como también la relación definida en el modelo estrella:

- `fact_sales[CustomerKey]` → `dim_customer[CustomerKey]`

En la tabla dinámica de Power Pivot se configuró:

| Campo       | Valor                        |
|-------------|------------------------------|
| **Filas**   | `dim_customer[CustomerKey]`  |
| **Columnas**| `dim_customer[Gender]`       |
| **Valores** | `SUM(fact_sales[SalesAmount])` |

Esto facilita el análisis del comportamiento de compra según esta variable demográfica.

<img width="415" height="313" alt="Image" src="https://github.com/user-attachments/assets/15c99afe-4c21-4f1b-8e5e-6f9e792dd5e7" />

3.	¿Cuál es la cantidad total vendida por producto? <br>
Se utilizaron las tablas `fact_sales` y `dim_product`, que cuenta con la relación definida en el modelo estrella:
Se inserto la tabal dinamica con el `nombre del producto` de la tabla dim_product y `la suma del monto de ventas` de la tabla fact_sales:


<img width="283" height="265" alt="image" src="https://github.com/user-attachments/assets/f560f3fc-5ff2-4bd1-a528-5c8ee3084f04" />


<br>
Gracias a esta tabla, se puede analizar la cantidad total vendida por cada producto, lo cual facilita el analizar que productos se venden más o menos. 
<br>
4.	¿Cuál fue la cantidad enviada por mes de envío?
Se utilizaron las tablas `fact_sales` y `dim_date`, que cuenta con la relación donde muestra las fechas de envio, de donde posteriormente se obtienen los meses.
Se inserto la tabal dinamica con el `mes` de la tabla dim_date y `la cantidad` de la tabla fact_sales:

<img width="269" height="337" alt="image" src="https://github.com/user-attachments/assets/df618c07-b9d0-44f3-b15a-ab4e59114f6e" />

<br>
Gracias a esta tabla, se puede observar que el mes con mas envíos es Junio. <br>  
 
5.	¿Cuánto se vendió por tamaño de producto y por estado civil del cliente?
Se utilizaron las tablas `fact_sales` y `dim_customer` para poder insertar en la tabla dinámica los datos de categoría de tamaño de producto, el estado civil del cliente y agruparlos. 
<img width="250" height="200" alt="image" src="https://github.com/user-attachments/assets/a25d5308-970e-4c86-9e2e-933e74f540af" />
Se observa que en todas las categorías de tamaño, el grupo de clientes casados presenta un volumen de compra significativamente mayor en comparación con el grupo solteros.



