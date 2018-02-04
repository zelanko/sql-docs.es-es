---
title: sys.dm_os_tasks (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/13/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.dm_os_tasks
- sys.dm_os_tasks_TSQL
- dm_os_tasks_TSQL
- dm_os_tasks
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_tasks dynamic management view
ms.assetid: 180a3c41-e71b-4670-819d-85ea7ef98bac
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b2fd7607fb0e22206ce309bd30427ba3f8dc7631
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/03/2018
---
# <a name="sysdmostasks-transact-sql"></a>sys.dm_os_tasks (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Devuelve una fila por cada tarea activa en la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!NOTE]  
>  Para llamar a esta desde [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] o [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], use el nombre **sys.dm_pdw_nodes_os_tasks**.  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**task_address**|**varbinary(8)**|Dirección de memoria del objeto.|  
|**task_state**|**nvarchar(60)**|Estado de la tarea. Puede ser uno de los siguientes:<br /><br /> PENDING: esperando un subproceso de trabajo.<br /><br /> RUNNABLE: se puede ejecutar, pero está esperando a recibir un cuanto.<br /><br /> RUNNING: ejecutándose actualmente en el programador.<br /><br /> SUSPENDED: tiene un trabajador, pero está esperando un evento.<br /><br /> DONE: completado.<br /><br /> SPINLOOP: atrapado en un subproceso.|  
|**context_switches_count**|**int**|Número de cambios de contexto del programador que esta tarea ha completado.|  
|**pending_io_count**|**int**|Número de entradas y salidas físicas realizadas por esta tarea.|  
|**pending_io_byte_count**|**bigint**|Recuento total de bytes de las entradas y salidas realizadas por esta tarea.|  
|**pending_io_byte_average**|**int**|Recuento promedio de bytes de las entradas y salidas realizadas por esta tarea.|  
|**scheduler_id**|**int**|Id. del programador primario. Es un identificador de la información del programador para esta tarea. Para obtener más información, consulte [sys.dm_os_schedulers &#40; Transact-SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-os-schedulers-transact-sql.md).|  
|**session_id**|**smallint**|Id. de la sesión que está asociada a la tarea.|  
|**exec_context_id**|**int**|Id. del contexto de ejecución que está asociado a la tarea.|  
|**request_id**|**int**|Id. de la solicitud de la tarea. Para obtener más información, consulte [sys.dm_exec_requests &#40; Transact-SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md).|  
|**worker_address**|**varbinary(8)**|Dirección de memoria del trabajador que ejecuta la tarea.<br /><br /> NULL = La tarea espera un trabajador que pueda ejecutarla o la tarea acaba de finalizar la ejecución.<br /><br /> Para obtener más información, consulte [sys.dm_os_workers &#40; Transact-SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-os-workers-transact-sql.md).|  
|**host_address**|**varbinary(8)**|Dirección de memoria del host.<br /><br /> 0 = No se ha usado el hospedaje para crear la tarea. Esto ayuda a identificar el host que se ha utilizado para crear esta tarea.<br /><br /> Para obtener más información, consulte [sys.dm_os_hosts &#40; Transact-SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-os-hosts-transact-sql.md).|  
|**parent_task_address**|**varbinary(8)**|Dirección de memoria de la tarea que es el elemento primario del objeto.|  
|**pdw_node_id**|**int**|**Se aplica a**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> El identificador para el nodo que se encuentra en esta distribución.|  
  
## <a name="permissions"></a>Permissions  
En [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], requiere `VIEW SERVER STATE` permiso.   
En [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] niveles de Premium, requieren la `VIEW DATABASE STATE` permiso en la base de datos. En [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] niveles estándar y básico, requiere la **administrador del servidor** o un **Administrador de Azure Active Directory** cuenta.   
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-monitoring-parallel-requests"></a>A. Supervisar solicitudes paralelas  
 Para las solicitudes que se ejecutan en paralelo, verá varias filas para la misma combinación de (\<**session_id**>, \< **request_id**>). Utilice la siguiente consulta para buscar el [configurar la max degree of parallelism Server Configuration Option](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md) para todas las solicitudes activas.  
  
> [!NOTE]  
>  A **request_id** es único dentro de una sesión.  
  
```  
SELECT  
    task_address,  
    task_state,  
    context_switches_count,  
    pending_io_count,  
    pending_io_byte_count,  
    pending_io_byte_average,  
    scheduler_id,  
    session_id,  
    exec_context_id,  
    request_id,  
    worker_address,  
    host_address  
  FROM sys.dm_os_tasks  
  ORDER BY session_id, request_id;  
```  
  
### <a name="b-associating-session-ids-with-windows-threads"></a>B. Asociar identificadores de sesión con subprocesos de Windows  
 Puede utilizar la siguiente consulta para asociar un valor de identificador de sesión a un identificador de subproceso de Windows. A continuación, puede supervisar el rendimiento del subproceso en el Monitor de rendimiento de Windows. La siguiente consulta no devuelve información para sesiones en espera.  
  
```  
SELECT STasks.session_id, SThreads.os_thread_id  
  FROM sys.dm_os_tasks AS STasks  
  INNER JOIN sys.dm_os_threads AS SThreads  
    ON STasks.worker_address = SThreads.worker_address  
  WHERE STasks.session_id IS NOT NULL  
  ORDER BY STasks.session_id;  
GO  
```  
  
## <a name="see-also"></a>Vea también  
  [Sistema operativo SQL Server relacionadas con vistas de administración dinámica &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)  
  
  


