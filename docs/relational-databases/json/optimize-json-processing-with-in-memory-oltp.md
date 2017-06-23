---
title: "Optimización del procesamiento de OLTP en memoria JSON | Microsoft Docs"
ms.custom: 
ms.date: 02/03/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-json
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: d9c5adb1-3209-4186-bc10-8e41a26f5e57
caps.latest.revision: 3
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 439b568fb268cdc6e6a817f36ce38aeaeac11fab
ms.openlocfilehash: 12ef08a1f90e0346828a9dafb4052864254954d7
ms.contentlocale: es-es
ms.lasthandoff: 06/23/2017

---
# <a name="optimize-json-processing-with-in-memory-oltp"></a>Optimización del procesamiento de OLTP en memoria JSON
[!INCLUDE[tsql-appliesto-ssvNxt-asdb-xxxx-xxx](../../includes/tsql-appliesto-ssvnxt-asdb-xxxx-xxx.md)]

SQL Server y Azure SQL Database permiten trabajar con texto en formato JSON. Para aumentar el rendimiento de las consultas OLTP que procesan datos JSON, puede almacenar documentos JSON en tablas optimizadas en memoria utilizando las columnas de cadena estándar (tipo NVARCHAR).

## <a name="store-json-in-memory-optimized-tables"></a>Almacenamiento de datos JSON en tablas con optimización para memoria
En el ejemplo siguiente se crea una tabla `Product` con optimización para memoria con dos columnas: `Tags` y `Data`.

```sql
CREATE SCHEMA xtp;
GO
CREATE TABLE xtp.Product(
    ProductID int PRIMARY KEY NONCLUSTERED, --standard column
    Name nvarchar(400) NOT NULL, --standard column
    Price float, --standard column

    Tags nvarchar(400),--json stored in string column
    Data nvarchar(4000) --json stored in string column

) WITH (MEMORY_OPTIMIZED=ON);
```
Al almacenar datos JSON en tablas con optimización para memoria, se aumenta el rendimiento de consulta gracias a que se aprovecha el acceso a los datos en memoria sin bloqueo.

## <a name="optimize-json-with-additional-in-memory-features"></a>Optimización de datos JSON con más características en memoria
Las nuevas características disponibles en SQL Server y Azure SQL Database permiten integrar completamente las funcionalidades JSON con las tecnologías existentes de OLTP en memoria. Por ejemplo, puede realizar las siguientes tareas:
 - Valide la estructura de los documentos JSON almacenados en tablas con optimización para memoria mediante las restricciones CHECK compiladas de forma nativa.
 - Exponga y tipe fuertemente los valores almacenados en documentos JSON con columnas calculadas.
 - Indexe los valores de los documentos JSON con índices con optimización para memoria.
 - Compile de forma negativa las consultas SQL que usan valores de documentos JSON o formatee los resultados como texto JSON.

## <a name="validate-json-columns"></a>Validación de columnas JSON
SQL Server y Azure SQL Database permiten agregar restricciones CHECK compiladas de forma nativa que validan el contenido de los documentos JSON almacenados en una columna de cadena, tal y como se muestra en el ejemplo siguiente.

```sql
DROP TABLE IF EXISTS xtp.Product;
GO
CREATE TABLE xtp.Product(
    ProductID int PRIMARY KEY NONCLUSTERED,
    Name nvarchar(400) NOT NULL,
    Price float,

    Tags nvarchar(400)
            CONSTRAINT [Tags should be formatted as JSON]
                CHECK (ISJSON(Tags)=1),
    Data nvarchar(4000)

) WITH (MEMORY_OPTIMIZED=ON);
```

La restricción CHECK compilada de forma nativa puede agregarse en las tablas existentes que contienen columnas JSON:

```sql
ALTER TABLE xtp.Product
    ADD CONSTRAINT [Data should be JSON]
        CHECK (ISJSON(Data)=1)
```

Con las restricciones CHECK de JSON compiladas de forma nativa, puede asegurarse de que el texto JSON almacenado en las tablas con optimización para memoria tiene el formato correcto.

## <a name="expose-json-values-using-computed-columns"></a>Exposición de valores JSON mediante columnas calculadas
Las columnas calculadas permiten exponer valores del texto JSON y obtener acceso a esos valores sin volver a evaluar las expresiones que capturan un valor del texto JSON y sin volver a analizar la estructura JSON. Los valores expuestos están fuertemente tipados y persisten físicamente en las columnas calculadas. Acceder a los valores JSON mediante columnas calculadas persistentes es más rápido que hacerlo a los valores del documento JSON.

En el ejemplo siguiente se muestra cómo exponer los dos valores siguientes de la columna `Data` JSON:
-   El país donde se fabricó un producto.
-   El costo de fabricación del producto.

```sql
DROP TABLE IF EXISTS xtp.Product;
GO
CREATE TABLE xtp.Product(
    ProductID int PRIMARY KEY NONCLUSTERED,
    Name nvarchar(400) NOT NULL,
    Price float,

    Data nvarchar(4000),

    MadeIn AS CAST(JSON_VALUE(Data, '$.MadeIn') as NVARCHAR(50)) PERSISTED,
    Cost   AS CAST(JSON_VALUE(Data, '$.ManufacturingCost') as float)

) WITH (MEMORY_OPTIMIZED=ON);
```

Las columnas calculadas `MadeIn` y `Cost` se actualizan cada vez que se guarda el documento JSON en los cambios de la columna `Data`.

## <a name="index-values-in-json-columns"></a>Indexación de valores en las columnas JSON
SQL Server y Azure SQL Database permiten indexar valores en columnas JSON utilizando índices con optimización para memoria. Se deben exponer los valores JSON que se indexan y se tipan fuertemente utilizando las columnas calculadas, tal y como se muestra en el ejemplo siguiente.

```sql
DROP TABLE IF EXISTS xtp.Product;
GO
CREATE TABLE xtp.Product(
    ProductID int PRIMARY KEY NONCLUSTERED,
    Name nvarchar(400) NOT NULL,
    Price float,

    Data nvarchar(4000),

    MadeIn AS CAST(JSON_VALUE(Data, '$.MadeIn') as NVARCHAR(50)) PERSISTED,
    Cost   AS CAST(JSON_VALUE(Data, '$.ManufacturingCost') as float) PERSISTED,

    INDEX [idx_Product_MadeIn] NONCLUSTERED (MadeIn)

) WITH (MEMORY_OPTIMIZED=ON)

ALTER TABLE Product
    ADD INDEX [idx_Product_Cost] NONCLUSTERED HASH(Cost)
        WITH (BUCKET_COUNT=20000)
```
Los valores de columnas JSON se pueden indexar con los índices NONCLUSTERED y HASH.
-   Los índices NONCLUSTERED optimizan las consultas que seleccionan rangos de filas por algún valor JSON u ordenan los resultados por valores JSON.
-   Los índices HASH proporcionan un rendimiento óptimo cuando se recupera una sola fila o una serie de filas especificando el valor exacto que se va a buscar.

## <a name="native-compilation-of-json-queries"></a>Compilación nativa de consultas JSON
Finalmente, la compilación nativa de procedimientos, funciones y desencadenadores de Transact-SQL que contienen consultas con funciones JSON mejora el rendimiento de las consultas y reduce los ciclos de CPU necesarios para ejecutar los procedimientos. En el ejemplo siguiente se muestra un procedimiento compilado de forma nativa que utiliza varias funciones: JSON_VALUE, OPENJSON y JSON_MODIFY.

```sql
CREATE PROCEDURE xtp.ProductList(@ProductIds nvarchar(100))
WITH SCHEMABINDING, NATIVE_COMPILATION
AS BEGIN
    ATOMIC WITH (transaction isolation level = snapshot,  language = N'English')

    SELECT ProductID,Name,Price,Data,Tags, JSON_VALUE(data,'$.MadeIn') AS MadeIn
    FROM xtp.Product
        JOIN OPENJSON(@ProductIds)
            ON ProductID = value

END;

CREATE PROCEDURE xtp.UpdateProductData(@ProductId int, @Property nvarchar(100), @Value nvarchar(100))
WITH SCHEMABINDING, NATIVE_COMPILATION
AS BEGIN
    ATOMIC WITH (transaction isolation level = snapshot,  language = N'English')

    UPDATE xtp.Product
    SET Data = JSON_MODIFY(Data, @Property, @Value)
    WHERE ProductID = @ProductId;

END
```

## <a name="learn-more-about-the-built-in-json-support-in-sql-server"></a>Obtener más información sobre la compatibilidad integrada de JSON en SQL Server  
Para una gran cantidad de soluciones específicas, casos de uso y recomendaciones, consulte el [entradas de blog sobre la compatibilidad integrada de JSON](http://blogs.msdn.com/b/sqlserverstorageengine/archive/tags/json/) en SQL Server y en la base de datos de SQL de Azure mediante el Administrador de programas de Microsoft Jovan Popovic.

