---
title: Sys.dm_exec_compute_node_status (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- DM_EXEC_COMPUTE_NODE_STATUS_TSQL
- DM_EXEC_COMPUTE_NODE_STATUS
dev_langs:
- TSQL
helpviewer_keywords:
- PolyBase,views
- PolyBase
- dm_exec_compute_node_status
- sys.dm_exec_compute_node_status management view
ms.assetid: b606f91f-3a08-4a4f-bb57-32ae155b3738
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 3341f692a4015d11eb90bebb142b7ab7ae7f3a25
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47774783"
---
# <a name="sysdmexeccomputenodestatus-transact-sql"></a>sys.dm_exec_compute_node_status (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2016-xxxx-asdw-pdw-md.md)]

  Contiene información adicional sobre el rendimiento y el estado de todos los nodos de PolyBase. Muestra una fila por cada nodo.  
  
|Nombre de la columna|Tipo de datos|Descripción|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|compute_node_id|**int**|Identificador numérico único asociado al nodo.|Único en clúster de escalabilidad horizontal, independientemente del tipo.|  
|process_id|**int**|||  
|nombreDeProceso|**nvarchar(255)**|Nombre lógico del nodo.|Cualquier cadena de longitud adecuada.|  
|allocated_memory|**bigint**|Memoria total asignada en este nodo.||  
|available_memory|**bigint**|Memoria total disponible en este nodo.||  
|process_cpu_usage|**bigint**|Uso de CPU de proceso total, en tics.||  
|total_cpu_usage|**bigint**|Uso total de CPU, en tics.||  
|Thread_Count|**bigint**|Número total de subprocesos en uso en este nodo.||  
|handle_count|**bigint**|Número total de identificadores en uso en este nodo.||  
|total_elapsed_time|**bigint**|Tiempo total transcurrido desde que el sistema, iniciar o reiniciar.|Tiempo total transcurrido desde que el sistema, iniciar o reiniciar. Si total_elapsed_time supera el valor máximo de un entero (24,8 días en milisegundos), provocará el error de materialización debido al desbordamiento. El valor máximo en milisegundos equivale a 24,8 días.|  
|is_available|**bit**|Marca que indica si este nodo está disponible.||  
|sent_time|**datetime**|Última vez que se envió un paquete de red por este||  
|received_time|**datetime**|Última vez que se envió un paquete de red por este nodo.||  
|error_id|**nvarchar(36)**|Identificador único del último error que se produjo en este nodo.||  
  
## <a name="see-also"></a>Vea también  
 [Solución de problemas con las vistas de administración dinámica de PolyBase](http://msdn.microsoft.com/library/ce9078b7-a750-4f47-b23e-90b83b783d80)   
 [Funciones y vistas de administración dinámica &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Vistas de administración dinámica relacionadas con la base de datos &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)  
  
  
