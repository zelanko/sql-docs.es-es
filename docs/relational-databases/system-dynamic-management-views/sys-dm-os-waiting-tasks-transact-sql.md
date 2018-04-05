---
title: sys.dm_os_waiting_tasks (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/13/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
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
caps.latest.revision: 30
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 9c21fa8cd03079695ddc8b94e9b2dc2ab105b2b5
ms.sourcegitcommit: 8b332c12850c283ae413e0b04b2b290ac2edb672
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/05/2018
---
# <a name="sysdmoswaitingtasks-transact-sql"></a>sys.dm_os_waiting_tasks (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Devuelve información sobre la cola de tareas que están esperando en algún recurso.  
  
> [!NOTE]  
>  Para llamar a esta desde [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] o [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], use el nombre **sys.dm_pdw_nodes_os_waiting_tasks**.  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**waiting_task_address**|**varbinary(8)**|Dirección de la tarea a la espera.|  
|**session_id**|**smallint**|Id. de la sesión asociada a la tarea.|  
|**exec_context_id**|**int**|Id. del contexto de ejecución asociado a la tarea.|  
|**wait_duration_ms**|**bigint**|Tiempo de espera total para este tipo de espera, en milisegundos. Este tiempo es incluye **signal_wait_time**.|  
|**wait_type**|**nvarchar(60)**|Nombre del tipo de espera.|  
|**resource_address**|**varbinary(8)**|Dirección del recurso por el que la tarea está esperando.|  
|**blocking_task_address**|**varbinary(8)**|Tarea que alberga actualmente este recurso.|  
|**blocking_session_id**|**smallint**|Id. de la sesión que bloquea la solicitud. Si esta columna es NULL, la solicitud no está bloqueada o la información de la sesión de bloqueo no está disponible (o no puede ser identificada).<br /><br /> -2 = El recurso de bloqueo es propiedad de una transacción distribuida huérfana.<br /><br /> -3 = El recurso de bloqueo es propiedad de una transacción de recuperación diferida.<br /><br /> -4 = No se pudo determinar el Id. de sesión del propietario del bloqueo temporal a causa de transiciones internas de estado del bloqueo temporal.|  
|**blocking_exec_context_id**|**int**|Id. del contexto de ejecución de la tarea de bloqueo.|  
|**resource_description**|**nvarchar(3072)**|Descripción del recurso utilizado. Para obtener más información, vea la siguiente lista:|  
|**pdw_node_id**|**int**|**Se aplica a**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> El identificador para el nodo que se encuentra en esta distribución.|  
  
## <a name="resourcedescription-column"></a>Columna resource_description  
 La columna resource_description tiene los siguientes valores posibles.  
  
 **Propietario del recurso de grupo de subprocesos:**  
  
-   Id. de grupo de subprocesos = programador\<hex-address >  
  
 **Propietario del recurso de consultas en paralelo:**  
  
-   exchangeEvent id={Port|Pipe}\<hex-address> WaitType=\<exchange-wait-type> nodeId=\<exchange-node-id>  
  
 **Exchange-wait-type:**  
  
-   e_waitNone  
  
-   e_waitPipeNewRow  
  
-   e_waitPipeGetRow  
  
-   e_waitSynchronizeConsumerOpen  
  
-   e_waitPortOpen  
  
-   e_waitPortClose  
  
-   e_waitRange  
  
 **Propietario del recurso de bloqueo:**  
  
-   \<type-specific-description> id=lock\<lock-hex-address> mode=\<mode> associatedObjectId=\<associated-obj-id>  
  
     **\<tipo-specific-description > puede ser:**  
  
    -   For DATABASE: databaselock subresource=\<databaselock-subresource> dbid=\<db-id>  
  
    -   ARCHIVO: Filelock fileid =\<archivo-id > subresource =\<filelock-subresource > dbid =\<db-id >  
  
    -   Object: Objectlock lockPartition =\<lock-partition-id > objid =\<obj-id > subresource =\<objectlock-subresource > dbid =\<db-id >  
  
    -   Para PAGE: Pagelock fileid =\<archivo-id > pageid =\<Id. de página > dbid =\<db-id > subresource =\<pagelock-subresource >  
  
    -   Key: Keylock hobtid =\<hobt-id > dbid =\<db-id >  
  
    -   Para EXTENT: Extentlock fileid =\<archivo-id > pageid =\<Id. de página > dbid =\<db-id >  
  
    -   RID: Ridlock fileid =\<archivo-id > pageid =\<Id. de página > dbid =\<db-id >  
  
    -   Application: Applicationlock hash =\<hash > databasePrincipalId =\<rol-id > dbid =\<db-id >  
  
    -   For METADATA: metadatalock subresource=\<metadata-subresource> classid=\<metadatalock-description> dbid=\<db-id>  
  
    -   For HOBT: hobtlock hobtid=\<hobt-id> subresource=\<hobt-subresource> dbid=\<db-id>  
  
    -   Para ALLOCATION_UNIT: Allocunitlock hobtid =\<hobt-id > subresource =\<alloc-unit-subresource > dbid =\<db-id >  
  
     **\<modo > puede ser:**  
  
     Sch-S, Sch-M, S, U, X, IS, IU, IX, SIU, SIX, UIX, BU, RangeS-S, RangeS-U, RangeI-N, RangeI-S, RangeI-U, RangeI-X, RangeX-, RangeX-U, RangeX-X  
  
 **Propietario de un recurso externo:**  
  
-   ExternalResource externo =\<tipo de espera >  
  
 **Propietario de recurso genérico:**  
  
-   TransactionMutex TransactionInfo Workspace=\<workspace-id>  
  
-   Mutex  
  
-   CLRTaskJoin  
  
-   CLRMonitorEvent  
  
-   CLRRWLockEvent  
  
-   resourceWait  
  
 **Propietario del recurso de bloqueo temporal:**  
  
-   \<db-id>:\<file-id>:\<page-in-file>  
  
-   \<GUID>  
  
-   \<latch-class> (\<latch-address>)  
  
## <a name="permissions"></a>Permissions

En [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], requiere `VIEW SERVER STATE` permiso.   
En [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)], requiere el `VIEW DATABASE STATE` permiso en la base de datos.   
 
## <a name="example"></a>Ejemplo
Este ejemplo identifica las sesiones bloqueadas.  Ejecute el [!INCLUDE[tsql](../../includes/tsql-md.md)] consultas [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].
```sql
SELECT * FROM sys.dm_os_waiting_tasks 
WHERE blocking_session_id IS NOT NULL; 
``` 
  
## <a name="see-also"></a>Vea también  
  [Vistas de administración dinámica relacionadas con el sistema operativo SQL Server &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)  
  
  


