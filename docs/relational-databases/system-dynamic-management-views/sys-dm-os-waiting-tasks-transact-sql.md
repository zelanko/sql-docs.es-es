---
title: Sys. dm_os_waiting_tasks (Transact-SQL) | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "72260380"
---
# <a name="sysdm_os_waiting_tasks-transact-sql"></a>sys.dm_os_waiting_tasks (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Devuelve información sobre la cola de tareas que están esperando en algún recurso. Para obtener más información acerca de las tareas, vea la [Guía de arquitectura de subprocesos y tareas](../../relational-databases/thread-and-task-architecture-guide.md).
   
> [!NOTE]  
>  Para llamar a este [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] método [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]desde o, use el nombre **Sys. dm_pdw_nodes_os_waiting_tasks**.  
  
|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**waiting_task_address**|**varbinary(8**|Dirección de la tarea a la espera.|  
|**session_id**|**smallint**|Id. de la sesión asociada a la tarea.|  
|**exec_context_id**|**int**|Id. del contexto de ejecución asociado a la tarea.|  
|**wait_duration_ms**|**bigint**|Tiempo de espera total para este tipo de espera, en milisegundos. Esta hora es inclusiva de **signal_wait_time**.|  
|**wait_type**|**nvarchar(60)**|Nombre del tipo de espera.|  
|**resource_address**|**varbinary(8**|Dirección del recurso por el que la tarea está esperando.|  
|**blocking_task_address**|**varbinary(8**|Tarea que alberga actualmente este recurso.|  
|**blocking_session_id**|**smallint**|Id. de la sesión que bloquea la solicitud. Si esta columna es NULL, la solicitud no está bloqueada o la información de la sesión de bloqueo no está disponible (o no puede ser identificada).<br /><br /> -2 = El recurso de bloqueo es propiedad de una transacción distribuida huérfana.<br /><br /> -3 = El recurso de bloqueo es propiedad de una transacción de recuperación diferida.<br /><br /> -4 = No se pudo determinar el Id. de sesión del propietario del bloqueo temporal a causa de transiciones internas de estado del bloqueo temporal.|  
|**blocking_exec_context_id**|**int**|Id. del contexto de ejecución de la tarea de bloqueo.|  
|**resource_description**|**nvarchar (a.**|Descripción del recurso utilizado. Para obtener más información, vea la siguiente lista:|  
|**pdw_node_id**|**int**|**Se aplica a**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)],[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> Identificador del nodo en el que se encuentra esta distribución.|  
  
## <a name="resource_description-column"></a>Columna resource_description  
 La columna resource_description tiene los siguientes posibles valores.  
  
 **Propietario del recurso de grupo de subprocesos:**  
  
-   ThreadPool ID =>\<de dirección Hex del programador  
  
 **Propietario del recurso de consulta en paralelo:**  
  
-   exchangeEvent ID = {puerto | Canalización\<} Hex-Address> WaitType\<= Exchange-wait-Type> nodeId\<= Exchange-node-ID>  
  
 **Exchange-wait-type:**  
  
-   e_waitNone  
  
-   e_waitPipeNewRow  
  
-   e_waitPipeGetRow  
  
-   e_waitSynchronizeConsumerOpen  
  
-   e_waitPortOpen  
  
-   e_waitPortClose  
  
-   e_waitRange  
  
 **Propietario de recurso de bloqueo:**  
  
-   \<Type-specific-Description> ID =\<Lock Lock-Hex-Address> Mode\<= Mode> associatedObjectId\<= asoció-obj-ID>  
  
     **\<el> de Descripción específica del tipo puede ser:**  
  
    -   En DATABASE: databaselock subresource =\<databaselock-subresource> DBID =\<dB-ID>  
  
    -   En FILE: FileLock fileid =\<File-ID> subresource =\<filelock-subresource> DBID =\<dB-ID>  
  
    -   Para OBJECT: objectlock lockPartition =\<Lock-Partition-ID> objid =\<obj-ID> subresource =\<objectlock-subresource> DBID =\<dB-ID>  
  
    -   En PAGE: pagelock fileid =\<File-ID> pageId =\<Page-ID> DBID =\<dB-ID> subresource =\<pagelock-subresource>  
  
    -   En Key: Keylock hobtid =\<hobt-ID> DBID =\<dB-ID>  
  
    -   Para extent: extentlock fileid\<= File-ID> pageId\<= id. de página>\<DBID = dB-ID>  
  
    -   Para RID: ridlock fileid =\<ID. de archivo> pageId\<= id. de página>\<DBID = dB-ID>  
  
    -   Para APPLICATION: applicationlock hash =\<hash> databasePrincipalId =\<role-ID> DBID =\<dB-ID>  
  
    -   En el caso de metadatos:\<metadatalock subresource = Metadata-subresource> classid =\<metadatalock-\<Description> DBID = dB-ID>  
  
    -   Para HOBT: hobtlock hobtid =\<HOBT-ID> subresource =\<HOBT-subresource> DBID =\<dB-ID>  
  
    -   Por ALLOCATION_UNIT: allocunitlock hobtid =\<hobt-ID> subresource =\<Alloc-UNIT-subresource> DBID =\<dB-ID>  
  
     **\<el modo> puede ser:**  
  
     Sch-S, Sch-M, S, U, X, IS, IU, IX, SIU, SIX, UIX, BU, RangeS-S, RangeS-U, RangeI-N, RangeI-S, RangeI-U, RangeI-X, RangeX-, RangeX-U, RangeX-X  
  
 **Propietario de recurso externo:**  
  
-   External ExternalResource =\<wait-Type>  
  
 **Propietario de recurso genérico:**  
  
-   TransactionMutex TransactionInfo Workspace =\<Workspace-ID>  
  
-   Mutex  
  
-   CLRTaskJoin  
  
-   CLRMonitorEvent  
  
-   CLRRWLockEvent  
  
-   resourceWait  
  
 **Propietario de recurso de bloqueo temporal:**  
  
-   \<dB-ID>:\<ID. de archivo>\<: página en archivo>  
  
-   \<GUID>  
  
-   \<> de clase de bloqueo\<temporal (> de dirección de bloqueo temporal)  
  
## <a name="permissions"></a>Permisos

En [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], requiere `VIEW SERVER STATE` el permiso.   
En [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] los niveles Premium, requiere el `VIEW DATABASE STATE` permiso en la base de datos. En [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] los niveles estándar y básico, requiere el **Administrador del servidor** o una cuenta de **Administrador de Azure Active Directory** .   
 
## <a name="example"></a>Ejemplo
En este ejemplo se identificarán las sesiones bloqueadas. Ejecute la [!INCLUDE[tsql](../../includes/tsql-md.md)] consulta en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].

```sql
SELECT * FROM sys.dm_os_waiting_tasks 
WHERE blocking_session_id IS NOT NULL; 
``` 
  
## <a name="see-also"></a>Consulte también  
[SQL Server vistas de administración dinámica relacionadas con el sistema operativo &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)      
[Guía de arquitectura de subprocesos y tareas](../../relational-databases/thread-and-task-architecture-guide.md)     
   
 
