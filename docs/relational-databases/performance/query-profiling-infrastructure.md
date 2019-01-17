---
title: Infraestructura de generación de perfiles de consultas | Microsoft Docs
ms.custom: ''
ms.date: 11/26/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- query plans [SQL Server]
- execution plans [SQL Server]
- query profiling
- lightweight query profiling
- lightweight profiling
- lwp
ms.assetid: 07f8f594-75b4-4591-8c29-d63811d7753e
author: pmasl
ms.author: pelopes
manager: amitban
ms.openlocfilehash: 39f3d82d65eb0dd05b8459742febd67d2bc56790
ms.sourcegitcommit: 0bb306da5374d726b1e681cd4b5459cb50d4a87a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2018
ms.locfileid: "53732032"
---
# <a name="query-profiling-infrastructure"></a>Infraestructura de generación de perfiles de consultas
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] ofrece la posibilidad de acceder a información en tiempo de ejecución sobre los planes de ejecución de consultas. Una de las acciones más importantes cuando se produce un problema de rendimiento es obtener una descripción precisa de la carga de trabajo que se está ejecutando y de cómo se controla el uso de recursos. Por eso es importante el acceso al [plan de ejecución real](../../relational-databases/performance/display-an-actual-execution-plan.md).

Aunque la finalización de una consulta es un requisito previo para la disponibilidad de un plan de consulta real, las [estadísticas de consultas dinámicas](../../relational-databases/performance/live-query-statistics.md) pueden proporcionar información en tiempo real sobre el proceso de ejecución de las consultas a medida que los datos fluyen de un [operador de plan de consulta](../../relational-databases/showplan-logical-and-physical-operators-reference.md) a otro. El plan de consulta activa muestra el progreso general de las consultas, así como estadísticas de tiempo de ejecución de nivel de operador como el número de filas, las filas generadas, el tiempo transcurrido, el progreso del operador, etc. Puesto que estos datos están disponibles en tiempo real sin necesidad de esperar a la finalización de la consulta, estas estadísticas de ejecución resultan extremadamente útiles para depurar problemas de rendimiento de consultas, como consultas de larga ejecución y consultas que se ejecutan de forma indefinida y nunca terminan.

## <a name="the-standard-query-execution-statistics-profiling-infrastructure"></a>Infraestructura de generación de perfiles de estadísticas de ejecución de consultas estándar

La *infraestructura de generación de perfiles de estadísticas de ejecución de consultas*, o generación de perfiles estándar, debe habilitarse para recopilar información sobre los planes de ejecución, concretamente el recuento de filas y el uso de CPU y E/S. Los siguientes métodos de recopilación de información de planes de ejecución para una **sesión de destino** aprovechan la infraestructura de generación de perfiles estándar:

- [SET STATISTICS XML](../../t-sql/statements/set-statistics-xml-transact-sql.md) 
- [SET STATISTICS PROFILE](../../t-sql/statements/set-statistics-profile-transact-sql.md)
- [Estadísticas de consultas activas](../../relational-databases/performance/live-query-statistics.md)

> [!NOTE]
> Al usar estadísticas de consulta dinámicas con [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)], se aprovecha la infraestructura de generación de perfiles estándar.    
> En versiones posteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], si la [infraestructura de generación de perfiles ligera](#lwp) está habilitada, son las estadísticas de consulta dinámicas las que la aprovechan, en lugar de la generación de perfiles estándar.

Los siguientes métodos de recopilación de información de planes de ejecución para **todas las sesiones** aprovechan la infraestructura de generación de perfiles estándar:

-  El evento extendido ***query_post_execution_showplan***. Para habilitar eventos extendidos, consulte [Monitor System Activity Using Extended Events](../../relational-databases/extended-events/monitor-system-activity-using-extended-events.md).  
- El evento de seguimiento **Showplan XML** de [Seguimiento de SQL](../../relational-databases/sql-trace/sql-trace.md) y [SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler.md). Para obtener más información sobre este evento de seguimiento, vea [Showplan XML [clase de eventos]](../../relational-databases/event-classes/showplan-xml-event-class.md).

Cuando se ejecuta una sesión de eventos extendidos que usa el evento *query_post_execution_showplan*, la DMV [sys.dm_exec_query_profiles](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-profiles-transact-sql.md) también se rellena, lo que habilita las estadísticas de consulta dinámicas para todas las sesiones mediante [Monitor de actividad](../../relational-databases/performance-monitor/activity-monitor.md) o una consulta directa a la DMV. Para obtener más información, consulte [Live Query Statistics](../../relational-databases/performance/live-query-statistics.md).

## <a name="lwp"></a> Infraestructura de generación de perfiles de estadísticas de ejecución de consultas ligera

A partir de [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] SP2 y [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], se ha incorporado una nueva *infraestructura de generación de perfiles de estadísticas de ejecución de consultas ligera*, o **generación de perfiles ligera**. 

> [!NOTE]
> Concretamente, los procedimientos almacenados compilados de forma nativa no se admiten con la generación de perfiles ligera.  

### <a name="lightweight-query-execution-statistics-profiling-infrastructure-v1"></a>Infraestructura de generación de perfiles de estadísticas de ejecución de consultas ligera v1

**Se aplica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (desde [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] SP2 hasta [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]). 
  
A partir de [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] SP2 y [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], se ha reducido la sobrecarga de rendimiento para recopilar información sobre los planes de ejecución gracias a la incorporación de la generación de perfiles ligera. A diferencia de la generación de perfiles estándar, la ligera no recopila información en tiempo de ejecución de CPU, aunque sigue recopilando la información de uso de E/S y de recuento de filas.

Además se ha incorporado un nuevo evento extendido***query_thread_profile*** que aprovecha la generación de perfiles ligera. Este evento extendido expone estadísticas de ejecución por operador, lo que ofrece más información sobre el rendimiento de cada nodo y subproceso. Se puede configurar una sesión de ejemplo con este evento extendido como en el ejemplo siguiente:

```sql
CREATE EVENT SESSION [NodePerfStats] ON SERVER
ADD EVENT sqlserver.query_thread_profile(
  ACTION(sqlos.scheduler_id,sqlserver.database_id,sqlserver.is_system,
    sqlserver.plan_handle,sqlserver.query_hash_signed,sqlserver.query_plan_hash_signed,
    sqlserver.server_instance_name,sqlserver.session_id,sqlserver.session_nt_username,
    sqlserver.sql_text))
ADD TARGET package0.ring_buffer(SET max_memory=(25600))
WITH (MAX_MEMORY=4096 KB,
  EVENT_RETENTION_MODE=ALLOW_SINGLE_EVENT_LOSS,
  MAX_DISPATCH_LATENCY=30 SECONDS,
  MAX_EVENT_SIZE=0 KB,
  MEMORY_PARTITION_MODE=NONE,
  TRACK_CAUSALITY=OFF,
  STARTUP_STATE=OFF);
```

> [!NOTE]
> Para más información sobre la sobrecarga de rendimiento del generación de perfiles de consulta, vea la entrada de blog [Developers Choice: Query progress - anytime, anywhere](https://blogs.msdn.microsoft.com/sql_server_team/query-progress-anytime-anywhere/) (Elección de los desarrolladores: progreso de la consulta, en cualquier momento y en cualquier lugar). 

Cuando se ejecuta una sesión de eventos extendidos que usa el evento *query_thread_profile*, la DMV [sys.dm_exec_query_profiles](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-profiles-transact-sql.md) también se rellena con la generación de perfiles ligera, lo que habilita las estadísticas de consulta dinámicas para todas las sesiones mediante [Monitor de actividad](../../relational-databases/performance-monitor/activity-monitor.md) o la consulta directa a la DMV.

### <a name="lightweight-query-execution-statistics-profiling-infrastructure-v2"></a>Infraestructura de generación de perfiles de estadísticas de ejecución de consultas ligera v2

**Se aplica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (desde [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1 hasta [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]). 

[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1 incluye una versión revisada de la generación de perfiles ligera con sobrecarga mínima. La generación de perfiles ligera también puede habilitarse de forma global mediante la [marca de seguimiento 7412](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) para las versiones indicadas anteriormente en *Se aplica a*. Se ha incorporado una nueva DMF [sys.dm_exec_query_statistics_xml](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-statistics-xml-transact-sql.md) para devolver el plan de ejecución de consultas de las solicitudes en curso.

A partir de [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP2 CU3 y [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] CU11, si la generación de perfiles ligera no está habilitada de forma global, se puede usar el nuevo argumento de [sugerencia de consulta USE HINT](../../t-sql/queries/hints-transact-sql-query.md#use_hint) **QUERY_PLAN_PROFILE** para habilitarla en el nivel de consulta y para cualquier sesión. Cuando una consulta que contiene esta nueva sugerencia finaliza, también se devuelve un nuevo evento extendido ***query_plan_profile*** que proporciona un archivo XML de plan de ejecución real similar al evento extendido *query_post_execution_showplan*. Se puede configurar una sesión de ejemplo con este evento extendido como en el ejemplo siguiente:

```sql
CREATE EVENT SESSION [PerfStats_LWP_Plan] ON SERVER
ADD EVENT sqlserver.query_plan_profile(
  ACTION(sqlos.scheduler_id,sqlserver.database_id,sqlserver.is_system,
    sqlserver.plan_handle,sqlserver.query_hash_signed,sqlserver.query_plan_hash_signed,
    sqlserver.server_instance_name,sqlserver.session_id,sqlserver.session_nt_username,
    sqlserver.sql_text))
ADD TARGET package0.ring_buffer(SET max_memory=(25600))
WITH (MAX_MEMORY=4096 KB,
  EVENT_RETENTION_MODE=ALLOW_SINGLE_EVENT_LOSS,
  MAX_DISPATCH_LATENCY=30 SECONDS,
  MAX_EVENT_SIZE=0 KB,
  MEMORY_PARTITION_MODE=NONE,
  TRACK_CAUSALITY=OFF,
  STARTUP_STATE=OFF);
```

### <a name="lightweight-query-execution-statistics-profiling-infrastructure-v3"></a>Infraestructura de generación de perfiles de estadísticas de ejecución de consultas ligera v3

**Se aplica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (a partir de [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)])

[!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] incluye una versión recién revisada de la generación de perfiles ligera que recopila información de recuento de filas para todas las ejecuciones. La generación de perfiles ligera está habilitada de forma predeterminada en [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] y la marca de seguimiento 7412 no tiene ningún efecto.

## <a name="remarks"></a>Notas

> [!IMPORTANT]
> Debido a un posible análisis AV aleatorio al ejecutar un procedimiento almacenado de supervisión que haga referencia a [sys.dm_exec_query_statistics_xml](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-statistics-xml-transact-sql.md), asegúrese de que [KB 4078596](http://support.microsoft.com/help/4078596) esté instalado en [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] y [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)].

A partir de la generación de perfiles ligera v2 y su baja sobrecarga, cualquier servidor que aún no esté enlazado a CPU puede ejecutar la generación de perfiles ligera **continuamente** y permitir que los profesionales de bases de datos pulsen en cualquier ejecución activa en cualquier momento, por ejemplo mediante Monitor de actividad o directamente al consultar a `sys.dm_exec_query_profiles`, y obtengan el plan de consulta con estadísticas en tiempo de ejecución.

Para más información sobre la sobrecarga de rendimiento del generación de perfiles de consulta, vea la entrada de blog [Developers Choice: Query progress - anytime, anywhere](https://blogs.msdn.microsoft.com/sql_server_team/query-progress-anytime-anywhere/) (Elección de los desarrolladores: progreso de la consulta, en cualquier momento y en cualquier lugar). 

## <a name="see-also"></a>Consulte también  
 [Supervisar y optimizar el rendimiento](../../relational-databases/performance/monitor-and-tune-for-performance.md)     
 [Herramientas de supervisión y optimización del rendimiento](../../relational-databases/performance/performance-monitoring-and-tuning-tools.md)     
 [Abrir el Monitor de actividad &#40;SQL Server Management Studio&#41;](../../relational-databases/performance-monitor/open-activity-monitor-sql-server-management-studio.md)     
 [Monitor de actividad](../../relational-databases/performance-monitor/activity-monitor.md)     
 [Monitoring Performance By Using the Query Store](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)     
 [Supervisar la actividad del sistema mediante eventos extendidos](../../relational-databases/extended-events/monitor-system-activity-using-extended-events.md)      
 [sys.dm_exec_query_statistics_xml](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-statistics-xml-transact-sql.md)     
 [sys.dm_exec_query_profiles](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-profiles-transact-sql.md)     
 [Marcas de seguimiento](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)    
 [Referencia de operadores lógicos y físicos del plan de presentación](../../relational-databases/showplan-logical-and-physical-operators-reference.md)    
 [Mostrar un plan de ejecución real](../../relational-databases/performance/display-an-actual-execution-plan.md)    
 [Estadísticas de consultas activas](../../relational-databases/performance/live-query-statistics.md)      
 [Developers Choice: Query progress - anytime, anywhere](https://blogs.msdn.microsoft.com/sql_server_team/query-progress-anytime-anywhere/) (Elección de los desarrolladores: progreso de la consulta, en cualquier momento y en cualquier lugar)
