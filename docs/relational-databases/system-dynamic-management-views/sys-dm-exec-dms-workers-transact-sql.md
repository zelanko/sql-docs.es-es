---
title: Sys. dm_exec_dms_workers (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2019
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- SYS.DM_EXEC_DMS_WORKERS_TSQL
- DM_EXEC_DMS_WORKERS_TSQL
- DM_EXEC_DMS_WORKERS
dev_langs:
- TSQL
helpviewer_keywords:
- PolyBase,views
- PolyBase
- dm_exec_dms_workers management view
- sys.dm_exec_dms_workers management view
ms.assetid: f468da29-78c3-4f10-8a3c-17905bbf46f2
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 4951954bb9f6336c2c984a8d74c2224eab4dfbb0
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/05/2020
ms.locfileid: "82821095"
---
# <a name="sysdm_exec_dms_workers-transact-sql"></a>Sys. dm_exec_dms_workers (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2016-xxxx-asdw-pdw-md.md)]

  Contiene información sobre todos los trabajadores que completan los pasos de DMS.  
  
 Esta vista muestra los datos de las últimas 1000 solicitudes y solicitudes activas; las solicitudes activas siempre tienen los datos presentes en esta vista.  
  
|Nombre de columna|Tipo de datos|Descripción|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|execution_id|`nvarchar(32)`|Consulta de la que forma parte este trabajador DMS. request_id, step_index y dms_step_index forman la clave de esta vista.||  
|step_index|`int`|Paso de consulta del que forma parte este trabajador de DMS.|Vea índice de paso en [Sys. dm_exec_distributed_request_steps &#40;&#41;de Transact-SQL ](../../relational-databases/system-dynamic-management-views/sys-dm-exec-distributed-request-steps-transact-sql.md).|  
|dms_step_index|`int`|Paso del plan DMS en el que se ejecuta este trabajador.|Vea [Sys. dm_exec_dms_workers (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-exec-dms-workers-transact-sql.md)|  
|compute_node_id|`int`|Nodo en el que se está ejecutando el trabajo.|Vea [Sys. dm_exec_compute_nodes &#40;&#41;de Transact-SQL ](../../relational-databases/system-dynamic-management-views/sys-dm-exec-compute-nodes-transact-sql.md).|  
|distribution_id|`int`|||  
|tipo|`nvarcha(32)`|||  
|status|`nvarchar(32)`|Estado de este paso|' Pending ', ' Running ', ' complete ', ' failed ', ' UndoFailed ', ' PendingCancel ', ' Canceled ', ' Undone ', ' Aborted '|  
|bytes_per_sec|`bigint`|||  
|bytes_processed|`bigint`|||  
|rows_processed|`bigint`|||  
|start_time|`datetime`|Hora a la que se inició la ejecución del paso|Menor o igual que la hora actual y mayor o igual que end_compile_time de la consulta a la que pertenece este paso.|  
|end_time|`datetime`|Hora a la que se completó la ejecución de este paso, se canceló o dio error.|Menor o igual que la hora actual y mayor o igual que start_time, se establece en NULL para los pasos que se encuentran actualmente en ejecución o en cola.|  
|total_elapsed_time|`int`|Cantidad total de tiempo que se ha estado ejecutando el paso de la consulta, en milisegundos|Entre 0 y la diferencia entre end_time y start_time. 0 para los pasos en cola.|  
|cpu_time|`bigint`|||  
|query_time|`int`|||  
|buffers_available|`int`|||  
|dms_cpid|`int`|||  
|sql_spid|`int`|||  
|error_id|`nvarchar(36)`|||  
|source_info|`nvarchar(4000)`|||  
|destination_info|`nvarchar(4000)`|||  
|.|`nvarchar(4000)`|||
|compute_pool_id|`int`|Identificador único para el grupo.|

## <a name="see-also"></a>Consulte también  
 [Solución de problemas de polybase con vistas de administración dinámica](https://msdn.microsoft.com/library/ce9078b7-a750-4f47-b23e-90b83b783d80)   
 [Funciones y vistas de administración dinámica &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Vistas de administración dinámica relacionadas con bases de datos &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)  
  
  
