---
title: Introducción a las características de rendimiento de SQL Server en Linux | Microsoft Docs
description: En este artículo se proporciona una introducción de las características de rendimiento de SQL Server para los usuarios de Linux que están familiarizados con SQL Server. Muchos de estos ejemplos funcionan en todas las plataformas, pero el contexto de este artículo es Linux.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 03/17/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 60036d26-4797-4872-9a9e-3552841c61be
ms.openlocfilehash: a340b3b8ded0824947cc242538ad19159b4abb4d
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/05/2019
ms.locfileid: "66713324"
---
# <a name="walkthrough-for-the-performance-features-of-sql-server-on-linux"></a>Tutorial para conocer las características de rendimiento de SQL Server en Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Si es un usuario de Linux que está familiarizado con SQL Server, las tareas siguientes le guiarán a través de algunas de las características de rendimiento. Estos no son únicos o específica de Linux, pero resulta útil para darle una idea de las áreas para investigar en profundidad. En cada ejemplo, se proporciona un vínculo a la documentación detallada para dicha área.

> [!NOTE]
> En los siguientes ejemplos, se usa la base de datos de ejemplo AdventureWorks. Para obtener instrucciones sobre cómo obtener e instalar esta base de datos de ejemplo, vea [restaurar una base de datos de SQL Server de Windows a Linux](sql-server-linux-migrate-restore-database.md).

## <a name="create-a-columnstore-index"></a>Crear un índice de almacén de columnas
Un índice de almacén de columnas es una tecnología para almacenar y consultar grandes almacenes de datos en un formato de datos en columnas denominado almacén de columnas.  

1. Agregar un índice de almacén de columnas a la tabla SalesOrderDetail ejecutando los siguientes comandos de Transact-SQL:

   ```sql
   CREATE NONCLUSTERED COLUMNSTORE INDEX [IX_SalesOrderDetail_ColumnStore]
      ON Sales.SalesOrderDetail
      (UnitPrice, OrderQty, ProductID)
   GO
   ```

2. Ejecute la siguiente consulta que utiliza el índice de almacén de columnas para examinar la tabla:

   ```sql
   SELECT ProductID, SUM(UnitPrice) SumUnitPrice, AVG(UnitPrice) AvgUnitPrice,
      SUM(OrderQty) SumOrderQty, AVG(OrderQty) AvgOrderQty
   FROM Sales.SalesOrderDetail
      GROUP BY ProductID
      ORDER BY ProductID
   ```

3. Compruebe que se usó el índice de almacén de columnas, buscar el object_id para el índice de almacén de columnas y confirme que aparece en las estadísticas de uso de la tabla SalesOrderDetail:

   ```sql
   SELECT * FROM sys.indexes WHERE name = 'IX_SalesOrderDetail_ColumnStore'
   GO

   SELECT * 
   FROM sys.dm_db_index_usage_stats
      WHERE database_id = DB_ID('AdventureWorks')
      AND object_id = OBJECT_ID('AdventureWorks.Sales.SalesOrderDetail');
   ```
   
## <a name="use-in-memory-oltp"></a>Usar OLTP en memoria
SQL Server proporciona características de OLTP en memoria que pueden mejorar considerablemente el rendimiento de sistemas de aplicaciones.  En esta sección de la Guía de evaluación le guiará por los pasos para crear una tabla optimizada para memoria almacenada en memoria y un procedimiento almacenado compilado de forma nativa que puede tener acceso a la tabla sin necesidad de que se compila o se interpreta.

### <a name="configure-database-for-in-memory-oltp"></a>Configurar la base de datos para OLTP en memoria
1. Se recomienda establecer la base de datos en un nivel de compatibilidad de al menos 130 para usar OLTP en memoria.  Use la siguiente consulta para comprobar el nivel de compatibilidad actual de AdventureWorks:  

   ```sql
   USE AdventureWorks
   GO
   SELECT d.compatibility_level
   FROM sys.databases as d
     WHERE d.name = Db_Name();
   GO
   ```
   
   Si es necesario, actualice el nivel 130:

   ```sql
   ALTER DATABASE CURRENT
   SET COMPATIBILITY_LEVEL = 130;
   GO
   ```

2. Cuando una transacción implica una tabla basada en disco y una tabla optimizada para memoria, es esencial que funcionan de la parte optimizada para memoria de la transacción en el nivel de aislamiento de transacción llamado SNAPSHOT.  Para aplicar de forma confiable este nivel para las tablas optimizadas para memoria en una transacción entre contenedores, ejecute lo siguiente:

   ```sql
   ALTER DATABASE CURRENT SET MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT=ON
   GO
   ```

3. Antes de poder crear una tabla optimizada para memoria, primero debe crear un grupo de archivos con optimización para memoria y un contenedor para los archivos de datos:

   ```sql
   ALTER DATABASE AdventureWorks ADD FILEGROUP AdventureWorks_mod CONTAINS memory_optimized_data
   GO  
   ALTER DATABASE AdventureWorks ADD FILE (NAME='AdventureWorks_mod', FILENAME='/var/opt/mssql/data/AdventureWorks_mod') TO FILEGROUP AdventureWorks_mod
   GO
   ```

### <a name="create-a-memory-optimized-table"></a>Crear una tabla optimizada para memoria
El almacén principal para las tablas optimizadas para memoria es memoria principal y, a diferencia de las tablas basadas en disco, no necesita datos para leerse desde el disco en búferes de memoria.  Para crear una tabla optimizada en memoria, utilice el MEMORY_OPTIMIZED = ON cláusula.

1. Ejecute la consulta siguiente para crear el dbo de la tabla optimizada para memoria. ShoppingCart.  De forma predeterminada, se conservarán los datos en disco por la durabilidad (tenga en cuenta que también se puede establecer la DURABILIDAD para conservar el esquema solamente). 

   ```sql
   CREATE TABLE dbo.ShoppingCart ( 
   ShoppingCartId INT IDENTITY(1,1) PRIMARY KEY NONCLUSTERED,
   UserId INT NOT NULL INDEX ix_UserId NONCLUSTERED HASH WITH (BUCKET_COUNT=1000000), 
   CreatedDate DATETIME2 NOT NULL, 
   TotalPrice MONEY
   ) WITH (MEMORY_OPTIMIZED=ON) 
   GO
   ```

2. Inserte algunos registros en la tabla:

   ```sql
   INSERT dbo.ShoppingCart VALUES (8798, SYSDATETIME(), NULL) 
   INSERT dbo.ShoppingCart VALUES (23, SYSDATETIME(), 45.4) 
   INSERT dbo.ShoppingCart VALUES (80, SYSDATETIME(), NULL) 
   INSERT dbo.ShoppingCart VALUES (342, SYSDATETIME(), 65.4) 
   ```

### <a name="natively-compiled-stored-procedure"></a>Procedimiento almacenado compilado de forma nativa
SQL Server admite procedimientos almacenados compilados de forma nativa que tienen acceso a tablas optimizadas para memoria. Las instrucciones de T-SQL se compilado en código máquina y se almacenan como archivos DLL nativos, lo que permite un acceso más rápido y ejecución de la consulta más eficaz que Transact-SQL tradicional.   Los procedimientos almacenados marcados con NATIVE_COMPILATION se compilan de forma nativa. 

1. Ejecute el siguiente script para crear un procedimiento almacenado compilado de forma nativa que inserta un gran número de registros en la tabla ShoppingCart:


   ```sql
   CREATE PROCEDURE dbo.usp_InsertSampleCarts @InsertCount int 
    WITH NATIVE_COMPILATION, SCHEMABINDING AS 
   BEGIN ATOMIC 
   WITH (TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE = N'us_english')

   DECLARE @i int = 0

   WHILE @i < @InsertCount 
    BEGIN 
     INSERT INTO dbo.ShoppingCart VALUES (1, SYSDATETIME() , NULL) 
     SET @i += 1 
    END
   END 
   ```
2. Insertar 1.000.000 de filas:

   ```sql
   EXEC usp_InsertSampleCarts 1000000 
   ```

3. Compruebe que las filas se han insertado:

   ```sql
   SELECT COUNT(*) FROM dbo.ShoppingCart 
   ```

### <a name="learn-more-about-in-memory-oltp"></a>Más información sobre OLTP en memoria
Para obtener más información sobre OLTP en memoria, vea los temas siguientes:

- [Inicio rápido 1: Tecnologías OLTP en memoria para acelerar el rendimiento de Transact-SQL](../relational-databases/in-memory-oltp/survey-of-initial-areas-in-in-memory-oltp.md)
- [Migrar a OLTP en memoria](../relational-databases/in-memory-oltp/migrating-to-in-memory-oltp.md)
- [Tabla temporal y variable de tabla más rápidas con optimización para memoria](../relational-databases/in-memory-oltp/faster-temp-table-and-table-variable-by-using-memory-optimization.md)
- [Supervisar y solucionar problemas de uso de memoria](../relational-databases/in-memory-oltp/monitor-and-troubleshoot-memory-usage.md)
- [OLTP en memoria (optimización en memoria)](../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)

## <a name="use-query-store"></a>Utilice Query Store
Query Store recopila información de rendimiento detallados acerca de las consultas, planes de ejecución y estadísticas en tiempo de ejecución.

Query Store no está activo de forma predeterminada y se puede habilitar con ALTER DATABASE:

   ```sql
   ALTER DATABASE AdventureWorks SET QUERY_STORE = ON;
   ```

Ejecute la siguiente consulta para devolver información acerca de las consultas y planes del almacén de consultas: 

   ```sql
   SELECT Txt.query_text_id, Txt.query_sql_text, Pl.plan_id, Qry.*
   FROM sys.query_store_plan AS Pl
      JOIN sys.query_store_query AS Qry
         ON Pl.query_id = Qry.query_id
      JOIN sys.query_store_query_text AS Txt
         ON Qry.query_text_id = Txt.query_text_id ;
   ```

## <a name="query-dynamic-management-views"></a>Vistas de administración dinámica de consultas
Vistas de administración dinámica devuelven información de estado de servidor que puede usarse para supervisar el estado de una instancia del servidor, diagnosticar problemas y optimizar el rendimiento.

Para consultar la vista de administración dinámica dm_os_wait estadísticas:

   ```sql
   SELECT wait_type, wait_time_ms
   FROM sys.dm_os_wait_stats;
   ```
