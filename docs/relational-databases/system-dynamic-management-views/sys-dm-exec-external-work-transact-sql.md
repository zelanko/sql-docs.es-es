---
title: Sys. dm_exec_external_work (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2019
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
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: b0ba7eecc8e117e429f6992622d0c7bb2073f86a
ms.sourcegitcommit: 26868c8ac3217176b370d972a26d307598a10328
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/05/2019
ms.locfileid: "74834334"
---
# <a name="sysdm_exec_external_work-transact-sql"></a>Sys. dm_exec_external_work (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2016-xxxx-asdw-pdw-md.md)]

  Devuelve información sobre la carga de trabajo por trabajador en cada nodo de proceso.  
  
 Consulte sys. dm_exec_external_work para identificar el trabajo que se va a establecer para comunicarse con el origen de datos externo (por ejemplo, Hadoop o SQL Server externo).  
  
|Nombre de columna|Tipo de datos|Descripción|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|execution_id|`nvarchar(32)`|Identificador único para la consulta de polybase asociada.|Vea *request_ID* en [sys. dm_exec_requests &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md).|  
|step_index|`int`|Solicitud que está realizando este trabajador.|Vea *step_index* en [sys. dm_exec_requests &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md).|  
|dms_step_index|`int`|Paso del plan DMS en el que se está ejecutando este trabajador.|Vea [Sys. dm_exec_dms_workers &#40;&#41;de Transact-SQL ](../../relational-databases/system-dynamic-management-views/sys-dm-exec-dms-workers-transact-sql.md).|  
|compute_node_id|`int`|Nodo en el que se está ejecutando el trabajo.|Vea [Sys. dm_exec_compute_nodes &#40;&#41;de Transact-SQL ](../../relational-databases/system-dynamic-management-views/sys-dm-exec-compute-nodes-transact-sql.md).|  
|tipo|`nvarchar(60)`|Tipo de trabajo externo.|' División de archivos '|  
|work_id|`int`|IDENTIFICADOR de la división real.|Mayor o igual que 0.|  
|input_name|`nvarchar(4000)`|Nombre de la entrada que se va a leer|Nombre de archivo cuando se usa Hadoop.|  
|read_location|`bigint`|Desplazamiento o ubicación de lectura.|Desplazamiento del archivo que se va a leer.|  
|bytes_processed|`bigint`|Número total de bytes asignados para el procesamiento de datos por parte de este trabajador. Es posible que esto no represente necesariamente los datos totales devueltos por la consulta. |Mayor o igual que 0.|  
|length|`bigint`|Longitud de la división o el bloque HDFS en el caso de Hadoop|Definible por el usuario. El valor predeterminado es 64M|  
|status|`nvarchar(32)`|Estado del trabajador|Pending, Processing, done, failed, Aborted|  
|start_time|`datetime`|Inicio del trabajo||  
|end_time|`datetime`|Fin del trabajo||  
|total_elapsed_time|`int`|Tiempo total en milisegundos||
|compute_pool_id|`int`|Identificador único para el grupo.|

## <a name="see-also"></a>Véase también  
 [Solución de problemas de polybase con vistas de administración dinámica](https://msdn.microsoft.com/library/ce9078b7-a750-4f47-b23e-90b83b783d80)   
 [Funciones y vistas de administración dinámica &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Vistas de administración dinámica relacionadas con bases de datos &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)  
  
  
