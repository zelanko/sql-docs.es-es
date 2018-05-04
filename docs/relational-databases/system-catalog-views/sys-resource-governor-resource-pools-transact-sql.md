---
title: Sys.resource_governor_resource_pools (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.resource_governor_resource_pools
- resource_governor_resource_pools
- sys.resource_governor_resource_pools_TSQL
- resource_governor_resource_pools_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.resource_governor_resource_pools catalog view
ms.assetid: 56793e9c-aa90-452e-88c6-d9b799239888
caps.latest.revision: 26
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: da4bc1038f383015b4c36c0c14c32312256b749e
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="sysresourcegovernorresourcepools-transact-sql"></a>sys.resource_governor_resource_pools (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve la configuración del grupo de recursos de servidor almacenada en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Cada fila de la vista determina la configuración de un grupo.  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|pool_id|**int**|Identificador único del grupo de recursos de servidor. No admite valores NULL.|  
|name|**sysname**|Nombre del grupo de recursos de servidor. No admite valores NULL.|  
|min_cpu_percent|**int**|Ancho banda de la CPU promedio garantizado para todas las solicitudes en el grupo de recursos de servidor cuando hay contención de CPU. No admite valores NULL.|  
|max_cpu_percent|**int**|Ancho banda de la CPU promedio máximo permitido para todas las solicitudes en el grupo de recursos de servidor cuando hay contención de CPU. No admite valores NULL.|  
|min_memory_percent|**int**|Ancho banda de la memoria garantizado para todas las solicitudes en el grupo de recursos de servidor. No se comparte con otros grupos de recursos de servidor. No admite valores NULL.|  
|max_memory_percent|**int**|Porcentaje de la memoria total del servidor que puede utilizarse en las solicitudes en este grupo de recursos de servidor. No admite valores NULL. El máximo efectivo depende de los mínimos del grupo. Por ejemplo, max_memory_percent puede estar establecido en 100, pero el máximo efectivo es menor.|  
|cap_cpu_percent|**int**|**Se aplica a**: desde [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> El límite máximo de ancho de banda de la CPU que recibirán todas las solicitudes en el grupo de recursos. Limita el ancho de banda máximo de la CPU en el nivel especificado. El intervalo permitido para el valor es de 1 a 100.|  
|min_iops_per_volume|**int**|**Se aplica a**: desde [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Las operaciones de E/S mínima por segundo (IOPS) por la configuración de volumen para este grupo. 0 = sin reserva. No puede ser null.|  
|max_iops_per_volume|**int**|**Se aplica a**: desde [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Las operaciones de E/S máxima por segundo (IOPS) por la configuración de volumen para este grupo. 0 = ilimitado. No puede ser null.|  
  
## <a name="remarks"></a>Comentarios  
 La vista de catálogo muestra los metadatos almacenados. Para ver la configuración en memoria, utilice la vista de administración dinámica correspondiente, [sys.dm_resource_governor_resource_pools &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-resource-pools-transact-sql.md).  
  
## <a name="permissions"></a>Permissions  
 Requiere el permiso VIEW ANY DEFINITION para ver el contenido; requiere el permiso CONTROL SERVER para cambiar el contenido.  
  
## <a name="see-also"></a>Vea también  
 [Vistas de catálogo del regulador de recursos &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/resource-governor-catalog-views-transact-sql.md)   
 [sys.dm_resource_governor_resource_pools &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-resource-pools-transact-sql.md)   
 [Regulador de recursos](../../relational-databases/resource-governor/resource-governor.md)   
 [sys.resource_governor_external_resource_pools &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-resource-governor-external-resource-pools-transact-sql.md)  
  
  
