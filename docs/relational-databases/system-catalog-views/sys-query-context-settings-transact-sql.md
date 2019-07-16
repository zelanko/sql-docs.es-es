---
title: sys.query_context_settings (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/29/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- QUERY_CONTEXT_SETTINGS_TSQL
- SYS.QUERY_CONTEXT_SETTINGS_TSQL
- SYS.QUERY_CONTEXT_SETTINGS
- QUERY_CONTEXT_SETTINGS
dev_langs:
- TSQL
helpviewer_keywords:
- sys.query_context_settings catalog view
ms.assetid: 3c1887df-6bd8-491e-82fc-d25ad9589faf
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||= azure-sqldw-latest||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 7736c0001c8e22b6cc7c72b2e721e31519d035b7
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68068065"
---
# <a name="sysquerycontextsettings-transact-sql"></a>sys.query_context_settings (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-asdw-xxx-md.md)]

  Contiene información sobre la semántica de valores de contexto asociados con una consulta. Hay una serie de valores de contexto disponibles en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que influyen en la semántica de consulta (definiendo el resultado correcto de la consulta). El mismo texto de consulta compilado en configuraciones diferentes puede producir resultados diferentes (en función de los datos subyacentes).  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**context_settings_id**|**bigint**|Clave principal. Este valor se expone en Showplan XML para las consultas.|  
|**set_options**|**varbinary(8)**|Máscara de bits que refleja el estado de varias opciones SET. Para obtener más información, consulte [sys.dm_exec_plan_attributes &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-plan-attributes-transact-sql.md).|  
|**language_id**|**smallint**|El identificador del idioma. Para obtener más información, consulte [sys.syslanguages &#40;Transact-SQL&#41;](../../relational-databases/system-compatibility-views/sys-syslanguages-transact-sql.md).|  
|**date_format**|**smallint**|El formato de fecha. Para más información, vea [SET DATEFORMAT &#40;Transact-SQL&#41;](../../t-sql/statements/set-dateformat-transact-sql.md).|  
|**date_first**|**tinyint**|El primer valor de fecha. Para más información, vea [SET DATEFIRST &#40;Transact-SQL&#41;](../../t-sql/statements/set-datefirst-transact-sql.md).|  
|**status**|**varbinary(2)**|Campo de máscara de bits que indica el tipo de consulta o contexto en el que se ejecutó la consulta. <br />Valor de la columna puede ser una combinación de varias marcas (expresado en formato hexadecimal):<br /><br /> 0 x 0: consulta normal (sin marcas específicas)<br /><br /> 0 x 1: consulta ejecutada a través de uno de los procedimientos almacenados de API de cursor<br /><br /> 0 x 2: consulta de notificación<br /><br /> 0 x 4: consulta interna<br /><br /> 0 x 8 - consulta parametrizada automática sin la parametrización universal<br /><br /> 0 x 10 - captura de cursor refresh query<br /><br /> 0 x 20 - consulta que se usa en las solicitudes de actualización de cursor<br /><br /> 0 x 40 - conjunto de resultados inicial se devuelve cuando se abre un cursor (Cursor automática capturar)<br /><br /> 0 x 80 - consulta cifrada<br /><br /> 0 x 100 - consulta en el contexto del predicado de seguridad de nivel de fila|  
|**required_cursor_options**|**int**|Opciones de cursor especificadas por el usuario, como el tipo de cursor.|  
|**acceptable_cursor_options**|**int**|Opciones de cursor que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] puede convertir de forma implícita para permitir la ejecución de la instrucción.|  
|**merge_action_type**|**smallint**|El tipo de plan de ejecución de desencadenador utilizado como resultado de una **mezcla** instrucción.<br /><br /> 0 indica un plan sin desencadenadores, un plan de desencadenadores que no se ejecuta como resultado de una **mezcla** instrucción o un plan de desencadenadores que se ejecuta como resultado de una **mezcla** instrucción que solo especifica un **Eliminar** acción.<br /><br /> 1 indica un **insertar** plan de desencadenadores que se ejecuta como resultado de una **mezcla** instrucción.<br /><br /> 2 indica un **actualización** plan de desencadenadores que se ejecuta como resultado de una **mezcla** instrucción.<br /><br /> 3 indica un **eliminar** plan de desencadenadores que se ejecuta como resultado de una **mezcla** instrucción que contiene el correspondiente **insertar** o **actualización** acción.<br /><br /> <br /><br /> Para ejecutar las acciones en cascada de desencadenadores anidados, este valor es la acción de la **mezcla** instrucción que provocó la cascada.|  
|**default_schema_id**|**int**|Id. del esquema predeterminado, que se usa para resolver los nombres que no son nombres completos.|  
|**is_replication_specific**|**bit**|Utilizado para la replicación.|  
|**is_contained**|**varbinary(1)**|1 indica que una base de datos independiente.|  
  
## <a name="permissions"></a>Permisos  
 Requiere el **VIEW DATABASE STATE** permiso.  
  
## <a name="see-also"></a>Vea también  
 [sys.database_query_store_options &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md)   
 [sys.query_store_plan &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-plan-transact-sql.md)   
 [sys.query_store_query &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-query-transact-sql.md)   
 [sys.query_store_query_text &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-query-text-transact-sql.md)   
 [sys.query_store_runtime_stats &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-transact-sql.md)   
 [sys.query_store_wait_stats &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-wait-stats-transact-sql.md)   
 [sys.query_store_runtime_stats_interval &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-interval-transact-sql.md)   
 [Monitoring Performance By Using the Query Store](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)   
 [Vistas de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Query Store Stored Procedures &#40;Transact-SQL&#41; (Procedimientos almacenados del Almacén de consultas &#40;Transact-SQL&#41;)](../../relational-databases/system-stored-procedures/query-store-stored-procedures-transact-sql.md)   
 [sys.fn_stmt_sql_handle_from_sql_stmt &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-stmt-sql-handle-from-sql-stmt-transact-sql.md)  
  
  
