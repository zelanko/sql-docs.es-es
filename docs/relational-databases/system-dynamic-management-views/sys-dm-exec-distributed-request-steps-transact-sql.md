---
title: Sys.dm_exec_distributed_request_steps (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
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
ms.openlocfilehash: f226ff8c5f18a0e812c6a457fe3382cb8f7b8d84
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2018
ms.locfileid: "37982597"
---
# <a name="sysdmexecdistributedrequeststeps-transact-sql"></a>sys.dm_exec_distributed_request_steps (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2016-xxxx-asdw-pdw-md.md)]

  Contiene información sobre todos los pasos que componen una solicitud determinada de PolyBase o una consulta. Muestra una fila por cada paso de consulta.  
  
|Nombre de la columna|Tipo de datos|Descripción|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|execution_id|**int**|execution_id y step_index conforman la clave para esta vista. Identificador numérico único asociado a la solicitud.|Vea el Id. de [sys.dm_exec_requests &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md).|  
|step_index|**int**|La posición de este paso en la secuencia de pasos que componen la solicitud.|de 0 a (n-1) para una solicitud de n pasos.|  
|operation_type|**nvarchar(128)**|Tipo de la operación representada por este paso.|'MoveOperation', 'OnOperation', 'RandomIDOperation', 'RemoteOperation', 'ReturnOperation', 'ShuffleMoveOperation', 'TempTablePropertiesOperation', 'DropDiagnosticsNotifyOperation', 'HadoopShuffleOperation', 'HadoopBroadCastOperation', 'HadoopRoundRobinOperation'|  
|distribution_type|**nvarchar(32)**|Donde se ejecuta el paso.|'AllComputeNodes "," AllDistributions', 'ComputeNode', 'Distribution', 'AllNodes', 'SubsetNodes', 'SubsetDistributions',' no se especifica'.|  
|valor location_type|**nvarchar(32)**|Donde se ejecuta el paso.|'Compute', 'Principal' o 'DMS'. Todos los pasos de movimiento de datos muestran 'DMS'.|  
|status|**nvarchar(32)**|Estado de este paso.|'Pendiente', 'Running', 'Completa', 'Error', 'UndoFailed', 'PendingCancel', 'cancela', 'Deshacer', 'Anulan'|  
|error_id|**nvarchar(36)**|Identificador único del error asociado con este paso, si procede|Vea el Id. de [sys.dm_exec_compute_node_errors &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-compute-node-errors-transact-sql.md), NULL si se ha producido ningún error.|  
|start_time|**datetime**|Hora en que inició el paso de ejecución|Menor o igual a la hora actual y mayor o igual que end_compile_time de la consulta a la que pertenece este paso.|  
|end_time|**datetime**|Hora a la que este paso completado su ejecución, cancelado o error.|Menor o igual a la hora actual y mayor o igual a start_time, establecido en NULL para conocer los pasos actualmente en ejecución o en cola.|  
|total_elapsed_time|**int**|Cantidad total de tiempo que ha estado ejecutando el paso de consulta, en milisegundos|Entre 0 y la diferencia existente entre start_time y end_time. 0 para los pasos en cola.|  
|row_count|**bigint**|Número total de filas modificadas o devuelto por esta solicitud|Para conocer los pasos que no cambie o devolver datos, el número de filas afectadas en caso contrario, es 0. Se establece en -1 para conocer los pasos DMS.|  
|comando|nvarchar(4000)|Contiene el texto completo del comando de este paso.|Cualquier cadena de solicitud válida para un paso. Truncarse si supera los 4000 caracteres.|  
  
## <a name="see-also"></a>Vea también  
 [Solución de problemas con las vistas de administración dinámica de PolyBase](http://msdn.microsoft.com/library/ce9078b7-a750-4f47-b23e-90b83b783d80)   
 [Funciones y vistas de administración dinámica &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Vistas de administración dinámica relacionadas con la base de datos &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)  
  
  
