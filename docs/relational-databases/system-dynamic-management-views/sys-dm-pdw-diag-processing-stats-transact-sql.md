---
title: Sys. dm_pdw_diag_processing_stats (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: df659c55-4f63-45f8-8afe-ce300031bc5b
author: CarlRabeler
ms.author: carlrab
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: aac1c35f86b0d7f9d12405cb25136015afb5a52b
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/05/2020
ms.locfileid: "82811423"
---
# <a name="sysdm_pdw_diag_processing_stats-transact-sql"></a>Sys. dm_pdw_diag_processing_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  Muestra información relacionada con todos los eventos de diagnóstico internos que se pueden incorporar en sesiones de diagnóstico definidas por el administrador. Consulte esta vista para conocer las estadísticas de los subsistemas de diagnóstico y eventos que controlan el rellenado de todas las demás DMV. Hay un grupo de colas para cada proceso en cada nodo.  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**pdw_node_id**|**int**|Nodo del dispositivo del que procede este registro.|  
|**process_id**|**int**|Identificador del proceso que ejecuta el envío de esta estadística.|  
|**target_name**|**nvarchar(255)**|Nombre de la cola.|  
|**queue_size**|**int**|Número de elementos de la cola de procesos. El tamaño de la cola suele ser 0. Un número positivo indica que el sistema está bajo esfuerzo y está creando trabajo pendiente de eventos. Un recuento positivo en las demás columnas significa que el sistema se ha dañado para esa cola concreta y cualquier DMV relacionada.|  
|**lost_events_count**|**bigint**|Número de eventos perdidos.|  
  
## <a name="see-also"></a>Consulte también  
 [Vistas de administración dinámica de SQL Data Warehouse y almacenamiento de datos paralelos &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
