---
title: Sys.database_query_store_options (Transact-SQL) | Microsoft Docs
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
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017
ms.openlocfilehash: 9a674efd6c2e7d9db42a0d731e9722fb267830e9
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/06/2018
ms.locfileid: "39552175"
---
# <a name="sysdatabasequerystoreoptions-transact-sql"></a>sys.database_query_store_options (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Devuelve las opciones de consulta Store para esta base de datos.  
  
**Se aplica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (de [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]), [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)].
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**desired_state**|**smallint**|Indica el modo de operación deseada de la consulta Store, establezca explícitamente por el usuario.<br /> 0 = OFF <br /> 1 = READ_ONLY<br /> 2 = READ_WRITE|  
|**desired_state_desc**|**Nvarchar (64)**|Descripción textual del modo de operación deseada de Query Store:<br />OFF<br />READ_ONLY<br />READ_WRITE|  
|**actual_state**|**smallint**|Indica el modo de operación de consulta Store. Además de la lista de los Estados deseados requeridos por el usuario, el estado real puede ser un estado de error.<br /> 0 = OFF <br /> 1 = READ_ONLY<br /> 2 = READ_WRITE<br /> 3 = ERROR|  
|**actual_state_desc**|**Nvarchar (64)**|Descripción textual del modo de operación real de la consulta Store.<br />OFF<br />READ_ONLY<br />READ_WRITE<br />error<br /><br /> Cuando el estado real es diferente del estado deseado, existen situaciones:<br /><br /> Query Store puede funcionar en modo de solo lectura incluso si el usuario especificó la lectura y escritura. Por ejemplo, que podría suceder si la base de datos está en modo de solo lectura o si el tamaño de la consulta Store superó la cuota.<br /><br /> Extremadamente raras, Query Store puede terminar en estado de ERROR debido a errores internos. Si esto ocurre, Query Store podría recuperarse mediante la ejecución de **sp_query_store_consistency_check** procedimiento almacenado dentro de la base de datos afectada.|  
|**readonly_reason**|**int**|Cuando el **desired_state_desc** es READ_WRITE y **actual_state_desc** es READ_ONLY, **readonly_reason** devuelve un poco de mapa para indicar por qué el Store de la consulta está en modo de solo lectura.<br /><br /> 1: la base de datos está en modo de solo lectura<br /><br /> 2 – la base de datos está en modo de usuario único<br /><br /> 4: base de datos está en modo de emergencia<br /><br /> 8: base de datos es la réplica secundaria (se aplica a Azure y Always On [!INCLUDE[ssSDS](../../includes/sssds-md.md)] replicación geográfica). Este valor se puede observar eficazmente solo en **legible** réplicas secundarias<br /><br /> 65536: el Store de la consulta ha alcanzado el límite de tamaño definido por la opción MAX_STORAGE_SIZE_MB.<br /><br /> 131072: el número de instrucciones diferentes en la consulta Store ha alcanzado el límite de memoria interna. Considere la posibilidad de quitar las consultas que no es necesario o actualizar a un mayor nivel de servicio para habilitar la transferencia de Query Store a modo de lectura y escritura.<br />Solo se aplica a [!INCLUDE[ssSDS](../../includes/sssds-md.md)].<br /><br /> 262144: tamaño de los elementos en la memoria a la espera se conserva en el disco ha alcanzado el límite de memoria interna. Query Store estará en modo de solo lectura temporalmente hasta que se conservan los elementos en la memoria en disco. <br />Solo se aplica a [!INCLUDE[ssSDS](../../includes/sssds-md.md)].<br /><br />524288: base de datos ha alcanzado el límite de tamaño de disco. Query Store es parte de la base de datos de usuario, por lo que si hay espacio no están disponible para una base de datos, lo que significa que la consulta Store no puede crecer más.<br />Solo se aplica a [!INCLUDE[ssSDS](../../includes/sssds-md.md)]. <br /> <br /> Para cambiar las operaciones de consulta Store back del modo de lectura y escritura, consulte **Compruebe Query Store está recopilando datos de consulta continuamente** sección de [recomendado con el Store consulta](../../relational-databases/performance/best-practice-with-the-query-store.md).|  
|**current_storage_size_mb**|**bigint**|Tamaño de la consulta Store en disco en megabytes.|  
|**flush_interval_seconds**|**bigint**|Define el período para regular el vaciado de datos de la consulta Store en el disco. Valor predeterminado es 900 (15 minutos).<br /><br /> Cambio mediante el uso de la `ALTER DATABASE <database> SET QUERY_STORE (DATA_FLUSH_INTERVAL_SECONDS  = <interval>)` instrucción.|  
|**interval_length_minutes**|**bigint**|El intervalo de agregación de estadísticas. No se permiten valores arbitrarios. Utilice uno de los siguientes: 1, 5, 10, 15, 30, 60 y 1440 minutos. El valor predeterminado es 60 minutos.|  
|**max_storage_size_mb**|**bigint**|Tamaño de disco máximo para la consulta de Store. Valor predeterminado es 100 MB.<br />Para la edición [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)] Premium, el valor predeterminado es 1 Gb y para la edición [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)] Basic, el valor predeterminado es 10 Mb.<br /><br /> Cambio mediante el uso de la `ALTER DATABASE <database> SET QUERY_STORE (MAX_STORAGE_SIZE_MB = <size>)` instrucción.|  
|**stale_query_threshold_days**|**bigint**|Número de días que las consultas con ninguna configuración de directiva se conservan en la consulta Store. Valor predeterminado es 30. Establézcalo en 0 para deshabilitar la directiva de retención.<br />En la edición básica de [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)] , el valor predeterminado es 7 días.<br /><br /> Cambio mediante el uso de la `ALTER DATABASE <database> SET QUERY_STORE ( CLEANUP_POLICY = ( STALE_QUERY_THRESHOLD_DAYS = <value> ) )` instrucción.|  
|**max_plans_per_query**|**bigint**|Limita el número máximo de planes almacenados. Valor predeterminado es 200. Si se alcanza el valor máximo, Query Store deja de capturar nuevos planes para esa consulta. Configuración en 0 quita la limitación con respecto al número de planes capturados.<br /><br /> Cambio mediante el uso de la `ALTER DATABASE<database> SET QUERY_STORE (MAX_PLANS_PER_QUERY = <n>)` instrucción.|  
|**query_capture_mode**|**smallint**|El modo de captura de consultas activo actualmente:<br /><br /> 1 = ALL - se capturan todas las consultas. Este es el valor de la configuración predeterminada para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] a través de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]).<br /><br /> 2 = AUTO - captura consultas pertinentes en función del consumo de recursos y el recuento de ejecución. Este es el valor de la configuración predeterminada para [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)].<br /><br /> 3 = NONE: dejar de capturar nuevas consultas. El almacén de consultas seguirá recopilando estadísticas de compilación y tiempo de ejecución para las consultas que ya se capturaron. Utilice esta configuración con precaución, ya que podría omitir para capturar consultas importantes.|  
|**query_capture_mode_desc**|**nvarchar(60)**|Descripción textual del modo de captura reales de Query Store:<br /><br /> Todos los (valor predeterminado para [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)])<br /><br /> AUTO (valor predeterminado para [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)])<br /><br /> Ninguno|  
|**size_based_cleanup_mode**|**smallint**|Controla si la limpieza se activará automáticamente cuando la cantidad total de datos se acerque al tamaño máximo:<br /><br /> 1 = OFF: tamaño en función de limpieza no se activará automáticamente.<br /><br /> 2 = AUTO - tamaño en función de limpieza se activará automáticamente cuando el tamaño en disco alcance el 90% de **max_storage_size_mb**. Es el valor de configuración predeterminado.<br /><br />La limpieza según el tamaño quita primero las consultas menos caras y más antiguas. Se detiene en aproximadamente el 80% de max_storage_size_mb.|  
|**size_based_cleanup_mode_desc**|**smallint**|Descripción textual del modo de limpieza basado en tamaño real de Query Store:<br /><br /> OFF <br /><br /> AUTOMÁTICO (predeterminado)|  
|**wait_stats_capture_mode**|**smallint**|Controla si consulta Store realiza la captura de estadísticas de espera: <br /><br /> 0 = OFF <br /><br /> 1 = ON <br /> **Se aplica a**: desde [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].|
|**wait_stats_mode_capture_desc**|**nvarchar(60)**|Descripción textual del modo de captura de estadísticas de espera real: <br /><br /> OFF <br /><br /> ACTIVADO (valor predeterminado)<br /> **Se aplica a**: desde [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].| 
  
## <a name="permissions"></a>Permisos  
 Requiere el **VIEW DATABASE STATE** permiso.  
  
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
 [Procedimientos almacenados de Query Store &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/query-store-stored-procedures-transact-sql.md)  
  
  
