---
title: sys.dm_pdw_sql_requests (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
ms.prod: 
ms.prod_service: sql-data-warehouse, pdw
ms.service: sql-data-warehouse
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 44e19609-902c-46cf-acdf-19ea75011365
caps.latest.revision: 
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 8f345dbbdda12ade363b4d5f8a52f5cca80e564f
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/03/2018
---
# <a name="sysdmpdwsqlrequests-transact-sql"></a>sys.dm_pdw_sql_requests (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Contiene información acerca de todas las distribuciones de consulta de SQL Server como parte de un paso de SQL en la consulta.  
  
|Nombre de la columna|Tipo de datos|Description|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|request_id|**nvarchar(32)**|Identificador único de la consulta a la que pertenece esta distribución de consultas SQL.<br /><br /> request_id, step_index y distribution_id forman la clave para esta vista.|See request_id in [sys.dm_pdw_exec_requests &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md).|  
|step_index|**int**|Índice del paso de consulta de que esta distribución es parte.<br /><br /> request_id, step_index y distribution_id forman la clave para esta vista.|See step_index in [sys.dm_pdw_request_steps &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql.md).|  
|pdw_node_id|**int**|Identificador único del nodo en el que se ejecutará esta distribución de la consulta.|Vea node_id en [sys.dm_pdw_nodes &#40; Transact-SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-transact-sql.md).|  
|distribution_id|**int**|Identificador único de la distribución en el que se ejecutará esta distribución de la consulta.<br /><br /> request_id, step_index y distribution_id forman la clave para esta vista.|Vea distribution_id en [sys.pdw_distributions &#40; Transact-SQL &#41; ](../../relational-databases/system-catalog-views/sys-pdw-distributions-transact-sql.md). Se establece en -1 para las solicitudes que se ejecutan en el ámbito de nodo, no en el ámbito de distribución.|  
|status|**nvarchar(32)**|Estado actual de la distribución de la consulta.|Pendiente, ejecuta, error, cancelado, completado, anulado, CancelSubmitted|  
|error_id|**nvarchar(36)**|Identificador único del error asociado con esta distribución de la consulta, si lo hay.|Vea error_id en [sys.dm_pdw_errors &#40; Transact-SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-errors-transact-sql.md). Se establece en NULL si se ha producido ningún error.|  
|start_time|**datetime**|Hora a qué consulta distribución inició la ejecución.|Menor o igual a la hora actual y mayor o igual que start_time del paso de consulta pertenece esta distribución de consulta|  
|end_time|**datetime**|Hora a la que esta distribución consulta completó su ejecución, cancelada o error.|Mayor o igual a la hora de inicio, o se establece en NULL si la distribución de la consulta está en curso o en cola.|  
|total_elapsed_time|**int**|Representa la hora en que se ha ejecutado la distribución de la consulta, en milisegundos.|Mayor o igual que 0. Es igual a las diferencias entre start_time y end_time para completado, error o cancelar las distribuciones de consulta.<br /><br /> Si total_elapsed_time supera el valor máximo de un entero, continuará total_elapsed_time sea el valor máximo. Esta condición generará la advertencia "se superó el valor máximo."<br /><br /> El valor máximo en milisegundos equivale a días 24,8.|  
|row_count|**bigint**|Número de filas cambiado o lee la distribución de esta consulta.|-1 para las operaciones que no cambian ni devolver datos, como CREATE TABLE y DROP TABLE.|  
|spid|**int**|Id. de sesión en la instancia de SQL Server ejecutando la distribución de la consulta.||  
|comando|**nvarchar(4000)**|Texto completo de comandos para la distribución de esta consulta.|Cualquier cadena de consulta o de solicitud válido.|  
  
 Para obtener información sobre el número máximo de filas conserva esta vista, vea la sección valores máximos de vista de sistema en el [valores mínimo y máximo (SQL Server PDW)](http://msdn.microsoft.com/en-us/5243f018-2713-45e3-9b61-39b2a57401b9) tema.  
  
## <a name="see-also"></a>Vea también  
 [Almacenamiento de datos SQL y vistas de administración dinámica de almacenamiento de datos en paralelo &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
