---
title: Sys.dm_pdw_diag_processing_stats (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-non-specified
ms.prod_service: pdw
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
ms.assetid: df659c55-4f63-45f8-8afe-ce300031bc5b
caps.latest.revision: "7"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 05dc9dc5854b970dd97227672f5f75eecbb34718
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
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
 [Almacenamiento de datos SQL y vistas de administración dinámica de almacenamiento de datos en paralelo &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
