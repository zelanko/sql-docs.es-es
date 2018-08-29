---
title: Sys.query_store_plan (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 09/12/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- QUERY_STORE_PLAN_TSQL
- SYS.QUERY_STORE_PLAN
- SYS.QUERY_STORE_PLAN_TSQL
- QUERY_STORE_PLAN
dev_langs:
- TSQL
helpviewer_keywords:
- query_store_plan catalog view
- sys.query_store_plan catalog view
ms.assetid: b4d05439-6360-45db-b1cd-794f4a64935e
caps.latest.revision: 18
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: e139f2e24a686940143c7a152c7e37563d5c8368
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/27/2018
ms.locfileid: "43062708"
---
# <a name="sysquerystoreplan-transact-sql"></a>Sys.query_store_plan (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Contiene información sobre cada plan de ejecución asociado con una consulta.  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**plan_id**|**bigint**|Clave principal.|  
|**query_id**|**bigint**|Clave externa. Se une a [sys.query_store_query &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-query-transact-sql.md).|  
|**plan_group_id**|**bigint**|Id. de grupo del plan. Las consultas de cursor suele requieran varios (rellenar y capturar) planes. Rellenar y son los planes de recuperación que se compilan juntos en el mismo grupo.<br /><br /> 0 significa que el plan no está en un grupo.|  
|**engine_version**|**nvarchar(32)**|Versión del motor usado para compilar el plan en **'principal.secundaria.compilación.revisión'** formato.|  
|**COMPATIBILITY_LEVEL**|**smallint**|Nivel de compatibilidad de base de datos de la base de datos al que hace referencia en la consulta.|  
|**query_plan_hash**|**binary (8)**|Hash MD5 de los planes individuales.|  
|**query_plan**|**nvarchar(max)**|SHOWPLAN XML del plan de consulta.|  
|**is_online_index_plan**|**bit**|Plan utilizó durante la generación de índice en línea.|  
|**is_trivial_plan**|**bit**|Plan es un plan trivial (salida en la etapa 0 del optimizador de consultas).|  
|**is_parallel_plan**|**bit**|Plan es paralelo.|  
|**is_forced_plan**|**bit**|Plan está marcado como fuerza cuando el usuario ejecuta el procedimiento almacenado **sys.sp_query_store_force_plan**. Mecanismo de forzado *no garantiza* que se utilizará para la consulta hace referenciada exactamente a este plan **query_id**. Forzar el plan produce se vuelve a compilar la consulta y normalmente produce exactamente el plan iguales o similar para el plan al que hace referencia **plan_id**. Si no tiene éxito al forzar el plan, **force_failure_count** se incrementa y **last_force_failure_reason** se rellena con el motivo del error.|  
|**is_natively_compiled**|**bit**|Plan incluye procedimientos compilados de forma nativa optimizados en memoria. (0 = FALSE, 1 = TRUE).|  
|**force_failure_count**|**bigint**|Número de veces que forzar este plan ha fallado. Se puede incrementar solo cuando se vuelve a compilar la consulta (*no en cada ejecución*). Se restablece a 0 cada vez **is_plan_forced** se cambia de **FALSE** a **TRUE**.|  
|**last_force_failure_reason**|**int**|Motivo de error de forzar el plan.<br /><br /> 0: ningún error, en caso contrario, número de error del error que provocó el forzado de un error<br /><br /> 8637: ONLINE_INDEX_BUILD<br /><br /> 8683: INVALID_STARJOIN<br /><br /> 8684: TIEMPO_DE_ESPERA<br /><br /> 8689: NO_DB<br /><br /> 8690: HINT_CONFLICT<br /><br /> 8691: SETOPT_CONFLICT<br /><br /> 8694: DQ_NO_FORCING_SUPPORTED<br /><br /> 8698: NO_PLAN<br /><br /> 8712: NO_INDEX<br /><br /> 8713: VIEW_COMPILE_FAILED<br /><br /> \<otro valor >: GENERAL_FAILURE|  
|**last_force_failure_reason_desc**|**nvarchar(128)**|Descripción textual del last_force_failure_reason_desc.<br /><br /> ONLINE_INDEX_BUILD: consulta intenta modificar los datos mientras la tabla de destino tiene un índice que se está generando en línea<br /><br /> INVALID_STARJOIN: plan contiene la especificación de StarJoin no válida<br /><br /> Tiempo_de_espera: Optimizador superado el número de operaciones permitidas durante la búsqueda del plan especificado por el plan forzado<br /><br /> NO_DB: Una base de datos especificada en el plan no existe.<br /><br /> HINT_CONFLICT: No se puede compilar la consulta porque el plan está en conflicto con una sugerencia de consulta<br /><br /> DQ_NO_FORCING_SUPPORTED: No se puede ejecutar la consulta porque el plan está en conflicto con el uso de la consulta distribuida u operaciones de texto completo.<br /><br /> NO_PLAN: Que el procesador de consultas no pudo producir el plan de consulta porque no se puede comprobar el plan forzado a ser válido para la consulta<br /><br /> NO_INDEX: Índice especificado en el plan ya no existe<br /><br /> VIEW_COMPILE_FAILED: No se pudo forzar el plan de consulta debido a un problema en una vista indizada que se hace referencia en el plan<br /><br /> GENERAL_FAILURE: error de forzar general (no se tratan con motivos anteriores)|  
|**count_compiles**|**bigint**|Planee las estadísticas de compilación.|  
|**initial_compile_start_time**|**datetimeoffset**|Planee las estadísticas de compilación.|  
|**last_compile_start_time**|**datetimeoffset**|Planee las estadísticas de compilación.|  
|**last_execution_time**|**datetimeoffset**|Último tiempo de ejecución hace referencia a la última hora de finalización del plan de consulta.|  
|**avg_compile_duration**|**float**|Planee las estadísticas de compilación.|  
|**last_compile_duration**|**bigint**|Planee las estadísticas de compilación.|  
  
## <a name="plan-forcing-limitations"></a>Limitaciones de forzar el plan
El Almacén de consultas dispone de un mecanismo para obligar al optimizador de consultas a usar un determinado plan de ejecución. Pero existen algunas limitaciones que pueden evitar la aplicación de un plan. 

En primer lugar, si el plan contiene las siguientes construcciones:
* Instrucción insert bulk.
* Instrucción insert bulk.
* Referencia a una tabla externa
* Consulta distribuida u operaciones de texto completo
* Uso de consultas globales 
* Cursores
* Especificación de combinación en estrella no válida 

En segundo lugar, si los objetos en los que se basa el plan ya no están disponibles:
* Base de datos (si la base de datos donde se originó el plan ya no existe)
* Índice (ya no existe o está deshabilitado)

Por último, problemas con el propio plan:
* No válido para la consulta
* El optimizador de consultas ha superado el número de operaciones permitidas
* XML de plan formado incorrectamente

## <a name="permissions"></a>Permisos  
 Requiere el **VIEW DATABASE STATE** permiso.  
  
## <a name="see-also"></a>Vea también  
 [sys.database_query_store_options &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md)   
 [sys.query_context_settings &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-context-settings-transact-sql.md)   
 [Sys.query_store_query &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-query-transact-sql.md)   
 [sys.query_store_query_text &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-query-text-transact-sql.md)   
 [Sys.query_store_runtime_stats &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-transact-sql.md)   
 [sys.query_store_wait_stats &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-wait-stats-transact-sql.md)  
 [sys.query_store_runtime_stats_interval &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-interval-transact-sql.md)   
 [Monitoring Performance By Using the Query Store](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)   
 [Vistas de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Procedimientos almacenados de Query Store &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/query-store-stored-procedures-transact-sql.md)  
  
  
