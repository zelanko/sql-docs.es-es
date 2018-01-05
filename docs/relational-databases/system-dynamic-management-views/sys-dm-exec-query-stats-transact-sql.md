---
title: Sys.dm_exec_query_stats (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 01/04/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- dm_exec_query_stats_TSQL
- dm_exec_query_stats
- sys.dm_exec_query_stats
- sys.dm_exec_query_stats_TSQL
dev_langs: TSQL
helpviewer_keywords: sys.dm_exec_query_stats dynamic management view
ms.assetid: eb7b58b8-3508-4114-97c2-d877bcb12964
caps.latest.revision: "64"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: cda9fe3ab2bc54f878e45834bca907976cb7793c
ms.sourcegitcommit: 4aeedbb88c60a4b035a49754eff48128714ad290
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/05/2018
---
# <a name="sysdmexecquerystats-transact-sql"></a>sys.dm_exec_query_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Devuelve estadísticas de rendimiento agregadas para planes de consulta almacenado en caché en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. La vista contiene una fila por cada instrucción de consulta dentro del plan en caché, y la duración de las filas está ligada al propio plan. Cuando se quita un plan de la caché, se eliminan las filas correspondientes de esta vista.  
  
> [!NOTE]
> Una consulta inicial de **sys.dm_exec_query_stats** podría producir resultados imprecisos si hay una carga de trabajo ejecutándose actualmente en el servidor. Pueden determinarse resultados más precisos volviendo a ejecutar la consulta.  
  
> [!NOTE]
> Para llamar a esta desde [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] o [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], use el nombre **sys.dm_pdw_nodes_exec_query_stats**.  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**sql_handle**|**varbinary(64)**  |Es un token que hace referencia al lote o al procedimiento almacenado del que forma parte la consulta.<br /><br /> **sql_handle**, junto con **statement_start_offset** y **statement_end_offset**, puede utilizarse para recuperar el texto SQL de la consulta mediante una llamada a la **sys.dm_exec_sql _TEXT** función de administración dinámica.|  
|**statement_start_offset**|**int**|Indica (en bytes y empezando por 0) la posición inicial de la consulta que la fila describe en el texto del lote o del objeto persistente.|  
|**statement_end_offset**|**int**|Indica (en bytes y empezando por 0) la posición final de la consulta que la fila describe en el texto del lote o del objeto persistente. Para las versiones anteriores [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)], un valor de -1 indica el final del lote. Los comentarios finales ya no se incluyen.|  
|**plan_generation_num**|**bigint**|Número de secuencia que se puede usar para distinguir entre instancias de los planes después de una nueva compilación.|  
|**plan_handle**|**varbinary(64)**|Token que hace referencia al plan compilado del que forma parte la consulta. Este valor puede pasarse a la [sys.dm_exec_query_plan](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-plan-transact-sql.md) función de administración dinámica para obtener el plan de consulta.<br /><br /> Será siempre 0x000 cuando un procedimiento almacenado nativo consulte una tabla optimizada para memoria.|  
|**creation_time**|**datetime**|Hora en que se compiló el plan.|  
|**last_execution_time**|**datetime**|Hora a la que se inició la ejecución del plan por última vez.|  
|**entre execution_count**|**bigint**|Número de veces que se ha ejecutado el plan desde que se compiló por última vez.|  
|**total_worker_time**|**bigint**|Tiempo total de CPU, notificado en microsegundos (pero solo con precisión de milisegundos), consumido por las ejecuciones de este plan desde su compilación.<br /><br /> Para los procedimientos almacenados compilados de forma nativa, **total_worker_time** puede no ser exacto si varias ejecuciones tardan menos de 1 milisegundo.|  
|**last_worker_time**|**bigint**|Tiempo de CPU, notificado en microsegundos (pero solo con precisión de milisegundos), que se consumió la última vez que se ejecutó el plan. <sup>1</sup>|  
|**min_worker_time**|**bigint**|Tiempo de CPU mínimo, notificado en microsegundos (pero solo con precisión de milisegundos), que este plan ha consumido alguna vez durante una sola ejecución. <sup>1</sup>|  
|**max_worker_time**|**bigint**|Tiempo de CPU máximo, notificado en microsegundos (pero solo con precisión de milisegundos), que este plan ha consumido alguna vez durante una sola ejecución. <sup>1</sup>|  
|**número**|**bigint**|Número total de lecturas físicas realizadas por las ejecuciones de este plan desde su compilación.<br /><br /> Será siempre 0 al consultar una tabla optimizada para memoria.|  
|**last_physical_reads**|**bigint**|Número de lecturas físicas realizadas la última vez que se ejecutó el plan.<br /><br /> Será siempre 0 al consultar una tabla optimizada para memoria.|  
|**min_physical_reads**|**bigint**|Número mínimo de lecturas físicas que ha realizado este plan durante una ejecución.<br /><br /> Será siempre 0 al consultar una tabla optimizada para memoria.|  
|**max_physical_reads**|**bigint**|Número máximo de lecturas físicas que ha realizado este plan durante una ejecución.<br /><br /> Será siempre 0 al consultar una tabla optimizada para memoria.|  
|**total_logical_writes**|**bigint**|Número total de escrituras lógicas realizadas por las ejecuciones de este plan desde su compilación.<br /><br /> Será siempre 0 al consultar una tabla optimizada para memoria.|  
|**last_logical_writes**|**bigint**|Número de páginas del grupo de búferes desfasadas la última vez que se ejecutó el plan. Si una página ya está desfasada (modificada) no se cuenta ninguna escritura.<br /><br /> Será siempre 0 al consultar una tabla optimizada para memoria.|  
|**min_logical_writes**|**bigint**|Número mínimo de escrituras lógicas que ha realizado este plan durante una ejecución.<br /><br /> Será siempre 0 al consultar una tabla optimizada para memoria.|  
|**max_logical_writes**|**bigint**|Número máximo de escrituras lógicas que ha realizado este plan durante una ejecución.<br /><br /> Será siempre 0 al consultar una tabla optimizada para memoria.|  
|**total_logical_reads**|**bigint**|Número total de lecturas lógicas realizadas por las ejecuciones de este plan desde su compilación.<br /><br /> Será siempre 0 al consultar una tabla optimizada para memoria.|  
|**last_logical_reads**|**bigint**|Número de lecturas lógicas realizadas la última vez que se ejecutó el plan.<br /><br /> Será siempre 0 al consultar una tabla optimizada para memoria.|  
|**min_logical_reads**|**bigint**|Número mínimo de lecturas lógicas que ha realizado este plan durante una ejecución.<br /><br /> Será siempre 0 al consultar una tabla optimizada para memoria.|  
|**max_logical_reads**|**bigint**|Número máximo de lecturas lógicas que ha realizado este plan durante una ejecución.<br /><br /> Será siempre 0 al consultar una tabla optimizada para memoria.|  
|**total_clr_time**|**bigint**|Tiempo, notificado en microsegundos (pero solo con precisión de milisegundos), consumido en [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] objetos de common language runtime (CLR) por las ejecuciones de este plan desde que se compiló. Los objetos CLR pueden ser procedimientos almacenados, funciones, desencadenadores, tipos y agregados.|  
|**last_clr_time**|**bigint**|Tiempo, notificado en microsegundos (pero solo con precisión de milisegundos), consumido por la ejecución dentro [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] objetos CLR durante la última ejecución de este plan. Los objetos CLR pueden ser procedimientos almacenados, funciones, desencadenadores, tipos y agregados.|  
|**min_clr_time**|**bigint**|Tiempo de CPU mínimo, notificado en microsegundos (pero solo con precisión de milisegundos), que este plan ha consumido alguna vez dentro de objetos CLR de [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] durante una sola ejecución. Los objetos CLR pueden ser procedimientos almacenados, funciones, desencadenadores, tipos y agregados.|  
|**max_clr_time**|**bigint**|Tiempo de CPU máximo, notificado en microsegundos (pero solo con precisión de milisegundos), que este plan ha consumido alguna vez dentro del CLR de [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] durante una sola ejecución. Los objetos CLR pueden ser procedimientos almacenados, funciones, desencadenadores, tipos y agregados.|  
|**total_elapsed_time**|**bigint**|Tiempo total transcurrido, notificado en microsegundos (pero solo con precisión de milisegundos), para las ejecuciones completadas de este plan.|  
|**last_elapsed_time**|**bigint**|Tiempo transcurrido, notificado en microsegundos (pero solo con precisión de milisegundos), para la ejecución completada más recientemente de este plan.|  
|**min_elapsed_time**|**bigint**|Tiempo mínimo transcurrido, notificado en microsegundos (pero solo con precisión de milisegundos), para cualquier ejecución completada de este plan.|  
|**max_elapsed_time**|**bigint**|Tiempo máximo transcurrido, notificado en microsegundos (pero solo con precisión de milisegundos), para cualquier ejecución completada de este plan.|  
|**query_hash**|**Binary (8)**|Valor hash binario que se calcula en la consulta y que se usa para identificar consultas con una lógica similar. Puede usar el hash de consulta para determinar el uso de recursos agregados para las consultas que solo se diferencian en los valores literales.|  
|**query_plan_hash**|**binary (8)**|Valor hash binario que se calcula en el plan de ejecución de consulta y que se usa para identificar planes de ejecución de consulta similares. Puede usar el hash del plan de consulta para buscar el costo acumulativo de las consultas con planes de ejecución similares.<br /><br /> Será siempre 0x000 cuando un procedimiento almacenado nativo consulte una tabla optimizada para memoria.|  
|**total_rows**|**bigint**|Número total de filas devueltas por la consulta. No puede ser null.<br /><br /> Será siempre 0 cuando un procedimiento almacenado nativo consulte una tabla optimizada para memoria.|  
|**last_rows**|**bigint**|Número de filas devueltas por la última ejecución de la consulta. No puede ser null.<br /><br /> Será siempre 0 cuando un procedimiento almacenado nativo consulte una tabla optimizada para memoria.|  
|**min_rows**|**bigint**|Número mínimo de filas alguna vez devueltas por la consulta durante una ejecución. No puede ser null.<br /><br /> Será siempre 0 cuando un procedimiento almacenado nativo consulte una tabla optimizada para memoria.|  
|**max_rows**|**bigint**|Número máximo de filas alguna vez devueltas por la consulta durante una ejecución. No puede ser null.<br /><br /> Será siempre 0 cuando un procedimiento almacenado nativo consulte una tabla optimizada para memoria.|  
|**statement_sql_handle**|**varbinary(64)**|**Se aplica a**: desde [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Rellena con valores distintos de NULL solo si el almacén de consultas está activado y recopilar las estadísticas para esa consulta determinada.|  
|**statement_context_id**|**bigint**|**Se aplica a**: desde [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Rellena con valores distintos de NULL solo si el almacén de consultas está activado y recopilar las estadísticas para esa consulta determinada.|  
|**total_dop**|**bigint**|La suma total de grado de paralelismo este plan utiliza desde que se compiló. Siempre es 0 para consultar una tabla con optimización para memoria.<br /><br /> **Se aplica a**: desde [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].|  
|**last_dop**|**bigint**|El grado de paralelismo de la última ejecución de este plan. Siempre es 0 para consultar una tabla con optimización para memoria.<br /><br /> **Se aplica a**: desde [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].|  
|**min_dop**|**bigint**|El mínimo grado de paralelismo este plan utilizado alguna vez durante una ejecución. Siempre es 0 para consultar una tabla con optimización para memoria.<br /><br /> **Se aplica a**: desde [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].|  
|**MAX_DOP**|**bigint**|El grado máximo de paralelismo este plan utilizado alguna vez durante una ejecución. Siempre es 0 para consultar una tabla con optimización para memoria.<br /><br /> **Se aplica a**: desde [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].|  
|**total_grant_kb**|**bigint**|La cantidad total de memoria reservada conceder a este plan recibido desde que se compiló en KB. Siempre es 0 para consultar una tabla con optimización para memoria.<br /><br /> **Se aplica a**: desde [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].|  
|**last_grant_kb**|**bigint**|La cantidad de memoria reservada conceder en KB cuando la última ejecución de este plan. Siempre es 0 para consultar una tabla con optimización para memoria.<br /><br /> **Se aplica a**: desde [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].|  
|**min_grant_kb**|**bigint**|La cantidad mínima de memoria reservada conceder en KB este plan recibido alguna vez durante una ejecución. Siempre es 0 para consultar una tabla con optimización para memoria.<br /><br /> **Se aplica a**: desde [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].|  
|**max_grant_kb**|**bigint**|La cantidad máxima de memoria reservada conceder en KB este plan recibido alguna vez durante una ejecución. Siempre es 0 para consultar una tabla con optimización para memoria.<br /><br /> **Se aplica a**: desde [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].|  
|**total_used_grant_kb**|**bigint**|La cantidad total de memoria reservada conceder a este plan utilizado desde que se compiló en KB. Siempre es 0 para consultar una tabla con optimización para memoria.<br /><br /> **Se aplica a**: desde [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].|  
|**last_used_grant_kb**|**bigint**|La cantidad de concesión de memoria usada en KB cuando la última ejecución de este plan. Siempre es 0 para consultar una tabla con optimización para memoria.<br /><br /> **Se aplica a**: desde [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].|  
|**min_used_grant_kb**|**bigint**|La cantidad mínima de memoria utilizada conceder en KB este plan utilizado alguna vez durante una ejecución. Siempre es 0 para consultar una tabla con optimización para memoria.<br /><br /> **Se aplica a**: desde [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].|  
|**max_used_grant_kb**|**bigint**|La cantidad máxima de memoria utilizada conceder en KB este plan utilizado alguna vez durante una ejecución. Siempre es 0 para consultar una tabla con optimización para memoria.<br /><br /> **Se aplica a**: desde [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].|  
|**total_ideal_grant_kb**|**bigint**|La cantidad total de concesión de memoria ideal en KB este plan estimado desde que se compiló. Siempre es 0 para consultar una tabla con optimización para memoria.<br /><br /> **Se aplica a**: desde [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].|  
|**last_ideal_grant_kb**|**bigint**|La cantidad de memoria ideal conceder en KB cuando la última ejecución de este plan. Siempre es 0 para consultar una tabla con optimización para memoria.<br /><br /> **Se aplica a**: desde [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].|  
|**min_ideal_grant_kb**|**bigint**|La cantidad mínima de memoria ideal conceder en KB este plan estimado alguna vez durante una ejecución. Siempre es 0 para consultar una tabla con optimización para memoria.<br /><br /> **Se aplica a**: desde [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].|  
|**max_ideal_grant_kb**|**bigint**|La cantidad máxima de memoria ideal conceder en KB este plan estimado alguna vez durante una ejecución. Siempre es 0 para consultar una tabla con optimización para memoria.<br /><br /> **Se aplica a**: desde [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].|  
|**total_reserved_threads**|**bigint**|La suma total de paralelo reservada de subprocesos de este plan utilizado alguna vez desde que se compiló. Siempre es 0 para consultar una tabla con optimización para memoria.<br /><br /> **Se aplica a**: desde [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].|  
|**last_reserved_threads**|**bigint**|El número de subprocesos paralelos reservados cuando la última ejecución de este plan. Siempre es 0 para consultar una tabla con optimización para memoria.<br /><br /> **Se aplica a**: desde [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].|  
|**min_reserved_threads**|**bigint**|El número mínimo de paralelo reservado este plan utilizado alguna vez durante una ejecución de subprocesos.  Siempre es 0 para consultar una tabla con optimización para memoria.<br /><br /> **Se aplica a**: desde [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].|  
|**max_reserved_threads**|**bigint**|El número máximo de paralelo reservado este plan utilizado alguna vez durante una ejecución de subprocesos. Siempre es 0 para consultar una tabla con optimización para memoria.<br /><br /> **Se aplica a**: desde [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].|  
|**total_used_threads**|**bigint**|La suma total de utiliza subprocesos paralelos este plan utilizado alguna vez desde que se compiló. Siempre es 0 para consultar una tabla con optimización para memoria.<br /><br /> **Se aplica a**: desde [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].|  
|**last_used_threads**|**bigint**|El número de subprocesos paralelos utilizados cuando la última ejecución de este plan. Siempre es 0 para consultar una tabla con optimización para memoria.<br /><br /> **Se aplica a**: desde [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].|  
|**min_used_threads**|**bigint**|El número mínimo de subprocesos paralelos utilizados este plan utilizado alguna vez durante una ejecución. Siempre es 0 para consultar una tabla con optimización para memoria.<br /><br /> **Se aplica a**: desde [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].|  
|**max_used_threads**|**bigint**|El número máximo de subprocesos paralelos utilizados este plan utilizado alguna vez durante una ejecución. Siempre es 0 para consultar una tabla con optimización para memoria.<br /><br /> **Se aplica a**: desde [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].|  
|**pdw_node_id**|**int**|El identificador para el nodo que se encuentra en esta distribución.<br /><br /> **Se aplica a**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)],[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]| 
|**total_columnstore_segment_reads**|**bigint**|La suma total de segmentos de almacén de columnas leídas por la consulta. No puede ser null.<br /><br /> **Se aplica a**: a partir de [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] CU3|    
|**last_columnstore_segment_reads**|**bigint**|El número de segmentos de almacén de columnas leídas por la última ejecución de la consulta. No puede ser null.<br /><br /> **Se aplica a**: a partir de [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] CU3|    
|**min_columnstore_segment_reads**|**bigint**|El número mínimo de segmentos de almacén de columnas alguna vez leídas por la consulta durante una ejecución. No puede ser null.<br /><br /> **Se aplica a**: a partir de [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] CU3|    
|**max_columnstore_segment_reads**|**bigint**|El número máximo de segmentos de almacén de columnas alguna vez leídas por la consulta durante una ejecución. No puede ser null.<br /><br /> **Se aplica a**: a partir de [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] CU3|    
|**total_columnstore_segment_skips**|**bigint**|La suma total de segmentos de almacén de columnas omitidos por la consulta. No puede ser null.<br /><br /> **Se aplica a**: a partir de [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] CU3|    
|**last_columnstore_segment_skips**|**bigint**|El número de segmentos de almacén de columnas que se omiten en la última ejecución de la consulta. No puede ser null.<br /><br /> **Se aplica a**: a partir de [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] CU3|    
|**min_columnstore_segment_skips**|**bigint**|El número mínimo de segmentos de almacén de columnas que nunca se omiten en la consulta durante una ejecución. No puede ser null.<br /><br /> **Se aplica a**: a partir de [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] CU3|    
|**max_columnstore_segment_skips**|**bigint**|El número máximo de segmentos de almacén de columnas que nunca se omiten en la consulta durante una ejecución. No puede ser null.<br /><br /> **Se aplica a**: a partir de [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] CU3|
  
> [!NOTE]
> <sup>1</sup> para los procedimientos almacenados compilados de forma nativa cuando se habilita la recopilación de estadísticas, el tiempo de trabajo se recopila en milisegundos. Si la consulta se ejecuta en menos de un milisegundo, el valor será 0.  
  
## <a name="permissions"></a>Permissions  
En [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], requiere `VIEW SERVER STATE` permiso.   
En [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] niveles de Premium, requieren la `VIEW DATABASE STATE` permiso en la base de datos. En [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] niveles estándar y básico, requiere la **administrador del servidor** o un **Administrador de Azure Active Directory** cuenta.
  
## <a name="remarks"></a>Comentarios  
 Cuando se completa una consulta, se actualizan las estadísticas en la vista.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-finding-the-top-n-queries"></a>A. Buscar las consultas TOP N  
 En el siguiente ejemplo se devuelve información acerca de las cinco primeras consultas clasificadas por el promedio de tiempo de CPU. Este ejemplo agrega las consultas según su hash de consulta para que las consultas lógicamente equivalentes se agrupen según su consumo acumulado de los recursos.  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT TOP 5 query_stats.query_hash AS "Query Hash",   
    SUM(query_stats.total_worker_time) / SUM(query_stats.execution_count) AS "Avg CPU Time",  
    MIN(query_stats.statement_text) AS "Statement Text"  
FROM   
    (SELECT QS.*,   
    SUBSTRING(ST.text, (QS.statement_start_offset/2) + 1,  
    ((CASE statement_end_offset   
        WHEN -1 THEN DATALENGTH(ST.text)  
        ELSE QS.statement_end_offset END   
            - QS.statement_start_offset)/2) + 1) AS statement_text  
     FROM sys.dm_exec_query_stats AS QS  
     CROSS APPLY sys.dm_exec_sql_text(QS.sql_handle) as ST) as query_stats  
GROUP BY query_stats.query_hash  
ORDER BY 2 DESC;  
```  
  
### <a name="b-returning-row-count-aggregates-for-a-query"></a>B. Devolver agregados de recuentos de filas para una consulta  
 En el ejemplo siguiente se devuelve información de agregado de recuento de filas (filas totales, filas mínimas, filas máximas y últimas filas) para las consultas.  
  
```sql  
SELECT qs.execution_count,  
    SUBSTRING(qt.text,qs.statement_start_offset/2 +1,   
                 (CASE WHEN qs.statement_end_offset = -1   
                       THEN LEN(CONVERT(nvarchar(max), qt.text)) * 2   
                       ELSE qs.statement_end_offset end -  
                            qs.statement_start_offset  
                 )/2  
             ) AS query_text,   
     qt.dbid, dbname= DB_NAME (qt.dbid), qt.objectid,   
     qs.total_rows, qs.last_rows, qs.min_rows, qs.max_rows  
FROM sys.dm_exec_query_stats AS qs   
CROSS APPLY sys.dm_exec_sql_text(qs.sql_handle) AS qt   
WHERE qt.text like '%SELECT%'   
ORDER BY qs.execution_count DESC;  
```  
  
## <a name="see-also"></a>Vea también  
 
 [Funciones y vistas de administración dinámica &#40; relacionada con la ejecución Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)   
 [Sys.dm_exec_sql_text &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sql-text-transact-sql.md)   
 [Sys.dm_exec_query_plan &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-plan-transact-sql.md)  
  
  


