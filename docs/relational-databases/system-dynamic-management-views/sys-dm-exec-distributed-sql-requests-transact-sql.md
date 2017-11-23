---
title: Sys.dm_exec_distributed_sql_requests (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DM_EXEC_DISTRIBUTED_SQL_REQUESTS_TSQL
- SYS.DM_EXEC_DISTRIBUTED_SQL_REQUESTS_TSQL
- DM_EXEC_DISTRIBUTED_SQL_REQUESTS
dev_langs: TSQL
helpviewer_keywords:
- PolyBase,views
- PolyBase
- sys.dm_exec_distributed_requests management view
- dm_exec_distributed_requests management view
ms.assetid: d065dc01-35d4-472f-9554-53ac41e7d104
caps.latest.revision: "8"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 922f2ce79dbabe3670b3488299a530b2a28e0cc2
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="sysdmexecdistributedsqlrequests-transact-sql"></a>Sys.dm_exec_distributed_sql_requests (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2016-xxxx-asdw-pdw-md.md)]

  Contiene información acerca de todas las distribuciones de consulta SQL como parte de un paso de SQL en la consulta.  Esta vista muestra los datos de los últimos 1000 solicitudes; solicitudes activas siempre tienen los datos presentes en esta vista.  
  
|Nombre de la columna|Tipo de datos|Description|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|execution_id|**nvarchar (32)**|execution_id y step_index forman la clave para esta vista. Identificador numérico único asociado a la solicitud.|Vea el Id. de [sys.dm_exec_requests &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)|  
|step_index|**int**|Índice del paso de consulta de que esta distribución es parte.|Vea step_index en [sys.dm_exec_distributed_request_steps &#40; Transact-SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-exec-distributed-request-steps-transact-sql.md).|  
|compute_node_id|**int**|Tipo de la operación representada por este paso.|Vea compute_node_id en [sys.dm_exec_compute_nodes &#40; Transact-SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-exec-compute-nodes-transact-sql.md).|  
|distribution_id|**int**|Donde se ejecuta el paso.|Se establece en -1 para las solicitudes que se ejecutan en el ámbito del nodo no es el ámbito de distribución.|  
|status|**nvarchar (32)**|Estado de este paso|Activo, cancelado, completado, error, en cola|  
|error_id|**nvarchar(36)**|Identificador único del error asociado con este paso, si lo hay|Vea el Id. de [sys.dm_exec_compute_node_errors &#40; Transact-SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-exec-compute-node-errors-transact-sql.md), NULL si no se produjo ningún error.|  
|start_time|**datetime**|Hora en que inició el paso de ejecución|Menor o igual a la hora actual y mayor o igual que end_compile_time de la consulta a la que pertenece este paso.|  
|end_time|**datetime**|Hora a la que este paso completado su ejecución, cancelado o error.|Menor o igual a la hora actual e igual o mayor que start_time, establecido en NULL para conocer los pasos actualmente en ejecución o en cola.|  
|total_elapsed_time|**int**|Cantidad total de tiempo que se ha estado ejecutando el paso de consulta en milisegundos|Entre 0 y la diferencia entre start_time y. 0 para conocer los pasos en cola.|  
|row_count|**bigint**|Número total de filas cambiadas o devuelto por esta solicitud|Para conocer los pasos que no cambie o devolver datos, número de filas afectadas en caso contrario, es 0. Se establece en -1 para conocer los pasos DMS.|  
|spid|**int**|Id. de sesión en la instancia de SQL Server ejecutando la distribución de consultas||  
|comando|nvarchar(4000)|Contiene el texto completo de los comandos de este paso.|Cualquier cadena de solicitud válido para un paso. Truncarse si supera los 4000 caracteres.|  
  
## <a name="see-also"></a>Vea también  
 [PolyBase, solución de problemas con las vistas de administración dinámica](http://msdn.microsoft.com/library/ce9078b7-a750-4f47-b23e-90b83b783d80)   
 [Funciones y vistas de administración dinámica &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Base de datos relacionadas con vistas de administración dinámica &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)  
  
  
