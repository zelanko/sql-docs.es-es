---
title: Sys.dm_pdw_sql_requests (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: ''
ms.prod_service: sql-data-warehouse, pdw
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 44e19609-902c-46cf-acdf-19ea75011365
author: ronortloff
ms.author: rortloff
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: cf7c48e09fc0ade7db65e2d67984be07914df90d
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/15/2018
ms.locfileid: "51664080"
---
# <a name="sysdmpdwsqlrequests-transact-sql"></a>Sys.dm_pdw_sql_requests (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Contiene información sobre todas las distribuciones de consulta de SQL Server como parte de un paso de SQL en la consulta.  
  
|Nombre de la columna|Tipo de datos|Descripción|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|request_id|**nvarchar(32)**|Identificador único de la consulta a la que pertenece esta distribución de la consulta SQL.<br /><br /> valor de distribution_id, step_index y request_id forman la clave para esta vista.|Vea request_id en [sys.dm_pdw_exec_requests &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md).|  
|step_index|**int**|Índice del paso de consulta de que esta distribución es parte.<br /><br /> valor de distribution_id, step_index y request_id forman la clave para esta vista.|Vea step_index en [sys.dm_pdw_request_steps &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql.md).|  
|pdw_node_id|**int**|Identificador único del nodo en el que se ejecutará esta distribución de la consulta.|Consulte node_id en [sys.dm_pdw_nodes &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-transact-sql.md).|  
|distribution_id|**int**|Identificador único de la distribución en el que se ejecutará esta distribución de la consulta.<br /><br /> valor de distribution_id, step_index y request_id forman la clave para esta vista.|Consulte en el valor de distribution_id [sys.pdw_distributions &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-distributions-transact-sql.md). Se establece en -1 para las solicitudes que se ejecutan en el ámbito del nodo, no en el ámbito de distribución.|  
|status|**nvarchar(32)**|Estado actual de la distribución de la consulta.|Pendiente, ejecutar, con error, cancelado, completado, anulado, CancelSubmitted|  
|error_id|**nvarchar(36)**|Identificador único del error asociadas con esta distribución de la consulta, si procede.|Vea error_id en [sys.dm_pdw_errors &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-errors-transact-sql.md). Se establece en NULL si se ha producido ningún error.|  
|start_time|**datetime**|Tiempo de distribución en la consulta que inició la ejecución.|Menor o igual a la hora actual y mayor o igual que start_time del paso de consulta pertenece esta distribución de consulta|  
|end_time|**datetime**|Hora a la que esta distribución consulta completado su ejecución, cancelada o error.|Mayor o igual a la hora de inicio, o se establece en NULL si la distribución de la consulta está en curso o en cola.|  
|total_elapsed_time|**int**|Representa el tiempo que se ejecuta la distribución de la consulta, en milisegundos.|Mayor o igual que 0. Igual que las diferencias entre start_time y end_time para completado, error o cancelar las distribuciones de la consulta.<br /><br /> Si total_elapsed_time supera el valor máximo de un entero, continuará total_elapsed_time sea el valor máximo. Esta condición generará la advertencia "se superó el valor máximo."<br /><br /> El valor máximo en milisegundos equivale a 24,8 días.|  
|row_count|**bigint**|Número de filas cambiado o lee esta distribución de la consulta.|-1 para las operaciones que no cambian ni devolver datos, como CREATE TABLE y DROP TABLE.|  
|spid|**int**|Id. de sesión en la instancia de SQL Server que ejecuta la distribución de la consulta.||  
|comando|**nvarchar(4000)**|Texto completo de comandos para esta distribución de la consulta.|Cualquier cadena de consulta o de solicitud válido.|  
  
 Para obtener información sobre el número máximo de filas retenidas por esta vista, consulte la sección de valores máximos de la vista del sistema en el [valores mínimos y máximos (SQL Server PDW)](https://msdn.microsoft.com/5243f018-2713-45e3-9b61-39b2a57401b9) tema.  
  
## <a name="see-also"></a>Vea también  
 [Vistas de administración dinámica de almacenamiento de datos en paralelo y SQL Data Warehouse &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
