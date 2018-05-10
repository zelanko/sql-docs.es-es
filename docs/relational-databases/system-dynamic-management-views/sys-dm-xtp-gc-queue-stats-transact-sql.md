---
title: Sys.dm_xtp_gc_queue_stats (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 08/02/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- dm_xtp_gc_stats
- dm_xtp_gc_stats_TSQL
- sys.dm_xtp_gc_stats_TSQL
- sys.dm_xtp_gc_stats
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_xtp_gc_stats dynamic management view
ms.assetid: addef774-318d-46a7-85df-f93168a800cb
caps.latest.revision: 18
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 58c9dee00bbf3353a89430d9eb629b7b91eb0744
ms.sourcegitcommit: d2573a8dec2d4102ce8882ee232cdba080d39628
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/07/2018
---
# <a name="sysdmxtpgcqueuestats-transact-sql"></a>sys.dm_xtp_gc_queue_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2014-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2014-xxxx-xxxx-xxx-md.md)]

  Genera información y distintas estadísticas sobre cada cola de trabajador de recolección de elementos no utilizados en el servidor. Hay una cola por cada CPU lógica.  
  
 El subproceso principal de recolección de elementos no utilizados (el subproceso inactivo) hace un seguimiento de las filas actualizadas, eliminadas e insertadas de todas las transacciones completadas desde la última invocación del subproceso principal de recolección de elementos no utilizados. Cuando el subproceso de recolección de elementos no utilizados se reactiva, determina si la marca de tiempo de la transacción activa más antigua ha cambiado. Si la transacción activa más antigua ha cambiado, el subproceso inactivo pone en cola elementos de trabajo (en fragmentos de 16 filas) para las transacciones cuyos conjuntos de escritura no son ya necesarios. Por ejemplo, si elimina 1.024 filas, en la cola habrá 64 elementos de trabajo no utilizados recopilados, cada uno de los cuales contiene 16 filas eliminadas.  Una vez que una transacción de usuario se confirma, selecciona todos los elementos puestos en cola en su programador. Si no hay ningún elemento en cola en su programador, la transacción de usuario buscará en todas las colas del nodo NUMA actual.  
  
 Es posible determinar si la recolección de elementos no utilizados está liberando memoria para las filas eliminadas; para ello, ejecute sys.dm_xtp_gc_queue_stats para ver si el trabajo puesto en cola se está procesando. Si no se están procesando las entradas de current_queue_depth o si no hay nuevos elementos de trabajo se agregan a current_queue_depth, esto es una indicación de que la recolección de elementos no está liberando memoria. Por ejemplo, la recolección de elementos no utilizados no se puede realizar si hay una transacción de ejecución prolongada.  
  
 Para obtener más información, vea [OLTP en memoria &#40;optimización en memoria&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md).  
  

|Nombre de columna|Tipo|Description|  
|-----------------|----------|-----------------|  
|queue_id|**int**|Identificador único de la cola.|  
|total_enqueues|**bigint**|El número total de elementos de trabajo de la recolección de elementos no utilizados puestos en esta cola desde que se inició el servidor.|  
|total_dequeues|**bigint**|El número total de elementos de trabajo de la recolección de elementos no utilizados quitados de esta cola desde que se inició el servidor.|  
|current_queue_depth|**bigint**|El número actual de elementos de trabajo de la recolección de elementos no utilizados presentes en esta cola. Este elemento puede implicar que el recolector de elementos no utilizados elimine varios de ellos.|  
|maximum_queue_depth|**bigint**|La profundidad máxima que ha visto esta cola.|  
|last_service_ticks|**bigint**|Los tics de CPU en el momento en que se dio servicio a la cola por última vez.|  
  
## <a name="permissions"></a>Permissions  
 Requiere el permiso VIEW SERVER STATE.  
  
## <a name="user-scenario"></a>Escenario de usuario  
 Este resultado muestra que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se ejecuta en 4 núcleos o que se ha establecido afinidad para la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en 4 núcleos:  
  
 Este resultado muestra que no hay elementos de trabajo en las colas que se van a procesar. Para la cola 0, los elementos de trabajo totales que se quitan de la cola desde que se inicia SQL son 15 625 y la profundidad máxima de cola fue 215 625.  
  
```  
queue_id total_enqueues total_dequeues current_queue_depth  maximum_queue_depth  last_service_ticks  
----------------------------------------------------------------------------------------------------  
0        15625                15625    0                    15625                1233573168347  
1        15625                15625    0                    15625                1234123295566  
2        15625                15625    0                    15625                1233569418146  
3        15625                15625    0                    15625                1233571605761  
```  
  
## <a name="see-also"></a>Vea también  
 [Vistas de administración dinámica de tablas optimizadas en memoria &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/memory-optimized-table-dynamic-management-views-transact-sql.md)  
  
  
