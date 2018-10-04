---
title: Sys.resource_governor_workload_groups (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.resource_governor_workload_groups
- resource_governor_workload_groups_TSQL
- sys.resource_governor_workload_groups_TSQL
- resource_governor_workload_groups
dev_langs:
- TSQL
helpviewer_keywords:
- sys.resource_governor_workload_groups catalog view
ms.assetid: 619ba4b7-868f-4784-b527-ec1dfd703c4f
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: d24885b194f8614e393c7529fac0dc34eb3e15fd
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47857233"
---
# <a name="sysresourcegovernorworkloadgroups-transact-sql"></a>sys.resource_governor_workload_groups (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve la configuración del grupo de cargas de trabajo almacenada en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Cada grupo de cargas de trabajo puede suscribirse a un único grupo de recursos de servidor.  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|group_id|**int**|Id. único del grupo de cargas de trabajo. No admite valores NULL.|  
|NAME|**sysname**|Nombre del grupo de cargas de trabajo No admite valores NULL.|  
|importance|**sysname**|**Nota:** importancia solo se aplica a los grupos de carga de trabajo en el mismo grupo de recursos.<br /><br /> Es la importancia relativa de una solicitud en este grupo de cargas de trabajo. La importancia puede ser uno de los siguientes, siendo MEDIUM el valor predeterminado: bajo, medio, alto.<br /><br /> No admite valores NULL.|  
|request_max_memory_grant_percent|**int**|Concesión máxima de memoria, en porcentaje, para una solicitud única. El valor predeterminado es 25. No admite valores NULL.<br /><br /> **Nota:** si este valor es mayor que 50 por ciento, las consultas grandes ejecutarán una vez. Por consiguiente, existe un mayor riesgo de que se produzca un error de memoria insuficiente mientras se está ejecutando la consulta.|  
|request_max_cpu_time_sec|**int**|Límite máximo de uso de CPU, en segundos, para una única solicitud. El valor predeterminado, 0, especifica que no hay límite. No admite valores NULL.<br /><br /> **Nota:** para obtener más información, consulte [CPU umbral de esta clase de eventos](../../relational-databases/event-classes/cpu-threshold-exceeded-event-class.md).|  
|request_memory_grant_timeout_sec|**int**|Tiempo de espera de la concesión de memoria, en segundos, para una única solicitud. El valor predeterminado, 0, utiliza un cálculo interno basado en el costo de la consulta. No admite valores NULL.|  
|max_dop|**int**|Grado máximo de paralelismo para el grupo de cargas de trabajo. El valor predeterminado, 0, utiliza la configuración global. No admite valores NULL.<br /><br /> **Nodo:** esta configuración invalidará la opción de consulta **maxdop**.|  
|group_max_requests|**int**|Número máximo de solicitudes simultáneas. El valor predeterminado, 0, especifica que no hay límite. No admite valores NULL.|  
|pool_id|**int**|Identificador del grupo de recursos de servidor que usa este grupo de cargas de trabajo.|  
|external_pool_id|**int**|**Se aplica a**: desde [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Id. de grupo de recursos externos que usa este grupo de cargas de trabajo.|  
  
## <a name="remarks"></a>Comentarios  
 La vista de catálogo muestra los metadatos almacenados. Para ver la configuración en memoria, utilice la vista de administración dinámica correspondiente, [sys.dm_resource_governor_workload_groups &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-workload-groups-transact-sql.md).  
  
 La configuración almacenada puede ser diferente a la configuración en memoria si se ha cambiado la configuración del regulador de recursos pero sin aplicar la instrucción ALTER RESOURCE GOVERNOR RECONFIGURE.  
  
## <a name="permissions"></a>Permisos  
 Requiere el permiso VIEW ANY DEFINITION para ver el contenido; requiere el permiso CONTROL SERVER para cambiar el contenido.  
  
## <a name="see-also"></a>Vea también  
 [sys.dm_resource_governor_workload_groups &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-workload-groups-transact-sql.md)   
 [Vistas de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Vistas de catálogo del regulador de recursos &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/resource-governor-catalog-views-transact-sql.md)  
  
  
