---
title: Desfragmentación de índices de almacén de columnas | Microsoft Docs
ms.custom: ''
ms.date: 01/27/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
ms.assetid: d3efda1a-7bdb-47f5-80bf-f075329edee5
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: c33b07af2ad43f15913580ce55c173d04a876366
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/28/2018
ms.locfileid: "52511540"
---
# <a name="columnstore-indexes---defragmentation"></a>Desfragmentación de índices de almacén de columnas
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Tareas para desfragmentar índices de almacén de columnas.  
  
## <a name="use-alter-index-reorganize-to-defragment-a-columnstore-index-online"></a>Usar ALTER INDEX REORGANIZE para desfragmentar un índice de almacén de columnas en línea  
 **Se aplica a:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (a partir de [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]), [!INCLUDE[ssSDS](../../includes/sssds-md.md)]  
  
Después de realizar cargas de cualquier tipo, puede haber varios grupos de filas pequeños en el almacén delta. Puede usar `ALTER INDEX REORGANIZE` para forzar a todos los grupos de filas al almacén de columnas y luego combinar los grupos de filas en menos grupos de filas con más filas.  La operación de reorganización también quitará las filas que se hayan eliminado del almacén de columnas.  
  
Para obtener más información, consulte las siguientes entradas de blog en el blog de equipo del motor de base de datos de SQL.  
-   [Minimización de la fragmentación en índices de almacén de columnas](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/03/07/columnstore-index-defragmentation-using-reorganize-command/)  
-   [Índices de almacén de columnas y directiva de combinación de grupos de filas](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/03/08/columnstore-index-merge-policy-for-reorganize/)  
  
### <a name="recommendations-for-reorganizing"></a>Recomendaciones para reorganizar  
Reorganice un índice de almacén de columnas después de una o varias cargas de datos para obtener mejoras en el rendimiento de las consultas lo más rápidamente posible. Inicialmente, el proceso de reorganización requerirá recursos de CPU adicionales para comprimir los datos, lo que podría reducir el rendimiento general del sistema. Sin embargo, tan pronto como los datos están comprimidos, el rendimiento de las consultas puede mejorar.  
  
Use el ejemplo de [sys.dm_db_column_store_row_group_physical_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-column-store-row-group-physical-stats-transact-sql.md) para calcular la fragmentación. Esto le ayudará a determinar si merece la pena realizar una operación REORGANIZE.  
  
### <a name="example-how-reorganizing-works"></a>Ejemplo: funcionamiento de la reorganización  
 En este ejemplo se muestra cómo ALTER INDEX REORGANIZE puede forzar a todos los grupos de filas del almacén delta al almacén de columnas y luego combinar los grupos de filas.  
  
1.  Ejecute este Transact-SQL para crear una tabla de almacenamiento provisional con 300.000 filas. Se usará para cargar filas de forma masiva en un índice de almacén de columnas.  
  
    ```sql  
    USE master;  
    GO  
  
    IF EXISTS (SELECT name FROM sys.databases  
        WHERE name = N'[columnstore]')  
        DROP DATABASE [columnstore];  
    GO  
  
    CREATE DATABASE [columnstore];  
    GO  
  
    IF EXISTS (SELECT name FROM sys.tables  
        WHERE name = N'staging'  
        AND object_id = OBJECT_ID (N'staging'))  
    DROP TABLE dbo.staging;  
    GO  
  
    CREATE TABLE [staging] (  
         AccountKey int NOT NULL,  
         AccountDescription nvarchar (50),  
         AccountType nvarchar(50),  
         AccountCodeAlternateKey int  
    );  
    GO  
  
    -- Load data  
    DECLARE @loop int;  
    DECLARE @AccountDescription varchar(50);  
    DECLARE @AccountKey int;  
    DECLARE @AccountType varchar(50);  
    DECLARE @AccountCode int;  
  
    SELECT @loop = 0;  
    BEGIN TRAN  
        WHILE (@loop < 300000)   
          BEGIN  
            SELECT @AccountKey = CAST (RAND()*10000000 AS int);  
            SELECT @AccountDescription = 'accountdesc ' + CONVERT(varchar(20), @AccountKey);  
            SELECT @AccountType = 'AccountType ' + CONVERT(varchar(20), @AccountKey);  
            SELECT @AccountCode =  CAST (RAND()*10000000 AS int);  
  
            INSERT INTO staging VALUES (  
               @AccountKey,   
               @AccountDescription,   
               @AccountType,   
               @AccountCode  
            );  
  
            SELECT @loop = @loop + 1;  
          END  
    COMMIT  
    ```  
  
2.  Cree una tabla almacenada como un índice de almacén de columnas.  
  
    ```sql  
    IF EXISTS (SELECT name FROM sys.tables  
        WHERE name = N'cci_target'  
        AND object_id = OBJECT_ID (N'cci_target'))  
    DROP TABLE dbo.cci_target;  
    GO  
  
    -- Create a table with a clustered columnstore index  
    -- and the same columns as the rowstore staging table.  
    CREATE TABLE cci_target (  
         AccountKey int NOT NULL,  
         AccountDescription nvarchar (50),  
         AccountType nvarchar(50),  
         AccountCodeAlternateKey int,  
         INDEX idx_cci_target CLUSTERED COLUMNSTORE  
    )  
    GO  
    ```  
  
3.  Inserte de forma masiva las filas de la tabla de almacenamiento provisional en la tabla de almacén de columnas. `INSERT INTO ... SELECT` realiza una inserción masiva. `TABLOCK` permite que `INSERT` se ejecute con paralelismo.  
  
    ```sql  
    -- Insert rows in parallel  
    INSERT INTO cci_target WITH (TABLOCK)  
    SELECT TOP (300000) * FROM staging;  
    GO  
    ```  
  
4.  Vea los grupos de filas mediante la vista de administración dinámica (DMV) *sys.dm_db_column_store_row_group_physical_stats*.  
  
    ```sql  
    -- Run this dynamic management view (DMV) to see the OPEN rowgroups.   
    -- The number of rowgroups depends on the degree of parallelism.   
    -- You will see multiple OPEN rowgroups depending on the degree of parallelism.   
    -- This is because insert operation can run in parallel in [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)].  
  
    SELECT *   
    FROM sys.dm_db_column_store_row_group_physical_stats   
    WHERE object_id  = object_id('cci_target')  
    ORDER BY row_group_id;  
    ```  
  
     En este ejemplo, los resultados muestran 8 grupos de filas OPEN con 37.500 filas cada uno. El número de grupos de filas OPEN depende de la configuración de *max_degree_of_parallelism*.  
  
     ![Grupos de filas Open](../../relational-databases/indexes/media/cci-openrowgroups.png "Grupos de filas Open")  
  
5.  Use `ALTER INDEX REORGANIZE` con la opción `COMPRESS_ALL_ROW_GROUPS` para forzar la compresión de todos los grupos de filas en el almacén de columnas.  
  
    ```sql  
    -- This command will force all CLOSED and OPEN rowgroups into the columnstore.  
    ALTER INDEX idx_cci_target ON cci_target   
    REORGANIZE WITH (COMPRESS_ALL_ROW_GROUPS = ON);  
  
    SELECT *   
    FROM sys.dm_db_column_store_row_group_physical_stats   
    WHERE object_id  = object_id('cci_target')  
    ORDER BY row_group_id;  
    ```  
  
     Los resultados muestran 8 grupos de filas COMPRESSED y 8 grupos de filas TOMBSTONE. Cada grupo de filas se comprimió en el almacén de columnas independientemente de su tamaño. El sistema quitará los grupos de filas TOMBSTONE.  
  
     ![Grupos de filas TOMBSTONE y COMPRESSED](../../relational-databases/indexes/media/cci-tombstone-compressed-rowgroups.png "Grupos de filas TOMBSTONE y COMPRESSED")  
  
6.  Para el rendimiento de las consultas es mucho mejor combinar pequeños grupos de filas. `ALTER INDEX REORGANIZE` combinará los grupos de filas `COMPRESSED`. Ahora que los grupos de filas delta están comprimidos en el almacén de columnas, vuelva a ejecutar ALTER INDEX REORGANIZE para combinar los grupos de filas pequeños COMPRESSED. Esta vez no es necesario usar la opción `COMPRESS_ALL_ROW_GROUPS`.  
  
    ```sql  
    -- Run this again and you will see that smaller rowgroups   
    -- combined into one compressed rowgroup with 300,000 rows  
    ALTER INDEX idx_cci_target ON cci_target REORGANIZE;  
  
    SELECT *   
    FROM sys.dm_db_column_store_row_group_physical_stats   
    WHERE object_id  = object_id('cci_target')  
    ORDER BY row_group_id;  
    ```  
  
     Los resultados muestran que ahora los 8 grupos de filas COMPRESSED están combinados en un grupo de filas COMPRESSED.  
  
     ![Grupos de filas combinados](../../relational-databases/indexes/media/cci-compressed-rowgroups.png "Grupos de filas combinados")  
  
## <a name="rebuild"></a> Usar ALTER INDEX REBUILD para desfragmentar el índice de almacén de columnas sin conexión  
 En SQL [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] y versiones posteriores, normalmente no es necesario volver a generar el índice de almacén de columnas, ya que `REORGANIZE` realiza las operaciones básicas de una recompilación en segundo plano como una operación en línea.  
  
 La recompilación de un índice de almacén de columnas quita la fragmentación y mueve todas las filas al almacén de columnas. Puede usar [CREATE COLUMNSTORE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-columnstore-index-transact-sql.md) o [ALTER INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md) para volver a generar completamente un índice agrupado de almacén de columnas existente. Además, puede usar ALTER INDEX... REBUILD para volver a crear una partición específica.  
  
### <a name="rebuild-process"></a>Proceso de regeneración  
 Para volver a generar un índice de almacén de columnas, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
1.  Adquiere un bloqueo exclusivo en la tabla o la partición mientras se produce la regeneración. Los datos están "desconectados" y no disponibles durante la recompilación, aunque se use `NOLOCK`, RCSI o SI.  
  
2.  Vuelve a comprimir todos los datos del almacén de columnas. Hay dos copias del índice de almacén de columnas mientras se está produciendo la regeneración. Cuando se finaliza la recopilación, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] elimina el índice original del almacén de columnas.  
  
### <a name="recommendations-for-rebuilding-a-columnstore-index"></a>Recomendaciones para volver a generar un índice de almacén de columnas  
 Volver a generar un índice de almacén de columnas es útil para quitar la fragmentación y para mover todas las filas al almacén de columnas. Siga estas recomendaciones:  
  
1.  Vuelva a generar una partición en lugar de la tabla completa.  
    -   Volver a generar la tabla completa tarda mucho si el índice es grande y requiere el espacio en disco suficiente para almacenar una copia adicional del índice durante la regeneración. Por lo general, solo es necesario volver a generar la partición que se ha usado más recientemente.  
    -   Para las tablas con particiones, no es necesario que vuelva a generar el índice de almacén de columnas completo, ya que es probable que se produzca la fragmentación solo en las particiones que se han modificado recientemente. Las tablas de hechos y las tablas de dimensiones de gran tamaño normalmente tienen particiones para poder realizar operaciones de copia de seguridad y de administración con los fragmentos de la tabla.  

2.  Vuelva a generar una partición después de haber realizado operaciones DML intensivas.  
    -   La regeneración de una partición desfragmentará la partición y reducirá el almacenamiento de disco. La recompilación eliminará todas las filas del almacén de columnas que están marcadas para eliminación y trasladará todos los grupos de filas del almacén delta al almacén de columnas. Tenga en cuenta que puede haber varios grupos de filas en el almacén delta con menos de un millón de filas cada uno.  
  
3.  Vuelva a generar una partición después de cargar los datos.  
    -   Esto garantiza que todos los datos se almacenan en el almacén de columnas. Cuando cada proceso simultáneo carga al mismo tiempo menos de 100.000 filas en la misma partición, esta puede acabar con varios almacenes delta. La regeneración trasladará todas las filas del almacén delta al almacén de columnas.  

## <a name="automatic-index-and-statistics-management"></a>Administración automática de índice y estadísticas

Aproveche soluciones como la [desfragmentación de índice adaptable](https://github.com/Microsoft/tigertoolbox/tree/master/AdaptiveIndexDefrag) para administrar automáticamente las actualizaciones de estadísticas y la desfragmentación de índices para una o varias bases de datos. Este procedimiento elige automáticamente si se debe volver a generar o reorganizar un índice según su nivel de fragmentación, entre otros parámetros y actualiza las estadísticas con un umbral lineal.

## <a name="see-also"></a>Ver también        
[Novedades de los índices de almacén de columnas](../../relational-databases/indexes/columnstore-indexes-what-s-new.md)    
[Rendimiento de las consultas de índices de almacén de columnas](../../relational-databases/indexes/columnstore-indexes-query-performance.md)   
[Introducción al almacén de columnas para análisis operativos en tiempo real](../../relational-databases/indexes/get-started-with-columnstore-for-real-time-operational-analytics.md)   
[Índices de almacén de columnas para el almacenamiento de datos](../../relational-databases/indexes/columnstore-indexes-data-warehouse.md)  
[Diseño de los índices de almacén de columnas](../../relational-databases/sql-server-index-design-guide.md#columnstore_index)    
[Desfragmentación de índice adaptable](https://github.com/Microsoft/tigertoolbox/tree/master/AdaptiveIndexDefrag)    
  
  
