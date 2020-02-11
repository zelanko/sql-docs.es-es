---
title: ¿Qué&#39;s nuevo (Motor de base de datos)? | Microsoft Docs
ms.custom: ''
ms.date: 06/22/2016
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: release-landing
ms.topic: conceptual
helpviewer_keywords:
- what's new [SQL Server Database Engine]
- Database Engine [SQL Server], what's new
ms.assetid: 8f625d5a-763c-4440-97b8-4b823a6e2439
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 5e51cda61bb44d1f143cab50901276b927cca73a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "70176079"
---
# <a name="what39s-new-database-engine"></a>Qué&#39;s nuevo (Motor de base de datos)
  Esta última versión del [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] incluye nuevas características y mejoras que aumentan la eficacia y la productividad de los arquitectos, desarrolladores y administradores que diseñan, desarrollan y mantienen sistemas de almacenamiento de datos. A continuación se muestran las áreas en las que ha mejorado el [!INCLUDE[ssDE](../includes/ssde-md.md)] .  
  
##  <a name="Feature"></a>Mejoras en las características de Motor de base de datos  
  
###  <a name="MemoryOpt"></a>Tablas con optimización para memoria  
 OLTP en memoria es un motor de base de datos optimizado para memoria integrado en el motor de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . OLTP en memoria está optimizado para OLTP. Para obtener más información, vea [OLTP en memoria &#40;optimización en memoria&#41;](../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md).  
 
  
###  <a name="DataFiles"></a>SQL Server de los archivos de datos en Azure  
 [SQL Server archivos de datos de Azure](../relational-databases/databases/sql-server-data-files-in-microsoft-azure.md) habilita la compatibilidad [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] nativa con archivos de base de datos almacenados como blobs de Azure. Esta característica permite crear una base de datos en [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ejecución en el entorno local o en una máquina virtual de Azure con una ubicación de almacenamiento dedicada para los datos en Azure BLOB Storage.  
  
  
###  <a name="AzureVM"></a>Hospedar una base de datos SQL Server en una máquina virtual de Azure  
 Use el Asistente para [implementar una base de datos de SQL Server en una máquina virtual de Azure](https://msdn.microsoft.com/library/dn195938\(v=sql.120\).aspx) para hospedar [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] una base de datos de una instancia de en una máquina virtual de Azure.  
  
  
###  <a name="Backup"></a>Mejoras en copias de seguridad y restauración  
 
  [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] contiene las siguientes mejoras para Copias de seguridad y restauración de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]:  
  
-   **Copia de seguridad en URL de SQL Server**  
  
     La copia de seguridad en URL de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] se introdujo en [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] SP1 CU2 y solo la admite [!INCLUDE[tsql](../includes/tsql-md.md)], PowerShell y SMO. En [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] puede usar [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] para realizar copias de seguridad o restaurar desde el servicio de almacenamiento de blobs de Azure. La nueva opción está disponible tanto para la tarea de copia de seguridad como para los planes de mantenimiento. Para obtener más información, consulte [uso de la tarea de copia de seguridad en SQL Server Management Studio](../relational-databases/backup-restore/sql-server-backup-to-url.md#BackupTaskSSMS), [SQL Server copia de seguridad en URL mediante el Asistente para planes de mantenimiento](../relational-databases/backup-restore/sql-server-backup-to-url.md#MaintenanceWiz)y [restauración desde Azure Storage mediante SQL Server Management Studio](../relational-databases/backup-restore/sql-server-backup-to-url.md#RestoreSSMS).  
  
-   **Copia de seguridad administrada de SQL Server en Azure**  
  
     Integrado en la Copia de seguridad en URL de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] es un servicio que proporciona [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] para administrar y programar copias de seguridad de bases de datos y de registros. En esta versión solo se admite la copia de seguridad en Azure Storage. 
  [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] se puede configurar tanto en el nivel de base de datos como en el nivel de instancia, y permite un control más específico en el nivel de base de datos y automatización en el nivel de instancia. [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]se puede configurar en [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] instancias que se ejecutan en [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] local y en instancias que se ejecutan en máquinas virtuales de Azure. Se recomienda para [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] las instancias que se ejecutan en máquinas virtuales de Azure. Para obtener más información, consulte [SQL Server copia de seguridad administrada en Azure](../relational-databases/backup-restore/sql-server-managed-backup-to-microsoft-azure.md).  
  
-   **Cifrado para copias de seguridad**  
  
     Ahora puede elegir cifrar el archivo de copia de seguridad durante una operación de copia de seguridad.  Admite varios algoritmos de cifrado, incluidos AES 128, AES 192, AES 256 y Triple DES. Debe utilizar un certificado o una clave asimétrica para realizar el cifrado durante la copia de seguridad. Para obtener más información, vea [Cifrado de copia de seguridad](../relational-databases/backup-restore/backup-encryption.md).  
  
  
###  <a name="CE"></a>Nuevo diseño para la estimación de la cardinalidad  
 La lógica de estimación de la cardinalidad, denominada estimador de cardinalidad, se ha rediseñado en [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] para mejorar la calidad de los planes de consulta y, por tanto, mejorar el rendimiento de las consultas. El nuevo estimador de cardinalidad incorpora suposiciones y algoritmos que funcionan bien en las cargas de trabajo OLTP y de almacenamiento de datos modernas. Se basa en un profundo estudio sobre la estimación de cardinalidad en las cargas de trabajo modernas y en lo que hemos aprendido durante los últimos 15 años para mejorar el estimador de cardinalidad de SQL Server. Los comentarios de los clientes indican que si bien la mayoría de las consultas se beneficiarán del cambio o no cambiarán, un número reducido puede mostrar regresiones en comparación con el estimador de cardinalidad anterior. Para obtener recomendaciones sobre la optimización del rendimiento y las pruebas, consulte [estimación de cardinalidad &#40;SQL Server&#41;](../relational-databases/performance/cardinality-estimation-sql-server.md).  
   
  
###  <a name="Durability"></a>Durabilidad diferida  
 
  [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] incorpora la capacidad de reducir la latencia, para lo cual identifica a todas las transacciones o a alguna de ellas como perdurable diferida. Una transacción perdurable diferida devuelve el control al cliente antes de que se escriba en el disco el registro de transacciones. La perdurabilidad se puede controlar a nivel de la base de datos, de COMMIT o del bloque ATOMIC.  
  
 Para obtener más información, vea el tema control de la durabilidad de las [transacciones](../relational-databases/logs/control-transaction-durability.md).  
  
  
###  <a name="AlwaysOn"></a>Mejoras de AlwaysOn  
 
  [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] contiene las mejoras siguientes para las instancias de clúster de conmutación por error AlwaysOn y los grupos de disponibilidad AlwaysOn:  
  
-   Un Asistente para agregar réplica de Azure simplifica la creación de soluciones híbridas para grupos de disponibilidad AlwaysOn. Para obtener más información, consulte [usar el Asistente para agregar réplica de Azure &#40;SQL Server&#41;](availability-groups/windows/use-the-add-azure-replica-wizard-sql-server.md).  
  
-   El número máximo de réplicas secundarias ha aumentado de 4 a 8.  
  
-   Cuando se desconectan de la réplica principal o durante la pérdida de quórum de clúster, las réplicas secundarias legibles quedan ahora disponibles para cargas de trabajo de lectura.  
  
-   Las instancias de clúster de conmutación por error (FCI) pueden usar ahora Volúmenes compartidos de clúster (CSV) como discos compartidos de clúster. Para obtener más información, consulte [Always on de instancias de clúster de conmutación por error](../sql-server/failover-clusters/windows/always-on-failover-cluster-instances-sql-server.md).  
  
-   Hay disponibles una nueva función del sistema, [sys.fn_hadr_is_primary_replica](/sql/relational-databases/system-functions/sys-fn-hadr-is-primary-replica-transact-sql), y una nueva DMV, [sys.dm_io_cluster_valid_path_names](/sql/relational-databases/system-dynamic-management-views/sys-dm-io-cluster-valid-path-names-transact-sql).  
  
-   Las DMV siguientes se han mejorado y ahora devuelven información de FCI: [sys.dm_hadr_cluster](/sql/relational-databases/system-dynamic-management-views/sys-dm-hadr-cluster-transact-sql), [sys.dm_hadr_cluster_members](/sql/relational-databases/system-dynamic-management-views/sys-dm-hadr-cluster-members-transact-sql)y [sys.dm_hadr_cluster_networks](/sql/relational-databases/system-dynamic-management-views/sys-dm-hadr-cluster-networks-transact-sql).  
  
  
###  <a name="OIR"></a>Conmutación e indización de particiones  
 Ahora se pueden volver a crear las particiones individuales de tablas con particiones. Para obtener más información, vea [ALTER INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-index-transact-sql).  
   
  
###  <a name="Lock"></a>Administrar la prioridad de bloqueo de las operaciones en línea  
 La opción `ONLINE = ON` contiene ahora una opción `WAIT_AT_LOW_PRIORITY` que permite especificar cuánto tiempo debe esperar el proceso de regeneración a los bloqueos necesarios. La opción `WAIT_AT_LOW_PRIORITY` también permite configurar la finalización de procesos de bloqueo relacionados con la instrucción de regeneración. Para obtener más información, vea [ALTER TABLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-table-transact-sql) y [ALTER INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-index-transact-sql). Puede encontrar información sobre la solución de problemas de los nuevos tipos de Estados de bloqueo en [Sys. dm_tran_locks &#40;Transact-sql&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-tran-locks-transact-sql) y [sys. dm_os_wait_stats &#40;transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql).  
 
  
###  <a name="CCI"></a>Índices de almacén de columnas  
 Estas nuevas características están disponibles para los índices de almacén de columnas:  
  
-   **Índices clúster de almacén de columnas**  
  
     Use un índice clúster de almacén de columnas para mejorar la compresión de datos y el rendimiento de las consultas para las cargas de trabajo de almacenamiento de datos que ejecutan principalmente cargas masivas y consultas de solo lectura. Puesto que el índice clúster de almacén de columnas es actualizable, la carga de trabajo puede realizar muchas operaciones de inserción, actualización y eliminación. Para obtener más información, consulte [índices de almacén de columnas descritos](../relational-databases/indexes/columnstore-indexes-described.md) y [uso de índices de almacén de columnas agrupados](../relational-databases/indexes/indexes.md).  
  
-   **All**  
  
     SHOWPLAN muestra información acerca de los índices de almacén de columnas. Las propiedades **EstimatedExecutionMode** y **ActualExecutionMode** tienen dos valores posibles: **Lote** o **Fila**.  La propiedad **Storage** tiene dos valores posibles: **RowStore** y **ColumnStore**.  
  
-   **Compresión de datos de archivado**  
  
     MODIFICAR ÍNDICE... Rebuild tiene una nueva opción de compresión de datos COLUMNSTORE_ARCHIVE que comprime aún más las particiones especificadas de un índice de almacén de columnas. Puede usarla para el archivado o para otras situaciones que requieran un tamaño menor de almacenamiento de datos y puedan permitirse usar más tiempo para el almacenamiento y la recuperación. Para obtener más información, vea [ALTER INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-index-transact-sql).  
   
  
###  <a name="Buffer"></a>Extensión del grupo de búferes  
 La opción [Extensión del grupo de búferes](configure-windows/buffer-pool-extension.md) proporciona integración sin problemas de unidades de estado sólido (SSD) como extensión de la memoria de acceso aleatorio no volátil (NvRAM) para el grupo de búferes del [!INCLUDE[ssDE](../includes/ssde-md.md)] que mejora significativamente el rendimiento de E/S.  
   
  
###  <a name="Stats"></a>Estadísticas incrementales  
 CREATE STATISTICS y las instrucciones relacionadas con las estadísticas ahora permiten crear estadísticas por cada partición con la opción INCREMENTAL. Las instrucciones relacionadas permiten o generan estadísticas incrementales. La sintaxis afectada incluye UPDATE STATISTICs, sp_createstats, CREATE INDEX, ALTER INDEX, ALTER DATABASE SET Options, DATABASEPROPERTYEX, sys. Databases y sys. stats. Para obtener más información, vea [Create statistics &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-statistics-transact-sql).  
  
  
###  <a name="RG"></a>Resource Governor mejoras para el control físico de e/s  
 El regulador de recursos permite especificar límites en cuanto a la cantidad de CPU, E/S física y memoria que las solicitudes entrantes procedentes de las aplicaciones pueden usar dentro de un grupo de recursos de servidor. En [!INCLUDE[ssSQL14](../includes/sssql14-md.md)], puede utilizar los nuevos valores MIN_IOPS_PER_VOLUME y MAX_IOPS_PER_VOLUME para controlar las E/S físicas emitidas para los subprocesos de usuario para un grupo de recursos de servidor determinado. Para obtener más información, vea [Resource Governor grupo de recursos de grupo](../relational-databases/resource-governor/resource-governor-resource-pool.md) y crear un [grupo de recursos &#40;&#41;de Transact-SQL ](/sql/t-sql/statements/create-resource-pool-transact-sql).  
  
 El valor MAX_OUTSTANDING_IO_PER_VOLUME de ALTER RESOURCE GOVERNOR establece las operaciones de E/S pendientes máximas por volumen de disco. Puede usar este valor para optimizar la regulación de recursos de E/S de acuerdo con las características de E/S de un volumen de disco y para limitar el número de operaciones de E/S emitidas en el límite de la instancia de SQL Server. Para obtener más información, vea [ALTER RESOURCE GOVERNOR &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-resource-governor-transact-sql).  
  
  
###  <a name="OnlineEvent"></a>Online index Operation (clase de eventos)  
 El informe de progreso para la clase de eventos Online Index Operation ahora tiene dos nuevas columnas de datos: **PartitionId** y **PartitionNumber**. Para obtener más información, vea [Progress Report: Online Index Operation Event Class](../relational-databases/event-classes/progress-report-online-index-operation-event-class.md).  
  
  
###  <a name="Compat"></a>Nivel de compatibilidad de bases de datos  
 El nivel de compatibilidad 90 no es válido en [!INCLUDE[ssSQL14](../includes/sssql14-md.md)]. Para obtener más información, vea [nivel de compatibilidad de Alter database &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-compatibility-level)  
  
##  <a name="TSQL"></a>Mejoras de Transact-SQL  
  
### <a name="inline-specification-of-clustered-and-nonclustered"></a>Especificación alineada de CLUSTERED y NONCLUSTERED  
 La especificación alineada de los índices `CLUSTERED` y `NONCLUSTERED` se permite ahora para las tablas basadas disco. La creación de una tabla con índices alineados es equivalente a la emisión de un comando de crear tabla seguido de las instrucciones `CREATE INDEX` correspondientes. Las columnas incluidas y las condiciones de filtro no son compatibles con los índices alineados.  
  
### <a name="select--into"></a>SELECCIONE... DENTRO  
 La instrucción `SELECT ... INTO` se ha mejorado y ahora puede ejecutarse en paralelo. El nivel de compatibilidad de la base de datos debe ser de 110 como mínimo.  
  
### <a name="includetsqlincludestsql-mdmd-enhancements-for-in-memory-oltp"></a>Mejoras de [!INCLUDE[tsql](../includes/tsql-md.md)] para OLTP en memoria  
 Para obtener información acerca de los cambios de [!INCLUDE[tsql](../includes/tsql-md.md)] para admitir OLTP en memoria, vea [Transact-SQL Support for In-Memory OLTP](../relational-databases/in-memory-oltp/transact-sql-support-for-in-memory-oltp.md).  
  
  
##  <a name="SystemTable"></a>Mejoras de la vista del sistema  
  
### <a name="sysxml_indexes"></a>sys.xml_indexes  
 [Sys. xml_indexes &#40;&#41;de Transact-SQL](/sql/relational-databases/system-catalog-views/sys-xml-indexes-transact-sql) tiene tres nuevas columnas `xml_index_type`: `xml_index_type_description`, y `path_id`.  
  
### <a name="sysdm_exec_query_profiles"></a>sys.dm_exec_query_profiles  
 [Sys. dm_exec_query_profiles &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-exec-query-profiles-transact-sql) supervisa el progreso de la consulta en tiempo real mientras una consulta se encuentra en ejecución.  
  
### <a name="syscolumn_store_row_groups"></a>sys.column_store_row_groups  
 [Sys. column_store_row_groups &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-column-store-row-groups-transact-sql) proporciona información del índice de almacén de columnas agrupado por segmento para ayudar al administrador a tomar decisiones de administración del sistema.  
  
### <a name="sysdatabases"></a>sys.databases  
 [Sys. Databases &#40;&#41;de Transact-SQL](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql) tiene tres nuevas columnas: `is_auto_create_stats_incremental_on`, `is_query_store_on`y `resource_pool_id`.  
  
### <a name="system-view-enhancements-for-in-memory-oltp"></a>Mejoras de las vistas del sistema para OLTP en memoria  
 Para obtener información sobre las mejoras de las vistas del sistema para admitir OLTP en memoria, consulte [vistas del sistema, procedimientos almacenados, DMV y tipos de espera para OLTP en memoria](../../2014/database-engine/system-views-stored-procedures-dmvs-and-wait-types-for-in-memory-oltp.md).  
   
  
##  <a name="Security"></a>Mejoras de seguridad  
  
### <a name="connect-any-database-permission"></a>Permiso CONNECT ANY DATABASE  
 Es un permiso nuevo de nivel de servidor. Conceda **CONNECT ANY DATABASE** a un inicio de sesión que debe conectarse a todas las bases de datos que existen actualmente y a todas las bases de datos que puedan crearse en futuro. No concede ningún permiso en ninguna base de datos más allá de conexión. Combine con **Select All User protegibles** o `VIEW SERVER STATE` para permitir que un proceso de auditoría vea todos los datos o todos los Estados de base [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]de datos en la instancia de.  
  
### <a name="impersonate-any-login-permission"></a>Permiso IMPERSONATE ANY LOGIN  
 Es un permiso nuevo de nivel de servidor. Cuando se concede, permite que un proceso de nivel intermedio suplante la cuenta de los clientes que se conecten a él, a medida que se conecta a las bases de datos. Cuando se deniega, se puede impedir que un inicio de sesión con un alto nivel de privilegios suplante a otros inicios de sesión. Por ejemplo, es posible bloquear un inicio de sesión con el permiso **CONTROL SERVER** para impedir que suplante a otros inicios de sesión.  
  
### <a name="select-all-user-securables-permission"></a>Permiso SELECT ALL USER SECURABLES  
 Es un permiso nuevo de nivel de servidor. Cuando se concede, un inicio de sesión como un auditor puede ver los datos de todas las bases de datos a las que el usuario puede conectarse.  
  
  
##  <a name="Deployment"></a>Mejoras en la implementación  
### <a name="azure-vm"></a>Azure VM
[Implementar una base de datos SQL Server en una máquina Virtual Microsoft Azure](../relational-databases/databases/deploy-a-sql-server-database-to-a-microsoft-azure-virtual-machine.md) permite la [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] implementación de una base de datos en una máquina virtual de Azure.  

### <a name="refs"></a>ReFS
Ahora se admite la implementación de bases de datos en ReFS.   
  
## <a name="see-also"></a>Consulte también  
 [Características compatibles con las ediciones de SQL Server 2014](../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md)  
   
