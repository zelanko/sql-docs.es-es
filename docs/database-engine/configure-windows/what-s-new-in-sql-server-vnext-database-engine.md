---
title: "Novedades de SQL Server vNext (motor de base de datos) | Microsoft Docs"
ms.custom: ""
ms.date: "03/13/2017"
ms.prod: "sql-vnext"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 42f45b23-6509-45e8-8ee7-76a78f99a920
caps.latest.revision: 15
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 13
---
# Novedades de SQL Server vNext (motor de base de datos)
[!INCLUDE[tsql-appliesto-ssvNxt-xxxx-xxxx-xxx](../../includes/tsql-appliesto-ssvnxt-xxxx-xxxx-xxx.md)]

**Nota:** SQL Server vNext además incluye las características agregadas en los Service Packs de SQL Server 2016. Para esos elementos, consulte [Novedades de SQL Server 2016 (motor de base de datos)](../../database-engine/configure-windows/what-s-new-in-sql-server-2016-database-engine.md).

## <a name="sql-server-database-engine-ctp-13"></a>Motor de base de datos de SQL Server (CTP 1.3)
- Mejoras en el rendimiento del punto de comprobación indirecto.
- Se agregó compatibilidad con grupos de disponibilidad sin clúster.
- Se agregó la configuración de los grupos de disponibilidad de confirmación de réplica mínima.
- Los grupos de disponibilidad ahora pueden funcionar entre Windows y Linux para habilitar las migraciones y pruebas entre distintos sistemas operativos.
- Se agregó compatibilidad con la directiva de retención de tablas temporales.
- Nuevo DMV SYS.DM_DB_STATS_HISTOGRAM.
- Se agregó compatibilidad con compilación y recompilación de índice de almacén de columnas no en clúster en línea.
- Cinco vistas de administración dinámica para devolver información sobre el proceso Linux. Para más información, consulte [Vistas de administración dinámica del proceso Linux](../../relational-databases/system-dynamic-management-views/linux-process-dynamic-management-views-transact-sql.md).   
- [sys.dm_db_stats_histogram (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-db-stats-histogram-transact-sql.md) se agregó para examinar las estadísticas.

## <a name="sql-server-database-engine-ctp-12"></a>Motor de base de datos de SQL Server (CTP 1.2)

- El Asesor de optimización de base de datos (DTA) que se lanzó con SQL Server Management Studio versión 16.4, cuando se analiza SQL Server 2016 y versiones posteriores, tiene opciones adicionales.    
   - Rendimiento mejorado. Para más información, consulte [Mejoras de rendimiento mediante las recomendaciones del Asistente para la optimización de motor de base de datos (DTA)](../../relational-databases/performance/performance-improvements-using-dta-recommendations.md).
   - La opción `-fc` para permitir las recomendaciones de los índices de almacén de columnas. Para más información, consulte [Utilidad DTA](../../tools/dta/dta-utility.md) y [Recomendaciones de índice de almacén de columnas en el Asistente para la optimización de motor de base de datos (DTA)](../../relational-databases/performance/columnstore-index-recommendations-in-database-engine-tuning-advisor-dta.md).  
   - La opción `-iq` para permitir que el DTA revise una carga de trabajo del Almacén de consultas. Para más información, consulte [Optimización de la base de datos mediante carga de trabajo del Almacén de consultas](../../relational-databases/performance/tuning-database-using-workload-from-query-store.md).
   

## <a name="sql-server-database-engine-ctp-11"></a>Motor de base de datos de SQL Server (CTP 1.1)

<a name="InMemoryBulletsCtp11"/>
- Para la funcionalidad In-Memory, las mejoras adicionales para las tablas con optimización para memoria y las funciones compiladas de forma nativa se muestran más abajo y los ejemplos de código están disponibles en el [texto situado a continuación](#InMemory_CodeSamples):
    - Compatibilidad con las columnas calculadas en tablas optimizadas para memoria, incluidos los índices en columnas calculadas.
    - Compatibilidad total con las funciones JSON en módulos compilados de forma nativa y en restricciones CHECK.
    - Operador `CROSS APPLY` en módulos compilados de forma nativa.   
- Se han agregado nuevas funciones de cadena [CONCAT_WS](../../t-sql/functions/concat-ws-transact-sql.md), [TRANSLATE](../../t-sql/functions/translate-transact-sql.md) y [TRIM](../../t-sql/functions/trim-transact-sql.md).   
- Ahora se admite la cláusula `WITHIN GROUP` para la función [STRING_AGG](../../t-sql/functions/string-agg-transact-sql.md).
- Se han agregado dos nuevas familias de intercalaciones japonesas (Japanese_Bushu_Kakusu_140 y Japanese_XJIS_140), así como la opción de intercalación con distinción de selector de variación (_VSS) para su uso en intercalaciones japonesas. Para obtener más información, consulte [Compatibilidad con la intercalación y Unicode](../../relational-databases/collations/collation-and-unicode-support.md).   
- Las nuevas opciones de acceso de forma masiva ([BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) y [OPENROWSET [BULK...]](../../t-sql/functions/openrowset-transact-sql.md)) permiten el acceso a los datos directamente desde un archivo especificado como formato CSV y desde archivos almacenados en Azure Blob Storage mediante la nueva opción `BLOB_STORAGE` de [EXTERNAL DATA SOURCE](../../t-sql/statements/create-external-data-source-transact-sql.md).


## <a name="sql-server-database-engine-ctp-10"></a>Motor de base de datos de SQL Server (CTP 1.0)

- Se ha agregado **COMPATIBILITY_LEVEL** de base de datos 140.   Los clientes que se ejecutan en este nivel obtendrán las características de lenguaje y los comportamientos del optimizador de consultas más recientes. Esto incluye cambios en cada versión preliminar que Microsoft publica.
- Mejoras en la manera en que los umbrales de actualización de estadísticas incrementales se calculan (necesario modo de compatibilidad&140;).
- Se ha agregado [sys.dm_exec_query_statistics_xml](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-statistics-xml-transact-sql.md).
- Se han agregado muchas mejoras de rendimiento y de lenguaje a las tablas en memoria:
    - `sp_spaceused` ya se admite en las tablas en memoria.
    - `sp_rename` ya se admite en los módulos nativos.
    - Ya se admiten instrucciones `CASE` en los módulos nativos.
    - Se ha quitado la limitación de ocho índices en las tablas en memoria.
    - `TOP (N) WITH TIES` ya se admite en los módulos nativos.
    - Ahora `ALTER TABLE` con las tablas en memoria es mucho más rápido en algunos casos.
    - La puesta al día de transacciones en las tablas en memoria ahora se hace en paralelo. Esto reduce considerablemente el tiempo necesario para hacer las conmutaciones por error o, en algunos casos, reinicia.
    - Los archivos de punto de comprobación en memoria ahora se pueden almacenar en el almacenamiento de Azure. Esto proporciona capacidades equivalentes a MDF si se compara con los archivos LDF, que ya tienen esta capacidad.
- Los índices de almacén de columnas en clúster ahora admiten columnas LOB (nvarchar(max), varchar(max), varbinary(max)).
- Se ha agregado la función de agregado [STRING_AGG](../../t-sql/functions/string-agg-transact-sql.md).  
- Nuevos permisos: `DATABASE SCOPED CREDENTIAL` es ahora una clase de objeto protegible, que admite permisos `CONTROL`, `ALTER`, `REFERENCES`, `TAKE OWNERSHIP` y `VIEW DEFINITION`. `ADMINISTER DATABASE BULK OPERATIONS` que está restringido a la base de datos SQL ahora está visible en `sys.fn_builtin_permissions`.   
- Se ha agregado la DMV [sys.dm_os_host_info](../../relational-databases/system-dynamic-management-views/sys-dm-os-host-info-transact-sql.md) para proporcionar información de sistema operativo para Windows y Linux.   
- Los roles de base de datos se crean con R Services para administrar los permisos asociados a paquetes. Para más información, vea [R Package management for SQL Server (Administración de paquetes de R para SQL Server)](../../advanced-analytics/r-services/r-package-management-for-sql-server-r-services.md).
 
<a name="InMemory_CodeSamples"/> 
## <a name="code-samples-for-new-in-memory-enhancements"></a>Ejemplos de código para las nuevas mejoras In-Memory

Las subsecciones siguientes proporcionan ejemplos de código Transact-SQL que ilustran las nuevas características In-Memory que aparecen listadas con viñetas en el texto precedente de este artículo.

La lista de viñetas CTP 1.1 para In-Memory se encuentra [aquí](#InMemoryBulletsCtp11).

#### <a name="computed-column-in-a-memory-optimized-table"></a>Columna calculada en una tabla con optimización para memoria

Esta instrucción CREATE TABLE muestra las siguientes características que se mencionaron en el texto precedente sobre CTP 1.1:

- Restricción CHECK JSON en una columna.
- Nuevas columnas calculadas.
- Un índice en una columna computada.

```tsql
CREATE TABLE Product(
    ProductID  int            PRIMARY KEY NONCLUSTERED,
    Name       nvarchar(400)  NOT NULL,
    Price      float,

    Data      nvarchar(4000)  CONSTRAINT [Data contains JSON]  CHECK (ISJSON(Data)=1),

    MadeIn  AS CAST(JSON_VALUE(Data, '$.MadeIn')            as NVARCHAR(50)) PERSISTED,
    Cost    AS CAST(JSON_VALUE(Data, '$.ManufacturingCost') as float       ),

    INDEX [idx_Product_MadeIn] NONCLUSTERED (MadeIn)
)
        WITH (MEMORY_OPTIMIZED=ON);
```

#### <a name="cross-apply-and-json-functions"></a>Funciones CROSS APPLY y JSON

Esta instrucción CREATE PROCEDURE, para un procedimiento almacenado y compilado de forma nativa, muestra las siguientes características que se mencionaron en el texto precedente sobre CTP 1.1:

- Operador CROSS APPLY.
- Funciones JSON.

```tsql
CREATE OR ALTER PROCEDURE ProductList()
    WITH SCHEMABINDING, NATIVE_COMPILATION
as begin
    atomic with (transaction isolation level = snapshot,  language = N'English')

    SELECT
            ProductID, Name, Price, Tags,
            Data,
            JSON_VALUE(Data,'$.MadeIn') AS MadeIn,
            value
        FROM Product
        CROSS APPLY OPENJSON(Data, '$.SalesReasons')
        FOR JSON PATH
end;
```
