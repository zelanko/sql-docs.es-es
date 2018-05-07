---
title: Características de SQL Server no admitidas para OLTP en memoria | Microsoft Docs
ms.custom: ''
ms.date: 07/19/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: in-memory-oltp
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine-imoltp
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: c39f03a7-e223-4fd7-bd30-142e28f51654
caps.latest.revision: 55
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: On Demand
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 0cdaeb155f34ec4adaf285c2b1345ab3af713980
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="unsupported-sql-server-features-for-in-memory-oltp"></a>Características de SQL Server no admitidas para OLTP en memoria
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

En este tema se describen las características de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cuyo uso no se admite con objetos optimizados para memoria.  
  
## <a name="includessnoversionincludesssnoversion-mdmd-features-not-supported-for-in-memory-oltp"></a>[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Características no admitidas para OLTP en memoria  

Las características siguientes de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no se admiten en una base de datos que tiene objetos optimizados para memoria (incluido el grupo de archivos de datos optimizados para memoria).  

  
|Característica no admitida|Descripción de la característica|  
|-------------------------|-------------------------|  
|Compresión de datos en tablas optimizadas para memoria.|Puede usar la característica de compresión de datos como ayuda para comprimir los datos de una base de datos y reducir el tamaño de la base de datos. Para obtener más información, consulte [Data Compression](../../relational-databases/data-compression/data-compression.md).|  
|Creación de particiones de tablas optimizadas para memoria e índices HASH, así como índices no agrupados.|Los datos de tablas e índices con particiones se dividen en unidades que pueden propagarse por más de un grupo de archivos de la base de datos. Para obtener más información, vea [Partitioned Tables and Indexes](../../relational-databases/partitions/partitioned-tables-and-indexes.md).|  
| REPLICATION | Las configuraciones de replicación que no sean la replicación transaccional en tablas optimizadas para memoria en los suscriptores son incompatibles con tablas o vistas que hacen referencia a tablas optimizadas para memoria.<br /><br />Si hay un grupo de archivos optimizados para memoria, no se admite la replicación con sync_mode=’database snapshot’.<br /><br />Para obtener más información, vea [Replicación para los suscriptores de tablas con optimización para memoria](../../relational-databases/replication/replication-to-memory-optimized-table-subscribers.md).|
|Creación de reflejo|No se admite la creación de reflejo de la base de datos para bases de datos con un grupo de archivos MEMORY_OPTIMIZED_DATA. Para obtener más información sobre la creación de reflejo, vea [Creación de reflejo de la base de datos &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md).|  
|Recompilar el registro|La recompilación del registro, ya sea a través de un adjunto o de ALTER DATABASE, no se admite para bases de datos con un grupo de archivos MEMORY_OPTIMIZED_DATA.|  
|Servidor vinculado|No se puede tener acceso a los servidores vinculados en la misma consulta o transacción como tablas optimizadas en memoria. Para obtener más información, vea [Servidores vinculados &#40;motor de base de datos&#41;](../../relational-databases/linked-servers/linked-servers-database-engine.md).|  
|Registro masivo|Independientemente del modelo de recuperación de la base de datos, todas las operaciones en tablas durables optimizadas para memoria siempre se registran completamente.|  
|Registro mínimo|Las tablas optimizadas para memoria no admiten el registro mínimo. Para obtener más información sobre el registro mínimo, vea [El registro de transacciones &#40;SQL Server&#41;](../../relational-databases/logs/the-transaction-log-sql-server.md) y [Requisitos previos para el registro mínimo durante la importación en bloque](../../relational-databases/import-export/prerequisites-for-minimal-logging-in-bulk-import.md).|  
|seguimiento de cambios|El seguimiento de cambios se puede habilitar en una base de datos con objetos de OLTP en memoria. Sin embargo, no se hace el seguimiento de los cambios en las tablas optimizadas para memoria.|  
| DDL, desencadenadores | No se admiten ni los desencadenadores DDL de nivel de base de datos ni de nivel de servidor con las tablas OLTP en memoria ni con módulos compilados de forma nativa. |  
| Captura de datos modificados (CDC) | CDC no se puede usar con una base de datos que tenga tablas optimizadas para memoria, debido a que CDC internamente usa un desencadenador DDL para DROP TABLE. |  
| Modo de fibra | El modo de fibra no se admite con tablas optimizadas para memoria:<br /><br />Si el modo de fibra está activo, no puede crear bases de datos con grupos de archivos optimizados para memoria ni agregar grupos de archivos optimizados para memoria a bases de datos existentes.<br /><br />Puede habilitar el modo de fibra si hay bases de datos con grupos de archivos optimizados para memoria. Sin embargo, para habilitar el modo de fibra hay que reiniciar el servidor. En esa situación, las bases de datos con grupos de archivos optimizados para memoria no se podrían recuperar. Luego vería un mensaje de error que recomendaría deshabilitar el modo de fibra para usar las bases de datos con grupos de archivos optimizados para memoria.<br /><br />Si el modo de fibra está activo, se produce un error al adjuntar y restaurar una base de datos con un grupo de archivos optimizados para memoria. Las bases de datos quedarían marcadas como sospechosas.<br /><br />Para obtener más información, consulte [lightweight pooling Server Configuration Option](../../database-engine/configure-windows/lightweight-pooling-server-configuration-option.md). |  
|Limitación de Service Broker|No puede tener acceso a una cola desde un procedimiento almacenado compilado de forma nativa.<br /><br /> No puede tener acceso a una cola en una base de datos remota en una transacción que tiene acceso a tablas optimizadas para memoria.|  
|Replicación en los suscriptores|La replicación transaccional en tablas optimizadas para memoria en suscriptores se admite pero con algunas restricciones. Para obtener más información, vea [Replicación en suscriptores de tablas con optimización para memoria](../../relational-databases/replication/replication-to-memory-optimized-table-subscribers.md).|  


#### <a name="cross-database-queries-and-transcations"></a>Consultas y transacciones entre bases de datos

Con algunas excepciones, las transacciones entre bases de datos no se admiten. En la tabla siguiente se describen qué casos se admiten y las restricciones correspondientes. (Vea también [Consultas entre bases de datos](../../relational-databases/in-memory-oltp/cross-database-queries.md)).  


|Bases de datos|Permitido|Description|  
|---------------|-------------|-----------------|  
| Bases de datos de usuario, **modelo** y **msdb**. | no | En la mayoría de los casos, las consultas y transacciones entre bases de datos *no* se admiten.<br /><br />Una consulta no puede acceder a otras bases de datos si usa una tabla optimizada para memoria o un procedimiento almacenado compilado de forma nativa. Esta restricción se aplica tanto a transacciones como a consultas.<br /><br />Las excepciones son las bases de datos del sistema **tempdb** y **master**. Aquí, la base de datos **master** está disponible para acceso de solo lectura. |
| Base de datos de **recursos**, **tempdb** | Sí | En una transacción que toca los objetos OLTP en memoria, las bases de datos de **recursos** y **tempdb** del sistema se pueden usar sin una restricción agregada.


## <a name="scenarios-not-supported"></a>Escenarios no admitidos  
  
- Acceso a tablas optimizadas para memoria mediante la conexión de contexto desde procedimientos almacenados CLR.  
  
- Cursores de conjunto de claves y dinámicos en consultas que tienen acceso a tablas optimizadas para memoria. Estos cursores se degradan a estáticos y de solo lectura.  
  
- No se admite el uso de **MERGE INTO** *destino*, donde *destino* es una tabla optimizada para memoria.
    - **MERGE USING** *origen* se admite para las tablas optimizadas para memoria.  
  
- El tipo de datos ROWVERSION (TIMESTAMP) no se admite. Para obtener más información, vea [FROM &#40;Transact-SQL&#41;](../../t-sql/queries/from-transact-sql.md).
  
- El cierre automático no se admite con las bases de datos que tienen un grupo de archivos MEMORY_OPTIMIZED_DATA.  
  
- Las instantáneas de base de datos no se admiten para bases de datos que tienen un grupo de archivos MEMORY_OPTIMIZED_DATA.  
  
- DDL transaccional, como las operaciones CREATE/ALTER/DROP de objetos OLTP en memoria, no se admite dentro de las transacciones de usuario.  
  
- Notificación de eventos.  
  
- Administración basada en directivas (PBM).
    - No se admiten los modos de impedir y solo registrar de PBM. La existencia de estas directivas en el servidor puede impedir la correcta ejecución de DDL de OLTP en memoria. Se admiten los modos a petición y programado.  

- La contención de base de datos ([Bases de datos contenidas](../../relational-databases/databases/contained-databases.md)) no es compatible con OLTP en memoria.
    - Se admite la autenticación de la base de datos independiente. En cambio, todos los objetos OLTP en memoria se marcan como "breaking containment" en la vista de administración dinámica (DMV) **dm_db_uncontained_entities**.

  
## <a name="see-also"></a>Ver también  

- [Compatibilidad de SQL Server con OLTP en memoria](../../relational-databases/in-memory-oltp/sql-server-support-for-in-memory-oltp.md)
