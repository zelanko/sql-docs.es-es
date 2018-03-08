---
title: Crear tabla como SELECT (almacenamiento de datos SQL Azure) | Documentos de Microsoft
ms.custom: 
ms.date: 10/07/2016
ms.prod: 
ms.prod_service: sql-data-warehouse, pdw
ms.reviewer: 
ms.service: sql-data-warehouse
ms.component: t-sql|statements
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: d1e08f88-64ef-4001-8a66-372249df2533
caps.latest.revision: 
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 429c2dc727d844c35943fa599e6fbcb911df04ac
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/25/2018
---
# <a name="create-table-as-select-azure-sql-data-warehouse"></a>Crear tabla como SELECT (almacenamiento de datos SQL Azure)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

Crear tabla AS seleccione (CTAS) es una de las características más importantes de T-SQL disponibles. Es una operación de ejecución en paralelo totalmente que crea una nueva tabla basada en la salida de una instrucción SELECT. CTAS es la forma más sencilla y rápida para crear una copia de una tabla.   
 
 Por ejemplo, use CTAS para:  
  
-   Volver a crear una tabla con una columna de distribución de hash diferente.
-   Volver a crear una tabla como replicados.   
-   Crear un índice de almacén en solo algunas de las columnas de la tabla.  
-   Consultar o importar datos externos.  

> [!NOTE]  
> Puesto que CTAS se agrega a las capacidades de creación de una tabla, en este tema trata de no repita el tema CREATE TABLE. En su lugar, se describen las diferencias entre las instrucciones CREATE TABLE y de CTAS. Para obtener los detalles de CREATE TABLE, vea [CREATE TABLE (almacenamiento de datos de SQL Azure)](https://msdn.microsoft.com/library/mt203953/) instrucción. 
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
<a name="syntax-bk"></a>

## <a name="syntax"></a>Sintaxis   

```  
CREATE TABLE [ database_name . [ schema_name ] . | schema_name. ] table_name   
    [ ( column_name [ ,...n ] ) ]  
    WITH ( 
      <distribution_option> -- required
      [ , <table_option> [ ,...n ] ]    
    )  
    AS <select_statement>   
[;]  

<distribution_option> ::=
    { 
        DISTRIBUTION = HASH ( distribution_column_name ) 
      | DISTRIBUTION = ROUND_ROBIN 
      | DISTRIBUTION = REPLICATE
    }   

<table_option> ::= 
    {   
        CLUSTERED COLUMNSTORE INDEX --default for SQL Data Warehouse 
      | HEAP --default for Parallel Data Warehouse   
      | CLUSTERED INDEX ( { index_column_name [ ASC | DESC ] } [ ,...n ] ) --default is ASC 
    }  
    | PARTITION ( partition_column_name RANGE [ LEFT | RIGHT ] --default is LEFT  
        FOR VALUES ( [ boundary_value [,...n] ] ) ) 
  
<select_statement> ::=  
    [ WITH <common_table_expression> [ ,...n ] ]  
    SELECT select_criteria  

```  

<a name="arguments-bk"></a>
  
## <a name="arguments"></a>Argumentos  
Para obtener más información, consulte el [sección argumentos](https://msdn.microsoft.com/library/mt203953/#Arguments) en CREATE TABLE.  

<a name="column-options-bk"></a>

### <a name="column-options"></a>Opciones de columna
`column_name` [ ,...`n` ]   
 Nombres de columna no permiten la [opciones de columna](https://msdn.microsoft.com/library/mt203953/#ColumnOptions) mencionados en CREATE TABLE.  En su lugar, puede proporcionar una lista opcional de uno o más nombres de columna para la nueva tabla. Las columnas de la nueva tabla utilizará los nombres especificados. Al especificar nombres de columna, el número de columnas en la lista de columnas debe coincidir con el número de columnas en los resultados de select. Si no especifica los nombres de columna, la nueva tabla de destino usará los nombres de columna en los resultados de la instrucción select. 
  
 No se puede especificar cualquier otra opción de columna como tipos de datos, intercalación o la nulabilidad. Cada uno de estos atributos se deriva de los resultados de la `SELECT` instrucción. Sin embargo, puede usar la instrucción SELECT para cambiar los atributos. Para obtener un ejemplo, vea [CTAS de uso para cambiar los atributos de columna](#ctas-change-column-attributes-bk).   

<a name="table-distribution-options-bk"></a>

### <a name="table-distribution-options"></a>Opciones de distribución de la tabla

`DISTRIBUTION` = `HASH`( *distribution_column_name* ) | ROUND_ROBIN | REPLICAR      
La instrucción CTAS requiere una opción de distribución y no tiene valores predeterminados. Esto es diferente de CREATE TABLE, que tiene los valores predeterminados. 

Para obtener más información y para entender cómo elegir la mejor columna de distribución, consulte el [tabla opciones de distribución](https://msdn.microsoft.com/library/mt203953/#TableDistributionOptions) sección en CREATE TABLE. 

<a name="table-partition-options-bk"></a>

### <a name="table-partition-options"></a>Opciones de partición de tabla
La instrucción CTAS crea una tabla sin particiones de forma predeterminada, incluso si la tabla de origen tiene particiones. Para crear una tabla con particiones con la instrucción CTAS, debe especificar la opción de partición. 

Para obtener más información, consulte el [opciones de partición de tabla](https://msdn.microsoft.com/library/mt203953/#TablePartitionOptions) sección en CREATE TABLE.

<a name="select-options-bk"></a>

### <a name="select-options"></a>Seleccione las opciones
La instrucción select es la diferencia fundamental entre CTAS y CREATE TABLE.  

 `WITH` *common_table_expression*  
 Especifica un conjunto de resultados temporal con nombre, conocido como expresión de tabla común (CTE). Para obtener más información, consulte [con common_table_expression &#40; Transact-SQL &#41; ](../../t-sql/queries/with-common-table-expression-transact-sql.md).  
  
 `SELECT` *select_criteria*  
 Rellena la nueva tabla con los resultados de una instrucción SELECT. *select_criteria* es el cuerpo de la instrucción SELECT que determina qué datos se deben copiar en la nueva tabla. Para obtener información acerca de las instrucciones SELECT, vea [SELECT &#40; Transact-SQL &#41; ](../../t-sql/queries/select-transact-sql.md).  
  
<a name="permissions-bk"></a>  
  
## <a name="permissions"></a>Permissions  
Requiere CTAS `SELECT` permiso en cualquier objeto al que hace referencia en el *select_criteria*.

Para que los permisos crear una tabla, consulte [permisos](https://msdn.microsoft.com/library/mt203953/#Permissions) en CREATE TABLE. 
  
<a name="general-remarks-bk"></a>
  
## <a name="general-remarks"></a>Notas generales
Para obtener más información, consulte [comentarios generales](https://msdn.microsoft.com/library/mt203953/#GeneralRemarks) en CREATE TABLE.

<a name="limitations-bk"></a>

## <a name="limitations-and-restrictions"></a>Limitaciones y restricciones  
Almacenamiento de datos de SQL Azure hace todavía no se han automática de soporte técnico de crear o actualizará las estadísticas automáticamente.  Para obtener el mejor rendimiento de las consultas, es importante crear las estadísticas en todas las columnas de todas las tablas después de ejecutar CTAS y después se realizan cambios sustanciales en los datos. Para más información, consulte [CREATE STATISTICS (Transact-SQL)](../../t-sql/statements/create-statistics-transact-sql.md).

[SET ROWCOUNT &#40; Transact-SQL &#41; ](../../t-sql/statements/set-rowcount-transact-sql.md) no tiene ningún efecto en CTAS. Para lograr un comportamiento similar, utilice [TOP &#40; Transact-SQL &#41; ](../../t-sql/queries/top-transact-sql.md).  
 
Para obtener más información, consulte [limitaciones y restricciones](https://msdn.microsoft.com/library/mt203953/#LimitationsRestrictions) en CREATE TABLE.

<a name="locking-behavior-bk"></a>
  
## <a name="locking-behavior"></a>Comportamiento del bloqueo  
 Para obtener más información, consulte [comportamiento de bloqueo](https://msdn.microsoft.com/library/mt203953/#LockingBehavior) en CREATE TABLE.
 
<a name="performance-bk"></a>
 
 ## <a name="performance"></a>Rendimiento 

Para una tabla hash está distribuido, puede usar CTAS para elegir una columna de distribución diferente para lograr un mejor rendimiento de las combinaciones y agregaciones. Si se elige que una columna de distribución diferente no es su objetivo, tendrá el mejor rendimiento de CTAS si se especifica la misma columna de distribución, ya que este modo evita volver a distribuir las filas. 

Si utilizas CTAS para crear la tabla y el rendimiento no es un factor, se puede especificar `ROUND_ROBIN` para evitar tener que decidir sobre una columna de distribución.

Para evitar el movimiento de datos en las consultas posteriores, puede especificar `REPLICATE` a costa de un mayor almacenamiento para cargar una copia completa de la tabla en cada nodo de ejecución.  


<a name="examples-copy-table-bk"></a>

## <a name="examples-for-copying-a-table"></a>Ejemplos para copiar una tabla

<a name="ctas-copy-table-bk"></a>

### <a name="a-use-ctas-to-copy-a-table"></a>A. Use CTAS para copiar una tabla 
Se aplica a: almacenamiento de datos SQL Azure y almacenamiento de datos paralelos

Quizás uno de los más comunes usos del `CTAS` es crear una copia de una tabla para que pueda cambiar el DDL. Si por ejemplo creó originalmente la tabla como `ROUND_ROBIN` y ahora desea cambiarla a una tabla que se distribuyen en una columna, `CTAS` es ¿cómo cambiaría la columna de distribución. `CTAS`También puede utilizarse para cambiar los tipos de particiones, la indización o la columna.

Supongamos que creó esta tabla mediante el tipo de distribución predeterminado de `ROUND_ROBIN` distribuidas porque se especificó ninguna columna de distribución en el `CREATE TABLE`.

```sql
CREATE TABLE FactInternetSales
(
    ProductKey int NOT NULL,
    OrderDateKey int NOT NULL,
    DueDateKey int NOT NULL,
    ShipDateKey int NOT NULL,
    CustomerKey int NOT NULL,
    PromotionKey int NOT NULL,
    CurrencyKey int NOT NULL,
    SalesTerritoryKey int NOT NULL,
    SalesOrderNumber nvarchar(20) NOT NULL,
    SalesOrderLineNumber tinyint NOT NULL,
    RevisionNumber tinyint NOT NULL,
    OrderQuantity smallint NOT NULL,
    UnitPrice money NOT NULL,
    ExtendedAmount money NOT NULL,
    UnitPriceDiscountPct float NOT NULL,
    DiscountAmount float NOT NULL,
    ProductStandardCost money NOT NULL,
    TotalProductCost money NOT NULL,
    SalesAmount money NOT NULL,
    TaxAmt money NOT NULL,
    Freight money NOT NULL,
    CarrierTrackingNumber nvarchar(25),
    CustomerPONumber nvarchar(25)
);
```

Ahora desea crear una nueva copia de esta tabla con un índice de almacén de columnas agrupado por lo que puede aprovechar el rendimiento de las tablas de almacén de columnas agrupado. También desea distribuir esta tabla en ProductKey desde anticipación de combinaciones en esta columna y para evitar el movimiento de datos durante las combinaciones en ProductKey. Por último también desea agregar la creación de particiones en OrderDateKey para que pueda eliminar rápidamente los datos antiguos colocando particiones antiguas. Aquí es la instrucción de CTAS que copiaría la tabla anterior en una nueva tabla.

```sql
CREATE TABLE FactInternetSales_new
WITH
(
    CLUSTERED COLUMNSTORE INDEX,
    DISTRIBUTION = HASH(ProductKey),
    PARTITION
    (
        OrderDateKey RANGE RIGHT FOR VALUES
        (
        20000101,20010101,20020101,20030101,20040101,20050101,20060101,20070101,20080101,20090101,
        20100101,20110101,20120101,20130101,20140101,20150101,20160101,20170101,20180101,20190101,
        20200101,20210101,20220101,20230101,20240101,20250101,20260101,20270101,20280101,20290101
        )
    )
)
AS SELECT * FROM FactInternetSales;
```

Por último, puede cambiar el nombre de las tablas para intercambiar en la nueva tabla y, a continuación, elimine la tabla anterior.

```sql
RENAME OBJECT FactInternetSales TO FactInternetSales_old;
RENAME OBJECT FactInternetSales_new TO FactInternetSales;

DROP TABLE FactInternetSales_old;
```

<a name="examples-column-bk"></a>

## <a name="examples-for-column-options"></a>Ejemplos de opciones de columna

<a name="ctas-change-column-attributes-bk"></a>

### <a name="b-use-ctas-to-change-column-attributes"></a>B. Usar CTAS para cambiar los atributos de columna 
Se aplica a: almacenamiento de datos SQL Azure y almacenamiento de datos paralelos

Este ejemplo utiliza para cambiar los tipos de datos, la nulabilidad y la intercalación de varias columnas en la tabla DimCustomer2 CTAS.  
  
```  
-- Original table 
CREATE TABLE [dbo].[DimCustomer2] (  
    [CustomerKey] int NOT NULL,  
    [GeographyKey] int NULL,  
    [CustomerAlternateKey] nvarchar(15) COLLATE SQL_Latin1_General_CP1_CI_AS NOT NULL  
)  
WITH (CLUSTERED COLUMNSTORE INDEX, DISTRIBUTION = HASH([CustomerKey]));  
  
-- CTAS example to change data types, nullability, and column collations  
CREATE TABLE test  
WITH (HEAP, DISTRIBUTION = ROUND_ROBIN)  
AS  
SELECT  
    CustomerKey AS CustomerKeyNoChange,  
    CustomerKey*1 AS CustomerKeyChangeNullable,  
    CAST(CustomerKey AS DECIMAL(10,2)) AS CustomerKeyChangeDataTypeNullable,  
    ISNULL(CAST(CustomerKey AS DECIMAL(10,2)),0) AS CustomerKeyChangeDataTypeNotNullable,  
    GeographyKey AS GeographyKeyNoChange,  
    ISNULL(GeographyKey,0) AS GeographyKeyChangeNotNullable,  
    CustomerAlternateKey AS CustomerAlternateKeyNoChange,  
    CASE WHEN CustomerAlternateKey = CustomerAlternateKey 
        THEN CustomerAlternateKey END AS CustomerAlternateKeyNullable,  
    CustomerAlternateKey COLLATE Latin1_General_CS_AS_KS_WS AS CustomerAlternateKeyChangeCollation  
FROM [dbo].[DimCustomer2]  
  
-- Resulting table 
CREATE TABLE [dbo].[test] (
    [CustomerKeyNoChange] int NOT NULL, 
    [CustomerKeyChangeNullable] int NULL, 
    [CustomerKeyChangeDataTypeNullable] decimal(10, 2) NULL, 
    [CustomerKeyChangeDataTypeNotNullable] decimal(10, 2) NOT NULL, 
    [GeographyKeyNoChange] int NULL, 
    [GeographyKeyChangeNotNullable] int NOT NULL, 
    [CustomerAlternateKeyNoChange] nvarchar(15) COLLATE SQL_Latin1_General_CP1_CI_AS NOT NULL, 
    [CustomerAlternateKeyNullable] nvarchar(15) COLLATE SQL_Latin1_General_CP1_CI_AS NULL, 
    [CustomerAlternateKeyChangeCollation] nvarchar(15) COLLATE Latin1_General_CS_AS_KS_WS NOT NULL
)
WITH (DISTRIBUTION = ROUND_ROBIN);
```
 
Como paso final, puede usar [RENAME &#40; Transact-SQL &#41; ](../../t-sql/statements/rename-transact-sql.md) para cambiar los nombres de tabla. Esto hace que DimCustomer2 ser la nueva tabla.

```
RENAME OBJECT DimCustomer2 TO DimCustomer2_old;
RENAME OBJECT test TO DimCustomer2;

DROP TABLE DimCustomer2_old;
```

<a name="examples-table-distribution-bk"></a>

## <a name="examples-for-table-distribution"></a>Ejemplos para la distribución de la tabla

<a name="ctas-change-distribution-method-bk"></a>

### <a name="c-use-ctas-to-change-the-distribution-method-for-a-table"></a>C. Usar CTAS para cambiar el método de distribución para una tabla
Se aplica a: almacenamiento de datos SQL Azure y almacenamiento de datos paralelos

Este sencillo ejemplo muestra cómo cambiar el método de distribución para una tabla. Para mostrar la mecánica de cómo hacer esto, cambia una tabla hash está distribuido a round robin y, a continuación, cambia la tabla turnos al hash distribuida. La tabla final coincide con la tabla original. 

En la mayoría de los casos no es necesario convertir una tabla hash está distribuido en una tabla de round robin. Más a menudo, deberá cambiar una tabla de round robin a una tabla distribuida de hash. Por ejemplo, puede cargar inicialmente una tabla nueva como round robin y, a continuación, mover posteriormente a una tabla hash está distribuido para obtener un mejor rendimiento de combinación.

Este ejemplo utiliza la base de datos de ejemplo AdventureWorksDW. Para cargar la versión de almacenamiento de datos SQL, vea [cargar datos de ejemplo en el almacenamiento de datos SQL](https://azure.microsoft.com/documentation/articles/sql-data-warehouse-load-sample-databases/)
 
```
-- DimSalesTerritory is hash-distributed.
-- Copy it to a round-robin table.
CREATE TABLE [dbo].[myTable]   
WITH   
  (   
    CLUSTERED COLUMNSTORE INDEX,  
    DISTRIBUTION = ROUND_ROBIN  
  )  
AS SELECT * FROM [dbo].[DimSalesTerritory]; 

-- Switch table names

RENAME OBJECT [dbo].[DimSalesTerritory] to [DimSalesTerritory_old];
RENAME OBJECT [dbo].[myTable] TO [DimSalesTerritory];

DROP TABLE [dbo].[DimSalesTerritory_old];

```  
A continuación, cambiar a una tabla distribuida de hash.

```
-- You just made DimSalesTerritory a round-robin table.
-- Change it back to the original hash-distributed table. 
CREATE TABLE [dbo].[myTable]   
WITH   
  (   
    CLUSTERED COLUMNSTORE INDEX,  
    DISTRIBUTION = HASH(SalesTerritoryKey) 
  )  
AS SELECT * FROM [dbo].[DimSalesTerritory]; 

-- Switch table names

RENAME OBJECT [dbo].[DimSalesTerritory] to [DimSalesTerritory_old];
RENAME OBJECT [dbo].[myTable] TO [DimSalesTerritory];

DROP TABLE [dbo].[DimSalesTerritory_old];
```
 
<a name="ctas-change-to-replicated-bk"></a>

### <a name="d-use-ctas-to-convert-a-table-to-a-replicated-table"></a>D. Usar CTAS para convertir una tabla en una tabla replicada  
Se aplica a: almacenamiento de datos SQL Azure y almacenamiento de datos paralelos 

En este ejemplo se aplica para convertir tablas round-robin o está distribuido hash en una tabla replicada. Este ejemplo concreto utiliza el método anterior para cambiar la distribución tipo un paso más allá.  Puesto que DimSalesTerritory es una dimensión y es probable que una tabla menor, puede elegir volver a crear la tabla como replicados para evitar el movimiento de datos al unirse a otras tablas. 

```
-- DimSalesTerritory is hash-distributed.
-- Copy it to a replicated table.
CREATE TABLE [dbo].[myTable]   
WITH   
  (   
    CLUSTERED COLUMNSTORE INDEX,  
    DISTRIBUTION = REPLICATE 
  )  
AS SELECT * FROM [dbo].[DimSalesTerritory]; 

-- Switch table names

RENAME OBJECT [dbo].[DimSalesTerritory] to [DimSalesTerritory_old];
RENAME OBJECT [dbo].[myTable] TO [DimSalesTerritory];

DROP TABLE [dbo].[DimSalesTerritory_old];
```
 
### <a name="e-use-ctas-to-create-a-table-with-fewer-columns"></a>E. Use CTAS para crear una tabla con menos columnas
Se aplica a: almacenamiento de datos SQL Azure y almacenamiento de datos paralelos 

En el ejemplo siguiente se crea una tabla distribuida round robin denominada `myTable (c, ln)`. La nueva tabla solo tiene dos columnas. Usa el alias de columna en la instrucción SELECT para los nombres de las columnas.  
  
```  
CREATE TABLE myTable  
WITH   
  (   
    CLUSTERED COLUMNSTORE INDEX,  
    DISTRIBUTION = ROUND_ROBIN  
  )  
AS SELECT CustomerKey AS c, LastName AS ln  
    FROM dimCustomer;  
  
```  

<a name="examples-query-hints-bk"></a>

## <a name="examples-for-query-hints"></a>Ejemplos de sugerencias de consulta

<a name="ctas-query-hint-bk"></a>

### <a name="f-use-a-query-hint-with-create-table-as-select-ctas"></a>F. Utilizar una sugerencia de consulta con CREATE TABLE AS SELECT (CTAS)  
Se aplica a: almacenamiento de datos SQL Azure y almacenamiento de datos paralelos
  
Esta consulta muestra la sintaxis básica para el uso de una sugerencia de combinación de la consulta con la instrucción de CTAS. Una vez enviada la consulta, [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] se aplica la estrategia de combinación hash al generar el plan de consulta para cada distribución individuales. Para obtener más información sobre la sugerencia de consulta de combinación hash, vea [cláusula OPTION &#40; Transact-SQL &#41; ](../../t-sql/queries/option-clause-transact-sql.md).  
  
```  
CREATE TABLE dbo.FactInternetSalesNew  
WITH   
  (   
    CLUSTERED COLUMNSTORE INDEX,  
    DISTRIBUTION = ROUND_ROBIN   
  )  
AS SELECT T1.* FROM dbo.FactInternetSales T1 JOIN dbo.DimCustomer T2  
ON ( T1.CustomerKey = T2.CustomerKey )  
OPTION ( HASH JOIN );  
```  

<a name="examples-external-tables"></a>

## <a name="examples-for-external-tables"></a>Ejemplos de tablas externas

<a name="ctas-azure-blob-storage-bk"></a>

### <a name="g-use-ctas-to-import-data-from-azure-blob-storage"></a>G. Utilice CTAS para importar datos desde almacenamiento de blobs de Azure  
Se aplica a: almacenamiento de datos SQL Azure y almacenamiento de datos paralelos  

Para importar datos desde una tabla externa, simplemente utilice CREATE TABLE AS SELECT para seleccionar de la tabla externa. La sintaxis para seleccionar datos de una tabla externa en [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] es igual que la sintaxis para seleccionar datos de una tabla normal.  
  
 En el ejemplo siguiente se define una tabla externa en los datos de una cuenta de almacenamiento de blobs de Azure. A continuación, utiliza CREATE TABLE AS SELECT para seleccionar de la tabla externa. Esto importa los datos de archivos de texto delimitado de almacenamiento de blobs de Azure y almacena los datos en un nuevo [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] tabla.  
  
```  
--Use your own processes to create the text-delimited files on Azure blob storage.  
--Create the external table called ClickStream.  
CREATE EXTERNAL TABLE ClickStreamExt (   
    url varchar(50),  
    event_date date,  
    user_IP varchar(50)  
)  
WITH (  
    LOCATION='/logs/clickstream/2015/',  
    DATA_SOURCE = MyAzureStorage,  
    FILE_FORMAT = TextFileFormat)  
;  
  
--Use CREATE TABLE AS SELECT to import the Azure blob storage data into a new   
--SQL Data Warehouse table called ClickStreamData  
CREATE TABLE ClickStreamData   
WITH  
  (  
    CLUSTERED COLUMNSTORE INDEX,  
    DISTRIBUTION = HASH (user_IP)  
  )  
AS SELECT * FROM ClickStreamExt  
;  
```  

<a name="ctas-import-Hadoop-bk"></a>
  
### <a name="h-use-ctas-to-import-hadoop-data-from-an-external-table"></a>H. Utilice CTAS para importar datos de Hadoop de una tabla externa  
Se aplica a:[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
Para importar datos desde una tabla externa, simplemente utilice CREATE TABLE AS SELECT para seleccionar de la tabla externa. La sintaxis para seleccionar datos de una tabla externa en [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] es igual que la sintaxis para seleccionar datos de una tabla normal.  
  
 En el ejemplo siguiente se define una tabla externa en un clúster de Hadoop. A continuación, utiliza CREATE TABLE AS SELECT para seleccionar de la tabla externa. Esto importa los datos de archivos de texto delimitado Hadoop y almacena los datos en un nuevo [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] tabla.  
  
```  
-- Create the external table called ClickStream.  
CREATE EXTERNAL TABLE ClickStreamExt (   
    url varchar(50),  
    event_date date,  
    user_IP varchar(50)  
)  
WITH (  
    LOCATION = 'hdfs://MyHadoop:5000/tpch1GB/employee.tbl',  
    FORMAT_OPTIONS ( FIELD_TERMINATOR = '|')  
)  
;  
  
-- Use your own processes to create the Hadoop text-delimited files 
-- on the Hadoop Cluster.  
  
-- Use CREATE TABLE AS SELECT to import the Hadoop data into a new 
-- table called ClickStreamPDW  
CREATE TABLE ClickStreamPDW   
WITH  
  (  
    CLUSTERED COLUMNSTORE INDEX,  
    DISTRIBUTION = HASH (user_IP)  
  )  
AS SELECT * FROM ClickStreamExt  
;   
```  
 
<a name="examples-workarounds-bk"></a>
 
## <a name="examples-using-ctas-to-replace-sql-server-code"></a>Ver ejemplos de uso CTAS para reemplazar el código de SQL Server

Usar CTAS para resolver algunas características no admitidas. Además de poder ejecutar el código en el almacén de datos, volver a escribir código existente para usar CTAS normalmente mejorará el rendimiento. Se trata de un resultado de su diseño totalmente ejecución en paralelo. 

> [!NOTE]
> Intente pensar "CTAS primera". Si cree que puede resolver un problema mediante `CTAS` , a continuación, que suele ser la mejor manera de enfocar, incluso si se escribe como resultado más datos.
>

<a name="ctas-replace-select-into-bk"></a>

### <a name="i-use-ctas-instead-of-selectinto"></a>I. Usar CTAS en lugar de SELECT... EN  
Se aplica a: almacenamiento de datos SQL Azure y almacenamiento de datos paralelos

Código de SQL Server utiliza normalmente SELECT... INTO para rellenar una tabla con los resultados de una instrucción SELECT. Este es un ejemplo de un servidor de SQL SELECT... EN la instrucción.

```sql
SELECT *
INTO    #tmp_fct
FROM    [dbo].[FactInternetSales]
```

Esta sintaxis no se admite en el almacenamiento de datos de SQL y almacenamiento de datos paralelos. Este ejemplo muestra cómo volver a escribir la instrucción SELECT anterior... EN la instrucción como una instrucción de CTAS. Puede elegir cualquiera de las opciones de distribución que se describe en la sintaxis CTAS. Este ejemplo usa el método de distribución de ROUND_ROBIN.

```sql
CREATE TABLE #tmp_fct
WITH
(
    DISTRIBUTION = ROUND_ROBIN
)
AS
SELECT  *
FROM    [dbo].[FactInternetSales]
;
```

<a name="ctas-replace-implicit-joins-bk"></a>

### <a name="j-use-ctas-and-implicit-joins-to-replace-ansi-joins-in-the-from-clause-of-an-update-statement"></a>J. Use CTAS y uniones implícitas para reemplazar las combinaciones ANSI en el `FROM` cláusula de una `UPDATE` instrucción  
Se aplica a: almacenamiento de datos SQL Azure y almacenamiento de datos paralelos  

Es posible que tener una actualización compleja que combina más de dos tablas juntos mediante sintaxis de unión de ANSI para realizar la actualización o eliminación.

Imagine que había que actualizar esta tabla:

```sql
CREATE TABLE [dbo].[AnnualCategorySales]
(   [EnglishProductCategoryName]    NVARCHAR(50)    NOT NULL
,   [CalendarYear]                  SMALLINT        NOT NULL
,   [TotalSalesAmount]              MONEY           NOT NULL
)
WITH
(
    DISTRIBUTION = ROUND_ROBIN
)
;
```

La consulta original podría haber buscando algo parecido a esto:

```sql
UPDATE  acs
SET     [TotalSalesAmount] = [fis].[TotalSalesAmount]
FROM    [dbo].[AnnualCategorySales]     AS acs
JOIN    (
        SELECT  [EnglishProductCategoryName]
        ,       [CalendarYear]
        ,       SUM([SalesAmount])              AS [TotalSalesAmount]
        FROM    [dbo].[FactInternetSales]       AS s
        JOIN    [dbo].[DimDate]                 AS d    ON s.[OrderDateKey]             = d.[DateKey]
        JOIN    [dbo].[DimProduct]              AS p    ON s.[ProductKey]               = p.[ProductKey]
        JOIN    [dbo].[DimProductSubCategory]   AS u    ON p.[ProductSubcategoryKey]    = u.[ProductSubcategoryKey]
        JOIN    [dbo].[DimProductCategory]      AS c    ON u.[ProductCategoryKey]       = c.[ProductCategoryKey]
        WHERE   [CalendarYear] = 2004
        GROUP BY
                [EnglishProductCategoryName]
        ,       [CalendarYear]
        ) AS fis
ON  [acs].[EnglishProductCategoryName]  = [fis].[EnglishProductCategoryName]
AND [acs].[CalendarYear]                = [fis].[CalendarYear]
;
```

Puesto que el almacenamiento de datos SQL no admite combinaciones ANSI en el `FROM` cláusula de una `UPDATE` (instrucción), no puede usar este código de SQL Server a través sin cambiar ligeramente.

Puede usar una combinación de una `CTAS` y una combinación implícita para reemplazar este código:

```sql
-- Create an interim table
CREATE TABLE CTAS_acs
WITH (DISTRIBUTION = ROUND_ROBIN)
AS
SELECT  ISNULL(CAST([EnglishProductCategoryName] AS NVARCHAR(50)),0)    AS [EnglishProductCategoryName]
,       ISNULL(CAST([CalendarYear] AS SMALLINT),0)                      AS [CalendarYear]
,       ISNULL(CAST(SUM([SalesAmount]) AS MONEY),0)                     AS [TotalSalesAmount]
FROM    [dbo].[FactInternetSales]       AS s
JOIN    [dbo].[DimDate]                 AS d    ON s.[OrderDateKey]             = d.[DateKey]
JOIN    [dbo].[DimProduct]              AS p    ON s.[ProductKey]               = p.[ProductKey]
JOIN    [dbo].[DimProductSubCategory]   AS u    ON p.[ProductSubcategoryKey]    = u.[ProductSubcategoryKey]
JOIN    [dbo].[DimProductCategory]      AS c    ON u.[ProductCategoryKey]       = c.[ProductCategoryKey]
WHERE   [CalendarYear] = 2004
GROUP BY
        [EnglishProductCategoryName]
,       [CalendarYear]
;

-- Use an implicit join to perform the update
UPDATE  AnnualCategorySales
SET     AnnualCategorySales.TotalSalesAmount = CTAS_ACS.TotalSalesAmount
FROM    CTAS_acs
WHERE   CTAS_acs.[EnglishProductCategoryName] = AnnualCategorySales.[EnglishProductCategoryName]
AND     CTAS_acs.[CalendarYear]               = AnnualCategorySales.[CalendarYear]
;

--Drop the interim table
DROP TABLE CTAS_acs
;
```

<a name="ctas-replace-ansi-joins-bk"></a>

### <a name="k-use-ctas-to-specify-which-data-to-keep-instead-of-using-ansi-joins-in-the-from-clause-of-a-delete-statement"></a>K. Use CTAS para especificar qué datos se deben mantener en lugar de utilizar ANSI combinaciones en la cláusula FROM de una instrucción DELETE  
Se aplica a: almacenamiento de datos SQL Azure y almacenamiento de datos paralelos  

A veces es usar el mejor método para eliminar datos `CTAS`. En lugar de eliminar los datos simplemente seleccione los datos que desea conservar. Este especialmente cierto para `DELETE` las instrucciones que utilizan ansi se une a sintaxis de unión ya que el almacenamiento de datos SQL no es compatible con ANSI en el `FROM` cláusula de una `DELETE` instrucción.

Hay un ejemplo de una instrucción DELETE convertido a continuación:

```sql
CREATE TABLE dbo.DimProduct_upsert
WITH
(   Distribution=HASH(ProductKey)
,   CLUSTERED INDEX (ProductKey)
)
AS -- Select Data you wish to keep
SELECT     p.ProductKey
,          p.EnglishProductName
,          p.Color
FROM       dbo.DimProduct p
RIGHT JOIN dbo.stg_DimProduct s
ON         p.ProductKey = s.ProductKey
;

RENAME OBJECT dbo.DimProduct        TO DimProduct_old;
RENAME OBJECT dbo.DimProduct_upsert TO DimProduct;
```

<a name="ctas-simplify-merge-bk"></a>

### <a name="l-use-ctas-to-simplify-merge-statements"></a>L. Usar CTAS para simplificar las instrucciones merge  
Se aplica a: almacenamiento de datos SQL Azure y almacenamiento de datos paralelos  

Las instrucciones Merge se pueden sustituir, al menos en parte, mediante el uso de `CTAS`. Es posible consolidar las `INSERT` y `UPDATE` en una única instrucción. Los registros eliminados tendría que estar cerrado en una segunda instrucción.

Un ejemplo de un `UPSERT` está disponible a continuación:

```sql
CREATE TABLE dbo.[DimProduct_upsert]
WITH
(   DISTRIBUTION = HASH([ProductKey])
,   CLUSTERED INDEX ([ProductKey])
)
AS
-- New rows and new versions of rows
SELECT      s.[ProductKey]
,           s.[EnglishProductName]
,           s.[Color]
FROM      dbo.[stg_DimProduct] AS s
UNION ALL  
-- Keep rows that are not being touched
SELECT      p.[ProductKey]
,           p.[EnglishProductName]
,           p.[Color]
FROM      dbo.[DimProduct] AS p
WHERE NOT EXISTS
(   SELECT  *
    FROM    [dbo].[stg_DimProduct] s
    WHERE   s.[ProductKey] = p.[ProductKey]
)
;

RENAME OBJECT dbo.[DimProduct]          TO [DimProduct_old];
RENAME OBJECT dbo.[DimpProduct_upsert]  TO [DimProduct];

```

<a name="ctas-data-type-and-nullability-bk"></a>

### <a name="m-explicitly-state-data-type-and-nullability-of-output"></a>M. Indicar explícitamente el tipo de datos y la nulabilidad de salida  
Se aplica a: almacenamiento de datos SQL Azure y almacenamiento de datos paralelos  

Al migrar código de SQL Server en almacenamiento de datos de SQL, es posible que ejecutar a través de este tipo de modelo de codificación:

```sql
DECLARE @d decimal(7,2) = 85.455
,       @f float(24)    = 85.455

CREATE TABLE result
(result DECIMAL(7,2) NOT NULL
)
WITH (DISTRIBUTION = ROUND_ROBIN)

INSERT INTO result
SELECT @d*@f
;
```

Instintivamente que piense debería migrar este código a un CTAS y se correcto. Sin embargo, hay un problema oculto aquí.

El siguiente código no produce el mismo resultado:

```sql
DECLARE @d decimal(7,2) = 85.455
,       @f float(24)    = 85.455
;

CREATE TABLE ctas_r
WITH (DISTRIBUTION = ROUND_ROBIN)
AS
SELECT @d*@f as result
;
```

Tenga en cuenta que la columna "resultado" traslada los valores de datos de tipo y la nulabilidad de la expresión. Esto puede provocar sutiles variaciones en valores si no tiene cuidado.

Pruebe lo siguiente como ejemplo:

```sql
SELECT result,result*@d
from result
;

SELECT result,result*@d
from ctas_r
;
```

El valor almacenado para el resultado es diferente. Dado que el valor almacenado en la columna de resultados se utiliza en otras expresiones el error pasa a ser incluso más significativo.

![CREATE TABLE AS SELECT resultados](../../t-sql/statements/media/create-table-as-select-results.png)

Esto es especialmente importante para las migraciones de datos. Aunque la segunda consulta es sin duda más precisa, hay un problema. Los datos podrían ser diferentes en comparación con el sistema de origen y que conduce a preguntas de integridad de la migración. Este es uno de los pocos casos donde la respuesta "incorrecta" es realmente la adecuada.

El motivo que se muestra esta discrepancia entre los dos resultados es hacia abajo hasta la conversión de tipos implícita. En el primer ejemplo de la tabla definen la definición de columna. Cuando se inserta la fila se realiza una conversión de tipos implícita. En el segundo ejemplo no hay ninguna conversión de tipos implícita como la expresión define el tipo de datos de la columna. Observe también que la columna en el segundo ejemplo se ha definido como una columna que acepta valores NULL, mientras que en el primer ejemplo no tiene. Cuando se creó la tabla en la nulabilidad en las columnas primer ejemplo se define explícitamente. En el segundo ejemplo, se acaba deja a la expresión y de forma predeterminada este resultaría en una definición de NULL.  

Para resolver estos problemas, debe establecer explícitamente la conversión de tipos y la nulabilidad en la `SELECT` parte de la `CTAS` instrucción. No se puede establecer estas propiedades en la parte de la tabla de crear.

En el ejemplo siguiente se muestra cómo corregir el código:

```sql
DECLARE @d decimal(7,2) = 85.455
,       @f float(24)    = 85.455

CREATE TABLE ctas_r
WITH (DISTRIBUTION = ROUND_ROBIN)
AS
SELECT ISNULL(CAST(@d*@f AS DECIMAL(7,2)),0) as result
```

Observe lo siguiente:
- CAST o CONVERT podría haber utilizado
- ISNULL se utiliza para forzar la nulabilidad no COALESCE
- ISNULL es la función más externa
- La segunda parte de la ISNULL es una constante, es decir, 0

> [!NOTE]
> Para que la nulabilidad establecerse correctamente, es fundamental usar `ISNULL` y no `COALESCE`. `COALESCE`no es una función determinista y por lo que el resultado de la expresión siempre será acepta valores NULL. `ISNULL`es diferente. Es determinista. Por lo tanto, cuando la segunda parte de la `ISNULL` función es una constante o un literal, el valor resultante será no NULL.

Esta sugerencia no es sólo es útil para garantizar la integridad de los cálculos. También es importante para el cambio de partición de tabla. Imagine que tiene esta tabla definida como los hechos:

```sql
CREATE TABLE [dbo].[Sales]
(
    [date]      INT     NOT NULL
,   [product]   INT     NOT NULL
,   [store]     INT     NOT NULL
,   [quantity]  INT     NOT NULL
,   [price]     MONEY   NOT NULL
,   [amount]    MONEY   NOT NULL
)
WITH
(   DISTRIBUTION = HASH([product])
,   PARTITION   (   [date] RANGE RIGHT FOR VALUES
                    (20000101,20010101,20020101
                    ,20030101,20040101,20050101
                    )
                )
)
;
```

Sin embargo, el campo de valor es una expresión calculada no es parte del origen de datos.

Para crear el conjunto de datos con particiones que desea hacer esto:

```sql
CREATE TABLE [dbo].[Sales_in]
WITH    
(   DISTRIBUTION = HASH([product])
,   PARTITION   (   [date] RANGE RIGHT FOR VALUES
                    (20000101,20010101
                    )
                )
)
AS
SELECT
    [date]    
,   [product]
,   [store]
,   [quantity]
,   [price]   
,   [quantity]*[price]  AS [amount]
FROM [stg].[source]
OPTION (LABEL = 'CTAS : Partition IN table : Create')
;
```

La consulta se ejecuta perfectamente. El problema se produce al intentar realizar el cambio de particiones. Las definiciones de tabla no coinciden. Para hacer que las definiciones de tabla coincida con el CTAS necesita modificarse.

```sql
CREATE TABLE [dbo].[Sales_in]
WITH    
(   DISTRIBUTION = HASH([product])
,   PARTITION   (   [date] RANGE RIGHT FOR VALUES
                    (20000101,20010101
                    )
                )
)
AS
SELECT
    [date]    
,   [product]
,   [store]
,   [quantity]
,   [price]   
,   ISNULL(CAST([quantity]*[price] AS MONEY),0) AS [amount]
FROM [stg].[source]
OPTION (LABEL = 'CTAS : Partition IN table : Create');
```

Por lo tanto, puede ver que la coherencia de los tipos y el mantenimiento de las propiedades de nulabilidad en una CTAS es una buena práctica de mejor ingeniería. Ayuda a mantener la integridad de los cálculos y también garantiza que la modificación de particiones es posible.
 
## <a name="see-also"></a>Vea también  
 [CREATE EXTERNAL DATA SOURCE &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-data-source-transact-sql.md)   
 [CREATE EXTERNAL FILE FORMAT &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-file-format-transact-sql.md)   
 [CREATE EXTERNAL TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-table-transact-sql.md)   
 [CREAR AS de tabla externa SELECT &#40; Transact-SQL &#41;](../../t-sql/statements/create-external-table-as-select-transact-sql.md)   
 [Crear tabla &#40; Almacenamiento de datos SQL de Azure &#41; ](../../t-sql/statements/create-table-azure-sql-data-warehouse.md) [Eliminar tabla &#40; Transact-SQL &#41;](../../t-sql/statements/drop-table-transact-sql.md)   
 [Eliminar tabla externa &#40; Transact-SQL &#41;](../../t-sql/statements/drop-external-table-transact-sql.md)   
 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)   
 [Modificar tabla externa &#40; Transact-SQL &#41;](http://msdn.microsoft.com/library/4ae1b23c-67f6-41d0-b614-7a8de914d145)  
  
  


