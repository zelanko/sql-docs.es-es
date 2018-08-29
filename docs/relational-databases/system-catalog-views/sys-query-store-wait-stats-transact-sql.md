---
title: Sys.query_store_wait_stats (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 04/21/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.query_store_wait_stats
- query_store_wait_stats
dev_langs:
- TSQL
helpviewer_keywords:
- query_store_wait_stats catalog view
- sys.query_store_wait_stats catalog view
ms.assetid: ccf7a57c-314b-450c-bd34-70749a02784a
caps.latest.revision: 18
author: AndrejsAnt
ms.author: AndrejsAnt
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 22bb241da9d575225c87ac8fbed989f38551b907
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/27/2018
ms.locfileid: "43066374"
---
# <a name="sysquerystorewaitstats-transact-sql"></a>Sys.query_store_wait_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2017-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-asdb-xxxx-xxx-md.md)]

  Contiene información sobre la información de espera para la consulta.  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**wait_stats_id**|**bigint**|Identificador de la fila que representa las estadísticas de espera de plan_id, runtime_stats_interval_id, execution_type y wait_category. Es único solo para los últimos intervalos de estadísticas en tiempo de ejecución. Puede haber varias filas que representa las estadísticas de espera para el plan al que hace referencia plan_id, con el tipo de ejecución representado por execution_type y la categoría de espera representado por wait_category intervalo activo actualmente. Normalmente, una fila representa las estadísticas de espera que se vacían en disco, mientras que otros (s) representan el estado en memoria. Por lo tanto, para obtener el estado real de cada intervalo debe agregar las métricas, agrupando plan_id, runtime_stats_interval_id, execution_type y wait_category. |  
|**plan_id**|**bigint**|Clave externa. Se une a [sys.query_store_plan &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-plan-transact-sql.md).|  
|**runtime_stats_interval_id**|**bigint**|Clave externa. Se une a [sys.query_store_runtime_stats_interval &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-interval-transact-sql.md).|  
|**wait_category**|**tinyint**|Tipos de espera se clasifican según la tabla siguiente y, a continuación, se agrega el tiempo de espera en estas categorías de espera. Las distintas categorías de espera exigen un análisis de seguimiento diferente para resolver el problema, pero los tipos de espera de la misma categoría dan lugar a experiencias de solución de problemas muy similares; el proporcionar la consulta afectada además de las esperas sería la pieza que falta para completar correctamente la mayoría de las investigaciones de este tipo.|
|**wait_category_desc**|**nvarchar(128)**|Para obtener una descripción textual del campo de categoría de espera, consulte la tabla siguiente.|
|**execution_type**|**tinyint**|Determina el tipo de ejecución de la consulta:<br /><br /> 0: ejecución normal (finalizada correctamente)<br /><br /> 3 – cliente iniciada anulada ejecución<br /><br /> 4 - excepción anula la ejecución|  
|**execution_type_desc**|**nvarchar(128)**|Descripción textual del campo de tipo de ejecución:<br /><br /> 0: normal<br /><br /> 3 – anulada<br /><br /> 4 - excepción|  
|**total_query_wait_time_ms**|**bigint**|Total de CPU de tiempo de espera para el plan de consulta dentro del intervalo de agregación y categoría (comunicado en milisegundos) de espera.|
|**avg_query_wait_time_ms**|**float**|Promedio de duración para el plan de consulta por ejecución dentro de la categoría de espera y de intervalo de agregación (comunicada en milisegundos) de espera.|
|**last_query_wait_time_ms**|**bigint**|Último espere la duración del plan de consulta dentro del intervalo de agregación y categoría (comunicado en milisegundos) de espera.|
|**min_query_wait_time_ms**|**bigint**|CPU mínima tiempo de espera para el plan de consulta dentro del intervalo de agregación y categoría (comunicado en milisegundos) de espera.|
|**max_query_wait_time_ms**|**bigint**|Máximo de CPU tiempo de espera para el plan de consulta dentro del intervalo de agregación y categoría (comunicado en milisegundos) de espera.|
|**stdev_query_wait_time_ms**|**float**|Desviación estándar de duración para el plan de consulta dentro del intervalo de agregación de espera de consultas y (comunicado en milisegundos) de categoría de espera.|

 ## <a name="wait-categories-mapping-table"></a>Tabla de asignación de categorías de espera  
  *"%" se usa como un carácter comodín*
  
|Valor entero|Categoría de espera|Incluyen tipos de espera en la categoría|  
|-----------------|---------------|-----------------|  
|**0**|**Unknown**|Desconocido |  
|**1**|**CPU**|SOS_SCHEDULER_YIELD|
|**2**|**Subproceso de trabajo**|THREADPOOL|
|**3**|**Bloqueo**|LCK_M_ %|
|**4**|**Bloqueo temporal**|LATCH_ %|
|**5**|**Bloqueo temporal del búfer**|PAGELATCH_ %|
|**6**|**Búfer de E/S**|PAGEIOLATCH_ %|
|**7**|**Compilación***|RESOURCE_SEMAPHORE_QUERY_COMPILE|
|**8**|**CLR DE SQL**|CLR %, % SQLCLR|
|**9**|**La creación de reflejo**|DBMIRROR %|
|**10**|**Transaction**|XACT %, % DTC, TRAN_MARKLATCH_ %, % MSQL_XACT_ TRANSACTION_MUTEX|
|**11**|**Inactivo**|SLEEP_ %, LAZYWRITER_SLEEP, SQLTRACE_BUFFER_FLUSH, SQLTRACE_INCREMENTAL_FLUSH_SLEEP, SQLTRACE_WAIT_ENTRIES, FT_IFTS_SCHEDULER_IDLE_WAIT, XE_DISPATCHER_WAIT, REQUEST_FOR_DEADLOCK_SEARCH, LOGMGR_QUEUE, ONDEMAND_TASK_QUEUE, CHECKPOINT_ COLA, XE_TIMER_EVENT|
|**12**|**PreEmptive**|PREEMPTIVE_ %|
|**13**|**Service Broker**|BROKER_ % **(pero no BROKER_RECEIVE_WAITFOR)**|
|**14**|**Registro de tran**|LOGMGR, LOGBUFFER, LOGMGR_RESERVE_APPEND, LOGMGR_FLUSH, LOGMGR_PMM_LOG, CHKPT, WRITELOGF|
|**15**|**E/S de red**|ASYNC_NETWORK_IO, NET_WAITFOR_PACKET, PROXY_NETWORK_IO, EXTERNAL_SCRIPT_NETWORK_IOF|
|**16**|**Parallelism**|CXPACKET, EXCHANGE|
|**17**|**Memoria**|RESOURCE_SEMAPHORE, CMEMTHREAD, CMEMPARTITIONED, EE_PMOLOCK, MEMORY_ALLOCATION_EXT, RESERVED_MEMORY_ALLOCATION_EXT, MEMORY_GRANT_UPDATE|
|**18**|**Espera de usuario**|WAITFOR, WAIT_FOR_RESULTS, BROKER_RECEIVE_WAITFOR|
|**19**|**Seguimiento**|TRACEWRITE, SQLTRACE_LOCK, SQLTRACE_FILE_BUFFER, SQLTRACE_FILE_WRITE_IO_COMPLETION, SQLTRACE_FILE_READ_IO_COMPLETION, SQLTRACE_PENDING_BUFFER_WRITERS, SQLTRACE_SHUTDOWN, QUERY_TRACEOUT, TRACE_EVTNOTIFF|
|**20**|**Búsqueda de texto completo**|FT_RESTART_CRAWL, EL RECOPILADOR DE TEXTO COMPLETO, MSSEARCH, FT_METADATA_MUTEX, FT_IFTSHC_MUTEX, FT_IFTSISM_MUTEX, FT_IFTS_RWLOCK, FT_COMPROWSET_RWLOCK, FT_MASTER_MERGE, FT_PROPERTYLIST_CACHE, FT_MASTER_MERGE_COORDINATOR, PWAIT_RESOURCE_SEMAPHORE_FT_ PARALLEL_QUERY_SYNC|
|**21**|**Otras E/S de disco**|ASYNC_IO_COMPLETION, IO_COMPLETION, BACKUPIO, WRITE_COMPLETION, IO_QUEUE_LIMIT, IO_RETRY|
|**22**|**Replicación**|SE_REPL_ %, REPL_ %, % HADR_ **(pero no HADR_THROTTLE_LOG_RATE_GOVERNOR)**, PWAIT_HADR_ %, REPLICA_WRITES, FCB_REPLICA_WRITE, FCB_REPLICA_READ, PWAIT_HADRSIM|
|**23**|**Regulador de velocidad de registros**|LOG_RATE_GOVERNOR, POOL_LOG_RATE_GOVERNOR, HADR_THROTTLE_LOG_RATE_GOVERNOR, INSTANCE_LOG_RATE_GOVERNOR|

***Compilación** categoría de espera no se admite actualmente. 

  
## <a name="permissions"></a>Permisos  
 Requiere el **VIEW DATABASE STATE** permiso.  
  
## <a name="see-also"></a>Vea también  
 [sys.database_query_store_options &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md)   
 [sys.query_context_settings &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-context-settings-transact-sql.md)   
 [sys.query_store_plan &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-plan-transact-sql.md)   
 [Sys.query_store_query &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-query-transact-sql.md)   
 [sys.query_store_query_text &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-query-text-transact-sql.md)   
 [sys.query_store_runtime_stats_interval &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-interval-transact-sql.md)   
 [Monitoring Performance By Using the Query Store](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)   
 [Vistas de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Procedimientos almacenados de Query Store &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/query-store-stored-procedures-transact-sql.md)  
  
  
