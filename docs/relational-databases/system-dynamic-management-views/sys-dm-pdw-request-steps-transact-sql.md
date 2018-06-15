---
title: Sys.dm_pdw_request_steps (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 08/01/2017
ms.prod: ''
ms.prod_service: sql-data-warehouse, pdw
ms.reviewer: ''
ms.service: sql-data-warehouse
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: cc563e88-0d34-436e-b914-b60d6ee0d50b
caps.latest.revision: 10
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 421d8db6ec62035b8605fde1293f727f7a6dc917
ms.sourcegitcommit: 7019ac41524bdf783ea2c129c17b54581951b515
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/23/2018
ms.locfileid: "34467201"
---
# <a name="sysdmpdwrequeststeps-transact-sql"></a>Sys.dm_pdw_request_steps (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Contiene información acerca de todos los pasos que componen una solicitud determinada o de consulta en [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]. Muestra una fila por cada paso de consulta.  
  
|Nombre de la columna|Tipo de datos|Description|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|request_id|**nvarchar(32)**|request_id y step_index forman la clave para esta vista.<br /><br /> Identificador numérico único asociado a la solicitud.|Vea request_id en [sys.dm_pdw_exec_requests &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md).|  
|step_index|**int**|request_id y step_index forman la clave para esta vista.<br /><br /> La posición de este paso en la secuencia de pasos que componen la solicitud.|de 0 a (n-1) para una solicitud con n pasos.|  
|operation_type|**nvarchar(35)**|Tipo de operación representada por este paso.|**Operaciones de plan de consulta de DMS:** 'ReturnOperation', 'PartitionMoveOperation', 'MoveOperation', 'BroadcastMoveOperation', 'ShuffleMoveOperation', 'TrimMoveOperation', 'CopyOperation', 'DistributeReplicatedTableMoveOperation'<br /><br /> **Operaciones de plan de consulta SQL:** 'OnOperation', 'RemoteOperation'<br /><br /> **Otras operaciones del plan de consulta:** 'MetaDataCreateOperation', 'RandomIDOperation'<br /><br /> **Las operaciones externas para lecturas:** 'HadoopShuffleOperation', 'HadoopRoundRobinOperation', 'HadoopBroadcastOperation'<br /><br /> **Las operaciones externas de MapReduce:** 'HadoopJobOperation', 'HdfsDeleteOperation'<br /><br /> **Las operaciones externas para operaciones de escritura:** 'ExternalExportDistributedOperation', 'ExternalExportReplicatedOperation', 'ExternalExportControlOperation'<br /><br /> Para obtener más información, vea "Descripción los planes de consulta" en la [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)].|  
|distribution_type|**nvarchar(32)**|Tipo de distribución que se someterán este paso.|'AllNodes', 'AllDistributions', 'AllComputeNodes', 'ComputeNode', 'Distribution', 'SubsetNodes', 'SubsetDistributions', 'No se especifica'|  
|valor location_type|**nvarchar(32)**|Donde se ejecuta el paso.|'Compute', 'Control', 'DMS'|  
|status|**nvarchar(32)**|Estado de este paso.|Pendiente, en ejecución, completado, error, UndoFailed, PendingCancel, cancelado, deshacer, anulado|  
|error_id|**nvarchar(36)**|Identificador único del error asociado con este paso, si lo hay.|Consulte error_id de [sys.dm_pdw_errors &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-errors-transact-sql.md). Es NULL si no hubiera ningún error.|  
|start_time|**datetime**|Hora en que inició el paso de ejecución.|Menor o igual a la hora actual y mayor o igual que end_compile_time de la consulta a la que pertenece este paso. Para obtener más información sobre las consultas, vea [sys.dm_pdw_exec_requests &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md).|  
|end_time|**datetime**|Hora a la que este paso completado su ejecución, cancelado o error.|Menor o igual a la hora actual y mayor o igual que start_time. Establecer en NULL para conocer los pasos actualmente en ejecución o en cola.|  
|total_elapsed_time|**int**|Cantidad total de tiempo que se ha ejecutado el paso de consulta, en milisegundos.|Entre 0 y la diferencia entre start_time y. 0 para conocer los pasos en cola.<br /><br /> Si total_elapsed_time supera el valor máximo de un entero, continuará total_elapsed_time sea el valor máximo. Esta condición generará la advertencia "se superó el valor máximo."<br /><br /> El valor máximo en milisegundos equivale a días 24,8.|  
|row_count|**bigint**|Número total de filas cambiado o devuelto por esta solicitud.|0 para conocer los pasos que no cambie o devolver datos. En caso contrario, número de filas afectadas.|  
|comando|**nvarchar(4000)**|Contiene el texto completo de los comandos de este paso.|Cualquier cadena de solicitud válido para un paso. NULL si la operación es del tipo MetaDataCreateOperation. Truncarse si supera los 4000 caracteres.|  
  
 Para obtener información sobre el número máximo de filas conserva esta vista, vea la sección valores máximos de vista de sistema en el "mínimo y máximo valores" en el [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)].  
  
## <a name="see-also"></a>Vea también  
 [Vistas de administración dinámica del almacenamiento de datos en paralelo y almacén de datos SQL &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
