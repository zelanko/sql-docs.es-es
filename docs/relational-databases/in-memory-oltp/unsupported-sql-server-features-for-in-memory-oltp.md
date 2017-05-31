---
title: "Características de SQL Server no admitidas para OLTP en memoria | Microsoft Docs"
ms.custom: 
ms.date: 10/17/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine-imoltp
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: c39f03a7-e223-4fd7-bd30-142e28f51654
caps.latest.revision: 55
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: e1b1d4a26616fe83a241267bc87b9e799d883e26
ms.contentlocale: es-es
ms.lasthandoff: 04/11/2017

---
# <a name="unsupported-sql-server-features-for-in-memory-oltp"></a>Características de SQL Server no admitidas para OLTP en memoria
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  En este tema se describen las características de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cuyo uso no se admite con objetos con optimización para memoria.  
  
## <a name="includessnoversionincludesssnoversion-mdmd-features-not-supported-for-in-memory-oltp"></a>[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Características no admitidas para OLTP en memoria  
 Las características siguientes de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no se admiten en una base de datos que tiene objetos con optimización para memoria (incluido el grupo de archivos de datos con optimización para memoria).  
  
|Característica no admitida|Descripción de la característica|  
|-------------------------|-------------------------|  
|Compresión de datos en tablas con optimización para memoria.|Puede usar la característica de compresión de datos como ayuda para comprimir los datos de una base de datos y reducir el tamaño de la base de datos. Para obtener más información, consulte [Data Compression](../../relational-databases/data-compression/data-compression.md).|  
|Creación de particiones de tablas con optimización para memoria e índices HASH, así como índices no agrupados.|Los datos de tablas e índices con particiones se dividen en unidades que pueden propagarse por más de un grupo de archivos de la base de datos. Para obtener más información, consulte [Partitioned Tables and Indexes](../../relational-databases/partitions/partitioned-tables-and-indexes.md).|  
|Replicación|Las configuraciones de replicación que no sean la replicación transaccional en tablas con optimización para memoria en los suscriptores son incompatibles con tablas o vistas que hacen referencia a tablas con optimización para memoria. La replicación con sync_mode=’database snapshot’ no se admite si hay un grupo de archivos con optimización para memoria. Para obtener más información, vea [Replicación para los suscriptores de tablas con optimización para memoria](../../relational-databases/replication/replication-to-memory-optimized-table-subscribers.md).|  
|Creación de reflejo|No se admite la creación de reflejo de la base de datos para bases de datos con un grupo de archivos MEMORY_OPTIMIZED_DATA. Para obtener más información sobre la creación de reflejo, vea [Creación de reflejo de la base de datos &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md).|  
|Recompilar el registro|La recompilación del registro, ya sea a través de un adjunto o de ALTER DATABASE, no se admite para bases de datos con un grupo de archivos MEMORY_OPTIMIZED_DATA.|  
|Servidor vinculado|No se puede tener acceso a los servidores vinculados en la misma consulta o transacción como tablas optimizadas en memoria. Para obtener más información, vea [Servidores vinculados &#40;motor de base de datos&#41;](../../relational-databases/linked-servers/linked-servers-database-engine.md).|  
|Registro masivo|Independientemente del modelo de recuperación de la base de datos, todas las operaciones en tablas durables con optimización para memoria siempre se registran completamente.|  
|Registro mínimo|Las tablas con optimización para memoria no admiten el registro mínimo. Para obtener más información sobre el registro mínimo, vea [El registro de transacciones &#40;SQL Server&#41;](../../relational-databases/logs/the-transaction-log-sql-server.md) y [Requisitos previos para el registro mínimo durante la importación en bloque](../../relational-databases/import-export/prerequisites-for-minimal-logging-in-bulk-import.md).|  
|Seguimiento de cambios|El seguimiento de cambios se puede habilitar en una base de datos con objetos de OLTP en memoria. Sin embargo, no se hace el seguimiento de los cambios en las tablas con optimización para memoria.|  
|DDL, desencadenadores|En las tablas y los módulos compilados de forma nativa de OLTP en memoria no se admiten desencadenadores DDL de nivel de servidor ni de nivel de base de datos.|  
|Captura de datos modificados (CDC)|CDC no se puede usar con una base de datos que tenga tablas con optimización para memoria, ya que usa un desencadenador DDL para DROP TABLE deforma oculta.|  
|Modo de fibra|El modo de fibra no se admite con tablas con optimización para memoria:<br /><br /> Si el modo de fibra está activo, no puede crear bases de datos con grupos de archivos con optimización para memoria ni agregar grupos de archivos con optimización para memoria a bases de datos existentes.<br /><br /> Puede habilitar el modo de fibra si hay bases de datos con grupos de archivos con optimización para memoria. Sin embargo, para habilitar el modo de fibra hay que reiniciar el servidor. En esa situación, las bases de datos con grupos de archivos con optimización para memoria no se podrán recuperar y aparecerá un mensaje de error que recomienda que deshabilite el modo de fibra para usar bases de datos con grupos de archivos con optimización para memoria.<br /><br /> Si se adjuntan y restauran bases de datos con grupos de archivos con optimización para memoria, se producirá un error cuando el modo de fibra esté activo. Las bases de datos se marcarán como SUSPECT.<br /><br /> <br /><br /> Para obtener más información, consulte [lightweight pooling Server Configuration Option](../../database-engine/configure-windows/lightweight-pooling-server-configuration-option.md).|  
|Limitación de Service Broker|No puede tener acceso a una cola desde un procedimiento almacenado compilado de forma nativa.<br /><br /> No puede tener acceso a una cola en una base de datos remota en una transacción que tiene acceso a tablas con optimización para memoria.|  
|Replicación en los suscriptores|La replicación transaccional en tablas con optimización para memoria en suscriptores se admite pero con algunas restricciones. Para obtener más información, vea [Replicación en suscriptores de tablas con optimización para memoria](../../relational-databases/replication/replication-to-memory-optimized-table-subscribers.md).|  
  
 Con algunas excepciones, las transacciones entre bases de datos no se admiten. En la tabla siguiente se describen qué casos se admiten y las restricciones correspondientes. (Vea también [Consultas entre bases de datos](../../relational-databases/in-memory-oltp/cross-database-queries.md)).  
  
|Bases de datos|Permitido|Descripción|  
|---------------|-------------|-----------------|  
|Bases de datos de usuario modelo y msdb|No|Las consultas y transacciones entre bases de datos no se admiten.<br /><br /> Las consultas y transacciones que tienen acceso a tablas con optimización para memoria o a procedimientos almacenados compilados de forma nativa no pueden tener acceso a otras bases de datos, excepto a las bases de datos del sistema maestra (acceso de solo lectura) y tempdb.|  
|Base de datos de recursos, tempdb|Sí|No hay restricciones en las transacciones entre bases de datos que, además de una base de datos de usuario único, usan solo la base de datos de recursos y tempdb.|  
|maestra|solo lectura|Las transacciones entre bases de datos que tocan OLTP en memoria y la base de datos maestra no pueden confirmarse si incluyen operaciones de escritura en la base de datos maestra. Se permiten las transacciones entre bases de datos que solo leen de la base de datos maestra y usan una base de datos de un solo usuario.|  
  
## <a name="scenarios-not-supported"></a>Escenarios no admitidos  
  
-   La contención de base de datos ([Bases de datos contenidas](../../relational-databases/databases/contained-databases.md)) no es compatible con OLTP en memoria. Se admite la autenticación de la base de datos independiente. Sin embargo, todos los objetos de OLTP en memoria se marcan como 'breaking containment' en la DMV dm_db_uncontained_entities.  
  
-   Acceso a tablas con optimización para memoria mediante la conexión de contexto desde procedimientos almacenados CLR.  
  
-   Cursores de conjunto de claves y dinámicos en consultas que tienen acceso a tablas con optimización para memoria. Estos cursores se degradan a estáticos y de solo lectura.  
  
-   El uso de **MERGE INTO***destino* con *destino* es una tabla con optimización para memoria. **MERGE USING***origen* se admite para las tablas con optimización para memoria.  
  
-   El tipo de datos ROWVERSION (TIMESTAMP) no se admite. Para obtener más información, vea [FROM &#40;Transact-SQL&#41;](../../t-sql/queries/from-transact-sql.md).  
  
-   El cierre automático no se admite con las bases de datos que tienen un grupo de archivos MEMORY_OPTIMIZED_DATA.  
  
-   Las instantáneas de base de datos no se admiten para bases de datos que tienen un grupo de archivos MEMORY_OPTIMIZED_DATA.  
  
-   DDL transaccional. Las operaciones CREATE, ALTER y DROP de objetos OLTP en memoria no se admiten dentro de las transacciones de usuario.  
  
-   Notificación de eventos.  
  
-   Administración basada en directivas (PBM). No se admiten los modos de impedir y solo registrar de PBM. La existencia de estas directivas en el servidor puede impedir la correcta ejecución de DDL de OLTP en memoria. Se admiten los modos a petición y programado.  
  
## <a name="see-also"></a>Vea también  
 [Compatibilidad de SQL Server con OLTP en memoria](../../relational-databases/in-memory-oltp/sql-server-support-for-in-memory-oltp.md)  
  
  

