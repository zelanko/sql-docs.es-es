---
title: Usar objetos de SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- server performance [SQL Server], objects for monitoring
- database monitoring [SQL Server], objects for monitoring
- charts [SQL Server]
- System Monitor [SQL Server], counters
- counters [SQL Server], listed
- objects [SQL Server], performance monitoring
- objects [SQL Server], Windows System Monitor
- performance counters [SQL Server], about performance counters
- System Monitor [SQL Server], objects
- performance counters [SQL Server]
- counters [SQL Server], about performance counters
- tuning databases [SQL Server], objects for monitoring
- database performance [SQL Server], objects for monitoring
- SQL Server, objects
- monitoring performance [SQL Server], objects for monitoring
- Windows System Monitor [SQL Server], objects
- Windows System Monitor [SQL Server], counters
- counters [SQL Server]
- performance counters [SQL Server], listed
ms.assetid: bcd731b1-3c4e-4086-b58a-af7a3af904ad
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: c073b0f438ec022e1b05f481652d6f08ef34cc53
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85066105"
---
# <a name="use-sql-server-objects"></a>Usar objetos de SQL Server
  Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] incluye objetos y contadores que el Monitor de sistema puede utilizar para supervisar la actividad de los equipos en los que se ejecute una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Un objeto es cualquier recurso de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , como un bloqueo de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o un proceso de Windows. Cada objeto contiene uno o más contadores que determinan diversos aspectos de los objetos que se van a supervisar. Por ejemplo, el objeto **Bloqueos de SQL Server** contiene los contadores **Número de interbloqueos/seg.** y **Tiempos de espera de bloqueos/seg.**  
  
 Algunos objetos tienen varias instancias si existen varios recursos de un determinado tipo en el equipo. Por ejemplo, el tipo de objeto **Procesador** tendrá varias instancias si un sistema contiene varios procesadores. El tipo de objeto **Bases de datos** tiene una instancia para cada base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Algunos tipos de objetos (por ejemplo, el objeto **Administrador de memoria** ) tienen solo una instancia. Si un tipo de objeto tiene varias instancias, puede agregar contadores para realizar un seguimiento de las estadísticas relativas a cada instancia o, en muchos casos, de todas las instancias a la vez. Los contadores de la instancia predeterminada aparecen con el formato **SQLServer:** _\<object name>_ . Los contadores de las instancias con nombre aparecen en el formato **MSSQL $** _\<instance name>_ **:** _\<counter name>_ o **SQLAgent $** _\<instance name>_ **:** _\<counter name>_ .  
  
 Al agregar o quitar contadores en el gráfico y guardar la configuración del gráfico, puede especificar los objetos y contadores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que se supervisan al iniciar el Monitor de sistema.  
  
 Puede configurar el Monitor de sistema para que muestre las estadísticas de cualquier contador de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Además, puede establecer un valor de umbral para cualquier contador de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y generar posteriormente una alerta cuando un contador supere dicho umbral. Para obtener más información sobre cómo establecer una alerta, vea [Crear una alerta de base de datos de SQL Server](create-a-sql-server-database-alert.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se muestran solo si se instala una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Si detiene y reinicia una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], se interrumpirá la presentación de estadísticas y, después, se reanudará automáticamente. Tenga en cuenta también que verá los contadores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en el complemento del Monitor de sistema incluso si [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no se está ejecutando. En una instancia en clúster, los contadores de rendimiento solo funcionan en el nodo en el que se ejecuta [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 Este tema contiene las siguientes secciones:  
  
-   [Objetos de rendimiento del Agente SQL Server](#SQLServerAgentPOs)  
  
-   [Objetos de rendimiento de Service Broker](#ServiceBrokerPOs)  
  
-   [Objetos de rendimiento de SQL Server](#SQLServerPOs)  
  
-   [Objetos de rendimiento de replicación de SQL Server](#SQLServerReplicationPOs)  
  
-   [Contadores de canalización SSIS](#SsisPipelineCounters)  
  
-   [Permisos necesarios](#RequiredPermissions)  
  
##  <a name="sql-server-agent-performance-objects"></a><a name="SQLServerAgentPOs"></a> Objetos de rendimiento del Agente SQL Server  
 En la tabla siguiente se enumeran los objetos de rendimiento proporcionados para el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] :  
  
|Objeto de rendimiento|Descripción|  
|------------------------|-----------------|  
|[SQLAgent:Alerts](sql-server-agent-alerts-object.md)|Proporciona información acerca de las alertas del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|  
|[SQLAgent:Jobs](sql-server-agent-jobs-object.md)|Proporciona información acerca de los trabajos del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|  
|[SQLAgent:JobSteps](sql-server-agent-jobsteps-object.md)|Proporciona información acerca de los pasos de trabajos del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|  
|[SQLAgent:Statistics](sql-server-agent-statistics-object.md)|Proporciona información acerca del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|  
  
##  <a name="service-broker-performance-objects"></a><a name="ServiceBrokerPOs"></a> Objetos de rendimiento de Service Broker  
 En la tabla siguiente se enumeran los objetos de rendimiento proporcionados para [!INCLUDE[ssSB](../../includes/sssb-md.md)].  
  
|Objeto de rendimiento|Descripción|  
|------------------------|-----------------|  
|[SQLServer:Broker Activation](sql-server-broker-activation-object.md)|Proporciona información acerca de las tareas activadas de [!INCLUDE[ssSB](../../includes/sssb-md.md)].|  
|[SQLServer:Broker Statistics](sql-server-broker-statistics-object.md)|Proporciona información general sobre [!INCLUDE[ssSB](../../includes/sssb-md.md)] .|  
|[SQLServer:Broker Transport](sql-server-broker-dbm-transport-object.md)|Proporciona información acerca de la conexión a red de [!INCLUDE[ssSB](../../includes/sssb-md.md)] .|  
  
##  <a name="sql-server-performance-objects"></a><a name="SQLServerPOs"></a> Objetos de rendimiento de SQL Server  
 En la tabla siguiente se describen los objetos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
|Objeto de rendimiento|Descripción|  
|------------------------|-----------------|  
|[SQLServer:Access Methods](sql-server-access-methods-object.md)|Mide y realiza búsquedas mediante objetos de base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y su asignación (por ejemplo, el número de búsquedas de índices o de páginas asignadas a índices y datos).|  
|[SQLServer:Backup Device](sql-server-backup-device-object.md)|Proporciona información acerca de dispositivos de copia de seguridad utilizados para operaciones de copias de seguridad y restauración, como el rendimiento del dispositivo.|  
|[SQLServer:Buffer Manager](sql-server-buffer-manager-object.md)|Proporciona información acerca de los búferes de memoria que utiliza [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], como la **memoria disponible** y la **proporción de aciertos de caché del búfer**.|  
|[SQL Server:Buffer Node](sql-server-buffer-node.md)|Proporciona información acerca de la frecuencia con que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] solicita páginas libres y obtiene acceso a las mismas.|  
|[SQLServer:CLR](sql-server-clr-object.md)|Proporciona información acerca de Common Language Runtime (CLR).|  
|[SQLServer:Cursor Manager by Type](sql-server-cursor-manager-by-type-object.md)|Proporciona información acerca de los cursores.|  
|[SQLServer:Cursor Manager Total](sql-server-cursor-manager-total-object.md)|Proporciona información acerca de los cursores.|  
|[SQLServer:Database Mirroring](sql-server-database-mirroring-object.md)|Proporciona información acerca de la creación de reflejos de la base de datos.|  
|[SQLServer:Databases](sql-server-databases-object.md)|Proporciona información acerca de una base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , como la cantidad de espacio de registro disponible o el número de transacciones activas en la base de datos. Pueden existir múltiples instancias de este objeto.|  
|[SQL Server:Deprecated Features](sql-server-deprecated-features-object.md)|Cuenta el número de veces que se usan las características obsoletas.|  
|[SQLServer:Exec Statistics](sql-server-execstatistics-object.md)|Proporciona información acerca de las estadísticas de ejecución.|  
|[SQLServer:General Statistics](sql-server-general-statistics-object.md)|Proporciona información acerca de la actividad general de todo el servidor, como el número de usuarios conectados a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|[SQL Server:HADR Availability Replica](sql-server-availability-replica.md)|Proporciona información acerca de las alertas del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssHADR](../../includes/sshadr-md.md)] .|  
|[SQL Server:HADR Database Replica](sql-server-database-replica.md)|Proporciona información acerca de las réplicas de base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssHADR](../../includes/sshadr-md.md)] .|  
|[SQLServer:Latches](sql-server-latches-object.md)|Proporciona información acerca de los bloqueos temporales de los recursos internos, como las páginas de las bases de datos que utiliza [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|[SQLServer:Locks](sql-server-locks-object.md)|Proporciona información acerca de las solicitudes de bloqueo individuales que realiza [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], como los tiempos de espera de bloqueos y los interbloqueos. Pueden existir múltiples instancias de este objeto.|  
|[SQLServer:Memory Manager](sql-server-memory-manager-object.md)|Proporciona información acerca de la utilización de memoria de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] como, por ejemplo, el número total de estructuras de bloqueo asignadas actualmente.|  
|[SQLServer:Caché del plan](sql-server-plan-cache-object.md)|Proporciona información acerca de la caché de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que se utiliza para almacenar objetos como procedimientos almacenados, desencadenadores y planes de consultas.|  
|[SQLServer: Estadísticas de grupo de recursos](sql-server-resource-pool-stats-object.md)|Proporciona información sobre las estadísticas del grupo de recursos de servidor del regulador de recursos.|  
|[SQLServer:SQL Errors](sql-server-sql-errors-object.md)|Proporciona información acerca de los errores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|  
|[SQLServer:SQL Statistics](sql-server-sql-statistics-object.md)|Proporciona información acerca de aspectos de consultas de [!INCLUDE[tsql](../../includes/tsql-md.md)] , como el número de lotes de instrucciones [!INCLUDE[tsql](../../includes/tsql-md.md)] que recibe [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|[SQLServer:Transactions](sql-server-transactions-object.md)|Proporciona información acerca de las transacciones activas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], como el número global de transacciones y el número de transacciones de instantáneas.|  
|[SQLServer:User Settable](sql-server-user-settable-object.md)|Realiza una supervisión personalizada. Cada contador puede ser un procedimiento almacenado personalizado o cualquier instrucción [!INCLUDE[tsql](../../includes/tsql-md.md)] que devuelva un valor para supervisar.|  
|[SQLServer: Estadísticas de espera](sql-server-wait-statistics-object.md)|Proporciona información acerca de las esperas.|  
|[SQLServer: Estadísticas de grupo de cargas de trabajo](sql-server-workload-group-stats-object.md)|Proporciona información sobre las estadísticas de grupo de cargas de trabajo del regulador de recursos.|  
  
##  <a name="sql-server-replication-performance-objects"></a><a name="SQLServerReplicationPOs"></a> Objetos de rendimiento de replicación de SQL Server  
 En la tabla siguiente se enumeran los objetos de rendimiento proporcionados para la replicación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] :  
  
|Objeto de rendimiento|Descripción|  
|------------------------|-----------------|  
|**SQLServer:Agentes de replicación**<br /><br /> **SQLServer:Instantánea de replicación**<br /><br /> **SQLServer:Lector del registro de replicación**<br /><br /> **SQLServer:Distribuidor de replicación**<br /><br /> **SQLServer:Mezcla de replicación**<br /><br /> Para más información, consulte [Monitoring Replication with System Monitor](../replication/monitor/monitoring-replication-with-system-monitor.md).|Proporciona información acerca de la actividad del agente de replicación.|  
  
##  <a name="ssis-pipeline-counters"></a><a name="SsisPipelineCounters"></a> Contadores de canalización SSIS  
 Para el contador **Canalización SSIS** , vea [Contadores de rendimiento](../../integration-services/performance/performance-counters.md).  
  
##  <a name="required-permissions"></a><a name="RequiredPermissions"></a> Permisos necesarios  
 La posibilidad de utilizar los objetos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] depende de los permisos de Windows, salvo **SQLAgent:Alertas**. Los usuarios deben ser miembros del rol fijo de servidor **sysadmin** para poder utilizar **SQLAgent:Alerts**.  
  
## <a name="see-also"></a>Consulte también  
 [Usar objetos de rendimiento](../../ssms/agent/use-performance-objects.md)   
 [sys.dm_os_performance_counters &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-os-performance-counters-transact-sql)  
  
  
