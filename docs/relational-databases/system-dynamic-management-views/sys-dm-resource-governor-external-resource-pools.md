---
title: Sys. DM _ _resource_governor_external_resource_pools (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2019
ms.prod: sql
ms.technology: machine-learning
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
ms.openlocfilehash: cf77a073a1432df839bfd13046c66018496e79f1
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/24/2019
ms.locfileid: "68468521"
---
# <a name="sysdmresourcegovernorexternalresourcepools-transact-sql"></a>Sys. DM _ _resource_governor_external_resource_pools (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss-xxxx-xxxx-xxx-md.md)]

Devuelve información sobre el estado actual del grupo de recursos externos, la configuración actual de los grupos de recursos y las estadísticas del grupo de recursos. 
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md).  
  
|Nombre de Colmn      |Tipo de datos      |Descripción|  
|----------------|---------------|-----------------| 
| external_pool_id|**int**|Identificador del grupo de recursos. No admite valores NULL. |
| NAME|**sysname**|Nombre del grupo de recursos. No admite valores NULL. 
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
| active_processes_count|**int**|El número de procesos externos que se ejecutan en el momento de la solicitud. No admite valores NULL. |

 
## <a name="permissions"></a>Permisos

Requiere el permiso `VIEW SERVER STATE`.

## <a name="see-also"></a>Vea también  
 [sys.dm_resource_governor_external_resource_pool_affinity &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-external-resource-pool-affinity-transact-sql.md)  
  
  
