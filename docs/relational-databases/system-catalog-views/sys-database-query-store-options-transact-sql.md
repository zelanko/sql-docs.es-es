---
title: Sys.database_query_store_options (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 10/25/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- DATABASE_QUERY_STORE_OPTIONS_TSQL
- DATABASE_QUERY_STORE_OPTIONS
- SYS.DATABASE_QUERY_STORE_OPTIONS_TSQL
- SYS.DATABASE_QUERY_STORE_OPTIONS
dev_langs:
- TSQL
helpviewer_keywords:
- database_query_store_options catalog view
- sys.database_query_store_options catalog view
ms.assetid: 16b47d55-8019-41ff-ad34-1e0112178067
caps.latest.revision: 24
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: a9ce2b5f63405a0754782e0dddae5584c1b47ee2
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2018
---
# <a name="sysdatabasequerystoreoptions-transact-sql"></a>sys.database_query_store_options (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Devuelve las opciones de almacén de consultas para esta base de datos.  
  
**Se aplica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (de [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]), [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)].
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**desired_state**|**smallint**|Indica el modo de operación del almacén de consultas, establezca explícitamente por el usuario.<br /> 0 = OFF <br /> 1 = READ_ONLY<br /> 2 = READ_WRITE|  
|**desired_state_desc**|**nvarchar(64)**|Descripción textual del modo de operación que desea del almacén de consultas:<br />OFF<br />READ_ONLY<br />READ_WRITE|  
|**actual_state**|**smallint**|Indica el modo de operación del almacén de consultas. Además de la lista de Estados deseados requeridos por el usuario, el estado real puede ser un estado de error.<br /> 0 = OFF <br /> 1 = READ_ONLY<br /> 2 = READ_WRITE<br /> 3 = ERROR|  
|**actual_state_desc**|**nvarchar(64)**|Descripción textual del modo de operación real del almacén de consultas.<br />OFF<br />READ_ONLY<br />READ_WRITE<br />ERROR<br /><br /> Hay ocasiones estado real es diferente del estado deseado:<br /><br /> Almacén de consultas puede funcionar en modo de solo lectura incluso si el usuario especificó lectura / escritura. Por ejemplo, que puede ocurrir si la base de datos está en modo de solo lectura o si el tamaño de almacén de consultas supera la cuota.<br /><br /> Extremadamente raras, el almacén de consultas puede terminar en estado de ERROR debido a errores internos. Si esto ocurre, el almacén de consultas podría recuperarse mediante la ejecución de **sp_query_store_consistency_check** procedimiento almacenado dentro de la base de datos.|  
|**readonly_reason**|**int**|Cuando el **desired_state_desc** es READ_WRITE y **actual_state_desc** es READ_ONLY, **readonly_reason** devuelve un poco de mapa para indicar por qué es el almacén de consultas en modo de solo lectura.<br /><br /> 1 – la base de datos está en modo de solo lectura<br /><br /> 2 – la base de datos está en modo de usuario único<br /><br /> 4: base de datos está en modo de emergencia<br /><br /> 8: base de datos es la réplica secundaria (se aplica a AlwaysOn y Azure [!INCLUDE[ssSDS](../../includes/sssds-md.md)] replicación geográfica). Este valor se puede observar eficazmente solo en **legible** réplicas secundarias<br /><br /> 65536: el almacén de consultas ha alcanzado el límite de tamaño establecido por la opción de MAX_STORAGE_SIZE_MB.<br /><br /> 131072 - el número de instrucciones diferentes en el almacén de consultas ha alcanzado el límite de memoria interna. Considere la posibilidad de quitar las consultas que no es necesario o actualizar a un mayor nivel de servicio para permitir la transferencia de almacén de consultas al modo de lectura y escritura.<br />Solo se aplica a [!INCLUDE[ssSDS](../../includes/sssds-md.md)].<br /><br /> 262144: tamaño de los elementos en memoria que esperan que se deben conservar en el disco ha alcanzado el límite de memoria interna. Almacén de consultas estará en modo de solo lectura temporalmente hasta que se conservan los elementos en la memoria en disco. <br />Solo se aplica a [!INCLUDE[ssSDS](../../includes/sssds-md.md)].<br /><br />524288: la base de datos ha alcanzado el límite de tamaño de disco. Almacén de consultas es parte de la base de datos de usuario, por lo que si hay espacio no están disponible para una base de datos, lo que significa que el almacén de consultas no puede crecer más ya.<br />Solo se aplica a [!INCLUDE[ssSDS](../../includes/sssds-md.md)]. <br /> <br /> Para cambiar las operaciones de almacén de consultas back de modo de lectura y escritura, consulte **Compruebe el almacén de consultas está recopilando datos de consulta continuamente** sección de [procedimiento recomendado con el almacén de consultas](../../relational-databases/performance/best-practice-with-the-query-store.md).|  
|**current_storage_size_mb**|**bigint**|Tamaño del almacén de consultas en el disco en megabytes.|  
|**flush_interval_seconds**|**bigint**|Define el período para regular el vaciado de datos de almacén de consultas en el disco. Valor predeterminado es 900 (15 minutos).<br /><br /> Cambio mediante el uso de la `ALTER DATABASE <database> SET QUERY_STORE (DATA_FLUSH_INTERVAL_SECONDS  = <interval>)` instrucción.|  
|**interval_length_minutes**|**bigint**|El intervalo de agregación de las estadísticas. No se permiten valores arbitrarios. Utilice uno de los siguientes valores: 1, 5, 10, 15, 30, 60 y 1440 minutos. El valor predeterminado es 60 minutos.|  
|**max_storage_size_mb**|**bigint**|Tamaño de disco máximo para el almacén de consultas. Valor predeterminado es 100 MB.<br />Para la edición [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)] Premium, el valor predeterminado es 1 Gb y para la edición [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)] Basic, el valor predeterminado es 10 Mb.<br /><br /> Cambio mediante el uso de la `ALTER DATABASE <database> SET QUERY_STORE (MAX_STORAGE_SIZE_MB = <size>)` instrucción.|  
|**stale_query_threshold_days**|**bigint**|Número de días que las consultas con ninguna configuración de directiva se conservan en el almacén de consultas. Valor predeterminado es 30. Establézcalo en 0 para deshabilitar la directiva de retención.<br />En la edición básica de [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)] , el valor predeterminado es 7 días.<br /><br /> Cambio mediante el uso de la `ALTER DATABASE <database> SET QUERY_STORE ( CLEANUP_POLICY = ( STALE_QUERY_THRESHOLD_DAYS = <value> ) )` instrucción.|  
|**max_plans_per_query**|**bigint**|Limita el número máximo de planes almacenados. Valor predeterminado es 200. Si se alcanza el valor máximo, el almacén de consultas deja de capturar nuevos planes para esa consulta. Valor en 0 elimina la limitación en relación con el número de planes capturados.<br /><br /> Cambio mediante el uso de la `ALTER DATABASE<database> SET QUERY_STORE (MAX_PLANS_PER_QUERY = <n>)` instrucción.|  
|**query_capture_mode**|**smallint**|El modo de captura de consulta activa:<br /><br /> 1 = ALL - se capturan todas las consultas. Este es el valor de configuración predeterminado para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] a través de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]).<br /><br /> 2 = AUTO - captura las consultas pertinentes en función del consumo de recursos y el número de ejecución. Este es el valor de configuración predeterminado para [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)].<br /><br /> 3 = NONE - dejar de capturar nuevas consultas. El almacén de consultas seguirá recopilando estadísticas de compilación y tiempo de ejecución para las consultas que ya se capturaron. Utilice esta configuración con precaución, ya que se pueden perder para capturar consultas importantes.|  
|**query_capture_mode_desc**|**nvarchar(60)**|Descripción textual del modo de captura reales de almacén de consultas:<br /><br /> TODOS (valor predeterminado para [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)])<br /><br /> AUTO (valor predeterminado para [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)])<br /><br /> Ninguno|  
|**size_based_cleanup_mode**|**smallint**|Controla si la limpieza se activará automáticamente cuando la cantidad total de datos se acerque al tamaño máximo:<br /><br /> 1 = OFF: tamaño en función de limpieza no se active automáticamente.<br /><br /> 2 = AUTO - tamaño en función de limpieza se activará automáticamente cuando el tamaño en disco alcanza el 90% de **max_storage_size_mb**. Es el valor de configuración predeterminado.<br /><br />La limpieza según el tamaño quita primero las consultas menos caras y más antiguas. Se detiene en aproximadamente el 80% de max_storage_size_mb.|  
|**size_based_cleanup_mode_desc**|**smallint**|Descripción textual del modo de limpieza basada en el tamaño real del almacén de consultas:<br /><br /> OFF <br /><br /> AUTOMÁTICO (predeterminado)|  
|**wait_stats_capture_mode**|**smallint**|Controla si se realiza la captura de las estadísticas de esperas de almacén de consultas: <br /><br /> 0 = OFF <br /><br /> 1 = ON <br /> **Se aplica a**: desde [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].|
|**wait_stats_mode_capture_desc**|**nvarchar(60)**|Descripción textual del modo de captura de las estadísticas de espera real: <br /><br /> OFF <br /><br /> ON (valor predeterminado)<br /> **Se aplica a**: desde [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
  
## <a name="permissions"></a>Permissions  
 Requiere la **VIEW DATABASE STATE** permiso.  
  
## <a name="see-also"></a>Vea también  
 [sys.query_context_settings &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-context-settings-transact-sql.md)   
 [sys.query_store_plan &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-plan-transact-sql.md)   
 [Sys.query_store_query &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-query-transact-sql.md)   
 [sys.query_store_query_text &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-query-text-transact-sql.md)   
 [Sys.query_store_runtime_stats &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-transact-sql.md)   
 [sys.query_store_wait_stats &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-wait-stats-transact-sql.md)  
 [sys.query_store_runtime_stats_interval &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-interval-transact-sql.md)   
 [Monitoring Performance By Using the Query Store](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)   
 [Vistas de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [sys.fn_stmt_sql_handle_from_sql_stmt &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-stmt-sql-handle-from-sql-stmt-transact-sql.md)   
 [Procedimientos almacenados del almacén de consultas &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/query-store-stored-procedures-transact-sql.md)  
  
  
