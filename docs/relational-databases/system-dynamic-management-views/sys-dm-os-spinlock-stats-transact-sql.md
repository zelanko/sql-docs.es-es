---
description: sys.dm_os_spinlock_stats (Transact-SQL)
title: sys.dm_os_spinlock_stats (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/03/2019
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: ''
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_os_spinlock_stats_TSQL
- dm_os_spinlock_stats_TSQL
- dm_os_spinlock_stats
- sys.dm_os_spinlock_stats
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_spinlock_stats dynamic management view
author: bluefooted
ms.author: pamela
ms.reviewer: maghan
manager: amitban
ms.openlocfilehash: 31f89519a70612ba22c2fda79218d9d92153109f
ms.sourcegitcommit: 04cf7905fa32e0a9a44575a6f9641d9a2e5ac0f8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/07/2020
ms.locfileid: "91810111"
---
# <a name="sysdm_os_spinlock_stats-transact-sql"></a>sys.dm_os_spinlock_stats (Transact-SQL)

[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

Devuelve información sobre todas las esperas de Spinlock organizadas por tipo.  
  

|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|name|**nvarchar(256)**|Nombre del tipo de Spinlock.|  
|colisiones|**bigint**|El número de veces que un subproceso intenta adquirir el Spinlock y se bloquea porque otro subproceso contiene el Spinlock actualmente.|  
|pone marcha|**bigint**|El número de veces que un subproceso ejecuta un bucle mientras intenta adquirir Spinlock.|  
|spins_per_collision|**real**|Proporción de giros por colisión.|  
|sleep_time|**bigint**|Cantidad de tiempo en milisegundos que los subprocesos invirtieron en el caso de una interrupción.|  
|retroceso|**int**|El número de veces que un subproceso que "gira" no puede adquirir el Spinlock y produce el programador.|  


## <a name="permissions"></a>Permisos  
En [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] , requiere el `VIEW SERVER STATE` permiso.   
En [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] los niveles Premium, requiere el `VIEW DATABASE STATE` permiso en la base de datos. En [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] los niveles estándar y básico, requiere el  **Administrador del servidor** o una cuenta de **Administrador de Azure Active Directory** .    
  
## <a name="remarks"></a>Observaciones  
 
 sys.dm_os_spinlock_stats se puede usar para identificar el origen de la contención de Spinlock. En algunas situaciones, es posible que pueda resolver o reducir la contención de Spinlock. No obstante, puede haber situaciones que requerirán ponerse en contacto con los servicios de soporte al cliente de [!INCLUDE[msCoName](../../includes/msconame-md.md)].  
  
 Puede restablecer el contenido de sys.dm_os_spinlock_stats mediante el uso `DBCC SQLPERF` de la siguiente manera:  
  
```  
DBCC SQLPERF ('sys.dm_os_spinlock_stats', CLEAR);  
GO  
```  
  
 Esto restablece todos los recuentos en 0.  
  
> [!NOTE]  
>  Estas estadísticas no permanecen si [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se reinicia. Todos los datos se acumulan desde la última vez que se restablecieron las estadísticas o desde que se inició [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="spinlocks"></a>Bloqueos por subproceso  
 Un Spinlock es un objeto de sincronización ligero que se usa para serializar el acceso a las estructuras de datos que normalmente se conservan durante un breve período de tiempo. Cuando un subproceso intenta tener acceso a un recurso protegido por un Spinlock que está siendo mantenido por otro subproceso, el subproceso ejecutará un bucle, o "gira" e intentará tener acceso al recurso de nuevo, en lugar de producir inmediatamente el programador como con un bloqueo temporal u otra espera de recurso. El subproceso continuará girando hasta que el recurso esté disponible o el bucle se complete, momento en el cual el subproceso producirá el programador y volverá a la cola ejecutable. Esta práctica ayuda a reducir el cambio excesivo de contexto de subprocesos, pero cuando la contención de un Spinlock es alta, se puede observar un uso significativo de la CPU.
   
 La siguiente tabla contiene breves descripciones de algunos de los tipos de Spinlock más comunes.  
  
|Tipo Spinlock|Descripción|  
|-----------------|-----------------|  
|ABR|Exclusivamente para uso interno.|
|ADB_CACHE|Exclusivamente para uso interno.|
|ALLOC_CACHES_HASH|Exclusivamente para uso interno.|
|APPENDONLY_STORAGE|Exclusivamente para uso interno.|
|APRC_BACK_OFF_STATS|Exclusivamente para uso interno.|
|APRC_EVENT_LIST|Exclusivamente para uso interno.|
|APRC_QUEUE_LIST|Exclusivamente para uso interno.|
|APRC_VALIDATION_QUEUE_LIST|Exclusivamente para uso interno.|
|ASYNC_OP_ADMIN_CLIENT_REGISTRATION_LIST|Exclusivamente para uso interno.|
|ASYNC_OP_ADMIN_WORK_REGISTRATION_HASH_TABLE|Exclusivamente para uso interno.|
|ASYNCSTATSLIST|Exclusivamente para uso interno.|
|BACKUP|Exclusivamente para uso interno.|
|BACKUP_COPY_CONTEXT|Exclusivamente para uso interno.|
|BACKUP_CTX|Exclusivamente para uso interno.|
|BASE_XACT_HASH|Exclusivamente para uso interno.|
|BLOCKER_ENUM|Exclusivamente para uso interno.|
|BPREPARTITION|Exclusivamente para uso interno.|
|BPWORKFILE|Exclusivamente para uso interno.|
|BUF_HASH|Exclusivamente para uso interno.|
|BUF_LINK|Exclusivamente para uso interno.|
|BUF_WRITE_LOG|Exclusivamente para uso interno.|
|CACHEOBJ_DBG|Exclusivamente para uso interno.|
|CHANNELFORCECLOSEMANAGER|Exclusivamente para uso interno.|
|CHECK_AGGREGATE_STATE|Exclusivamente para uso interno.|
|CLR_HOSTTASK|Exclusivamente para uso interno.|
|CLR_SPIN_LOCK|Exclusivamente para uso interno.|
|CMED_DATABASE|Exclusivamente para uso interno.|
|CMED_HASH_SET|Exclusivamente para uso interno.|
|COLUMNDATASETSESSIONLIST|Exclusivamente para uso interno.|
|COLUMNSTORE_HASHTABLE|Exclusivamente para uso interno.|
|COLUMNSTOREBUILDSTATE_LIST|Exclusivamente para uso interno.|
|COM_INIT|Exclusivamente para uso interno.|
|CONFIRMABLE|Exclusivamente para uso interno.|
|COMPPLAN_SKELETON|Exclusivamente para uso interno.|
|CONNECTION_MANAGER|Exclusivamente para uso interno.|
|CONEXIÓN|Exclusivamente para uso interno.|
|CSIBUILDMEM|Exclusivamente para uso interno.|
|CURSOR|Exclusivamente para uso interno.|
|CURSQL|Exclusivamente para uso interno.|
|DATAPORTCONSUMER|Exclusivamente para uso interno.|
|DATAPORTSOURCEINFOCREDIT|Exclusivamente para uso interno.|
|DATAPORTSOURCEINFOQUEUE|Exclusivamente para uso interno.|
|DATASET_FREELIST|Exclusivamente para uso interno.|
|DBCC_CHECK|Exclusivamente para uso interno.|
|DBSEEDING_OPERATION|Exclusivamente para uso interno.|
|DBT_HASH|Exclusivamente para uso interno.|
|DBT_IO_LIST|Exclusivamente para uso interno.|
|DBTABLE|Controla el acceso a una estructura de datos en memoria para cada base de datos de una SQL Server que contiene las propiedades de esa base de datos. Consulte [este artículo](https://techcommunity.microsoft.com/t5/SQL-Server/Improving-Concurrency-Scalability-of-SQL-Server-workload-by/ba-p/384789) para más información. |
|DEFERRED_WF_EXT_DROP|Exclusivamente para uso interno.|
|DEK_INSTANCE|Exclusivamente para uso interno.|
|DELAYED_PARTITIONED_STACK|Exclusivamente para uso interno.|
|DELETEBITMAP|Exclusivamente para uso interno.|
|DIAG_MANAGER|Exclusivamente para uso interno.|
|DIAG_OBJECT|Exclusivamente para uso interno.|
|DIGEST_CACHE|Exclusivamente para uso interno.|
|DINPBUF|Exclusivamente para uso interno.|
|DIRECTLOGCONSUMER|Exclusivamente para uso interno.|
|DP_LIST|Controla el acceso a la lista de páginas desfasadas para una base de datos que tiene activado el punto de comprobación indirecto. Consulte [este artículo](https://techcommunity.microsoft.com/t5/SQL-Server/Indirect-Checkpoint-and-tempdb-8211-the-good-the-bad-and-the-non/ba-p/385510) para más información.|
|DROP|Exclusivamente para uso interno.|
|DROP_TEMPO|Exclusivamente para uso interno.|
|DROPPED_ALLOC_UNIT|Exclusivamente para uso interno.|
|DTC_HASHTABLE|Exclusivamente para uso interno.|
|DTT_LIST|Exclusivamente para uso interno.|
|ENDD_LIST|Exclusivamente para uso interno.|
|EXT_CACHE|Exclusivamente para uso interno.|
|EXTENT_ACTIVATION|Exclusivamente para uso interno.|
|FABRIC_DB_MGR_PTR|Exclusivamente para uso interno.|
|FABRIC_LOG_MANAGEMENT_INPUT_VALUE|Exclusivamente para uso interno.|
|FABRIC_REPLICA_TRANSPORT|Exclusivamente para uso interno.|
|FABRIC_TVF_DATA_CONSUMER_LIST|Exclusivamente para uso interno.|
|FABRIC_TVF_LOAD_LIB|Exclusivamente para uso interno.|
|FCB_REPLICA_SYNC|Exclusivamente para uso interno.|
|FGCB_PRP_FILL|Exclusivamente para uso interno.|
|FILE_HANDLE_CACHE|Exclusivamente para uso interno.|
|FILE_TABLE|Exclusivamente para uso interno.|
|FILESTREAM_CHUNKER|Exclusivamente para uso interno.|
|FREE_SPACE_CACHE_ENTRY|Exclusivamente para uso interno.|
|FS_CONTAINER_LIST_WITH_DELETE|Exclusivamente para uso interno.|
|FS_DELETED_FOLDER_CLEANUP|Exclusivamente para uso interno.|
|FSAGENT|Exclusivamente para uso interno.|
|FSGHOST_STATUS|Exclusivamente para uso interno.|
|FT_INIT|Exclusivamente para uso interno.|
|GHOST_FREE|Exclusivamente para uso interno.|
|GHOST_HASH|Exclusivamente para uso interno.|
|GLOBAL_SCHEDULER_LIST|Exclusivamente para uso interno.|
|GLOBAL_TRACE_FLAGS|Exclusivamente para uso interno.|
|GLOBALTRANS|Exclusivamente para uso interno.|
|GROUP_COMMIT_FEEDBACK_LOOP|Exclusivamente para uso interno.|
|GUARDIAN|Exclusivamente para uso interno.|
|HADR_AGH_X_ACCESS|Exclusivamente para uso interno.|
|HADR_AR_CONTROLLER_COLLECTION|Exclusivamente para uso interno.|
|HADR_AR_DB_MGR|Exclusivamente para uso interno.|
|HADR_AR_TRANSPORT|Exclusivamente para uso interno.|
|HADR_COMPRESSION_MGR_POOL|Exclusivamente para uso interno.|
|HADR_FABRIC_FACTORY|Exclusivamente para uso interno.|
|HADR_PRIORITY_QUEUE|Exclusivamente para uso interno.|
|HADR_TRANSPORT_CONTROL|Exclusivamente para uso interno.|
|HADR_TRANSPORT_LIST|Exclusivamente para uso interno.|
|HADRSEEDINGLIST|Exclusivamente para uso interno.|
|HOBT_DROPPED|Exclusivamente para uso interno.|
|HOBT_HASH|Exclusivamente para uso interno.|
|HTTP|Exclusivamente para uso interno.|
|HTTP_CONNCACHE|Exclusivamente para uso interno.|
|HTTP_ENDPOINT|Exclusivamente para uso interno.|
|IDENTITY|Exclusivamente para uso interno.|
|INDEX_CREATE|Exclusivamente para uso interno.|
|IO_DISPENSER_PAUSE|Exclusivamente para uso interno.|
|IO_RG_VOLUME_HASHTABLE|Exclusivamente para uso interno.|
|IOREQ|Exclusivamente para uso interno.|
|ISSRESOURCE|Exclusivamente para uso interno.|
|KTM_ENLISTMENT|Exclusivamente para uso interno.|
|LANG_RES_LOAD|Exclusivamente para uso interno.|
|LIVE_TARGET_TVF|Exclusivamente para uso interno.|
|LOCK_FREE_LIST|Exclusivamente para uso interno.|
|LOCK_HASH|Protege el acceso a la tabla hash del administrador de bloqueos que almacena información acerca de los bloqueos que se mantienen en una base de datos. Consulte [este artículo](https://support.microsoft.com/kb/2926217) para más información.|
|LOCK_NOTIFICATION|Exclusivamente para uso interno.|
|LOCK_RESOURCE_ID|Exclusivamente para uso interno.|
|LOCK_RW_ABTX_HASH_SET|Exclusivamente para uso interno.|
|LOCK_RW_AGDB_HEALTH_DIAG|Exclusivamente para uso interno.|
|LOCK_RW_CMED_HASH_SET|Exclusivamente para uso interno.|
|LOCK_RW_DPT_TABLE|Exclusivamente para uso interno.|
|LOCK_RW_IN_ROW_TRACKER|Exclusivamente para uso interno.|
|LOCK_RW_LOGIN_RATE_STATS|Exclusivamente para uso interno.|
|LOCK_RW_PVS_PAGE_TRACKER|Exclusivamente para uso interno.|
|LOCK_RW_RBIO_REQ|Exclusivamente para uso interno.|
|LOCK_RW_SECURITY_CACHE|Exclusivamente para uso interno.|
|LOCK_RW_TEST|Exclusivamente para uso interno.|
|LOCK_RW_WPR_BUCKET|Exclusivamente para uso interno.|
|LOCK_SORT_STREAM|Exclusivamente para uso interno.|
|LOCK_SQLSATELLITE_MESSAGE|Exclusivamente para uso interno.|
|LOG_CONSOLIDATION|Exclusivamente para uso interno.|
|LOG_RG_GOVERNOR|Exclusivamente para uso interno.|
|LOGCACHE_ACCESS|Exclusivamente para uso interno.|
|LOGFLUSHQ|Exclusivamente para uso interno.|
|LOGIOSEQ|Exclusivamente para uso interno.|
|LOGIOSEQMAPPENDINGMESSAGEQUEUE|Exclusivamente para uso interno.|
|LOGLC|Exclusivamente para uso interno.|
|LOGLFM|Exclusivamente para uso interno.|
|LOGON_TRIGGER_CACHE|Exclusivamente para uso interno.|
|LOGPOOL_HASHBUCKET|Exclusivamente para uso interno.|
|LOGPOOL_REFCOUNTEDOBJECT|Exclusivamente para uso interno.|
|LOGPOOL_SHAREDCACHEBUFFER|Exclusivamente para uso interno.|
|LOGPOOL_SIZEPERRESOURCEPOOL|Exclusivamente para uso interno.|
|LPE_BATCH|Exclusivamente para uso interno.|
|LPE_SESSION|Exclusivamente para uso interno.|
|LPE_SXTP|Exclusivamente para uso interno.|
|LSID|Exclusivamente para uso interno.|
|LSLIST|Exclusivamente para uso interno.|
|LSNREFLIST|Exclusivamente para uso interno.|
|LSS_SYNC_DTC|Exclusivamente para uso interno.|
|MD_CHANGE_NOTIFICATION|Exclusivamente para uso interno.|
|MDB_REMOTE_BATCH_STATS_HASH_TABLE|Exclusivamente para uso interno.|
|MDB_REMOTE_SESSION_HASH_TABLE|Exclusivamente para uso interno.|
|MEM_MGR|Exclusivamente para uso interno.|
|MGR_CACHE|Exclusivamente para uso interno.|
|MIGRATION_BUF_LIST|Exclusivamente para uso interno.|
|NETCONN_ADDRESS|Exclusivamente para uso interno.|
|ONDEMAND_TASK|Exclusivamente para uso interno.|
|ONE_PROC_SIM_NODE_CONTEXT|Exclusivamente para uso interno.|
|ONE_PROC_SIM_NODE_CONTEXT_LIST|Exclusivamente para uso interno.|
|ONE_PROC_SIM_REPLICA_CONTEXT|Exclusivamente para uso interno.|
|ONE_PROC_SIM_SERVICE_PARTITION|Exclusivamente para uso interno.|
|OPT_IDX_MISS_ID|Exclusivamente para uso interno.|
|OPT_IDX_MISS_KEY|Exclusivamente para uso interno.|
|OPT_IDX_STATS|Exclusivamente para uso interno.|
|OPT_INFO_MGR|Exclusivamente para uso interno.|
|PAGE_WORKITEMLIST|Exclusivamente para uso interno.|
|PAGECOPIER|Exclusivamente para uso interno.|
|PARALLELREDOCACHE|Exclusivamente para uso interno.|
|PARTITIONED_HEAP_FREE_LIST|Exclusivamente para uso interno.|
|PROGRESS_REPORT|Exclusivamente para uso interno.|
|QE_SHUTDOWN|Exclusivamente para uso interno.|
|QSCAN_CACHE|Exclusivamente para uso interno.|
|QUERY_EXEC_STATS|Exclusivamente para uso interno.|
|QUERY_STORE_ASYNC_PERSIST|Exclusivamente para uso interno.|
|QUERY_STORE_ASYNC_QUEUE_TLIST|Exclusivamente para uso interno.|
|QUERY_STORE_CAPTURE_POLICY_INTERVAL|Exclusivamente para uso interno.|
|QUERY_STORE_CAPTURE_POLICY_STATS|Exclusivamente para uso interno.|
|QUERY_STORE_CAPTURE_POLICY_THRESHOLD|Exclusivamente para uso interno.|
|QUERY_STORE_CURRENT_INTERVAL|Exclusivamente para uso interno.|
|QUERY_STORE_HT_CACHE|Exclusivamente para uso interno.|
|QUERY_STORE_LIST|Exclusivamente para uso interno.|
|QUERY_STORE_PLAN_COMP_AGG|Exclusivamente para uso interno.|
|QUERY_STORE_PLAN_LIST|Exclusivamente para uso interno.|
|QUERY_STORE_READ_ONLY_FLAGS|Exclusivamente para uso interno.|
|QUERY_STORE_SELF_AGG|Exclusivamente para uso interno.|
|QUERY_STORE_STMT_COMP_AGG|Exclusivamente para uso interno.|
|QUERYEXEC|Exclusivamente para uso interno.|
|QUERYSCAN|Exclusivamente para uso interno.|
|RANGE_GENERATION|Exclusivamente para uso interno.|
|READ_AHEAD|Exclusivamente para uso interno.|
|REDOMGRSTATE|Exclusivamente para uso interno.|
|REMOTE_SESSION_CACHE|Exclusivamente para uso interno.|
|REMOTEBLOCKIO|Exclusivamente para uso interno.|
|REMOTEOP|Exclusivamente para uso interno.|
|REPL_LOGREADER_HISTORY_CACHE|Exclusivamente para uso interno.|
|REPL_LOGREADER_PERDB_HISTORY_CACHE|Exclusivamente para uso interno.|
|RESMANAGER|Exclusivamente para uso interno.|
|RECURSO|Exclusivamente para uso interno.|
|RESQUEUE|Exclusivamente para uso interno.|
|RFS_THREAD_QUEUE|Exclusivamente para uso interno.|
|RG_TIMER|Exclusivamente para uso interno.|
|ROWGROUP_VERSIONS|Exclusivamente para uso interno.|
|RPCCHANNELPOOL|Exclusivamente para uso interno.|
|RPCPACKAGE|Exclusivamente para uso interno.|
|RPCREQUESTORCONTEXT|Exclusivamente para uso interno.|
|RWLOCK_LAST|Exclusivamente para uso interno.|
|SATELLITE_CONNECTION|Exclusivamente para uso interno.|
|SBS_CLIENT_ENDPOINTS|Exclusivamente para uso interno.|
|SBS_CLIENT_REQUESTS|Exclusivamente para uso interno.|
|SBS_DISPATCH|Exclusivamente para uso interno.|
|SBS_PENDING|Exclusivamente para uso interno.|
|SBS_SERVER_XACT_TASK_PROXY|Exclusivamente para uso interno.|
|SBS_TRANSPORT|Exclusivamente para uso interno.|
|SBS_UCS_DISPATCH|Exclusivamente para uso interno.|
|SEGURIDAD|Exclusivamente para uso interno.|
|SECURITY_CACHE|Exclusivamente para uso interno.|
|SECURITY_FEDAUTH_AAD_BECWSCONNS|Exclusivamente para uso interno.|
|SEMANTIC_TICACHE|Exclusivamente para uso interno.|
|SEQUENCED_OBJECT|Exclusivamente para uso interno.|
|SEQUEUE_SIZED_THREADSAFE|Exclusivamente para uso interno.|
|SESSION_KILLER|Exclusivamente para uso interno.|
|SESSION_MANAGER|Exclusivamente para uso interno.|
|SESSION_SEC_CONTEXT|Exclusivamente para uso interno.|
|SETRANGE_SYNC|Exclusivamente para uso interno.|
|SHARABLE_SESSION_OBJECTS|Exclusivamente para uso interno.|
|SLO_INFO_LIST|Exclusivamente para uso interno.|
|SNI|Exclusivamente para uso interno.|
|SNI_NODE_PENDING_IO_QUEUE|Exclusivamente para uso interno.|
|SOAPSESSIONS|Exclusivamente para uso interno.|
|SOS_ABORT_TASK|Exclusivamente para uso interno.|
|SOS_ACTIVEDESCRIPTOR|Exclusivamente para uso interno.|
|SOS_BLOCKALLOCPARTIALLIST|Exclusivamente para uso interno.|
|SOS_BLOCKDESCRIPTORBUCKET|Exclusivamente para uso interno.|
|SOS_CACHESTORE|Sincroniza el acceso a varias cachés en memoria en SQL Server como la caché del plan o la memoria caché de la tabla temporal. La contención intensiva en este tipo de Spinlock puede significar muchos aspectos diferentes en función de la memoria caché específica que se encuentra en la contención. Póngase en contacto con los [!INCLUDE[msCoName](../../includes/msconame-md.md)] servicios de soporte al cliente para obtener ayuda para solucionar este tipo de Spinlock. |
|SOS_CACHESTORE_CLOCK|Exclusivamente para uso interno.|
|SOS_CLOCKALG_INTERNODE_SYNC|Exclusivamente para uso interno.|
|SOS_DEBUG_HOOK|Exclusivamente para uso interno.|
|SOS_DESCDATABUFFERLIST|Exclusivamente para uso interno.|
|SOS_LARGEPAGE_ALLOCATOR|Exclusivamente para uso interno.|
|SOS_MINITHREAD|Exclusivamente para uso interno.|
|SOS_NODE|Exclusivamente para uso interno.|
|SOS_OBJECT_POOL|Exclusivamente para uso interno.|
|SOS_OBJECT_STORE|Exclusivamente para uso interno.|
|SOS_OOM_CHECK|Exclusivamente para uso interno.|
|SOS_PHYS_PAGE_CACHE|Exclusivamente para uso interno.|
|SOS_RESOURCE_CLERK_LIST|Exclusivamente para uso interno.|
|SOS_RINGBUFFER_RECORD|Exclusivamente para uso interno.|
|SOS_RW|Exclusivamente para uso interno.|
|SOS_SATELLITE_USER_POOL|Exclusivamente para uso interno.|
|SOS_SCHEDULER|Exclusivamente para uso interno.|
|SOS_SELIST_SIZED_SLOCK|Exclusivamente para uso interno.|
|SOS_SUSPEND_QUEUE|Exclusivamente para uso interno.|
|SOS_SYSTHREAD|Exclusivamente para uso interno.|
|SOS_SYSTHREAD_DISPATCHER|Exclusivamente para uso interno.|
|SOS_TASK|Exclusivamente para uso interno.|
|SOS_TLIST|Exclusivamente para uso interno.|
|SOS_VM_LOW|Exclusivamente para uso interno.|
|SOS_WAIT_STATS|Exclusivamente para uso interno.|
|SOS_WAITABLE_ADDRESS_HASHBUCKET|Exclusivamente para uso interno.|
|SPIN_EVENT_MUTEX|Exclusivamente para uso interno.|
|SPL_DISPATCHER_LIST|Exclusivamente para uso interno.|
|SPL_DISPATCHER_QUEUE|Exclusivamente para uso interno.|
|SPL_NONYIELD_ANALYSIS|Exclusivamente para uso interno.|
|SPL_QUERY_STORE_CTX_INITIALIZED|Exclusivamente para uso interno.|
|SPL_QUERY_STORE_EXEC_STATS_AGG|Exclusivamente para uso interno.|
|SPL_QUERY_STORE_EXEC_STATS_READ|Exclusivamente para uso interno.|
|SPL_QUERY_STORE_STATS_COOKIE_CACHE|Exclusivamente para uso interno.|
|SPL_SOS_DISPATCHER|Exclusivamente para uso interno.|
|SPL_TDS_PKT_QUEUE|Exclusivamente para uso interno.|
|SPL_XE_BUFFER_MGR|Exclusivamente para uso interno.|
|SPL_XE_DISPATCHER_QUEUE|Exclusivamente para uso interno.|
|SPL_XE_NOTIFICATION_CALLBACK_LIST|Exclusivamente para uso interno.|
|SPL_XE_SESSION_EVENT_MGR|Exclusivamente para uso interno.|
|SPL_XE_SESSION_MGR|Exclusivamente para uso interno.|
|SPL_XE_SESSION_TARGET_MGR|Exclusivamente para uso interno.|
|SPT_PROFILE|Exclusivamente para uso interno.|
|SQL_MGR|Exclusivamente para uso interno.|
|SQL_NORM|Exclusivamente para uso interno.|
|SQLTRACE_FILE_BUFFER|Exclusivamente para uso interno.|
|SRVPROC|Exclusivamente para uso interno.|
|STACK_HASHER|Exclusivamente para uso interno.|
|Subbloqueo|Exclusivamente para uso interno.|
|SUBPDESC|Exclusivamente para uso interno.|
|SUBPDESC_LIST|Exclusivamente para uso interno.|
|SVC_BROKER_CTRL|Exclusivamente para uso interno.|
|SVC_BROKER_DEBUG_LIST|Exclusivamente para uso interno.|
|SVC_BROKER_LIST|Exclusivamente para uso interno.|
|SVC_BROKER_OBJECT|Exclusivamente para uso interno.|
|SYNCPOINT_RESOURCE|Exclusivamente para uso interno.|
|TaskElapsedExecutionMonitor|Exclusivamente para uso interno.|
|TDS_TVP|Exclusivamente para uso interno.|
|TESTTEAM|Exclusivamente para uso interno.|
|TESTTEAMEXPONENTIAL|Exclusivamente para uso interno.|
|TESTTEAMEXPONENTIALTASTAS|Exclusivamente para uso interno.|
|TESTTEAMTASTAS|Exclusivamente para uso interno.|
|TMP_SESS_KEY|Exclusivamente para uso interno.|
|TSQL_DEBUG|Exclusivamente para uso interno.|
|TXFRM_REPL|Exclusivamente para uso interno.|
|VDI_OPERATION|Exclusivamente para uso interno.|
|WINFAB_REPORT_FAULT|Exclusivamente para uso interno.|
|WRITE_PAGE_RECORDER|Exclusivamente para uso interno.|
|X_PACKET_LIST|Exclusivamente para uso interno.|
|X_PIPE|Exclusivamente para uso interno.|
|X_PIPE_DEMAND|Exclusivamente para uso interno.|
|X_PORT|Exclusivamente para uso interno.|
|XACT_LOCK_INFO|Exclusivamente para uso interno.|
|XACT_LOCKINFO_TASK|Exclusivamente para uso interno.|
|XACT_WORKSPACE|Exclusivamente para uso interno.|
|XCB|Exclusivamente para uso interno.|
|XCB_FREE_LIST|Exclusivamente para uso interno.|
|XCB_HASH|Exclusivamente para uso interno.|
|XCHNG_TRACE|Exclusivamente para uso interno.|
|XDES|Exclusivamente para uso interno.|
|XDES_HASH|Exclusivamente para uso interno.|
|XDESMGR|Exclusivamente para uso interno.|
|XDESTABLELIST|Exclusivamente para uso interno.|
|XE_RATE_LIMITER_STRETCHDB|Exclusivamente para uso interno.|
|XE_SESSION_STORAGE|Exclusivamente para uso interno.|
|XID_ARRAY|Exclusivamente para uso interno.|
|XIO_BLOCKLIST|Exclusivamente para uso interno.|
|XIO_REQSTR|Exclusivamente para uso interno.|
|XIO_SEQNUMBUMP|Exclusivamente para uso interno.|
|XIOSTATS|Exclusivamente para uso interno.|
|XTP_RT_DATA_LIST|Exclusivamente para uso interno.|
|XTS_MGR|Exclusivamente para uso interno.|
|XVB_CSN|Exclusivamente para uso interno.|
|XVB_LIST|Exclusivamente para uso interno.|
 

  
## <a name="see-also"></a>Consulte también  
 
 [DBCC SQLPERF &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-sqlperf-transact-sql.md)   
 
 [SQL Server vistas de administración dinámica relacionadas con el sistema operativo &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)  

 [¿Cuándo se Spinlock un controlador importante del uso de CPU en SQL Server?](https://techcommunity.microsoft.com/t5/SQL-Server-Support/When-is-Spinlock-a-Significant-Driver-of-CPU-utilization-in-SQL/ba-p/530142)

 [Diagnóstico y resolución de la contención de Spinlock en SQL Server](../diagnose-resolve-spinlock-contention.md)
  
  


