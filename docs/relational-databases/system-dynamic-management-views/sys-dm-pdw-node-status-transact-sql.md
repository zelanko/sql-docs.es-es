---
title: Sys.dm_pdw_node_status (Transact-SQL) | Microsoft Docs
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
ms.assetid: 8e263b65-81d0-49d0-8873-62ef424369d6
caps.latest.revision: 7
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 423bae3ce66e21721e328a23d51a8356be40ea2a
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2018
ms.locfileid: "38000807"
---
# <a name="sysdmpdwnodestatus-transact-sql"></a>Sys.dm_pdw_node_status (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  Contiene información adicional (a través de [sys.dm_pdw_nodes &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-transact-sql.md)) sobre el rendimiento y el estado de todos los nodos del dispositivo. Muestra una fila por cada nodo en el dispositivo.  
  
|Nombre de la columna|Tipo de datos|Descripción|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|pdw_node_id|**int**|Identificador numérico único asociado al nodo.<br /><br /> Clave para esta vista.|Es único en todo el dispositivo, independientemente del tipo.|  
|process_id|**int**|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]||  
|nombreDeProceso|**nvarchar(255)**|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]||  
|allocated_memory|**bigint**|Memoria total asignada en este nodo.||  
|available_memory|**bigint**|Memoria total disponible en este nodo.||  
|process_cpu_usage|**bigint**|Uso de CPU de proceso total, en tics.||  
|total_cpu_usage|**bigint**|Uso total de CPU, en tics.||  
|Thread_Count|**bigint**|Número total de subprocesos en uso en este nodo.||  
|handle_count|**bigint**|Número total de identificadores en uso en este nodo.||  
|total_elapsed_time|**bigint**|Tiempo total transcurrido desde que el sistema, iniciar o reiniciar.|Tiempo total transcurrido desde que el sistema, iniciar o reiniciar. Si total_elapsed_time supera el valor máximo de un entero (24,8 días en milisegundos), provocará el error de materialización debido al desbordamiento.<br /><br /> El valor máximo en milisegundos equivale a 24,8 días.|  
|is_available|**bit**|Marca que indica si este nodo está disponible.||  
|sent_time|**datetime**|Última vez que se envió un paquete de red por este nodo.||  
|received_time|**datetime**|Última vez que se recibió un paquete de red por este nodo.||  
|error_id|**nvarchar(36)**|Identificador único del último error que se produjo en este nodo.||  
  
## <a name="see-also"></a>Vea también  
 [Vistas de administración dinámica de almacenamiento de datos en paralelo y SQL Data Warehouse &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
