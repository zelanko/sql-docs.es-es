---
title: Consultas de PolyBase | Microsoft Docs
ms.custom: 
ms.date: 12/08/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: polybase
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine-polybase
ms.tgt_pltfrm: 
ms.topic: article
keywords: PolyBase
helpviewer_keywords:
- PolyBase, import and export
- Hadoop, import with PolyBase
- Hadoop, export with PolyBase
- Azure blob storage, import with PolyBase
- Azure blob storage, export with PolyBase
ms.assetid: 2c5aa2bd-af7d-4f57-9a28-9673c2a4c07e
caps.latest.revision: "18"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: bad7cdb475aa1b9416e7a0463485293e0035de8d
ms.sourcegitcommit: 05e2814fac4d308196b84f1f0fbac6755e8ef876
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/12/2017
---
# <a name="polybase-queries"></a>PolyBase Queries
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  En este artículo se proporcionan ejemplos de consultas mediante el uso de la característica [PolyBase](../../relational-databases/polybase/polybase-guide.md) de SQL Server 2016. Antes de usar estos ejemplos, también debe comprender cuáles son las instrucciones T-SQL necesarias para configurar PolyBase (consulte [Objetos T-SQL de PolyBase](../../relational-databases/polybase/polybase-t-sql-objects.md)).
  
## <a name="queries"></a>Consultas  
 Ejecute instrucciones de Transact-SQL en tablas externas o use herramientas de BI para consultar tablas externas.
  
## <a name="select-from-external-table"></a>SELECT desde tabla externa  
 Consulta simple que devuelve datos de una tabla externa definida.  
  
```tsql  
SELECT TOP 10 * FROM [dbo].[SensorData];   
```
  
 Consulta simple que incluye un predicado.

```
SELECT * FROM [dbo].[SensorData]
WHERE Speed > 65;
```

## <a name="join-external-tables-with-local-tables"></a>JOIN tablas externas con tablas locales

```
SELECT InsuranceCustomers.FirstName,   
                           InsuranceCustomers.LastName,   
                           SensorData.Speed  
FROM InsuranceCustomers INNER JOIN SensorData    
ON InsuranceCustomers.CustomerKey = SensorData.CustomerKey   
WHERE SensorData.Speed > 65   
ORDER BY SensorData.Speed DESC  
  
```  
  
## <a name="pushdown-computation-to-hadoop"></a>Cálculo de la aplicación para Hadoop

Las variaciones de la aplicación se muestran aquí.

### <a name="pushdown-for-selecting-a-subset-of-rows"></a>Aplicación para seleccionar un subconjunto de filas

Use la aplicación del predicado para mejorar el rendimiento de una consulta que selecciona un subconjunto de filas de una tabla externa.

En este ejemplo, SQL Server 2016 inicia un trabajo de Map Reduce para recuperar las filas que coinciden con el predicado `customer.account_balance < 200000` en Hadoop. Como la consulta se puede completar correctamente sin examinar todas las filas de la tabla, solo las filas que cumplen los criterios del predicado se copian en SQL Server. Esto ahorra mucho tiempo y exige menos espacio de almacenamiento temporal cuando el número de saldos de cliente < 200000 es pequeño en comparación con el número de clientes con saldos de cuenta > = 200000.

```
SELECT * FROM customer WHERE customer.account_balance < 200000
SELECT * FROM SensorData WHERE Speed > 65;  
```

### <a name="pushdown-for-selecting-a-subset-of-columns"></a>Aplicación para seleccionar un subconjunto de columnas

Use la aplicación del predicado para mejorar el rendimiento de una consulta que selecciona un subconjunto de columnas de una tabla externa.

En esta consulta, SQL Server inicia un trabajo asignar/reducir para preprocesar el archivo de texto delimitado por Hadoop para que únicamente los datos de las dos columnas, customer.name y customer.zip_code, se copien en PDW de SQL Server.

```
SELECT customer.name, customer.zip_code FROM customer WHERE customer.account_balance < 200000
```

### <a name="pushdown-for-basic-expressions-and-operators"></a>Aplicación para operadores y expresiones básicas

SQL Server permite las siguientes expresiones básicas y operadores para la aplicación del predicado.

+ Operadores de comparación binarios (\<, >, =, !=, <>, >=, <=) para valores de hora, fecha y numéricos.

+ Operadores aritméticos (+, -, *, /, %).

+ Operadores lógicos (AND, OR).

+ Operadores unarios (NOT, IS NULL, IS NOT NULL).

Los operadores BETWEEN, NOT, IN y LIKE podrían aplicarse. El comportamiento real depende de cómo el optimizador de consultas vuelva a escribir las expresiones de operador como una serie de instrucciones que usan operadores relacionales básicos.

La consulta de este ejemplo tiene varios predicados que se pueden insertar en Hadoop. SQL Server puede insertar trabajos de Map Reduce en Hadoop para ejecutar el predicado `customer.account_balance <= 200000`. La expresión `BETWEEN 92656 and 92677` se compone también de operaciones binarias y lógicas que se pueden insertar en Hadoop. La operación lógica **AND** en `customer.account_balance and customer.zipcode` es una expresión final.

Dada esta combinación de predicados, los trabajos de Map Reduce pueden ejecutar todos la cláusula WHERE. Solo los datos que cumplen los criterios SELECT se vuelven a copiar en PDW de SQL Server.

```
SELECT * FROM customer WHERE customer.account_balance <= 200000 AND customer.zipcode BETWEEN 92656 AND 92677
```

### <a name="force-pushdown"></a>Forzar aplicación

```
SELECT * FROM [dbo].[SensorData]
WHERE Speed > 65
OPTION (FORCE EXTERNALPUSHDOWN);
```

### <a name="disable-pushdown"></a>Deshabilitar aplicación

```
SELECT * FROM [dbo].[SensorData]
WHERE Speed > 65
OPTION (DISABLE EXTERNALPUSHDOWN);
```

## <a name="import-data"></a>Importar datos

Importe datos desde Almacenamiento de Azure o Hadoop en SQL Server para obtener un almacenamiento persistente. Use SELECT INTO para importar datos a los que se hace referencia en una tabla externa para el almacenamiento persistente en SQL Server. Cree una tabla relacional sobre la marcha y luego cree un índice de almacén de columnas sobre la tabla en un segundo paso.

```sql
-- PolyBase scenario - import external data into SQL Server
-- Import data for fast drivers into SQL Server to do more in-depth analysis
-- Leverage columnstore technology
  
SELECT DISTINCT   
        Insured_Customers.FirstName, Insured_Customers.LastName,   
        Insured_Customers.YearlyIncome, Insured_Customers.MaritalStatus  
INTO Fast_Customers from Insured_Customers INNER JOIN   
(  
        SELECT * FROM CarSensor_Data where Speed > 35   
) AS SensorD  
ON Insured_Customers.CustomerKey = SensorD.CustomerKey  
ORDER BY YearlyIncome  
  
CREATE CLUSTERED COLUMNSTORE INDEX CCI_FastCustomers ON Fast_Customers;  
```

## <a name="export-data"></a>Exportar datos

Exporte datos de SQL Server a Hadoop o Almacenamiento de Azure. 

En primer lugar, habilite la funcionalidad de exportación; para ello, establezca el valor `sp_configure` de "Permitir exportación de PolyBase" en 1. Luego, cree una tabla externa que apunte al directorio de destino. A continuación, utilice INSERT INTO para exportar datos de una tabla de SQL Server local a un origen de datos externo. 

La instrucción INSERT INTO crea el directorio de destino, si no existe, y los resultados de la instrucción SELECT se exportan a la ubicación especificada en el formato de archivo especificado. Los archivos externos se denominan *QueryID_date_time_ID.format*, donde *ID* es un identificador incremental y *format* es el formato de los datos exportados. Por ejemplo, un nombre de archivo podría ser QID776_20160130_182739_0.orc.

> [!NOTE]
> Al exportar datos a Hadoop o Azure Blob Storage mediante PolyBase, solo se exportan los datos, y no los nombres de columna (metadatos), tal y como se define en el comando CREATE EXTERNAL TABLE.

```sql  
-- PolyBase scenario  - export data from SQL Server to Hadoop
-- Create an external table
CREATE EXTERNAL TABLE [dbo].[FastCustomers2009] (  
        [FirstName] char(25) NOT NULL,   
        [LastName] char(25) NOT NULL,   
        [YearlyIncome] float NULL,   
        [MaritalStatus] char(1) NOT NULL  
)  
WITH (  
        LOCATION='/old_data/2009/customerdata',  
        DATA_SOURCE = HadoopHDP2,  
        FILE_FORMAT = TextFileFormat,  
        REJECT_TYPE = VALUE,  
        REJECT_VALUE = 0  
);  
  
-- Export data: Move old data to Hadoop while keeping it query-able via an external table.  
INSERT INTO dbo.FastCustomer2009  
SELECT T.* FROM Insured_Customers T1 JOIN CarSensor_Data T2  
ON (T1.CustomerKey = T2.CustomerKey)  
WHERE T2.YearMeasured = 2009 and T2.Speed > 40;  
```

## <a name="new-catalog-views"></a>Nuevas vistas de catálogo

Las siguientes nuevas vistas de catálogo muestran recursos externos.
  
```sql
SELECT * FROM sys.external_data_sources;   
SELECT * FROM sys.external_file_formats;  
SELECT * FROM sys.external_tables;  
```
  
 Determine si una tabla es una tabla externa mediante `is_external`  
  
```sql  
SELECT name, type, is_external FROM sys.tables WHERE name='myTableName'   
```  
  
## <a name="next-steps"></a>Pasos siguientes  

Para obtener más información sobre solución de problemas, vea [Solución de problemas de PolyBase](../../relational-databases/polybase/polybase-troubleshooting.md).
