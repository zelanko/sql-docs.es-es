---
title: Sys.dm_exec_external_work (Transact-SQL) | Documentos de Microsoft
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
- DM_EXEC_EXTERNAL_WORK
- DM_EXEC_EXTERNAL_WORK_TSQL
- SYS.DM_EXEC_EXTERNAL_WORK_TSQL
dev_langs: TSQL
helpviewer_keywords:
- sys.dm_exec_external_work management view
- dm_exec_external_work management view
- PolyBase,views
- PolyBase
ms.assetid: 7597d97b-1fde-4135-ac35-4af12968f300
caps.latest.revision: "8"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b3287e4ae13d7ea06ab00197067ba856e601b9c7
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="sysdmexecexternalwork-transact-sql"></a>Sys.dm_exec_external_work (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2016-xxxx-asdw-pdw-md.md)]

  Devuelve información sobre la carga de trabajo por trabajo, en cada nodo de ejecución.  
  
 Sys.dm_exec_external_work de consulta para identificar el trabajo terminado para comunicarse con el origen de datos externo (por ejemplo, Hadoop o externos de SQL Server).  
  
|Nombre de la columna|Tipo de datos|Description|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|execution_id|**nvarchar (32)**|Identificador único para las consultas de PolyBase asociado.|Vea *request_ID* en [sys.dm_exec_requests &#40; Transact-SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md).|  
|step_index|**int**|La solicitud está realizando este trabajador.|Vea *step_index* en [sys.dm_exec_requests &#40; Transact-SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md).|  
|dms_step_index|**int**|Paso a paso en el plan DMS que se está ejecutando este trabajo.|Vea [sys.dm_exec_dms_workers &#40; Transact-SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-exec-dms-workers-transact-sql.md).|  
|compute_node_id|**int**|El nodo el trabajador está ejecutando.|Vea [sys.dm_exec_compute_nodes &#40; Transact-SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-exec-compute-nodes-transact-sql.md).|  
|Tipo|**nvarchar (60)**|El tipo de trabajo externo.|'Archivo división'|  
|work_id|**int**|Id. de la división real.|Mayor o igual que 0.|  
|input_name|**nvarchar(4000)**|Nombre de la entrada que debe leerse|Nombre de archivo cuando se usa Hadoop.|  
|read_location|**bigint**|Desplazar o leer la ubicación.|Desplazamiento del archivo que desea leer.|  
|bytes_processed|**bigint**|Número total de bytes procesado por este trabajador.|Mayor o igual que 0.|  
|length|**bigint**|Longitud de la división o un bloque HDFS en el caso de Hadoop|Definibles por el usuario. El valor predeterminado es 64M|  
|status|**nvarchar (32)**|Estado del trabajador|Pendiente, procesamiento, realizar, no se pudo, anulado|  
|start_time|**datetime**|A partir del trabajo||  
|end_time|**datetime**|Finalización del trabajo||  
|total_elapsed_time|**int**|Tiempo total en milisegundos||  
  
## <a name="see-also"></a>Vea también  
 [PolyBase, solución de problemas con las vistas de administración dinámica](http://msdn.microsoft.com/library/ce9078b7-a750-4f47-b23e-90b83b783d80)   
 [Funciones y vistas de administración dinámica &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Base de datos relacionadas con vistas de administración dinámica &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)  
  
  
