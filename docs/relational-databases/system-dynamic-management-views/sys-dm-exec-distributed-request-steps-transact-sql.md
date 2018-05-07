---
title: Sys.dm_exec_distributed_request_steps (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- SYS.DM_EXEC_DISTRIBUTED_REQUEST_STEPS_TSQL
- DM_EXEC_DISTRIBUTED_REQUEST_STEPS_TSQL
- DM_EXEC_DISTRIBUTED_REQUEST_STEPS
dev_langs:
- TSQL
helpviewer_keywords:
- PolyBase,views
- PolyBase
- dm_exec_distributed_request_steps
- sys.dm_exec_distributed_request_steps management view
ms.assetid: 1954541d-b716-4e03-8fcc-7022f428e01d
caps.latest.revision: 8
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 503193a77d068c11599bd34950240c7f08cebb9b
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2018
---
# <a name="sysdmexecdistributedrequeststeps-transact-sql"></a>sys.dm_exec_distributed_request_steps (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2016-xxxx-asdw-pdw-md.md)]

  Contiene información sobre todos los pasos que componen una determinada solicitud de PolyBase o la consulta. Muestra una fila por cada paso de consulta.  
  
|Nombre de la columna|Tipo de datos|Description|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|execution_id|**int**|execution_id y step_index forman la clave para esta vista. Identificador numérico único asociado a la solicitud.|Vea el Id. de [sys.dm_exec_requests &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md).|  
|step_index|**int**|La posición de este paso en la secuencia de pasos que componen la solicitud.|de 0 a (n-1) para una solicitud con n pasos.|  
|operation_type|**nvarchar(128)**|Tipo de la operación representada por este paso.|'MoveOperation', 'OnOperation', 'RandomIDOperation', 'RemoteOperation', 'ReturnOperation', 'ShuffleMoveOperation', 'TempTablePropertiesOperation', 'DropDiagnosticsNotifyOperation', 'HadoopShuffleOperation', 'HadoopBroadCastOperation' 'HadoopRoundRobinOperation'|  
|distribution_type|**nvarchar(32)**|Donde se ejecuta el paso.|'AllComputeNodes ',' AllDistributions', 'ComputeNode', 'Distribution', 'AllNodes', 'SubsetNodes', 'SubsetDistributions',' no se especifica'.|  
|valor location_type|**nvarchar(32)**|Donde se ejecuta el paso.|'Compute', 'Head' o 'DMS'. Todos los pasos de movimiento de datos muestran 'DMS'.|  
|status|**nvarchar(32)**|Estado de este paso|'Pendiente', 'Running', 'Complete', 'Error', 'UndoFailed', 'PendingCancel', 'cancela', 'Deshacer', 'Anulan'|  
|error_id|**nvarchar(36)**|Identificador único del error asociado con este paso, si lo hay|Vea el Id. de [sys.dm_exec_compute_node_errors &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-compute-node-errors-transact-sql.md), NULL si no se produjo ningún error.|  
|start_time|**datetime**|Hora en que inició el paso de ejecución|Menor o igual a la hora actual y mayor o igual que end_compile_time de la consulta a la que pertenece este paso.|  
|end_time|**datetime**|Hora a la que este paso completado su ejecución, cancelado o error.|Menor o igual a la hora actual e igual o mayor que start_time, establecido en NULL para conocer los pasos actualmente en ejecución o en cola.|  
|total_elapsed_time|**int**|Cantidad total de tiempo que se ha estado ejecutando el paso de consulta en milisegundos|Entre 0 y la diferencia entre start_time y. 0 para conocer los pasos en cola.|  
|row_count|**bigint**|Número total de filas cambiadas o devuelto por esta solicitud|Para conocer los pasos que no cambie o devolver datos, número de filas afectadas en caso contrario, es 0. Se establece en -1 para conocer los pasos DMS.|  
|comando|nvarchar(4000)|Contiene el texto completo de los comandos de este paso.|Cualquier cadena de solicitud válido para un paso. Truncarse si supera los 4000 caracteres.|  
  
## <a name="see-also"></a>Vea también  
 [PolyBase, solución de problemas con las vistas de administración dinámica](http://msdn.microsoft.com/library/ce9078b7-a750-4f47-b23e-90b83b783d80)   
 [Funciones y vistas de administración dinámica &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Vistas de administración dinámica relacionadas con la base de datos &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)  
  
  
