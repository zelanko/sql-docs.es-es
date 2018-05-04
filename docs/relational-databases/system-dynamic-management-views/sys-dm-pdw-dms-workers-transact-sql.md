---
title: Sys.dm_pdw_dms_workers (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/07/2017
ms.prod: ''
ms.prod_service: sql-data-warehouse, pdw
ms.service: sql-data-warehouse
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 0a284d18-3c46-4ffa-bcc9-689e660ee8b4
caps.latest.revision: 7
author: barbkess
ms.author: barbkess
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: ad9e41d1092f17d2fb5c37b7f16d2f6be056506b
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="sysdmpdwdmsworkers-transact-sql"></a>Sys.dm_pdw_dms_workers (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Contiene información sobre todos los trabajadores completar los pasos DMS.  
  
|Nombre de la columna|Tipo de datos|Description|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|request_id|**nvarchar(32)**|Consulta que forma parte de este trabajo DMS.<br /><br /> request_id, step_index y dms_step_index forman la clave para esta vista.|Vea request_id en [sys.dm_pdw_exec_requests &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md).|  
|step_index|**int**|Consultar el paso de de que este trabajo DMS forma parte.<br /><br /> request_id, step_index y dms_step_index forman la clave para esta vista.|Vea step_index en [sys.dm_pdw_request_steps &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql.md).|  
|dms_step_index|**int**|Paso a paso en el plan DMS que se está ejecutando este trabajo.<br /><br /> request_id, step_index y dms_step_index forman la clave para esta vista.||  
|pdw_node_id|**int**|Nodo que se está ejecutando el trabajo.|Vea node_id en [sys.dm_pdw_nodes &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-transact-sql.md).|  
|distribution_id|**Int**|Distribución que se ejecuta el trabajo, si existe.|Vea distribution_id en [sys.pdw_distributions &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-distributions-transact-sql.md).|  
|Tipo|**nvarchar(32)**|Tipo de subproceso de trabajo DMS que representa esta entrada.|'DIRECT_CONVERTER', 'DIRECT_READER', 'FILE_READER', 'HASH_CONVERTER', 'HASH_READER', 'ROUNDROBIN_CONVERTER', 'EXPORT_READER', 'EXTERNAL_READER', 'EXTERNAL_WRITER', 'PARALLEL_COPY_READER', 'REJECT_WRITER', 'ESCRITOR'|  
|status|**nvarchar(32)**|Estado del trabajador DMS.|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]|  
|bytes_per_sec|**bigint**|Rendimiento de lectura o escritura en el último segundo.|Mayor o igual que 0. Es NULL si la consulta se ha cancelado o no se pudo para ejecuta el trabajo.|  
|bytes_processed|**bigint**|Número total de bytes procesado por este trabajador.|Mayor o igual que 0. Es NULL si la consulta se ha cancelado o no se pudo para ejecuta el trabajo.|  
|rows_processed|**bigint**|Número de filas leídas o escritas para este trabajador.|Mayor o igual que 0. Es NULL si la consulta se ha cancelado o no se pudo para ejecuta el trabajo.|  
|start_time|**datetime**|Hora en que empezó la ejecución de este trabajo.|Mayor o igual a la hora de inicio del paso de consulta al que pertenece este trabajador. Vea [sys.dm_pdw_request_steps &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql.md).|  
|end_time|**datetime**|Tiempo en el que finalizó la ejecución, no se pudo o se canceló.|NULL para los trabajos en curso o en cola. En caso contrario, es mayor que start_time.|  
|total_elapsed_time|**int**|Tiempo total empleado en ejecución, en milisegundos.|Mayor o igual que 0.<br /><br /> Tiempo total transcurrido desde que el sistema, iniciar o reiniciar. Si total_elapsed_time supera el valor máximo de un entero (24,8 días en milisegundos), provocará el error de materialización debido a desbordamiento.<br /><br /> El valor máximo en milisegundos equivale a días 24,8.|  
|cpu_time|**bigint**|Tiempo de CPU utilizado por este trabajador, en milisegundos.|Mayor o igual que 0.|  
|query_time|**int**|Período de tiempo antes de SQL inicia devolver filas para el subproceso, en milisegundos.|Mayor o igual que 0.|  
|buffers_available|**int**|Número de búferes sin usar.| Es NULL si la consulta se ha cancelado o no se pudo para ejecuta el trabajo.|  
|sql_spid|**int**|Id. de sesión en la instancia de SQL Server realiza el trabajo de este trabajador DMS.||  
|dms_cpid|**int**|Id. de proceso del subproceso real que se está ejecutando.||  
|error_id|**nvarchar(36)**|Identificador único del error que se produjo durante la ejecución de este trabajo, si existe.|Vea error_id en [sys.dm_pdw_request_steps &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql.md).|  
|source_info|**nvarchar(4000)**|Para un lector, la especificación de las tablas de origen y columnas.||  
|destination_info|**nvarchar(4000)**|Para un sistema de escritura, especificación de las tablas de destino.||  
  
 Para obtener información sobre el número máximo de filas conserva esta vista, consulte [valores máximos de vista de sistema](http://msdn.microsoft.com/en-us/5243f018-2713-45e3-9b61-39b2a57401b9).  
  
## <a name="see-also"></a>Vea también  
 [Vistas de administración dinámica del almacenamiento de datos en paralelo y almacén de datos SQL &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
