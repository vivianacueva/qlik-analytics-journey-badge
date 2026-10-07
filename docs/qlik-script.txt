## 🔧 Resumen del Qlik Script

El script está organizado por secciones para separar las diferentes etapas de construcción y optimización del modelo de datos.

### 1. Configuración y variables

Se establecen las configuraciones generales de Qlik, como formatos numéricos y de fecha, y se definen variables para centralizar las conexiones a las fuentes de datos:

- `vFileLocation` → ubicación de los archivos en Qlik Cloud.
- `vDBConn` → conexión a la base de datos SQL Server.

### 2. Mapping Tables

Se crean tablas de mapeo para incorporar información de diferentes fuentes sin añadir tablas adicionales al modelo.

Se utilizan principalmente para:

- Incorporar el nombre de la división a `Customers`.
- Incorporar el nombre del transportista a `Orders`.
- Obtener `UnitCost` desde `Products` para calcular el coste de los productos vendidos en `OrderDetails`.

Esta sección forma parte de la optimización del modelo desde **Snowflake → Star Schema**.

### 3. Tablas de medidas

Se cargan las principales tablas transaccionales:

- `Orders`
- `OrderDetails`

Durante la carga se realizan transformaciones y cálculos como:

- Creación de contadores y claves.
- Categorización del peso de los pedidos.
- Creación de clases mediante `Class()`.
- Cálculo de ventas por línea.
- Cálculo del coste de los bienes vendidos (*Cost of Goods Sold*).
- Cálculo del margen.
- Cálculo del importe total de cada pedido.
- Filtrado mediante `Exists()`.
- Creación de claves compuestas con `AutoNumber()`.

También se utilizan `Left Join` para incorporar información de otras tablas y reducir el número de tablas del modelo final.

### 4. Dimensiones procedentes de la base de datos

Se cargan las principales dimensiones:

- `Customers`
- `Products`
- `Categories`
- `Divisions`
- `Shippers`

Como parte de la optimización, algunas dimensiones se integran mediante **Mapping Load** o **Join** para reducir asociaciones y simplificar el modelo.

Por ejemplo, la información de `Categories` se incorpora directamente a `Products`, evitando mantener una tabla adicional de categorías.

### 5. Dimensiones procedentes de archivos

Se incorporan datos desde diferentes tipos de archivos:

- Excel.
- Excel con múltiples hojas.
- CSV.
- XML.
- Archivos de ancho fijo.
- Scripts externos `.qvs`.

Entre las tablas y estructuras utilizadas se encuentran:

- `Employees`
- `Teams`
- `Offices`
- `OrgStructure`
- `Suppliers`

También se utiliza `Concatenate()` para incorporar nuevos empleados a la tabla existente y `Qualify/Unqualify` para controlar asociaciones y evitar claves sintéticas o referencias no deseadas.

### 6. Transformaciones y modelado avanzado

El script incorpora diferentes técnicas de modelado de Qlik:

- `Mapping Load` y `ApplyMap()`.
- `Resident Load`.
- `Preceding Load`.
- `Left Join`.
- `Concatenate`.
- `AutoNumber`.
- `Exists()`.
- `Qualify / Unqualify`.
- `Crosstable`.
- `Hierarchy`.
- `HierarchyBelongsTo`.
- `IntervalMatch`.

Estas técnicas permiten transformar y enriquecer los datos antes de llegar al modelo analítico final.

### 7. IntervalMatch

Se utiliza `IntervalMatch` para asociar el precio de catálogo (`CataloguePrice`) con un rango de precios definido en una tabla externa.

Posteriormente, el grupo de precios se incorpora a `Products`, manteniendo la estructura del modelo estrella y evitando tablas y asociaciones innecesarias.

### 8. Crosstable

Se utiliza `Crosstable` para transformar la estructura de habilidades de los empleados desde un formato donde cada habilidad es una columna a un formato más adecuado para el análisis.

Esto genera una estructura basada en:

- Empleado.
- Habilidad.
- Indicador de posesión de la habilidad.

### 9. Jerarquías organizativas

Se utilizan `Hierarchy()` y `HierarchyBelongsTo()` para representar la estructura jerárquica de empleados y managers.

Esto permite analizar las relaciones organizativas y obtener información sobre los diferentes niveles de la jerarquía.

### 10. Master Calendar

Se construye un **Master Calendar** independiente a partir de las fechas mínimas y máximas de `Orders`.

El calendario incorpora atributos como:

- Año.
- Mes.
- Día.
- Semana.
- Trimestre.
- `MonthYear`.
- `WeekYear`.
- Calendario fiscal.
- Flags YTD, QTD y MTD.
- Mes actual y mes anterior.

También se utiliza `InYearToDate()` para facilitar el análisis de periodos acumulados.

### 11. Data Island

Se crea una tabla independiente de `ExchangeRates` como ejemplo de **Data Island**.

La tabla contiene información de tipos de cambio y permite utilizar una selección de moneda como elemento independiente para realizar conversiones en las expresiones de análisis.

### 12. Creación y exportación de QVDs

El script incluye ejemplos de exportación de tablas a formato **QVD** mediante `STORE`.

Además, se utiliza un bucle para recorrer todas las tablas del modelo y generar automáticamente un QVD por cada tabla.

Esta parte permite aplicar una arquitectura basada en QVD y sirve como base para separar procesos de extracción, transformación y carga.

### 13. Resultado del script

El resultado final es un modelo de datos optimizado alrededor de un **Star Schema**, donde se reducen tablas y asociaciones innecesarias mediante Mapping Loads, Joins y otras técnicas de transformación.

El script combina fuentes SQL y archivos externos, incorpora un Master Calendar y aplica técnicas avanzadas de modelado y optimización de Qlik Cloud.