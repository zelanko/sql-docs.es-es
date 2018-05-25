---
title: Sys.dm_pdw_diag_processing_stats (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: df659c55-4f63-45f8-8afe-ce300031bc5b
caps.latest.revision: 7
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 22c3a810349f1e41557572bd2bf5ce3ba25a7a27
ms.sourcegitcommit: 7019ac41524bdf783ea2c129c17b54581951b515
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/23/2018
---
# <a name="sysdmpdwdiagprocessingstats-transact-sql"></a>Sys.dm_pdw_diag_processing_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  Muestra información relacionada con todos los eventos de diagnóstico internos que pudieron incorporarse definidas por el Administrador de sesiones de diagnóstico. Consultar esta vista para comprender las estadísticas detrás de los subsistemas de eventos y el diagnóstico de esa unidad de la población de todas las otras DMV. Hay un grupo de colas para cada proceso en cada nodo.  
  
|Nombre de la columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**pdw_node_id**|**int**|Este registro procede de un nodo de dispositivo.|  
|**Id**|**int**|Identificador del proceso que ejecuta enviar esta estadística.|  
|**target_name**|**nvarchar(255)**|Nombre de la cola.|  
|**queue_size**|**int**|El número de elementos en la cola de procesos. Normalmente, el tamaño de la cola es 0. Un número positivo indica que el sistema está en situaciones de estrés y está creando el trabajo acumulado de eventos. Un recuento positivo en las otras columnas significa sistema se ha dañado para esa cola en particular y cualquier relacionada DMV.|  
|**lost_events_count**|**bigint**|El número de eventos perdidos.|  
  
## <a name="see-also"></a>Vea también  
 [Vistas de administración dinámica del almacenamiento de datos en paralelo y almacén de datos SQL &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
