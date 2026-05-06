# Escuela Politécnica Nacional

# Business Intelligence

## Práctica 4

**Integrantes:** Doménica J. Cárdenas, Salma Morales, Danna Morales, Gabriel Del Valle, Belén Cholango.

## Trabajo en grupo

### Diagrama Modelo Estrella de **products.csv**

------------

### Normalizar en un esquema estrella los datos del archivo "Tabla_Desnormalizada_Ventas.csv"

##### Diagrama Modelo Estrella de **Tabla_Desnormalizada_Ventas.csv**

--------

##### Procedimiento resolución SQL 

Lo primero que realizamos fue entrar al pgAdmin, y dentro de public ir a Query Tool. Una vez aquí, procedemos con la creación de la tabla "ventas".

**CREATE TABLE ventas (
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
);**

Se verifica que esta tabla haya sido creada con el comando:

**SELECT * FROM ventas;** 

[primera imagen]

Ahora procedemos a realizar la importación de datos del archivo .csv en la tabla recien creada. 

[siguiente imagenes]

Se verifica que los datos hayan sido importados correctamente.

[siguientes imagenes]

Ahora procedemos a crear la tabla Dim_Producto ejecutando:

**CREATE TABLE dim_producto (
    ProductKey INT PRIMARY KEY,
    ProductCode VARCHAR(20),
    ProductName VARCHAR(100),
    ListPrice NUMERIC(10,2),
    Color VARCHAR(30),
    Size VARCHAR(30),
    Category VARCHAR(50),
    Subcategory VARCHAR(50)
);**

y se llena con sus debidos datos

**INSERT INTO dim_producto
SELECT DISTINCT
    ProductKey,
    ProductCode,
    ProductName,
    ListPrice,
    Color,
    Size,
    Category,
    Subcategory
FROM ventas;**

Continuamos con la creación de la tabla Dim_Cliente:

**CREATE TABLE dim_cliente (
    CustomerKey INT PRIMARY KEY,
    BirthDate DATE,
    MaritalStatus VARCHAR(30),
    Gender VARCHAR(10),
    Income NUMERIC(10,2),
    Children INT,
    HomeOwner VARCHAR(10),
    Cars INT
);**

y se llena con los datos que sean necesarios

**INSERT INTO dim_cliente
SELECT DISTINCT
    CustomerKey,
    BirthDate,
    MaritalStatus,
    Gender,
    Income,
    Children,
    HomeOwner,
    Cars
FROM ventas;**

Ahora vamos a crear las dos dimensiones de fecha, primero

1. dim_fecha_orden

**CREATE TABLE dim_fecha_orden (
    OrderDateKey INT PRIMARY KEY,
    OrderDate DATE
);**

2. dim_fecha_envio

**CREATE TABLE dim_fecha_envio (
    ShipDateKey INT PRIMARY KEY,
    ShipDate DATE
);**

Y una vez cada tabla este creada se llena con sus debidos datos

1. Llenar dim_fecha_orden

**INSERT INTO dim_fecha_orden
SELECT DISTINCT
    OrderDateKey,
    OrderDate
FROM ventas;**

2. Llenar dim_fecha_envio

**INSERT INTO dim_fecha_envio
SELECT DISTINCT
    ShipDateKey,
    ShipDate
FROM ventas;**

Una vez completada la creación de las tablas de dimensiones, procederemos a crear la tabla principal que es la de fact_ventas

**CREATE TABLE fact_ventas (
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
);**

una vez creada, se insertan datos

**INSERT INTO fact_ventas
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
FROM ventas;**

Finalmente comprobamos que esten todos los datos dentro de la tabla principal con **SELECT * FROM fact_ventas**.

[siguientes imagenes]

--------
##### Contestar las siguientes preguntas en SQL:

1. ¿Cuántas ventas se realizaron por categoría de producto y mes?
2. ¿Cuál es el ingreso total (ventas) por cliente y género?
3. ¿Cuál es la cantidad total vendida por producto?
4. ¿Cuál fue la cantidad enviada por mes de envío?
5. ¿Cuánto se vendió por tamaño de producto y por estado civil del cliente?

