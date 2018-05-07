---
title: Sys.server_event_sessions (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- server_event_sessions
- server_event_sessions_TSQL
- sys.server_event_sessions_TSQL
- sys.server_event_sessions
dev_langs:
- TSQL
helpviewer_keywords:
- sys.server_event_sessions catalog view
- xe
ms.assetid: 796f3093-6a3e-4d67-8da6-b9810ae9ef5b
caps.latest.revision: 15
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 06f4385e35efe104bf83f98ef325a6d51e960df8
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2018
---
# <a name="sysservereventsessions-transact-sql"></a>sys.server_event_sessions (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Enumera todas las definiciones de sesión de eventos existentes en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|event_session_id|**int**|Id. único de la sesión de eventos. No admite valores NULL.|  
|name|**sysname**|Nombre definido por el usuario para identificar la sesión de eventos. nombre es único. No admite valores NULL.|  
|event_retention_mode|**nchar (1)**|Determina cómo se controla la pérdida de eventos. El valor predeterminado es S. No admite valores NULL. Es uno de los siguientes valores:<br /><br /> S. Asigna event_retention_mode_desc = ALLOW_SINGLE_EVENT_LOSS<br /><br /> M. Asigna event_retention_mode_desc = ALLOW_MULTIPLE_EVENT_LOSS<br /><br /> N. Asigna event_retention_mode_desc = NO_EVENT_LOSS|  
|event_retention_mode_desc|**sysname**|Describe cómo se controla la pérdida de eventos. El valor predeterminado es ALLOW_SINGLE_EVENT_LOSS. No admite valores NULL. Es uno de los siguientes valores:<br /><br /> ALLOW_SINGLE_EVENT_LOSS. Pueden perderse los eventos de la sesión. Se quitan eventos individuales únicamente cuando todos los búferes de eventos están llenos. La pérdida de eventos individuales cuando los búferes están llenos permite un rendimiento de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] aceptable, al mismo tiempo que minimiza las pérdidas en el flujo de eventos procesado.<br /><br /> ALLOW_MULTIPLE_EVENT_LOSS. Pueden perderse búferes de eventos completos de la sesión. El número de eventos perdidos depende del tamaño de la memoria asignada a la sesión, el particionamiento de la memoria y el tamaño de los eventos del búfer. Esta opción minimiza el impacto en el rendimiento del servidor si los búferes de eventos se llenan rápidamente. Sin embargo, pueden perderse un gran número de eventos de la sesión.<br /><br /> NO_EVENT_LOSS. No se permite ninguna pérdida de eventos. Esta opción asegura que se retienen todos los eventos que aparecen. Al utilizar esta opción, se fuerza a todas las tareas que activan eventos a que esperen que haya espacio disponible en un búfer de eventos. Esto puede conducir a una degradación detectable en el rendimiento mientras la sesión de eventos está activa.|  
|max_dispatch_latency|**int**|La cantidad de tiempo, en milisegundos, durante el que los eventos se almacenarán en memoria antes de servirse a los destinos de la sesión. Los valores válidos son de 1 a 2147483648, y -1. Un valor de -1 indica que la latencia de la expedición es infinita. Acepta valores NULL.|  
|max_memory|**int**|La cantidad de memoria asignada a la sesión para el almacenado en búfer de los eventos. El valor predeterminado es 4 MB. Acepta valores NULL.|  
|max_event_size|**int**|La cantidad de memoria reservada para los eventos que no pueden almacenarse en los búferes de sesión de eventos. Si max_event_size supera el tamaño de búfer calculado, se asignarán dos búferes adicionales de max_event_size a la sesión de evento. Acepta valores NULL.|  
|memory_partition_mode|**nchar (1)**|Ubicación en memoria donde se crean los búferes de eventos. El modo de la partición predeterminado es G. No admite valores NULL. MEMORY_PARTITION_MODE es uno de:<br /><br /> G - NONE<br /><br /> C - PER_CPU<br /><br /> N - PER_NODE|  
|memory_partition_mode_desc|**sysname**|El valor predeterminado es NONE. No admite valores NULL. Es uno de los siguientes valores:<br /><br /> NONE. Un conjunto único de búferes se crean dentro de una instancia de SQL Server.<br /><br /> PER_CPU. Se crea un conjunto de búferes para cada CPU.<br /><br /> PER_NODE. Se crea un conjunto de búferes para cada nodo de acceso no uniforme a memoria (NUMA).|  
|track_causality|**bit**|Habilite o deshabilite el seguimiento de causalidad. Si está establecido en 1 (ON), se habilita el seguimiento y se pueden correlacionar los eventos relacionados en diferentes conexiones con el servidor. El valor predeterminado es 0 (OFF). No admite valores NULL.|  
|startup_state|**bit**|Valor que determina si se inicia automáticamente la sesión cuando el servidor se inicia. El valor predeterminado es 0. No admite valores NULL. Puede ser uno de los siguientes:<br /><br /> 0 (OFF). La sesión no se inicia cuando el servidor se inicia.<br /><br /> 1 (ON). La sesión de eventos se inicia cuando el servidor se inicia.|  
  
## <a name="permissions"></a>Permissions  
 es necesario contar con el permiso VIEW SERVER STATE en el servidor.  
  
## <a name="see-also"></a>Vea también  
 [Vistas de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Vistas de catálogo de eventos extendidos &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/extended-events-catalog-views-transact-sql.md)   
 [Eventos extendidos](../../relational-databases/extended-events/extended-events.md)  
  
  
