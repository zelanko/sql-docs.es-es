---
title: Sys.dm_exec_query_profiles (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/16/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- dm_exec_query_profiles_TSQL
- sys.dm_exec_query_profiles_TSQL
- dm_exec_query_profiles
- sys.dm_exec_query_profiles
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_exec_query_profiles dynamic management view
ms.assetid: 54efc6cb-eea8-4f6d-a4d0-aa05eeb54081
caps.latest.revision: 19
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 77e8bd3a2372753eb53a7bd42e7344e0117dc44b
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/27/2018
ms.locfileid: "43067797"
---
# <a name="sysdmexecqueryprofiles-transact-sql"></a>sys.dm_exec_query_profiles (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2014-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2014-asdb-xxxx-xxx-md.md)]

  Supervisa el progreso de la consulta en tiempo real mientras la consulta está en ejecución. Por ejemplo, use esta DMV para determinar qué parte de la consulta se está ejecutando con lentitud. Combine esta DMV con otras DMV del sistema mediante las columnas identificadas en el campo de descripción. O bien, combine esta DMV con otros contadores de rendimiento (como el Monitor de rendimiento, xperf) mediante las columnas de marca de tiempo.  
  
## <a name="table-returned"></a>Tabla devuelta  
 Los contadores devueltos son por operador y por subproceso. Los resultados son dinámicos y no se corresponden con los resultados de las opciones existentes como SET STATISTICS XML ON, que solamente genera resultados cuando se completa la consulta.  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|session_id|**smallint**|Identifica la sesión en la que se ejecuta esta consulta. Hace referencia a dm_exec_sessions.session_id.|  
|request_id|**int**|Identifica la solicitud de destino. Hace referencia a dm_exec_sessions.request_id.|  
|sql_handle|**varbinary (64)**|Identifica la consulta de destino. Hace referencia a dm_exec_query_stats.sql_handle.|  
|plan_handle|**varbinary (64)**|Identifica la consulta de destino (hace referencia a dm_exec_query_stats.plan_handle).|  
|physical_operator_name|**nvarchar(256)**|Nombre del operador físico.|  
|node_id|**int**|Identifica un nodo de operador en el árbol de consulta.|  
|thread_id|**int**|Distingue los subprocesos (para una consulta en paralelo) que pertenecen al mismo nodo de operador de consulta.|  
|task_address|**varbinary (8)**|Identifica la tarea de SQLOS que está utilizando este subproceso. Hace referencia a dm_os_tasks.task_address.|  
|row_count|**bigint**|Número de filas que ha devuelto hasta ahora el operador.|  
|rewind_count|**bigint**|Número de rebobinados hasta ahora.|  
|rebind_count|**bigint**|Número de reenlaces hasta ahora.|  
|end_of_scan_count|**bigint**|Número de finales de examen hasta ahora.|  
|estimate_row_count|**bigint**|Número de filas estimado. Puede ser útil comparar estimated_row_count con el row_count real.|  
|first_active_time|**bigint**|Hora, en milisegundos, a la que se llamó por primera vez al operador.|  
|last_active_time|**bigint**|Hora, en milisegundos, a la que se llamó por última vez al operador.|  
|open_time|**bigint**|Marca de tiempo al abrir (en milisegundos).|  
|first_row_time|**bigint**|Marca de tiempo en la que se abrió la primera fila (en milisegundos).|  
|last_row_time|**bigint**|Marca de tiempo en la que se abrió la última fila (en milisegundos).|  
|close_time|**bigint**|Marca de tiempo al cerrar (en milisegundos).|  
|dividir|**bigint**|Tiempo total transcurrido (en milisegundos) acumulado hasta ahora por las operaciones del nodo de destino.|  
|cpu_time_ms|**bigint**|Tiempo total de CPU (en milisegundos) acumulado hasta ahora por las operaciones del nodo de destino.|  
|database_id|**smallint**|Identificador de la base de datos que contiene el objeto en el que se efectúan las lecturas y escrituras.|  
|object_id|**int**|El identificador para el objeto en el que se efectúan las lecturas y escrituras. Hace referencia a sys.objects.object_id.|  
|index_id|**int**|El índice (si existe) en el que se abre el conjunto de filas.|  
|scan_count|**bigint**|Número de exámenes de índice o tabla hasta ahora.|  
|logical_read_count|**bigint**|Número de lecturas lógicas hasta ahora.|  
|physical_read_count|**bigint**|Número de lecturas físicas hasta ahora.|  
|read_ahead_count|**bigint**|Número de lecturas anticipadas hasta ahora.|  
|write_page_count|**bigint**|Número de escrituras en páginas hasta ahora debido al rebosamiento.|  
|lob_logical_read_count|**bigint**|Número de lecturas lógicas LOB hasta ahora.|  
|lob_physical_read_count|**bigint**|Número de lecturas físicas LOB hasta ahora.|  
|lob_read_ahead_count|**bigint**|Número de lecturas anticipadas LOB hasta ahora.|  
|segment_read_count|**int**|Número de lecturas anticipadas de segmento hasta ahora.|  
|segment_skip_count|**int**|Número de segmentos omitidos hasta ahora.| 
|actual_read_row_count|**bigint**|Número de filas leídas por un operador antes de aplica el predicado residual.| 
|estimated_read_row_count|**bigint**|**Se aplica a:** partir [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] SP1. <br/>Número de filas estimado que leerá un operador antes de aplica el predicado residual.|  
  
## <a name="general-remarks"></a>Notas generales  
 Si el nodo del plan de consultas no tiene E/S, todos los contadores relativos a E/S se establecen en NULL.  
  
 Los contadores relativos a E/S de los que informa esta DMV son más granulares que los que informa SET STATISTICS IO en los dos aspectos siguientes:  
  
-   SET STATISTICS IO agrupa todos los contadores para todas las E/S en una tabla determinada. Con esta DMV obtendrá contadores independientes por cada nodo en el plan de consultas que realice E/S en la tabla.  
  
-   Si se realizaran búsquedas en paralelo, esta DMV informa sobre los contadores para cada uno de los subprocesos paralelos que se ejecutan en la búsqueda.
 
 A partir de [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1, las estadísticas de ejecución de consulta estándar infraestructura de generación de perfiles no existe en paralelo con una estadísticas de ejecución ligero infraestructura de generación de perfiles. La nueva infraestructura generación de perfiles de consulta ejecución estadísticas reduce considerablemente la sobrecarga de rendimiento de recopilación de estadísticas de ejecución de consulta por cada operador, como el número real de filas. Esta característica se puede habilitar mediante global inicio [marca de seguimiento 7412](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md), o se activa automáticamente cuando se usan eventos extendidos query_thread_profile.

>[!NOTE]
> No se admiten CPU y el tiempo transcurrido en la infraestructura de generación de perfiles ligera consulta ejecución estadísticas para reducir el impacto de rendimiento.

 ESTABLECER STATISTICS XML ON y SET STATISTICS PROFILE ON use siempre las estadísticas de ejecución de consulta heredado infraestructura de generación de perfiles.
  
## <a name="permissions"></a>Permisos  

En [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], requiere `VIEW SERVER STATE` permiso.   
En [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)], requiere el `VIEW DATABASE STATE` permiso en la base de datos.   
   
## <a name="examples"></a>Ejemplos  
 Paso 1: Inicio de sesión a una sesión en el que va a ejecutar la consulta que vaya a analizar con sys.dm_exec_query_profiles. Para configurar la consulta para la generación de perfiles use SET STATISTICS PROFILE en. Ejecute la consulta en esta misma sesión.  
  
```  
--Configure query for profiling with sys.dm_exec_query_profiles  
SET STATISTICS PROFILE ON;  
GO  

--Or enable query profiling globally under SQL Server 2016 SP1 or above  
DBCC TRACEON (7412, -1);  
GO 
  
--Next, run your query in this session, or in any other session if query profiling has been enabled globally 
```  
  
 Paso 2: Inicio de sesión a una segunda sesión que es diferente de la sesión en el que se está ejecutando la consulta.  
  
 La siguiente instrucción resume el progreso que ha realizado la consulta que se ejecutaba de forma simultánea en la sesión 54. Para ello, calcula el número total de filas resultantes de todos los subprocesos para cada nodo y lo compara con el número estimado de filas resultantes para ese nodo.  
  
```  
--Run this in a different session than the session in which your query is running. 
--Note that you may need to change session id 54 below with the session id you want to monitor.
SELECT node_id,physical_operator_name, SUM(row_count) row_count, 
  SUM(estimate_row_count) AS estimate_row_count, 
  CAST(SUM(row_count)*100 AS float)/SUM(estimate_row_count)  
FROM sys.dm_exec_query_profiles   
WHERE session_id=54
GROUP BY node_id,physical_operator_name  
ORDER BY node_id;  
```  
  
## <a name="see-also"></a>Vea también  
 [Funciones y vistas de administración dinámica &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Funciones y vistas de administración dinámica relacionadas con ejecuciones &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)  
  
  

