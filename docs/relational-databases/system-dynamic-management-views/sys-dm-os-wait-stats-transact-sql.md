---
title: Sys.dm_os_wait_stats (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 04/23/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- dm_os_wait_stats_TSQL
- dm_os_wait_stats
- sys.dm_os_wait_stats
- sys.dm_os_wait_stats_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_wait_stats dynamic management view
ms.assetid: 568d89ed-2c96-4795-8a0c-2f3e375081da
caps.latest.revision: 111
author: MashaMSFT
ms.author: mathoma
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: e2ae34c5ffd67712e925d8dda26dbc79680e3520
ms.sourcegitcommit: 7019ac41524bdf783ea2c129c17b54581951b515
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/23/2018
---
# <a name="sysdmoswaitstats-transact-sql"></a>sys.dm_os_wait_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Devuelve información acerca de todas las esperas encontradas por los subprocesos ejecutados. Puede utilizar esta vista agregada para diagnosticar problemas de rendimiento con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y también con lotes y consultas específicos. [Sys.dm_exec_session_wait_stats &#40;Transact-SQL&#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-exec-session-wait-stats-transact-sql.md) proporciona información similar por sesión.  
  
> [!NOTE] 
> Para llamar a esta desde **[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] o [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]**, use el nombre **sys.dm_pdw_nodes_os_wait_stats**.  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|wait_type|**nvarchar(60)**|Nombre del tipo de espera. Para obtener más información, consulte [tipos de esperas](#WaitTypes), más adelante en este tema.|  
|waiting_tasks_count|**bigint**|Número de esperas de este tipo de espera. Este recuento se incrementa al inicio de cada espera.|  
|wait_time_ms|**bigint**|Tiempo total de espera de este tipo en milisegundos. Este tiempo incluye el tiempo de signal_wait_time_ms.|  
|max_wait_time_ms|**bigint**|Tiempo de espera máximo de este tipo de espera.|  
|signal_wait_time_ms|**bigint**|Diferencia entre el momento en que se indicó el subproceso en espera y el momento en que empezó a ejecutarse.|  
|pdw_node_id|**int**|El identificador para el nodo que se encuentra en esta distribución. <br/> **Se aplica a**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] |  
  
## <a name="permissions"></a>Permissions

En [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], requiere `VIEW SERVER STATE` permiso.   
En [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)], requiere el `VIEW DATABASE STATE` permiso en la base de datos.   

##  <a name="WaitTypes"></a> Tipos de esperas  
 **Las esperas de recursos** las esperas de recursos tienen lugar cuando un trabajador solicita acceso a un recurso que no está disponible porque el recurso está usando otro trabajador o aún no está disponible. Algunos ejemplos de esperas de recursos son los bloqueos, bloqueos temporales y esperas de red y E/S de disco. Las esperas de bloqueos y bloqueos temporales son esperas en objetos de sincronización.  
  
**Esperas de colas**  
 Las esperas de colas tienen lugar cuando un trabajador está inactivo, esperando que se le asigne un trabajo. Las esperas de colas se ven normalmente con tareas en segundo plano del sistema como las tareas de supervisión de interbloqueos y de limpieza de registros eliminados. Estas tareas esperarán a que las solicitudes de trabajo se pongan en una cola de trabajo. Las esperas de colas también pueden activarse periódicamente incluso si no se han puesto en cola paquetes nuevos.  
  
 **Esperas externas**  
 Las esperas externas tienen lugar cuando un trabajador de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] espera que se termine un evento externo, como una llamada a un procedimiento almacenado extendido o una consulta de servidor vinculado. Cuando diagnostique problemas de bloqueo, recuerde que las esperas externas no siempre implican que el trabajador esté inactivo, porque se puede ejecutar activamente algún código externo.  
  
 `sys.dm_os_wait_stats` muestra el tiempo para las esperas que se han completado. En esta vista de administración dinámica no se muestran las esperas actuales.  
  
 Un subproceso de trabajo de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no se considera en espera si alguna de las siguientes situaciones es verdadera:  
  
-   Un recurso pasa a estar disponible.  
  
-   Una cola no está vacía.  
  
-   Un proceso externo finaliza.  
  
 Aunque el subproceso ya no esté en espera, no tiene que empezar a ejecutarse inmediatamente. Esto se debe a que un subproceso primero se pone en la cola de trabajadores ejecutables y debe esperar a que se ejecute un cuanto en el programador.  
  
 En [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] los contadores de tiempo de espera son **bigint** valores y por lo tanto, no son tan propensos a completar el ciclo como los contadores equivalentes en versiones anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Determinados tipos de tiempos de espera durante la ejecución de consultas pueden indicar cuellos de botella o puntos de pausa en la consulta. De forma similar, tiempos de espera altos, o contadores de espera en todo el servidor pueden indicar cuellos de botella o puntos de actividad en interacciones de consultas de interacción en la instancia del servidor. Por ejemplo, las esperas de bloqueos indican la contención de datos por las consultas; las esperas de bloqueos temporales de E/S de páginas indican tiempos de respuesta de E/S bajos; las esperas de actualizaciones de bloqueos temporales de páginas indican un diseño de archivo incorrecto.  
  
 El contenido de esta vista de administración dinámica se puede restablecer ejecutando el siguiente comando:  
  
```sql  
DBCC SQLPERF ('sys.dm_os_wait_stats', CLEAR);  
GO  
```  
  
Este comando restablece todos los contadores en 0.  
  
> [!NOTE]
> Estas estadísticas no permanecen cuando se reinicia [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y todos los datos se acumulan desde la última vez que se restablecieron las estadísticas o se inició el servidor.  
  
 En la tabla siguiente se muestran los tipos de espera encontrados por las tareas.  

|Tipo |Description| 
|-------------------------- |--------------------------| 
|ABR |Solamente se identifica con fines informativos. No compatible. La compatibilidad con versiones posteriores no está garantizada.| | 
|AM_INDBUILD_ALLOCATION |TBD <br />**Se aplica a**: desde [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|AM_SCHEMAMGR_UNSHARED_CACHE |TBD <br />**Se aplica a**: desde [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|ASSEMBLY_FILTER_HASHTABLE |TBD <br />**Se aplica a**: desde [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|ASSEMBLY_LOAD |Tiene lugar durante el acceso exclusivo a la carga de ensamblados.| 
|ASYNC_DISKPOOL_LOCK |Tiene lugar cuando existe un intento de sincronizar subprocesos paralelos que ejecutan tareas como la creación o la inicialización de un archivo.| 
|ASYNC_IO_COMPLETION |Tiene lugar cuando una tarea está esperando que finalice una operación de E/S.| 
|ASYNC_NETWORK_IO |Tiene lugar en escrituras en la red cuando la tarea se bloquea tras la red. Comprueba que el cliente procesa datos en el servidor.| 
|ASYNC_OP_COMPLETION |TBD <br />**Se aplica a**: desde [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|ASYNC_OP_CONTEXT_READ |TBD <br />**Se aplica a**: desde [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|ASYNC_OP_CONTEXT_WRITE |TBD <br />**Se aplica a**: desde [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|ASYNC_SOCKETDUP_IO |TBD <br />**Se aplica a**: desde [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|AUDIT_GROUPCACHE_LOCK |Tiene lugar cuando se produce una espera en un bloqueo que controla el acceso a una caché especial. La memoria caché contiene información acerca de las auditorías que se usan para auditar cada grupo de acciones de auditoría.| 
|AUDIT_LOGINCACHE_LOCK |Tiene lugar cuando se produce una espera en un bloqueo que controla el acceso a una caché especial. La memoria caché contiene información acerca de las auditorías que se usan para auditar los grupo de acciones de auditoría de inicio de sesión.| 
|AUDIT_ON_DEMAND_TARGET_LOCK |Tiene lugar cuando se produce una espera en un bloqueo que se usa para asegurar la inicialización única de destinos de Extended Events relacionados con las auditorías.| 
|AUDIT_XE_SESSION_MGR |Tiene lugar cuando se produce una espera en un bloqueo que se usa para sincronizar el inicio y la detención de sesiones de Extended Events relacionados con las auditorías.| 
|BACKUP |Tiene lugar cuando una tarea se bloquea como parte de un proceso de copia de seguridad.| 
|BACKUP_OPERATOR |Tiene lugar cuando una tarea está esperando a que se monte una cinta. Para ver el estado de la cinta, consulte sys.dm_io_backup_tapes. Si no hay pendiente ninguna operación de montaje, este tiempo de espera puede indicar un problema de hardware con la unidad de cinta.| 
|BACKUPBUFFER |Tiene lugar cuando una tarea de copia de seguridad espera por datos, o espera a un búfer donde se almacenarán datos. Este tipo no es normal, excepto cuando una tarea está esperando a que se monte una cinta.| 
|BACKUPIO |Tiene lugar cuando una tarea de copia de seguridad espera por datos, o espera a un búfer donde se almacenarán datos. Este tipo no es normal, excepto cuando una tarea está esperando a que se monte una cinta.| 
|BACKUPTHREAD |Tiene lugar cuando una tarea está esperando que finalice una tarea de copia de seguridad. Los tiempos de espera pueden ser largos, desde unos minutos a varias horas. Si la tarea que se está esperando está en un proceso de E/S, este tipo no indica ningún problema.| 
|BAD_PAGE_PROCESS |Tiene lugar cuando el registrador de páginas sospechosas en segundo plano intenta impedir la ejecución más veces que cada cinco segundos. Un exceso de páginas sospechosas provoca la ejecución frecuente del registrador.| 
|BLOB_METADATA |TBD <br />**Se aplica a**: desde [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|BMPALLOCATION |TBD <br />**Se aplica a**: desde [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|BMPBUILD |TBD <br />**Se aplica a**: desde [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|BMPREPARTITION |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|BMPREPLICATION |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|BPSORT |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|BROKER_CONNECTION_RECEIVE_TASK |Tiene lugar cuando se espera el acceso para recibir un mensaje en el extremo de una conexión. El acceso de recepción al extremo está serializado.| 
|BROKER_DISPATCHER |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|BROKER_ENDPOINT_STATE_MUTEX |Se produce cuando hay contención de acceso al estado de un extremo de conexión de Service Broker. El acceso al estado de los cambios está serializado.| 
|BROKER_EVENTHANDLER |Se produce cuando una tarea está esperando en el controlador de eventos principal de Service Broker. Debería ocurrir brevemente.| 
|BROKER_FORWARDER |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|BROKER_INIT |Se produce al inicializar a Service Broker en cada base de datos activa. No debería ocurrir con frecuencia.| 
|BROKER_MASTERSTART |Se produce cuando una tarea está esperando que el controlador de eventos principal de Service Broker para iniciar. Debería ocurrir brevemente.| 
|BROKER_RECEIVE_WAITFOR |Tiene lugar cuando RECEIVE WAITFOR está en espera. Esto puede significar que ningún mensaje esté preparado para recibirse en la cola o una contención de bloqueo impide recibir los mensajes de la cola.| 
|BROKER_REGISTERALLENDPOINTS |Se produce durante la inicialización de un extremo de conexión de Service Broker. Debería ocurrir brevemente.| 
|BROKER_SERVICE |Se produce cuando la lista de destino de Service Broker que está asociada a un servicio de destino se actualiza o vuelve a un nivel de prioridad.| 
|BROKER_SHUTDOWN |Se produce cuando hay un apagado planeado de Service Broker. Debería ocurrir brevemente, si ocurre.| 
|BROKER_START |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|BROKER_TASK_SHUTDOWN |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|BROKER_TASK_STOP |Se produce cuando el controlador de tareas de cola de Service Broker intenta cerrar la tarea. La comprobación de estado se serializa y debe estar en estado de ejecución de antemano.| 
|BROKER_TASK_SUBMIT |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|BROKER_TO_FLUSH |Se produce cuando la transmisión vaciador diferida vaciados de la memoria en Service Broker objetos a una tabla de trabajo.| 
|BROKER_TRANSMISSION_OBJECT |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|BROKER_TRANSMISSION_TABLE |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|BROKER_TRANSMISSION_WORK |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|BROKER_TRANSMITTER |Se produce cuando el transmisor de Service Broker está esperando trabajo.| 
|BUILTIN_HASHKEY_MUTEX |Puede producirse después del inicio de una instancia, mientras se inicializan las estructuras de datos internas. No se producirá después de la inicialización de las estructuras de datos.| 
|CHANGE_TRACKING_WAITFORCHANGES |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|CHECK_PRINT_RECORD |Solamente se identifica con fines informativos. No compatible. La compatibilidad con versiones posteriores no está garantizada.| 
|CHECK_SCANNER_MUTEX |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|CHECK_TABLES_INITIALIZATION |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|CHECK_TABLES_SINGLE_SCAN |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|CHECK_TABLES_THREAD_BARRIER |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|CHECKPOINT_QUEUE |Tiene lugar mientras la tarea del punto de comprobación está esperando la siguiente solicitud de punto de comprobación.| 
|CHKPT |Tiene lugar en el inicio del servidor para indicar al subproceso de punto de comprobación que puede iniciarse.| 
|CLEAR_DB |Tiene lugar durante las operaciones que cambian el estado de una base de datos, como la apertura o el cierre de una base de datos.| 
|CLR_AUTO_EVENT |Tiene lugar cuando una tarea está realizando actualmente la ejecución de Common Language Runtime (CLR) y espera que se inicie un evento automático determinado. Son habituales las esperas largas y no indican ningún problema.| 
|CLR_CRST |Tiene lugar cuando una tarea está realizando actualmente una ejecución CLR y espera entrar en una sección crítica de la tarea que utiliza actualmente otra tarea.| 
|CLR_JOIN |Tiene lugar cuando una tarea está realizando actualmente la ejecución de CLR y espera a que finalice otra tarea. Este estado de espera tiene lugar cuando existe una combinación entre tareas.| 
|CLR_MANUAL_EVENT |Tiene lugar cuando una tarea está realizando actualmente la ejecución de CLR y espera que se inicie un evento manual específico.| 
|CLR_MEMORY_SPY |Tiene lugar durante la espera de una adquisición de bloqueo para una estructura de datos que se usa para registrar todas las asignaciones de memoria virtual que proceden de CLR. La estructura de datos se bloquea para mantener su integridad si existe un acceso paralelo.| 
|CLR_MONITOR |Tiene lugar cuando una tarea está realizando actualmente la ejecución de CLR y espera para obtener un bloqueo en la supervisión.| 
|CLR_RWLOCK_READER |Tiene lugar cuando una tarea está realizando actualmente la ejecución de CLR y espera un bloqueo del lector.| 
|CLR_RWLOCK_WRITER |Tiene lugar cuando una tarea está realizando actualmente la ejecución de CLR y espera un bloqueo del escritor.| 
|CLR_SEMAPHORE |Tiene lugar cuando una tarea está realizando actualmente la ejecución de CLR y espera un semáforo.| 
|CLR_TASK_START |Tiene lugar mientras se espera que una tarea CLR complete el inicio.| 
|CLRHOST_STATE_ACCESS |Tiene lugar cuando se produce una espera para obtener acceso exclusivo a las estructuras de datos que hospedan el CLR. Este tipo de espera se produce al configurar o anular el motor en tiempo de ejecución de CRL.| 
|CMEMPARTITIONED |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|CMEMTHREAD |Tiene lugar cuando una tarea está esperando en un objeto de memoria seguro para subprocesos. El tiempo de espera puede aumentar cuando existe una contención porque muchas tareas intentan asignar memoria desde el mismo objeto de memoria.| 
|COLUMNSTORE_BUILD_THROTTLE |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|COLUMNSTORE_COLUMNDATASET_SESSION_LIST |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|COMMIT_TABLE |TBD| 
|CONNECTION_ENDPOINT_LOCK |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|COUNTRECOVERYMGR |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|CREATE_DATINISERVICE |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|CXCONSUMER |Tiene lugar con planes de consulta paralelos cuando un subproceso consumidor espera un subproceso productor enviar filas. Esto es una parte normal de ejecución en paralelo. <br /> **Se aplica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (a partir de [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP2, [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] CU3), [!INCLUDE[ssSDS](../../includes/sssds-md.md)]|
|CXPACKET |Se produce con planes de consulta paralelos al sincronizar el iterador de intercambios del procesador de consultas y cuando generar y consumir filas. Si la espera es excesiva y no se puede reducir ajustando la consulta (por ejemplo, agregando índices), considere la posibilidad de ajustar el umbral de costo para paralelismo o de reducir el grado de paralelismo.<br /> **Nota:** a partir de [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP2, [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] CU3, y [!INCLUDE[ssSDS](../../includes/sssds-md.md)], CXPACKET solo hace referencia que se va a sincronizar el iterador de intercambios del procesador de consultas, así como generar filas para los subprocesos de consumidor. Subprocesos de consumidor se realiza un seguimiento por separado en el tipo de espera CXCONSUMER.| 
|CXROWSET_SYNC |Tiene lugar durante un examen de intervalo en paralelo.| 
|DAC_INIT |Tiene lugar mientras se inicializa la conexión de administrador dedicada.| 
|DBCC_SCALE_OUT_EXPR_CACHE |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|DBMIRROR_DBM_EVENT |Solamente se identifica con fines informativos. No compatible. La compatibilidad con versiones posteriores no está garantizada.| 
|DBMIRROR_DBM_MUTEX |Solamente se identifica con fines informativos. No compatible. La compatibilidad con versiones posteriores no está garantizada.| 
|DBMIRROR_EVENTS_QUEUE |Tiene lugar cuando la creación de reflejo de bases de datos espera que se procesen eventos.| 
|DBMIRROR_SEND |Tiene lugar cuando una tarea está esperando un trabajo acumulado de comunicaciones en el nivel de red para limpiar y poder enviar mensajes. Indica que el nivel de comunicaciones empieza a sobrecargarse y afecta al rendimiento de la creación del reflejo de los datos de la base de datos.| 
|DBMIRROR_WORKER_QUEUE |Indica que la tarea de trabajo de creación de reflejo de bases de datos está esperando más trabajo.| 
|DBMIRRORING_CMD |Tiene lugar cuando una tarea está esperando que los registros se guarden en el disco. Este estado de espera está previsto que dure largos periodos de tiempo.| 
|DBSEEDING_FLOWCONTROL |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|DBSEEDING_OPERATION |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|DEADLOCK_ENUM_MUTEX |Se produce cuando la supervisión de interbloqueos y sys.dm_os_waiting_tasks intentan asegurarse de que SQL Server no se ejecuta varias búsquedas de interbloqueos al mismo tiempo.| 
|DEADLOCK_TASK_SEARCH |Un tiempo de espera largo en este recurso indica que el servidor está ejecutando consultas por encima de sys.dm_os_waiting_tasks y que estas consultas impiden que la supervisión de interbloqueos ejecute la búsqueda de interbloqueos. Este tipo de espera solo lo utiliza el supervisor de interbloqueos. Las consultas por encima de sys.dm_os_waiting_tasks utilizan DEADLOCK_ENUM_MUTEX.| 
|DEBUG |Se produce durante Transact-SQL y depuración de CLR para la sincronización interna.| 
|DIRECTLOGCONSUMER_LIST |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|DIRTY_PAGE_POLL |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|DIRTY_PAGE_SYNC |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|DIRTY_PAGE_TABLE_LOCK |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|DISABLE_VERSIONING |Se produce cuando SQL Server sondea al administrador de transacciones de versiones para comprobar si la marca de tiempo de la primera transacción activa es posterior a la marca de tiempo de cuando el estado empezó a cambiar. Si es así, todas las transacciones de instantáneas que se iniciaron antes de ejecutar la instrucción ALTER DATABASE han finalizado. Este estado de espera se utiliza cuando SQL Server deshabilita el control de versiones mediante la instrucción ALTER DATABASE.| 
|DISKIO_SUSPEND |Tiene lugar cuando una tarea está esperando tener acceso a un archivo cuando está activa una copia de seguridad externa. Se notifica para cada proceso de usuario en espera. Un recuento mayor de cinco procesos por usuario puede indicar que la copia de seguridad externa tarda mucho en finalizarse.| 
|DISPATCHER_PRIORITY_QUEUE_SEMAPHORE |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|DISPATCHER_QUEUE_SEMAPHORE |Tiene lugar cuando un subproceso del grupo de distribuidores espera más trabajo para su procesamiento. Se prevé que el tiempo de espera de este tipo de espera aumente cuando el distribuidor esté inactivo.| 
|DLL_LOADING_MUTEX |Tiene lugar una vez mientras se espera que se cargue la DLL del analizador XML.| 
|DPT_ENTRY_LOCK |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|DROP_DATABASE_TIMER_TASK |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|DROPTEMP |Tiene lugar entre intentos para quitar un objeto temporal si se produjo un error en el intento anterior. La duración de la espera crece de forma exponencial en cada intento de eliminación con error.| 
|DTC |Tiene lugar cuando una tarea está esperando en un evento que se utiliza para administrar la transición de estado. Controles de este estado cuando la recuperación de transacciones del Coordinador de transacciones distribuidas de Microsoft (MS DTC) se produce después de que SQL Server recibe notificación de que el servicio MS DTC no está disponible.| 
|DTC_ABORT_REQUEST |Tiene lugar en una sesión del trabajador de MS DTC cuando la sesión espera a tener la propiedad de una transacción de MS DTC. Después de que MS DTC es propietario de la transacción, la sesión puede revertir la transacción. Generalmente, la sesión esperará a otra sesión que esté utilizando la transacción.| 
|DTC_RESOLVE |Tiene lugar cuando una tarea de recepción espera a la base de datos maestra en una transacción entre bases de datos por lo que la tarea puede consultar el resultado de la transacción.| 
|DTC_STATE |Tiene lugar cuando una tarea está esperando en un evento que protege los cambios al objeto de estado global de MS DTC. Este estado debe mantenerse durante periodos muy cortos.| 
|DTC_TMDOWN_REQUEST |Se produce en una sesión del trabajador de MS DTC cuando SQL Server recibe notificación de que el servicio MS DTC no está disponible. Primero, el trabajador esperará a que se inicie el proceso de recepción de MS DTC. A continuación, el trabajador espera a obtener el resultado de la transacción distribuida en la que está trabajando. Esto puede continuar hasta que se restablezca la conexión con el servicio de MS DTC.| 
|DTC_WAITFOR_OUTCOME |Tiene lugar cuando las tareas de recepción esperan a que MS DTC se vuelva a activar para habilitar la resolución de las transacciones preparadas.| 
|DTCNEW_ENLIST |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|DTCNEW_PREPARE |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|DTCNEW_RECOVERY |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|DTCNEW_TM |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|DTCNEW_TRANSACTION_ENLISTMENT |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|DTCPNTSYNC |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|DUMP_LOG_COORDINATOR |Tiene lugar cuando una tarea principal espera que una subtarea genere datos. Normalmente, este estado no tiene lugar. Una espera larga indica un bloqueo inesperado. La subtarea debe investigarse.| 
|DUMP_LOG_COORDINATOR_QUEUE |TBD| 
|DUMPTRIGGER |Solamente se identifica con fines informativos. No compatible. La compatibilidad con versiones posteriores no está garantizada.| 
|EC |Solamente se identifica con fines informativos. No compatible. La compatibilidad con versiones posteriores no está garantizada.| 
|EE_PMOLOCK |Tiene lugar durante la sincronización de determinados tipos de asignaciones de memoria durante la ejecución de instrucciones.| 
|EE_SPECPROC_MAP_INIT |Tiene lugar durante la sincronización de la creación de una tabla hash de procedimiento interna. Esta espera solo se puede producir durante el acceso inicial de la tabla hash después de la instancia de SQL Server se inicia.| 
|ENABLE_EMPTY_VERSIONING |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|ENABLE_VERSIONING |Se produce cuando SQL Server espera a que todas las transacciones de actualización de esta base de datos finalice antes de declarar la base de datos preparada para pasar al estado permitido de aislamiento de instantánea. Este estado se utiliza cuando SQL Server habilita el aislamiento de instantánea mediante la instrucción ALTER DATABASE.| 
|ERROR_REPORTING_MANAGER |Tiene lugar durante la sincronización de múltiples inicializaciones simultáneas de registros de errores.| 
|EXCHANGE |Tiene lugar en la sincronización en el iterador de intercambios del procesador de consultas, durante consultas en paralelo.| 
|EXECSYNC |Tiene lugar durante consultas en paralelo mientras se sincroniza en el procesador de consultas en áreas no relacionadas con el iterador de intercambios. Algunos ejemplos de estas áreas son mapas de bits, objetos binarios grandes (LOB) y el iterador de spool. Los LOB pueden utilizar con frecuencia este estado de espera.| 
|EXECUTION_PIPE_EVENT_INTERNAL |Tiene lugar durante la sincronización entre las partes productor y consumidor de la ejecución por lotes que se envían a través del contexto de conexión.| 
|EXTERNAL_RG_UPDATE |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|EXTERNAL_SCRIPT_NETWORK_IO |TBD <br /> **Se aplica a**: [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] hasta la versión actual.| 
|EXTERNAL_SCRIPT_PREPARE_SERVICE |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|EXTERNAL_SCRIPT_SHUTDOWN |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|EXTERNAL_WAIT_ON_LAUNCHER, |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|FABRIC_HADR_TRANSPORT_CONNECTION |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|FABRIC_REPLICA_CONTROLLER_LIST |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|FABRIC_REPLICA_CONTROLLER_STATE_AND_CONFIG |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|FABRIC_REPLICA_PUBLISHER_EVENT_PUBLISH |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|FABRIC_REPLICA_PUBLISHER_SUBSCRIBER_LIST |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|FABRIC_WAIT_FOR_BUILD_REPLICA_EVENT_PROCESSING |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|FAILPOINT |Solamente se identifica con fines informativos. No compatible. La compatibilidad con versiones posteriores no está garantizada.| 
|FCB_REPLICA_READ |Tiene lugar cuando se sincronizan las lecturas de un archivo disperso de instantáneas (o una instantánea temporal creada por DBCC).| 
|FCB_REPLICA_WRITE |Tiene lugar cuando se sincroniza la inserción o extracción de una página en un archivo disperso de instantáneas (o en una instantánea temporal creada por DBCC).| 
|FEATURE_SWITCHES_UPDATE |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|FFT_NSO_DB_KILL_FLAG |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|FFT_NSO_DB_LIST |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|FFT_NSO_FCB |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|FFT_NSO_FCB_FIND |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|FFT_NSO_FCB_PARENT |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|FFT_NSO_FCB_RELEASE_CACHED_ENTRIES |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|FFT_NSO_FCB_STATE |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|FFT_NSO_FILEOBJECT |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|FFT_NSO_TABLE_LIST |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|FFT_NTFS_STORE |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|FFT_RECOVERY |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|FFT_RSFX_COMM |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|FFT_RSFX_WAIT_FOR_MEMORY |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|FFT_STARTUP_SHUTDOWN |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|FFT_STORE_DB |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|FFT_STORE_ROWSET_LIST |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|FFT_STORE_TABLE |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|FILE_VALIDATION_THREADS |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|FILESTREAM_CACHE |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|FILESTREAM_CHUNKER |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|FILESTREAM_CHUNKER_INIT |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|FILESTREAM_FCB |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|FILESTREAM_FILE_OBJECT |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|FILESTREAM_WORKITEM_QUEUE |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|FILETABLE_SHUTDOWN |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|FOREIGN_REDO |TBD <br /> **Se aplica a**: [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] hasta la versión actual.| 
|FORWARDER_TRANSITION |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|FS_FC_RWLOCK |Tiene lugar cuando se produce una espera en el recolector de elementos no utilizados FILESTREAM para realizar una de las acciones siguientes:| 
|FS_GARBAGE_COLLECTOR_SHUTDOWN |Tiene lugar cuando el recolector de elementos no utilizados FILESTREAM espera hasta que se completan las tareas de limpieza.| 
|FS_HEADER_RWLOCK |Tiene lugar cuando se produce una espera para adquirir acceso al encabezado FILESTREAM de un contenedor de datos FILESTREAM al contenido de lectura o de actualización en el archivo de encabezado de FILESTREAM (Filestream.hdr).| 
|FS_LOGTRUNC_RWLOCK |Tiene lugar cuando se produce una espera para adquirir acceso al truncamiento del registro de FILESTREAM para realizar una de las acciones siguientes:| 
|FSA_FORCE_OWN_XACT |Tiene lugar cuando una operación de E/S del archivo de FILESTREAM debe enlazarse con la transacción asociada pero ésta pertenece actualmente a otra sesión.| 
|FSAGENT |Tiene lugar cuando una operación de E/S del archivo de FILESTREAM espera un recurso del agente de FILESTREAM que está utilizando otra operación de E/S de archivo.| 
|FSTR_CONFIG_MUTEX |Tiene lugar cuando se produce una espera hasta que se complete la configuración de otra característica de FILESTREAM.| 
|FSTR_CONFIG_RWLOCK |Tiene lugar cuando se produce una espera para serializar el acceso a los parámetros de configuración de FILESTREAM.| 
|FT_COMPROWSET_RWLOCK |El texto completo espera en la operación de metadatos de fragmento. Solamente se documenta con fines informativos. No compatible. La compatibilidad con versiones posteriores no está garantizada.| 
|FT_IFTS_RWLOCK |El texto completo está esperando la sincronización interna. Solamente se documenta con fines informativos. No compatible. La compatibilidad con versiones posteriores no está garantizada.| 
|TDPFT_IFTS_SCHEDULER_IDLE_WAIT |Tipo de espera de la suspensión del programador de texto completo. El programador está inactivo.| 
|FT_IFTSHC_MUTEX |El texto completo está esperando una operación de control de fdhost. Solamente se documenta con fines informativos. No compatible. La compatibilidad con versiones posteriores no está garantizada.| 
|FT_IFTSISM_MUTEX |El texto completo está esperando la operación de comunicación. Solamente se documenta con fines informativos. No compatible. La compatibilidad con versiones posteriores no está garantizada.| 
|FT_MASTER_MERGE |El texto completo está esperando la operación de combinación maestra. Solamente se documenta con fines informativos. No compatible. La compatibilidad con versiones posteriores no está garantizada.| 
|FT_MASTER_MERGE_COORDINATOR |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|FT_METADATA_MUTEX |Solamente se documenta con fines informativos. No compatible. La compatibilidad con versiones posteriores no está garantizada.| 
|FT_PROPERTYLIST_CACHE |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|FT_RESTART_CRAWL |Tiene lugar cuando un rastreo de texto completo debe reiniciarse desde el último punto correcto conocido para recuperarse de un error transitorio. La espera permite que completen o abandonen el paso actual las tareas del trabajador que se están ejecutando en dicho rellenado.| 
|FULLTEXT GATHERER |Tiene lugar durante la sincronización de operaciones de texto completo.| 
|GDMA_GET_RESOURCE_OWNER |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|GHOSTCLEANUP_UPDATE_STATS |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|GHOSTCLEANUPSYNCMGR |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|GLOBAL_QUERY_CANCEL |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|GLOBAL_QUERY_CLOSE |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|GLOBAL_QUERY_CONSUMER |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|GLOBAL_QUERY_PRODUCER |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|GLOBAL_TRAN_CREATE |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|GLOBAL_TRAN_UCS_SESSION |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|GUARDIAN |Solamente se identifica con fines informativos. No compatible. La compatibilidad con versiones posteriores no está garantizada.| 
|HADR_AG_MUTEX |Se produce cuando una instrucción siempre DDL o un comando de clústeres de conmutación por error de Windows Server está esperando para el acceso de lectura/escritura exclusivo a la configuración de un grupo de disponibilidad., <br /> **Se aplica a**: desde [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_AR_CRITICAL_SECTION_ENTRY |Se produce cuando una instrucción siempre DDL o un comando de clústeres de conmutación por error de Windows Server está esperando para el acceso de lectura/escritura exclusivo al estado en tiempo de ejecución de la réplica local del grupo de disponibilidad asociada., <br /> **Se aplica a**: desde [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_AR_MANAGER_MUTEX |Se produce cuando el cierre de la réplica de disponibilidad espera a que el inicio se complete o cuando un inicio de una réplica de disponibilidad espera a que el cierre se complete. Solo para uso interno., <br /> **Se aplica a**: desde [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_AR_UNLOAD_COMPLETED |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_ARCONTROLLER_NOTIFICATIONS_SUBSCRIBER_LIST |El publicador de un evento de réplica de disponibilidad (como un cambio de estado o de configuración) espera a un acceso de lectura/escritura exclusivo a la lista de suscriptores de evento. Solo para uso interno., <br /> **Se aplica a**: desde [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_BACKUP_BULK_LOCK |Siempre en base de datos principal se recibió una solicitud de copia de seguridad de una base de datos secundaria y está esperando para el fondo del subproceso termine de procesar la solicitud al adquirir o liberar el bloqueo BulkOp., <br /> **Se aplica a**: desde [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_BACKUP_QUEUE |El subproceso en segundo plano de copia de seguridad de la principal base de datos AlwaysOn está esperando una nueva solicitud de trabajo de la base de datos secundaria. (normalmente, esto se produce cuando la base de datos principal es contiene el registro BulkOp y espera para que la base de datos secundaria indicar que la base de datos principal puede liberar el bloqueo)., <br /> **Se aplica a**: desde [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_CLUSAPI_CALL |Un subproceso de SQL Server está esperando para cambiar del modo no preferente (programado por SQL Server) a modo preferente (programado por el sistema operativo) para invocar la API de agrupación en clústeres de conmutación por error de Windows Server., <br /> **Se aplica a**: desde [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_COMPRESSED_CACHE_SYNC |Esperando el acceso a la memoria caché de bloques de registros comprimidos que se utiliza para evitar la compresión redundante de los bloques de registro enviados a varias bases de datos secundarias., <br /> **Se aplica a**: desde [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_CONNECTIVITY_INFO |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_DATABASE_FLOW_CONTROL |En espera de que se envíen mensajes al asociado cuando se ha alcanzado el número máximo de mensajes en cola. Indica que los exámenes del registro se ejecutan más rápidamente de lo que la red necesita. Esto es un problema solo si envíos en la red son más lentas de lo esperado., <br /> **Se aplica a**: desde [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_DATABASE_VERSIONING_STATE |Se produce en el cambio de estado de control de versiones de un siempre en base de datos secundaria. Esta espera es para estructuras de datos internas y suele ser muy breve y no tener efecto directo sobre acceso a datos., <br /> **Se aplica a**: desde [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_DATABASE_WAIT_FOR_RECOVERY |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_DATABASE_WAIT_FOR_RESTART |Esperando a que la base de datos se reinicie bajo el control de grupos de disponibilidad AlwaysOn. En condiciones normales, esto no es un problema para el cliente porque se prevé esperas., <br /> **Se aplica a**: desde [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_DATABASE_WAIT_FOR_TRANSITION_TO_VERSIONING |Una consulta en los objetos en una base de datos secundaria legible de un siempre en grupo de disponibilidad se bloquea en las versiones de fila mientras se espera la confirmación o reversión de todas las transacciones que estaban en curso cuando se habilitó la réplica secundaria para las cargas de trabajo de lecturas. Este tipo de espera garantiza que las versiones de fila están disponibles antes de la ejecución de una consulta con aislamiento de instantánea., <br /> **Se aplica a**: desde [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_DB_COMMAND |Esperando las respuestas a mensajes conversacionales (que requieren una respuesta explícita del otro lado, mediante la infraestructura de mensajes conversacionales AlwaysOn). Un número de distintos tipos de mensaje usa este tipo de espera., <br /> **Se aplica a**: desde [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_DB_OP_COMPLETION_SYNC |Esperando las respuestas a mensajes conversacionales (que requieren una respuesta explícita del otro lado, mediante la infraestructura de mensajes conversacionales AlwaysOn). Un número de distintos tipos de mensaje usa este tipo de espera., <br /> **Se aplica a**: desde [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_DB_OP_START_SYNC |Una instrucción siempre DDL o un comando de clústeres de conmutación por error de Windows Server está esperando acceso serializado a una base de datos de disponibilidad y su estado en tiempo de ejecución., <br /> **Se aplica a**: desde [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_DBR_SUBSCRIBER |El publicador de un evento de réplica de disponibilidad (como un cambio de estado o de configuración) espera a un acceso de lectura/escritura exclusivo al estado de runtime de un suscriptor de evento que se corresponda con una base de datos de disponibilidad. Solo para uso interno., <br /> **Se aplica a**: desde [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_DBR_SUBSCRIBER_FILTER_LIST |El publicador de un evento de réplica de disponibilidad (como un cambio de estado o de configuración) espera a un acceso de lectura/escritura exclusivo a la lista de suscriptores de evento que se corresponda con las bases de datos de disponibilidad. Solo para uso interno., <br /> **Se aplica a**: desde [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_DBSEEDING |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_DBSEEDING_LIST |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_DBSTATECHANGE_SYNC |Espera de control de simultaneidad para actualizar el estado interno de la réplica de base de datos., <br /> **Se aplica a**: desde [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_FABRIC_CALLBACK |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_FILESTREAM_BLOCK_FLUSH |El Administrador de transporte FILESTREAM siempre en espera hasta que finalice el procesamiento de un bloque de registro., <br /> **Se aplica a**: desde [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_FILESTREAM_FILE_CLOSE |El Administrador de transporte FILESTREAM siempre en espera hasta que el siguiente archivo FILESTREAM se procesa y su controlador se cierra., <br /> **Se aplica a**: desde [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_FILESTREAM_FILE_REQUEST |Un siempre en la réplica secundaria espera de la réplica principal enviar FILESTREAM solicitado todos los archivos durante la reversión., <br /> **Se aplica a**: desde [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_FILESTREAM_IOMGR |El Administrador de transporte FILESTREAM siempre en espera de bloqueo de lectura/escritura que proteja el Administrador de FILESTREAM siempre en E/S durante el inicio o apagado., <br /> **Se aplica a**: desde [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_FILESTREAM_IOMGR_IOCOMPLETION |El Administrador de FILESTREAM siempre en E/S es esperar la finalización de E/S., <br /> **Se aplica a**: desde [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_FILESTREAM_MANAGER |El Administrador de transporte FILESTREAM Always On está esperando el bloqueo de lectura/escritura que proteja el Administrador de transporte FILESTREAM Always On durante el inicio o apagado., <br /> **Se aplica a**: desde [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_FILESTREAM_PREPROC |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_GROUP_COMMIT |El procesamiento de la confirmación de la transacción está esperando para permitir la confirmación de un grupo de modo que se puedan poner varios registros del registro de confirmación en un solo bloque de registros. Esta espera es una condición esperada que optimiza la E/S del registro, capturar y operaciones de envío., <br /> **Se aplica a**: desde [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_LOGCAPTURE_SYNC |El control de simultaneidad alrededor del objeto de aplicación o de la captura de registro al crear o destruir exámenes. Esto es una espera prevista cuando asociados cambian el estado de conexión o estado., <br /> **Se aplica a**: desde [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_LOGCAPTURE_WAIT |En espera de que los registros estén disponibles. Puede ocurrir al esperar a que las conexiones generen nuevos registros o a que se complete la entrada/salida al leer un registro que no está en la memoria caché. Se trata de una espera prevista si el examen del registro se pone al día hasta el final del registro o se lee desde el disco., <br /> **Se aplica a**: desde [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_LOGPROGRESS_SYNC |Espera de control de simultaneidad al actualizar el estado de progreso de registro de réplicas de base de datos., <br /> **Se aplica a**: desde [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_NOTIFICATION_DEQUEUE |Una tarea en segundo plano que procesa las notificaciones de Clústeres de conmutación por error de Windows Server está esperando la siguiente notificación. Solo para uso interno., <br /> **Se aplica a**: desde [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_NOTIFICATION_WORKER_EXCLUSIVE_ACCESS |El Administrador de réplica de disponibilidad AlwaysOn está esperando acceso serializado al estado en tiempo de ejecución de una tarea en segundo plano que procesa las notificaciones de clústeres de conmutación por error de Windows Server. Solo para uso interno., <br /> **Se aplica a**: desde [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_NOTIFICATION_WORKER_STARTUP_SYNC |Una tarea en segundo plano está esperando a que se complete el inicio de una tarea en segundo plano que procesa las notificaciones de Clústeres de conmutación por error de Windows Server. Solo para uso interno., <br /> **Se aplica a**: desde [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_NOTIFICATION_WORKER_TERMINATION_SYNC |Una tarea en segundo plano está esperando a que se termine una tarea en segundo plano que procesa las notificaciones de Clústeres de conmutación por error de Windows Server. Solo para uso interno., <br /> **Se aplica a**: desde [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_PARTNER_SYNC |Espera de control de simultaneidad en la lista de socios comerciales., <br /> **Se aplica a**: desde [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_READ_ALL_NETWORKS |En espera para obtener acceso de lectura o escritura a la lista de redes WSFC. Exclusivamente para uso interno. Nota: El motor mantiene una lista de redes WSFC que se usa en las vistas de administración dinámica (por ejemplo, sys.dm_hadr_cluster_networks) o para validar siempre en Transact-SQL instrucciones que hacen referencia WSFC información de la red. Esta lista se actualiza tras el inicio del motor, relativas a WSFC notificaciones e interno siempre en reinicio (por ejemplo, pérdida y recuperando el quórum de WSFC). Normalmente, las tareas se bloquearán cuando una actualización de esa lista esté en curso. , <br /> **Se aplica a**: desde [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_RECOVERY_WAIT_FOR_CONNECTION |En espera de que la base de datos secundaria se conecte a la principal antes de realizar la recuperación. Se trata de una espera prevista, que puede alargarse si la conexión a la réplica principal se establece con lentitud., <br /> **Se aplica a**: desde [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_RECOVERY_WAIT_FOR_UNDO |La recuperación de la base de datos espera a que la base de datos secundaria finalice la fase de reversión e inicialización para traerla de nuevo al punto de registro común con la base de datos principal. Se trata de una espera prevista tras las conmutaciones por error. Deshacer progreso puede realizar el seguimiento a través del Monitor de sistema de Windows (perfmon.exe) y vistas de administración dinámica., <br /> **Se aplica a**: desde [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_REPLICAINFO_SYNC |Esperando el control de simultaneidad actualizar el estado actual de la réplica., <br /> **Se aplica a**: desde [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_SEEDING_CANCELLATION |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_SEEDING_FILE_LIST |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_SEEDING_LIMIT_BACKUPS |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_SEEDING_SYNC_COMPLETION |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_SEEDING_TIMEOUT_TASK |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_SEEDING_WAIT_FOR_COMPLETION |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_SYNC_COMMIT |En espera del procesamiento de confirmación de transacciones para las bases de datos secundarias sincronizadas para reforzar el registro. Esta espera también se refleja en el contador de rendimiento Retraso de transacción. Este tipo de espera se espera para sincronizar grupos de disponibilidad e indica el tiempo para enviar, escribir y reconocer el registro en las bases de datos secundarias., <br /> **Se aplica a**: desde [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_SYNCHRONIZING_THROTTLE |En espera para que el proceso de confirmación de transacciones permita a una base de datos secundaria ponerse al día con la principal al final del registro para pasar al estado sincronizado. Esto es una espera prevista cuando una base de datos secundaria se pone al día., <br /> **Se aplica a**: desde [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_TDS_LISTENER_SYNC |El sistema AlwaysOn interno o el clúster de WSFC, se solicitará que los agentes de escucha se inician o se ha detenido. El proceso de esta solicitud siempre es asíncrono y hay un mecanismo para quitar las solicitudes redundantes. También hay momentos en que este proceso se suspende debido a los cambios en la configuración. Todas las esperas relacionadas con este mecanismo de sincronización del agente de escucha usan este tipo de espera. Solo para uso interno., <br /> **Se aplica a**: desde [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_TDS_LISTENER_SYNC_PROCESSING |Se usa al final de una instrucción siempre en Transact-SQL que requiere iniciar o detener el agente de escucha del grupo de anavailability. Puesto que la operación de inicio/detención se realiza de forma asincrónica, el subproceso de usuario se bloqueará con este tipo de espera hasta que se conoce la situación del agente de escucha., <br /> **Se aplica a**: desde [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_THROTTLE_LOG_RATE_GOVERNOR |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_THROTTLE_LOG_RATE_LOG_SIZE |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_THROTTLE_LOG_RATE_SEEDING |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_THROTTLE_LOG_RATE_SEND_RECV_QUEUE_SIZE |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_TIMER_TASK |En espera de obtener el bloqueo en el objeto de tarea de temporizador y se usa también para las esperas reales entre los momentos en que el trabajo se realiza. Por ejemplo, para una tarea que se ejecuta cada 10 segundos, tras una ejecución, grupos de disponibilidad AlwaysOn esperan aproximadamente 10 segundos para volver a programar la tarea y la espera se incluye aquí., <br /> **Se aplica a**: desde [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_TRANSPORT_DBRLIST |En espera para acceder a la lista de réplicas de bases de datos de la capa de transporte. Utilizado para el interbloqueo que concede acceso a él., <br /> **Se aplica a**: desde [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_TRANSPORT_FLOW_CONTROL |En espera cuando el número de mensajes de inicio de AlwaysOn no reconocidos pendientes está por encima de la salida umbral de control de flujo. Se trata de forma de réplica a réplica de disponibilidad (no para una base de datos a base de datos)., <br /> **Se aplica a**: desde [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_TRANSPORT_SESSION |Grupos de disponibilidad AlwaysOn está esperando mientras se cambia o tener acceso al estado de transporte subyacente., <br /> **Se aplica a**: desde [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_WORK_POOL |Espera de control de simultaneidad en el objeto de tarea del trabajo de segundo plano de grupos de disponibilidad AlwaysOn., <br /> **Se aplica a**: desde [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_WORK_QUEUE |Grupos de disponibilidad AlwaysOn esperando nuevos trabajos que se asignará el subproceso de trabajo en segundo plano. Esto es una espera prevista cuando hay trabajadores preparados en espera para el nuevo trabajo, que es el estado normal., <br /> **Se aplica a**: desde [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HADR_XRF_STACK_ACCESS |Obtener acceso a (Buscar, agregar y eliminar) la pila de bifurcación de recuperación extendida para una base de datos de disponibilidad AlwaysOn., <br /> **Se aplica a**: desde [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HCCO_CACHE |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HK_RESTORE_FILEMAP |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HKCS_PARALLEL_MIGRATION |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HKCS_PARALLEL_RECOVERY |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HTBUILD |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HTDELETE |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HTMEMO |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HTREINIT |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HTREPARTITION |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|HTTP_ENUMERATION |Tiene lugar en el inicio para enumerar los extremos HTTP al iniciar HTTP.| 
|HTTP_START |Tiene lugar cuando una conexión espera hasta que HTTP complete la inicialización.| 
|HTTP_STORAGE_CONNECTION |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|IMPPROV_IOWAIT |Se produce cuando SQL Server espera una carga masiva de E/S para finalizar.| 
|INSTANCE_LOG_RATE_GOVERNOR |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|INTERNAL_TESTING |Solamente se identifica con fines informativos. No compatible. La compatibilidad con versiones posteriores no está garantizada.| 
|IO_AUDIT_MUTEX |Tiene lugar durante la sincronización de búferes de eventos de seguimiento.| 
|IO_COMPLETION |Tiene lugar mientras se espera la finalización de operaciones de E/S. Generalmente, este tipo de espera representa operaciones de E/S de páginas que no son de datos. Esperas de finalización de E/S de páginas de datos aparecen como PAGEIOLATCH\_ \* espera.| 
|IO_QUEUE_LIMIT |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|IO_RETRY |Tiene lugar cuando una operación de E/S como una lectura o una escritura de disco no se realiza correctamente debido a un número insuficiente de recursos y, posteriormente, se vuelve a intentar.| 
|IOAFF_RANGE_QUEUE |Solamente se identifica con fines informativos. No compatible. La compatibilidad con versiones posteriores no está garantizada.| 
|KSOURCE_WAKEUP |Se utiliza en la tarea de control de servicios mientras se esperan solicitudes del Administrador de control de servicios. Se prevén esperas largas que no indican ningún problema.| 
|KTM_ENLISTMENT |Solamente se identifica con fines informativos. No compatible. La compatibilidad con versiones posteriores no está garantizada.| 
|KTM_RECOVERY_MANAGER |Solamente se identifica con fines informativos. No compatible. La compatibilidad con versiones posteriores no está garantizada.| 
|KTM_RECOVERY_RESOLUTION |Solamente se identifica con fines informativos. No compatible. La compatibilidad con versiones posteriores no está garantizada.| 
|LATCH_DT |Tiene lugar cuando se espera un bloqueo temporal de destrucción (DT). No incluye bloqueos temporales de búfer ni de marca de transacción. Una lista de bloqueo temporal\_ \* esperas en sys.dm_os_latch_stats está disponible. Tenga en cuenta que los grupos LATCH_NL, LATCH_SH, LATCH_UP, LATCH_EX y LATCH_DT de sys.dm_os_latch_stats esperan juntos.| 
|LATCH_EX |Tiene lugar cuando se espera un bloqueo temporal exclusivo (EX). No incluye bloqueos temporales de búfer ni de marca de transacción. Una lista de bloqueo temporal\_ \* esperas en sys.dm_os_latch_stats está disponible. Tenga en cuenta que los grupos LATCH_NL, LATCH_SH, LATCH_UP, LATCH_EX y LATCH_DT de sys.dm_os_latch_stats esperan juntos.| 
|LATCH_KP |Tiene lugar cuando se espera un bloqueo temporal de mantenimiento (KP). No incluye bloqueos temporales de búfer ni de marca de transacción. Una lista de bloqueo temporal\_ \* esperas en sys.dm_os_latch_stats está disponible. Tenga en cuenta que los grupos LATCH_NL, LATCH_SH, LATCH_UP, LATCH_EX y LATCH_DT de sys.dm_os_latch_stats esperan juntos.| 
|LATCH_NL |Solamente se identifica con fines informativos. No compatible. La compatibilidad con versiones posteriores no está garantizada.| 
|LATCH_SH |Tiene lugar cuando se espera un bloqueo temporal de uso compartido (SH). No incluye bloqueos temporales de búfer ni de marca de transacción. Una lista de bloqueo temporal\_ \* esperas en sys.dm_os_latch_stats está disponible. Tenga en cuenta que los grupos LATCH_NL, LATCH_SH, LATCH_UP, LATCH_EX y LATCH_DT de sys.dm_os_latch_stats esperan juntos.| 
|LATCH_UP |Tiene lugar cuando se espera un bloqueo temporal de actualización (UP). No incluye bloqueos temporales de búfer ni de marca de transacción. Una lista de bloqueo temporal\_ \* esperas en sys.dm_os_latch_stats está disponible. Tenga en cuenta que los grupos LATCH_NL, LATCH_SH, LATCH_UP, LATCH_EX y LATCH_DT de sys.dm_os_latch_stats esperan juntos.| 
|LAZYWRITER_SLEEP |Tiene lugar cuando se suspenden tareas de escritura diferida. Ésta es una medida del tiempo invertido por las tareas en segundo plano que esperan. No tenga en cuenta este estado cuando busque pausas del usuario.| 
|LCK_M_BU |Tiene lugar cuando una tarea está esperando adquirir un bloqueo de actualización masiva (BU).| 
|LCK_M_BU_ABORT_BLOCKERS |Tiene lugar cuando una tarea está esperando adquirir un bloqueo de actualización masiva (BU) con ABORT BLOCKERS. (Relacionado con la opción de espera de prioridad baja de ALTER TABLE y ALTER INDEX.), <br /> **Se aplica a**: desde [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LCK_M_BU_LOW_PRIORITY |Tiene lugar cuando una tarea está esperando adquirir un bloqueo de actualización masiva (BU) con prioridad baja. (Relacionado con la opción de espera de prioridad baja de ALTER TABLE y ALTER INDEX.), <br /> **Se aplica a**: desde [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LCK_M_IS |Tiene lugar cuando una tarea está esperando adquirir un bloqueo de intención compartida (IS).| 
|LCK_M_IS_ABORT_BLOCKERS |Tiene lugar cuando una tarea está esperando adquirir un bloqueo de intención compartida (IS) con ABORT BLOCKERS. (Relacionado con la opción de espera de prioridad baja de ALTER TABLE y ALTER INDEX.), <br /> **Se aplica a**: desde [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LCK_M_IS_LOW_PRIORITY |Tiene lugar cuando una tarea está esperando adquirir un bloqueo de intención compartida (IS) con baja prioridad. (Relacionado con la opción de espera de prioridad baja de ALTER TABLE y ALTER INDEX.), <br /> **Se aplica a**: desde [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LCK_M_IU |Tiene lugar cuando una tarea está esperando adquirir un bloqueo de intención de actualización (IU).| 
|LCK_M_IU_ABORT_BLOCKERS |Tiene lugar cuando una tarea está esperando adquirir un bloqueo de intención de actualización (IU) con ABORT BLOCKERS. (Relacionado con la opción de espera de prioridad baja de ALTER TABLE y ALTER INDEX.), <br /> **Se aplica a**: desde [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LCK_M_IU_LOW_PRIORITY |Tiene lugar cuando una tarea está esperando adquirir un bloqueo de intención de actualización (IU) con baja prioridad. (Relacionado con la opción de espera de prioridad baja de ALTER TABLE y ALTER INDEX.), <br /> **Se aplica a**: desde [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LCK_M_IX |Tiene lugar cuando una tarea está esperando adquirir un bloqueo de intención exclusiva (IX).| 
|LCK_M_IX_ABORT_BLOCKERS |Tiene lugar cuando una tarea está esperando adquirir un bloqueo de intención exclusiva (IX) con ABORT BLOCKERS. (Relacionado con la opción de espera de prioridad baja de ALTER TABLE y ALTER INDEX.), <br /> **Se aplica a**: desde [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LCK_M_IX_LOW_PRIORITY |Tiene lugar cuando una tarea está esperando adquirir un bloqueo de intención exclusiva (IX) con baja prioridad. (Relacionado con la opción de espera de prioridad baja de ALTER TABLE y ALTER INDEX.), <br /> **Se aplica a**: desde [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LCK_M_RIn_NL |Tiene lugar cuando una tarea está esperando adquirir un bloqueo NULL en el valor de clave actual y un bloqueo de intervalo de inserción entre la clave anterior y la actual. Un bloqueo NULL en la clave es un bloqueo de liberación instantánea.| 
|LCK_M_RIn_NL_ABORT_BLOCKERS |Tiene lugar cuando una tarea está esperando adquirir un bloqueo NULL con ABORT BLOCKERS en el valor de clave actual y un bloqueo de intervalo de inserción con ABORT BLOCKERS entre la clave anterior y la actual. Un bloqueo NULL en la clave es un bloqueo de liberación instantánea. (Relacionado con la opción de espera de prioridad baja de ALTER TABLE y ALTER INDEX.), <br /> **Se aplica a**: desde [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LCK_M_RIn_NL_LOW_PRIORITY |Tiene lugar cuando una tarea está esperando adquirir un bloqueo NULL con baja prioridad en el valor de clave actual y un bloqueo de intervalo de inserción con baja prioridad entre la clave anterior y la actual. Un bloqueo NULL en la clave es un bloqueo de liberación instantánea. (Relacionado con la opción de espera de prioridad baja de ALTER TABLE y ALTER INDEX.), <br /> **Se aplica a**: desde [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LCK_M_RIn_S |Tiene lugar cuando una tarea está esperando adquirir un bloqueo de uso compartido en el valor de clave actual y un bloqueo de intervalo de inserción entre la clave anterior y la actual.| 
|LCK_M_RIn_S_ABORT_BLOCKERS |Tiene lugar cuando una tarea está esperando adquirir un bloqueo compartido con ABORT BLOCKERS en el valor de clave actual y un bloqueo de intervalo de inserción con ABORT BLOCKERS entre la clave anterior y la actual. (Relacionado con la opción de espera de prioridad baja de ALTER TABLE y ALTER INDEX.), <br /> **Se aplica a**: desde [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LCK_M_RIn_S_LOW_PRIORITY |Tiene lugar cuando una tarea está esperando adquirir un bloqueo compartido con baja prioridad en el valor de clave actual y un bloqueo de intervalo de inserción con baja prioridad entre la clave anterior y la actual. (Relacionado con la opción de espera de prioridad baja de ALTER TABLE y ALTER INDEX.), <br /> **Se aplica a**: desde [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LCK_M_RIn_U |La tarea espera adquirir un bloqueo de actualización en el valor de clave actual y un bloqueo de intervalo de inserción entre la clave anterior y la actual.| 
|LCK_M_RIn_U_ABORT_BLOCKERS |La tarea está esperando adquirir un bloqueo de actualización con ABORT BLOCKERS en el valor de clave actual y un bloqueo de intervalo de inserción con ABORT BLOCKERS entre la clave anterior y la actual. (Relacionado con la opción de espera de prioridad baja de ALTER TABLE y ALTER INDEX.), <br /> **Se aplica a**: desde [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LCK_M_RIn_U_LOW_PRIORITY |La tarea está esperando adquirir un bloqueo de actualización con baja prioridad en el valor de clave actual y un bloqueo de intervalo de inserción con baja prioridad entre la clave anterior y la actual. (Relacionado con la opción de espera de prioridad baja de ALTER TABLE y ALTER INDEX.), <br /> **Se aplica a**: desde [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LCK_M_RIn_X |Tiene lugar cuando una tarea está esperando adquirir un bloqueo exclusivo en el valor de clave actual y un bloqueo de intervalo de inserción entre la clave anterior y la actual.| 
|LCK_M_RIn_X_ABORT_BLOCKERS |Tiene lugar cuando una tarea está esperando adquirir un bloqueo exclusivo con ABORT BLOCKERS en el valor de clave actual y un bloqueo de intervalo de inserción con ABORT BLOCKERS entre la clave anterior y la actual. (Relacionado con la opción de espera de prioridad baja de ALTER TABLE y ALTER INDEX.), <br /> **Se aplica a**: desde [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LCK_M_RIn_X_LOW_PRIORITY |Tiene lugar cuando una tarea está esperando adquirir un bloqueo exclusivo con baja prioridad en el valor de clave actual y un bloqueo de intervalo de inserción con baja prioridad entre la clave anterior y la actual. (Relacionado con la opción de espera de prioridad baja de ALTER TABLE y ALTER INDEX.), <br /> **Se aplica a**: desde [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LCK_M_RS_S |Tiene lugar cuando una tarea está esperando adquirir un bloqueo de uso compartido en el valor de clave actual y un bloqueo de intervalo compartido entre la clave anterior y la actual.| 
|LCK_M_RS_S_ABORT_BLOCKERS |Tiene lugar cuando una tarea está esperando adquirir un bloqueo compartido con ABORT BLOCKERS en el valor de clave actual y un bloqueo de intervalo compartido con ABORT BLOCKERS entre la clave anterior y la actual. (Relacionado con la opción de espera de prioridad baja de ALTER TABLE y ALTER INDEX.), <br /> **Se aplica a**: desde [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LCK_M_RS_S_LOW_PRIORITY |Tiene lugar cuando una tarea está esperando adquirir un bloqueo compartido con baja prioridad en el valor de clave actual y un bloqueo de intervalo compartido con baja prioridad entre la clave anterior y la actual. (Relacionado con la opción de espera de prioridad baja de ALTER TABLE y ALTER INDEX.), <br /> **Se aplica a**: desde [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LCK_M_RS_U |Tiene lugar cuando una tarea está esperando adquirir un bloqueo de actualización en el valor de clave actual y un bloqueo de intervalo de actualización entre la clave anterior y la actual.| 
|LCK_M_RS_U_ABORT_BLOCKERS |Tiene lugar cuando una tarea está esperando adquirir un bloqueo de actualización con ABORT BLOCKERS en el valor de clave actual y un bloqueo de intervalo de actualización con ABORT BLOCKERS entre la clave anterior y la actual. (Relacionado con la opción de espera de prioridad baja de ALTER TABLE y ALTER INDEX.), <br /> **Se aplica a**: desde [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LCK_M_RS_U_LOW_PRIORITY |Tiene lugar cuando una tarea está esperando adquirir un bloqueo de actualización con baja prioridad en el valor de clave actual y un bloqueo de intervalo de actualización con baja prioridad entre la clave anterior y la actual. (Relacionado con la opción de espera de prioridad baja de ALTER TABLE y ALTER INDEX.), <br /> **Se aplica a**: desde [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LCK_M_RX_S |Tiene lugar cuando una tarea está esperando adquirir un bloqueo de uso compartido en el valor de clave actual y un bloqueo de intervalo exclusivo entre la clave anterior y la actual.| 
|LCK_M_RX_S_ABORT_BLOCKERS |Tiene lugar cuando una tarea está esperando adquirir un bloqueo compartido con ABORT BLOCKERS en el valor de clave actual y un bloqueo de intervalo exclusivo con bloqueo ABORT BLOCKERS entre la clave anterior y la actual. (Relacionado con la opción de espera de prioridad baja de ALTER TABLE y ALTER INDEX.), <br /> **Se aplica a**: desde [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LCK_M_RX_S_LOW_PRIORITY |Tiene lugar cuando una tarea está esperando adquirir un bloqueo compartido con baja prioridad en el valor de clave actual y un bloqueo de intervalo exclusivo con bloqueo de baja prioridad entre la clave anterior y la actual. (Relacionado con la opción de espera de prioridad baja de ALTER TABLE y ALTER INDEX.), <br /> **Se aplica a**: desde [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LCK_M_RX_U |Tiene lugar cuando una tarea está esperando adquirir un bloqueo de actualización en el valor de clave actual y un bloqueo de intervalo exclusivo entre la clave anterior y la actual.| 
|LCK_M_RX_U_ABORT_BLOCKERS |Tiene lugar cuando una tarea está esperando adquirir un bloqueo de actualización con ABORT BLOCKERS en el valor de clave actual y un bloqueo de intervalo exclusivo con ABORT BLOCKERS entre la clave anterior y la actual. (Relacionado con la opción de espera de prioridad baja de ALTER TABLE y ALTER INDEX.), <br /> **Se aplica a**: desde [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LCK_M_RX_U_LOW_PRIORITY |Tiene lugar cuando una tarea está esperando adquirir un bloqueo de actualización con baja prioridad en el valor de clave actual y un bloqueo de intervalo exclusivo con baja prioridad entre la clave anterior y la actual. (Relacionado con la opción de espera de prioridad baja de ALTER TABLE y ALTER INDEX.), <br /> **Se aplica a**: desde [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LCK_M_RX_X |Tiene lugar cuando una tarea está esperando adquirir un bloqueo exclusivo en el valor de clave actual y un bloqueo de intervalo exclusivo entre la clave anterior y la actual.| 
|LCK_M_RX_X_ABORT_BLOCKERS |Tiene lugar cuando una tarea está esperando adquirir un bloqueo exclusivo con ABORT BLOCKERS en el valor de clave actual y un bloqueo de intervalo exclusivo con ABORT BLOCKERS entre la clave anterior y la actual. (Relacionado con la opción de espera de prioridad baja de ALTER TABLE y ALTER INDEX.), <br /> **Se aplica a**: desde [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LCK_M_RX_X_LOW_PRIORITY |Tiene lugar cuando una tarea está esperando adquirir un bloqueo exclusivo con baja prioridad en el valor de clave actual y un bloqueo de intervalo exclusivo con baja prioridad entre la clave anterior y la actual. (Relacionado con la opción de espera de prioridad baja de ALTER TABLE y ALTER INDEX.), <br /> **Se aplica a**: desde [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LCK_M_S |Tiene lugar cuando una tarea está esperando a adquirir un bloqueo compartido.| 
|LCK_M_S_ABORT_BLOCKERS |Tiene lugar cuando una tarea está esperando adquirir un bloqueo compartido con ABORT BLOCKERS. (Relacionado con la opción de espera de prioridad baja de ALTER TABLE y ALTER INDEX.), <br /> **Se aplica a**: desde [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LCK_M_S_LOW_PRIORITY |Tiene lugar cuando una tarea está esperando adquirir un bloqueo compartido con baja prioridad. (Relacionado con la opción de espera de prioridad baja de ALTER TABLE y ALTER INDEX.), <br /> **Se aplica a**: desde [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LCK_M_SCH_M |Tiene lugar cuando una tarea está esperando a adquirir un bloqueo de modificación de esquema.| 
|LCK_M_SCH_M_ABORT_BLOCKERS |Tiene lugar cuando una tarea está esperando a adquirir un bloqueo de modificación de esquema con ABORT BLOCKERS. (Relacionado con la opción de espera de prioridad baja de ALTER TABLE y ALTER INDEX.), <br /> **Se aplica a**: desde [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LCK_M_SCH_M_LOW_PRIORITY |Tiene lugar cuando una tarea está esperando a adquirir un bloqueo de modificación de esquema con baja prioridad. (Relacionado con la opción de espera de prioridad baja de ALTER TABLE y ALTER INDEX.), <br /> **Se aplica a**: desde [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LCK_M_SCH_S |Tiene lugar cuando una tarea está esperando adquirir un bloqueo de uso compartido de esquema.| 
|LCK_M_SCH_S_ABORT_BLOCKERS |Tiene lugar cuando una tarea está esperando a adquirir un bloqueo de uso compartido de esquema con ABORT BLOCKERS. (Relacionado con la opción de espera de prioridad baja de ALTER TABLE y ALTER INDEX.), <br /> **Se aplica a**: desde [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LCK_M_SCH_S_LOW_PRIORITY |Tiene lugar cuando una tarea está esperando a adquirir un bloqueo de uso compartido de esquema con baja prioridad. (Relacionado con la opción de espera de prioridad baja de ALTER TABLE y ALTER INDEX.), <br /> **Se aplica a**: desde [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LCK_M_SIU |Tiene lugar cuando una tarea está esperando adquirir un bloqueo de uso compartido con intento de actualización.| 
|LCK_M_SIU_ABORT_BLOCKERS |Tiene lugar cuando una tarea está esperando adquirir un bloqueo de uso compartido con actualización intensiva con ABORT BLOCKERS. (Relacionado con la opción de espera de prioridad baja de ALTER TABLE y ALTER INDEX.), <br /> **Se aplica a**: desde [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LCK_M_SIU_LOW_PRIORITY |Tiene lugar cuando una tarea está esperando adquirir un bloqueo de uso compartido con actualización exclusiva con baja prioridad. (Relacionado con la opción de espera de prioridad baja de ALTER TABLE y ALTER INDEX.), <br /> **Se aplica a**: desde [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LCK_M_SIX |Tiene lugar cuando una tarea está esperando adquirir un bloqueo de uso compartido con intención exclusiva.| 
|LCK_M_SIX_ABORT_BLOCKERS |Tiene lugar cuando una tarea está esperando adquirir un bloqueo de uso compartido con intención exclusiva con ABORT BLOCKERS. (Relacionado con la opción de espera de prioridad baja de ALTER TABLE y ALTER INDEX.), <br /> **Se aplica a**: desde [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LCK_M_SIX_LOW_PRIORITY |Tiene lugar cuando una tarea está esperando adquirir un bloqueo de uso compartido con intención exclusiva con baja prioridad. (Relacionado con la opción de espera de prioridad baja de ALTER TABLE y ALTER INDEX.), <br /> **Se aplica a**: desde [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LCK_M_U |Tiene lugar cuando una tarea está esperando a adquirir un bloqueo de actualización.| 
|LCK_M_U_ABORT_BLOCKERS |Tiene lugar cuando una tarea está esperando adquirir un bloqueo de actualización con ABORT BLOCKERS. (Relacionado con la opción de espera de prioridad baja de ALTER TABLE y ALTER INDEX.), <br /> **Se aplica a**: desde [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LCK_M_U_LOW_PRIORITY |Tiene lugar cuando una tarea está esperando adquirir un bloqueo de actualización con baja prioridad. (Relacionado con la opción de espera de prioridad baja de ALTER TABLE y ALTER INDEX.), <br /> **Se aplica a**: desde [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LCK_M_UIX |Tiene lugar cuando una tarea está esperando adquirir un bloqueo de actualización con intención exclusiva.| 
|LCK_M_UIX_ABORT_BLOCKERS |Tiene lugar cuando una tarea está esperando adquirir un bloqueo de actualización con intención exclusiva con ABORT BLOCKERS. (Relacionado con la opción de espera de prioridad baja de ALTER TABLE y ALTER INDEX.), <br /> **Se aplica a**: desde [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LCK_M_UIX_LOW_PRIORITY |Tiene lugar cuando una tarea está esperando adquirir un bloqueo de actualización con intención exclusiva con baja prioridad. (Relacionado con la opción de espera de prioridad baja de ALTER TABLE y ALTER INDEX.), <br /> **Se aplica a**: desde [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LCK_M_X |Tiene lugar cuando una tarea está esperando a adquirir un bloqueo exclusivo.| 
|LCK_M_X_ABORT_BLOCKERS |Tiene lugar cuando una tarea está esperando adquirir un bloqueo exclusivo con ABORT BLOCKERS. (Relacionado con la opción de espera de prioridad baja de ALTER TABLE y ALTER INDEX.), <br /> **Se aplica a**: desde [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LCK_M_X_LOW_PRIORITY |Tiene lugar cuando una tarea está esperando adquirir un bloqueo exclusivo con baja prioridad. (Relacionado con la opción de espera de prioridad baja de ALTER TABLE y ALTER INDEX.), <br /> **Se aplica a**: desde [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LOG_POOL_SCAN |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LOG_RATE_GOVERNOR |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LOGBUFFER |Tiene lugar cuando una tarea está esperando tener espacio en el búfer del registro para almacenar un registro. Valores coherentemente altos pueden indicar que los dispositivos de registro no pueden hacer frente a la cantidad de registros que va a generar el servidor.| 
|LOGCAPTURE_LOGPOOLTRUNCPOINT |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LOGGENERATION |Solamente se identifica con fines informativos. No compatible. La compatibilidad con versiones posteriores no está garantizada.| 
|LOGMGR |Tiene lugar cuando una tarea está esperando que finalicen operaciones de E/S pendientes para cerrar el registro mientras se cierra la base de datos.| 
|LOGMGR_FLUSH |Solamente se identifica con fines informativos. No compatible. La compatibilidad con versiones posteriores no está garantizada.| 
|LOGMGR_PMM_LOG |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LOGMGR_QUEUE |Tiene lugar mientras la tarea de escritura en registro espera solicitudes de trabajo.| 
|LOGMGR_RESERVE_APPEND |Tiene lugar cuando una tarea está esperando comprobar si el truncamiento del registro libera espacio del registro para permitir que la tarea escriba un nuevo registro. Para reducir esta espera, puede aumentar el tamaño de los archivos de registro de la base de datos correspondiente.| 
|LOGPOOL_CACHESIZE |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LOGPOOL_CONSUMER |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LOGPOOL_CONSUMERSET |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LOGPOOL_FREEPOOLS |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LOGPOOL_MGRSET |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LOGPOOL_REPLACEMENTSET |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LOGPOOLREFCOUNTEDOBJECT_REFDONE |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|LOWFAIL_MEMMGR_QUEUE |Tiene lugar mientras se espera que haya memoria disponible para su uso.| 
|MD_AGENT_YIELD |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|MD_LAZYCACHE_RWLOCK |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|MEMORY_ALLOCATION_EXT |Se produce al asignar memoria desde el bloque de memoria interno de SQL Server o el sistema operativo., <br /> **Se aplica a**: desde [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|MEMORY_GRANT_UPDATE |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|METADATA_LAZYCACHE_RWLOCK |TBD <br /> **Se aplica a**: [!INCLUDE[ssKilimanjaro_md](../../includes/sskilimanjaro-md.md)] solo. |  
|MIGRATIONBUFFER |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|MISCELLANEOUS |Solamente se identifica con fines informativos. No compatible. La compatibilidad con versiones posteriores no está garantizada.| 
|MISCELLANEOUS |Solamente se identifica con fines informativos. No compatible. La compatibilidad con versiones posteriores no está garantizada.| 
|MSQL_DQ |Tiene lugar cuando una tarea está esperando que finalice una operación de consulta distribuida. Se utiliza para detectar potenciales interbloqueos de aplicación MARS (Conjuntos de resultados activos múltiples). La espera termina cuando finaliza la llamada a la consulta distribuida.| 
|MSQL_XACT_MGR_MUTEX |Tiene lugar cuando una tarea está esperando obtener la propiedad del administrador de transacciones de la sesión para realizar una operación de transacción en el nivel de sesión.| 
|MSQL_XACT_MUTEX |Tiene lugar durante la sincronización del uso de transacciones. Una solicitud debe adquirir la exclusión mutua para poder utilizar la transacción.| 
|MSQL_XP |Tiene lugar cuando una tarea está esperando que finalice un procedimiento almacenado extendido. SQL Server utiliza este estado de espera para detectar potenciales interbloqueos de aplicación MARS. La espera se detiene cuando finaliza la llamada al procedimiento almacenado extendido.| 
|MSSEARCH |Tiene lugar durante las llamadas a la búsqueda de texto completo. Esta espera termina cuando finaliza la operación de texto completo. No indica contención, sino la duración de las operaciones de texto completo.| 
|NET_WAITFOR_PACKET |Tiene lugar cuando una conexión está esperando un paquete de red durante una lectura de red.| 
|NETWORKSXMLMGRLOAD |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|NODE_CACHE_MUTEX |TBD| 
|OLEDB |Se produce cuando SQL Server llama el proveedor SQL Server Native Client OLE DB. Este estado de espera no se usa para la sincronización. Se usa para indicar la duración de las llamadas al proveedor OLE DB.| 
|ONDEMAND_TASK_QUEUE |Tiene lugar mientras una tarea en segundo plano espera solicitudes de tarea del sistema de alta prioridad. Los tiempos de espera largos indican que no ha habido que procesar solicitudes de alta prioridad; no deben suponer un problema.| 
|PAGEIOLATCH_DT |Tiene lugar cuando una tarea está esperando en un bloqueo temporal por un búfer que está en una solicitud de E/S. La solicitud de bloqueo temporal está en modo de destrucción. Las esperas largas pueden indicar problemas en el subsistema del disco.| 
|PAGEIOLATCH_EX |Tiene lugar cuando una tarea está esperando en un bloqueo temporal por un búfer que está en una solicitud de E/S. La solicitud de bloqueo temporal está en modo exclusivo. Las esperas largas pueden indicar problemas en el subsistema del disco.| 
|PAGEIOLATCH_KP |Tiene lugar cuando una tarea está esperando en un bloqueo temporal por un búfer que está en una solicitud de E/S. La solicitud de bloqueo temporal está en modo de conservación. Las esperas largas pueden indicar problemas en el subsistema del disco.| 
|PAGEIOLATCH_NL |Solamente se identifica con fines informativos. No compatible. La compatibilidad con versiones posteriores no está garantizada.| 
|PAGEIOLATCH_SH |Tiene lugar cuando una tarea está esperando en un bloqueo temporal por un búfer que está en una solicitud de E/S. La solicitud de bloqueo temporal está en modo compartido. Las esperas largas pueden indicar problemas en el subsistema del disco.| 
|PAGEIOLATCH_UP |Tiene lugar cuando una tarea está esperando en un bloqueo temporal por un búfer que está en una solicitud de E/S. La solicitud de bloqueo temporal está en modo de actualización. Las esperas largas pueden indicar problemas en el subsistema del disco.| 
|PAGELATCH_DT |Tiene lugar cuando una tarea está esperando en un bloqueo temporal por un búfer que no está en una solicitud de E/S. La solicitud de bloqueo temporal está en modo de destrucción.| 
|PAGELATCH_EX |Tiene lugar cuando una tarea está esperando en un bloqueo temporal por un búfer que no está en una solicitud de E/S. La solicitud de bloqueo temporal está en modo exclusivo.| 
|PAGELATCH_KP |Tiene lugar cuando una tarea está esperando en un bloqueo temporal por un búfer que no está en una solicitud de E/S. La solicitud de bloqueo temporal está en modo de conservación.| 
|PAGELATCH_NL |Solamente se identifica con fines informativos. No compatible. La compatibilidad con versiones posteriores no está garantizada.| 
|PAGELATCH_SH |Tiene lugar cuando una tarea está esperando en un bloqueo temporal por un búfer que no está en una solicitud de E/S. La solicitud de bloqueo temporal está en modo compartido.| 
|PAGELATCH_UP |Tiene lugar cuando una tarea está esperando en un bloqueo temporal por un búfer que no está en una solicitud de E/S. La solicitud de bloqueo temporal está en modo de actualización.| 
|PARALLEL_BACKUP_QUEUE |Tiene lugar cuando se serializa la salida generada por RESTORE HEADERONLY, RESTORE FILELISTONLY o RESTORE LABELONLY.| 
|PARALLEL_REDO_DRAIN_WORKER |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PARALLEL_REDO_FLOW_CONTROL |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PARALLEL_REDO_LOG_CACHE |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PARALLEL_REDO_TRAN_LIST |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PARALLEL_REDO_TRAN_TURN |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PARALLEL_REDO_WORKER_SYNC |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PARALLEL_REDO_WORKER_WAIT_WORK |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PERFORMANCE_COUNTERS_RWLOCK |TBD| 
|PHYSICAL_SEEDING_DMV |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|POOL_LOG_RATE_GOVERNOR |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PREEMPTIVE_ABR |Solamente se identifica con fines informativos. No compatible. La compatibilidad con versiones posteriores no está garantizada.| 
|PREEMPTIVE_AUDIT_ACCESS_EVENTLOG |Tiene lugar cuando el programador del sistema operativo de [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] (SQLOS) cambia a modo preferente para escribir un evento de auditoría en el registro de eventos de Windows. <br /> **Se aplica a**: [!INCLUDE[ssKilimanjaro_md](../../includes/sskilimanjaro-md.md)] solo. |  
|PREEMPTIVE_AUDIT_ACCESS_SECLOG |Tiene lugar cuando el programador de SQLOS cambia a modo preferente para escribir un evento de auditoría en el registro de seguridad de Windows. <br /> **Se aplica a**: [!INCLUDE[ssKilimanjaro_md](../../includes/sskilimanjaro-md.md)] solo. |  
|PREEMPTIVE_CLOSEBACKUPMEDIA |Tiene lugar cuando el programador de SQLOS cambia a modo preferente para cerrar el medio de copia de seguridad.| 
|PREEMPTIVE_CLOSEBACKUPTAPE |Tiene lugar cuando el programador de SQLOS cambia a modo preferente para cerrar un dispositivo de copia de seguridad de cinta.| 
|PREEMPTIVE_CLOSEBACKUPVDIDEVICE |Tiene lugar cuando el programador de SQLOS cambia a modo preferente para cerrar un dispositivo de copia de seguridad virtual.| 
|PREEMPTIVE_CLUSAPI_CLUSTERRESOURCECONTROL |Tiene lugar cuando el programador de SQLOS cambia a modo preferente para realizar las operaciones de clúster de conmutación por error de Windows.| 
|PREEMPTIVE_COM_COCREATEINSTANCE |Tiene lugar cuando el programador de SQLOS cambia a modo preferente para crear un objeto COM.| 
|PREEMPTIVE_COM_COGETCLASSOBJECT |TBD| 
|PREEMPTIVE_COM_CREATEACCESSOR |TBD| 
|PREEMPTIVE_COM_DELETEROWS |TBD| 
|PREEMPTIVE_COM_GETCOMMANDTEXT |TBD| 
|PREEMPTIVE_COM_GETDATA |TBD| 
|PREEMPTIVE_COM_GETNEXTROWS |TBD| 
|PREEMPTIVE_COM_GETRESULT |TBD| 
|PREEMPTIVE_COM_GETROWSBYBOOKMARK |TBD| 
|PREEMPTIVE_COM_LBFLUSH |TBD| 
|PREEMPTIVE_COM_LBLOCKREGION |TBD| 
|PREEMPTIVE_COM_LBREADAT |TBD| 
|PREEMPTIVE_COM_LBSETSIZE |TBD| 
|PREEMPTIVE_COM_LBSTAT |TBD| 
|PREEMPTIVE_COM_LBUNLOCKREGION |TBD| 
|PREEMPTIVE_COM_LBWRITEAT |TBD| 
|PREEMPTIVE_COM_QUERYINTERFACE |TBD| 
|PREEMPTIVE_COM_RELEASE |TBD| 
|PREEMPTIVE_COM_RELEASEACCESSOR |TBD| 
|PREEMPTIVE_COM_RELEASEROWS |TBD| 
|PREEMPTIVE_COM_RELEASESESSION |TBD| 
|PREEMPTIVE_COM_RESTARTPOSITION |TBD| 
|PREEMPTIVE_COM_SEQSTRMREAD |TBD| 
|PREEMPTIVE_COM_SEQSTRMREADANDWRITE |TBD| 
|PREEMPTIVE_COM_SETDATAFAILURE |TBD| 
|PREEMPTIVE_COM_SETPARAMETERINFO |TBD| 
|PREEMPTIVE_COM_SETPARAMETERPROPERTIES |TBD| 
|PREEMPTIVE_COM_STRMLOCKREGION |TBD| 
|PREEMPTIVE_COM_STRMSEEKANDREAD |TBD| 
|PREEMPTIVE_COM_STRMSEEKANDWRITE |TBD| 
|PREEMPTIVE_COM_STRMSETSIZE |TBD| 
|PREEMPTIVE_COM_STRMSTAT |TBD| 
|PREEMPTIVE_COM_STRMUNLOCKREGION |TBD| 
|PREEMPTIVE_CONSOLEWRITE |TBD| 
|PREEMPTIVE_CREATEPARAM |TBD| 
|PREEMPTIVE_DEBUG |TBD| 
|PREEMPTIVE_DFSADDLINK |TBD| 
|PREEMPTIVE_DFSLINKEXISTCHECK |TBD| 
|PREEMPTIVE_DFSLINKHEALTHCHECK |TBD| 
|PREEMPTIVE_DFSREMOVELINK |TBD| 
|PREEMPTIVE_DFSREMOVEROOT |TBD| 
|PREEMPTIVE_DFSROOTFOLDERCHECK |TBD| 
|PREEMPTIVE_DFSROOTINIT |TBD| 
|PREEMPTIVE_DFSROOTSHARECHECK |TBD| 
|PREEMPTIVE_DTC_ABORT |TBD| 
|PREEMPTIVE_DTC_ABORTREQUESTDONE |TBD| 
|PREEMPTIVE_DTC_BEGINTRANSACTION |TBD| 
|PREEMPTIVE_DTC_COMMITREQUESTDONE |TBD| 
|PREEMPTIVE_DTC_ENLIST |TBD| 
|PREEMPTIVE_DTC_PREPAREREQUESTDONE |TBD| 
|PREEMPTIVE_FILESIZEGET |TBD| 
|PREEMPTIVE_FSAOLEDB_ABORTTRANSACTION |TBD| 
|PREEMPTIVE_FSAOLEDB_COMMITTRANSACTION |TBD| 
|PREEMPTIVE_FSAOLEDB_STARTTRANSACTION |TBD| 
|PREEMPTIVE_FSRECOVER_UNCONDITIONALUNDO |TBD| 
|PREEMPTIVE_GETRMINFO |TBD| 
|PREEMPTIVE_HADR_LEASE_MECHANISM |Administrador de concesiones de grupos de disponibilidad AlwaysOn de programación para el diagnóstico CSS., <br /> **Se aplica a**: desde [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PREEMPTIVE_HTTP_EVENT_WAIT |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PREEMPTIVE_HTTP_REQUEST |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PREEMPTIVE_LOCKMONITOR |TBD| 
|PREEMPTIVE_MSS_RELEASE |TBD| 
|PREEMPTIVE_ODBCOPS |TBD| 
|PREEMPTIVE_OLE_UNINIT |TBD| 
|PREEMPTIVE_OLEDB_ABORTORCOMMITTRAN |TBD| 
|PREEMPTIVE_OLEDB_ABORTTRAN |TBD| 
|PREEMPTIVE_OLEDB_GETDATASOURCE |TBD| 
|PREEMPTIVE_OLEDB_GETLITERALINFO |TBD| 
|PREEMPTIVE_OLEDB_GETPROPERTIES |TBD| 
|PREEMPTIVE_OLEDB_GETPROPERTYINFO |TBD| 
|PREEMPTIVE_OLEDB_GETSCHEMALOCK |TBD| 
|PREEMPTIVE_OLEDB_JOINTRANSACTION |TBD| 
|PREEMPTIVE_OLEDB_RELEASE |TBD| 
|PREEMPTIVE_OLEDB_SETPROPERTIES |TBD| 
|PREEMPTIVE_OLEDBOPS |TBD| 
|PREEMPTIVE_OS_ACCEPTSECURITYCONTEXT |TBD| 
|PREEMPTIVE_OS_ACQUIRECREDENTIALSHANDLE |TBD| 
|PREEMPTIVE_OS_AUTHENTICATIONOPS |TBD| 
|PREEMPTIVE_OS_AUTHORIZATIONOPS |TBD| 
|PREEMPTIVE_OS_AUTHZGETINFORMATIONFROMCONTEXT |TBD| 
|PREEMPTIVE_OS_AUTHZINITIALIZECONTEXTFROMSID |TBD| 
|PREEMPTIVE_OS_AUTHZINITIALIZERESOURCEMANAGER |TBD| 
|PREEMPTIVE_OS_BACKUPREAD |TBD| 
|PREEMPTIVE_OS_CLOSEHANDLE |TBD| 
|PREEMPTIVE_OS_CLUSTEROPS |TBD| 
|PREEMPTIVE_OS_COMOPS |TBD| 
|PREEMPTIVE_OS_COMPLETEAUTHTOKEN |TBD| 
|PREEMPTIVE_OS_COPYFILE |TBD| 
|PREEMPTIVE_OS_CREATEDIRECTORY |TBD| 
|PREEMPTIVE_OS_CREATEFILE |TBD| 
|PREEMPTIVE_OS_CRYPTACQUIRECONTEXT |TBD| 
|PREEMPTIVE_OS_CRYPTIMPORTKEY |TBD| 
|PREEMPTIVE_OS_CRYPTOPS |TBD| 
|PREEMPTIVE_OS_DECRYPTMESSAGE |TBD| 
|PREEMPTIVE_OS_DELETEFILE |TBD| 
|PREEMPTIVE_OS_DELETESECURITYCONTEXT |TBD| 
|PREEMPTIVE_OS_DEVICEIOCONTROL |TBD| 
|PREEMPTIVE_OS_DEVICEOPS |TBD| 
|PREEMPTIVE_OS_DIRSVC_NETWORKOPS |TBD| 
|PREEMPTIVE_OS_DISCONNECTNAMEDPIPE |TBD| 
|PREEMPTIVE_OS_DOMAINSERVICESOPS |TBD| 
|PREEMPTIVE_OS_DSGETDCNAME |TBD| 
|PREEMPTIVE_OS_DTCOPS |TBD| 
|PREEMPTIVE_OS_ENCRYPTMESSAGE |TBD| 
|PREEMPTIVE_OS_FILEOPS |TBD| 
|PREEMPTIVE_OS_FINDFILE |TBD| 
|PREEMPTIVE_OS_FLUSHFILEBUFFERS |TBD| 
|PREEMPTIVE_OS_FORMATMESSAGE |TBD| 
|PREEMPTIVE_OS_FREECREDENTIALSHANDLE |TBD| 
|PREEMPTIVE_OS_FREELIBRARY |TBD| 
|PREEMPTIVE_OS_GENERICOPS |TBD| 
|PREEMPTIVE_OS_GETADDRINFO |TBD| 
|PREEMPTIVE_OS_GETCOMPRESSEDFILESIZE |TBD| 
|PREEMPTIVE_OS_GETDISKFREESPACE |TBD| 
|PREEMPTIVE_OS_GETFILEATTRIBUTES |TBD| 
|PREEMPTIVE_OS_GETFILESIZE |TBD| 
|PREEMPTIVE_OS_GETFINALFILEPATHBYHANDLE |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PREEMPTIVE_OS_GETLONGPATHNAME |TBD| 
|PREEMPTIVE_OS_GETPROCADDRESS |TBD| 
|PREEMPTIVE_OS_GETVOLUMENAMEFORVOLUMEMOUNTPOINT |TBD| 
|PREEMPTIVE_OS_GETVOLUMEPATHNAME |TBD| 
|PREEMPTIVE_OS_INITIALIZESECURITYCONTEXT |TBD| 
|PREEMPTIVE_OS_LIBRARYOPS |TBD| 
|PREEMPTIVE_OS_LOADLIBRARY |TBD| 
|PREEMPTIVE_OS_LOGONUSER |TBD| 
|PREEMPTIVE_OS_LOOKUPACCOUNTSID |TBD| 
|PREEMPTIVE_OS_MESSAGEQUEUEOPS |TBD| 
|PREEMPTIVE_OS_MOVEFILE |TBD| 
|PREEMPTIVE_OS_NETGROUPGETUSERS |TBD| 
|PREEMPTIVE_OS_NETLOCALGROUPGETMEMBERS |TBD| 
|PREEMPTIVE_OS_NETUSERGETGROUPS |TBD| 
|PREEMPTIVE_OS_NETUSERGETLOCALGROUPS |TBD| 
|PREEMPTIVE_OS_NETUSERMODALSGET |TBD| 
|PREEMPTIVE_OS_NETVALIDATEPASSWORDPOLICY |TBD| 
|PREEMPTIVE_OS_NETVALIDATEPASSWORDPOLICYFREE |TBD| 
|PREEMPTIVE_OS_OPENDIRECTORY |TBD| 
|PREEMPTIVE_OS_PDH_WMI_INIT |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PREEMPTIVE_OS_PIPEOPS |TBD| 
|PREEMPTIVE_OS_PROCESSOPS |TBD| 
|PREEMPTIVE_OS_QUERYCONTEXTATTRIBUTES |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PREEMPTIVE_OS_QUERYREGISTRY |TBD| 
|PREEMPTIVE_OS_QUERYSECURITYCONTEXTTOKEN |TBD| 
|PREEMPTIVE_OS_REMOVEDIRECTORY |TBD| 
|PREEMPTIVE_OS_REPORTEVENT |TBD| 
|PREEMPTIVE_OS_REVERTTOSELF |TBD| 
|PREEMPTIVE_OS_RSFXDEVICEOPS |TBD| 
|PREEMPTIVE_OS_SECURITYOPS |TBD| 
|PREEMPTIVE_OS_SERVICEOPS |TBD| 
|PREEMPTIVE_OS_SETENDOFFILE |TBD| 
|PREEMPTIVE_OS_SETFILEPOINTER |TBD| 
|PREEMPTIVE_OS_SETFILEVALIDDATA |TBD| 
|PREEMPTIVE_OS_SETNAMEDSECURITYINFO |TBD| 
|PREEMPTIVE_OS_SQLCLROPS |TBD| 
|PREEMPTIVE_OS_SQMLAUNCH |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssKilimanjaro_md](../../includes/sskilimanjaro-md.md)] hasta [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)]. |  
|PREEMPTIVE_OS_VERIFYSIGNATURE |TBD| 
|PREEMPTIVE_OS_VERIFYTRUST |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PREEMPTIVE_OS_VSSOPS |TBD| 
|PREEMPTIVE_OS_WAITFORSINGLEOBJECT |TBD| 
|PREEMPTIVE_OS_WINSOCKOPS |TBD| 
|PREEMPTIVE_OS_WRITEFILE |TBD| 
|PREEMPTIVE_OS_WRITEFILEGATHER |TBD| 
|PREEMPTIVE_OS_WSASETLASTERROR |TBD| 
|PREEMPTIVE_REENLIST |TBD| 
|PREEMPTIVE_RESIZELOG |TBD| 
|PREEMPTIVE_ROLLFORWARDREDO |TBD| 
|PREEMPTIVE_ROLLFORWARDUNDO |TBD| 
|PREEMPTIVE_SB_STOPENDPOINT |TBD| 
|PREEMPTIVE_SERVER_STARTUP |TBD| 
|PREEMPTIVE_SETRMINFO |TBD| 
|PREEMPTIVE_SHAREDMEM_GETDATA |TBD| 
|PREEMPTIVE_SNIOPEN |TBD| 
|PREEMPTIVE_SOSHOST |TBD| 
|PREEMPTIVE_SOSTESTING |Solamente se identifica con fines informativos. No compatible. La compatibilidad con versiones posteriores no está garantizada.| 
|PREEMPTIVE_SP_SERVER_DIAGNOSTICS |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PREEMPTIVE_STARTRM |TBD| 
|PREEMPTIVE_STREAMFCB_CHECKPOINT |TBD| 
|PREEMPTIVE_STREAMFCB_RECOVER |TBD| 
|PREEMPTIVE_STRESSDRIVER |Solamente se identifica con fines informativos. No compatible. La compatibilidad con versiones posteriores no está garantizada.| 
|PREEMPTIVE_TESTING |Solamente se identifica con fines informativos. No compatible. La compatibilidad con versiones posteriores no está garantizada.| 
|PREEMPTIVE_TRANSIMPORT |TBD| 
|PREEMPTIVE_UNMARSHALPROPAGATIONTOKEN |TBD| 
|PREEMPTIVE_VSS_CREATESNAPSHOT |TBD| 
|PREEMPTIVE_VSS_CREATEVOLUMESNAPSHOT |TBD| 
|PREEMPTIVE_XE_CALLBACKEXECUTE |TBD| 
|PREEMPTIVE_XE_CX_FILE_OPEN |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PREEMPTIVE_XE_CX_HTTP_CALL |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PREEMPTIVE_XE_DISPATCHER |TBD| 
|PREEMPTIVE_XE_ENGINEINIT |TBD| 
|PREEMPTIVE_XE_GETTARGETSTATE |TBD| 
|PREEMPTIVE_XE_SESSIONCOMMIT |TBD| 
|PREEMPTIVE_XE_TARGETFINALIZE |TBD| 
|PREEMPTIVE_XE_TARGETINIT |TBD| 
|PREEMPTIVE_XE_TIMERRUN |TBD| 
|PREEMPTIVE_XETESTING |Solamente se identifica con fines informativos. No compatible. La compatibilidad con versiones posteriores no está garantizada.| 
|PRINT_ROLLBACK_PROGRESS |Se utiliza para esperar mientras los procesos del usuario finalizan en una base de datos que se ha pasado utilizando la cláusula de terminación ALTER DATABASE. Para obtener más información, consulte ALTER DATABASE (Transact-SQL).| 
|PRU_ROLLBACK_DEFERRED |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PWAIT_ALL_COMPONENTS_INITIALIZED |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PWAIT_COOP_SCAN |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PWAIT_DIRECTLOGCONSUMER_GETNEXT |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PWAIT_EVENT_SESSION_INIT_MUTEX |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PWAIT_FABRIC_REPLICA_CONTROLLER_DATA_LOSS |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PWAIT_HADR_ACTION_COMPLETED |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PWAIT_HADR_CHANGE_NOTIFIER_TERMINATION_SYNC |Se produce cuando una tarea en segundo plano está esperando la finalización de la tarea en segundo plano que recibe (a través de sondeo) las notificaciones de clústeres de conmutación por error de Windows Server., <br /> **Se aplica a**: desde [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PWAIT_HADR_CLUSTER_INTEGRATION |Una agregación, reemplazamiento o quitar operación está esperando para obtener un bloqueo de escritura en una lista interna AlwaysOn (por ejemplo, una lista de redes, direcciones de red o agentes de escucha de grupo de disponibilidad). Solo, para uso interno <br /> **Se aplica a**: desde [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PWAIT_HADR_FAILOVER_COMPLETED |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PWAIT_HADR_JOIN |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PWAIT_HADR_OFFLINE_COMPLETED |Una de AlwaysOn disponibilidad grupo operación de eliminación está esperando que el grupo de disponibilidad de destino se quede sin conexión antes de destruir los objetos de clústeres de conmutación por error de Windows Server., <br /> **Se aplica a**: desde [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PWAIT_HADR_ONLINE_COMPLETED |Un siempre en crear o está esperando la operación del grupo de disponibilidad de conmutación por error para que el grupo de disponibilidad de destino para ponerse en línea., <br /> **Se aplica a**: desde [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PWAIT_HADR_POST_ONLINE_COMPLETED |Una de AlwaysOn disponibilidad grupo operación de eliminación está esperando la finalización de cualquier tarea en segundo plano que se programara como parte de un comando anterior. Por ejemplo, el puede haber una tarea en segundo plano que esté pasando las bases de datos de disponibilidad al rol principal. La DDL DROP AVAILABILITY GROUP siempre debe esperar a que esta tarea en segundo plano termine para evitar condiciones de carrera., <br /> **Se aplica a**: desde [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PWAIT_HADR_SERVER_READY_CONNECTIONS |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PWAIT_HADR_WORKITEM_COMPLETED |Espera interna de un subproceso que espera a que una tarea de trabajo asincrónico se complete. Se trata de una espera prevista y es para utilizar CSS., <br /> **Se aplica a**: desde [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PWAIT_HADRSIM |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PWAIT_LOG_CONSOLIDATION_IO |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PWAIT_LOG_CONSOLIDATION_POLL |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PWAIT_MD_LOGIN_STATS |Se produce durante la sincronización interna en los metadatos estadísticas de inicio de sesión., <br /> **Se aplica a**: desde [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PWAIT_MD_RELATION_CACHE |Se produce durante la sincronización interna en los metadatos de tabla o un índice., <br /> **Se aplica a**: desde [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PWAIT_MD_SERVER_CACHE |Se produce durante la sincronización interna en los metadatos en servidores vinculados., <br /> **Se aplica a**: desde [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PWAIT_MD_UPGRADE_CONFIG |Se produce durante la sincronización interna de la actualización de configuraciones de servidor de gran., <br /> **Se aplica a**: desde [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PWAIT_PREEMPTIVE_APP_USAGE_TIMER |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PWAIT_PREEMPTIVE_AUDIT_ACCESS_WINDOWSLOG |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PWAIT_QRY_BPMEMORY |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PWAIT_REPLICA_ONLINE_INIT_MUTEX |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PWAIT_RESOURCE_SEMAPHORE_FT_PARALLEL_QUERY_SYNC |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PWAIT_SBS_FILE_OPERATION |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PWAIT_XTP_FSSTORAGE_MAINTENANCE |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|PWAIT_XTP_HOST_STORAGE_WAIT |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|QDS_ASYNC_CHECK_CONSISTENCY_TASK |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|QDS_ASYNC_PERSIST_TASK |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|QDS_ASYNC_PERSIST_TASK_START |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|QDS_ASYNC_QUEUE |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|QDS_BCKG_TASK |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|QDS_BLOOM_FILTER |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|QDS_CLEANUP_STALE_QUERIES_TASK_MAIN_LOOP_SLEEP |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|QDS_CTXS |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|QDS_DB_DISK |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|QDS_DYN_VECTOR |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|QDS_EXCLUSIVE_ACCESS |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|QDS_HOST_INIT |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|QDS_LOADDB |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|QDS_PERSIST_TASK_MAIN_LOOP_SLEEP |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|QDS_QDS_CAPTURE_INIT |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|QDS_SHUTDOWN_QUEUE |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|QDS_STMT |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|QDS_STMT_DISK |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|QDS_TASK_SHUTDOWN |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|QDS_TASK_START |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|QE_WARN_LIST_SYNC |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|QPJOB_KILL |Indica que una llamada a KILL ha cancelado una actualización de estadísticas automáticas asincrónicas cuando la actualización se empezaba a ejecutar. El subproceso de terminación está suspendido, en espera de que empiece a escuchar comandos KILL. Un buen valor es menor que un segundo.| 
|QPJOB_WAITFOR_ABORT |Indica que una llamada a KILL ha cancelado una actualización de estadísticas automáticas asincrónicas cuando se estaba ejecutando. La actualización no se ha completado, sino que está suspendida hasta que finalice la coordinación del mensaje del subproceso de terminación. Es un estado normal, pero excepcional, y debe ser muy corto. Un buen valor es menor que un segundo.| 
|QRY_MEM_GRANT_INFO_MUTEX |Tiene lugar cuando la administración de memoria de ejecución de la consulta intenta controlar el acceso a la lista estática de información de concesiones. Este estado muestra información acerca de las solicitudes de memoria en espera y concedidas actualmente. Este estado es un sencillo estado de control de acceso. En este estado nunca debe esperarse mucho. Si esta exclusión mutua no se libera, todas las nuevas consultas que utilizan memoria dejarán de responder.| 
|QRY_PARALLEL_THREAD_MUTEX |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|QRY_PROFILE_LIST_MUTEX |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|QUERY_ERRHDL_SERVICE_DONE |Solamente se identifica con fines informativos. No compatible. <br /> **Se aplica a**: [!INCLUDE[ssKilimanjaro_md](../../includes/sskilimanjaro-md.md)] solo. |  
|QUERY_WAIT_ERRHDL_SERVICE |Solamente se identifica con fines informativos.  No compatible. <br /> **Se aplica a**: [!INCLUDE[ssKilimanjaro_md](../../includes/sskilimanjaro-md.md)] solo.  |  
|QUERY_EXECUTION_INDEX_SORT_EVENT_OPEN |Tiene lugar en determinados casos, cuando la generación de índices sin conexión se ejecuta en paralelo y los diferentes subprocesos de trabajo que realizan la ordenación sincronizan el acceso a los archivos de ordenación.| 
|QUERY_NOTIFICATION_MGR_MUTEX |Tiene lugar durante la sincronización de la recopilación de elementos no utilizados en el administrador de notificaciones de consulta.| 
|QUERY_NOTIFICATION_SUBSCRIPTION_MUTEX |Tiene lugar durante la sincronización del estado en las transacciones de notificaciones de consulta.| 
|QUERY_NOTIFICATION_TABLE_MGR_MUTEX |Tiene lugar durante la sincronización interna en el administrador de notificaciones de consulta.| 
|QUERY_NOTIFICATION_UNITTEST_MUTEX |Solamente se identifica con fines informativos. No compatible. La compatibilidad con versiones posteriores no está garantizada.| 
|QUERY_OPTIMIZER_PRINT_MUTEX |Tiene lugar durante la sincronización de la producción de salida de diagnóstico del optimizador de consultas. Este tipo de espera sólo se produce si se ha habilitado la configuración de diagnóstico bajo la dirección de soporte técnico de Microsoft.| 
|QUERY_TASK_ENQUEUE_MUTEX |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|QUERY_TRACEOUT |Solamente se identifica con fines informativos. No compatible. La compatibilidad con versiones posteriores no está garantizada.| 
|RBIO_WAIT_VLF |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|RECOVER_CHANGEDB |Tiene lugar durante la sincronización del estado de base de datos en una base de datos en estado de espera activa.| 
|RECOVERY_MGR_LOCK |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|REDO_THREAD_PENDING_WORK |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|REDO_THREAD_SYNC |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|REMOTE_BLOCK_IO |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|REMOTE_DATA_ARCHIVE_MIGRATION_DMV |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|REMOTE_DATA_ARCHIVE_SCHEMA_DMV |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|REMOTE_DATA_ARCHIVE_SCHEMA_TASK_QUEUE |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|REPL_CACHE_ACCESS |Tiene lugar durante la sincronización en caché de artículos de una replicación. Durante estas esperas, el registro del LOG de replicación se detiene temporalmente y se bloquean las instrucciones de lenguaje de definición de datos (DLL) en una tabla publicada.| 
|REPL_HISTORYCACHE_ACCESS |TBD| 
|REPL_SCHEMA_ACCESS |Tiene lugar durante la sincronización de la información de versión del esquema de replicación. Este estado se produce cuando las instrucciones de DDL se ejecutan en el objeto replicado y cuando el registro del LOG genera o consume un esquema con versiones basado en las repeticiones de DDL. Contención puede verse en este tipo de espera si tiene muchas bases de datos publicados en un publicador único con la replicación transaccional y las bases de datos publicados son muy activos.| 
|REPL_TRANFSINFO_ACCESS |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|REPL_TRANHASHTABLE_ACCESS |TBD| 
|REPL_TRANTEXTINFO_ACCESS |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|REPLICA_WRITES |Tiene lugar mientras una tarea espera que finalicen las escrituras de página en instantáneas de la base de datos o en réplicas DBCC.| 
|REQUEST_DISPENSER_PAUSE |Tiene lugar cuando una tarea espera que finalicen todas las operaciones de E/S pendientes para poder inmovilizar la E/S en un archivo y realizar una copia de seguridad de instantánea.| 
|REQUEST_FOR_DEADLOCK_SEARCH |Tiene lugar mientras la supervisión de interbloqueos espera que comience la siguiente búsqueda de interbloqueos. Esta espera está prevista entre detecciones de interbloqueos; un tiempo de espera total largo en este recurso no indica un problema.| 
|RESERVED_MEMORY_ALLOCATION_EXT |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|RESMGR_THROTTLED |Tiene lugar cuando entra una nueva solicitud y se acelera basándose en GROUP_MAX_REQUESTS.| 
|RESOURCE_GOVERNOR_IDLE |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|RESOURCE_QUEUE |Tiene lugar durante la sincronización de diferentes colas internas de recursos.| 
|RESOURCE_SEMAPHORE |Tiene lugar cuando una solicitud de memoria de consulta no se puede conceder de forma inmediata debido a otras consultas simultáneas. Un número alto de esperas y tiempos de espera largos pueden indicar un número excesivo de consultas simultáneas o cantidades excesivas de solicitud de memoria.| 
|RESOURCE_SEMAPHORE_MUTEX |Tiene lugar mientras una consulta espera que se satisfaga su solicitud de reserva de subproceso. También se produce durante la sincronización de solicitudes de compilación de consultas y de concesión de memoria.| 
|RESOURCE_SEMAPHORE_QUERY_COMPILE |Tiene lugar cuando el número de compilaciones de consultas simultáneas alcanza un límite de aceleración. Un número alto de esperas y tiempos de espera largos pueden indicar compilaciones excesivas, recompilaciones o planes que no se pueden almacenar en caché.| 
|RESOURCE_SEMAPHORE_SMALL_QUERY |Tiene lugar cuando no se puede conceder de forma inmediata una solicitud de memoria de una consulta pequeña debido a otras consultas simultáneas. El tiempo de espera no debe superar unos segundos, ya que el servidor transfiere la solicitud al grupo principal de memoria de consulta si no puede conceder la memoria solicitada en este tiempo. Esperas altas pueden indicar un número excesivo de consultas pequeñas simultáneas y el bloqueo del grupo principal de memoria debido a consultas en espera. <br /> **Se aplica a**: [!INCLUDE[ssKilimanjaro_md](../../includes/sskilimanjaro-md.md)] solo. |  
|RESTORE_FILEHANDLECACHE_ENTRYLOCK |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|RESTORE_FILEHANDLECACHE_LOCK |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|RG_RECONFIG |TBD| 
|ROWGROUP_OP_STATS |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|ROWGROUP_VERSION |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|RTDATA_LIST |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|SATELLITE_CARGO |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|SATELLITE_SERVICE_SETUP |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|SATELLITE_TASK |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|SBS_DISPATCH |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|SBS_RECEIVE_TRANSPORT |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|SBS_TRANSPORT |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|SCAN_CHAR_HASH_ARRAY_INITIALIZATION |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|SEC_DROP_TEMP_KEY |Tiene lugar después de un error en el intento de quitar una clave de seguridad temporal y antes de volver a intentarlo.| 
|SECURITY_CNG_PROVIDER_MUTEX |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|SECURITY_CRYPTO_CONTEXT_MUTEX |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|SECURITY_DBE_STATE_MUTEX |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|SECURITY_KEYRING_RWLOCK |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|SECURITY_MUTEX |Tiene lugar cuando se esperan exclusiones mutuas que controlen el acceso a la lista global de proveedores de servicios criptográficos de Administración extensible de claves (EKM) y la lista de ámbito de sesión de sesiones de EKM.| 
|SECURITY_RULETABLE_MUTEX |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|SEMPLAT_DSI_BUILD |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|SEQUENCE_GENERATION |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|SEQUENTIAL_GUID |Tiene lugar mientras se obtiene un nuevo GUID secuencial.| 
|SERVER_IDLE_CHECK |Se produce durante la sincronización de estado inactivo de la instancia de SQL Server cuando se intenta declarar una instancia de SQL Server como inactiva o intentando activarse un monitor de recursos.| 
|SERVER_RECONFIGURE |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|SESSION_WAIT_STATS_CHILDREN |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|SHARED_DELTASTORE_CREATION |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|SHUTDOWN |Tiene lugar mientras una instrucción de cierre del sistema espera que las conexiones activas salgan.| 
|SLEEP_BPOOL_FLUSH |Tiene lugar cuando un punto de comprobación acelera la emisión de nuevas operaciones de E/S para evitar sobrecargar el subsistema del disco.| 
|SLEEP_BUFFERPOOL_HELPLW |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|SLEEP_DBSTARTUP |Tiene lugar durante el inicio de la base de datos mientras se espera la recuperación de todas las bases de datos.| 
|SLEEP_DCOMSTARTUP |Se produce una vez como máximo durante el inicio de la instancia de SQL Server mientras se espera que finalice la inicialización de DCOM.| 
|SLEEP_MASTERDBREADY |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|SLEEP_MASTERMDREADY |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|SLEEP_MASTERUPGRADED |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|SLEEP_MEMORYPOOL_ALLOCATEPAGES |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|SLEEP_MSDBSTARTUP |Tiene lugar cuando Seguimiento de SQL espera a que la base de datos msdb complete su inicio.| 
|SLEEP_RETRY_VIRTUALALLOC |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|SLEEP_SYSTEMTASK |Tiene lugar durante el inicio de una tarea en segundo plano mientras se espera que tempdb finalice el inicio.| 
|SLEEP_TASK |Tiene lugar cuando una tarea se mantiene inactiva mientras espera que se produzca un evento genérico.| 
|SLEEP_TEMPDBSTARTUP |Tiene lugar mientras una tarea espera que tempdb finalice el inicio.| 
|SLEEP_WORKSPACE_ALLOCATEPAGE |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|SLO_UPDATE |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|SMSYNC |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|SNI_CONN_DUP |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|SNI_CRITICAL_SECTION |Se produce durante la sincronización interna en los componentes de red de SQL Server.| 
|SNI_HTTP_WAITFOR_0_DISCON |Se produce durante el cierre de SQL Server, mientras se espera que todas las conexiones HTTP pendientes salir.| 
|SNI_LISTENER_ACCESS |Tiene lugar mientras se espera que los nodos de acceso a memoria no uniforme (NUMA) actualicen el cambio de estado. El acceso al cambio de estado está serializado.| 
|SNI_TASK_COMPLETION |Tiene lugar cuando se espera que finalicen todas las tareas durante un cambio de estado del nodo NUMA.| 
|SNI_WRITE_ASYNC |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|SOAP_READ |Tiene lugar mientras se espera que se complete una lectura de red HTTP.| 
|SOAP_WRITE |Tiene lugar mientras se espera que finalice una escritura de red HTTP.| 
|SOCKETDUPLICATEQUEUE_CLEANUP |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|SOS_CALLBACK_REMOVAL |Tiene lugar mientras se lleva a cabo la sincronización en una lista de devoluciones de llamada para quitar una devolución de llamada. No se espera que este contador cambie una vez completada la inicialización del servidor.| 
|SOS_DISPATCHER_MUTEX |Tiene lugar durante la sincronización interna del grupo de distribuidores. Esto incluye el ajuste del grupo.| 
|SOS_LOCALALLOCATORLIST |Tiene lugar durante la sincronización interna en el administrador de memoria de [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]. <br /> **Se aplica a**: [!INCLUDE[ssKilimanjaro_md](../../includes/sskilimanjaro-md.md)] solo. |  
|SOS_MEMORY_TOPLEVELBLOCKALLOCATOR |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|SOS_MEMORY_USAGE_ADJUSTMENT |Tiene lugar cuando se ajusta el uso de memoria entre los fondos.| 
|SOS_OBJECT_STORE_DESTROY_MUTEX |Tiene lugar durante la sincronización interna en grupos de memoria cuando se destruyen objetos del grupo.| 
|SOS_PHYS_PAGE_CACHE |Registra el tiempo que espera un subproceso para adquirir la exclusión mutua que debe adquirir antes de asignar páginas físicas o antes de devolver dichas páginas al sistema operativo. Esperas de este tipo solo aparecen si la instancia de SQL Server utiliza memoria AWE., <br /> **Se aplica a**: desde [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|SOS_PROCESS_AFFINITY_MUTEX |Tiene lugar durante la sincronización del acceso a la configuración de afinidad de procesos.| 
|SOS_RESERVEDMEMBLOCKLIST |Se produce durante la sincronización interna en el Administrador de memoria de SQL Server. <br /> **Se aplica a**: [!INCLUDE[ssKilimanjaro_md](../../includes/sskilimanjaro-md.md)] solo. |  
|SOS_SCHEDULER_YIELD |Tiene lugar cuando una tarea genera de forma voluntaria el programador para que se ejecuten otras tareas. Mientras, la tarea espera la renovación de su cuanto.| 
|SOS_SMALL_PAGE_ALLOC |Tiene lugar durante la asignación y la liberación de la memoria que administran algunos objetos de memoria.| 
|SOS_STACKSTORE_INIT_MUTEX |Tiene lugar durante la sincronización de la inicialización de almacenamiento interno.| 
|SOS_SYNC_TASK_ENQUEUE_EVENT |Tiene lugar cuando una tarea se inicia de forma sincrónica. Mayoría de las tareas en SQL Server se inicia de forma asincrónica, en el que control vuelve al iniciador inmediatamente después de la solicitud de tarea se ha colocado en la cola de trabajo.| 
|SOS_VIRTUALMEMORY_LOW |Tiene lugar cuando una asignación de memoria espera que un administrador de recursos libere memoria virtual.| 
|SOSHOST_EVENT |Se produce cuando un componente hospedado, como CLR, espera un objeto de sincronización de eventos de SQL Server.| 
|SOSHOST_INTERNAL |Tiene lugar durante la sincronización de devoluciones de llamada del administrador de memoria que utilizan los componentes hospedados, como CLR.| 
|SOSHOST_MUTEX |Se produce cuando un componente hospedado, como CLR, espera un objeto de sincronización de exclusión mutua de SQL Server.| 
|SOSHOST_RWLOCK |Se produce cuando un componente hospedado, como CLR, espera un objeto de sincronización de lector y escritor de SQL Server.| 
|SOSHOST_SEMAPHORE |Se produce cuando un componente hospedado, como CLR, espera un objeto de sincronización de semáforo de SQL Server.| 
|SOSHOST_SLEEP |Tiene lugar cuando una tarea hospedada se mantiene inactiva mientras espera que se produzca un evento genérico. Las tareas hospedadas son las que utilizan los componentes hospedados, como CLR.| 
|SOSHOST_TRACELOCK |Tiene lugar durante la sincronización del acceso a flujos de seguimiento.| 
|SOSHOST_WAITFORDONE |Tiene lugar cuando un componente hospedado, como CLR, espera la finalización de una tarea.| 
|SP_PREEMPTIVE_SERVER_DIAGNOSTICS_SLEEP |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|SP_SERVER_DIAGNOSTICS_BUFFER_ACCESS |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|SP_SERVER_DIAGNOSTICS_INIT_MUTEX |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|SP_SERVER_DIAGNOSTICS_SLEEP |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|SQLCLR_APPDOMAIN |Tiene lugar mientras CLR espera que complete el inicio de un dominio de aplicación.| 
|SQLCLR_ASSEMBLY |Tiene lugar mientras se espera el acceso a la lista de ensamblados cargada en el dominio de aplicación.| 
|SQLCLR_DEADLOCK_DETECTION |Tiene lugar mientras CLR espera la finalización de la detección de interbloqueos.| 
|SQLCLR_QUANTUM_PUNISHMENT |Tiene lugar cuando una tarea de CLR se acelera porque ha sobrepasado su cuanto de ejecución. Esta aceleración se lleva a cabo para reducir el efecto de esta tarea que consume muchos recursos en otras tareas.| 
|SQLSORT_NORMMUTEX |Tiene lugar durante la sincronización interna, mientras se inicializan estructuras de ordenación internas.| 
|SQLSORT_SORTMUTEX |Tiene lugar durante la sincronización interna, mientras se inicializan estructuras de ordenación internas.| 
|SQLTRACE_BUFFER_FLUSH |Tiene lugar cuando una tarea está esperando a que una tarea en segundo plano vuelque los búferes de seguimiento al disco cada cuatro segundos. <br /> **Se aplica a**: [!INCLUDE[ssKilimanjaro_md](../../includes/sskilimanjaro-md.md)] solo. |  
|SQLTRACE_FILE_BUFFER |Se produce durante la sincronización en búferes de seguimiento durante un seguimiento de archivos., <br /> **Se aplica a**: desde [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|SQLTRACE_FILE_READ_IO_COMPLETION |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|SQLTRACE_FILE_WRITE_IO_COMPLETION |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|SQLTRACE_INCREMENTAL_FLUSH_SLEEP |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|SQLTRACE_LOCK |TBD <br /> **Se aplica**: [!INCLUDE[ssKilimanjaro_md](../../includes/sskilimanjaro-md.md)] solo. |  
|SQLTRACE_PENDING_BUFFER_WRITERS |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|SQLTRACE_SHUTDOWN |Tiene lugar mientras el cierre del sistema de seguimiento espera la finalización de los eventos de seguimiento pendientes.| 
|SQLTRACE_WAIT_ENTRIES |Tiene lugar cuando una cola de eventos de Seguimiento de SQL espera que lleguen paquetes a la cola.| 
|SRVPROC_SHUTDOWN |Tiene lugar mientras el proceso de cierre del sistema espera la liberación de los recursos internos para cerrar sin problemas.| 
|STARTUP_DEPENDENCY_MANAGER |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|TDS_BANDWIDTH_STATE |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|TDS_INIT |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|TDS_PROXY_CONTAINER |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|TEMPOBJ |Tiene lugar cuando se sincronizan eliminaciones de objetos temporales. Esta espera no es muy común y solo se produce si una tarea ha solicitado el acceso exclusivo para eliminaciones de tablas temp.| 
|TEMPORAL_BACKGROUND_PROCEED_CLEANUP |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|TERMINATE_LISTENER |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|THREADPOOL |Tiene lugar cuando una tarea está esperando un trabajador en el que ejecutarse. Puede indicar que la configuración de número máximo de trabajadores es demasiado baja o que se tarda un tiempo inusualmente largo en las ejecuciones por lotes, lo que reduce el número de trabajadores disponibles para satisfacer otros lotes.| 
|TIMEPRIV_TIMEPERIOD |Tiene lugar durante la sincronización interna del temporizador de Extended Events.| 
|TRACE_EVTNOTIF |TBD| 
|TRACEWRITE |Tiene lugar cuando el proveedor de seguimiento de conjuntos de filas de Seguimiento de SQL espera un búfer libre o el procesamiento de un búfer con eventos.| 
|TRAN_MARKLATCH_DT |Tiene lugar cuando se espera un bloqueo temporal en modo de destrucción en un bloqueo temporal de marca de transacción. Los bloqueos temporales de marca de transacción se utilizan para la sincronización de confirmaciones con transacciones marcadas.| 
|TRAN_MARKLATCH_EX |Tiene lugar cuando se espera un bloqueo temporal en modo exclusivo en una transacción marcada. Los bloqueos temporales de marca de transacción se utilizan para la sincronización de confirmaciones con transacciones marcadas.| 
|TRAN_MARKLATCH_KP |Tiene lugar cuando se espera un bloqueo temporal en modo de mantenimiento en una transacción marcada. Los bloqueos temporales de marca de transacción se utilizan para la sincronización de confirmaciones con transacciones marcadas.| 
|TRAN_MARKLATCH_NL |Solamente se identifica con fines informativos. No compatible. La compatibilidad con versiones posteriores no está garantizada.| 
|TRAN_MARKLATCH_SH |Tiene lugar cuando se espera un bloqueo temporal en modo compartido en una transacción marcada. Los bloqueos temporales de marca de transacción se utilizan para la sincronización de confirmaciones con transacciones marcadas.| 
|TRAN_MARKLATCH_UP |Tiene lugar cuando se espera un bloqueo temporal en modo de actualización en una transacción marcada. Los bloqueos temporales de marca de transacción se utilizan para la sincronización de confirmaciones con transacciones marcadas.| 
|TRANSACTION_MUTEX |Tiene lugar durante la sincronización del acceso a una transacción por parte de varios lotes.| 
|UCS_ENDPOINT_CHANGE |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|UCS_MANAGER |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|UCS_MEMORY_NOTIFICATION |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|UCS_SESSION_REGISTRATION |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|UCS_TRANSPORT |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|UCS_TRANSPORT_STREAM_CHANGE |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|UTIL_PAGE_ALLOC |Tiene lugar cuando los exámenes del registro de transacciones esperan que haya memoria disponible durante la presión de memoria.| 
|VDI_CLIENT_COMPLETECOMMAND |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|VDI_CLIENT_GETCOMMAND |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|VDI_CLIENT_OPERATION |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|VDI_CLIENT_OTHER |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|VERSIONING_COMMITTING |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|VIA_ACCEPT |Tiene lugar cuando se completa la conexión del proveedor del Adaptador de interfaz virtual (VIA) durante el inicio.| 
|VIEW_DEFINITION_MUTEX |Tiene lugar durante la sincronización del acceso a definiciones de vista almacenadas en memoria caché.| 
|WAIT_FOR_RESULTS |Tiene lugar cuando se espera el inicio de una notificación de consulta.| 
|WAIT_SCRIPTDEPLOYMENT_REQUEST |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|WAIT_SCRIPTDEPLOYMENT_WORKER |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|WAIT_XLOGREAD_SIGNAL |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|WAIT_XTP_ASYNC_TX_COMPLETION |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|WAIT_XTP_CKPT_AGENT_WAKEUP |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|WAIT_XTP_CKPT_CLOSE |Se produce cuando se espera que complete un punto de comprobación., <br /> **Se aplica a**: desde [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|WAIT_XTP_CKPT_ENABLED |Se produce cuando los puntos de comprobación están deshabilitados y, a continuación, en espera de puntos de comprobación para habilitarse., <br /> **Se aplica a**: desde [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|WAIT_XTP_CKPT_STATE_LOCK |Se produce al sincronizar la comprobación del estado de punto de comprobación., <br /> **Se aplica a**: desde [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|WAIT_XTP_COMPILE_WAIT |TBD <br /> **Se aplica a**: [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|WAIT_XTP_GUEST |Tiene lugar cuando el asignador de memoria de la base de datos debe dejar de recibir notificaciones de memoria insuficiente., <br /> **Se aplica a**: desde [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|WAIT_XTP_HOST_WAIT |Se produce cuando espera sean desencadenado por el motor de base de datos e implementada por el host., <br /> **Se aplica a**: desde [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|WAIT_XTP_OFFLINE_CKPT_BEFORE_REDO |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|WAIT_XTP_OFFLINE_CKPT_LOG_IO |Se produce cuando un punto de comprobación sin conexión está esperando para un registro de lectura de E/S para completar., <br /> **Se aplica a**: desde [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|WAIT_XTP_OFFLINE_CKPT_NEW_LOG |Se produce cuando un punto de comprobación sin conexión está esperando para que nuevas entradas del registro Examinar., <br /> **Se aplica a**: desde [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|WAIT_XTP_PROCEDURE_ENTRY |Se produce cuando un procedimiento drop está esperando para todas las ejecuciones actuales del procedimiento para completar., <br /> **Se aplica a**: desde [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|WAIT_XTP_RECOVERY |Se produce cuando la recuperación de la base de datos está esperando para la recuperación de objetos optimizados en memoria para finalizar., <br /> **Se aplica a**: desde [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|WAIT_XTP_SERIAL_RECOVERY |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|WAIT_XTP_SWITCH_TO_INACTIVE |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|WAIT_XTP_TASK_SHUTDOWN |Se produce cuando se espera un subproceso de OLTP en memoria completar., <br /> **Se aplica a**: desde [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|WAIT_XTP_TRAN_DEPENDENCY |Se produce cuando se espera dependencias de la transacción., <br /> **Se aplica a**: desde [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|WAITFOR |Se produce como resultado de una instrucción WAITFOR Transact-SQL. La duración de la espera viene determinada por los parámetros de la instrucción. Se trata de una espera iniciada por el usuario.| 
|WAITFOR_PER_QUEUE |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|WAITFOR_TASKSHUTDOWN |Solamente se identifica con fines informativos. No compatible. La compatibilidad con versiones posteriores no está garantizada.| 
|WAITSTAT_MUTEX |Tiene lugar durante la sincronización del acceso a la colección de estadísticas utilizadas para rellenar sys.dm_os_wait_stats.| 
|WCC |Solamente se identifica con fines informativos. No compatible. La compatibilidad con versiones posteriores no está garantizada.| 
|WINDOW_AGGREGATES_MULTIPASS |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|WINFAB_API_CALL |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|WINFAB_REPLICA_BUILD_OPERATION |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|WINFAB_REPORT_FAULT |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|WORKTBL_DROP |Tiene lugar mientras se establece una pausa antes de volver a intentar una eliminación incorrecta de tablas de trabajo.| 
|WRITE_COMPLETION |Tiene lugar mientras está en curso una operación de escritura.| 
|WRITELOG |Tiene lugar mientras se espera que se complete un vaciado del registro. Las operaciones habituales que provocan vaciados del registro son los puntos de comprobación y las confirmaciones de transacciones.| 
|XACT_OWN_TRANSACTION |Tiene lugar mientras se espera adquirir la propiedad de una transacción.| 
|XACT_RECLAIM_SESSION |Tiene lugar mientras se espera que el propietario actual de una sesión libere la propiedad de la sesión.| 
|XACTLOCKINFO |Tiene lugar durante la sincronización del acceso a la lista de bloqueos de una transacción. Además de la propia transacción, a la lista de bloqueos tienen acceso operaciones como la detección de interbloqueos y la migración de bloqueos durante divisiones de página.| 
|XACTWORKSPACE_MUTEX |Tiene lugar durante la sincronización de bajas de una transacción, así como del número de bloqueos de base de datos entre los miembros dados de alta de una transacción.| 
|XDB_CONN_DUP_HASH |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|XDES_HISTORY |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|XDES_OUT_OF_ORDER_LIST |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|XDES_SNAPSHOT |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|XDESTSVERMGR |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|XE_BUFFERMGR_ALLPROCESSED_EVENT |Tiene lugar cuando los búferes de sesión de Extended Events se vacían en los destinos. Esta espera se produce en un subproceso en segundo plano.| 
|XE_BUFFERMGR_FREEBUF_EVENT |Tiene lugar cuando se presenta alguna de las siguientes condiciones:| 
|XE_CALLBACK_LIST |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|XE_CX_FILE_READ |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|XE_DISPATCHER_CONFIG_SESSION_LIST |Tiene lugar cuando una sesión de Extended Events que está utilizando destinos asincrónicos se inicia o se detiene. Esta espera indica alguna de las siguientes situaciones:| 
|XE_DISPATCHER_JOIN |Tiene lugar cuando un subproceso en segundo plano que se utiliza para sesiones de Extended Events está finalizando.| 
|XE_DISPATCHER_WAIT |Tiene lugar cuando un subproceso en segundo plano que se utiliza para sesiones de Extended Events está esperando a que se procesen los búferes de eventos.| 
|XE_FILE_TARGET_TVF |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|XE_LIVE_TARGET_TVF |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|XE_MODULEMGR_SYNC |Solamente se identifica con fines informativos. No compatible. La compatibilidad con versiones posteriores no está garantizada.| 
|XE_OLS_LOCK |Solamente se identifica con fines informativos. No compatible. La compatibilidad con versiones posteriores no está garantizada.| 
|XE_PACKAGE_LOCK_BACKOFF |Solamente se identifica con fines informativos. No compatible. <br /> **Se aplica a**: [!INCLUDE[ssKilimanjaro_md](../../includes/sskilimanjaro-md.md)] solo. |  
|XE_SERVICES_EVENTMANUAL |TBD| 
|XE_SERVICES_MUTEX |TBD| 
|XE_SERVICES_RWLOCK |TBD| 
|XE_SESSION_CREATE_SYNC |TBD| 
|XE_SESSION_FLUSH |TBD| 
|XE_SESSION_SYNC |TBD| 
|XE_STM_CREATE |TBD| 
|XE_TIMER_EVENT |TBD| 
|XE_TIMER_MUTEX |TBD| 
|XE_TIMER_TASK_DONE |TBD| 
|XIO_CREDENTIAL_MGR_RWLOCK |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|XIO_CREDENTIAL_RWLOCK |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|XIO_EDS_MGR_RWLOCK |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|XIO_EDS_RWLOCK |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|XIO_IOSTATS_BLOBLIST_RWLOCK |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|XIO_IOSTATS_FCBLIST_RWLOCK |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|XIO_LEASE_RENEW_MGR_RWLOCK |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|XTP_HOST_DB_COLLECTION |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|XTP_HOST_LOG_ACTIVITY |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|XTP_HOST_PARALLEL_RECOVERY |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|XTP_PREEMPTIVE_TASK |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|XTP_TRUNCATION_LSN |TBD <br /> **Se aplica a**: desde [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|XTPPROC_CACHE_ACCESS |Se produce al tener acceso a todos los objetos de caché de procedimiento almacenado compilado de forma nativa., <br /> **Se aplica a**: desde [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
|XTPPROC_PARTITIONED_STACK_CREATE |Tiene lugar cuando asignar de forma nativa por nodo NUMA compila las estructuras de memoria caché de procedimiento almacenado (se debe realizar un único subproceso) para un procedimiento determinado., <br /> **Se aplica a**: desde [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].|

  
 Los siguientes XEvents se relacionan con la partición **conmutador** y regeneración de índice en línea. Para obtener información sobre la sintaxis, vea [ALTER TABLE &#40;Transact-SQL&#41; ](../../t-sql/statements/alter-table-transact-sql.md) y [ALTER INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md).  
  
-   lock_request_priority_state  
  
-   process_killed_by_abort_blockers  
  
-   ddl_with_wait_at_low_priority  
  
 Para una matriz de compatibilidad de bloqueos, vea [sys.dm_tran_locks &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-tran-locks-transact-sql.md).  
  
## <a name="see-also"></a>Vea también  
    
 [Vistas de administración dinámica relacionadas con el sistema operativo SQL Server &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)   
 [sys.dm_exec_session_wait_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-session-wait-stats-transact-sql.md)   
 [sys.dm_db_wait_stats &#40;Azure SQL Database&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-wait-stats-azure-sql-database.md)  
  
  


