---
title: Sys. dm_pdw_nodes_exec_query_profiles (Transact-SQL) | Microsoft Docs
description: Vista de administración dinámica que se puede usar para supervisar el progreso de las consultas de almacenamiento de datos en tiempo real mientras la consulta está en ejecución.
ms.custom: ''
ms.date: 10/14/2019
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: ''
author: XiaoyuMSFT
ms.author: xiaoyul
monikerRange: =azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: 7237e7f7b49916e09f4a8c5cab0d7d49486cb971
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "73145660"
---
# <a name="sysdm_pdw_nodes_exec_query_profiles-transact-sql"></a>Sys. dm_pdw_nodes_exec_query_profiles (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md.md)]

Supervisa el progreso de las consultas de almacenamiento de datos en tiempo real mientras la consulta está en ejecución.   
  
## <a name="table-returned"></a>Tabla devuelta  
Los contadores devueltos son por operador y por subproceso. Los resultados son dinámicos y no coinciden con los resultados de las opciones `SET STATISTICS XML ON` existentes, como, por ejemplo, las que solo crean los resultados cuando finaliza la consulta.  
  
|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|pdw_node_id|**int**|IDENTIFICADOR numérico único asociado al nodo.|
|session_id|**smallint**|Identifica la sesión en la que se ejecuta esta consulta. Hace referencia a dm_exec_sessions.session_id.|  
|request_id|**int**|Identifica la solicitud de destino. Hace referencia a dm_exec_sessions.request_id.|  
|sql_handle|**varbinary (64)**|Es un token que identifica de forma única el lote o el procedimiento almacenado del que forma parte la consulta. Hace referencia a dm_exec_query_stats.sql_handle.|  
|plan_handle|**varbinary (64)**|Es un token que identifica de forma única un plan de ejecución de consulta para un lote que se ha ejecutado y su plan reside en la caché del plan, o se está ejecutando actualmente. Hace referencia a dm_exec_query_stats. plan_handle.|  
|physical_operator_name|**nvarchar(256)**|Nombre del operador físico.|  
|node_id|**int**|Identifica un nodo de operador en el árbol de consulta.|  
|thread_id|**int**|Distingue los subprocesos (para una consulta en paralelo) que pertenecen al mismo nodo de operador de consulta.|  
|task_address|**varbinary(8**|Identifica la tarea de SQLOS que está utilizando este subproceso. Hace referencia a dm_os_tasks.task_address.|  
|row_count|**BIGINT**|Número de filas que ha devuelto hasta ahora el operador.|  
|rewind_count|**BIGINT**|Número de rebobinados hasta ahora.|  
|rebind_count|**BIGINT**|Número de reenlaces hasta ahora.|  
|end_of_scan_count|**BIGINT**|Número de finales de examen hasta ahora.|  
|estimate_row_count|**BIGINT**|Número de filas estimado. Puede ser útil comparar estimated_row_count con el row_count real.|  
|first_active_time|**BIGINT**|Hora, en milisegundos, a la que se llamó por primera vez al operador.|  
|last_active_time|**BIGINT**|Hora, en milisegundos, a la que se llamó por última vez al operador.|  
|open_time|**BIGINT**|Marca de tiempo al abrir (en milisegundos).|  
|first_row_time|**BIGINT**|Marca de tiempo en la que se abrió la primera fila (en milisegundos).|  
|last_row_time|**BIGINT**|Marca de tiempo en la que se abrió la última fila (en milisegundos).|  
|close_time|**BIGINT**|Marca de tiempo al cerrar (en milisegundos).|  
|elapsed_time_ms|**BIGINT**|Tiempo total transcurrido (en milisegundos) utilizado por las operaciones del nodo de destino hasta ahora.|  
|cpu_time_ms|**BIGINT**|Tiempo total de CPU (en milisegundos) utilizado por las operaciones del nodo de destino hasta ahora.|  
|database_id|**smallint**|Identificador de la base de datos que contiene el objeto en el que se efectúan las lecturas y escrituras.|  
|object_id|**int**|El identificador para el objeto en el que se efectúan las lecturas y escrituras. Hace referencia a sys.objects.object_id.|  
|index_id|**int**|El índice (si existe) en el que se abre el conjunto de filas.|  
|scan_count|**BIGINT**|Número de exámenes de índice o tabla hasta ahora.|  
|logical_read_count|**BIGINT**|Número de lecturas lógicas hasta ahora.|  
|physical_read_count|**BIGINT**|Número de lecturas físicas hasta ahora.|  
|read_ahead_count|**BIGINT**|Número de lecturas anticipadas hasta ahora.|  
|write_page_count|**BIGINT**|Número de escrituras en páginas hasta ahora debido al rebosamiento.|  
|lob_logical_read_count|**BIGINT**|Número de lecturas lógicas LOB hasta ahora.|  
|lob_physical_read_count|**BIGINT**|Número de lecturas físicas LOB hasta ahora.|  
|lob_read_ahead_count|**BIGINT**|Número de lecturas anticipadas LOB hasta ahora.|  
|segment_read_count|**int**|Número de lecturas anticipadas de segmento hasta ahora.|  
|segment_skip_count|**int**|Número de segmentos omitidos hasta ahora.| 
|actual_read_row_count|**BIGINT**|Número de filas leídas por un operador antes de que se aplicara el predicado residual.| 
|estimated_read_row_count|**BIGINT**|**Se aplica a:** A partir [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] de SP1. <br/>Número de filas que un operador debe leer antes de que se aplicara el predicado residual.|  
  
## <a name="remarks"></a>Observaciones  
Se aplican los mismos comentarios en [Sys. dm_exec_query_profiles](https://docs.microsoft.com/sql/relational-databases/system-dynamic-management-views/sys-dm-exec-query-profiles-transact-sql?view=sql-server-ver15) .  

## <a name="permissions"></a>Permisos  
 Requiere el permiso `VIEW SERVER STATE` en el servidor.  

## <a name="see-also"></a>Consulte también  
 [Vistas de administración dinámica de SQL Data Warehouse y almacenamiento de datos paralelos &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
   

 ## <a name="next-steps"></a>Pasos siguientes
 Para obtener más sugerencias sobre desarrollo, consulte la [información general sobre desarrollo de SQL Data Warehouse](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-overview-develop).
