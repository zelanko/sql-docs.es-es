---
description: Sys. dm_resource_governor_external_resource_pools (Transact-SQL)
title: Sys. dm_resource_governor_external_resource_pools (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/06/2020
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
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 32df69f207de0e1c604c10d58f4d28b4a3a34aa5
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88454866"
---
# <a name="sysdm_resource_governor_external_resource_pools-transact-sql"></a>Sys. dm_resource_governor_external_resource_pools (Transact-SQL)
[!INCLUDE [SQL Server 2016 and later](../../includes/applies-to-version/sqlserver2016.md)]

Devuelve información sobre el estado actual del grupo de recursos externos, la configuración actual de los grupos de recursos y las estadísticas del grupo de recursos. 
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md).  
  
|Nombre de la columna      |Tipo de datos      |Descripción|  
|----------------|---------------|-----------------| 
| external_pool_id|**int**|Identificador del grupo de recursos. No admite valores NULL. |
| name|**sysname**|Nombre del grupo de recursos. No admite valores NULL. 
| pool_version|**int**|Número de versión interno.|
| max_cpu_percent|**int**|La configuración actual del ancho banda de la CPU promedio máximo permitido para todas las solicitudes en el grupo de recursos de servidor cuando hay contención de CPU. No admite valores NULL. |
| max_processes|**int**|Número máximo de procesos externos simultáneos. El valor predeterminado, 0, especifica que no hay límite. No admite valores NULL.|
| max_memory_percent|**int**|La configuración actual del porcentaje de memoria total del servidor que pueden utilizar las solicitudes en este grupo de recursos de servidor. No admite valores NULL. |
| statistics_start_time|**datetime**|La hora en que se restablecieron las estadísticas para este grupo. No admite valores NULL. 
| peak_memory_kb|**bigint**|Cantidad máxima de memoria utilizada, en kilobytes, para el grupo de recursos. No admite valores NULL. |
| write_io_count|**int**|Total de operaciones de E/S de escritura emitidas desde el restablecimiento de las estadísticas de Resource Governor No admite valores NULL. |
| read_io_count|**int**|Total de operaciones de E/S de lectura emitidas desde el restablecimiento de las estadísticas de Resource Governor No admite valores NULL. |
| total_cpu_kernel_ms|**bigint**|Tiempo del kernel de usuario de CPU acumulativo en milisegundos desde el restablecimiento de las estadísticas de Resource Governor No admite valores NULL. |
| total_cpu_user_ms|**bigint**|Tiempo de usuario de CPU acumulativo en milisegundos desde el restablecimiento de las estadísticas de Resource Governor No admite valores NULL. |
| active_processes_count|**int**|Número de procesos externos que se ejecutan en el momento de la solicitud No admite valores NULL. |

 
## <a name="permissions"></a>Permisos

Requiere el permiso `VIEW SERVER STATE`.

> [!NOTE]
> SQL Machine Learning Services 2019 para Linux no admite la capacidad de establecer la afinidad de la CPU.

## <a name="see-also"></a>Consulte también  
 [sys.dm_resource_governor_external_resource_pool_affinity &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-external-resource-pool-affinity-transact-sql.md)  
  
  
