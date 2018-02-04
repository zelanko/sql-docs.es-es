---
title: sys.dm_os_nodes (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/19/2017
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
- sys.dm_os_nodes
- dm_os_nodes_TSQL
- dm_os_nodes
- sys.dm_os_nodes_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_nodes dynamic management view
ms.assetid: c768b67c-82a4-47f5-850b-0ea282358d50
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f2abdd42300c8264f87513f428c7c6f4aa22645d
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/03/2018
---
# <a name="sysdmosnodes-transact-sql"></a>sys.dm_os_nodes (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Un componente interno denominado SQLOS crea las estructuras de nodo que imitan el procesador de hardware. Estas estructuras se pueden cambiar utilizando NUMA de software para crear los diseños de nodo personalizados.  
  
 En la tabla siguiente se proporciona información acerca de estos nodos.  
  
> **Nota:** para llamar a esta DMV de [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] o [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], use el nombre **sys.dm_pdw_nodes_os_nodes**.  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|node_id|**smallint**|Identificador del nodo.|  
|node_state_desc|**nvarchar(256)**|Descripción del estado del nodo. Los valores se muestran primero con los valores mutuamente exclusivos, seguidos de los valores combinables. Por ejemplo:<br /><br /> Online, Thread Resources Low, Lazy Preemptive<br /><br /> Hay cuatro valores node_state_desc mutuamente excluyentes. Se enumeran a continuación con sus descripciones.<br /><br /> En línea: El nodo está en línea<br /><br /> Sin conexión: Nodo está sin conexión<br /><br /> INACTIVO: Nodo no tiene ninguna solicitud de trabajo pendiente y ha entrado en un estado de inactividad.<br /><br /> IDLE_READY: Nodo no tiene trabajo solicitudes pendientes y está listo para entrar en un estado inactivo.<br /><br /> Hay cinco valores node_state_desc combinables, con sus descripciones.<br /><br /> DAC: Este nodo está reservado para la conexión administrativa dedicada.<br /><br /> THREAD_RESOURCES_LOW: No hay ningún subproceso nuevo puede crearse en este nodo debido a una condición de memoria insuficiente.<br /><br /> HOT ADDED: Indica los nodos se agregaron en respuesta a eventos de CPU de agregar un acceso rápido.|  
|memory_object_address|**varbinary(8)**|Dirección del objeto de memoria asociada con este nodo. Relación uno a uno respecto a sys.dm_os_memory_objects.memory_object_address.|  
|memory_clerk_address|**varbinary(8)**|Dirección de distribuidor de memoria asociada con este nodo. Relación uno a uno con respecto a sys.dm_os_memory_clerks.memory_clerk_address.|  
|io_completion_worker_address|**varbinary(8)**|La dirección del trabajador asignada a la realización de E/S para este nodo. Relación uno a uno con respecto a sys.dm_os_workers.worker_address.|  
|memory_node_id|**smallint**|Identificador del nodo de memoria al que pertenece este nodo. Relación varios a uno con respecto a  sys.dm_os_memory_nodes.memory_node_id.|  
|cpu_affinity_mask|**bigint**|Mapa de bits que identifica las CPU con las que este nodo está asociado.|  
|online_scheduler_count|**smallint**|Número de programadores en línea que están administrados por este nodo.|  
|idle_scheduler_count|**smallint**|Número de programadores en línea que no tienen ningún trabajador activo.|  
|active_worker_count|**int**|Número de trabajadores que están activos en todos los programadores administrados por este nodo.|  
|avg_load_balance|**int**|Promedio de tareas por programador en este nodo.|  
|timer_task_affinity_mask|**bigint**|Mapa de bits que identifica los programadores que pueden tener asignadas tareas de temporizador.|  
|permanent_task_affinity_mask|**bigint**|Mapa de bits que identifica los programadores que pueden tener asignadas tareas permanentes.|  
|resource_monitor_state|**bit**|Cada nodo tiene asignado un monitor de recursos. El monitor de recursos puede estar en ejecución o inactivo. El valor 1 indica en ejecución y 0 inactividad.|  
|online_scheduler_mask|**bigint**|Identifica la máscara de afinidad de proceso para este nodo.|  
|processor_group|**smallint**|Identifica el grupo de procesadores para este nodo.|  
|cpu_count |**int** |Número de CPU disponibles para este nodo. |
|pdw_node_id|**int**|El identificador para el nodo que se encuentra en esta distribución.<br /><br /> **Se aplica a**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]|  
  
## <a name="permissions"></a>Permissions  
En [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], requiere `VIEW SERVER STATE` permiso.   
En [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] niveles de Premium, requieren la `VIEW DATABASE STATE` permiso en la base de datos. En [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] niveles estándar y básico, requiere la **administrador del servidor** o un **Administrador de Azure Active Directory** cuenta.  
  
## <a name="see-also"></a>Vea también  
  
 [Sistema operativo SQL Server relacionadas con vistas de administración dinámica &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)   
 [Soft-NUMA &#40;SQL Server&#41;](../../database-engine/configure-windows/soft-numa-sql-server.md)  
  
  


