---
title: Base de datos tempdb | Microsoft Docs
description: En este tema se proporcionan detalles relacionados con la configuración y el uso de la base de datos tempdb en SQL Server en Azure SQL Database.
ms.custom: P360
ms.date: 08/21/2019
ms.prod: sql
ms.prod_service: database-engine
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- temporary tables [SQL Server], tempdb database
- tempdb database [SQL Server], about tempdb
- temporary stored procedures [SQL Server]
- tempdb database [SQL Server]
ms.assetid: ce4053fb-e37a-4851-b711-8e504059a780
author: stevestein
ms.author: sstein
ms.reviewer: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 46807e551052ca6da38fde744d9a1e9dd7c794b0
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/30/2020
ms.locfileid: "79288499"
---
# <a name="tempdb-database"></a>Base de datos TempDB

[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

La base de datos del sistema **TempDB** es un recurso global disponible para todos los usuarios conectados a la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o a SQL Database. Tempdb se usa para contener:  
  
- **Objetos de usuario** temporales creados explícitamente, como: tablas e índices temporales locales o globales, procedimientos almacenados temporales, variables de tabla, tablas devueltas en funciones con valores de tabla o cursores.  
- **Objetos internos** que se crean mediante el motor de base de datos. Entre ellas se incluyen las siguientes:
  - Tablas de trabajo para almacenar resultados intermedios para colas, cursores, ordenaciones y almacenamiento temporal de objetos grandes (LOB).
  - Archivos de trabajo para operaciones de combinación hash o de agregado hash.
  - Resultados de orden intermedio de operaciones como crear o volver a generar índices (si se ha especificado SORT_IN_TEMPDB), o algunas consultas GROUP BY, ORDER BY o UNION.

  > [!NOTE]
  > Cada objeto interno usa un mínimo de nueve páginas, una página IAM y una extensión de ocho páginas. Para obtener más información acerca de las páginas y las extensiones, vea [Páginas y extensiones](../../relational-databases/pages-and-extents-architecture-guide.md#pages-and-extents).
  > [!IMPORTANT]
  > Los grupos elásticos y las bases de datos únicas de Azure SQL Database admiten tablas temporales globales y procedimientos almacenados temporales globales que se almacenan en TempDB y que tienen como ámbito el nivel de base de datos. Las tablas temporales globales y los procedimientos almacenados temporales globales se comparten entre todos los usuarios en la misma base de datos de Azure SQL. Las sesiones de usuario de otras bases de datos de Azure SQL no pueden acceder a tablas temporales globales. Para obtener más información, vea [Database scoped global temporary tables (Azure SQL Database)](../../t-sql/statements/create-table-transact-sql.md#database-scoped-global-temporary-tables-azure-sql-database) (Tablas temporales globales con ámbito de base de datos [Azure SQL Database]). [Instancia administrada de Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance) admite los mismos objetos temporales que SQL Server.
  > En el caso de los grupos elásticos y las bases de datos únicas de Azure SQL Database, solo se aplican la base de datos maestra y la base de datos TempDB. Para obtener más información, vea la [Qué es un servidor de Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-servers-databases#what-is-an-azure-sql-database-server). Para obtener una explicación de TempDB en el contexto de los grupos elásticos y las bases de datos únicas de Azure SQL Database, consulte [Base de datos TempDB](#tempdb-database-in-sql-database). En el caso de Instancia administrada de Azure SQL Database, se aplican todas las bases de datos del sistema.

- **Almacenes de versiones**, que son una colección de páginas de datos que contiene las filas de datos que son necesarias para admitir las características que utilizan versiones de fila. Hay dos almacenes de versiones: un almacén de versiones común y otro de generación de índices en línea. Los almacenes de versión contienen:
  - Versiones de fila generadas por las transacciones de modificación de datos en una base de datos que utiliza transacciones de lectura confirmada que usan transacciones de aislamiento de versiones de fila o de aislamiento de instantáneas.  
  - Versiones de fila que se generan mediante transacciones de modificación de datos para características como operaciones de índice en línea, conjuntos de resultados activos múltiples (MARS) y desencadenadores AFTER.  
  
Las operaciones de **TempDB** se registran de forma mínima, por lo que las transacciones se pueden revertir. **TempDB** se vuelve a crear cada vez que se inicia [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], de forma que el sistema siempre se inicia con una copia limpia de la base de datos. Las tablas y los procedimientos almacenados temporales se quitan automáticamente en la desconexión y ninguna conexión permanece activa cuando se cierra el sistema. Por tanto, en la base de datos **TempDB** no hay nada que deba guardarse de una a otra sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. No se permite realizar operaciones de copia de seguridad y restauración en **TempDB**.  

## <a name="physical-properties-of-tempdb-in-sql-server"></a>Propiedades físicas de TempDB en SQL Server

En la tabla siguiente se muestran los valores iniciales de configuración de los archivos de datos y registro de **TempDB** en SQL Server, que se basan en los valores predeterminados para la base de datos modelo. El tamaño de estos archivos puede variar ligeramente para diferentes ediciones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
|Archivo|Nombre lógico|Nombre físico|Tamaño inicial|Crecimiento del archivo|  
|----------|------------------|-------------------|------------------|-----------------|  
|Datos principales|tempdev|tempdb.mdf|8 megabytes|Crecimiento automático de 64 MB hasta llenar el disco.|  
|Archivos de datos secundarios*|temp#|tempdb_mssql_ # .ndf|8 megabytes|Crecimiento automático de 64 MB hasta llenar el disco.|  
|Log|templog|templog.ldf|8 megabytes|Crecimiento automático de 64 megabytes hasta un máximo de 2 terabytes.|  
  
\* El número de archivos depende del número de procesadores (lógicos) del equipo. Como regla general, si el número de procesadores lógicos es inferior o igual a ocho, use el mismo número de archivos de datos que procesadores lógicos. Si el número de procesadores lógicos es superior a ocho, use ocho archivos de datos y, después, si se mantiene la contención, aumente el número de archivos de datos en múltiplos de 4 hasta que la contención se reduzca a niveles aceptables, o bien modifique el código o la carga de trabajo.

> [!NOTE]
> El valor predeterminado para el número de archivos de datos se basa en las directrices [KB 2154845](https://support.microsoft.com/kb/2154845/).  
  
### <a name="moving-the-tempdb-data-and-log-files-in-sql-server"></a>Mover los archivos de datos y registro de TempDB en SQL Server

Para mover los archivos de registro y de datos de **TempDB**, consulte [Mover bases de datos del sistema](../../relational-databases/databases/move-system-databases.md).  
  
### <a name="database-options-for-tempdb-in-sql-server"></a>Opciones de base de datos de TempDB en SQL Server

En la siguiente tabla se muestra el valor predeterminado de las opciones de base de datos de la base de datos **TempDB** y se indica si la opción se puede modificar. Para ver la configuración actual de estas opciones, utilice la vista de catálogo [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) .  
  
|Opción de base de datos|Valor predeterminado|Se puede modificar|  
|---------------------|-------------------|---------------------|  
|ALLOW_SNAPSHOT_ISOLATION|Apagado|Sí|  
|ANSI_NULL_DEFAULT|Apagado|Sí|  
|ANSI_NULLS|Apagado|Sí|  
|ANSI_PADDING|Apagado|Sí|  
|ANSI_WARNINGS|Apagado|Sí|  
|ARITHABORT|Apagado|Sí|  
|AUTO_CLOSE|Apagado|No|  
|AUTO_CREATE_STATISTICS|ACTIVAR|Sí|  
|AUTO_SHRINK|Apagado|No|  
|AUTO_UPDATE_STATISTICS|ACTIVAR|Sí|  
|AUTO_UPDATE_STATISTICS_ASYNC|Apagado|Sí|  
|CHANGE_TRACKING|Apagado|No|  
|CONCAT_NULL_YIELDS_NULL|Apagado|Sí|  
|CURSOR_CLOSE_ON_COMMIT|Apagado|Sí|  
|CURSOR_DEFAULT|GLOBAL|Sí|  
|Opciones de disponibilidad de la base de datos|ONLINE<br /><br /> MULTI_USER<br /><br /> READ_WRITE|No<br /><br /> No<br /><br /> No|  
|DATE_CORRELATION_OPTIMIZATION|Apagado|Sí|  
|DB_CHAINING|ACTIVAR|No|  
|ENCRYPTION|Apagado|No|  
|MIXED_PAGE_ALLOCATION|Apagado|No|  
|NUMERIC_ROUNDABORT|Apagado|Sí|  
|PAGE_VERIFY|CHECKSUM para las nuevas instalaciones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /><br /> NONE para las actualizaciones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|Sí|  
|PARAMETERIZATION|SIMPLE|Sí|  
|QUOTED_IDENTIFIER|Apagado|Sí|  
|READ_COMMITTED_SNAPSHOT|Apagado|No|  
|RECOVERY|SIMPLE|No|  
|RECURSIVE_TRIGGERS|Apagado|Sí|  
|Opciones de Service Broker|ENABLE_BROKER|Sí|  
|TRUSTWORTHY|Apagado|No|  
  
Para obtener una descripción de estas opciones de la base de datos, vea [Opciones de ALTER DATABASE SET (Transact-SQL)](../../t-sql/statements/alter-database-transact-sql-set-options.md).  
  
## <a name="tempdb-database-in-sql-database"></a>Base de datos TempDB en SQL Database

### <a name="tempdb-sizes-for-dtu-based-service-tiers"></a>Tamaños de TempDB para los niveles de servicio basado en DTU

|SLO|Tamaño de archivo de datos de TempDB máximo (GB)|Número de archivos de datos de TempDB|Tamaño de datos de TempDB máximo (GB)|
|---|---:|---:|---:|
|Básica|13|1|13|
|S0|13|1|13|
|S1|13|1|13|
|S2|13|1|13|
|S3|32|1|32
|S4|32|2|64|
|S6|32|3|96|
|S7|32|6|192|
|S9|32|12|384|
|S12|32|12|384|
|P1|13|12|156|
|P2|13|12|156|
|P4|13|12|156|
|P6|13|12|156|
|P11|13|12|156|
|P15|13|12|156|
|Grupos elásticos premium (todas las configuraciones de DTU)|13|12|156|
|Grupos elásticos estándar (S0 a S2)|13|12|156|
|Grupos elásticos estándar (S3 y superior) |32|12|384|
|Grupos elásticos básicos (todas las configuraciones de DTU)|13|12|156|
||||

### <a name="tempdb-sizes-for-vcore-based-service-tiers"></a>Tamaños de TempDB para los niveles de servicio basado en núcleo virtual

Vea [Límites de recursos basados en núcleos virtuales](https://docs.microsoft.com/azure/sql-database/sql-database-vcore-resource-limits).

## <a name="restrictions"></a>Restricciones

En la base de datos **TempDB** no se pueden realizar las siguientes operaciones:  
  
- Agregar grupos de archivos
- Realizar una copia de seguridad o restaurar la base de datos
- Cambiar intercalaciones. La intercalación predeterminada es la intercalación de servidor
- Cambiar el propietario de la base de datos. **TempDB** es propiedad de **sa**
- Crear una instantánea de base de datos
- Quitar la base de datos.
- Eliminar el usuario **guest** de la base de datos
- Habilitar el mecanismo de captura de cambios en los datos
- Participar en el reflejo de la base de datos
- Quitar el grupo de archivos principal, el archivo de datos principal o el archivo de registro
- Cambiar el nombre de la base de datos o del grupo de archivos principal
- Ejecutar DBCC CHECKALLOC
- Ejecutar DBCC CHECKCATALOG
- Establecer la base de datos en OFFLINE
- Establecer la base de datos o el grupo de archivos principal en READ_ONLY
  
## <a name="permissions"></a>Permisos

Cualquier usuario puede crear objetos temporales en TempDB. Los usuarios solo pueden acceder a sus propios objetos, a menos que reciban permisos adicionales. Es posible revocar el permiso de conexión a TempDB para impedir que un usuario use TempDB, pero no es una práctica recomendada ya que algunas operaciones rutinarias necesitan el uso de TempDB.  

## <a name="optimizing-tempdb-performance-in-sql-server"></a>Optimizar el rendimiento de TempDB en SQL Server
El tamaño y la ubicación física de la base de datos TempDB puede afectar al rendimiento de un sistema. Por ejemplo, si el tamaño definido en TempDB es demasiado pequeño, parte de la carga de procesamiento del sistema puede deberse al crecimiento automático de TempDB hasta el tamaño necesario para admitir la carga de trabajo cada vez que se reinicia la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].

Siempre que sea posible, use la [inicialización de archivo instantáneo de la base de datos](../../relational-databases/databases/database-instant-file-initialization.md) para mejorar el rendimiento de las operaciones de crecimiento del archivo de datos.

Asigne espacio previamente para todos los archivos de TempDB estableciendo el tamaño de archivo en un valor lo suficientemente alto para acomodar la carga de trabajo habitual del entorno. La asignación previa evita que TempDB se expanda con demasiada frecuencia, lo que afecta al rendimiento. La base de datos TempDB debe establecerse de modo que crezca automáticamente, pero solo con el fin de aumentar el espacio en disco para las excepciones no previstas.

Los archivos de datos deberían ser del mismo tamaño dentro de cada [grupo de archivos](../../relational-databases/databases/database-files-and-filegroups.md#filegroups), ya que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utiliza un algoritmo de relleno proporcional que favorece las asignaciones en los archivos con más espacio libre. La división de TempDB en varios archivos de datos del mismo tamaño proporciona un alto grado de eficiencia paralela en las operaciones que usan TempDB.

Establezca el incremento de crecimiento de archivos en un tamaño razonable para evitar que los archivos de la base de datos TempDB crezcan en un porcentaje demasiado pequeño. Si el crecimiento de los archivos es demasiado pequeño comparado con la cantidad de datos que se escriben en TempDB, es posible que sea necesario expandir TempDB constantemente y que esto afecte al rendimiento.

Para comprobar los parámetros actuales de tamaño y de crecimiento de TempDB, use la consulta siguiente:

```sql
 SELECT name AS FileName,
    size*1.0/128 AS FileSizeInMB,
    CASE max_size
        WHEN 0 THEN 'Autogrowth is off.'
        WHEN -1 THEN 'Autogrowth is on.'
        ELSE 'Log file grows to a maximum size of 2 TB.'
    END,
    growth AS 'GrowthValue',
    'GrowthIncrement' =
        CASE
            WHEN growth = 0 THEN 'Size is fixed.'
            WHEN growth > 0 AND is_percent_growth = 0
                THEN 'Growth value is in 8-KB pages.'
            ELSE 'Growth value is a percentage.'
        END
FROM tempdb.sys.database_files;
GO
```

Coloque la base de datos TempDB en un subsistema de E/S rápido. Cree bandas en disco si hay muchos discos conectados directamente. No es necesario que los archivos de datos individuales o de grupos de TempDB estén en discos o ejes diferentes, a menos que también se estén produciendo cuellos de botella de E/S.

Coloque la base de datos TempDB en discos diferentes de los que utilizan las bases de datos de usuario.

## <a name="performance-improvements-in-tempdb-for-sql-server"></a>Mejoras de rendimiento de TempDB para SQL Server
A partir de [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], se optimiza el rendimiento de **TempDB** de las maneras siguientes:  
  
- Las tablas temporales y las variables de tabla se almacenan en caché. El almacenamiento en caché permite que las operaciones que quitan y crean los objetos temporales se ejecuten muy rápidamente y reduce la contención de la asignación de páginas  
- El protocolo de bloqueo temporal de página de asignación se ha mejorado para reducir el número de bloqueos temporales UP (actualizaciones).  
- Se reduce la sobrecarga del registro de **TempDB** para reducir el consumo de ancho de banda de E/S del disco en el archivo de registro de **TempDB**.  
- El programa de instalación agrega varios archivos de datos TempDB durante una instalación nueva de la instancia. Esta tarea puede realizarse con el nuevo control de entrada de la IU en la sección **Configuración del motor de base de datos** y un parámetro de línea de comandos `/SQLTEMPDBFILECOUNT`. De manera predeterminada, la configuración agrega tantos archivos de datos de TempDB como el número de procesadores lógicos u ocho, lo que sea menor.  
- Si hay varios archivos de datos **TempDB**, todos crecen automáticamente al mismo tiempo y la misma cantidad en función de la configuración de crecimiento. [La marca de seguimiento 1117](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) ya no es necesaria.  
- Todas las asignaciones de **TempDB** usarán extensiones uniformes. [La marca de seguimiento 1118](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) ya no es necesaria.  
- Para el grupo de archivos principal, la propiedad AUTOGROW_ALL_FILES se activa y la propiedad no se puede modificar.

Para más información sobre la mejora del rendimiento en TempDB, consulte el artículo de blog siguiente:

[TEMPDB - Files and Trace Flags and Updates, Oh My!](https://blogs.msdn.microsoft.com/sql_server_team/tempdb-files-and-trace-flags-and-updates-oh-my/) (TEMPDB: archivos, marcas de seguimiento y actualizaciones)

## <a name="memory-optimized-tempdb-metadata"></a>Metadatos tempdb optimizados para memoria
La contención de metadatos tempdb ha sido históricamente un cuello de botella en la escalabilidad para muchas cargas de trabajo que se ejecutan en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] introduce una nueva característica que forma parte de la familia de características [Base de datos en memoria](../in-memory-database.md), metadatos TempDB optimizados para memoria, que quita este cuello de botella de forma eficaz y desbloquea un nuevo nivel de escalabilidad para cargas de trabajo intensivas de TempDB. En [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)], las tablas del sistema implicadas en la administración de metadatos de la tabla temporal del sistema se pueden mover a tablas optimizadas para memoria no duraderas y sin bloqueos temporales.

Vea este vídeo de 7 minutos para obtener información general sobre cómo y cuándo usar los metadatos de TempDB con optimización para memoria:

> [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/How-and-When-To-Memory-Optimized-TempDB-Metadata/player?WT.mc_id=dataexposed-c9-niner]


Para poder participar en esta nueva característica, use el siguiente script:

```sql
ALTER SERVER CONFIGURATION SET MEMORY_OPTIMIZED TEMPDB_METADATA = ON 
```

Para que este cambio de configuración surta efecto, es necesario reiniciar el servicio.

Esta implementación presenta algunas limitaciones que cabe tener en cuenta:

1. Activar o desactivar la característica no es una acción dinámica. Debido a los cambios intrínsecos que deben realizarse en la estructura de TempDB, es necesario llevar a cabo un reinicio para habilitar o deshabilitar la característica.

2. Una única transacción no puede acceder a tablas optimizadas para memoria en más de una base de datos.  Esto significa que cualquier transacción que implique una tabla optimizada para memoria en una base de datos de usuario no podrá acceder a vistas del sistema tempdb en la misma transacción.  Si intenta acceder a vistas del sistema tempdb en la misma transacción en forma de tabla optimizada para memoria en una base de datos de usuario, recibirá el error siguiente:
    
    ```
    A user transaction that accesses memory optimized tables or natively compiled modules cannot access more than one user database or databases model and msdb, and it cannot write to master.
    ```
    
    Ejemplo:
    
    ```sql
    BEGIN TRAN
    SELECT *
    FROM tempdb.sys.tables  -----> Creates a user In-Memory OLTP Transaction on Tempdb
    INSERT INTO <user database>.<schema>.<mem-optimized table>
    VALUES (1)  ----> Attempts to create user In-Memory OLTP transaction but will fail
    COMMIT TRAN
    ```
    
3. Las consultas en tablas optimizadas para memoria no admiten las sugerencias de bloqueo y aislamiento, por lo que las consultas en vistas de catálogo tempdb optimizadas para memoria no respetarán dichas sugerencias. Como sucede con otras vistas de catálogo del sistema en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], todas las transacciones realizadas en vistas del sistema estarán en aislamiento READ COMMITTED (o, en este caso, READ COMMITTED SNAPSHOT).

4. Los [índices de almacén de columnas](../indexes/columnstore-indexes-overview.md) no se pueden crear en tablas temporales cuando los metadatos de TempDB optimizados para memoria están habilitados.

5. Debido a la limitación en los índices de almacén de columnas, no se admite el uso del procedimiento almacenado del sistema sp_estimate_data_compression_savings con el parámetro de compresión de datos COLUMNSTORE o COLUMNSTORE_ARCHIVE cuando se habilitan los metadatos de TempDB optimizados para memoria.

> [!NOTE] 
> Estas limitaciones solo se aplican al hacer referencia a vistas del sistema tempdb. Si lo desea, puede crear una tabla temporal en la misma transacción al acceder a una tabla optimizada para memoria en una base de datos de usuario.

Puede comprobar si tempdb está optimizado para memoria mediante el siguiente comando de T-SQL:
```
SELECT SERVERPROPERTY('IsTempdbMetadataMemoryOptimized')
```

Si se produce un error al iniciar el servidor por algún motivo después de habilitar los metadatos tempdb optimizados para memoria, se puede omitir la característica si inicia el servidor de SQL Server con [configuración mínima](../../database-engine/configure-windows/start-sql-server-with-minimal-configuration.md) con la opción de inicio **-f**. Esto le permitirá deshabilitar la característica y, después, reiniciar SQL Server en modo normal.

## <a name="capacity-planning-for-tempdb-in-sql-server"></a>Planeamiento de capacidad para TempDB en SQL Server
Determinar el tamaño adecuado para TempDB en un entorno de producción [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] depende de muchos factores. Como se ha descrito en el artículo anterior, estos factores incluyen la carga de trabajo existente y las características de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que se usan. Se recomienda analizar la carga de trabajo existente llevando a cabo las siguientes tareas en un entorno de prueba de SQL Server:

- Establezca el crecimiento automático en ON para TempDB.
- Ejecute consultas individuales o archivos de seguimiento de carga de trabajo y supervise el uso del espacio de TempDB.
- Ejecute operaciones de mantenimiento de índice, como volver a generar índices, y supervise el espacio de TempDB.
- Utilice los valores de uso de espacio de los pasos anteriores para predecir el uso de carga de trabajo total; ajuste este valor para la actividad simultánea proyectada y, a continuación, establezca el tamaño de TempDB según corresponda.

## <a name="how-to-monitor-tempdb-use"></a>Supervisión del uso de TempDB
Si se agota el espacio de disco de TempDB, se pueden producir interrupciones importantes en el entorno de producción de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y es posible que las aplicaciones en ejecución no puedan finalizar sus operaciones. Puede utilizar la vista de administración dinámica [sys.dm_db_file_space_usage](../../relational-databases/system-dynamic-management-views/sys-dm-db-session-space-usage-transact-sql.md) para supervisar el espacio en disco que utilizan los archivos de TempDB:

```sql
 -- Determining the Amount of Free Space in TempDB
SELECT SUM(unallocated_extent_page_count) AS [free pages],
  (SUM(unallocated_extent_page_count)*1.0/128) AS [free space in MB]
FROM sys.dm_db_file_space_usage;

-- Determining the Amount Space Used by the Version Store
SELECT SUM(version_store_reserved_page_count) AS [version store pages used],
  (SUM(version_store_reserved_page_count)*1.0/128) AS [version store space in MB]
FROM sys.dm_db_file_space_usage;

-- Determining the Amount of Space Used by Internal Objects
SELECT SUM(internal_object_reserved_page_count) AS [internal object pages used],
  (SUM(internal_object_reserved_page_count)*1.0/128) AS [internal object space in MB]
FROM sys.dm_db_file_space_usage;

-- Determining the Amount of Space Used by User Objects
SELECT SUM(user_object_reserved_page_count) AS [user object pages used],
  (SUM(user_object_reserved_page_count)*1.0/128) AS [user object space in MB]
FROM sys.dm_db_file_space_usage;
 ```

Asimismo, para supervisar la actividad de asignación o desasignación de páginas en TempDB en la sesión o tarea, se pueden utilizar las vistas de administración dinámica [sys.dm_db_session_space_usage](../../relational-databases/system-dynamic-management-views/sys-dm-db-session-space-usage-transact-sql.md) y [sys.dm_db_task_space_usage](../../relational-databases/system-dynamic-management-views/sys-dm-db-task-space-usage-transact-sql.md). Estas vistas pueden utilizarse para identificar consultas grandes, tablas temporales o variables de tabla que utilizan mucho espacio de disco de TempDB. También hay muchos contadores que se pueden utilizar para supervisar el espacio libre disponible en TempDB, así como los recursos que está utilizando TempDB. Para obtener más información, vea la próxima sección.

```sql
-- Obtaining the space consumed by internal objects in all currently running tasks in each session
SELECT session_id,
  SUM(internal_objects_alloc_page_count) AS task_internal_objects_alloc_page_count,
  SUM(internal_objects_dealloc_page_count) AS task_internal_objects_dealloc_page_count
FROM sys.dm_db_task_space_usage
GROUP BY session_id;

-- Obtaining the space consumed by internal objects in the current session for both running and completed tasks
SELECT R2.session_id,
  R1.internal_objects_alloc_page_count
  + SUM(R2.internal_objects_alloc_page_count) AS session_internal_objects_alloc_page_count,
  R1.internal_objects_dealloc_page_count
  + SUM(R2.internal_objects_dealloc_page_count) AS session_internal_objects_dealloc_page_count
FROM sys.dm_db_session_space_usage AS R1
INNER JOIN sys.dm_db_task_space_usage AS R2 ON R1.session_id = R2.session_id
GROUP BY R2.session_id, R1.internal_objects_alloc_page_count,
  R1.internal_objects_dealloc_page_count;;
```

## <a name="related-content"></a>Contenido relacionado
[Opción SORT_IN_TEMPDB para índices](../../relational-databases/indexes/sort-in-TempDB-option-for-indexes.md)    
[Bases de datos del sistema](../../relational-databases/databases/system-databases.md)    
[sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)    
[sys.master_files](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md)    
[Mover archivos de base de datos](../../relational-databases/databases/move-database-files.md)    
  
