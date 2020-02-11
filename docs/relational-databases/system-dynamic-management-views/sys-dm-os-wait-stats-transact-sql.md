---
title: Sys. dm_os_wait_stats (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/19/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
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
author: MashaMSFT
ms.author: mathoma
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: f0abc089809e6b811f0ff64684bdaeed742ebcae
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "74190348"
---
# <a name="sysdm_os_wait_stats-transact-sql"></a>sys.dm_os_wait_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Devuelve información acerca de todas las esperas encontradas por los subprocesos ejecutados. Puede utilizar esta vista agregada para diagnosticar problemas de rendimiento con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y también con lotes y consultas específicos. [Sys. dm_exec_session_wait_stats &#40;&#41;de Transact-SQL](../../relational-databases/system-dynamic-management-views/sys-dm-exec-session-wait-stats-transact-sql.md) proporciona información similar por sesión.  
  
> [!NOTE] 
> Para llamar a este método desde ** [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] o [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] **, use el nombre **Sys. dm_pdw_nodes_os_wait_stats**.  
  
|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|wait_type|**nvarchar (60)**|Nombre del tipo de espera. Para obtener más información, vea [Tipos de esperas](#WaitTypes), más adelante en este tema.|  
|waiting_tasks_count|**BIGINT**|Número de esperas de este tipo de espera. Este recuento se incrementa al inicio de cada espera.|  
|wait_time_ms|**BIGINT**|Tiempo total de espera de este tipo en milisegundos. Este tiempo incluye el tiempo de signal_wait_time_ms.|  
|max_wait_time_ms|**BIGINT**|Tiempo de espera máximo de este tipo de espera.|  
|signal_wait_time_ms|**BIGINT**|Diferencia entre el momento en que se indicó el subproceso en espera y el momento en que empezó a ejecutarse.|  
|pdw_node_id|**int**|Identificador del nodo en el que se encuentra esta distribución. <br/> **Se aplica a**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)],[!INCLUDE[ssPDW](../../includes/sspdw-md.md)] |  
  
## <a name="permissions"></a>Permisos

En [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], requiere `VIEW SERVER STATE` el permiso.   
En [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] los niveles Premium, requiere el `VIEW DATABASE STATE` permiso en la base de datos. En [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] los niveles estándar y básico, requiere el **Administrador del servidor** o una cuenta de **Administrador de Azure Active Directory** .   

##  <a name="WaitTypes"></a>Tipos de esperas  
 **Esperas de recursos** Las esperas de recursos se producen cuando un trabajador solicita acceso a un recurso que no está disponible porque otro trabajador lo está utilizando o aún no está disponible. Algunos ejemplos de esperas de recursos son los bloqueos, bloqueos temporales y esperas de red y E/S de disco. Las esperas de bloqueos y bloqueos temporales son esperas en objetos de sincronización.  
  
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
  
 En [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , los contadores de tiempo de espera son valores **BIGINT** y, por tanto, no son tan propensos a la sustitución de contadores que los contadores equivalentes en versiones anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
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

|type |Descripción| 
|-------------------------- |--------------------------| 
|ABR |Solamente se identifica con fines informativos. No compatible. La compatibilidad con versiones posteriores no está garantizada.| | 
|AM_INDBUILD_ALLOCATION |Exclusivamente para uso interno. <br />**Válido para** : [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] y versiones posteriores.| 
|AM_SCHEMAMGR_UNSHARED_CACHE |Exclusivamente para uso interno. <br />**Válido para** : [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] y versiones posteriores.| 
|ASSEMBLY_FILTER_HASHTABLE |Exclusivamente para uso interno. <br />**Válido para** : [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] y versiones posteriores.| 
|ASSEMBLY_LOAD |Tiene lugar durante el acceso exclusivo a la carga de ensamblados.| 
|ASYNC_DISKPOOL_LOCK |Tiene lugar cuando existe un intento de sincronizar subprocesos paralelos que ejecutan tareas como la creación o la inicialización de un archivo.| 
|ASYNC_IO_COMPLETION |Tiene lugar cuando una tarea está esperando que finalice una operación de E/S.| 
|ASYNC_NETWORK_IO |Tiene lugar en escrituras en la red cuando la tarea se bloquea tras la red. Comprueba que el cliente procesa datos en el servidor.| 
|ASYNC_OP_COMPLETION |Exclusivamente para uso interno. <br />**Válido para** : [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] y versiones posteriores.| 
|ASYNC_OP_CONTEXT_READ |Exclusivamente para uso interno. <br />**Válido para** : [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] y versiones posteriores.| 
|ASYNC_OP_CONTEXT_WRITE |Exclusivamente para uso interno. <br />**Válido para** : [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] y versiones posteriores.| 
|ASYNC_SOCKETDUP_IO |Exclusivamente para uso interno. <br />**Válido para** : [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] y versiones posteriores.| 
|AUDIT_GROUPCACHE_LOCK |Tiene lugar cuando se produce una espera en un bloqueo que controla el acceso a una caché especial. La memoria caché contiene información acerca de las auditorías que se usan para auditar cada grupo de acciones de auditoría.| 
|AUDIT_LOGINCACHE_LOCK |Tiene lugar cuando se produce una espera en un bloqueo que controla el acceso a una caché especial. La memoria caché contiene información acerca de las auditorías que se usan para auditar los grupo de acciones de auditoría de inicio de sesión.| 
|AUDIT_ON_DEMAND_TARGET_LOCK |Tiene lugar cuando se produce una espera en un bloqueo que se usa para asegurar la inicialización única de destinos de Extended Events relacionados con las auditorías.| 
|AUDIT_XE_SESSION_MGR |Tiene lugar cuando se produce una espera en un bloqueo que se usa para sincronizar el inicio y la detención de sesiones de Extended Events relacionados con las auditorías.| 
|BACKUP |Tiene lugar cuando una tarea se bloquea como parte de un proceso de copia de seguridad.| 
|BACKUP_OPERATOR |Tiene lugar cuando una tarea está esperando a que se monte una cinta. Para ver el estado de la cinta, consulta sys.dm_io_backup_tapes. Si no hay pendiente ninguna operación de montaje, este tiempo de espera puede indicar un problema de hardware con la unidad de cinta.| 
|BACKUPBUFFER |Tiene lugar cuando una tarea de copia de seguridad espera por datos, o espera a un búfer donde se almacenarán datos. Este tipo no es normal, excepto cuando una tarea está esperando a que se monte una cinta.| 
|BACKUPIO |Tiene lugar cuando una tarea de copia de seguridad espera por datos, o espera a un búfer donde se almacenarán datos. Este tipo no es normal, excepto cuando una tarea está esperando a que se monte una cinta.| 
|BACKUPTHREAD |Tiene lugar cuando una tarea está esperando que finalice una tarea de copia de seguridad. Los tiempos de espera pueden ser largos, desde unos minutos a varias horas. Si la tarea que se está esperando está en un proceso de E/S, este tipo no indica ningún problema.| 
|BAD_PAGE_PROCESS |Tiene lugar cuando el registrador de páginas sospechosas en segundo plano intenta impedir la ejecución más veces que cada cinco segundos. Un exceso de páginas sospechosas provoca la ejecución frecuente del registrador.| 
|BLOB_METADATA |Exclusivamente para uso interno. <br />**Válido para** : [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] y versiones posteriores.| 
|BMPALLOCATION |Tiene lugar con planes en modo por lotes en paralelo al sincronizar la asignación de un filtro de mapa de bits grande. Si la espera es excesiva y no se puede reducir ajustando la consulta (por ejemplo, agregando índices), considere la posibilidad de ajustar el umbral de costo para paralelismo o de reducir el grado de paralelismo.<br />**Válido para** : [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] y versiones posteriores.| 
|BMPBUILD |Tiene lugar con planes en modo por lotes en paralelo al sincronizar la compilación de un filtro de mapa de bits grande. Si la espera es excesiva y no se puede reducir ajustando la consulta (por ejemplo, agregando índices), considere la posibilidad de ajustar el umbral de costo para paralelismo o de reducir el grado de paralelismo. <br />**Válido para** : [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] y versiones posteriores.| 
|BMPREPARTITION |Tiene lugar con planes en modo por lotes en paralelo al sincronizar la creación de particiones de un filtro de mapa de bits grande. Si la espera es excesiva y no se puede reducir ajustando la consulta (por ejemplo, agregando índices), considere la posibilidad de ajustar el umbral de costo para paralelismo o de reducir el grado de paralelismo. <br /> **Válido para** : [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] y versiones posteriores.| 
|BMPREPLICATION |Tiene lugar con planes en modo por lotes en paralelo al sincronizar la replicación de un filtro de mapa de bits grande entre subprocesos de trabajo. Si la espera es excesiva y no se puede reducir ajustando la consulta (por ejemplo, agregando índices), considere la posibilidad de ajustar el umbral de costo para paralelismo o de reducir el grado de paralelismo. <br /> **Válido para** : [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] y versiones posteriores.| 
|BPSORT |Tiene lugar con planes en modo por lotes en paralelo al sincronizar la ordenación de un DataSet entre varios subprocesos. Si la espera es excesiva y no se puede reducir ajustando la consulta (por ejemplo, agregando índices), considere la posibilidad de ajustar el umbral de costo para paralelismo o de reducir el grado de paralelismo. <br /> **Válido para** : [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] y versiones posteriores.| 
|BROKER_CONNECTION_RECEIVE_TASK |Tiene lugar cuando se espera el acceso para recibir un mensaje en el extremo de una conexión. El acceso de recepción al extremo está serializado.| 
|BROKER_DISPATCHER |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] y versiones posteriores.| 
|BROKER_ENDPOINT_STATE_MUTEX |Se produce cuando hay contención para tener acceso al estado de un extremo de conexión de Service Broker. El acceso al estado de los cambios está serializado.| 
|BROKER_EVENTHANDLER |Tiene lugar cuando una tarea está esperando en el controlador de eventos principal del Service Broker. Debería ocurrir brevemente.| 
|BROKER_FORWARDER |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] y versiones posteriores.| 
|BROKER_INIT |Se produce al inicializar Service Broker en cada base de datos activa. No debería ocurrir con frecuencia.| 
|BROKER_MASTERSTART |Tiene lugar cuando una tarea está esperando a que se inicie el controlador de eventos principal del Service Broker. Debería ocurrir brevemente.| 
|BROKER_RECEIVE_WAITFOR |Tiene lugar cuando RECEIVE WAITFOR está en espera. Esto puede significar que no hay ningún mensaje listo para recibirse en la cola o que una contención de bloqueo impide que reciba mensajes de la cola.| 
|BROKER_REGISTERALLENDPOINTS |Tiene lugar durante la inicialización de un extremo de conexión de Service Broker. Debería ocurrir brevemente.| 
|BROKER_SERVICE |Se produce cuando se actualiza o se vuelve a establecer la prioridad de la lista de destino de Service Broker asociada a un servicio de destino.| 
|BROKER_SHUTDOWN |Se produce cuando hay un cierre planeado de Service Broker. Debería ocurrir brevemente, si ocurre.| 
|BROKER_START |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] y versiones posteriores.| 
|BROKER_TASK_SHUTDOWN |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] y versiones posteriores.| 
|BROKER_TASK_STOP |Se produce cuando el controlador de tareas de cola de Service Broker intenta cerrar la tarea. La comprobación de estado se serializa y debe estar en estado de ejecución de antemano.| 
|BROKER_TASK_SUBMIT |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] y versiones posteriores.| 
|BROKER_TO_FLUSH |Se produce cuando el vaciador diferido de Service Broker vacía los objetos de transmisión en memoria en una tabla de trabajo.| 
|BROKER_TRANSMISSION_OBJECT |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] y versiones posteriores.| 
|BROKER_TRANSMISSION_TABLE |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] y versiones posteriores.| 
|BROKER_TRANSMISSION_WORK |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] y versiones posteriores.| 
|BROKER_TRANSMITTER |Se produce cuando el transmisor de Service Broker está esperando trabajo. Service Broker tiene un componente denominado transmisor que programa los mensajes de varios cuadros de diálogo que se van a enviar a través de la conexión a través de uno o varios puntos de conexión. El transmisor tiene dos subprocesos dedicados para este fin. Este tipo de espera se cobra cuando estos subprocesos de transmisor están esperando a que se envíen mensajes de diálogo con las conexiones de transporte. Los valores altos de waiting_tasks_count para este punto de tipo de espera son el trabajo intermitente de estos subprocesos de transmisor y no son indicaciones de ningún problema de rendimiento. Si Service Broker no se utiliza en absoluto, waiting_tasks_count debe ser 2 (para los dos subprocesos de transmisor) y wait_time_ms debe ser el doble de la duración desde el inicio de la instancia. Vea [estadísticas de espera de Service Broker](https://blogs.msdn.microsoft.com/sql_service_broker/2008/12/01/service-broker-wait-types).|
|BUILTIN_HASHKEY_MUTEX |Puede producirse después del inicio de una instancia, mientras se inicializan las estructuras de datos internas. No se producirá después de la inicialización de las estructuras de datos.| 
|CHANGE_TRACKING_WAITFORCHANGES |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] y versiones posteriores.| 
|CHECK_PRINT_RECORD |Solamente se identifica con fines informativos. No compatible. La compatibilidad con versiones posteriores no está garantizada.| 
|CHECK_SCANNER_MUTEX |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] y versiones posteriores.| 
|CHECK_TABLES_INITIALIZATION |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] y versiones posteriores.| 
|CHECK_TABLES_SINGLE_SCAN |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] y versiones posteriores.| 
|CHECK_TABLES_THREAD_BARRIER |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] y versiones posteriores.| 
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
|CMEMPARTITIONED |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] y versiones posteriores.| 
|CMEMTHREAD |Tiene lugar cuando una tarea está esperando en un objeto de memoria seguro para subprocesos. El tiempo de espera puede aumentar cuando existe una contención porque muchas tareas intentan asignar memoria desde el mismo objeto de memoria.| 
|COLUMNSTORE_BUILD_THROTTLE |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] y versiones posteriores.| 
|COLUMNSTORE_COLUMNDATASET_SESSION_LIST |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] y versiones posteriores.| 
|COMMIT_TABLE |Exclusivamente para uso interno.| 
|CONNECTION_ENDPOINT_LOCK |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] y versiones posteriores.| 
|COUNTRECOVERYMGR |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] y versiones posteriores.| 
|CREATE_DATINISERVICE |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] y versiones posteriores.| 
|CXCONSUMER |Tiene lugar con planes de consulta paralelos cuando un subproceso de consumidor espera a que un subproceso de productor envíe filas. Se trata de una parte normal de la ejecución de consultas en paralelo. <br /> **Se aplica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (a [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] partir de [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] SP2, CU3)[!INCLUDE[ssSDS](../../includes/sssds-md.md)]|
|CXPACKET |Tiene lugar con planes de consulta paralelos al sincronizar el iterador de intercambio del procesador de consultas y al generar y consumir filas. Si la espera es excesiva y no se puede reducir ajustando la consulta (por ejemplo, agregando índices), considere la posibilidad de ajustar el umbral de costo para paralelismo o de reducir el grado de paralelismo.<br /> **Nota:** A partir [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] de SP2 [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] , CU3 y [!INCLUDE[ssSDS](../../includes/sssds-md.md)], esperas cxpacket solo hace referencia a la sincronización del iterador de intercambio del procesador de consultas y a la generación de filas para los subprocesos de consumidor. Se realiza un seguimiento de los subprocesos de consumidor por separado en el tipo de espera CXCONSUMER.| 
|CXROWSET_SYNC |Tiene lugar durante un examen de intervalo en paralelo.| 
|DAC_INIT |Tiene lugar mientras se inicializa la conexión de administrador dedicada.| 
|DBCC_SCALE_OUT_EXPR_CACHE |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] y versiones posteriores.| 
|DBMIRROR_DBM_EVENT |Solamente se identifica con fines informativos. No compatible. La compatibilidad con versiones posteriores no está garantizada.| 
|DBMIRROR_DBM_MUTEX |Solamente se identifica con fines informativos. No compatible. La compatibilidad con versiones posteriores no está garantizada.| 
|DBMIRROR_EVENTS_QUEUE |Tiene lugar cuando la creación de reflejo de bases de datos espera que se procesen eventos.| 
|DBMIRROR_SEND |Tiene lugar cuando una tarea está esperando un trabajo acumulado de comunicaciones en el nivel de red para limpiar y poder enviar mensajes. Indica que el nivel de comunicaciones empieza a sobrecargarse y afecta al rendimiento de la creación del reflejo de los datos de la base de datos.| 
|DBMIRROR_WORKER_QUEUE |Indica que la tarea de trabajo de creación de reflejo de bases de datos está esperando más trabajo.| 
|DBMIRRORING_CMD |Tiene lugar cuando una tarea está esperando que los registros se guarden en el disco. Este estado de espera está previsto que dure largos periodos de tiempo.| 
|DBSEEDING_FLOWCONTROL |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] y versiones posteriores.| 
|DBSEEDING_OPERATION |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] y versiones posteriores.| 
|DEADLOCK_ENUM_MUTEX |Se produce cuando el monitor de interbloqueo y sys. dm_os_waiting_tasks intentan asegurarse de que SQL Server no ejecuta varias búsquedas de interbloqueo al mismo tiempo.| 
|DEADLOCK_TASK_SEARCH |Un tiempo de espera largo en este recurso indica que el servidor está ejecutando consultas por encima de sys.dm_os_waiting_tasks y que estas consultas impiden que la supervisión de interbloqueos ejecute la búsqueda de interbloqueos. Este tipo de espera solo lo utiliza el supervisor de interbloqueos. Las consultas por encima de sys.dm_os_waiting_tasks utilizan DEADLOCK_ENUM_MUTEX.| 
|DEBUG |Tiene lugar durante la depuración de Transact-SQL y CLR para la sincronización interna.| 
|DIRECTLOGCONSUMER_LIST |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] y versiones posteriores.| 
|DIRTY_PAGE_POLL |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] y versiones posteriores.| 
|DIRTY_PAGE_SYNC |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] y versiones posteriores.| 
|DIRTY_PAGE_TABLE_LOCK |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] y versiones posteriores.| 
|DISABLE_VERSIONING |Se produce cuando SQL Server sondea el administrador de transacciones de versión para ver si la marca de tiempo de la transacción activa más temprana es posterior a la marca de tiempo de cuando el Estado empezó a cambiar. Si es así, todas las transacciones de instantáneas que se iniciaron antes de ejecutar la instrucción ALTER DATABASE han finalizado. Este estado de espera se utiliza cuando SQL Server deshabilita el control de versiones mediante la instrucción ALTER DATABASE.| 
|DISKIO_SUSPEND |Tiene lugar cuando una tarea está esperando tener acceso a un archivo cuando está activa una copia de seguridad externa. Se notifica para cada proceso de usuario en espera. Un recuento mayor de cinco procesos por usuario puede indicar que la copia de seguridad externa tarda mucho en finalizarse.| 
|DISPATCHER_PRIORITY_QUEUE_SEMAPHORE |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] y versiones posteriores.| 
|DISPATCHER_QUEUE_SEMAPHORE |Tiene lugar cuando un subproceso del grupo de distribuidores espera más trabajo para su procesamiento. Se prevé que el tiempo de espera de este tipo de espera aumente cuando el distribuidor esté inactivo.| 
|DLL_LOADING_MUTEX |Tiene lugar una vez mientras se espera que se cargue la DLL del analizador XML.| 
|DPT_ENTRY_LOCK |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] y versiones posteriores.| 
|DROP_DATABASE_TIMER_TASK |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] y versiones posteriores.| 
|DROPTEMP |Tiene lugar entre intentos para quitar un objeto temporal si se produjo un error en el intento anterior. La duración de la espera crece de forma exponencial en cada intento de eliminación con error.| 
|DTC |Tiene lugar cuando una tarea está esperando en un evento que se utiliza para administrar la transición de estado. Este estado controla cuándo se produce la recuperación de transacciones de Microsoft Coordinador de transacciones distribuidas (MS DTC) después de que SQL Server reciba la notificación de que el servicio MS DTC ha dejado de estar disponible.| 
|DTC_ABORT_REQUEST |Tiene lugar en una sesión del trabajador de MS DTC cuando la sesión espera a tener la propiedad de una transacción de MS DTC. Después de que MS DTC es propietario de la transacción, la sesión puede revertir la transacción. Generalmente, la sesión esperará a otra sesión que esté utilizando la transacción.| 
|DTC_RESOLVE |Tiene lugar cuando una tarea de recepción espera a la base de datos maestra en una transacción entre bases de datos por lo que la tarea puede consultar el resultado de la transacción.| 
|DTC_STATE |Tiene lugar cuando una tarea está esperando en un evento que protege los cambios al objeto de estado global de MS DTC. Este estado debe mantenerse durante periodos muy cortos.| 
|DTC_TMDOWN_REQUEST |Se produce en una sesión de trabajador de MS DTC cuando SQL Server recibe una notificación de que el servicio MS DTC no está disponible. Primero, el trabajador esperará a que se inicie el proceso de recepción de MS DTC. A continuación, el trabajador espera a obtener el resultado de la transacción distribuida en la que está trabajando. Esto puede continuar hasta que se restablezca la conexión con el servicio de MS DTC.| 
|DTC_WAITFOR_OUTCOME |Tiene lugar cuando las tareas de recepción esperan a que MS DTC se vuelva a activar para habilitar la resolución de las transacciones preparadas.| 
|DTCNEW_ENLIST |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] y versiones posteriores.| 
|DTCNEW_PREPARE |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] y versiones posteriores.| 
|DTCNEW_RECOVERY |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] y versiones posteriores.| 
|DTCNEW_TM |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] y versiones posteriores.| 
|DTCNEW_TRANSACTION_ENLISTMENT |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] y versiones posteriores.| 
|DTCPNTSYNC |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] y versiones posteriores.| 
|DUMP_LOG_COORDINATOR |Tiene lugar cuando una tarea principal espera que una subtarea genere datos. Normalmente, este estado no tiene lugar. Una espera larga indica un bloqueo inesperado. La subtarea debe investigarse.| 
|DUMP_LOG_COORDINATOR_QUEUE |Exclusivamente para uso interno.| 
|DUMPTRIGGER |Solamente se identifica con fines informativos. No compatible. La compatibilidad con versiones posteriores no está garantizada.| 
|EC |Solamente se identifica con fines informativos. No compatible. La compatibilidad con versiones posteriores no está garantizada.| 
|EE_PMOLOCK |Tiene lugar durante la sincronización de determinados tipos de asignaciones de memoria durante la ejecución de instrucciones.| 
|EE_SPECPROC_MAP_INIT |Tiene lugar durante la sincronización de la creación de una tabla hash de procedimiento interna. Esta espera solo puede producirse durante el acceso inicial de la tabla hash después de que se inicie la instancia de SQL Server.| 
|ENABLE_EMPTY_VERSIONING |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] y versiones posteriores.| 
|ENABLE_VERSIONING |Se produce cuando SQL Server espera a que finalicen todas las transacciones de actualización de esta base de datos antes de declarar la base de datos lista para pasar al estado permitido de aislamiento de instantánea. Este estado se utiliza cuando SQL Server habilita el aislamiento de instantáneas mediante la instrucción ALTER DATABASE.| 
|ERROR_REPORTING_MANAGER |Tiene lugar durante la sincronización de múltiples inicializaciones simultáneas de registros de errores.| 
|EXCHANGE |Tiene lugar en la sincronización en el iterador de intercambios del procesador de consultas, durante consultas en paralelo.| 
|EXECSYNC |Tiene lugar durante consultas en paralelo mientras se sincroniza en el procesador de consultas en áreas no relacionadas con el iterador de intercambios. Algunos ejemplos de estas áreas son mapas de bits, objetos binarios grandes (LOB) y el iterador de spool. Los LOB pueden utilizar con frecuencia este estado de espera.| 
|EXECUTION_PIPE_EVENT_INTERNAL |Tiene lugar durante la sincronización entre las partes productor y consumidor de la ejecución por lotes que se envían a través del contexto de conexión.| 
|EXTERNAL_RG_UPDATE |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] y versiones posteriores.| 
|EXTERNAL_SCRIPT_NETWORK_IO |Exclusivamente para uso interno. <br /> **Se aplica a**: [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] hasta el actual.| 
|EXTERNAL_SCRIPT_PREPARE_SERVICE |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] y versiones posteriores.| 
|EXTERNAL_SCRIPT_SHUTDOWN |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] y versiones posteriores.| 
|EXTERNAL_WAIT_ON_LAUNCHER, |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] y versiones posteriores.| 
|FABRIC_HADR_TRANSPORT_CONNECTION |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] y versiones posteriores.| 
|FABRIC_REPLICA_CONTROLLER_LIST |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] y versiones posteriores.| 
|FABRIC_REPLICA_CONTROLLER_STATE_AND_CONFIG |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] y versiones posteriores.| 
|FABRIC_REPLICA_PUBLISHER_EVENT_PUBLISH |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] y versiones posteriores.| 
|FABRIC_REPLICA_PUBLISHER_SUBSCRIBER_LIST |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] y versiones posteriores.| 
|FABRIC_WAIT_FOR_BUILD_REPLICA_EVENT_PROCESSING |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] y versiones posteriores.| 
|FAILPOINT |Solamente se identifica con fines informativos. No compatible. La compatibilidad con versiones posteriores no está garantizada.| 
|FCB_REPLICA_READ |Tiene lugar cuando se sincronizan las lecturas de un archivo disperso de instantáneas (o una instantánea temporal creada por DBCC).| 
|FCB_REPLICA_WRITE |Tiene lugar cuando se sincroniza la inserción o extracción de una página en un archivo disperso de instantáneas (o en una instantánea temporal creada por DBCC).| 
|FEATURE_SWITCHES_UPDATE |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] y versiones posteriores.| 
|FFT_NSO_DB_KILL_FLAG |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] y versiones posteriores.| 
|FFT_NSO_DB_LIST |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] y versiones posteriores.| 
|FFT_NSO_FCB |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] y versiones posteriores.| 
|FFT_NSO_FCB_FIND |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] y versiones posteriores.| 
|FFT_NSO_FCB_PARENT |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] y versiones posteriores.| 
|FFT_NSO_FCB_RELEASE_CACHED_ENTRIES |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] y versiones posteriores.| 
|FFT_NSO_FCB_STATE |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] y versiones posteriores.| 
|FFT_NSO_FILEOBJECT |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] y versiones posteriores.| 
|FFT_NSO_TABLE_LIST |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] y versiones posteriores.| 
|FFT_NTFS_STORE |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] y versiones posteriores.| 
|FFT_RECOVERY |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] y versiones posteriores.| 
|FFT_RSFX_COMM |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] y versiones posteriores.| 
|FFT_RSFX_WAIT_FOR_MEMORY |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] y versiones posteriores.| 
|FFT_STARTUP_SHUTDOWN |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] y versiones posteriores.| 
|FFT_STORE_DB |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] y versiones posteriores.| 
|FFT_STORE_ROWSET_LIST |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] y versiones posteriores.| 
|FFT_STORE_TABLE |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] y versiones posteriores.| 
|FILE_VALIDATION_THREADS |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] y versiones posteriores.| 
|FILESTREAM_CACHE |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] y versiones posteriores.| 
|FILESTREAM_CHUNKER |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] y versiones posteriores.| 
|FILESTREAM_CHUNKER_INIT |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] y versiones posteriores.| 
|FILESTREAM_FCB |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] y versiones posteriores.| 
|FILESTREAM_FILE_OBJECT |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] y versiones posteriores.| 
|FILESTREAM_WORKITEM_QUEUE |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] y versiones posteriores.| 
|FILETABLE_SHUTDOWN |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] y versiones posteriores.| 
|FOREIGN_REDO |Exclusivamente para uso interno. <br /> **Se aplica a**: [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] hasta el actual.| 
|FORWARDER_TRANSITION |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] y versiones posteriores.| 
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
|FT_MASTER_MERGE_COORDINATOR |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] y versiones posteriores.| 
|FT_METADATA_MUTEX |Solamente se documenta con fines informativos. No compatible. La compatibilidad con versiones posteriores no está garantizada.| 
|FT_PROPERTYLIST_CACHE |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] y versiones posteriores.| 
|FT_RESTART_CRAWL |Tiene lugar cuando un rastreo de texto completo debe reiniciarse desde el último punto correcto conocido para recuperarse de un error transitorio. La espera permite que completen o abandonen el paso actual las tareas del trabajador que se están ejecutando en dicho rellenado.| 
|FULLTEXT GATHERER |Tiene lugar durante la sincronización de operaciones de texto completo.| 
|GDMA_GET_RESOURCE_OWNER |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] y versiones posteriores.| 
|GHOSTCLEANUP_UPDATE_STATS |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] y versiones posteriores.| 
|GHOSTCLEANUPSYNCMGR |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] y versiones posteriores.| 
|GLOBAL_QUERY_CANCEL |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] y versiones posteriores.| 
|GLOBAL_QUERY_CLOSE |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] y versiones posteriores.| 
|GLOBAL_QUERY_CONSUMER |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] y versiones posteriores.| 
|GLOBAL_QUERY_PRODUCER |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] y versiones posteriores.| 
|GLOBAL_TRAN_CREATE |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] y versiones posteriores.| 
|GLOBAL_TRAN_UCS_SESSION |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] y versiones posteriores.| 
|GUARDIAN |Solamente se identifica con fines informativos. No compatible. La compatibilidad con versiones posteriores no está garantizada.| 
|HADR_AG_MUTEX |Se produce cuando una Always On instrucción DDL o un comando de clústeres de conmutación por error de Windows Server está esperando el acceso exclusivo de lectura y escritura a la configuración de un grupo de disponibilidad. <br /> **Válido para** : [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] y versiones posteriores.| 
|HADR_AR_CRITICAL_SECTION_ENTRY |Se produce cuando una Always On instrucción DDL o un comando de clústeres de conmutación por error de Windows Server está esperando el acceso exclusivo de lectura y escritura al estado de tiempo de ejecución de la réplica local del grupo de disponibilidad asociado. <br /> **Válido para** : [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] y versiones posteriores.| 
|HADR_AR_MANAGER_MUTEX |Se produce cuando el cierre de la réplica de disponibilidad espera a que el inicio se complete o cuando un inicio de una réplica de disponibilidad espera a que el cierre se complete. Solo para uso interno., <br /> **Válido para** : [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] y versiones posteriores.| 
|HADR_AR_UNLOAD_COMPLETED |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] y versiones posteriores.| 
|HADR_ARCONTROLLER_NOTIFICATIONS_SUBSCRIBER_LIST |El publicador de un evento de réplica de disponibilidad (como un cambio de estado o de configuración) espera a un acceso de lectura/escritura exclusivo a la lista de suscriptores de evento. Solo para uso interno., <br /> **Válido para** : [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] y versiones posteriores.| 
|HADR_BACKUP_BULK_LOCK |La base de datos principal Always On recibió una solicitud de copia de seguridad de una base de datos secundaria y está esperando a que el subproceso en segundo plano termine de procesar la solicitud al adquirir o liberar el bloqueo BulkOp. <br /> **Válido para** : [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] y versiones posteriores.| 
|HADR_BACKUP_QUEUE |El subproceso en segundo plano de reserva de la base de datos principal Always On está esperando una nueva solicitud de trabajo de la base de datos secundaria. (normalmente, esto ocurre cuando la base de datos principal contiene el registro BulkOp y está esperando a que la base de datos secundaria indique que la base de datos principal puede liberar el bloqueo). <br /> **Válido para** : [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] y versiones posteriores.| 
|HADR_CLUSAPI_CALL |Un subproceso de SQL Server está a la espera de cambiar del modo no preferente (programado por SQL Server) al modo preferente (programado por el sistema operativo) para invocar las API de clústeres de conmutación por error de Windows Server. <br /> **Válido para** : [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] y versiones posteriores.| 
|HADR_COMPRESSED_CACHE_SYNC |Esperando el acceso a la caché de bloques de registro comprimidos que se usa para evitar la compresión redundante de los bloques de registro enviados a varias bases de datos secundarias. <br /> **Válido para** : [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] y versiones posteriores.| 
|HADR_CONNECTIVITY_INFO |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] y versiones posteriores.| 
|HADR_DATABASE_FLOW_CONTROL |En espera de que se envíen mensajes al asociado cuando se ha alcanzado el número máximo de mensajes en cola. Indica que los exámenes del registro se ejecutan más rápidamente de lo que la red necesita. Esto es un problema solo si los envíos de red son más lentos de lo esperado. <br /> **Válido para** : [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] y versiones posteriores.| 
|HADR_DATABASE_VERSIONING_STATE |Se produce en el cambio de estado de control de versiones de una base de datos secundaria Always On. Esta espera es para las estructuras de datos internas y suele ser muy breve sin ningún efecto directo sobre el acceso a los datos. <br /> **Válido para** : [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] y versiones posteriores.| 
|HADR_DATABASE_WAIT_FOR_RECOVERY |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] y versiones posteriores.| 
|HADR_DATABASE_WAIT_FOR_RESTART |Esperando a que la base de datos se reinicie en Always On control de grupos de disponibilidad. En condiciones normales, esto no es un problema del cliente porque se esperan esperas aquí. <br /> **Válido para** : [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] y versiones posteriores.| 
|HADR_DATABASE_WAIT_FOR_TRANSITION_TO_VERSIONING |Una consulta en los objetos de una base de datos secundaria legible de un grupo de disponibilidad de Always On se bloquea en las versiones de fila mientras se espera la confirmación o la reversión de todas las transacciones que estaban en curso cuando la réplica secundaria estaba habilitada para cargas de trabajo de lectura. Este tipo de espera garantiza que las versiones de fila están disponibles antes de la ejecución de una consulta en aislamiento de instantánea. <br /> **Válido para** : [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] y versiones posteriores.| 
|HADR_DB_COMMAND |Esperando respuestas a los mensajes de conversación (que requieren una respuesta explícita del otro lado, mediante el Always On infraestructura de mensajes de conversación). Varios tipos de mensajes diferentes usan este tipo de espera. <br /> **Válido para** : [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] y versiones posteriores.| 
|HADR_DB_OP_COMPLETION_SYNC |Esperando respuestas a los mensajes de conversación (que requieren una respuesta explícita del otro lado, mediante el Always On infraestructura de mensajes de conversación). Varios tipos de mensajes diferentes usan este tipo de espera. <br /> **Válido para** : [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] y versiones posteriores.| 
|HADR_DB_OP_START_SYNC |Una Always On instrucción DDL o un comando de clústeres de conmutación por error de Windows Server está esperando el acceso serializado a una base de datos de disponibilidad y su estado en tiempo de ejecución. <br /> **Válido para** : [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] y versiones posteriores.| 
|HADR_DBR_SUBSCRIBER |El publicador de un evento de réplica de disponibilidad (como un cambio de estado o de configuración) espera a un acceso de lectura/escritura exclusivo al estado de runtime de un suscriptor de evento que se corresponda con una base de datos de disponibilidad. Solo para uso interno., <br /> **Válido para** : [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] y versiones posteriores.| 
|HADR_DBR_SUBSCRIBER_FILTER_LIST |El publicador de un evento de réplica de disponibilidad (como un cambio de estado o de configuración) espera a un acceso de lectura/escritura exclusivo a la lista de suscriptores de evento que se corresponda con las bases de datos de disponibilidad. Solo para uso interno., <br /> **Válido para** : [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] y versiones posteriores.| 
|HADR_DBSEEDING |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] y versiones posteriores.| 
|HADR_DBSEEDING_LIST |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] y versiones posteriores.| 
|HADR_DBSTATECHANGE_SYNC |La espera del control de simultaneidad para actualizar el estado interno de la réplica de base de datos. <br /> **Válido para** : [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] y versiones posteriores.| 
|HADR_FABRIC_CALLBACK |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] y versiones posteriores.| 
|HADR_FILESTREAM_BLOCK_FLUSH |El administrador de transporte Always On FILESTREAM está esperando hasta que finalice el procesamiento de un bloque de registro. <br /> **Válido para** : [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] y versiones posteriores.| 
|HADR_FILESTREAM_FILE_CLOSE |El administrador de transporte de Always On FILESTREAM espera hasta que se procesa el siguiente archivo FILESTREAM y se cierra su identificador. <br /> **Válido para** : [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] y versiones posteriores.| 
|HADR_FILESTREAM_FILE_REQUEST |Una réplica secundaria Always On está esperando a que la réplica principal Envíe todos los archivos FILESTREAM solicitados durante la operación de deshacer. <br /> **Válido para** : [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] y versiones posteriores.| 
|HADR_FILESTREAM_IOMGR |El administrador de transporte de FILESTREAM Always On está esperando el bloqueo de R/W que protege el administrador de e/s de FILESTREAM Always On durante el inicio o el apagado. <br /> **Válido para** : [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] y versiones posteriores.| 
|HADR_FILESTREAM_IOMGR_IOCOMPLETION |El administrador de e/s de FILESTREAM Always On está esperando la finalización de e/s. <br /> **Válido para** : [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] y versiones posteriores.| 
|HADR_FILESTREAM_MANAGER |El administrador de transporte de Always On FILESTREAM está esperando el bloqueo de R/W que protege el administrador de transporte de FILESTREAM Always On durante el inicio o el apagado. <br /> **Válido para** : [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] y versiones posteriores.| 
|HADR_FILESTREAM_PREPROC |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] y versiones posteriores.| 
|HADR_GROUP_COMMIT |El procesamiento de la confirmación de la transacción está esperando para permitir la confirmación de un grupo de modo que se puedan poner varios registros del registro de confirmación en un solo bloque de registros. Esta espera es una condición esperada que optimiza las operaciones de e/s de registro, captura y envío. <br /> **Válido para** : [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] y versiones posteriores.| 
|HADR_LOGCAPTURE_SYNC |El control de simultaneidad alrededor del objeto de aplicación o de la captura de registro al crear o destruir exámenes. Se trata de una espera esperada cuando los asociados cambian el estado o el estado de la conexión. <br /> **Válido para** : [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] y versiones posteriores.| 
|HADR_LOGCAPTURE_WAIT |En espera de que los registros estén disponibles. Puede ocurrir al esperar a que las conexiones generen nuevos registros o a que se complete la entrada/salida al leer un registro que no está en la memoria caché. Se trata de una espera esperada si el examen del registro se detecta hasta el final del registro o si está leyendo desde el disco. <br /> **Válido para** : [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] y versiones posteriores.| 
|HADR_LOGPROGRESS_SYNC |La espera del control de simultaneidad al actualizar el estado de progreso del registro de las réplicas de base de datos. <br /> **Válido para** : [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] y versiones posteriores.| 
|HADR_NOTIFICATION_DEQUEUE |Una tarea en segundo plano que procesa las notificaciones de Clústeres de conmutación por error de Windows Server está esperando la siguiente notificación. Solo para uso interno., <br /> **Válido para** : [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] y versiones posteriores.| 
|HADR_NOTIFICATION_WORKER_EXCLUSIVE_ACCESS |El administrador de réplicas de disponibilidad Always On está esperando el acceso serializado al estado en tiempo de ejecución de una tarea en segundo plano que procesa las notificaciones de clústeres de conmutación por error de Windows Server. Solo para uso interno., <br /> **Válido para** : [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] y versiones posteriores.| 
|HADR_NOTIFICATION_WORKER_STARTUP_SYNC |Una tarea en segundo plano está esperando a que se complete el inicio de una tarea en segundo plano que procesa las notificaciones de Clústeres de conmutación por error de Windows Server. Solo para uso interno., <br /> **Válido para** : [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] y versiones posteriores.| 
|HADR_NOTIFICATION_WORKER_TERMINATION_SYNC |Una tarea en segundo plano está esperando a que se termine una tarea en segundo plano que procesa las notificaciones de Clústeres de conmutación por error de Windows Server. Solo para uso interno., <br /> **Válido para** : [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] y versiones posteriores.| 
|HADR_PARTNER_SYNC |La espera del control de simultaneidad en la lista de socios comerciales. <br /> **Válido para** : [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] y versiones posteriores.| 
|HADR_READ_ALL_NETWORKS |En espera para obtener acceso de lectura o escritura a la lista de redes WSFC. Exclusivamente para uso interno. Nota: el motor mantiene una lista de redes de WSFC que se utiliza en las vistas de administración dinámica (como sys. dm_hadr_cluster_networks) o para validar Always On instrucciones Transact-SQL que hacen referencia a información de red de WSFC. Esta lista se actualiza tras el inicio del motor, las notificaciones relacionadas con WSFC y el reinicio de Always On interno (por ejemplo, la pérdida y la reobtención del cuórum de WSFC). Normalmente, las tareas se bloquearán cuando una actualización de esa lista esté en curso. , <br /> **Válido para** : [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] y versiones posteriores.| 
|HADR_RECOVERY_WAIT_FOR_CONNECTION |En espera de que la base de datos secundaria se conecte a la principal antes de realizar la recuperación. Se trata de una espera esperada, que puede alargarse si la conexión a la principal es lenta para establecerla. <br /> **Válido para** : [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] y versiones posteriores.| 
|HADR_RECOVERY_WAIT_FOR_UNDO |La recuperación de la base de datos espera a que la base de datos secundaria finalice la fase de reversión e inicialización para traerla de nuevo al punto de registro común con la base de datos principal. Se trata de una espera esperada después de las conmutaciones por error. Se puede realizar un seguimiento del progreso mediante el monitor de sistema de Windows (Perfmon. exe) y las vistas de administración dinámica. <br /> **Válido para** : [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] y versiones posteriores.| 
|HADR_REPLICAINFO_SYNC |Esperar a que el control de simultaneidad actualice el estado de la réplica actual. <br /> **Válido para** : [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] y versiones posteriores.| 
|HADR_SEEDING_CANCELLATION |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] y versiones posteriores.| 
|HADR_SEEDING_FILE_LIST |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] y versiones posteriores.| 
|HADR_SEEDING_LIMIT_BACKUPS |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] y versiones posteriores.| 
|HADR_SEEDING_SYNC_COMPLETION |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] y versiones posteriores.| 
|HADR_SEEDING_TIMEOUT_TASK |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] y versiones posteriores.| 
|HADR_SEEDING_WAIT_FOR_COMPLETION |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] y versiones posteriores.| 
|HADR_SYNC_COMMIT |En espera del procesamiento de confirmación de transacciones para las bases de datos secundarias sincronizadas para reforzar el registro. Esta espera también se refleja en el contador de rendimiento Retraso de transacción. Este tipo de espera se espera para los grupos de disponibilidad sincronizados e indica el tiempo que se debe enviar, escribir y confirmar el registro en las bases de datos secundarias. <br /> **Válido para** : [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] y versiones posteriores.| 
|HADR_SYNCHRONIZING_THROTTLE |En espera para que el proceso de confirmación de transacciones permita a una base de datos secundaria ponerse al día con la principal al final del registro para pasar al estado sincronizado. Se trata de una espera esperada cuando una base de datos secundaria se pone al día. <br /> **Válido para** : [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] y versiones posteriores.| 
|HADR_TDS_LISTENER_SYNC |Tanto el sistema Always On interno como el clúster de WSFC solicitarán que los agentes de escucha se inicien o se detengan. El proceso de esta solicitud siempre es asíncrono y hay un mecanismo para quitar las solicitudes redundantes. También hay momentos en que este proceso se suspende debido a los cambios en la configuración. Todas las esperas relacionadas con este mecanismo de sincronización del agente de escucha usan este tipo de espera. Solo para uso interno., <br /> **Válido para** : [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] y versiones posteriores.| 
|HADR_TDS_LISTENER_SYNC_PROCESSING |Se usa al final de una Always On instrucción de Transact-SQL que requiere el inicio o la detención de un agente de escucha del grupo de disponibilidad. Dado que la operación de inicio y detención se realiza de forma asincrónica, el subproceso de usuario se bloqueará con este tipo de espera hasta que se conozca la situación del agente de escucha. <br /> **Válido para** : [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] y versiones posteriores.| 
|HADR_THROTTLE_LOG_RATE_GOVERNOR |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] y versiones posteriores.| 
|HADR_THROTTLE_LOG_RATE_MISMATCHED_SLO | Tiene lugar cuando una réplica secundaria de replicación geográfica se configura con un menor tamaño de proceso (SLO inferior) que la principal. Una base de datos principal está limitada debido al consumo de registro retrasado por parte de la secundaria. Esto se debe a que la base de datos secundaria tiene una capacidad de proceso insuficiente para mantenerse al día de la tasa de cambio de la base de datos principal. <br /> **Se aplica a**: Azure SQL Database| 
|HADR_THROTTLE_LOG_RATE_LOG_SIZE |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] y versiones posteriores.| 
|HADR_THROTTLE_LOG_RATE_SEEDING |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] y versiones posteriores.| 
|HADR_THROTTLE_LOG_RATE_SEND_RECV_QUEUE_SIZE |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] y versiones posteriores.| 
|HADR_TIMER_TASK |En espera de obtener el bloqueo en el objeto de tarea de temporizador y se usa también para las esperas reales entre los momentos en que el trabajo se realiza. Por ejemplo, para una tarea que se ejecuta cada 10 segundos, después de una ejecución, Always On grupos de disponibilidad espera unos 10 segundos para volver a programar la tarea y la espera se incluye aquí. <br /> **Válido para** : [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] y versiones posteriores.| 
|HADR_TRANSPORT_DBRLIST |En espera para acceder a la lista de réplicas de bases de datos de la capa de transporte. Se usa para el Spinlock que concede acceso a él. <br /> **Válido para** : [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] y versiones posteriores.| 
|HADR_TRANSPORT_FLOW_CONTROL |En espera cuando el número de mensajes de Always On no confirmados pendientes está por encima del umbral de control de flujo de salida. Esto se basa en una réplica de disponibilidad a réplica (no de base de datos a base de datos). <br /> **Válido para** : [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] y versiones posteriores.| 
|HADR_TRANSPORT_SESSION |Always On grupos de disponibilidad está esperando mientras cambia o tiene acceso al estado de transporte subyacente. <br /> **Válido para** : [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] y versiones posteriores.| 
|HADR_WORK_POOL |La espera del control de simultaneidad en el objeto de tarea de trabajo en segundo plano grupos de disponibilidad de Always On. <br /> **Válido para** : [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] y versiones posteriores.| 
|HADR_WORK_QUEUE |Always On el subproceso de trabajo en segundo plano de los grupos de disponibilidad a la espera de que se asigne nuevo trabajo. Se trata de una espera esperada cuando hay trabajadores listos en espera de un nuevo trabajo, que es el estado normal. <br /> **Válido para** : [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] y versiones posteriores.| 
|HADR_XRF_STACK_ACCESS |Acceso (búsqueda, adición y eliminación) de la pila de bifurcación de recuperación extendida para una base de datos de disponibilidad de Always On. <br /> **Válido para** : [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] y versiones posteriores.| 
|HCCO_CACHE |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] y versiones posteriores.| 
|HK_RESTORE_FILEMAP |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] y versiones posteriores.| 
|HKCS_PARALLEL_MIGRATION |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] y versiones posteriores.| 
|HKCS_PARALLEL_RECOVERY |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] y versiones posteriores.| 
|HTBUILD |Tiene lugar con planes en modo por lotes en paralelo al sincronizar la compilación de la tabla hash en el lado de entrada de una combinación o agregación hash. Si la espera es excesiva y no se puede reducir ajustando la consulta (por ejemplo, agregando índices), considere la posibilidad de ajustar el umbral de costo para paralelismo o de reducir el grado de paralelismo. <br /> **Válido para** : [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] y versiones posteriores.| 
|HTDELETE |Tiene lugar con planes en modo por lotes en paralelo al sincronizar al final de una combinación o agregación hash. Si la espera es excesiva y no se puede reducir ajustando la consulta (por ejemplo, agregando índices), considere la posibilidad de ajustar el umbral de costo para paralelismo o de reducir el grado de paralelismo. <br /> **Válido para** : [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] y versiones posteriores.| 
|HTMEMO |Tiene lugar con planes en modo por lotes en paralelo al sincronizar antes de examinar la tabla hash para generar coincidencias o no coincidencias en la combinación o agregación hash. Si la espera es excesiva y no se puede reducir ajustando la consulta (por ejemplo, agregando índices), considere la posibilidad de ajustar el umbral de costo para paralelismo o de reducir el grado de paralelismo. <br /> **Válido para** : [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] y versiones posteriores.| 
|HTREINIT |Tiene lugar con planes en modo por lotes en paralelo al sincronizar antes de restablecer una combinación o agregación hash para la siguiente combinación parcial. Si la espera es excesiva y no se puede reducir ajustando la consulta (por ejemplo, agregando índices), considere la posibilidad de ajustar el umbral de costo para paralelismo o de reducir el grado de paralelismo. <br /> **Válido para** : [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] y versiones posteriores.| 
|HTREPARTITION |Tiene lugar con planes en modo por lotes en paralelo al sincronizar la creación de particiones de la tabla hash en el lado de entrada de una combinación o agregación hash. Si la espera es excesiva y no se puede reducir ajustando la consulta (por ejemplo, agregando índices), considere la posibilidad de ajustar el umbral de costo para paralelismo o de reducir el grado de paralelismo.<br /> **Válido para** : [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] y versiones posteriores.| 
|HTTP_ENUMERATION |Tiene lugar en el inicio para enumerar los extremos HTTP al iniciar HTTP.| 
|HTTP_START |Tiene lugar cuando una conexión espera hasta que HTTP complete la inicialización.| 
|HTTP_STORAGE_CONNECTION |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] y versiones posteriores.| 
|IMPPROV_IOWAIT |Se produce cuando SQL Server espera a que finalice una e/s de carga masiva.| 
|INSTANCE_LOG_RATE_GOVERNOR |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] y versiones posteriores.| 
|INTERNAL_TESTING |Solamente se identifica con fines informativos. No compatible. La compatibilidad con versiones posteriores no está garantizada.| 
|IO_AUDIT_MUTEX |Tiene lugar durante la sincronización de búferes de eventos de seguimiento.| 
|IO_COMPLETION |Tiene lugar mientras se espera la finalización de operaciones de E/S. Generalmente, este tipo de espera representa operaciones de E/S de páginas que no son de datos. Las esperas de finalización de e/s de\_ \* la página de datos aparecen como esperas PAGEIOLATCH.| 
|IO_QUEUE_LIMIT |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] y versiones posteriores.| 
|IO_RETRY |Tiene lugar cuando una operación de E/S como una lectura o una escritura de disco no se realiza correctamente debido a un número insuficiente de recursos y, posteriormente, se vuelve a intentar.| 
|IOAFF_RANGE_QUEUE |Solamente se identifica con fines informativos. No compatible. La compatibilidad con versiones posteriores no está garantizada.| 
|KSOURCE_WAKEUP |Se utiliza en la tarea de control de servicios mientras se esperan solicitudes del Administrador de control de servicios. Se prevén esperas largas que no indican ningún problema.| 
|KTM_ENLISTMENT |Solamente se identifica con fines informativos. No compatible. La compatibilidad con versiones posteriores no está garantizada.| 
|KTM_RECOVERY_MANAGER |Solamente se identifica con fines informativos. No compatible. La compatibilidad con versiones posteriores no está garantizada.| 
|KTM_RECOVERY_RESOLUTION |Solamente se identifica con fines informativos. No compatible. La compatibilidad con versiones posteriores no está garantizada.| 
|LATCH_DT |Tiene lugar cuando se espera un bloqueo temporal de destrucción (DT). No incluye bloqueos temporales de búfer ni de marca de transacción. Hay disponible una lista\_ \* de esperas de bloqueos temporales en sys. dm_os_latch_stats. Tenga en cuenta que los grupos LATCH_NL, LATCH_SH, LATCH_UP, LATCH_EX y LATCH_DT de sys.dm_os_latch_stats esperan juntos.| 
|LATCH_EX |Tiene lugar cuando se espera un bloqueo temporal exclusivo (EX). No incluye bloqueos temporales de búfer ni de marca de transacción. Hay disponible una lista\_ \* de esperas de bloqueos temporales en sys. dm_os_latch_stats. Tenga en cuenta que los grupos LATCH_NL, LATCH_SH, LATCH_UP, LATCH_EX y LATCH_DT de sys.dm_os_latch_stats esperan juntos.| 
|LATCH_KP |Tiene lugar cuando se espera un bloqueo temporal de mantenimiento (KP). No incluye bloqueos temporales de búfer ni de marca de transacción. Hay disponible una lista\_ \* de esperas de bloqueos temporales en sys. dm_os_latch_stats. Tenga en cuenta que los grupos LATCH_NL, LATCH_SH, LATCH_UP, LATCH_EX y LATCH_DT de sys.dm_os_latch_stats esperan juntos.| 
|LATCH_NL |Solamente se identifica con fines informativos. No compatible. La compatibilidad con versiones posteriores no está garantizada.| 
|LATCH_SH |Tiene lugar cuando se espera un bloqueo temporal de uso compartido (SH). No incluye bloqueos temporales de búfer ni de marca de transacción. Hay disponible una lista\_ \* de esperas de bloqueos temporales en sys. dm_os_latch_stats. Tenga en cuenta que los grupos LATCH_NL, LATCH_SH, LATCH_UP, LATCH_EX y LATCH_DT de sys.dm_os_latch_stats esperan juntos.| 
|LATCH_UP |Tiene lugar cuando se espera un bloqueo temporal de actualización (UP). No incluye bloqueos temporales de búfer ni de marca de transacción. Hay disponible una lista\_ \* de esperas de bloqueos temporales en sys. dm_os_latch_stats. Tenga en cuenta que los grupos LATCH_NL, LATCH_SH, LATCH_UP, LATCH_EX y LATCH_DT de sys.dm_os_latch_stats esperan juntos.| 
|LAZYWRITER_SLEEP |Tiene lugar cuando se suspenden tareas de escritura diferida. Ésta es una medida del tiempo invertido por las tareas en segundo plano que esperan. No tenga en cuenta este estado cuando busque pausas del usuario.| 
|LCK_M_BU |Tiene lugar cuando una tarea está esperando adquirir un bloqueo de actualización masiva (BU).| 
|LCK_M_BU_ABORT_BLOCKERS |Tiene lugar cuando una tarea está esperando adquirir un bloqueo de actualización masiva (BU) con ABORT BLOCKERS. (Relacionado con la opción de espera de prioridad baja de ALTER TABLE y ALTER INDEX). <br /> **Válido para** : [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] y versiones posteriores.| 
|LCK_M_BU_LOW_PRIORITY |Tiene lugar cuando una tarea está esperando adquirir un bloqueo de actualización masiva (BU) con prioridad baja. (Relacionado con la opción de espera de prioridad baja de ALTER TABLE y ALTER INDEX). <br /> **Válido para** : [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] y versiones posteriores.| 
|LCK_M_IS |Tiene lugar cuando una tarea está esperando adquirir un bloqueo de intención compartida (IS).| 
|LCK_M_IS_ABORT_BLOCKERS |Tiene lugar cuando una tarea está esperando adquirir un bloqueo de intención compartida (IS) con ABORT BLOCKERS. (Relacionado con la opción de espera de prioridad baja de ALTER TABLE y ALTER INDEX). <br /> **Válido para** : [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] y versiones posteriores.| 
|LCK_M_IS_LOW_PRIORITY |Tiene lugar cuando una tarea está esperando adquirir un bloqueo de intención compartida (IS) con baja prioridad. (Relacionado con la opción de espera de prioridad baja de ALTER TABLE y ALTER INDEX). <br /> **Válido para** : [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] y versiones posteriores.| 
|LCK_M_IU |Tiene lugar cuando una tarea está esperando adquirir un bloqueo de intención de actualización (IU).| 
|LCK_M_IU_ABORT_BLOCKERS |Tiene lugar cuando una tarea está esperando adquirir un bloqueo de intención de actualización (IU) con ABORT BLOCKERS. (Relacionado con la opción de espera de prioridad baja de ALTER TABLE y ALTER INDEX). <br /> **Válido para** : [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] y versiones posteriores.| 
|LCK_M_IU_LOW_PRIORITY |Tiene lugar cuando una tarea está esperando adquirir un bloqueo de intención de actualización (IU) con baja prioridad. (Relacionado con la opción de espera de prioridad baja de ALTER TABLE y ALTER INDEX). <br /> **Válido para** : [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] y versiones posteriores.| 
|LCK_M_IX |Tiene lugar cuando una tarea está esperando adquirir un bloqueo de intención exclusiva (IX).| 
|LCK_M_IX_ABORT_BLOCKERS |Tiene lugar cuando una tarea está esperando adquirir un bloqueo de intención exclusiva (IX) con ABORT BLOCKERS. (Relacionado con la opción de espera de prioridad baja de ALTER TABLE y ALTER INDEX). <br /> **Válido para** : [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] y versiones posteriores.| 
|LCK_M_IX_LOW_PRIORITY |Tiene lugar cuando una tarea está esperando adquirir un bloqueo de intención exclusiva (IX) con baja prioridad. (Relacionado con la opción de espera de prioridad baja de ALTER TABLE y ALTER INDEX). <br /> **Válido para** : [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] y versiones posteriores.| 
|LCK_M_RIn_NL |Tiene lugar cuando una tarea está esperando adquirir un bloqueo NULL en el valor de clave actual y un bloqueo de intervalo de inserción entre la clave anterior y la actual. Un bloqueo NULL en la clave es un bloqueo de liberación instantánea.| 
|LCK_M_RIn_NL_ABORT_BLOCKERS |Tiene lugar cuando una tarea está esperando adquirir un bloqueo NULL con ABORT BLOCKERS en el valor de clave actual y un bloqueo de intervalo de inserción con ABORT BLOCKERS entre la clave anterior y la actual. Un bloqueo NULL en la clave es un bloqueo de liberación instantánea. (Relacionado con la opción de espera de prioridad baja de ALTER TABLE y ALTER INDEX). <br /> **Válido para** : [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] y versiones posteriores.| 
|LCK_M_RIn_NL_LOW_PRIORITY |Tiene lugar cuando una tarea está esperando adquirir un bloqueo NULL con baja prioridad en el valor de clave actual y un bloqueo de intervalo de inserción con baja prioridad entre la clave anterior y la actual. Un bloqueo NULL en la clave es un bloqueo de liberación instantánea. (Relacionado con la opción de espera de prioridad baja de ALTER TABLE y ALTER INDEX). <br /> **Válido para** : [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] y versiones posteriores.| 
|LCK_M_RIn_S |Tiene lugar cuando una tarea está esperando adquirir un bloqueo de uso compartido en el valor de clave actual y un bloqueo de intervalo de inserción entre la clave anterior y la actual.| 
|LCK_M_RIn_S_ABORT_BLOCKERS |Tiene lugar cuando una tarea está esperando adquirir un bloqueo compartido con ABORT BLOCKERS en el valor de clave actual y un bloqueo de intervalo de inserción con ABORT BLOCKERS entre la clave anterior y la actual. (Relacionado con la opción de espera de prioridad baja de ALTER TABLE y ALTER INDEX). <br /> **Válido para** : [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] y versiones posteriores.| 
|LCK_M_RIn_S_LOW_PRIORITY |Tiene lugar cuando una tarea está esperando adquirir un bloqueo compartido con baja prioridad en el valor de clave actual y un bloqueo de intervalo de inserción con baja prioridad entre la clave anterior y la actual. (Relacionado con la opción de espera de prioridad baja de ALTER TABLE y ALTER INDEX). <br /> **Válido para** : [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] y versiones posteriores.| 
|LCK_M_RIn_U |La tarea espera adquirir un bloqueo de actualización en el valor de clave actual y un bloqueo de intervalo de inserción entre la clave anterior y la actual.| 
|LCK_M_RIn_U_ABORT_BLOCKERS |La tarea está esperando adquirir un bloqueo de actualización con ABORT BLOCKERS en el valor de clave actual y un bloqueo de intervalo de inserción con ABORT BLOCKERS entre la clave anterior y la actual. (Relacionado con la opción de espera de prioridad baja de ALTER TABLE y ALTER INDEX). <br /> **Válido para** : [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] y versiones posteriores.| 
|LCK_M_RIn_U_LOW_PRIORITY |La tarea está esperando adquirir un bloqueo de actualización con baja prioridad en el valor de clave actual y un bloqueo de intervalo de inserción con baja prioridad entre la clave anterior y la actual. (Relacionado con la opción de espera de prioridad baja de ALTER TABLE y ALTER INDEX). <br /> **Válido para** : [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] y versiones posteriores.| 
|LCK_M_RIn_X |Tiene lugar cuando una tarea está esperando adquirir un bloqueo exclusivo en el valor de clave actual y un bloqueo de intervalo de inserción entre la clave anterior y la actual.| 
|LCK_M_RIn_X_ABORT_BLOCKERS |Tiene lugar cuando una tarea está esperando adquirir un bloqueo exclusivo con ABORT BLOCKERS en el valor de clave actual y un bloqueo de intervalo de inserción con ABORT BLOCKERS entre la clave anterior y la actual. (Relacionado con la opción de espera de prioridad baja de ALTER TABLE y ALTER INDEX). <br /> **Válido para** : [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] y versiones posteriores.| 
|LCK_M_RIn_X_LOW_PRIORITY |Tiene lugar cuando una tarea está esperando adquirir un bloqueo exclusivo con baja prioridad en el valor de clave actual y un bloqueo de intervalo de inserción con baja prioridad entre la clave anterior y la actual. (Relacionado con la opción de espera de prioridad baja de ALTER TABLE y ALTER INDEX). <br /> **Válido para** : [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] y versiones posteriores.| 
|LCK_M_RS_S |Tiene lugar cuando una tarea está esperando adquirir un bloqueo de uso compartido en el valor de clave actual y un bloqueo de intervalo compartido entre la clave anterior y la actual.| 
|LCK_M_RS_S_ABORT_BLOCKERS |Tiene lugar cuando una tarea está esperando adquirir un bloqueo compartido con ABORT BLOCKERS en el valor de clave actual y un bloqueo de intervalo compartido con ABORT BLOCKERS entre la clave anterior y la actual. (Relacionado con la opción de espera de prioridad baja de ALTER TABLE y ALTER INDEX). <br /> **Válido para** : [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] y versiones posteriores.| 
|LCK_M_RS_S_LOW_PRIORITY |Tiene lugar cuando una tarea está esperando adquirir un bloqueo compartido con baja prioridad en el valor de clave actual y un bloqueo de intervalo compartido con baja prioridad entre la clave anterior y la actual. (Relacionado con la opción de espera de prioridad baja de ALTER TABLE y ALTER INDEX). <br /> **Válido para** : [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] y versiones posteriores.| 
|LCK_M_RS_U |Tiene lugar cuando una tarea está esperando adquirir un bloqueo de actualización en el valor de clave actual y un bloqueo de intervalo de actualización entre la clave anterior y la actual.| 
|LCK_M_RS_U_ABORT_BLOCKERS |Tiene lugar cuando una tarea está esperando adquirir un bloqueo de actualización con ABORT BLOCKERS en el valor de clave actual y un bloqueo de intervalo de actualización con ABORT BLOCKERS entre la clave anterior y la actual. (Relacionado con la opción de espera de prioridad baja de ALTER TABLE y ALTER INDEX). <br /> **Válido para** : [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] y versiones posteriores.| 
|LCK_M_RS_U_LOW_PRIORITY |Tiene lugar cuando una tarea está esperando adquirir un bloqueo de actualización con baja prioridad en el valor de clave actual y un bloqueo de intervalo de actualización con baja prioridad entre la clave anterior y la actual. (Relacionado con la opción de espera de prioridad baja de ALTER TABLE y ALTER INDEX). <br /> **Válido para** : [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] y versiones posteriores.| 
|LCK_M_RX_S |Tiene lugar cuando una tarea está esperando adquirir un bloqueo de uso compartido en el valor de clave actual y un bloqueo de intervalo exclusivo entre la clave anterior y la actual.| 
|LCK_M_RX_S_ABORT_BLOCKERS |Tiene lugar cuando una tarea está esperando adquirir un bloqueo compartido con ABORT BLOCKERS en el valor de clave actual y un bloqueo de intervalo exclusivo con bloqueo ABORT BLOCKERS entre la clave anterior y la actual. (Relacionado con la opción de espera de prioridad baja de ALTER TABLE y ALTER INDEX). <br /> **Válido para** : [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] y versiones posteriores.| 
|LCK_M_RX_S_LOW_PRIORITY |Tiene lugar cuando una tarea está esperando adquirir un bloqueo compartido con baja prioridad en el valor de clave actual y un bloqueo de intervalo exclusivo con bloqueo de baja prioridad entre la clave anterior y la actual. (Relacionado con la opción de espera de prioridad baja de ALTER TABLE y ALTER INDEX). <br /> **Válido para** : [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] y versiones posteriores.| 
|LCK_M_RX_U |Tiene lugar cuando una tarea está esperando adquirir un bloqueo de actualización en el valor de clave actual y un bloqueo de intervalo exclusivo entre la clave anterior y la actual.| 
|LCK_M_RX_U_ABORT_BLOCKERS |Tiene lugar cuando una tarea está esperando adquirir un bloqueo de actualización con ABORT BLOCKERS en el valor de clave actual y un bloqueo de intervalo exclusivo con ABORT BLOCKERS entre la clave anterior y la actual. (Relacionado con la opción de espera de prioridad baja de ALTER TABLE y ALTER INDEX). <br /> **Válido para** : [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] y versiones posteriores.| 
|LCK_M_RX_U_LOW_PRIORITY |Tiene lugar cuando una tarea está esperando adquirir un bloqueo de actualización con baja prioridad en el valor de clave actual y un bloqueo de intervalo exclusivo con baja prioridad entre la clave anterior y la actual. (Relacionado con la opción de espera de prioridad baja de ALTER TABLE y ALTER INDEX). <br /> **Válido para** : [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] y versiones posteriores.| 
|LCK_M_RX_X |Tiene lugar cuando una tarea está esperando adquirir un bloqueo exclusivo en el valor de clave actual y un bloqueo de intervalo exclusivo entre la clave anterior y la actual.| 
|LCK_M_RX_X_ABORT_BLOCKERS |Tiene lugar cuando una tarea está esperando adquirir un bloqueo exclusivo con ABORT BLOCKERS en el valor de clave actual y un bloqueo de intervalo exclusivo con ABORT BLOCKERS entre la clave anterior y la actual. (Relacionado con la opción de espera de prioridad baja de ALTER TABLE y ALTER INDEX). <br /> **Válido para** : [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] y versiones posteriores.| 
|LCK_M_RX_X_LOW_PRIORITY |Tiene lugar cuando una tarea está esperando adquirir un bloqueo exclusivo con baja prioridad en el valor de clave actual y un bloqueo de intervalo exclusivo con baja prioridad entre la clave anterior y la actual. (Relacionado con la opción de espera de prioridad baja de ALTER TABLE y ALTER INDEX). <br /> **Válido para** : [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] y versiones posteriores.| 
|LCK_M_S |Tiene lugar cuando una tarea está esperando a adquirir un bloqueo compartido.| 
|LCK_M_S_ABORT_BLOCKERS |Tiene lugar cuando una tarea está esperando adquirir un bloqueo compartido con ABORT BLOCKERS. (Relacionado con la opción de espera de prioridad baja de ALTER TABLE y ALTER INDEX). <br /> **Válido para** : [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] y versiones posteriores.| 
|LCK_M_S_LOW_PRIORITY |Tiene lugar cuando una tarea está esperando adquirir un bloqueo compartido con baja prioridad. (Relacionado con la opción de espera de prioridad baja de ALTER TABLE y ALTER INDEX). <br /> **Válido para** : [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] y versiones posteriores.| 
|LCK_M_SCH_M |Tiene lugar cuando una tarea está esperando a adquirir un bloqueo de modificación de esquema.| 
|LCK_M_SCH_M_ABORT_BLOCKERS |Tiene lugar cuando una tarea está esperando a adquirir un bloqueo de modificación de esquema con ABORT BLOCKERS. (Relacionado con la opción de espera de prioridad baja de ALTER TABLE y ALTER INDEX). <br /> **Válido para** : [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] y versiones posteriores.| 
|LCK_M_SCH_M_LOW_PRIORITY |Tiene lugar cuando una tarea está esperando a adquirir un bloqueo de modificación de esquema con baja prioridad. (Relacionado con la opción de espera de prioridad baja de ALTER TABLE y ALTER INDEX). <br /> **Válido para** : [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] y versiones posteriores.| 
|LCK_M_SCH_S |Tiene lugar cuando una tarea está esperando adquirir un bloqueo de uso compartido de esquema.| 
|LCK_M_SCH_S_ABORT_BLOCKERS |Tiene lugar cuando una tarea está esperando a adquirir un bloqueo de uso compartido de esquema con ABORT BLOCKERS. (Relacionado con la opción de espera de prioridad baja de ALTER TABLE y ALTER INDEX). <br /> **Válido para** : [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] y versiones posteriores.| 
|LCK_M_SCH_S_LOW_PRIORITY |Tiene lugar cuando una tarea está esperando a adquirir un bloqueo de uso compartido de esquema con baja prioridad. (Relacionado con la opción de espera de prioridad baja de ALTER TABLE y ALTER INDEX). <br /> **Válido para** : [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] y versiones posteriores.| 
|LCK_M_SIU |Tiene lugar cuando una tarea está esperando adquirir un bloqueo de uso compartido con intento de actualización.| 
|LCK_M_SIU_ABORT_BLOCKERS |Tiene lugar cuando una tarea está esperando adquirir un bloqueo de uso compartido con actualización intensiva con ABORT BLOCKERS. (Relacionado con la opción de espera de prioridad baja de ALTER TABLE y ALTER INDEX). <br /> **Válido para** : [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] y versiones posteriores.| 
|LCK_M_SIU_LOW_PRIORITY |Tiene lugar cuando una tarea está esperando adquirir un bloqueo de uso compartido con actualización exclusiva con baja prioridad. (Relacionado con la opción de espera de prioridad baja de ALTER TABLE y ALTER INDEX). <br /> **Válido para** : [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] y versiones posteriores.| 
|LCK_M_SIX |Tiene lugar cuando una tarea está esperando adquirir un bloqueo de uso compartido con intención exclusiva.| 
|LCK_M_SIX_ABORT_BLOCKERS |Tiene lugar cuando una tarea está esperando adquirir un bloqueo de uso compartido con intención exclusiva con ABORT BLOCKERS. (Relacionado con la opción de espera de prioridad baja de ALTER TABLE y ALTER INDEX). <br /> **Válido para** : [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] y versiones posteriores.| 
|LCK_M_SIX_LOW_PRIORITY |Tiene lugar cuando una tarea está esperando adquirir un bloqueo de uso compartido con intención exclusiva con baja prioridad. (Relacionado con la opción de espera de prioridad baja de ALTER TABLE y ALTER INDEX). <br /> **Válido para** : [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] y versiones posteriores.| 
|LCK_M_U |Tiene lugar cuando una tarea está esperando a adquirir un bloqueo de actualización.| 
|LCK_M_U_ABORT_BLOCKERS |Tiene lugar cuando una tarea está esperando adquirir un bloqueo de actualización con ABORT BLOCKERS. (Relacionado con la opción de espera de prioridad baja de ALTER TABLE y ALTER INDEX). <br /> **Válido para** : [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] y versiones posteriores.| 
|LCK_M_U_LOW_PRIORITY |Tiene lugar cuando una tarea está esperando adquirir un bloqueo de actualización con baja prioridad. (Relacionado con la opción de espera de prioridad baja de ALTER TABLE y ALTER INDEX). <br /> **Válido para** : [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] y versiones posteriores.| 
|LCK_M_UIX |Tiene lugar cuando una tarea está esperando adquirir un bloqueo de actualización con intención exclusiva.| 
|LCK_M_UIX_ABORT_BLOCKERS |Tiene lugar cuando una tarea está esperando adquirir un bloqueo de actualización con intención exclusiva con ABORT BLOCKERS. (Relacionado con la opción de espera de prioridad baja de ALTER TABLE y ALTER INDEX). <br /> **Válido para** : [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] y versiones posteriores.| 
|LCK_M_UIX_LOW_PRIORITY |Tiene lugar cuando una tarea está esperando adquirir un bloqueo de actualización con intención exclusiva con baja prioridad. (Relacionado con la opción de espera de prioridad baja de ALTER TABLE y ALTER INDEX). <br /> **Válido para** : [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] y versiones posteriores.| 
|LCK_M_X |Tiene lugar cuando una tarea está esperando a adquirir un bloqueo exclusivo.| 
|LCK_M_X_ABORT_BLOCKERS |Tiene lugar cuando una tarea está esperando adquirir un bloqueo exclusivo con ABORT BLOCKERS. (Relacionado con la opción de espera de prioridad baja de ALTER TABLE y ALTER INDEX). <br /> **Válido para** : [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] y versiones posteriores.| 
|LCK_M_X_LOW_PRIORITY |Tiene lugar cuando una tarea está esperando adquirir un bloqueo exclusivo con baja prioridad. (Relacionado con la opción de espera de prioridad baja de ALTER TABLE y ALTER INDEX). <br /> **Válido para** : [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] y versiones posteriores.| 
|LOG_POOL_SCAN |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] y versiones posteriores.| 
|LOG_RATE_GOVERNOR |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] y versiones posteriores.| 
|LOGBUFFER |Tiene lugar cuando una tarea está esperando tener espacio en el búfer del registro para almacenar un registro. Valores coherentemente altos pueden indicar que los dispositivos de registro no pueden hacer frente a la cantidad de registros que va a generar el servidor.| 
|LOGCAPTURE_LOGPOOLTRUNCPOINT |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] y versiones posteriores.| 
|LOGGENERATION |Solamente se identifica con fines informativos. No compatible. La compatibilidad con versiones posteriores no está garantizada.| 
|LOGMGR |Tiene lugar cuando una tarea está esperando que finalicen operaciones de E/S pendientes para cerrar el registro mientras se cierra la base de datos.| 
|LOGMGR_FLUSH |Solamente se identifica con fines informativos. No compatible. La compatibilidad con versiones posteriores no está garantizada.| 
|LOGMGR_PMM_LOG |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] y versiones posteriores.| 
|LOGMGR_QUEUE |Tiene lugar mientras la tarea de escritura en registro espera solicitudes de trabajo.| 
|LOGMGR_RESERVE_APPEND |Tiene lugar cuando una tarea está esperando comprobar si el truncamiento del registro libera espacio del registro para permitir que la tarea escriba un nuevo registro. Para reducir esta espera, puede aumentar el tamaño de los archivos de registro de la base de datos correspondiente.| 
|LOGPOOL_CACHESIZE |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] y versiones posteriores.| 
|LOGPOOL_CONSUMER |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] y versiones posteriores.| 
|LOGPOOL_CONSUMERSET |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] y versiones posteriores.| 
|LOGPOOL_FREEPOOLS |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] y versiones posteriores.| 
|LOGPOOL_MGRSET |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] y versiones posteriores.| 
|LOGPOOL_REPLACEMENTSET |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] y versiones posteriores.| 
|LOGPOOLREFCOUNTEDOBJECT_REFDONE |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] y versiones posteriores.| 
|LOWFAIL_MEMMGR_QUEUE |Tiene lugar mientras se espera que haya memoria disponible para su uso.| 
|MD_AGENT_YIELD |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] y versiones posteriores.| 
|MD_LAZYCACHE_RWLOCK |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] y versiones posteriores.| 
|MEMORY_ALLOCATION_EXT |Tiene lugar durante la asignación de memoria desde el grupo de memoria del SQL Server interno o el sistema operativo. <br /> **Válido para** : [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] y versiones posteriores.| 
|MEMORY_GRANT_UPDATE |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] y versiones posteriores.| 
|METADATA_LAZYCACHE_RWLOCK |Exclusivamente para uso interno. <br /> Solo **se aplica a**: [!INCLUDE[ssKilimanjaro_md](../../includes/sskilimanjaro-md.md)] . |  
|MIGRATIONBUFFER |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] y versiones posteriores.| 
|MISCELLANEOUS |Solamente se identifica con fines informativos. No compatible. La compatibilidad con versiones posteriores no está garantizada.| 
|MISCELLANEOUS |Solamente se identifica con fines informativos. No compatible. La compatibilidad con versiones posteriores no está garantizada.| 
|MSQL_DQ |Tiene lugar cuando una tarea está esperando que finalice una operación de consulta distribuida. Se utiliza para detectar potenciales interbloqueos de aplicación MARS (Conjuntos de resultados activos múltiples). La espera termina cuando finaliza la llamada a la consulta distribuida.| 
|MSQL_XACT_MGR_MUTEX |Tiene lugar cuando una tarea está esperando obtener la propiedad del administrador de transacciones de la sesión para realizar una operación de transacción en el nivel de sesión.| 
|MSQL_XACT_MUTEX |Tiene lugar durante la sincronización del uso de transacciones. Una solicitud debe adquirir la exclusión mutua para poder utilizar la transacción.| 
|MSQL_XP |Tiene lugar cuando una tarea está esperando que finalice un procedimiento almacenado extendido. SQL Server utiliza este estado de espera para detectar interbloqueos potenciales de la aplicación MARS. La espera se detiene cuando finaliza la llamada al procedimiento almacenado extendido.| 
|MSSEARCH |Tiene lugar durante las llamadas a la búsqueda de texto completo. Esta espera termina cuando finaliza la operación de texto completo. No indica contención, sino la duración de las operaciones de texto completo.| 
|NET_WAITFOR_PACKET |Tiene lugar cuando una conexión está esperando un paquete de red durante una lectura de red.| 
|NETWORKSXMLMGRLOAD |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] y versiones posteriores.| 
|NODE_CACHE_MUTEX |Exclusivamente para uso interno.| 
|OLEDB |Se produce cuando SQL Server llama al proveedor de OLE DB de SQL Server Native Client. Este estado de espera no se usa para la sincronización. Se usa para indicar la duración de las llamadas al proveedor OLE DB.| 
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
|PARALLEL_REDO_DRAIN_WORKER |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] y versiones posteriores.| 
|PARALLEL_REDO_FLOW_CONTROL |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] y versiones posteriores.| 
|PARALLEL_REDO_LOG_CACHE |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] y versiones posteriores.| 
|PARALLEL_REDO_TRAN_LIST |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] y versiones posteriores.| 
|PARALLEL_REDO_TRAN_TURN |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] y versiones posteriores.| 
|PARALLEL_REDO_WORKER_SYNC |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] y versiones posteriores.| 
|PARALLEL_REDO_WORKER_WAIT_WORK |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] y versiones posteriores.| 
|PERFORMANCE_COUNTERS_RWLOCK |Exclusivamente para uso interno.| 
|PHYSICAL_SEEDING_DMV |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] y versiones posteriores.| 
|POOL_LOG_RATE_GOVERNOR |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] y versiones posteriores.| 
|PREEMPTIVE_ABR |Solamente se identifica con fines informativos. No compatible. La compatibilidad con versiones posteriores no está garantizada.| 
|PREEMPTIVE_AUDIT_ACCESS_EVENTLOG |Tiene lugar cuando el programador del sistema operativo de [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] (SQLOS) cambia a modo preferente para escribir un evento de auditoría en el registro de eventos de Windows. <br /> Solo **se aplica a**: [!INCLUDE[ssKilimanjaro_md](../../includes/sskilimanjaro-md.md)] . |  
|PREEMPTIVE_AUDIT_ACCESS_SECLOG |Tiene lugar cuando el programador de SQLOS cambia a modo preferente para escribir un evento de auditoría en el registro de seguridad de Windows. <br /> Solo **se aplica a**: [!INCLUDE[ssKilimanjaro_md](../../includes/sskilimanjaro-md.md)] . |  
|PREEMPTIVE_CLOSEBACKUPMEDIA |Tiene lugar cuando el programador de SQLOS cambia a modo preferente para cerrar el medio de copia de seguridad.| 
|PREEMPTIVE_CLOSEBACKUPTAPE |Tiene lugar cuando el programador de SQLOS cambia a modo preferente para cerrar un dispositivo de copia de seguridad de cinta.| 
|PREEMPTIVE_CLOSEBACKUPVDIDEVICE |Tiene lugar cuando el programador de SQLOS cambia a modo preferente para cerrar un dispositivo de copia de seguridad virtual.| 
|PREEMPTIVE_CLUSAPI_CLUSTERRESOURCECONTROL |Tiene lugar cuando el programador de SQLOS cambia a modo preferente para realizar las operaciones de clúster de conmutación por error de Windows.| 
|PREEMPTIVE_COM_COCREATEINSTANCE |Tiene lugar cuando el programador de SQLOS cambia a modo preferente para crear un objeto COM.| 
|PREEMPTIVE_COM_COGETCLASSOBJECT |Exclusivamente para uso interno.| 
|PREEMPTIVE_COM_CREATEACCESSOR |Exclusivamente para uso interno.| 
|PREEMPTIVE_COM_DELETEROWS |Exclusivamente para uso interno.| 
|PREEMPTIVE_COM_GETCOMMANDTEXT |Exclusivamente para uso interno.| 
|PREEMPTIVE_COM_GETDATA |Exclusivamente para uso interno.| 
|PREEMPTIVE_COM_GETNEXTROWS |Exclusivamente para uso interno.| 
|PREEMPTIVE_COM_GETRESULT |Exclusivamente para uso interno.| 
|PREEMPTIVE_COM_GETROWSBYBOOKMARK |Exclusivamente para uso interno.| 
|PREEMPTIVE_COM_LBFLUSH |Exclusivamente para uso interno.| 
|PREEMPTIVE_COM_LBLOCKREGION |Exclusivamente para uso interno.| 
|PREEMPTIVE_COM_LBREADAT |Exclusivamente para uso interno.| 
|PREEMPTIVE_COM_LBSETSIZE |Exclusivamente para uso interno.| 
|PREEMPTIVE_COM_LBSTAT |Exclusivamente para uso interno.| 
|PREEMPTIVE_COM_LBUNLOCKREGION |Exclusivamente para uso interno.| 
|PREEMPTIVE_COM_LBWRITEAT |Exclusivamente para uso interno.| 
|PREEMPTIVE_COM_QUERYINTERFACE |Exclusivamente para uso interno.| 
|PREEMPTIVE_COM_RELEASE |Exclusivamente para uso interno.| 
|PREEMPTIVE_COM_RELEASEACCESSOR |Exclusivamente para uso interno.| 
|PREEMPTIVE_COM_RELEASEROWS |Exclusivamente para uso interno.| 
|PREEMPTIVE_COM_RELEASESESSION |Exclusivamente para uso interno.| 
|PREEMPTIVE_COM_RESTARTPOSITION |Exclusivamente para uso interno.| 
|PREEMPTIVE_COM_SEQSTRMREAD |Exclusivamente para uso interno.| 
|PREEMPTIVE_COM_SEQSTRMREADANDWRITE |Exclusivamente para uso interno.| 
|PREEMPTIVE_COM_SETDATAFAILURE |Exclusivamente para uso interno.| 
|PREEMPTIVE_COM_SETPARAMETERINFO |Exclusivamente para uso interno.| 
|PREEMPTIVE_COM_SETPARAMETERPROPERTIES |Exclusivamente para uso interno.| 
|PREEMPTIVE_COM_STRMLOCKREGION |Exclusivamente para uso interno.| 
|PREEMPTIVE_COM_STRMSEEKANDREAD |Exclusivamente para uso interno.| 
|PREEMPTIVE_COM_STRMSEEKANDWRITE |Exclusivamente para uso interno.| 
|PREEMPTIVE_COM_STRMSETSIZE |Exclusivamente para uso interno.| 
|PREEMPTIVE_COM_STRMSTAT |Exclusivamente para uso interno.| 
|PREEMPTIVE_COM_STRMUNLOCKREGION |Exclusivamente para uso interno.| 
|PREEMPTIVE_CONSOLEWRITE |Exclusivamente para uso interno.| 
|PREEMPTIVE_CREATEPARAM |Exclusivamente para uso interno.| 
|PREEMPTIVE_DEBUG |Exclusivamente para uso interno.| 
|PREEMPTIVE_DFSADDLINK |Exclusivamente para uso interno.| 
|PREEMPTIVE_DFSLINKEXISTCHECK |Exclusivamente para uso interno.| 
|PREEMPTIVE_DFSLINKHEALTHCHECK |Exclusivamente para uso interno.| 
|PREEMPTIVE_DFSREMOVELINK |Exclusivamente para uso interno.| 
|PREEMPTIVE_DFSREMOVEROOT |Exclusivamente para uso interno.| 
|PREEMPTIVE_DFSROOTFOLDERCHECK |Exclusivamente para uso interno.| 
|PREEMPTIVE_DFSROOTINIT |Exclusivamente para uso interno.| 
|PREEMPTIVE_DFSROOTSHARECHECK |Exclusivamente para uso interno.| 
|PREEMPTIVE_DTC_ABORT |Exclusivamente para uso interno.| 
|PREEMPTIVE_DTC_ABORTREQUESTDONE |Exclusivamente para uso interno.| 
|PREEMPTIVE_DTC_BEGINTRANSACTION |Exclusivamente para uso interno.| 
|PREEMPTIVE_DTC_COMMITREQUESTDONE |Exclusivamente para uso interno.| 
|PREEMPTIVE_DTC_ENLIST |Exclusivamente para uso interno.| 
|PREEMPTIVE_DTC_PREPAREREQUESTDONE |Exclusivamente para uso interno.| 
|PREEMPTIVE_FILESIZEGET |Exclusivamente para uso interno.| 
|PREEMPTIVE_FSAOLEDB_ABORTTRANSACTION |Exclusivamente para uso interno.| 
|PREEMPTIVE_FSAOLEDB_COMMITTRANSACTION |Exclusivamente para uso interno.| 
|PREEMPTIVE_FSAOLEDB_STARTTRANSACTION |Exclusivamente para uso interno.| 
|PREEMPTIVE_FSRECOVER_UNCONDITIONALUNDO |Exclusivamente para uso interno.| 
|PREEMPTIVE_GETRMINFO |Exclusivamente para uso interno.| 
|PREEMPTIVE_HADR_LEASE_MECHANISM |Always On la programación del administrador de concesiones de grupos de disponibilidad para el diagnóstico de Soporte técnico de Microsoft. <br /> **Válido para** : [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] y versiones posteriores.| 
|PREEMPTIVE_HTTP_EVENT_WAIT |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] y versiones posteriores.| 
|PREEMPTIVE_HTTP_REQUEST |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] y versiones posteriores.| 
|PREEMPTIVE_LOCKMONITOR |Exclusivamente para uso interno.| 
|PREEMPTIVE_MSS_RELEASE |Exclusivamente para uso interno.| 
|PREEMPTIVE_ODBCOPS |Exclusivamente para uso interno.| 
|PREEMPTIVE_OLE_UNINIT |Exclusivamente para uso interno.| 
|PREEMPTIVE_OLEDB_ABORTORCOMMITTRAN |Exclusivamente para uso interno.| 
|PREEMPTIVE_OLEDB_ABORTTRAN |Exclusivamente para uso interno.| 
|PREEMPTIVE_OLEDB_GETDATASOURCE |Exclusivamente para uso interno.| 
|PREEMPTIVE_OLEDB_GETLITERALINFO |Exclusivamente para uso interno.| 
|PREEMPTIVE_OLEDB_GETPROPERTIES |Exclusivamente para uso interno.| 
|PREEMPTIVE_OLEDB_GETPROPERTYINFO |Exclusivamente para uso interno.| 
|PREEMPTIVE_OLEDB_GETSCHEMALOCK |Exclusivamente para uso interno.| 
|PREEMPTIVE_OLEDB_JOINTRANSACTION |Exclusivamente para uso interno.| 
|PREEMPTIVE_OLEDB_RELEASE |Exclusivamente para uso interno.| 
|PREEMPTIVE_OLEDB_SETPROPERTIES |Exclusivamente para uso interno.| 
|PREEMPTIVE_OLEDBOPS |Exclusivamente para uso interno.| 
|PREEMPTIVE_OS_ACCEPTSECURITYCONTEXT |Exclusivamente para uso interno.| 
|PREEMPTIVE_OS_ACQUIRECREDENTIALSHANDLE |Exclusivamente para uso interno.| 
|PREEMPTIVE_OS_AUTHENTICATIONOPS |Exclusivamente para uso interno.| 
|PREEMPTIVE_OS_AUTHORIZATIONOPS |Exclusivamente para uso interno.| 
|PREEMPTIVE_OS_AUTHZGETINFORMATIONFROMCONTEXT |Exclusivamente para uso interno.| 
|PREEMPTIVE_OS_AUTHZINITIALIZECONTEXTFROMSID |Exclusivamente para uso interno.| 
|PREEMPTIVE_OS_AUTHZINITIALIZERESOURCEMANAGER |Exclusivamente para uso interno.| 
|PREEMPTIVE_OS_BACKUPREAD |Exclusivamente para uso interno.| 
|PREEMPTIVE_OS_CLOSEHANDLE |Exclusivamente para uso interno.| 
|PREEMPTIVE_OS_CLUSTEROPS |Exclusivamente para uso interno.| 
|PREEMPTIVE_OS_COMOPS |Exclusivamente para uso interno.| 
|PREEMPTIVE_OS_COMPLETEAUTHTOKEN |Exclusivamente para uso interno.| 
|PREEMPTIVE_OS_COPYFILE |Exclusivamente para uso interno.| 
|PREEMPTIVE_OS_CREATEDIRECTORY |Exclusivamente para uso interno.| 
|PREEMPTIVE_OS_CREATEFILE |Exclusivamente para uso interno.| 
|PREEMPTIVE_OS_CRYPTACQUIRECONTEXT |Exclusivamente para uso interno.| 
|PREEMPTIVE_OS_CRYPTIMPORTKEY |Exclusivamente para uso interno.| 
|PREEMPTIVE_OS_CRYPTOPS |Exclusivamente para uso interno.| 
|PREEMPTIVE_OS_DECRYPTMESSAGE |Exclusivamente para uso interno.| 
|PREEMPTIVE_OS_DELETEFILE |Exclusivamente para uso interno.| 
|PREEMPTIVE_OS_DELETESECURITYCONTEXT |Exclusivamente para uso interno.| 
|PREEMPTIVE_OS_DEVICEIOCONTROL |Exclusivamente para uso interno.| 
|PREEMPTIVE_OS_DEVICEOPS |Exclusivamente para uso interno.| 
|PREEMPTIVE_OS_DIRSVC_NETWORKOPS |Exclusivamente para uso interno.| 
|PREEMPTIVE_OS_DISCONNECTNAMEDPIPE |Exclusivamente para uso interno.| 
|PREEMPTIVE_OS_DOMAINSERVICESOPS |Exclusivamente para uso interno.| 
|PREEMPTIVE_OS_DSGETDCNAME |Exclusivamente para uso interno.| 
|PREEMPTIVE_OS_DTCOPS |Exclusivamente para uso interno.| 
|PREEMPTIVE_OS_ENCRYPTMESSAGE |Exclusivamente para uso interno.| 
|PREEMPTIVE_OS_FILEOPS |Exclusivamente para uso interno.| 
|PREEMPTIVE_OS_FINDFILE |Exclusivamente para uso interno.| 
|PREEMPTIVE_OS_FLUSHFILEBUFFERS |Exclusivamente para uso interno.| 
|PREEMPTIVE_OS_FORMATMESSAGE |Exclusivamente para uso interno.| 
|PREEMPTIVE_OS_FREECREDENTIALSHANDLE |Exclusivamente para uso interno.| 
|PREEMPTIVE_OS_FREELIBRARY |Exclusivamente para uso interno.| 
|PREEMPTIVE_OS_GENERICOPS |Exclusivamente para uso interno.| 
|PREEMPTIVE_OS_GETADDRINFO |Exclusivamente para uso interno.| 
|PREEMPTIVE_OS_GETCOMPRESSEDFILESIZE |Exclusivamente para uso interno.| 
|PREEMPTIVE_OS_GETDISKFREESPACE |Exclusivamente para uso interno.| 
|PREEMPTIVE_OS_GETFILEATTRIBUTES |Exclusivamente para uso interno.| 
|PREEMPTIVE_OS_GETFILESIZE |Exclusivamente para uso interno.| 
|PREEMPTIVE_OS_GETFINALFILEPATHBYHANDLE |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] y versiones posteriores.| 
|PREEMPTIVE_OS_GETLONGPATHNAME |Exclusivamente para uso interno.| 
|PREEMPTIVE_OS_GETPROCADDRESS |Exclusivamente para uso interno.| 
|PREEMPTIVE_OS_GETVOLUMENAMEFORVOLUMEMOUNTPOINT |Exclusivamente para uso interno.| 
|PREEMPTIVE_OS_GETVOLUMEPATHNAME |Exclusivamente para uso interno.| 
|PREEMPTIVE_OS_INITIALIZESECURITYCONTEXT |Exclusivamente para uso interno.| 
|PREEMPTIVE_OS_LIBRARYOPS |Exclusivamente para uso interno.| 
|PREEMPTIVE_OS_LOADLIBRARY |Exclusivamente para uso interno.| 
|PREEMPTIVE_OS_LOGONUSER |Exclusivamente para uso interno.| 
|PREEMPTIVE_OS_LOOKUPACCOUNTSID |Exclusivamente para uso interno.| 
|PREEMPTIVE_OS_MESSAGEQUEUEOPS |Exclusivamente para uso interno.| 
|PREEMPTIVE_OS_MOVEFILE |Exclusivamente para uso interno.| 
|PREEMPTIVE_OS_NETGROUPGETUSERS |Exclusivamente para uso interno.| 
|PREEMPTIVE_OS_NETLOCALGROUPGETMEMBERS |Exclusivamente para uso interno.| 
|PREEMPTIVE_OS_NETUSERGETGROUPS |Exclusivamente para uso interno.| 
|PREEMPTIVE_OS_NETUSERGETLOCALGROUPS |Exclusivamente para uso interno.| 
|PREEMPTIVE_OS_NETUSERMODALSGET |Exclusivamente para uso interno.| 
|PREEMPTIVE_OS_NETVALIDATEPASSWORDPOLICY |Exclusivamente para uso interno.| 
|PREEMPTIVE_OS_NETVALIDATEPASSWORDPOLICYFREE |Exclusivamente para uso interno.| 
|PREEMPTIVE_OS_OPENDIRECTORY |Exclusivamente para uso interno.| 
|PREEMPTIVE_OS_PDH_WMI_INIT |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] y versiones posteriores.| 
|PREEMPTIVE_OS_PIPEOPS |Exclusivamente para uso interno.| 
|PREEMPTIVE_OS_PROCESSOPS |Exclusivamente para uso interno.| 
|PREEMPTIVE_OS_QUERYCONTEXTATTRIBUTES |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] y versiones posteriores.| 
|PREEMPTIVE_OS_QUERYREGISTRY |Exclusivamente para uso interno.| 
|PREEMPTIVE_OS_QUERYSECURITYCONTEXTTOKEN |Exclusivamente para uso interno.| 
|PREEMPTIVE_OS_REMOVEDIRECTORY |Exclusivamente para uso interno.| 
|PREEMPTIVE_OS_REPORTEVENT |Exclusivamente para uso interno.| 
|PREEMPTIVE_OS_REVERTTOSELF |Exclusivamente para uso interno.| 
|PREEMPTIVE_OS_RSFXDEVICEOPS |Exclusivamente para uso interno.| 
|PREEMPTIVE_OS_SECURITYOPS |Exclusivamente para uso interno.| 
|PREEMPTIVE_OS_SERVICEOPS |Exclusivamente para uso interno.| 
|PREEMPTIVE_OS_SETENDOFFILE |Exclusivamente para uso interno.| 
|PREEMPTIVE_OS_SETFILEPOINTER |Exclusivamente para uso interno.| 
|PREEMPTIVE_OS_SETFILEVALIDDATA |Exclusivamente para uso interno.| 
|PREEMPTIVE_OS_SETNAMEDSECURITYINFO |Exclusivamente para uso interno.| 
|PREEMPTIVE_OS_SQLCLROPS |Exclusivamente para uso interno.| 
|PREEMPTIVE_OS_SQMLAUNCH |Exclusivamente para uso interno. <br /> **Se aplica a** [!INCLUDE[ssKilimanjaro_md](../../includes/sskilimanjaro-md.md)] : [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)]hasta. |  
|PREEMPTIVE_OS_VERIFYSIGNATURE |Exclusivamente para uso interno.| 
|PREEMPTIVE_OS_VERIFYTRUST |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] y versiones posteriores.| 
|PREEMPTIVE_OS_VSSOPS |Exclusivamente para uso interno.| 
|PREEMPTIVE_OS_WAITFORSINGLEOBJECT |Exclusivamente para uso interno.| 
|PREEMPTIVE_OS_WINSOCKOPS |Exclusivamente para uso interno.| 
|PREEMPTIVE_OS_WRITEFILE |Exclusivamente para uso interno.| 
|PREEMPTIVE_OS_WRITEFILEGATHER |Exclusivamente para uso interno.| 
|PREEMPTIVE_OS_WSASETLASTERROR |Exclusivamente para uso interno.| 
|PREEMPTIVE_REENLIST |Exclusivamente para uso interno.| 
|PREEMPTIVE_RESIZELOG |Exclusivamente para uso interno.| 
|PREEMPTIVE_ROLLFORWARDREDO |Exclusivamente para uso interno.| 
|PREEMPTIVE_ROLLFORWARDUNDO |Exclusivamente para uso interno.| 
|PREEMPTIVE_SB_STOPENDPOINT |Exclusivamente para uso interno.| 
|PREEMPTIVE_SERVER_STARTUP |Exclusivamente para uso interno.| 
|PREEMPTIVE_SETRMINFO |Exclusivamente para uso interno.| 
|PREEMPTIVE_SHAREDMEM_GETDATA |Exclusivamente para uso interno.| 
|PREEMPTIVE_SNIOPEN |Exclusivamente para uso interno.| 
|PREEMPTIVE_SOSHOST |Exclusivamente para uso interno.| 
|PREEMPTIVE_SOSTESTING |Solamente se identifica con fines informativos. No compatible. La compatibilidad con versiones posteriores no está garantizada.| 
|PREEMPTIVE_SP_SERVER_DIAGNOSTICS |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] y versiones posteriores.| 
|PREEMPTIVE_STARTRM |Exclusivamente para uso interno.| 
|PREEMPTIVE_STREAMFCB_CHECKPOINT |Exclusivamente para uso interno.| 
|PREEMPTIVE_STREAMFCB_RECOVER |Exclusivamente para uso interno.| 
|PREEMPTIVE_STRESSDRIVER |Solamente se identifica con fines informativos. No compatible. La compatibilidad con versiones posteriores no está garantizada.| 
|PREEMPTIVE_TESTING |Solamente se identifica con fines informativos. No compatible. La compatibilidad con versiones posteriores no está garantizada.| 
|PREEMPTIVE_TRANSIMPORT |Exclusivamente para uso interno.| 
|PREEMPTIVE_UNMARSHALPROPAGATIONTOKEN |Exclusivamente para uso interno.| 
|PREEMPTIVE_VSS_CREATESNAPSHOT |Exclusivamente para uso interno.| 
|PREEMPTIVE_VSS_CREATEVOLUMESNAPSHOT |Exclusivamente para uso interno.| 
|PREEMPTIVE_XE_CALLBACKEXECUTE |Exclusivamente para uso interno.| 
|PREEMPTIVE_XE_CX_FILE_OPEN |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] y versiones posteriores.| 
|PREEMPTIVE_XE_CX_HTTP_CALL |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] y versiones posteriores.| 
|PREEMPTIVE_XE_DISPATCHER |Exclusivamente para uso interno.| 
|PREEMPTIVE_XE_ENGINEINIT |Exclusivamente para uso interno.| 
|PREEMPTIVE_XE_GETTARGETSTATE |Exclusivamente para uso interno.| 
|PREEMPTIVE_XE_SESSIONCOMMIT |Exclusivamente para uso interno.| 
|PREEMPTIVE_XE_TARGETFINALIZE |Exclusivamente para uso interno.| 
|PREEMPTIVE_XE_TARGETINIT |Exclusivamente para uso interno.| 
|PREEMPTIVE_XE_TIMERRUN |Exclusivamente para uso interno.| 
|PREEMPTIVE_XETESTING |Solamente se identifica con fines informativos. No compatible. La compatibilidad con versiones posteriores no está garantizada.| 
|PRINT_ROLLBACK_PROGRESS |Se utiliza para esperar mientras los procesos del usuario finalizan en una base de datos que se ha pasado utilizando la cláusula de terminación ALTER DATABASE. Para obtener más información, consulte ALTER DATABASE (Transact-SQL).| 
|PRU_ROLLBACK_DEFERRED |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] y versiones posteriores.| 
|PWAIT_ALL_COMPONENTS_INITIALIZED |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] y versiones posteriores.| 
|PWAIT_COOP_SCAN |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] y versiones posteriores.| 
|PWAIT_DIRECTLOGCONSUMER_GETNEXT |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] y versiones posteriores.| 
|PWAIT_EVENT_SESSION_INIT_MUTEX |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] y versiones posteriores.| 
|PWAIT_FABRIC_REPLICA_CONTROLLER_DATA_LOSS |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] y versiones posteriores.| 
|PWAIT_HADR_ACTION_COMPLETED |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] y versiones posteriores.| 
|PWAIT_HADR_CHANGE_NOTIFIER_TERMINATION_SYNC |Tiene lugar cuando una tarea en segundo plano está esperando la finalización de la tarea en segundo plano que recibe las notificaciones de clústeres de conmutación por error de Windows Server (a través del sondeo). <br /> **Válido para** : [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] y versiones posteriores.| 
|PWAIT_HADR_CLUSTER_INTEGRATION |Una operación de anexar, reemplazar o quitar está esperando para obtener un bloqueo de escritura en una lista interna de Always On (como una lista de redes, direcciones de red o agentes de escucha del grupo de disponibilidad). Solo para uso interno, <br /> **Válido para** : [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] y versiones posteriores.| 
|PWAIT_HADR_FAILOVER_COMPLETED |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] y versiones posteriores.| 
|PWAIT_HADR_JOIN |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] y versiones posteriores.| 
|PWAIT_HADR_OFFLINE_COMPLETED |Un Always On operación Drop Availability Group está esperando a que el grupo de disponibilidad de destino se desconecte antes de destruir los objetos de clústeres de conmutación por error de Windows Server. <br /> **Válido para** : [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] y versiones posteriores.| 
|PWAIT_HADR_ONLINE_COMPLETED |Un Always On operación de creación o conmutación por error del grupo de disponibilidad está esperando a que el grupo de disponibilidad de destino se ponga en línea. <br /> **Válido para** : [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] y versiones posteriores.| 
|PWAIT_HADR_POST_ONLINE_COMPLETED |Una operación de Always On Drop Availability Group está esperando la finalización de cualquier tarea en segundo plano programada como parte de un comando anterior. Por ejemplo, el puede haber una tarea en segundo plano que esté pasando las bases de datos de disponibilidad al rol principal. El DDL DROP AVAILABILITY GROUP debe esperar a que finalice esta tarea en segundo plano para evitar las condiciones de carrera. <br /> **Válido para** : [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] y versiones posteriores.| 
|PWAIT_HADR_SERVER_READY_CONNECTIONS |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] y versiones posteriores.| 
|PWAIT_HADR_WORKITEM_COMPLETED |Espera interna de un subproceso que espera a que una tarea de trabajo asincrónico se complete. Se trata de una espera esperada y es para uso de CSS. <br /> **Válido para** : [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] y versiones posteriores.| 
|PWAIT_HADRSIM |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] y versiones posteriores.| 
|PWAIT_LOG_CONSOLIDATION_IO |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] y versiones posteriores.| 
|PWAIT_LOG_CONSOLIDATION_POLL |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] y versiones posteriores.| 
|PWAIT_MD_LOGIN_STATS |Tiene lugar durante la sincronización interna en los metadatos de las estadísticas de inicio de sesión. <br /> **Válido para** : [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] y versiones posteriores.| 
|PWAIT_MD_RELATION_CACHE |Tiene lugar durante la sincronización interna en los metadatos de la tabla o el índice. <br /> **Válido para** : [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] y versiones posteriores.| 
|PWAIT_MD_SERVER_CACHE |Tiene lugar durante la sincronización interna en los metadatos de los servidores vinculados. <br /> **Válido para** : [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] y versiones posteriores.| 
|PWAIT_MD_UPGRADE_CONFIG |Tiene lugar durante la sincronización interna al actualizar las configuraciones de todo el servidor. <br /> **Válido para** : [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] y versiones posteriores.| 
|PWAIT_PREEMPTIVE_APP_USAGE_TIMER |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] y versiones posteriores.| 
|PWAIT_PREEMPTIVE_AUDIT_ACCESS_WINDOWSLOG |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] y versiones posteriores.| 
|PWAIT_QRY_BPMEMORY |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] y versiones posteriores.| 
|PWAIT_REPLICA_ONLINE_INIT_MUTEX |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] y versiones posteriores.| 
|PWAIT_RESOURCE_SEMAPHORE_FT_PARALLEL_QUERY_SYNC |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] y versiones posteriores.| 
|PWAIT_SBS_FILE_OPERATION |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] y versiones posteriores.| 
|PWAIT_XTP_FSSTORAGE_MAINTENANCE |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] y versiones posteriores.| 
|PWAIT_XTP_HOST_STORAGE_WAIT |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] y versiones posteriores.| 
|QDS_ASYNC_CHECK_CONSISTENCY_TASK |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] y versiones posteriores.| 
|QDS_ASYNC_PERSIST_TASK |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] y versiones posteriores.| 
|QDS_ASYNC_PERSIST_TASK_START |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] y versiones posteriores.| 
|QDS_ASYNC_QUEUE |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] y versiones posteriores.| 
|QDS_BCKG_TASK |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] y versiones posteriores.| 
|QDS_BLOOM_FILTER |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] y versiones posteriores.| 
|QDS_CLEANUP_STALE_QUERIES_TASK_MAIN_LOOP_SLEEP |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] y versiones posteriores.| 
|QDS_CTXS |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] y versiones posteriores.| 
|QDS_DB_DISK |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] y versiones posteriores.| 
|QDS_DYN_VECTOR |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] y versiones posteriores.| 
|QDS_EXCLUSIVE_ACCESS |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] y versiones posteriores.| 
|QDS_HOST_INIT |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] y versiones posteriores.| 
|QDS_LOADDB |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] y versiones posteriores.| 
|QDS_PERSIST_TASK_MAIN_LOOP_SLEEP |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] y versiones posteriores.| 
|QDS_QDS_CAPTURE_INIT |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] y versiones posteriores.| 
|QDS_SHUTDOWN_QUEUE |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] y versiones posteriores.| 
|QDS_STMT |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] y versiones posteriores.| 
|QDS_STMT_DISK |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] y versiones posteriores.| 
|QDS_TASK_SHUTDOWN |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] y versiones posteriores.| 
|QDS_TASK_START |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] y versiones posteriores.| 
|QE_WARN_LIST_SYNC |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] y versiones posteriores.| 
|QPJOB_KILL |Indica que una llamada a KILL ha cancelado una actualización de estadísticas automáticas asincrónicas cuando la actualización se empezaba a ejecutar. El subproceso de terminación está suspendido, en espera de que empiece a escuchar comandos KILL. Un buen valor es menor que un segundo.| 
|QPJOB_WAITFOR_ABORT |Indica que una llamada a KILL ha cancelado una actualización de estadísticas automáticas asincrónicas cuando se estaba ejecutando. La actualización no se ha completado, sino que está suspendida hasta que finalice la coordinación del mensaje del subproceso de terminación. Es un estado normal, pero excepcional, y debe ser muy corto. Un buen valor es menor que un segundo.| 
|QRY_MEM_GRANT_INFO_MUTEX |Tiene lugar cuando la administración de memoria de ejecución de la consulta intenta controlar el acceso a la lista estática de información de concesiones. Este estado muestra información acerca de las solicitudes de memoria en espera y concedidas actualmente. Este estado es un sencillo estado de control de acceso. En este estado nunca debe esperarse mucho. Si esta exclusión mutua no se libera, todas las nuevas consultas que utilizan memoria dejarán de responder.| 
|QRY_PARALLEL_THREAD_MUTEX |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] y versiones posteriores.| 
|QRY_PROFILE_LIST_MUTEX |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] y versiones posteriores.| 
|QUERY_ERRHDL_SERVICE_DONE |Solamente se identifica con fines informativos. No compatible. <br /> Solo **se aplica a**: [!INCLUDE[ssKilimanjaro_md](../../includes/sskilimanjaro-md.md)] . |  
|QUERY_WAIT_ERRHDL_SERVICE |Solamente se identifica con fines informativos.  No compatible. <br /> Solo **se aplica a**: [!INCLUDE[ssKilimanjaro_md](../../includes/sskilimanjaro-md.md)] .  |  
|QUERY_EXECUTION_INDEX_SORT_EVENT_OPEN |Tiene lugar en determinados casos, cuando la generación de índices sin conexión se ejecuta en paralelo y los diferentes subprocesos de trabajo que realizan la ordenación sincronizan el acceso a los archivos de ordenación.| 
|QUERY_NOTIFICATION_MGR_MUTEX |Tiene lugar durante la sincronización de la recopilación de elementos no utilizados en el administrador de notificaciones de consulta.| 
|QUERY_NOTIFICATION_SUBSCRIPTION_MUTEX |Tiene lugar durante la sincronización del estado en las transacciones de notificaciones de consulta.| 
|QUERY_NOTIFICATION_TABLE_MGR_MUTEX |Tiene lugar durante la sincronización interna en el administrador de notificaciones de consulta.| 
|QUERY_NOTIFICATION_UNITTEST_MUTEX |Solamente se identifica con fines informativos. No compatible. La compatibilidad con versiones posteriores no está garantizada.| 
|QUERY_OPTIMIZER_PRINT_MUTEX |Tiene lugar durante la sincronización de la producción de salida de diagnóstico del optimizador de consultas. Este tipo de espera solo se produce si la configuración de diagnóstico se ha habilitado bajo la dirección del servicio de soporte técnico de Microsoft.| 
|QUERY_TASK_ENQUEUE_MUTEX |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] y versiones posteriores.| 
|QUERY_TRACEOUT |Solamente se identifica con fines informativos. No compatible. La compatibilidad con versiones posteriores no está garantizada.| 
|RBIO_WAIT_VLF |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] y versiones posteriores.| 
|RBIO_RG_STORAGE |Tiene lugar cuando se está limitando un nodo de proceso de base de datos de hiperescala debido al consumo de registro retrasado en los servidores de páginas. <br /> **Se aplica a**: Azure SQL Database hiperscale.|
|RBIO_RG_DESTAGE |Tiene lugar cuando se está limitando un nodo de proceso de base de datos de hiperescala debido al consumo de registro retrasado en el almacenamiento de registros a largo plazo. <br /> **Se aplica a**: Azure SQL Database hiperscale.|
|RBIO_RG_REPLICA |Tiene lugar cuando se está limitando un nodo de proceso de base de datos de hiperescala debido al consumo de registro retrasado por los nodos de la réplica secundaria legible. <br /> **Se aplica a**: Azure SQL Database hiperscale.|
|RBIO_RG_LOCALDESTAGE |Se produce cuando se está limitando un nodo de proceso de base de datos de hiperescala debido al consumo de registro retrasado por el servicio de registro. <br /> **Se aplica a**: Azure SQL Database hiperscale.|
|RECOVER_CHANGEDB |Tiene lugar durante la sincronización del estado de base de datos en una base de datos en estado de espera activa.| 
|RECOVERY_MGR_LOCK |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] y versiones posteriores.| 
|REDO_THREAD_PENDING_WORK |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] y versiones posteriores.| 
|REDO_THREAD_SYNC |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] y versiones posteriores.| 
|REMOTE_BLOCK_IO |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] y versiones posteriores.| 
|REMOTE_DATA_ARCHIVE_MIGRATION_DMV |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] y versiones posteriores.| 
|REMOTE_DATA_ARCHIVE_SCHEMA_DMV |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] y versiones posteriores.| 
|REMOTE_DATA_ARCHIVE_SCHEMA_TASK_QUEUE |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] y versiones posteriores.| 
|REPL_CACHE_ACCESS |Tiene lugar durante la sincronización en caché de artículos de una replicación. Durante estas esperas, el registro del LOG de replicación se detiene temporalmente y se bloquean las instrucciones de lenguaje de definición de datos (DLL) en una tabla publicada.| 
|REPL_HISTORYCACHE_ACCESS |Exclusivamente para uso interno.| 
|REPL_SCHEMA_ACCESS |Tiene lugar durante la sincronización de la información de versión del esquema de replicación. Este estado se produce cuando las instrucciones de DDL se ejecutan en el objeto replicado y cuando el registro del LOG genera o consume un esquema con versiones basado en las repeticiones de DDL. Se puede observar la contención en este tipo de espera si tiene muchas bases de datos publicadas en un único publicador con la replicación transaccional y las bases de datos publicadas están muy activas.| 
|REPL_TRANFSINFO_ACCESS |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] y versiones posteriores.| 
|REPL_TRANHASHTABLE_ACCESS |Exclusivamente para uso interno.| 
|REPL_TRANTEXTINFO_ACCESS |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] y versiones posteriores.| 
|REPLICA_WRITES |Tiene lugar mientras una tarea espera que finalicen las escrituras de página en instantáneas de la base de datos o en réplicas DBCC.| 
|REQUEST_DISPENSER_PAUSE |Tiene lugar cuando una tarea espera que finalicen todas las operaciones de E/S pendientes para poder inmovilizar la E/S en un archivo y realizar una copia de seguridad de instantánea.| 
|REQUEST_FOR_DEADLOCK_SEARCH |Tiene lugar mientras la supervisión de interbloqueos espera que comience la siguiente búsqueda de interbloqueos. Esta espera está prevista entre detecciones de interbloqueos; un tiempo de espera total largo en este recurso no indica un problema.| 
|RESERVED_MEMORY_ALLOCATION_EXT |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] y versiones posteriores.| 
|RESMGR_THROTTLED |Tiene lugar cuando entra una nueva solicitud y se acelera basándose en GROUP_MAX_REQUESTS.| 
|RESOURCE_GOVERNOR_IDLE |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] y versiones posteriores.| 
|RESOURCE_QUEUE |Tiene lugar durante la sincronización de diferentes colas internas de recursos.| 
|RESOURCE_SEMAPHORE |Tiene lugar cuando una solicitud de memoria de consulta no se puede conceder de forma inmediata debido a otras consultas simultáneas. Un número alto de esperas y tiempos de espera largos pueden indicar un número excesivo de consultas simultáneas o cantidades excesivas de solicitud de memoria.| 
|RESOURCE_SEMAPHORE_MUTEX |Tiene lugar mientras una consulta espera que se satisfaga su solicitud de reserva de subproceso. También se produce durante la sincronización de solicitudes de compilación de consultas y de concesión de memoria.| 
|RESOURCE_SEMAPHORE_QUERY_COMPILE |Tiene lugar cuando el número de compilaciones de consultas simultáneas alcanza un límite de aceleración. Un número alto de esperas y tiempos de espera largos pueden indicar compilaciones excesivas, recompilaciones o planes que no se pueden almacenar en caché.| 
|RESOURCE_SEMAPHORE_SMALL_QUERY |Tiene lugar cuando no se puede conceder de forma inmediata una solicitud de memoria de una consulta pequeña debido a otras consultas simultáneas. El tiempo de espera no debe superar unos segundos, ya que el servidor transfiere la solicitud al grupo principal de memoria de consulta si no puede conceder la memoria solicitada en este tiempo. Esperas altas pueden indicar un número excesivo de consultas pequeñas simultáneas y el bloqueo del grupo principal de memoria debido a consultas en espera. <br /> Solo **se aplica a**: [!INCLUDE[ssKilimanjaro_md](../../includes/sskilimanjaro-md.md)] . |  
|RESTORE_FILEHANDLECACHE_ENTRYLOCK |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] y versiones posteriores.| 
|RESTORE_FILEHANDLECACHE_LOCK |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] y versiones posteriores.| 
|RG_RECONFIG |Exclusivamente para uso interno.| 
|ROWGROUP_OP_STATS |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] y versiones posteriores.| 
|ROWGROUP_VERSION |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] y versiones posteriores.| 
|RTDATA_LIST |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] y versiones posteriores.| 
|SATELLITE_CARGO |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] y versiones posteriores.| 
|SATELLITE_SERVICE_SETUP |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] y versiones posteriores.| 
|SATELLITE_TASK |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] y versiones posteriores.| 
|SBS_DISPATCH |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] y versiones posteriores.| 
|SBS_RECEIVE_TRANSPORT |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] y versiones posteriores.| 
|SBS_TRANSPORT |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] y versiones posteriores.| 
|SCAN_CHAR_HASH_ARRAY_INITIALIZATION |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] y versiones posteriores.| 
|SEC_DROP_TEMP_KEY |Tiene lugar después de un error en el intento de quitar una clave de seguridad temporal y antes de volver a intentarlo.| 
|SECURITY_CNG_PROVIDER_MUTEX |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] y versiones posteriores.| 
|SECURITY_CRYPTO_CONTEXT_MUTEX |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] y versiones posteriores.| 
|SECURITY_DBE_STATE_MUTEX |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] y versiones posteriores.| 
|SECURITY_KEYRING_RWLOCK |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] y versiones posteriores.| 
|SECURITY_MUTEX |Tiene lugar cuando se esperan exclusiones mutuas que controlen el acceso a la lista global de proveedores de servicios criptográficos de Administración extensible de claves (EKM) y la lista de ámbito de sesión de sesiones de EKM.| 
|SECURITY_RULETABLE_MUTEX |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] y versiones posteriores.| 
|SEMPLAT_DSI_BUILD |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] y versiones posteriores.| 
|SEQUENCE_GENERATION |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] y versiones posteriores.| 
|SEQUENTIAL_GUID |Tiene lugar mientras se obtiene un nuevo GUID secuencial.| 
|SERVER_IDLE_CHECK |Tiene lugar durante la sincronización del estado inactivo de la instancia de SQL Server cuando un monitor de recursos intenta declarar una instancia de SQL Server como inactiva o intentando reactivarse.| 
|SERVER_RECONFIGURE |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] y versiones posteriores.| 
|SESSION_WAIT_STATS_CHILDREN |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] y versiones posteriores.| 
|SHARED_DELTASTORE_CREATION |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] y versiones posteriores.| 
|SHUTDOWN |Tiene lugar mientras una instrucción de cierre del sistema espera que las conexiones activas salgan.| 
|SLEEP_BPOOL_FLUSH |Tiene lugar cuando un punto de comprobación acelera la emisión de nuevas operaciones de E/S para evitar sobrecargar el subsistema del disco.| 
|SLEEP_BUFFERPOOL_HELPLW |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] y versiones posteriores.| 
|SLEEP_DBSTARTUP |Tiene lugar durante el inicio de la base de datos mientras se espera la recuperación de todas las bases de datos.| 
|SLEEP_DCOMSTARTUP |Se produce una vez como máximo durante el inicio de SQL Server instancia mientras espera a que se complete la inicialización de DCOM.| 
|SLEEP_MASTERDBREADY |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] y versiones posteriores.| 
|SLEEP_MASTERMDREADY |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] y versiones posteriores.| 
|SLEEP_MASTERUPGRADED |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] y versiones posteriores.| 
|SLEEP_MEMORYPOOL_ALLOCATEPAGES |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] y versiones posteriores.| 
|SLEEP_MSDBSTARTUP |Tiene lugar cuando Seguimiento de SQL espera a que la base de datos msdb complete su inicio.| 
|SLEEP_RETRY_VIRTUALALLOC |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] y versiones posteriores.| 
|SLEEP_SYSTEMTASK |Tiene lugar durante el inicio de una tarea en segundo plano mientras se espera que tempdb finalice el inicio.| 
|SLEEP_TASK |Tiene lugar cuando una tarea se mantiene inactiva mientras espera que se produzca un evento genérico.| 
|SLEEP_TEMPDBSTARTUP |Tiene lugar mientras una tarea espera que tempdb finalice el inicio.| 
|SLEEP_WORKSPACE_ALLOCATEPAGE |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] y versiones posteriores.| 
|SLO_UPDATE |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] y versiones posteriores.| 
|SMSYNC |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] y versiones posteriores.| 
|SNI_CONN_DUP |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] y versiones posteriores.| 
|SNI_CRITICAL_SECTION |Tiene lugar durante la sincronización interna en SQL Server componentes de red.| 
|SNI_HTTP_WAITFOR_0_DISCON |Tiene lugar durante el cierre de SQL Server, mientras se espera a que se cierren las conexiones HTTP pendientes.| 
|SNI_LISTENER_ACCESS |Tiene lugar mientras se espera que los nodos de acceso a memoria no uniforme (NUMA) actualicen el cambio de estado. El acceso al cambio de estado está serializado.| 
|SNI_TASK_COMPLETION |Tiene lugar cuando se espera que finalicen todas las tareas durante un cambio de estado del nodo NUMA.| 
|SNI_WRITE_ASYNC |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] y versiones posteriores.| 
|SOAP_READ |Tiene lugar mientras se espera que se complete una lectura de red HTTP.| 
|SOAP_WRITE |Tiene lugar mientras se espera que finalice una escritura de red HTTP.| 
|SOCKETDUPLICATEQUEUE_CLEANUP |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] y versiones posteriores.| 
|SOS_CALLBACK_REMOVAL |Tiene lugar mientras se lleva a cabo la sincronización en una lista de devoluciones de llamada para quitar una devolución de llamada. No se espera que este contador cambie una vez completada la inicialización del servidor.| 
|SOS_DISPATCHER_MUTEX |Tiene lugar durante la sincronización interna del grupo de distribuidores. Esto incluye el ajuste del grupo.| 
|SOS_LOCALALLOCATORLIST |Tiene lugar durante la sincronización interna en el administrador de memoria de [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]. <br /> Solo **se aplica a**: [!INCLUDE[ssKilimanjaro_md](../../includes/sskilimanjaro-md.md)] . |  
|SOS_MEMORY_TOPLEVELBLOCKALLOCATOR |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] y versiones posteriores.| 
|SOS_MEMORY_USAGE_ADJUSTMENT |Tiene lugar cuando se ajusta el uso de memoria entre los fondos.| 
|SOS_OBJECT_STORE_DESTROY_MUTEX |Tiene lugar durante la sincronización interna en grupos de memoria cuando se destruyen objetos del grupo.| 
|SOS_PHYS_PAGE_CACHE |Registra el tiempo que espera un subproceso para adquirir la exclusión mutua que debe adquirir antes de asignar páginas físicas o antes de devolver dichas páginas al sistema operativo. Las esperas de este tipo solo aparecen si la instancia de SQL Server usa la memoria AWE. <br /> **Válido para** : [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] y versiones posteriores.| 
|SOS_PROCESS_AFFINITY_MUTEX |Tiene lugar durante la sincronización del acceso a la configuración de afinidad de procesos.| 
|SOS_RESERVEDMEMBLOCKLIST |Tiene lugar durante la sincronización interna en el administrador de memoria de SQL Server. <br /> Solo **se aplica a**: [!INCLUDE[ssKilimanjaro_md](../../includes/sskilimanjaro-md.md)] . |  
|SOS_SCHEDULER_YIELD |Tiene lugar cuando una tarea genera de forma voluntaria el programador para que se ejecuten otras tareas. Mientras, la tarea espera la renovación de su cuanto.| 
|SOS_SMALL_PAGE_ALLOC |Tiene lugar durante la asignación y la liberación de la memoria que administran algunos objetos de memoria.| 
|SOS_STACKSTORE_INIT_MUTEX |Tiene lugar durante la sincronización de la inicialización de almacenamiento interno.| 
|SOS_SYNC_TASK_ENQUEUE_EVENT |Tiene lugar cuando una tarea se inicia de forma sincrónica. La mayoría de las tareas de SQL Server se inician de una manera asincrónica, en la que el control vuelve al iniciador inmediatamente después de que se haya colocado la solicitud de tarea en la cola de trabajo.| 
|SOS_VIRTUALMEMORY_LOW |Tiene lugar cuando una asignación de memoria espera que un administrador de recursos libere memoria virtual.| 
|SOSHOST_EVENT |Se produce cuando un componente hospedado, como CLR, espera un objeto de sincronización de eventos SQL Server.| 
|SOSHOST_INTERNAL |Tiene lugar durante la sincronización de devoluciones de llamada del administrador de memoria que utilizan los componentes hospedados, como CLR.| 
|SOSHOST_MUTEX |Se produce cuando un componente hospedado, como CLR, espera un objeto de sincronización de exclusión mutua SQL Server.| 
|SOSHOST_RWLOCK |Se produce cuando un componente hospedado, como CLR, espera un objeto de sincronización de lector-escritor SQL Server.| 
|SOSHOST_SEMAPHORE |Se produce cuando un componente hospedado, como CLR, espera un objeto de sincronización de semáforo SQL Server.| 
|SOSHOST_SLEEP |Tiene lugar cuando una tarea hospedada se mantiene inactiva mientras espera que se produzca un evento genérico. Las tareas hospedadas son las que utilizan los componentes hospedados, como CLR.| 
|SOSHOST_TRACELOCK |Tiene lugar durante la sincronización del acceso a flujos de seguimiento.| 
|SOSHOST_WAITFORDONE |Tiene lugar cuando un componente hospedado, como CLR, espera la finalización de una tarea.| 
|SP_PREEMPTIVE_SERVER_DIAGNOSTICS_SLEEP |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] y versiones posteriores.| 
|SP_SERVER_DIAGNOSTICS_BUFFER_ACCESS |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] y versiones posteriores.| 
|SP_SERVER_DIAGNOSTICS_INIT_MUTEX |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] y versiones posteriores.| 
|SP_SERVER_DIAGNOSTICS_SLEEP |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] y versiones posteriores.| 
|SQLCLR_APPDOMAIN |Tiene lugar mientras CLR espera que complete el inicio de un dominio de aplicación.| 
|SQLCLR_ASSEMBLY |Tiene lugar mientras se espera el acceso a la lista de ensamblados cargada en el dominio de aplicación.| 
|SQLCLR_DEADLOCK_DETECTION |Tiene lugar mientras CLR espera la finalización de la detección de interbloqueos.| 
|SQLCLR_QUANTUM_PUNISHMENT |Tiene lugar cuando una tarea de CLR se acelera porque ha sobrepasado su cuanto de ejecución. Esta aceleración se lleva a cabo para reducir el efecto de esta tarea que consume muchos recursos en otras tareas.| 
|SQLSORT_NORMMUTEX |Tiene lugar durante la sincronización interna, mientras se inicializan estructuras de ordenación internas.| 
|SQLSORT_SORTMUTEX |Tiene lugar durante la sincronización interna, mientras se inicializan estructuras de ordenación internas.| 
|SQLTRACE_BUFFER_FLUSH |Tiene lugar cuando una tarea está esperando a que una tarea en segundo plano vuelque los búferes de seguimiento al disco cada cuatro segundos. <br /> Solo **se aplica a**: [!INCLUDE[ssKilimanjaro_md](../../includes/sskilimanjaro-md.md)] . |  
|SQLTRACE_FILE_BUFFER |Tiene lugar durante la sincronización en búferes de seguimiento durante un seguimiento de archivos. <br /> **Válido para** : [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] y versiones posteriores.| 
|SQLTRACE_FILE_READ_IO_COMPLETION |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] y versiones posteriores.| 
|SQLTRACE_FILE_WRITE_IO_COMPLETION |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] y versiones posteriores.| 
|SQLTRACE_INCREMENTAL_FLUSH_SLEEP |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] y versiones posteriores.| 
|SQLTRACE_LOCK |Exclusivamente para uso interno. <br /> Solo **se aplica a**: [!INCLUDE[ssKilimanjaro_md](../../includes/sskilimanjaro-md.md)] . |  
|SQLTRACE_PENDING_BUFFER_WRITERS |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] y versiones posteriores.| 
|SQLTRACE_SHUTDOWN |Tiene lugar mientras el cierre del sistema de seguimiento espera la finalización de los eventos de seguimiento pendientes.| 
|SQLTRACE_WAIT_ENTRIES |Tiene lugar cuando una cola de eventos de Seguimiento de SQL espera que lleguen paquetes a la cola.| 
|SRVPROC_SHUTDOWN |Tiene lugar mientras el proceso de cierre del sistema espera la liberación de los recursos internos para cerrar sin problemas.| 
|STARTUP_DEPENDENCY_MANAGER |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] y versiones posteriores.| 
|TDS_BANDWIDTH_STATE |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] y versiones posteriores.| 
|TDS_INIT |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] y versiones posteriores.| 
|TDS_PROXY_CONTAINER |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] y versiones posteriores.| 
|TEMPOBJ |Tiene lugar cuando se sincronizan eliminaciones de objetos temporales. Esta espera no es muy común y solo se produce si una tarea ha solicitado el acceso exclusivo para eliminaciones de tablas temp.| 
|TEMPORAL_BACKGROUND_PROCEED_CLEANUP |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] y versiones posteriores.| 
|TERMINATE_LISTENER |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] y versiones posteriores.| 
|THREADPOOL |Tiene lugar cuando una tarea está esperando un trabajador en el que ejecutarse. Puede indicar que la configuración de número máximo de trabajadores es demasiado baja o que se tarda un tiempo inusualmente largo en las ejecuciones por lotes, lo que reduce el número de trabajadores disponibles para satisfacer otros lotes.| 
|TIMEPRIV_TIMEPERIOD |Tiene lugar durante la sincronización interna del temporizador de Extended Events.| 
|TRACE_EVTNOTIF |Exclusivamente para uso interno.| 
|TRACEWRITE |Tiene lugar cuando el proveedor de seguimiento de conjuntos de filas de Seguimiento de SQL espera un búfer libre o el procesamiento de un búfer con eventos.| 
|TRAN_MARKLATCH_DT |Tiene lugar cuando se espera un bloqueo temporal en modo de destrucción en un bloqueo temporal de marca de transacción. Los bloqueos temporales de marca de transacción se utilizan para la sincronización de confirmaciones con transacciones marcadas.| 
|TRAN_MARKLATCH_EX |Tiene lugar cuando se espera un bloqueo temporal en modo exclusivo en una transacción marcada. Los bloqueos temporales de marca de transacción se utilizan para la sincronización de confirmaciones con transacciones marcadas.| 
|TRAN_MARKLATCH_KP |Tiene lugar cuando se espera un bloqueo temporal en modo de mantenimiento en una transacción marcada. Los bloqueos temporales de marca de transacción se utilizan para la sincronización de confirmaciones con transacciones marcadas.| 
|TRAN_MARKLATCH_NL |Solamente se identifica con fines informativos. No compatible. La compatibilidad con versiones posteriores no está garantizada.| 
|TRAN_MARKLATCH_SH |Tiene lugar cuando se espera un bloqueo temporal en modo compartido en una transacción marcada. Los bloqueos temporales de marca de transacción se utilizan para la sincronización de confirmaciones con transacciones marcadas.| 
|TRAN_MARKLATCH_UP |Tiene lugar cuando se espera un bloqueo temporal en modo de actualización en una transacción marcada. Los bloqueos temporales de marca de transacción se utilizan para la sincronización de confirmaciones con transacciones marcadas.| 
|TRANSACTION_MUTEX |Tiene lugar durante la sincronización del acceso a una transacción por parte de varios lotes.| 
|UCS_ENDPOINT_CHANGE |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] y versiones posteriores.| 
|UCS_MANAGER |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] y versiones posteriores.| 
|UCS_MEMORY_NOTIFICATION |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] y versiones posteriores.| 
|UCS_SESSION_REGISTRATION |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] y versiones posteriores.| 
|UCS_TRANSPORT |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] y versiones posteriores.| 
|UCS_TRANSPORT_STREAM_CHANGE |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] y versiones posteriores.| 
|UTIL_PAGE_ALLOC |Tiene lugar cuando los exámenes del registro de transacciones esperan que haya memoria disponible durante la presión de memoria.| 
|VDI_CLIENT_COMPLETECOMMAND |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] y versiones posteriores.| 
|VDI_CLIENT_GETCOMMAND |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] y versiones posteriores.| 
|VDI_CLIENT_OPERATION |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] y versiones posteriores.| 
|VDI_CLIENT_OTHER |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] y versiones posteriores.| 
|VERSIONING_COMMITTING |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] y versiones posteriores.| 
|VIA_ACCEPT |Tiene lugar cuando se completa la conexión del proveedor del Adaptador de interfaz virtual (VIA) durante el inicio.| 
|VIEW_DEFINITION_MUTEX |Tiene lugar durante la sincronización del acceso a definiciones de vista almacenadas en memoria caché.| 
|WAIT_FOR_RESULTS |Tiene lugar cuando se espera el inicio de una notificación de consulta.| 
|WAIT_ON_SYNC_STATISTICS_REFRESH |Tiene lugar cuando se espera que se complete la actualización sincrónica de las estadísticas antes de que se pueda reanudar la compilación y la ejecución de la consulta.<br /> **Se aplica a: a**partir de[!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)]|
|WAIT_SCRIPTDEPLOYMENT_REQUEST |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] y versiones posteriores.| 
|WAIT_SCRIPTDEPLOYMENT_WORKER |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] y versiones posteriores.| 
|WAIT_XLOGREAD_SIGNAL |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] y versiones posteriores.| 
|WAIT_XTP_ASYNC_TX_COMPLETION |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] y versiones posteriores.| 
|WAIT_XTP_CKPT_AGENT_WAKEUP |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] y versiones posteriores.| 
|WAIT_XTP_CKPT_CLOSE |Tiene lugar cuando se espera que se complete un punto de control. <br /> **Válido para** : [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] y versiones posteriores.| 
|WAIT_XTP_CKPT_ENABLED |Se produce al deshabilitar los puntos de comprobación y esperar a que se habiliten los puntos de control. <br /> **Válido para** : [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] y versiones posteriores.| 
|WAIT_XTP_CKPT_STATE_LOCK |Se produce al sincronizar la comprobación del estado del punto de comprobación. <br /> **Válido para** : [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] y versiones posteriores.| 
|WAIT_XTP_COMPILE_WAIT |Exclusivamente para uso interno. <br /> **Se aplica a**: [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] y versiones posteriores.| 
|WAIT_XTP_GUEST |Se produce cuando el asignador de memoria de la base de datos debe dejar de recibir notificaciones de memoria insuficiente. <br /> **Válido para** : [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] y versiones posteriores.| 
|WAIT_XTP_HOST_WAIT |Se produce cuando el motor de base de datos desencadena las esperas e implementa el host. <br /> **Válido para** : [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] y versiones posteriores.| 
|WAIT_XTP_OFFLINE_CKPT_BEFORE_REDO |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] y versiones posteriores.| 
|WAIT_XTP_OFFLINE_CKPT_LOG_IO |Tiene lugar cuando el punto de comprobación sin conexión está esperando a que se complete la e/s de lectura de registro. <br /> **Válido para** : [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] y versiones posteriores.| 
|WAIT_XTP_OFFLINE_CKPT_NEW_LOG |Se produce cuando el punto de comprobación sin conexión está esperando a que se analicen nuevos registros. <br /> **Válido para** : [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] y versiones posteriores.| 
|WAIT_XTP_PROCEDURE_ENTRY |Se produce cuando un procedimiento Drop está esperando a que se completen todas las ejecuciones actuales de ese procedimiento. <br /> **Válido para** : [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] y versiones posteriores.| 
|WAIT_XTP_RECOVERY |Tiene lugar cuando la recuperación de la base de datos está esperando a que finalice la recuperación de objetos optimizados para memoria. <br /> **Válido para** : [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] y versiones posteriores.| 
|WAIT_XTP_SERIAL_RECOVERY |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] y versiones posteriores.| 
|WAIT_XTP_SWITCH_TO_INACTIVE |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] y versiones posteriores.| 
|WAIT_XTP_TASK_SHUTDOWN |Tiene lugar cuando se espera que se complete un subproceso de OLTP en memoria. <br /> **Válido para** : [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] y versiones posteriores.| 
|WAIT_XTP_TRAN_DEPENDENCY |Se produce al esperar las dependencias de la transacción. <br /> **Válido para** : [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] y versiones posteriores.| 
|WAITFOR |Se produce como resultado de una instrucción WAITFOR de Transact-SQL. La duración de la espera viene determinada por los parámetros de la instrucción. Se trata de una espera iniciada por el usuario.| 
|WAITFOR_PER_QUEUE |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] y versiones posteriores.| 
|WAITFOR_TASKSHUTDOWN |Solamente se identifica con fines informativos. No compatible. La compatibilidad con versiones posteriores no está garantizada.| 
|WAITSTAT_MUTEX |Tiene lugar durante la sincronización del acceso a la colección de estadísticas utilizadas para rellenar sys.dm_os_wait_stats.| 
|WCC |Solamente se identifica con fines informativos. No compatible. La compatibilidad con versiones posteriores no está garantizada.| 
|WINDOW_AGGREGATES_MULTIPASS |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] y versiones posteriores.| 
|WINFAB_API_CALL |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] y versiones posteriores.| 
|WINFAB_REPLICA_BUILD_OPERATION |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] y versiones posteriores.| 
|WINFAB_REPORT_FAULT |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] y versiones posteriores.| 
|WORKTBL_DROP |Tiene lugar mientras se establece una pausa antes de volver a intentar una eliminación incorrecta de tablas de trabajo.| 
|WRITE_COMPLETION |Tiene lugar mientras está en curso una operación de escritura.| 
|WRITELOG |Tiene lugar mientras se espera que se complete un vaciado del registro. Las operaciones habituales que provocan vaciados del registro son los puntos de comprobación y las confirmaciones de transacciones.| 
|XACT_OWN_TRANSACTION |Tiene lugar mientras se espera adquirir la propiedad de una transacción.| 
|XACT_RECLAIM_SESSION |Tiene lugar mientras se espera que el propietario actual de una sesión libere la propiedad de la sesión.| 
|XACTLOCKINFO |Tiene lugar durante la sincronización del acceso a la lista de bloqueos de una transacción. Además de la propia transacción, a la lista de bloqueos tienen acceso operaciones como la detección de interbloqueos y la migración de bloqueos durante divisiones de página.| 
|XACTWORKSPACE_MUTEX |Tiene lugar durante la sincronización de bajas de una transacción, así como del número de bloqueos de base de datos entre los miembros dados de alta de una transacción.| 
|XDB_CONN_DUP_HASH |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] y versiones posteriores.| 
|XDES_HISTORY |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] y versiones posteriores.| 
|XDES_OUT_OF_ORDER_LIST |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] y versiones posteriores.| 
|XDES_SNAPSHOT |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] y versiones posteriores.| 
|XDESTSVERMGR |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] y versiones posteriores.| 
|XE_BUFFERMGR_ALLPROCESSED_EVENT |Tiene lugar cuando los búferes de sesión de Extended Events se vacían en los destinos. Esta espera se produce en un subproceso en segundo plano.| 
|XE_BUFFERMGR_FREEBUF_EVENT |Tiene lugar cuando se presenta alguna de las siguientes condiciones:| 
|XE_CALLBACK_LIST |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] y versiones posteriores.| 
|XE_CX_FILE_READ |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] y versiones posteriores.| 
|XE_DISPATCHER_CONFIG_SESSION_LIST |Tiene lugar cuando una sesión de Extended Events que está utilizando destinos asincrónicos se inicia o se detiene. Esta espera indica alguna de las siguientes situaciones:| 
|XE_DISPATCHER_JOIN |Tiene lugar cuando un subproceso en segundo plano que se utiliza para sesiones de Extended Events está finalizando.| 
|XE_DISPATCHER_WAIT |Tiene lugar cuando un subproceso en segundo plano que se utiliza para sesiones de Extended Events está esperando a que se procesen los búferes de eventos.| 
|XE_FILE_TARGET_TVF |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] y versiones posteriores.| 
|XE_LIVE_TARGET_TVF |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] y versiones posteriores.| 
|XE_MODULEMGR_SYNC |Solamente se identifica con fines informativos. No compatible. La compatibilidad con versiones posteriores no está garantizada.| 
|XE_OLS_LOCK |Solamente se identifica con fines informativos. No compatible. La compatibilidad con versiones posteriores no está garantizada.| 
|XE_PACKAGE_LOCK_BACKOFF |Solamente se identifica con fines informativos. No compatible. <br /> Solo **se aplica a**: [!INCLUDE[ssKilimanjaro_md](../../includes/sskilimanjaro-md.md)] . |  
|XE_SERVICES_EVENTMANUAL |Exclusivamente para uso interno.| 
|XE_SERVICES_MUTEX |Exclusivamente para uso interno.| 
|XE_SERVICES_RWLOCK |Exclusivamente para uso interno.| 
|XE_SESSION_CREATE_SYNC |Exclusivamente para uso interno.| 
|XE_SESSION_FLUSH |Exclusivamente para uso interno.| 
|XE_SESSION_SYNC |Exclusivamente para uso interno.| 
|XE_STM_CREATE |Exclusivamente para uso interno.| 
|XE_TIMER_EVENT |Exclusivamente para uso interno.| 
|XE_TIMER_MUTEX |Exclusivamente para uso interno.| 
|XE_TIMER_TASK_DONE |Exclusivamente para uso interno.| 
|XIO_CREDENTIAL_MGR_RWLOCK |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] y versiones posteriores.| 
|XIO_CREDENTIAL_RWLOCK |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] y versiones posteriores.| 
|XIO_EDS_MGR_RWLOCK |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] y versiones posteriores.| 
|XIO_EDS_RWLOCK |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] y versiones posteriores.| 
|XIO_IOSTATS_BLOBLIST_RWLOCK |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] y versiones posteriores.| 
|XIO_IOSTATS_FCBLIST_RWLOCK |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] y versiones posteriores.| 
|XIO_LEASE_RENEW_MGR_RWLOCK |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] y versiones posteriores.| 
|XTP_HOST_DB_COLLECTION |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] y versiones posteriores.| 
|XTP_HOST_LOG_ACTIVITY |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] y versiones posteriores.| 
|XTP_HOST_PARALLEL_RECOVERY |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] y versiones posteriores.| 
|XTP_PREEMPTIVE_TASK |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] y versiones posteriores.| 
|XTP_TRUNCATION_LSN |Exclusivamente para uso interno. <br /> **Válido para** : [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] y versiones posteriores.| 
|XTPPROC_CACHE_ACCESS |Se produce cuando se obtiene acceso a todos los objetos de caché de procedimientos almacenados compilados de forma nativa. <br /> **Válido para** : [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] y versiones posteriores.| 
|XTPPROC_PARTITIONED_STACK_CREATE |Se produce al asignar estructuras de caché de procedimientos almacenados compilados de forma nativa por nodo NUMA (debe realizarse con un solo subproceso) para un procedimiento determinado. <br /> **Válido para** : [!INCLUDE[ssSQL12](../../includes/sssql11-md.md)] y versiones posteriores.|

  
 Los siguientes XEvents están relacionados con el **modificador** de partición y la regeneración de índices en línea. Para obtener información sobre la sintaxis, vea [ALTER TABLE &#40;Transact-sql&#41;](../../t-sql/statements/alter-table-transact-sql.md) y [ALTER index &#40;transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md).  
  
-   lock_request_priority_state  
  
-   process_killed_by_abort_blockers  
  
-   ddl_with_wait_at_low_priority  
  
 Para obtener una matriz de compatibilidad de bloqueos, vea [Sys. dm_tran_locks &#40;&#41;de Transact-SQL ](../../relational-databases/system-dynamic-management-views/sys-dm-tran-locks-transact-sql.md).  
  
## <a name="see-also"></a>Consulte también  
    
 [SQL Server vistas de administración dinámica relacionadas con el sistema operativo &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)   
 [Sys. dm_exec_session_wait_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-session-wait-stats-transact-sql.md)   
 [Sys. dm_db_wait_stats &#40;Azure SQL Database&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-wait-stats-azure-sql-database.md)  
  
  


