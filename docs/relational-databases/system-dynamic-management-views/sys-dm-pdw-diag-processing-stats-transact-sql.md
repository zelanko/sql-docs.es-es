---
title: sys.dm_pdw_diag_processing_stats (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: df659c55-4f63-45f8-8afe-ce300031bc5b
author: stevestein
ms.author: sstein
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 8b880820ac633402d1d3cdd679b16a54d1be358e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67899538"
---
# <a name="sysdmpdwdiagprocessingstats-transact-sql"></a>sys.dm_pdw_diag_processing_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  Muestra información relacionada con todos los eventos de diagnóstico internos que podrían incorporarse definidas por el Administrador de sesiones de diagnóstico. Consultar esta vista para comprender las estadísticas detrás de los subsistemas de eventos y el diagnóstico de esa unidad de la población de todas las otras DMV. Hay un grupo de colas para cada proceso en cada nodo.  
  
|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**pdw_node_id**|**int**|Este registro es de un nodo de dispositivo.|  
|**process_id**|**int**|Identificador del proceso que ejecuta el envío de esta estadística.|  
|**target_name**|**nvarchar(255)**|Nombre de la cola.|  
|**queue_size**|**int**|El número de elementos en la cola de procesos. Normalmente, el tamaño de la cola es 0. Un número positivo indica que el sistema está bajo presión y está creando el trabajo acumulado de eventos. Un recuento positivo en las otras columnas significa sistema se ha dañado para esa cola en particular y todas las DMV relacionadas.|  
|**lost_events_count**|**bigint**|El número de eventos perdidos.|  
  
## <a name="see-also"></a>Vea también  
 [Vistas de administración dinámica de almacenamiento de datos en paralelo y SQL Data Warehouse &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
