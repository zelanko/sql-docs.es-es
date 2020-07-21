---
title: Características de SQL Server admitidas | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: c39f03a7-e223-4fd7-bd30-142e28f51654
author: rothja
ms.author: jroth
ms.openlocfilehash: e7eb4324d56c3ab45486063cb8097603ac3a416b
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85050008"
---
# <a name="supported-sql-server-features"></a>Características admitidas de SQL Server
  En este tema se describen las características de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que se pueden usar o no con objetos optimizados para memoria.  
  
## <a name="ssnoversion-features-supported-for-in-memory-oltp"></a>Características de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] admitidas para OLTP en memoria  
 Las características siguientes de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se admiten en una base de datos que tiene objetos optimizados para memoria, incluido el grupo de archivos optimizados para memoria.  
  
 Para obtener información acerca de los tipos de datos admitidos, vea [Supported Data Types](supported-data-types-for-in-memory-oltp.md).  
  
-   Opciones y operaciones admitidas en tablas optimizadas para memoria. Para obtener más información, vea [CREATE TABLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-table-transact-sql).  
  
-   Opciones y operaciones admitidas en procedimientos almacenados compilados de forma nativa. Para obtener más información, vea [CREATE PROCEDURE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-procedure-transact-sql).  
  
-   Capacidad de obtener acceso a tablas optimizadas para memoria mediante [!INCLUDE[tsql](../../../includes/tsql-md.md)] interpretado. [!INCLUDE[tsql](../../../includes/tsql-md.md)] interpretado proporciona un área expuesta equivalente a tener acceso a tablas que no tienen optimización para memoria mediante procedimientos almacenados que no están compilados de forma nativa y [!INCLUDE[tsql](../../../includes/tsql-md.md)]. Para más información, vea [Acceso a tablas con optimización para memoria mediante Transact-SQL interpretado](accessing-memory-optimized-tables-using-interpreted-transact-sql.md).  
  
-   Control de simultaneidad optimista y varias versiones. Para obtener más información, consulte [Transaction Isolation Levels](../../database-engine/transaction-isolation-levels.md).  
  
-   Copia de seguridad y restauración de una base de datos que contiene un grupo de archivos de datos optimizado para memoria. Para obtener más información, consulte [copia de seguridad y restauración de bases de datos de SQL Server](../backup-restore/back-up-and-restore-of-sql-server-databases.md).  
  
-   Vistas de catálogo, vistas de administración dinámica y eventos extendidos para aportar compatibilidad. Para más información, vea [Propiedades, vistas del sistema, procedimientos almacenados, tipos de espera y DMV nuevos y actualizados para OLTP en memoria](../../database-engine/system-views-stored-procedures-dmvs-and-wait-types-for-in-memory-oltp.md).  
  
-   Objetos de administración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para más información, vea [Compatibilidad de Objetos de administración de SQL Server con OLTP en memoria](sql-server-management-objects-support-for-in-memory-oltp.md).  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Para más información, vea [Compatibilidad de SQL Server Management Studio con OLTP en memoria](sql-server-management-studio-support-for-in-memory-oltp.md).  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell. Para obtener más información, vea [Información general de SQL Server PowerShell](https://msdn.microsoft.com/library/cc281954\(SQL.105\).aspx).  
  
-   Importar y exportar datos de forma masiva con la utilidad bcp. Para más información, vea [Importar y exportar datos de forma masiva con la utilidad bcp &#40;SQL Server&#41;](../import-export/import-and-export-bulk-data-by-using-the-bcp-utility-sql-server.md).  
  
-   Recuperación tras bloqueo.  
  
-   Varios contenedores en un grupo de archivos de datos optimizados para memoria para almacenar objetos de OLTP en memoria y reducir el objetivo de tiempo de recuperación (RTO).  
  
-   Los bloques de registro de transacciones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] calculan la suma de comprobación y la validan.  
  
-   La nueva sugerencia de tabla SNAPSHOT. Para obtener más información, vea [Sugerencias de tabla &#40;Transact-SQL&#41;](/sql/t-sql/queries/hints-transact-sql-table).  
  
-   Nivel de base de datos COMPAT.  
  
-   Base de datos parcialmente independiente. Se admite la autenticación de la base de datos independiente. Sin embargo, todos los objetos de OLTP en memoria se marcan como 'breaking containment' en la DMV dm_db_uncontained_entities.  
  
-   Service Broker, con limitaciones. No puede tener acceso a una cola desde un procedimiento almacenado compilado de forma nativa. No puede tener acceso a una cola en una base de datos remota en una transacción que tiene acceso a tablas optimizadas para memoria.  
  
-   Clústeres de conmutación por error: como parte de la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] oferta de AlwaysOn, las instancias de clúster de conmutación por error de AlwaysOn aprovechan la funcionalidad de clústeres de conmutación por error de Windows Server (WSFC) para proporcionar alta disponibilidad local mediante redundancia en el nivel de instancia de servidor, una instancia de clúster de conmutación por error (FCI). Para obtener más información, vea [Always On Failover Cluster Instances (SQL Server)](../../sql-server/failover-clusters/windows/always-on-failover-cluster-instances-sql-server.md) (Instancias de clúster de conmutación por error de Always On [SQL Server]).  
  
-   Integración con AlwaysOn: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ofrece varias opciones para crear alta disponibilidad para un servidor o una base de datos, incluida AlwaysOn. Para más información, vea [Soluciones de alta disponibilidad &#40;SQL Server&#41;](../../sql-server/failover-clusters/high-availability-solutions-sql-server.md).  
  
-   Trasvase de registros: el trasvase de registros de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] permite enviar automáticamente copias de seguridad del registro de transacciones desde una base de datos principal de una instancia del servidor principal a una o varias bases de datos secundarias en instancias independientes del servidor secundario. Para más información, vea [Acerca del trasvase de registros &#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md).  
  
-   La replicación transaccional en tablas optimizadas para memoria en suscriptores se admite con algunas restricciones. Para obtener más información, vea [replicación en suscriptores de tablas con optimización para memoria](../replication/replication-to-memory-optimized-table-subscribers.md).  
  
-   Regulador de recursos: el regulador de recursos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] es una característica que puede utilizar para administrar la carga de trabajo y el consumo de recursos del sistema de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Resource Governor permite especificar la cantidad máxima de CPU, E/S física y memoria que pueden usar las solicitudes de aplicación entrantes. Para obtener más información, consulte [Managing Memory for In-Memory OLTP](../../database-engine/managing-memory-for-in-memory-oltp.md) y [Resource Governor](../resource-governor/resource-governor.md).  
  
-   OLTP en memoria tiene restricciones en las páginas de códigos compatibles para las columnas (var)char en tablas optimizadas para memoria y las intercalaciones compatibles utilizadas en índices y procedimientos almacenados compilados de forma nativa. Para obtener más información, consulte [Collations and Code Pages](../../database-engine/collations-and-code-pages.md).  
  
-   Compatibilidad con BACPAC.  
  
## <a name="ssnoversion-features-not-supported-for-in-memory-oltp"></a>[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Características no admitidas para OLTP en memoria  
 Las características siguientes de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no se admiten en una base de datos que tiene objetos optimizados para memoria (incluido el grupo de archivos de datos optimizados para memoria).  
  
|Característica no admitida|Descripción de la característica|  
|-------------------------|-------------------------|  
|Compresión de datos en tablas optimizadas para memoria.|Puede usar la característica de compresión de datos como ayuda para comprimir los datos de una base de datos y reducir el tamaño de la base de datos. Para obtener más información, consulte [Data Compression](../data-compression/data-compression.md).|  
|Creación de particiones de tablas optimizadas para memoria e índices HASH.|Los datos de tablas e índices con particiones se dividen en unidades que pueden propagarse por más de un grupo de archivos de la base de datos. Para obtener más información, vea [Partitioned Tables and Indexes](../partitions/partitioned-tables-and-indexes.md).|  
|Cifrado de datos transparente (TDE) en el grupo de archivos de datos optimizado para memoria de una base de datos.|El cifrado de datos transparente (TDE) realiza el cifrado y descifrado de E/S en tiempo real de los datos y los archivos de registro. Para obtener más información, vea [Cifrado de datos transparente &#40;TDE&#41;](../security/encryption/transparent-data-encryption.md).<br /><br /> El TDE se puede habilitar en una base de datos que tenga objetos de OLTP en memoria. Las entradas del registro de OLTP en memoria se cifran si se ha habilitado el TDE. Los archivos de punto de comprobación de las tablas durables no se cifran, incluso aunque el TDE esté habilitado en la base de datos.|  
|Replicación|Las configuraciones de replicación que no sean la replicación transaccional en tablas optimizadas para memoria en los suscriptores son incompatibles con tablas o vistas que hacen referencia a tablas optimizadas para memoria. La replicación mediante sync_mode = ' Database Snapshot ' no se admite si hay un grupo de archivos optimizados para memoria. Para obtener más información, vea [replicación en suscriptores de tablas con optimización para memoria](../replication/replication-to-memory-optimized-table-subscribers.md).|  
|Conjuntos de resultados activos múltiples (MARS)|Las tablas optimizadas para memoria no admiten Multiple Active Result Sets (MARS). Este error también puede indicar que se está usando un servidor vinculado. El servidor vinculado puede utilizar MARS. Las tablas optimizadas para memoria no admiten servidores vinculados. En su lugar, conéctese directamente al servidor y a la base de datos que hospedan las tablas optimizadas para memoria.|  
|Creación de reflejo|Creación de reflejo de la base de datos es una solución para aumentar la disponibilidad de una base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para obtener más información, vea [Creación de reflejo de la base de datos &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md).|  
|Recompilar el registro|La recompilación del registro, ya sea a través de un adjunto o de ALTER DATABASE, no se admite para bases de datos con un grupo de archivos MEMORY_OPTIMIZED_DATA.|  
|Servidor vinculado|Para obtener más información, vea [Servidores vinculados &#40;motor de base de datos&#41;](../linked-servers/linked-servers-database-engine.md).|  
|Registro masivo|Independientemente del modelo de recuperación de la base de datos, todas las operaciones en tablas durables optimizadas para memoria siempre se registran completamente.|  
|Registro mínimo|Las tablas optimizadas para memoria no admiten el registro mínimo. Para obtener más información sobre el registro mínimo, vea [El registro de transacciones &#40;SQL Server&#41;](../logs/the-transaction-log-sql-server.md) y [Requisitos previos para el registro mínimo durante la importación en bloque](../import-export/prerequisites-for-minimal-logging-in-bulk-import.md).|  
|Seguimiento de cambios|El seguimiento de cambios se puede habilitar en una base de datos con objetos de OLTP en memoria. Sin embargo, no se hace el seguimiento de los cambios en las tablas optimizadas para memoria.|  
|DDL, desencadenadores|En las tablas y los procedimientos almacenados compilados de forma nativa de OLTP en memoria no se admiten desencadenadores DDL de nivel de servidor ni de nivel de base de datos.|  
|Captura de datos modificados (CDC)|CDC no se debe habilitar en una base de datos que tiene objetos de OLTP en memoria, ya que impide determinadas operaciones como DROP.|  
|Contención de la base de datos|La contención de la base de datos no se admite en las bases de datos con procedimientos almacenados compilados de forma nativa y tablas optimizadas para memoria. Para obtener más información, vea bases de datos [independientes](../databases/contained-databases.md) .|  
|Conexiones de contexto|No se admite el acceso a las tablas optimizadas para memoria con la conexión de contexto desde procedimientos almacenados CLR.|  
|Cursores|Cursores de conjunto de claves y dinámicos en consultas que tienen acceso a tablas optimizadas para memoria. Estas consultas se degradan a estáticas que llegan a ser de solo lectura.|  
|TABLESTAMP|No se admite TABLESTAMP. Para obtener más información, vea [FROM &#40;Transact-SQL&#41;](/sql/t-sql/queries/from-transact-sql).|  
|AUTO_CLOSE|No se admite AUTO_CLOSE. Para obtener más información, consulte [Set the AUTO_CLOSE Database Option to OFF](../policy-based-management/set-the-auto-close-database-option-to-off.md).|  
|Instantáneas de base de datos|No se admiten las instantáneas de base de datos. Para más información, vea [Instantáneas de base de datos &#40;SQL Server&#41;](../databases/database-snapshots-sql-server.md).|  
|DDL transaccional|No se admite DDL transaccional en OLTP en memoria.|  
|Notificaciones de eventos|No se admiten las notificaciones de eventos. Para más información, consulte [Event Notifications](../service-broker/event-notifications.md).|  
|Modo de fibra|El modo de fibra no es compatible con OLTP en memoria.|  
|Administración basada en directivas (PBM).|No se admiten los modos de impedir y solo registrar de PBM. La existencia de estas directivas en el servidor puede impedir la correcta ejecución de DDL de OLTP en memoria. Se admiten los modos a petición y programado.|  
|Implementación o extracción de DACFX|No se admite la implementación/extracción de DAC Framework en OLTP en memoria.|  
  
 Con algunas excepciones, las transacciones entre bases de datos no se admiten. En la tabla siguiente se describen qué casos se admiten y las restricciones correspondientes. (Vea también [Consultas entre bases de datos](cross-database-queries.md)).  
  
|Bases de datos|Permitida|Description|  
|---------------|-------------|-----------------|  
|Bases de datos de usuario, modelo y msdb|No|Las consultas y transacciones entre bases de datos no se admiten.<br /><br /> Las consultas y transacciones que tienen acceso a tablas optimizadas para memoria o a procedimientos almacenados compilados de forma nativa no pueden tener acceso a otras bases de datos, excepto a las bases de datos del sistema maestra (acceso de solo lectura) y tempdb.|  
|Base de datos de recursos y tempdb|Yes|No hay restricciones en las transacciones entre bases de datos que, además de una base de datos de usuario único, usan solo la base de datos de recursos y tempdb.|  
|maestro|solo lectura|Las transacciones entre bases de datos que tocan OLTP en memoria y la base de datos maestra no pueden confirmarse si incluyen operaciones de escritura en la base de datos maestra. Se permiten las transacciones entre bases de datos que solo leen de la base de datos maestra y usan una base de datos de un solo usuario.|  
  
## <a name="see-also"></a>Consulte también  
 [Compatibilidad de SQL Server con OLTP en memoria](sql-server-support-for-in-memory-oltp.md)  
  
  
