---
title: Sys.dm_resource_governor_workload_groups (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 04/24/2018
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.service: ''
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_resource_governor_workload_groups
- sys.dm_resource_governor_workload_groups_TSQL
- dm_resource_governor_workload_groups
- dm_resource_governor_workload_groups_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_resource_governor_workload_groups dynamic management view
ms.assetid: f63c4914-1272-43ef-b135-fe1aabd953e0
caps.latest.revision: 27
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 93c479c12291c2af7d3a4abafb8a5226dd44fbd9
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="sysdmresourcegovernorworkloadgroups-transact-sql"></a>sys.dm_resource_governor_workload_groups (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-asdb-asdw-pdw-md.md)]

  Devuelve las estadísticas del grupo de cargas de trabajo y la configuración actual en memoria del grupo de cargas de trabajo. Puede unirse esta vista con sys.dm_resource_governor_resource_pools para obtener el nombre del grupo de recursos de servidor.  
  
> [!NOTE]  
>  Para llamar a esta desde [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] o [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], use el nombre **sys.dm_pdw_nodes_resource_governor_workload_groups**.  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|group_id|**int**|Id. del grupo de cargas de trabajo No admite valores NULL.|  
|name|**sysname**|Nombre del grupo de cargas de trabajo No admite valores NULL.|  
|pool_id|**int**|Id. del grupo de recursos de servidor. No admite valores NULL.|  
|external_pool_id|**int**|**Se aplica a**: desde [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Id. del grupo de recursos externos. No admite valores NULL.|  
|statistics_start_time|**datetime**|Tiempo en que se restableció la colección de estadísticas para el grupo de cargas de trabajo. No admite valores NULL.|  
|total_request_count|**bigint**|El recuento acumulado de solicitudes completadas en el grupo de cargas de trabajo. No admite valores NULL.|  
|total_queued_request_count|**bigint**|El recuento acumulado de solicitudes en cola una vez alcanzado el límite de GROUP_MAX_REQUESTS. No admite valores NULL.|  
|active_request_count|**int**|Recuento actual de solicitudes. No admite valores NULL.|  
|queued_request_count|**int**|Recuento actual de solicitudes en cola. No admite valores NULL.|  
|total_cpu_limit_violation_count|**bigint**|Recuento acumulado de solicitudes que superan el límite de CPU. No admite valores NULL.|  
|total_cpu_usage_ms|**bigint**|Uso acumulado de la CPU en milisegundos de este grupo de cargas de trabajo. No admite valores NULL.|  
|max_request_cpu_time_ms|**bigint**|Uso máximo de CPU, en milisegundos, para una única solicitud. No admite valores NULL.<br /><br /> **Nota:** es un valor medido, al contrario que request_max_cpu_time_sec, que es un valor configurable. Para obtener más información, vea [Clase de eventos Umbral de la CPU superado](../../relational-databases/event-classes/cpu-threshold-exceeded-event-class.md).|  
|blocked_task_count|**int**|Contador actual de tareas bloqueadas. No admite valores NULL.|  
|total_lock_wait_count|**bigint**|Recuento acumulado de esperas del bloqueo producidas. No admite valores NULL.|  
|total_lock_wait_time_ms|**bigint**|Suma acumulada de tiempo transcurrido, en milisegundos, que se mantiene un bloqueo. No admite valores NULL.|  
|total_query_optimization_count|**bigint**|El recuento acumulado de optimizaciones de consultas en este grupo de cargas de trabajo. No admite valores NULL.|  
|total_suboptimal_plan_generation_count|**bigint**|Recuento acumulado de generaciones de planes poco óptimos producidas en este grupo de cargas de trabajo debido a la presión de memoria. No admite valores NULL.|  
|total_reduced_memgrant_count|**bigint**|Recuento acumulado de concesiones de memoria que alcanzaron el límite máximo de tamaño de consulta. No admite valores NULL.|  
|max_request_grant_memory_kb|**bigint**|El tamaño máximo de la concesión de memoria, en kilobytes, de una única solicitud desde que se restablecieron las estadísticas. No admite valores NULL.|  
|active_parallel_thread_count|**bigint**|Recuento actual de uso del subproceso paralelo. No admite valores NULL.|  
|importance|**sysname**|Valor de la configuración actual de la importancia relativa de una solicitud en este grupo de cargas de trabajo. La importancia puede ser uno de los siguientes, siendo Medium es el valor predeterminado: bajo, medio o alto.<br /><br /> No admite valores NULL.|  
|request_max_memory_grant_percent|**int**|Valor actual de la concesión máxima de memoria, en porcentaje, para una única solicitud. No admite valores NULL.|  
|request_max_cpu_time_sec|**int**|Valor actual máximo de uso de CPU, en segundos, para una única solicitud. No admite valores NULL.|  
|request_memory_grant_timeout_sec|**int**|Valor actual del tiempo de espera de concesiones de memoria, en segundos, para una única solicitud. No admite valores NULL.|  
|group_max_requests|**int**|Valor actual del número máximo de solicitudes simultáneas. No admite valores NULL.|  
|max_dop|**int**|Grado máximo de paralelismo para el grupo de cargas de trabajo. El valor predeterminado, 0, utiliza la configuración global. No admite valores NULL.|  
|pdw_node_id|**int**|**Se aplica a**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> El identificador para el nodo que se encuentra en esta distribución.|  
  
## <a name="remarks"></a>Comentarios  
 Esta vista de administración dinámica muestra la configuración en memoria. Para ver los metadatos almacenados de la configuración, utilice la vista de catálogo sys.resource_governor_workload_groups.  
  
 Cuando ALTER RESOURCE GOVERNOR RESET STATISTICS se ejecuta correctamente, se restablecen los contadores siguientes: statistics_start_time, total_request_count, total_queued_request_count, total_cpu_limit_violation_count, total_cpu_usage_ms, max_request_ cpu_time_ms, total_lock_wait_count, total_lock_wait_time_ms, total_query_optimization_count, total_suboptimal_plan_generation_count, total_reduced_memgrant_count y max_request_grant_memory_kb. statistics_start_time se establece en la fecha actual del sistema y la hora, los otros contadores se establecen en cero (0).  
  
## <a name="permissions"></a>Permissions  
 Requiere el permiso VIEW SERVER STATE.  
  
## <a name="see-also"></a>Vea también  
 [Funciones y vistas de administración dinámica &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [sys.dm_resource_governor_resource_pools &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-resource-pools-transact-sql.md)   
 [sys.resource_governor_workload_groups &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-resource-governor-workload-groups-transact-sql.md)   
 [ALTER RESOURCE GOVERNOR &#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-governor-transact-sql.md)  
  
  



