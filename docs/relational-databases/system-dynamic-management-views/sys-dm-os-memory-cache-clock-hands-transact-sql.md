---
title: Sys.dm_os_memory_cache_clock_hands (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 12/21/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_os_memory_cache_clock_hands_TSQL
- dm_os_memory_cache_clock_hands
- dm_os_memory_cache_clock_hands_TSQL
- sys.dm_os_memory_cache_clock_hands
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_memory_cache_clock_hands dynamic management view
ms.assetid: 0660eddc-691c-425f-9d43-71151d644de7
caps.latest.revision: 37
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 2983aa6c054b462f20382457fe66a364dac6ec88
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="sysdmosmemorycacheclockhands-transact-sql"></a>sys.dm_os_memory_cache_clock_hands (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve el estado de cada manecilla de un reloj de caché específico.  
  
> [!NOTE]  
>  Para llamar a esta desde [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] o [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], use el nombre **sys.dm_pdw_nodes_os_memory_cache_clock_hands**.  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**cache_address**|**varbinary (8)**|Dirección de la caché asociada al reloj. No admite valores NULL.|  
|**Nombre**|**nvarchar(256)**|Nombre de la caché. No admite valores NULL.|  
|**Tipo**|**nvarchar(60)**|Tipo de almacén de la caché. Pueden existir varias cachés del mismo tipo. No admite valores NULL.|  
|**clock_hand**|**nvarchar(60)**|Tipo de manecilla. Es uno de los siguientes:<br /><br /> External<br /><br /> Interno<br /><br /> No admite valores NULL.|  
|**clock_status**|**nvarchar(60)**|Estado del reloj. Es uno de los siguientes:<br /><br /> Suspendida<br /><br /> En ejecución<br /><br /> No admite valores NULL.|  
|**rounds_count**|**bigint**|Número de rastreos realizados en toda la caché para eliminar entradas. No admite valores NULL.|  
|**removed_all_rounds_count**|**bigint**|Número de entradas quitadas por todos los rastreos. No admite valores NULL.|  
|**updated_last_round_count**|**bigint**|Número de entradas actualizadas durante el último rastreo. No admite valores NULL.|  
|**removed_last_round_count**|**bigint**|Número de entradas quitadas durante el último rastreo. No admite valores NULL.|  
|**last_tick_time**|**bigint**|Última vez, en milisegundos, que se movió la manecilla del reloj. No admite valores NULL.|  
|**round_start_time**|**bigint**|Tiempo, en milisegundos, del rastreo anterior. No admite valores NULL.|  
|**last_round_start_time**|**bigint**|Tiempo total, en milisegundos, que ha tardado el reloj en completar el ciclo anterior. No admite valores NULL.|  
|**pdw_node_id**|**int**|**Se aplica a**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> El identificador para el nodo que se encuentra en esta distribución.|  
  
## <a name="permissions"></a>Permissions  

En [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], requiere `VIEW SERVER STATE` permiso.   
En [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)], requiere el `VIEW DATABASE STATE` permiso en la base de datos.   
  
## <a name="remarks"></a>Comentarios  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] almacena información en memoria en una estructura denominada caché en memoria. La información en la caché pueden ser datos, entradas de índices, planes de procedimientos compilados y diversos tipos de información de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para evitar tener que volver a crear la información, ésta se mantiene en la caché de memoria mientras sea posible y, normalmente, se quita de la caché cuando es demasiado antigua para ser útil o cuando se necesita espacio en la memoria para nueva información. El proceso que quita la información antigua se denomina rastreo de memoria. El rastreo de memoria es una actividad frecuente, pero no continua. Un algoritmo de reloj controla el rastreo de la caché de memoria. Cada reloj puede controlar varios rastreos de memoria, que se denominan manecillas. La manecilla del reloj de la caché de memoria es la ubicación actual de una de las manecillas de un rastreo de memoria.  

## <a name="see-also"></a>Vea también  
 [Vistas de administración dinámica relacionadas con el sistema operativo SQL Server &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)    
 [sys.dm_os_memory_cache_counters &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-cache-counters-transact-sql.md)
  

