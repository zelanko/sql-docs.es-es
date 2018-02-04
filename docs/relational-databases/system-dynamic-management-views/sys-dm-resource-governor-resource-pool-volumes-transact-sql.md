---
title: sys.dm_resource_governor_resource_pool_volumes (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 08/09/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.dm_resource_governor_resource_pool_volumes_TSQL
- dm_resource_governor_resource_pool_volumes_TSQL
- dm_resource_governor_resource_pool_volumes
- sys.dm_resource_governor_resource_pool_volumes
dev_langs:
- TSQL
helpviewer_keywords:
- dm_resource_governor_resource_pool_volumes
- sys.dm_resource_governor_resource_pool_volumes
ms.assetid: fa692e56-c561-4533-97c5-bc12c600553f
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a60bd54400d9e9d82c3abbde9d828c1877b0753b
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/03/2018
---
# <a name="sysdmresourcegovernorresourcepoolvolumes-transact-sql"></a>sys.dm_resource_governor_resource_pool_volumes (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2014-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2014-xxxx-xxxx-xxx-md.md)]

  Devuelve información sobre las estadísticas de E/S del grupo de recursos actual para cada volumen de disco. Esta información también está disponible en el nivel de grupo de recursos en [sys.dm_resource_governor_resource_pools &#40; Transact-SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-resource-pools-transact-sql.md).  
  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|pool_id|**int**|Identificador del grupo de recursos. No admite valores NULL.|  
|volume_name|**sysname**|El nombre del volumen de disco. No admite valores NULL.|  
|read_io_queued_total|**int**|El total de lectura en cola de IOs desde que se restableció el regulador de recursos. No admite valores NULL.|  
|read_io_issued_total|**int**|El total de operaciones de E/S de lectura emitidas desde que se restablecieron las estadísticas del regulador de recursos. No admite valores NULL.|  
|read_ios_completed_total|**int**|El total de operaciones de E/S de lectura completadas desde que se restablecieron las estadísticas del regulador de recursos. No admite valores NULL.|  
|read_ios_throttled_total|**int**|El total de operaciones de E/S de lectura limitadas desde que se restablecieron las estadísticas del regulador de recursos. No admite valores NULL.|  
|read_bytes_total|**bigint**|El número total de bytes leídos desde que se restablecieron las estadísticas del regulador de recursos. No admite valores NULL.|  
|read_io_stall_total_ms|**bigint**|Tiempo total (en milisegundos) desde que llegó la operación de E/S de lectura hasta que se completó. No admite valores NULL.|  
|read_io_stall_queued_ms|**bigint**|Tiempo total (en milisegundos) desde que llegó la operación de E/S de lectura hasta que hubo el problema. Este es el retraso que introduce el regulador de recursos de E/S. No admite valores NULL.|  
|write_io_queued_total|**int**|El total de operaciones de E/S de escritura puestas en cola desde que se restablecieron las estadísticas del regulador de recursos. No admite valores NULL.|  
|write_io_issued_total|**int**|El total de operaciones de E/S de escritura emitidas desde que se restablecieron las estadísticas del regulador de recursos. No admite valores NULL.|  
|write_io_completed_total|**int**|El total de operaciones de E/S de escritura completadas desde que se restablecieron las estadísticas del regulador de recursos. No admite valores NULL|  
|write_io_throttled_total|**int**|El total de operaciones de E/S de escritura limitadas desde que se restablecieron las estadísticas del regulador de recursos. No admite valores NULL|  
|write_bytes_total|**bigint**|El número total de bytes escritos desde que se restablecieron las estadísticas del regulador de recursos. No admite valores NULL.|  
|write_io_stall_total_ms|**bigint**|Tiempo total (en milisegundos) desde que se emitió la operación de E/S de escritura hasta que se completó. No admite valores NULL.|  
|write_io_stall_queued_ms|**bigint**|Tiempo total (en milisegundos) desde que llegó la operación de E/S de escritura hasta que hubo el problema. Este es el retraso que introduce el regulador de recursos de E/S. No admite valores NULL.|  
|io_issue_violations_total|**int**|Total de infracciones de emisiones de operaciones de E/S. Es decir, el número de veces en que la tasa de emisiones de operaciones de E/S ha sido inferior a la tasa reservada. No admite valores NULL.|  
|io_issue_delay_total_ms|**bigint**|Tiempo total (en milisegundos) entre la emisión programada y la emisión real de operaciones de E/S. No admite valores NULL.|  
  
## <a name="permissions"></a>Permissions  
 Requiere el permiso VIEW SERVER STATE.  
  
## <a name="see-also"></a>Vea también  
 [Funciones y vistas de administración dinámica &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [sys.dm_resource_governor_workload_groups &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-workload-groups-transact-sql.md)   
 [sys.resource_governor_resource_pools &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-resource-governor-resource-pools-transact-sql.md)   
 [ALTER RESOURCE GOVERNOR &#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-governor-transact-sql.md)  
  
  

