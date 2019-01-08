---
title: Sys.dm_exec_external_work (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- DM_EXEC_EXTERNAL_WORK
- DM_EXEC_EXTERNAL_WORK_TSQL
- SYS.DM_EXEC_EXTERNAL_WORK_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_exec_external_work management view
- dm_exec_external_work management view
- PolyBase,views
- PolyBase
ms.assetid: 7597d97b-1fde-4135-ac35-4af12968f300
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: a53a32f01dcf4646ee0bc12843c188b9b0e8e4c0
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/27/2018
ms.locfileid: "52418629"
---
# <a name="sysdmexecexternalwork-transact-sql"></a>sys.dm_exec_external_work (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2016-xxxx-asdw-pdw-md.md)]

  Devuelve información acerca de la carga de trabajo por trabajo, en cada nodo de proceso.  
  
 Sys.dm_exec_external_work de consulta para identificar el trabajo en marcha para comunicarse con el origen de datos externo (por ejemplo, Hadoop o externas de SQL Server).  
  
|Nombre de la columna|Tipo de datos|Descripción|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|execution_id|**nvarchar(32)**|Identificador único para las consultas de PolyBase asociado.|Consulte *request_ID* en [sys.dm_exec_requests &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md).|  
|step_index|**int**|La solicitud está realizando este trabajador.|Consulte *step_index* en [sys.dm_exec_requests &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md).|  
|dms_step_index|**int**|El paso en el plan DMS que se está ejecutando este trabajo.|Consulte [sys.dm_exec_dms_workers &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-dms-workers-transact-sql.md).|  
|compute_node_id|**int**|El nodo del trabajador se ejecuta en.|Consulte [sys.dm_exec_compute_nodes &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-compute-nodes-transact-sql.md).|  
|Tipo|**nvarchar(60)**|El tipo de trabajo externo.|"División de archivos"|  
|work_id|**int**|Id. de la división real.|Mayor o igual que 0.|  
|input_name|**nvarchar(4000)**|Nombre de la entrada de lectura|Nombre de archivo cuando el uso de Hadoop.|  
|read_location|**bigint**|Desplazamiento o leer la ubicación.|Desplazamiento del archivo que se va a leer.|  
|bytes_processed|**bigint**|Número total de bytes procesado por este trabajador.|Mayor o igual que 0.|  
|length|**bigint**|Longitud de la división o bloque HDFS en el caso de Hadoop|Definibles por el usuario. El valor predeterminado es 64M|  
|status|**nvarchar(32)**|Estado del trabajo|Pendiente, en proceso, terminado, error, anulado|  
|start_time|**datetime**|A partir del trabajo||  
|end_time|**datetime**|Finalización del trabajo||  
|total_elapsed_time|**int**|Tiempo total en milisegundos||  
  
## <a name="see-also"></a>Vea también  
 [Solución de problemas con las vistas de administración dinámica de PolyBase](https://msdn.microsoft.com/library/ce9078b7-a750-4f47-b23e-90b83b783d80)   
 [Funciones y vistas de administración dinámica &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Vistas de administración dinámica relacionadas con la base de datos &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)  
  
  
