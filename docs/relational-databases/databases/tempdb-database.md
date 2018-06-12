---
title: Base de datos tempdb | Microsoft Docs
description: En este tema se proporcionan detalles relacionados con la configuración y el uso de la base de datos tempdb en SQL Server en Azure SQL Database.
ms.custom: P360
ms.date: 12/19/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: databases
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- temporary tables [SQL Server], tempdb database
- tempdb database [SQL Server], about tempdb
- temporary stored procedures [SQL Server]
- tempdb database [SQL Server]
ms.assetid: ce4053fb-e37a-4851-b711-8e504059a780
author: stevestein
ms.author: sstein
manager: craigg
ms.reviewer: carlrab
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 98e93ce7e85d6c027e2b9b347ff54425440d2674
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/04/2018
ms.locfileid: "34582327"
---
# <a name="tempdb-database"></a>Base de datos tempdb
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  La base de datos del sistema **tempdb** es un recurso global disponible para todos los usuarios conectados a la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o a SQL Database. Tempdb se usa para contener:  
  
- **Objetos de usuario** temporales creados explícitamente, como: tablas e índices temporales locales o globales, procedimientos almacenados temporales, variables de tabla, tablas devueltas en funciones con valores de tabla o cursores.  
- **Objetos internos** que se crean mediante el motor de base de datos. Estos incluyen:
  - Tablas de trabajo para almacenar resultados intermedios para colas, cursores, ordenaciones y almacenamiento temporal de objetos grandes (LOB).
  - Archivos de trabajo para operaciones de combinación hash o de agregado hash.
  - Resultados de orden intermedio de operaciones como crear o volver a generar índices (si se ha especificado SORT_IN_TEMPDB), o algunas consultas GROUP BY, ORDER BY o UNION.

  > [!NOTE]
  > Cada objeto interno usa un mínimo de nueve páginas, una página IAM y una extensión de ocho páginas. Para obtener más información acerca de las páginas y las extensiones, vea [Páginas y extensiones](../../relational-databases/pages-and-extents-architecture-guide.md#pages-and-extents).

  > [!IMPORTANT]
  > Azure SQL Database admite tablas temporales globales y procedimientos almacenados temporales globales que se almacenan en tempdb y que tienen como ámbito el nivel de base de datos. Las tablas temporales globales y los procedimientos almacenados temporales globales se comparten entre todos los usuarios en la misma base de datos de Azure SQL. Las sesiones de usuario de otras bases de datos de Azure SQL no pueden acceder a tablas temporales globales. Para obtener más información, vea [Database scoped global temporary tables (Azure SQL Database)](../../t-sql/statements/create-table-transact-sql.md#database-scoped-global-temporary-tables-azure-sql-database) (Tablas temporales globales con ámbito de base de datos [Azure SQL Database]).

- **Almacenes de versiones**, que son una colección de páginas de datos que contiene las filas de datos que son necesarias para admitir las características que utilizan versiones de fila. Hay dos almacenes de versiones: un almacén de versiones común y otro de generación de índices en línea. Los almacenes de versión contienen:
  - Versiones de fila generadas por las transacciones de modificación de datos en una base de datos que utiliza transacciones de lectura confirmada que usan transacciones de aislamiento de versiones de fila o de aislamiento de instantáneas.  
  - Versiones de fila que se generan mediante transacciones de modificación de datos para características como operaciones de índice en línea, conjuntos de resultados activos múltiples (MARS) y desencadenadores AFTER.  
  
Las operaciones de **tempdb** se registran de forma mínima, por lo que las transacciones se pueden revertir. **tempdb** se vuelve a crear cada vez que se inicia [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , de forma que el sistema siempre se inicia con una copia limpia de la base de datos. Las tablas y los procedimientos almacenados temporales se quitan automáticamente en la desconexión y ninguna conexión permanece activa cuando se cierra el sistema. Por tanto, en la base de datos **tempdb** no hay nada que deba guardarse de una a otra sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . No se permite realizar operaciones de copia de seguridad y restauración en **tempdb**.  
  
## <a name="physical-properties-of-tempdb-in-sql-server"></a>Propiedades físicas de tempdb en SQL Server
 En la tabla siguiente se muestran los valores iniciales de configuración de los archivos de datos y registro de **tempdb** en SQL Server, que se basan en los valores predeterminados para la base de datos modelo. El tamaño de estos archivos puede variar ligeramente para diferentes ediciones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
|Archivo|Nombre lógico|Nombre físico|Tamaño inicial|Crecimiento del archivo|  
|----------|------------------|-------------------|------------------|-----------------|  
|Datos principales|tempdev|tempdb.mdf|8 megabytes|Crecimiento automático de 64 MB hasta llenar el disco.|  
|Archivos de datos secundarios*|temp#|tempdb_mssql_ # .ndf|8 megabytes|Crecimiento automático de 64 MB hasta llenar el disco.|  
|Log|templog|templog.ldf|8 megabytes|Crecimiento automático de 64 megabytes hasta un máximo de 2 terabytes.|  
  
 \* El número de archivos depende del número de procesadores (lógicos) del equipo. Como regla general, si el número de procesadores lógicos es inferior o igual a ocho, use el mismo número de archivos de datos que procesadores lógicos. Si el número de procesadores lógicos es superior a ocho, use ocho archivos de datos y, después, si se mantiene la contención, aumente el número de archivos de datos en múltiplos de 4 hasta que la contención se reduzca a niveles aceptables, o bien modifique el código o la carga de trabajo.

> [!NOTE]
> El valor predeterminado para el número de archivos de datos se basa en las directrices [KB 2154845](http://support.microsoft.com/kb/2154845/).  
  
### <a name="moving-the-tempdb-data-and-log-files-in-sql-server"></a>Mover los archivos de datos y registro de tempdb en SQL Server  
 Para mover los archivos de registro y de datos de **tempdb** , vea [Mover bases de datos del sistema](../../relational-databases/databases/move-system-databases.md).  
  
### <a name="database-options-for-tempdb-in-sql-server"></a>Opciones de base de datos de tempdb en SQL Server  
 En la siguiente tabla se muestra el valor predeterminado de las opciones de base de datos de la base de datos **tempdb** y se indica si la opción se puede modificar. Para ver la configuración actual de estas opciones, utilice la vista de catálogo [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) .  
  
|Opción de base de datos|Valor predeterminado|Se puede modificar|  
|---------------------|-------------------|---------------------|  
|ALLOW_SNAPSHOT_ISOLATION|OFF|Sí|  
|ANSI_NULL_DEFAULT|OFF|Sí|  
|ANSI_NULLS|OFF|Sí|  
|ANSI_PADDING|OFF|Sí|  
|ANSI_WARNINGS|OFF|Sí|  
|ARITHABORT|OFF|Sí|  
|AUTO_CLOSE|OFF|no|  
|AUTO_CREATE_STATISTICS|ON|Sí|  
|AUTO_SHRINK|OFF|no|  
|AUTO_UPDATE_STATISTICS|ON|Sí|  
|AUTO_UPDATE_STATISTICS_ASYNC|OFF|Sí|  
|CHANGE_TRACKING|OFF|no|  
|CONCAT_NULL_YIELDS_NULL|OFF|Sí|  
|CURSOR_CLOSE_ON_COMMIT|OFF|Sí|  
|CURSOR_DEFAULT|GLOBAL|Sí|  
|Opciones de disponibilidad de la base de datos|ONLINE<br /><br /> MULTI_USER<br /><br /> READ_WRITE|no<br /><br /> no<br /><br /> no|  
|DATE_CORRELATION_OPTIMIZATION|OFF|Sí|  
|DB_CHAINING|ON|no|  
|ENCRYPTION|OFF|no|  
|MIXED_PAGE_ALLOCATION|OFF|no|  
|NUMERIC_ROUNDABORT|OFF|Sí|  
|PAGE_VERIFY|CHECKSUM para las nuevas instalaciones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /><br /> NONE para las actualizaciones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|Sí|  
|PARAMETERIZATION|SIMPLE|Sí|  
|QUOTED_IDENTIFIER|OFF|Sí|  
|READ_COMMITTED_SNAPSHOT|OFF|no|  
|RECOVERY|SIMPLE|no|  
|RECURSIVE_TRIGGERS|OFF|Sí|  
|Opciones de Service Broker|ENABLE_BROKER|Sí|  
|TRUSTWORTHY|OFF|no|  
  
 Para obtener una descripción de estas opciones de la base de datos, vea [Opciones de ALTER DATABASE SET (Transact-SQL)](../../t-sql/statements/alter-database-transact-sql-set-options.md).  
  
## <a name="tempdb-database-in-sql-database"></a>Base de datos tempdb en SQL Database


### <a name="tempdb-sizes-for-dtu-based-service-tiers"></a>tamaños de tempdb para los niveles de servicio basado en DTU

|SLO|Tamaño de archivo de datos de tempdb máximo (MB)|Número de archivos de datos de tempdb|Tamaño máximo de datos de tempdb (MB)|
|---|---:|---:|---:|
|Básico|14 225|1|14 225|
|S0|14 225|1|14 225| 
|S1|14 225|1|14 225| 
|S2|14 225| 1|14 225| 
|S3|32 768|1|32 768| 
|S4|32 768|2|65,536| 
|S6|32 768|3|98304| 
|S7|32 768|6|196 608| 
|S9|32 768|12|393 216| 
|S12|32 768|12|393 216| 
|P1|32 768|12|393 216| 
|P2|32 768|12|393 216| 
|P4|32 768|12|393 216| 
|P6|32 768|12|393 216| 
|P11|32 768|12|393 216| 
|P15|32 768|12|393 216| 
|Grupos elásticos premium (todas las configuraciones de DTU)|14 225|12|170 700| 
|Grupos elásticos estándar (todas las configuraciones de DTU)|14 225|12|170 700| 
|Grupos elásticos básicos (todas las configuraciones de DTU)|14 225|12|170 700| 
||||

### <a name="tempdb-sizes-for-vcore-based-service-tiers"></a>tamaños de tempdb para los niveles de servicio basado en núcleo virtual

Vea [Límites de recursos basados en núcleos virtuales](https://docs.microsoft.com/azure/sql-database/sql-database-vcore-resource-limits).

## <a name="restrictions"></a>Restrictions  
 En la base de datos **tempdb** no se pueden realizar las siguientes operaciones:  
  
- Agregar grupos de archivos.  
- Realizar una copia de seguridad o restaurar la base de datos.  
- Cambiar intercalaciones. La intercalación predeterminada es la intercalación de servidor.  
- Cambiar el propietario de la base de datos. **tempdb** es propiedad de **sa**.  
- Crear una instantánea de base de datos.  
- Eliminar la base de datos.  
- Eliminar el usuario **guest** de la base de datos.  
- Habilitar el mecanismo de captura de cambios en los datos.  
- Participar en el reflejo de la base de datos.  
- Quitar el grupo de archivos principal, el archivo de datos principal o el archivo de registro.  
- Cambiar el nombre de la base de datos o del grupo de archivos principal.  
- Ejecutar DBCC CHECKALLOC.  
- Ejecutar DBCC CHECKCATALOG.  
- Establecer la base de datos en OFFLINE.  
- Establecer la base de datos o el grupo de archivos principal en READ_ONLY.  
  
## <a name="permissions"></a>Permisos  
 Cualquier usuario puede crear objetos temporales en tempdb. Los usuarios solo pueden acceder a sus propios objetos, a menos que reciban permisos adicionales. Es posible revocar el permiso de conexión a tempdb para impedir que un usuario use tempdb, pero no es una práctica recomendada ya que algunas operaciones rutinarias necesitan el uso de tempdb.  

## <a name="optimizing-tempdb-performance-in-sql-server"></a>Optimizar el rendimiento de tempdb en SQL Server 
 El tamaño y la ubicación física de la base de datos tempdb puede afectar al rendimiento de un sistema. Por ejemplo, si el tamaño definido en tempdb es demasiado pequeño, parte de la carga de procesamiento del sistema puede deberse al crecimiento automático de tempdb hasta el tamaño necesario para admitir la carga de trabajo cada vez que se reinicia la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].

 Siempre que sea posible, use la [inicialización de archivo instantáneo de la base de datos](../../relational-databases/databases/database-instant-file-initialization.md) para mejorar el rendimiento de las operaciones de crecimiento del archivo de datos.
 
 Asigne espacio previamente para todos los archivos de tempdb estableciendo el tamaño de archivo en un valor lo suficientemente alto para acomodar la carga de trabajo habitual del entorno. La asignación previa evita que tempdb se expanda con demasiada frecuencia, lo que afecta al rendimiento. La base de datos tempdb debe establecerse de modo que crezca automáticamente, pero solo con el fin de aumentar el espacio en disco para las excepciones no previstas. 

 Los archivos de datos deberían ser del mismo tamaño dentro de cada [grupo de archivos](../../relational-databases/databases/database-files-and-filegroups.md#filegroups), ya que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utiliza un algoritmo de relleno proporcional que favorece las asignaciones en los archivos con más espacio libre. La división de tempdb en varios archivos de datos del mismo tamaño proporciona un alto grado de eficiencia paralela en las operaciones que usan tempdb. 
 
 Establezca el incremento de crecimiento de archivos en un tamaño razonable para evitar que los archivos de la base de datos tempdb crezcan en un porcentaje demasiado pequeño. Si el crecimiento de los archivos es demasiado pequeño comparado con la cantidad de datos que se escriben en tempdb, es posible que sea necesario expandir tempdb constantemente y que esto afecte al rendimiento.
 
 Para comprobar los parámetros actuales de tamaño y de crecimiento de tempdb, use la consulta siguiente:
 ```sql
 SELECT name AS FileName, 
    size*1.0/128 AS FileSizeinMB,
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
 
 Coloque la base de datos tempdb en un subsistema de E/S rápido. Cree bandas en disco si hay muchos discos conectados directamente. No es necesario que los archivos de datos individuales o de grupos de tempdb estén en discos o ejes diferentes, a menos que también se estén produciendo cuellos de botella de E/S.
 
 Coloque la base de datos tempdb en discos diferentes de los que utilizan las bases de datos de usuario.

## <a name="performance-improvements-in-tempdb-for-sql-server"></a>Mejoras de rendimiento de tempdb para SQL Server 
 A partir de [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], se optimiza el rendimiento de **tempdb** de las maneras siguientes:  
  
- Las tablas temporales y las variables de tabla se almacenan en caché. El almacenamiento en caché permite que las operaciones que quitan y crean los objetos temporales se ejecuten muy rápidamente y reduce la contención de la asignación de páginas  
- El protocolo de bloqueo temporal de página de asignación se ha mejorado para reducir el número de bloqueos temporales UP (actualizaciones).  
- Se reduce la sobrecarga del registro de **tempdb** para reducir el consumo de ancho de banda de E/S del disco en el archivo de registro de **tempdb**.  
- El programa de instalación agrega varios archivos de datos tempdb durante una instalación nueva de la instancia. Esta tarea puede realizarse con el nuevo control de entrada de la IU en la sección **Configuración del motor de base de datos** y un parámetro de línea de comandos /SQLTEMPDBFILECOUNT. De manera predeterminada, la configuración agrega tantos archivos de datos de tempdb como el número de procesadores lógicos u ocho, lo que sea menor.  
- Si hay varios archivos de datos **tempdb**, todos crecen automáticamente al mismo tiempo y la misma cantidad en función de la configuración de crecimiento. La marca de seguimiento 1117 ya no es necesaria.  
- Todas las asignaciones de **tempdb** usarán extensiones uniformes. [La marca de seguimiento 1118](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) ya no es necesaria.  
- Para el grupo de archivos principal, la propiedad AUTOGROW_ALL_FILES se activa y la propiedad no se puede modificar. 

## <a name="capacity-planning-for-tempdb-in-sql-server"></a>Planeamiento de capacidad para tempdb en SQL Server
 Determinar el tamaño adecuado para tempdb en un entorno de producción de SQL Server depende de muchos factores. Como se ha descrito en el artículo anterior, estos factores incluyen la carga de trabajo existente y las características de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que se usan. Se recomienda analizar la carga de trabajo existente llevando a cabo las siguientes tareas en un entorno de prueba de SQL Server:
- Establezca el crecimiento automático en ON para tempdb.
- Ejecute consultas individuales o archivos de seguimiento de carga de trabajo y supervise el uso del espacio de tempdb.
- Ejecute operaciones de mantenimiento de índice, como volver a generar índices, y supervise el espacio de tempdb. 
- Utilice los valores de uso de espacio de los pasos anteriores para predecir el uso de carga de trabajo total; ajuste este valor para la actividad simultánea proyectada y, a continuación, establezca el tamaño de tempdb según corresponda.

## <a name="how-to-monitor-tempdb-use"></a>Cómo supervisar el uso de tempdb
  Si se agota el espacio de disco de tempdb, se pueden producir interrupciones importantes en el entorno de producción de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y es posible que las aplicaciones en ejecución no puedan finalizar sus operaciones. Puede utilizar la vista de administración dinámica [sys.dm_db_file_space_usage](../../relational-databases/system-dynamic-management-views/sys-dm-db-session-space-usage-transact-sql.md) para supervisar el espacio en disco que utilizan los archivos de tempdb:
  
 ```sql
 -- Determining the Amount of Free Space in tempdb
 SELECT SUM(unallocated_extent_page_count) AS [free pages], 
  (SUM(unallocated_extent_page_count)*1.0/128) AS [free space in MB]
 FROM sys.dm_db_file_space_usage;
 ```
 
 ```sql
 -- Determining the Amount Space Used by the Version Store
 SELECT SUM(version_store_reserved_page_count) AS [version store pages used],
  (SUM(version_store_reserved_page_count)*1.0/128) AS [version store space in MB]
 FROM sys.dm_db_file_space_usage;
 ```
 
 ```sql
 -- Determining the Amount of Space Used by Internal Objects
 SELECT SUM(internal_object_reserved_page_count) AS [internal object pages used],
  (SUM(internal_object_reserved_page_count)*1.0/128) AS [internal object space in MB]
 FROM sys.dm_db_file_space_usage;
 ```
 
 ```sql
 -- Determining the Amount of Space Used by User Objects
 SELECT SUM(user_object_reserved_page_count) AS [user object pages used],
  (SUM(user_object_reserved_page_count)*1.0/128) AS [user object space in MB]
 FROM sys.dm_db_file_space_usage;
 ```
  
  Asimismo, para supervisar la actividad de asignación o desasignación de páginas en tempdb en la sesión o tarea, se pueden utilizar las vistas de administración dinámica [sys.dm_db_session_space_usage](../../relational-databases/system-dynamic-management-views/sys-dm-db-session-space-usage-transact-sql.md) y [sys.dm_db_task_space_usage](../../relational-databases/system-dynamic-management-views/sys-dm-db-task-space-usage-transact-sql.md). Estas vistas pueden utilizarse para identificar consultas grandes, tablas temporales o variables de tabla que utilizan mucho espacio de disco de tempdb. También hay muchos contadores que se pueden utilizar para supervisar el espacio libre disponible en tempdb, así como los recursos que está utilizando tempdb. Para obtener más información, vea la próxima sección.

 ```sql
 -- Obtaining the space consumed by internal objects in all currently running tasks in each session
 SELECT session_id, 
  SUM(internal_objects_alloc_page_count) AS task_internal_objects_alloc_page_count,
  SUM(internal_objects_dealloc_page_count) AS task_internal_objects_dealloc_page_count 
 FROM sys.dm_db_task_space_usage 
 GROUP BY session_id;
 ```
 
 ```sql
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
 [Opción SORT_IN_TEMPDB para índices](../../relational-databases/indexes/sort-in-tempdb-option-for-indexes.md)  
 [Bases de datos del sistema](../../relational-databases/databases/system-databases.md)  
 [sys.databases (Transact-SQL)](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)  
 [sys.master_files (Transact-SQL)](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md)  
 [Mover archivos de base de datos](../../relational-databases/databases/move-database-files.md)  
  
## <a name="see-also"></a>Ver también  
 [Trabajar con tempdb en SQL Server 2005](http://go.microsoft.com/fwlink/?LinkId=81216)  
 [Troubleshooting Insufficient Disk Space in tempdb](http://msdn.microsoft.com/library/ms176029.aspx) (Solucionar problemas de espacio en disco insuficiente en tempdb) 
