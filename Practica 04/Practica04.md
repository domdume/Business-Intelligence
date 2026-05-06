# Escuela Politécnica Nacional

# Business Intelligence

## Práctica 4

**Integrantes:** Doménica J. Cárdenas, Salma Morales, Danna Morales, Gabriel Del Valle, Belén Cholango.

## Trabajo en grupo

### Diagrama Modelo Estrella de **products.csv**

<img width="600" height="454" alt="image" src="https://github.com/user-attachments/assets/ffbb31c9-4798-4680-b427-6bf11e202cff" />

------------

### Normalizar en un esquema estrella los datos del archivo "Tabla_Desnormalizada_Ventas.csv"

##### Diagrama Modelo Estrella de **Tabla_Desnormalizada_Ventas.csv**

<img width="762" height="478" alt="image" src="https://github.com/user-attachments/assets/e5be750b-b32c-444c-888d-068b54c8617f" />


--------

##### Procedimiento resolución SQL 

1. En primer lugar, se accedió a pgAdmin y una vez dentro del esquema public, se seleccionó la herramienta de `Query Tool`, la cual permitio ejecutar las consultas Sql.
   
2. Una vez dentro del entorno, se procedió a crear la tabla `ventas`, la cual contiene toda la información inicial para el análisis.

```

  CREATE TABLE ventas (
    ProductKey INT,
    ProductCode VARCHAR(20),
    ProductName VARCHAR(100),
    ListPrice NUMERIC(10,2),
    Color VARCHAR(30),
    Size VARCHAR(30),
    Category VARCHAR(50),
    Subcategory VARCHAR(50),
    CustomerKey INT,
    BirthDate DATE,
    MaritalStatus VARCHAR(30),
    Gender VARCHAR(10),
    Income NUMERIC(10,2),
    Children INT,
    HomeOwner VARCHAR(10),
    Cars INT,
    OrderDateKey INT,
    OrderDate DATE,
    ShipDateKey INT,
    ShipDate DATE,
    OrderNumber VARCHAR(20),
    OrderLineNumber INT,
    Quantity INT,
    UnitPrice NUMERIC(10,2),
    ProductCost NUMERIC(10,2),
    SalesAmount NUMERIC(10,2)
);
```

3. Se verificó que la tabla se haya creado correctamente mediante la siguiente consulta:

 ```
SELECT * FROM ventas;
 ```
<img width="1600" height="185" alt="image" src="https://github.com/user-attachments/assets/d2d8dc2e-6c43-460d-901a-0c3be529c3b0" />

4. A continuación, se realizó la importación de datos desde un archivo `.csv` hacia la tabla `ventas` utilizando las herramientas de pgAdmin.

<img width="551" height="429" alt="image" src="https://github.com/user-attachments/assets/38f38545-687d-474e-babc-d95bb5a10fbe" />


<img width="551" height="429" alt="image" src="https://github.com/user-attachments/assets/45fe4a71-996f-4b75-b544-bea924261320" />

-----------------------------------------------------------------------------------------------
Se comprobó que los datos se hayan cargado correctamente ejecutando una consulta sobre la tabla. 

<img width="1489" height="609" alt="image" src="https://github.com/user-attachments/assets/0d6e1ccf-f225-4627-8553-1f348f6b3dd7" />

5. **Creacion de las tablas de dimensión**

Se creó la tabla dim_producto, que almacena la información relacionada con los productos. 

```
CREATE TABLE dim_producto (
    ProductKey INT PRIMARY KEY,
    ProductCode VARCHAR(20),
    ProductName VARCHAR(100),
    ListPrice NUMERIC(10,2),
    Color VARCHAR(30),
    Size VARCHAR(30),
    Category VARCHAR(50),
    Subcategory VARCHAR(50)
);
```
Con la tabla creada, se insertaron los datos únicos desde la tabla ventas:

```
INSERT INTO dim_producto
SELECT DISTINCT
    ProductKey,
    ProductCode,
    ProductName,
    ListPrice,
    Color,
    Size,
    Category,
    Subcategory
FROM ventas;
```

Continuamos con la creación de la tabla Dim_Cliente:

```
CREATE TABLE dim_cliente (
    CustomerKey INT PRIMARY KEY,
    BirthDate DATE,
    MaritalStatus VARCHAR(30),
    Gender VARCHAR(10),
    Income NUMERIC(10,2),
    Children INT,
    HomeOwner VARCHAR(10),
    Cars INT
);
```
y se cargan con los datos que sean necesarios para el analisis

```
INSERT INTO dim_cliente
SELECT DISTINCT
    CustomerKey,
    BirthDate,
    MaritalStatus,
    Gender,
    Income,
    Children,
    HomeOwner,
    Cars
FROM ventas;
```
A continuación se creó las dos dimensiones de fecha, primero

- **dim_fecha_orden**
```
CREATE TABLE dim_fecha_orden (
    OrderDateKey INT PRIMARY KEY,
    OrderDate DATE
);
```

- **dim_fecha_envio**

```
CREATE TABLE dim_fecha_envio (
    ShipDateKey INT PRIMARY KEY,
    ShipDate DATE
);
```

Despues de que cada tabla este creada, se procedió con la incersión de sus debidos datos

- Insertar en **dim_fecha_orden**

```
INSERT INTO dim_fecha_orden
SELECT DISTINCT
    OrderDateKey,
    OrderDate
FROM ventas;
```

2. Insertar en **dim_fecha_envio**

```
INSERT INTO dim_fecha_envio
SELECT DISTINCT
    ShipDateKey,
    ShipDate
FROM ventas;
```

Una vez completada las tablas de dimensiones, se procedio a crear la tabla principal que es la de fact_ventas que integra todas las relaciones:

```
CREATE TABLE fact_ventas (
    OrderNumber VARCHAR(20),
    OrderLineNumber INT,
    ProductKey INT REFERENCES dim_producto(ProductKey),
    CustomerKey INT REFERENCES dim_cliente(CustomerKey),
    OrderDateKey INT REFERENCES dim_fecha_orden(OrderDateKey),
    ShipDateKey INT REFERENCES dim_fecha_envio(ShipDateKey),
    Quantity INT,
    UnitPrice NUMERIC(10,2),
    ProductCost NUMERIC(10,2),
    SalesAmount NUMERIC(10,2),
    PRIMARY KEY (OrderNumber, OrderLineNumber)
);
```

Una vez creada dicha tabla, se insertan datos: 

```
INSERT INTO fact_ventas
SELECT
    OrderNumber,
    OrderLineNumber,
    ProductKey,
    CustomerKey,
    OrderDateKey,
    ShipDateKey,
    Quantity,
    UnitPrice,
    ProductCost,
    SalesAmount
FROM ventas;
```

Finalmente, se comprobó que todos los datos se hayan cargado correctamente en la tabla de hechos mediante la consulta:

```
SELECT * FROM fact_ventas;
```

<img width="1486" height="579" alt="image" src="https://github.com/user-attachments/assets/055ae9ab-6cdd-4d28-b8c4-7aaf722b5416" />

--------
##### Contestar las siguientes preguntas en SQL:

1. ¿Cuántas ventas se realizaron por categoría de producto y mes?
2. ¿Cuál es el ingreso total (ventas) por cliente y género?
3. ¿Cuál es la cantidad total vendida por producto?
4. ¿Cuál fue la cantidad enviada por mes de envío?
5. ¿Cuánto se vendió por tamaño de producto y por estado civil del cliente?

