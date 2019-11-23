---
title: sys.dm_os_waiting_tasks (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/13/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_os_waiting_tasks
- sys.dm_os_waiting_tasks_TSQL
- dm_os_waiting_tasks_TSQL
- sys.dm_os_waiting_tasks
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_waiting_tasks dynamic management view
ms.assetid: ca5e6844-368c-42e2-b187-6e5f5afc8df3
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: c0a89a48fa960812ee955cd3b7ecb30069161f61
ms.sourcegitcommit: aece9f7db367098fcc0c508209ba243e05547fe1
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/11/2019
ms.locfileid: "72260380"
---
# <a name="sysdm_os_waiting_tasks-transact-sql"></a>sys.dm_os_waiting_tasks (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Devuelve información sobre la cola de tareas que están esperando en algún recurso. Para obtener más información acerca de las tareas, vea la [Guía de arquitectura de subprocesos y tareas](../../relational-databases/thread-and-task-architecture-guide.md).
   
> [!NOTE]  
>  Para llamarlo desde [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] o [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], utilice el nombre **Sys. dm_pdw_nodes_os_waiting_tasks**.  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**waiting_task_address**|**varbinary(8)**|Dirección de la tarea a la espera.|  
|**session_id**|**smallint**|Id. de la sesión asociada a la tarea.|  
|**exec_context_id**|**int**|Id. del contexto de ejecución asociado a la tarea.|  
|**wait_duration_ms**|**bigint**|Tiempo de espera total para este tipo de espera, en milisegundos. Esta hora es inclusiva de **signal_wait_time**.|  
|**wait_type**|**nvarchar(60)**|Nombre del tipo de espera.|  
|**resource_address**|**varbinary(8)**|Dirección del recurso por el que la tarea está esperando.|  
|**blocking_task_address**|**varbinary(8)**|Tarea que alberga actualmente este recurso.|  
|**blocking_session_id**|**smallint**|Id. de la sesión que bloquea la solicitud. Si esta columna es NULL, la solicitud no está bloqueada o la información de la sesión de bloqueo no está disponible (o no puede ser identificada).<br /><br /> -2 = El recurso de bloqueo es propiedad de una transacción distribuida huérfana.<br /><br /> -3 = El recurso de bloqueo es propiedad de una transacción de recuperación diferida.<br /><br /> -4 = No se pudo determinar el Id. de sesión del propietario del bloqueo temporal a causa de transiciones internas de estado del bloqueo temporal.|  
|**blocking_exec_context_id**|**int**|Id. del contexto de ejecución de la tarea de bloqueo.|  
|**resource_description**|**nvarchar(3072)**|Descripción del recurso utilizado. Para obtener más información, vea la siguiente lista:|  
|**pdw_node_id**|**int**|**Se aplica a**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> Identificador del nodo en el que se encuentra esta distribución.|  
  
## <a name="resource_description-column"></a>Columna resource_description  
 La columna resource_description tiene los siguientes valores posibles.  
  
 **Propietario del recurso de grupo de subprocesos:**  
  
-   ThreadPool ID = Scheduler\<dirección Hex >  
  
 **Propietario del recurso de consulta en paralelo:**  
  
-   exchangeEvent ID = {puerto | Pipe}\<dirección Hex > WaitType =\<Exchange-wait-Type > nodeId =\<Exchange-node-ID >  
  
 **Exchange-wait-Type:**  
  
-   e_waitNone  
  
-   e_waitPipeNewRow  
  
-   e_waitPipeGetRow  
  
-   e_waitSynchronizeConsumerOpen  
  
-   e_waitPortOpen  
  
-   e_waitPortClose  
  
-   e_waitRange  
  
 **Propietario del recurso de bloqueo:**  
  
-   \<Type-specific-Description > ID = Lock\<Lock-Hex-Address > Mode =\<Mode > associatedObjectId =\<asoció-obj-ID >  
  
     **\<> de Descripción específica del tipo puede ser:**  
  
    -   En DATABASE: databaselock subresource =\<databaselock-subresource > DBID =\<dB-ID >  
  
    -   En FILE: FileLock fileid =\<ID. de archivo > subresource =\<FileLock-subresource > DBID =\<dB-ID >  
  
    -   Para OBJECT: objectlock lockPartition =\<Lock-Partition-ID > objid =\<obj-ID > subresource =\<objectlock-subresource > DBID =\<dB-ID >  
  
    -   En la página: pagelock fileid =\<ID. de archivo > pageId =\<ID. de página > DBID =\<dB-ID > subresource =\<pagelock-subresource >  
  
    -   En Key: Keylock hobtid =\<hobt-ID > DBID =\<dB-ID >  
  
    -   Para extent: extentlock fileid =\<ID. de archivo > pageId =\<ID. de página > DBID =\<dB-ID >  
  
    -   Para RID: ridlock fileid =\<ID. de archivo > pageId =\<ID. de página > DBID =\<dB-ID >  
  
    -   Para APPLICATION: applicationlock hash =\<hash > databasePrincipalId =\<ID. de rol > DBID =\<dB-ID >  
  
    -   En el caso de metadatos: metadatalock subresource =\<Metadata-subresource > classid =\<metadatalock-Description > DBID =\<dB-ID >  
  
    -   Para HOBT: hobtlock hobtid =\<HOBT-ID > subresource =\<HOBT-subresource > DBID =\<dB-ID >  
  
    -   Por ALLOCATION_UNIT: allocunitlock hobtid =\<hobt-ID > subresource =\<Alloc-Unit-subresource > DBID =\<dB-ID >  
  
     **el modo de \<> puede ser:**  
  
     Sch-S, Sch-M, S, U, X, IS, IU, IX, SIU, SIX, UIX, BU, RangeS-S, RangeS-U, RangeI-N, RangeI-S, RangeI-U, RangeI-X, RangeX-, RangeX-U, RangeX-X  
  
 **Propietario del recurso externo:**  
  
-   External ExternalResource =\<tipo de espera >  
  
 **Propietario de recurso genérico:**  
  
-   TransactionMutex TransactionInfo Workspace =\<Workspace-ID >  
  
-   Mutex  
  
-   CLRTaskJoin  
  
-   CLRMonitorEvent  
  
-   CLRRWLockEvent  
  
-   resourceWait  
  
 **Propietario del recurso de bloqueo temporal:**  
  
-   \<db-id>:\<file-id>:\<page-in-file>  
  
-   \<GUID>  
  
-   \<latch-class> (\<latch-address>)  
  
## <a name="permissions"></a>Permisos

En [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], requiere `VIEW SERVER STATE` permiso.   
En [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] niveles Premium, requiere el permiso `VIEW DATABASE STATE` en la base de datos. En [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] los niveles estándar y básico, requiere el **Administrador del servidor** o una cuenta de **Administrador de Azure Active Directory** .   
 
## <a name="example"></a>Ejemplo
En este ejemplo se identificarán las sesiones bloqueadas. Ejecute la consulta [!INCLUDE[tsql](../../includes/tsql-md.md)] en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].

```sql
SELECT * FROM sys.dm_os_waiting_tasks 
WHERE blocking_session_id IS NOT NULL; 
``` 
  
## <a name="see-also"></a>Vea también  
[SQL Server &#40;vistas de administración dinámica relacionadas con el sistema operativo&#41;     Transact-SQL](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)  
[Guía de arquitectura de subprocesos y tareas](../../relational-databases/thread-and-task-architecture-guide.md)     
   
 
