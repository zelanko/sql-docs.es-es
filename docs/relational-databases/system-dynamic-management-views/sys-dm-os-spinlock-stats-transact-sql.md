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
ms.openlocfilehash: 05e8698484f9445de7a5fb3265d1e0e294dc65d7
ms.sourcegitcommit: 2991ad5324601c8618739915aec9b184a8a49c74
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/11/2020
ms.locfileid: "97332074"
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
En SQL Database objetivos de servicio Basic, S0 y S1, y para las bases de datos de grupos elásticos, `Server admin` `Azure Active Directory admin` se requiere la cuenta o. En el resto de los objetivos del servicio SQL Database, `VIEW DATABASE STATE` se requiere el permiso en la base de datos.    
  
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
|ABR|Solo para uso interno.|
|ADB_CACHE|Solo para uso interno.|
|ALLOC_CACHES_HASH|Solo para uso interno.|
|APPENDONLY_STORAGE|Solo para uso interno.|
|APRC_BACK_OFF_STATS|Solo para uso interno.|
|APRC_EVENT_LIST|Solo para uso interno.|
|APRC_QUEUE_LIST|Solo para uso interno.|
|APRC_VALIDATION_QUEUE_LIST|Solo para uso interno.|
|ASYNC_OP_ADMIN_CLIENT_REGISTRATION_LIST|Solo para uso interno.|
|ASYNC_OP_ADMIN_WORK_REGISTRATION_HASH_TABLE|Solo para uso interno.|
|ASYNCSTATSLIST|Solo para uso interno.|
|BACKUP|Solo para uso interno.|
|BACKUP_COPY_CONTEXT|Solo para uso interno.|
|BACKUP_CTX|Solo para uso interno.|
|BASE_XACT_HASH|Solo para uso interno.|
|BLOCKER_ENUM|Solo para uso interno.|
|BPREPARTITION|Solo para uso interno.|
|BPWORKFILE|Solo para uso interno.|
|BUF_HASH|Solo para uso interno.|
|BUF_LINK|Solo para uso interno.|
|BUF_WRITE_LOG|Solo para uso interno.|
|CACHEOBJ_DBG|Solo para uso interno.|
|CHANNELFORCECLOSEMANAGER|Solo para uso interno.|
|CHECK_AGGREGATE_STATE|Solo para uso interno.|
|CLR_HOSTTASK|Solo para uso interno.|
|CLR_SPIN_LOCK|Solo para uso interno.|
|CMED_DATABASE|Solo para uso interno.|
|CMED_HASH_SET|Solo para uso interno.|
|COLUMNDATASETSESSIONLIST|Solo para uso interno.|
|COLUMNSTORE_HASHTABLE|Solo para uso interno.|
|COLUMNSTOREBUILDSTATE_LIST|Solo para uso interno.|
|COM_INIT|Solo para uso interno.|
|CONFIRMABLE|Solo para uso interno.|
|COMPPLAN_SKELETON|Solo para uso interno.|
|CONNECTION_MANAGER|Solo para uso interno.|
|CONEXIÓN|Solo para uso interno.|
|CSIBUILDMEM|Solo para uso interno.|
|CURSOR|Solo para uso interno.|
|CURSQL|Solo para uso interno.|
|DATAPORTCONSUMER|Solo para uso interno.|
|DATAPORTSOURCEINFOCREDIT|Solo para uso interno.|
|DATAPORTSOURCEINFOQUEUE|Solo para uso interno.|
|DATASET_FREELIST|Solo para uso interno.|
|DBCC_CHECK|Solo para uso interno.|
|DBSEEDING_OPERATION|Solo para uso interno.|
|DBT_HASH|Solo para uso interno.|
|DBT_IO_LIST|Solo para uso interno.|
|DBTABLE|Controla el acceso a una estructura de datos en memoria para cada base de datos de una SQL Server que contiene las propiedades de esa base de datos. Consulte [este artículo](https://techcommunity.microsoft.com/t5/SQL-Server/Improving-Concurrency-Scalability-of-SQL-Server-workload-by/ba-p/384789) para más información. |
|DEFERRED_WF_EXT_DROP|Solo para uso interno.|
|DEK_INSTANCE|Solo para uso interno.|
|DELAYED_PARTITIONED_STACK|Solo para uso interno.|
|DELETEBITMAP|Solo para uso interno.|
|DIAG_MANAGER|Solo para uso interno.|
|DIAG_OBJECT|Solo para uso interno.|
|DIGEST_CACHE|Solo para uso interno.|
|DINPBUF|Solo para uso interno.|
|DIRECTLOGCONSUMER|Solo para uso interno.|
|DP_LIST|Controla el acceso a la lista de páginas desfasadas para una base de datos que tiene activado el punto de comprobación indirecto. Consulte [este artículo](https://techcommunity.microsoft.com/t5/SQL-Server/Indirect-Checkpoint-and-tempdb-8211-the-good-the-bad-and-the-non/ba-p/385510) para más información.|
|DROP|Solo para uso interno.|
|DROP_TEMPO|Solo para uso interno.|
|DROPPED_ALLOC_UNIT|Solo para uso interno.|
|DTC_HASHTABLE|Solo para uso interno.|
|DTT_LIST|Solo para uso interno.|
|ENDD_LIST|Solo para uso interno.|
|EXT_CACHE|Solo para uso interno.|
|EXTENT_ACTIVATION|Solo para uso interno.|
|FABRIC_DB_MGR_PTR|Solo para uso interno.|
|FABRIC_LOG_MANAGEMENT_INPUT_VALUE|Solo para uso interno.|
|FABRIC_REPLICA_TRANSPORT|Solo para uso interno.|
|FABRIC_TVF_DATA_CONSUMER_LIST|Solo para uso interno.|
|FABRIC_TVF_LOAD_LIB|Solo para uso interno.|
|FCB_REPLICA_SYNC|Solo para uso interno.|
|FGCB_PRP_FILL|Solo para uso interno.|
|FILE_HANDLE_CACHE|Solo para uso interno.|
|FILE_TABLE|Solo para uso interno.|
|FILESTREAM_CHUNKER|Solo para uso interno.|
|FREE_SPACE_CACHE_ENTRY|Solo para uso interno.|
|FS_CONTAINER_LIST_WITH_DELETE|Solo para uso interno.|
|FS_DELETED_FOLDER_CLEANUP|Solo para uso interno.|
|FSAGENT|Solo para uso interno.|
|FSGHOST_STATUS|Solo para uso interno.|
|FT_INIT|Solo para uso interno.|
|GHOST_FREE|Solo para uso interno.|
|GHOST_HASH|Solo para uso interno.|
|GLOBAL_SCHEDULER_LIST|Solo para uso interno.|
|GLOBAL_TRACE_FLAGS|Solo para uso interno.|
|GLOBALTRANS|Solo para uso interno.|
|GROUP_COMMIT_FEEDBACK_LOOP|Solo para uso interno.|
|GUARDIAN|Solo para uso interno.|
|HADR_AGH_X_ACCESS|Solo para uso interno.|
|HADR_AR_CONTROLLER_COLLECTION|Solo para uso interno.|
|HADR_AR_DB_MGR|Solo para uso interno.|
|HADR_AR_TRANSPORT|Solo para uso interno.|
|HADR_COMPRESSION_MGR_POOL|Solo para uso interno.|
|HADR_FABRIC_FACTORY|Solo para uso interno.|
|HADR_PRIORITY_QUEUE|Solo para uso interno.|
|HADR_TRANSPORT_CONTROL|Solo para uso interno.|
|HADR_TRANSPORT_LIST|Solo para uso interno.|
|HADRSEEDINGLIST|Solo para uso interno.|
|HOBT_DROPPED|Solo para uso interno.|
|HOBT_HASH|Solo para uso interno.|
|HTTP|Solo para uso interno.|
|HTTP_CONNCACHE|Solo para uso interno.|
|HTTP_ENDPOINT|Solo para uso interno.|
|IDENTITY|Solo para uso interno.|
|INDEX_CREATE|Solo para uso interno.|
|IO_DISPENSER_PAUSE|Solo para uso interno.|
|IO_RG_VOLUME_HASHTABLE|Solo para uso interno.|
|IOREQ|Solo para uso interno.|
|ISSRESOURCE|Solo para uso interno.|
|KTM_ENLISTMENT|Solo para uso interno.|
|LANG_RES_LOAD|Solo para uso interno.|
|LIVE_TARGET_TVF|Solo para uso interno.|
|LOCK_FREE_LIST|Solo para uso interno.|
|LOCK_HASH|Protege el acceso a la tabla hash del administrador de bloqueos que almacena información acerca de los bloqueos que se mantienen en una base de datos. Consulte [este artículo](https://support.microsoft.com/kb/2926217) para más información.|
|LOCK_NOTIFICATION|Solo para uso interno.|
|LOCK_RESOURCE_ID|Solo para uso interno.|
|LOCK_RW_ABTX_HASH_SET|Solo para uso interno.|
|LOCK_RW_AGDB_HEALTH_DIAG|Solo para uso interno.|
|LOCK_RW_CMED_HASH_SET|Solo para uso interno.|
|LOCK_RW_DPT_TABLE|Solo para uso interno.|
|LOCK_RW_IN_ROW_TRACKER|Solo para uso interno.|
|LOCK_RW_LOGIN_RATE_STATS|Solo para uso interno.|
|LOCK_RW_PVS_PAGE_TRACKER|Solo para uso interno.|
|LOCK_RW_RBIO_REQ|Solo para uso interno.|
|LOCK_RW_SECURITY_CACHE|Solo para uso interno.|
|LOCK_RW_TEST|Solo para uso interno.|
|LOCK_RW_WPR_BUCKET|Solo para uso interno.|
|LOCK_SORT_STREAM|Solo para uso interno.|
|LOCK_SQLSATELLITE_MESSAGE|Solo para uso interno.|
|LOG_CONSOLIDATION|Solo para uso interno.|
|LOG_RG_GOVERNOR|Solo para uso interno.|
|LOGCACHE_ACCESS|Solo para uso interno.|
|LOGFLUSHQ|Solo para uso interno.|
|LOGIOSEQ|Solo para uso interno.|
|LOGIOSEQMAPPENDINGMESSAGEQUEUE|Solo para uso interno.|
|LOGLC|Solo para uso interno.|
|LOGLFM|Solo para uso interno.|
|LOGON_TRIGGER_CACHE|Solo para uso interno.|
|LOGPOOL_HASHBUCKET|Solo para uso interno.|
|LOGPOOL_REFCOUNTEDOBJECT|Solo para uso interno.|
|LOGPOOL_SHAREDCACHEBUFFER|Solo para uso interno.|
|LOGPOOL_SIZEPERRESOURCEPOOL|Solo para uso interno.|
|LPE_BATCH|Solo para uso interno.|
|LPE_SESSION|Solo para uso interno.|
|LPE_SXTP|Solo para uso interno.|
|LSID|Solo para uso interno.|
|LSLIST|Solo para uso interno.|
|LSNREFLIST|Solo para uso interno.|
|LSS_SYNC_DTC|Solo para uso interno.|
|MD_CHANGE_NOTIFICATION|Solo para uso interno.|
|MDB_REMOTE_BATCH_STATS_HASH_TABLE|Solo para uso interno.|
|MDB_REMOTE_SESSION_HASH_TABLE|Solo para uso interno.|
|MEM_MGR|Solo para uso interno.|
|MGR_CACHE|Solo para uso interno.|
|MIGRATION_BUF_LIST|Solo para uso interno.|
|NETCONN_ADDRESS|Solo para uso interno.|
|ONDEMAND_TASK|Solo para uso interno.|
|ONE_PROC_SIM_NODE_CONTEXT|Solo para uso interno.|
|ONE_PROC_SIM_NODE_CONTEXT_LIST|Solo para uso interno.|
|ONE_PROC_SIM_REPLICA_CONTEXT|Solo para uso interno.|
|ONE_PROC_SIM_SERVICE_PARTITION|Solo para uso interno.|
|OPT_IDX_MISS_ID|Solo para uso interno.|
|OPT_IDX_MISS_KEY|Solo para uso interno.|
|OPT_IDX_STATS|Solo para uso interno.|
|OPT_INFO_MGR|Solo para uso interno.|
|PAGE_WORKITEMLIST|Solo para uso interno.|
|PAGECOPIER|Solo para uso interno.|
|PARALLELREDOCACHE|Solo para uso interno.|
|PARTITIONED_HEAP_FREE_LIST|Solo para uso interno.|
|PROGRESS_REPORT|Solo para uso interno.|
|QE_SHUTDOWN|Solo para uso interno.|
|QSCAN_CACHE|Solo para uso interno.|
|QUERY_EXEC_STATS|Solo para uso interno.|
|QUERY_STORE_ASYNC_PERSIST|Solo para uso interno.|
|QUERY_STORE_ASYNC_QUEUE_TLIST|Solo para uso interno.|
|QUERY_STORE_CAPTURE_POLICY_INTERVAL|Solo para uso interno.|
|QUERY_STORE_CAPTURE_POLICY_STATS|Solo para uso interno.|
|QUERY_STORE_CAPTURE_POLICY_THRESHOLD|Solo para uso interno.|
|QUERY_STORE_CURRENT_INTERVAL|Solo para uso interno.|
|QUERY_STORE_HT_CACHE|Solo para uso interno.|
|QUERY_STORE_LIST|Solo para uso interno.|
|QUERY_STORE_PLAN_COMP_AGG|Solo para uso interno.|
|QUERY_STORE_PLAN_LIST|Solo para uso interno.|
|QUERY_STORE_READ_ONLY_FLAGS|Solo para uso interno.|
|QUERY_STORE_SELF_AGG|Solo para uso interno.|
|QUERY_STORE_STMT_COMP_AGG|Solo para uso interno.|
|QUERYEXEC|Solo para uso interno.|
|QUERYSCAN|Solo para uso interno.|
|RANGE_GENERATION|Solo para uso interno.|
|READ_AHEAD|Solo para uso interno.|
|REDOMGRSTATE|Solo para uso interno.|
|REMOTE_SESSION_CACHE|Solo para uso interno.|
|REMOTEBLOCKIO|Solo para uso interno.|
|REMOTEOP|Solo para uso interno.|
|REPL_LOGREADER_HISTORY_CACHE|Solo para uso interno.|
|REPL_LOGREADER_PERDB_HISTORY_CACHE|Solo para uso interno.|
|RESMANAGER|Solo para uso interno.|
|RECURSO|Solo para uso interno.|
|RESQUEUE|Solo para uso interno.|
|RFS_THREAD_QUEUE|Solo para uso interno.|
|RG_TIMER|Solo para uso interno.|
|ROWGROUP_VERSIONS|Solo para uso interno.|
|RPCCHANNELPOOL|Solo para uso interno.|
|RPCPACKAGE|Solo para uso interno.|
|RPCREQUESTORCONTEXT|Solo para uso interno.|
|RWLOCK_LAST|Solo para uso interno.|
|SATELLITE_CONNECTION|Solo para uso interno.|
|SBS_CLIENT_ENDPOINTS|Solo para uso interno.|
|SBS_CLIENT_REQUESTS|Solo para uso interno.|
|SBS_DISPATCH|Solo para uso interno.|
|SBS_PENDING|Solo para uso interno.|
|SBS_SERVER_XACT_TASK_PROXY|Solo para uso interno.|
|SBS_TRANSPORT|Solo para uso interno.|
|SBS_UCS_DISPATCH|Solo para uso interno.|
|SEGURIDAD|Solo para uso interno.|
|SECURITY_CACHE|Solo para uso interno.|
|SECURITY_FEDAUTH_AAD_BECWSCONNS|Solo para uso interno.|
|SEMANTIC_TICACHE|Solo para uso interno.|
|SEQUENCED_OBJECT|Solo para uso interno.|
|SEQUEUE_SIZED_THREADSAFE|Solo para uso interno.|
|SESSION_KILLER|Solo para uso interno.|
|SESSION_MANAGER|Solo para uso interno.|
|SESSION_SEC_CONTEXT|Solo para uso interno.|
|SETRANGE_SYNC|Solo para uso interno.|
|SHARABLE_SESSION_OBJECTS|Solo para uso interno.|
|SLO_INFO_LIST|Solo para uso interno.|
|SNI|Solo para uso interno.|
|SNI_NODE_PENDING_IO_QUEUE|Solo para uso interno.|
|SOAPSESSIONS|Solo para uso interno.|
|SOS_ABORT_TASK|Solo para uso interno.|
|SOS_ACTIVEDESCRIPTOR|Solo para uso interno.|
|SOS_BLOCKALLOCPARTIALLIST|Solo para uso interno.|
|SOS_BLOCKDESCRIPTORBUCKET|Solo para uso interno.|
|SOS_CACHESTORE|Sincroniza el acceso a varias cachés en memoria en SQL Server como la caché del plan o la memoria caché de la tabla temporal. La contención intensiva en este tipo de Spinlock puede significar muchos aspectos diferentes en función de la memoria caché específica que se encuentra en la contención. Póngase en contacto con los [!INCLUDE[msCoName](../../includes/msconame-md.md)] servicios de soporte al cliente para obtener ayuda para solucionar este tipo de Spinlock. |
|SOS_CACHESTORE_CLOCK|Solo para uso interno.|
|SOS_CLOCKALG_INTERNODE_SYNC|Solo para uso interno.|
|SOS_DEBUG_HOOK|Solo para uso interno.|
|SOS_DESCDATABUFFERLIST|Solo para uso interno.|
|SOS_LARGEPAGE_ALLOCATOR|Solo para uso interno.|
|SOS_MINITHREAD|Solo para uso interno.|
|SOS_NODE|Solo para uso interno.|
|SOS_OBJECT_POOL|Solo para uso interno.|
|SOS_OBJECT_STORE|Solo para uso interno.|
|SOS_OOM_CHECK|Solo para uso interno.|
|SOS_PHYS_PAGE_CACHE|Solo para uso interno.|
|SOS_RESOURCE_CLERK_LIST|Solo para uso interno.|
|SOS_RINGBUFFER_RECORD|Solo para uso interno.|
|SOS_RW|Solo para uso interno.|
|SOS_SATELLITE_USER_POOL|Solo para uso interno.|
|SOS_SCHEDULER|Solo para uso interno.|
|SOS_SELIST_SIZED_SLOCK|Solo para uso interno.|
|SOS_SUSPEND_QUEUE|Solo para uso interno.|
|SOS_SYSTHREAD|Solo para uso interno.|
|SOS_SYSTHREAD_DISPATCHER|Solo para uso interno.|
|SOS_TASK|Solo para uso interno.|
|SOS_TLIST|Solo para uso interno.|
|SOS_VM_LOW|Solo para uso interno.|
|SOS_WAIT_STATS|Solo para uso interno.|
|SOS_WAITABLE_ADDRESS_HASHBUCKET|Solo para uso interno.|
|SPIN_EVENT_MUTEX|Solo para uso interno.|
|SPL_DISPATCHER_LIST|Solo para uso interno.|
|SPL_DISPATCHER_QUEUE|Solo para uso interno.|
|SPL_NONYIELD_ANALYSIS|Solo para uso interno.|
|SPL_QUERY_STORE_CTX_INITIALIZED|Solo para uso interno.|
|SPL_QUERY_STORE_EXEC_STATS_AGG|Solo para uso interno.|
|SPL_QUERY_STORE_EXEC_STATS_READ|Solo para uso interno.|
|SPL_QUERY_STORE_STATS_COOKIE_CACHE|Solo para uso interno.|
|SPL_SOS_DISPATCHER|Solo para uso interno.|
|SPL_TDS_PKT_QUEUE|Solo para uso interno.|
|SPL_XE_BUFFER_MGR|Solo para uso interno.|
|SPL_XE_DISPATCHER_QUEUE|Solo para uso interno.|
|SPL_XE_NOTIFICATION_CALLBACK_LIST|Solo para uso interno.|
|SPL_XE_SESSION_EVENT_MGR|Solo para uso interno.|
|SPL_XE_SESSION_MGR|Solo para uso interno.|
|SPL_XE_SESSION_TARGET_MGR|Solo para uso interno.|
|SPT_PROFILE|Solo para uso interno.|
|SQL_MGR|Solo para uso interno.|
|SQL_NORM|Solo para uso interno.|
|SQLTRACE_FILE_BUFFER|Solo para uso interno.|
|SRVPROC|Solo para uso interno.|
|STACK_HASHER|Solo para uso interno.|
|Subbloqueo|Solo para uso interno.|
|SUBPDESC|Solo para uso interno.|
|SUBPDESC_LIST|Solo para uso interno.|
|SVC_BROKER_CTRL|Solo para uso interno.|
|SVC_BROKER_DEBUG_LIST|Solo para uso interno.|
|SVC_BROKER_LIST|Solo para uso interno.|
|SVC_BROKER_OBJECT|Solo para uso interno.|
|SYNCPOINT_RESOURCE|Solo para uso interno.|
|TaskElapsedExecutionMonitor|Solo para uso interno.|
|TDS_TVP|Solo para uso interno.|
|TESTTEAM|Solo para uso interno.|
|TESTTEAMEXPONENTIAL|Solo para uso interno.|
|TESTTEAMEXPONENTIALTASTAS|Solo para uso interno.|
|TESTTEAMTASTAS|Solo para uso interno.|
|TMP_SESS_KEY|Solo para uso interno.|
|TSQL_DEBUG|Solo para uso interno.|
|TXFRM_REPL|Solo para uso interno.|
|VDI_OPERATION|Solo para uso interno.|
|WINFAB_REPORT_FAULT|Solo para uso interno.|
|WRITE_PAGE_RECORDER|Solo para uso interno.|
|X_PACKET_LIST|Solo para uso interno.|
|X_PIPE|Solo para uso interno.|
|X_PIPE_DEMAND|Solo para uso interno.|
|X_PORT|Solo para uso interno.|
|XACT_LOCK_INFO|Solo para uso interno.|
|XACT_LOCKINFO_TASK|Solo para uso interno.|
|XACT_WORKSPACE|Solo para uso interno.|
|XCB|Solo para uso interno.|
|XCB_FREE_LIST|Solo para uso interno.|
|XCB_HASH|Solo para uso interno.|
|XCHNG_TRACE|Solo para uso interno.|
|XDES|Solo para uso interno.|
|XDES_HASH|Solo para uso interno.|
|XDESMGR|Solo para uso interno.|
|XDESTABLELIST|Solo para uso interno.|
|XE_RATE_LIMITER_STRETCHDB|Solo para uso interno.|
|XE_SESSION_STORAGE|Solo para uso interno.|
|XID_ARRAY|Solo para uso interno.|
|XIO_BLOCKLIST|Solo para uso interno.|
|XIO_REQSTR|Solo para uso interno.|
|XIO_SEQNUMBUMP|Solo para uso interno.|
|XIOSTATS|Solo para uso interno.|
|XTP_RT_DATA_LIST|Solo para uso interno.|
|XTS_MGR|Solo para uso interno.|
|XVB_CSN|Solo para uso interno.|
|XVB_LIST|Solo para uso interno.|
 

  
## <a name="see-also"></a>Consulte también  
 
 [DBCC SQLPERF &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-sqlperf-transact-sql.md)   
 
 [SQL Server vistas de administración dinámica relacionadas con el sistema operativo &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)  

 [¿Cuándo se Spinlock un controlador importante del uso de CPU en SQL Server?](https://techcommunity.microsoft.com/t5/SQL-Server-Support/When-is-Spinlock-a-Significant-Driver-of-CPU-utilization-in-SQL/ba-p/530142)

 [Diagnóstico y resolución de la contención de Spinlock en SQL Server](../diagnose-resolve-spinlock-contention.md)
  
  


