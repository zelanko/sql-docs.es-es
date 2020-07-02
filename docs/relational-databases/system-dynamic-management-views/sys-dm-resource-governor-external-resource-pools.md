---
title: Sys. dm_resource_governor_external_resource_pools (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2019
ms.prod: sql
ms.technology: machine-learning-services
ms.reviewer: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_resource_governor_external_resource_pools_TSQL
- sys.dm_resource_governor_external_resource_pools
- dm_resource_governor_external_resource_pools
- dm_resource_governor_external_resource_pools_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- dm_resource_governor_external_resource_pools
- sys.dm_resource_governor_external_resource_pools
author: dphansen
ms.author: davidph
manager: cgronlun
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: 5a143d4f7052995dddd8bc9cc5239b8ccc7a366f
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85718747"
---
# <a name="sysdm_resource_governor_external_resource_pools-transact-sql"></a>Sys. dm_resource_governor_external_resource_pools (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

Devuelve información sobre el estado actual del grupo de recursos externos, la configuración actual de los grupos de recursos y las estadísticas del grupo de recursos. 
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md).  
  
|Nombre de Colmn      |Tipo de datos      |Descripción|  
|----------------|---------------|-----------------| 
| external_pool_id|**int**|Identificador del grupo de recursos. No admite valores NULL. |
| name|**sysname**|Nombre del grupo de recursos. No admite valores NULL. 
| pool_version|**int**|Número de versión interno.|
| max_cpu_percent|**int**|La configuración actual del ancho banda de la CPU promedio máximo permitido para todas las solicitudes en el grupo de recursos de servidor cuando hay contención de CPU. No admite valores NULL. |
| max_processes|**int**|Número máximo de procesos externos simultáneos. El valor predeterminado, 0, especifica que no hay límite. No admite valores NULL.|
| max_memory_percent|**int**|La configuración actual del porcentaje de memoria total del servidor que pueden utilizar las solicitudes en este grupo de recursos de servidor. No admite valores NULL. |
| statistics_start_time|**datetime**|La hora en que se restablecieron las estadísticas para este grupo. No admite valores NULL. 
| peak_memory_kb|**bigint**|Cantidad máxima de memoria utilizada, en kilobytes, para el grupo de recursos. No admite valores NULL. |
| write_io_count|**int**|El total de operaciones de E/S de escritura emitidas desde que se restablecieron las estadísticas del regulador de recursos. No admite valores NULL. |
| read_io_count|**int**|El total de operaciones de E/S de lectura emitidas desde que se restablecieron las estadísticas del regulador de recursos. No admite valores NULL. |
| total_cpu_kernel_ms|**bigint**|Tiempo de kernel de usuario de CPU acumulado, en milisegundos, desde que se restablecieron las estadísticas de regulador de recursos. No admite valores NULL. |
| total_cpu_user_ms|**bigint**|Tiempo de usuario acumulado de la CPU en milisegundos desde que se restablecieron las estadísticas del regulador de recursos. No admite valores NULL. |
| active_processes_count|**int**|Número de procesos externos que se ejecutan en el momento de la solicitud No admite valores NULL. |

 
## <a name="permissions"></a>Permisos

Requiere el permiso `VIEW SERVER STATE`.

## <a name="see-also"></a>Consulte también  
 [sys.dm_resource_governor_external_resource_pool_affinity &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-external-resource-pool-affinity-transact-sql.md)  
  
  
