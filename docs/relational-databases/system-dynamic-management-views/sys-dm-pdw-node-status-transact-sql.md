---
title: Sys.dm_pdw_node_status (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: pdw
ms.service: ''
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 8e263b65-81d0-49d0-8873-62ef424369d6
caps.latest.revision: 7
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Inactive
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 2ff2f23fcfc6314d06f55bca2b918d954f43514e
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="sysdmpdwnodestatus-transact-sql"></a>Sys.dm_pdw_node_status (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  Contiene información adicional (en [sys.dm_pdw_nodes &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-transact-sql.md)) sobre el rendimiento y el estado de todos los nodos de dispositivo. Muestra una fila por cada nodo en el dispositivo.  
  
|Nombre de la columna|Tipo de datos|Description|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|pdw_node_id|**int**|Identificador numérico único asociado al nodo.<br /><br /> Clave para esta vista.|Único en el dispositivo, independientemente del tipo.|  
|process_id|**int**|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]||  
|nombreproceso|**nvarchar(255)**|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]||  
|allocated_memory|**bigint**|Total asignado a memoria en este nodo.||  
|available_memory|**bigint**|Memoria total disponible en este nodo.||  
|process_cpu_usage|**bigint**|Uso de CPU de proceso total, en tics.||  
|total_cpu_usage|**bigint**|Uso total de CPU, en tics.||  
|Thread_Count|**bigint**|Número total de subprocesos en uso en este nodo.||  
|handle_count|**bigint**|Número total de identificadores en uso en este nodo.||  
|total_elapsed_time|**bigint**|Tiempo total transcurrido desde que el sistema, iniciar o reiniciar.|Tiempo total transcurrido desde que el sistema, iniciar o reiniciar. Si total_elapsed_time supera el valor máximo de un entero (24,8 días en milisegundos), provocará el error de materialización debido a desbordamiento.<br /><br /> El valor máximo en milisegundos equivale a días 24,8.|  
|is_available|**bit**|Marca que indica si este nodo está disponible.||  
|sent_time|**datetime**|Última vez que se ha enviado un paquete de red desde este nodo.||  
|received_time|**datetime**|Última hora de este nodo, ha recibido un paquete de red.||  
|error_id|**nvarchar(36)**|Identificador único del último error producido en este nodo.||  
  
## <a name="see-also"></a>Vea también  
 [Vistas de administración dinámica del almacenamiento de datos en paralelo y almacén de datos SQL &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
