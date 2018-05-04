---
title: sys.dm_exec_text_query_plan (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 10/20/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- dm_exec_text_query_plan
- sys.dm_exec_text_query_plan_TSQL
- dm_exec_text_query_plan_TSQL
- sys.dm_exec_text_query_plan
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_exec_text_query_plan dynamic management function
ms.assetid: 9d5e5f59-6973-4df9-9eb2-9372f354ca57
caps.latest.revision: 10
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: a7490548f90a1612fe6966a52c8edbe606452bca
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="sysdmexectextqueryplan-transact-sql"></a>sys.dm_exec_text_query_plan (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Devuelve el plan de presentación en formato de texto para un lote [!INCLUDE[tsql](../../includes/tsql-md.md)] o para una instrucción concreta dentro del mismo. El plan de consulta especificado por el identificador del plan puede estar almacenado en caché o ejecutándose. Esta función con valores de tabla es similar a [sys.dm_exec_query_plan &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-plan-transact-sql.md), pero tiene las siguientes diferencias:  
  
-   El resultado del plan de consulta se devuelve en formato de texto.  
  
-   El resultado del plan de consulta no está limitado en tamaño.  
  
-   Se pueden especificar instrucciones individuales dentro del lote.  
  
**Se aplica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] (hasta la [versión actual](http://go.microsoft.com/fwlink/p/?LinkId=299658)) [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
sys.dm_exec_text_query_plan   
(   
    plan_handle   
    , { statement_start_offset | 0 | DEFAULT }  
        , { statement_end_offset | -1 | DEFAULT }  
)  
```  
  
## <a name="arguments"></a>Argumentos  
*plan_handle*  
Identifica de forma exclusiva un plan de consulta para un lote que está almacenado en caché o ejecutándose. *plan_handle* es **varbinary(64)**.  
  
El identificador del plan puede obtenerse de los siguientes objetos de administración dinámica:  
  
-  [sys.dm_exec_cached_plans](../../relational-databases/system-dynamic-management-views/sys-dm-exec-cached-plans-transact-sql.md)  
  
-  [sys.dm_exec_query_stats](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md)  
  
-  [sys.dm_exec_requests](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)  
  
*statement_start_offset* | 0 | VALOR PREDETERMINADO  
Indica, en bytes, la posición inicial de la consulta que la fila describe en el texto del lote o del objeto permanente. *statement_start_offset* es **int**. El valor 0 indica el principio del lote. El valor predeterminado es 0.  
  
El desplazamiento inicial de la instrucción puede obtenerse de los siguientes objetos de administración dinámica:  
  
-  [sys.dm_exec_query_stats](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md)  
  
-  [sys.dm_exec_requests](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)  
  
*statement_end_offset* | -1 | VALOR PREDETERMINADO  
Indica, en bytes, la posición final de la consulta que la fila describe en el texto del lote o del objeto permanente.  
  
*statement_start_offset* es **int**.  
  
El valor -1 indica el final del lote. El valor predeterminado es -1.  
  
## <a name="table-returned"></a>Tabla devuelta  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**dbid**|**smallint**|Identificador de la base de datos de contexto que estaba activa al compilarse la instrucción [!INCLUDE[tsql](../../includes/tsql-md.md)] correspondiente a este plan. En el caso de instrucciones SQL ad hoc y preparadas, identificador de la base de datos en que se compilaron las instrucciones.<br /><br /> Esta columna acepta valores NULL.|  
|**objectid**|**int**|Identificador del objeto (por ejemplo, procedimiento almacenado o función definida por el usuario) de este plan de consulta. Para lotes ad hoc y preparados, esta columna es **null**.<br /><br /> Esta columna acepta valores NULL.|  
|**number**|**smallint**|Entero de procedimiento almacenado numerado. Por ejemplo, un grupo de procedimientos de la **pedidos** aplicación puede llamarse **orderproc; 1**, **orderproc; 2**, y así sucesivamente. Para lotes ad hoc y preparados, esta columna es **null**.<br /><br /> Esta columna acepta valores NULL.|  
|**Cifrado**|**bit**|Indica si el procedimiento almacenado correspondiente está cifrado.<br /><br /> 0 = no cifrado<br /><br /> 1 = cifrado<br /><br /> La columna no acepta valores NULL.|  
|**query_plan**|**nvarchar(max)**|Contiene la representación del plan de presentación de tiempo de compilación del plan de ejecución de consulta que se especifica con *plan_handle*. El plan de presentación está en formato de texto. Se genera un plan para cada lote que contiene, por ejemplo, instrucciones [!INCLUDE[tsql](../../includes/tsql-md.md)] "ad hoc", llamadas a procedimientos almacenados y llamadas a funciones definidas por el usuario.<br /><br /> Esta columna acepta valores NULL.|  
  
## <a name="remarks"></a>Comentarios  
 En las siguientes condiciones, no se devuelve ninguna salida de Showplan en el **plan** columna de la tabla devuelta para **sys.dm_exec_text_query_plan**:  
  
-   Si el plan de consulta se especifica mediante el uso de *plan_handle* se ha desalojado de la caché del plan, el **query_plan** columna de la tabla devuelta es null. Por ejemplo, esta condición puede producirse si hay un retraso entre el momento en que se captura el identificador del plan y cuando se utiliza con **sys.dm_exec_text_query_plan**.  
  
-   Algunas instrucciones [!INCLUDE[tsql](../../includes/tsql-md.md)] no se almacenan en la caché, como, por ejemplo, instrucciones de operaciones masivas o instrucciones que contienen literales de cadenas de más de 8 KB. Planes de presentación de dichas instrucciones no se puede recuperar mediante el uso de **sys.dm_exec_text_query_plan** porque no existen en la memoria caché.  
  
-   Si un [!INCLUDE[tsql](../../includes/tsql-md.md)] lote o procedimiento almacenado contiene una llamada a una función definida por el usuario o una llamada a SQL dinámico, por ejemplo, con EXEC (*cadena*), la compila el plan de presentación XML por la función definida por el usuario no se incluye en la tabla devuelto por **sys.dm_exec_text_query_plan** para el lote o procedimiento almacenado. En su lugar, debe realizar una llamada independiente a **sys.dm_exec_text_query_plan** para el *plan_handle* que corresponde a la función definida por el usuario.  
  
Cuando se utiliza una consulta "ad hoc" [simple](../../relational-databases/query-processing-architecture-guide.md#SimpleParam) o [parametrización forzada](../../relational-databases/query-processing-architecture-guide.md#ForcedParam), **query_plan** columna contendrá el texto de la instrucción y no el plan de consulta real. Para devolver el plan de consulta, llame a **sys.dm_exec_text_query_plan** con el identificador del plan de la consulta con parámetros preparada. Puede determinar si la consulta era con parámetros haciendo referencia a la **sql** columna de la [sys.syscacheobjects](../../relational-databases/system-compatibility-views/sys-syscacheobjects-transact-sql.md) vista o la columna de texto de la [sys.dm_exec_sql_text](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sql-text-transact-sql.md)vista de administración dinámica.  
  
## <a name="permissions"></a>Permissions  
 Para ejecutar **sys.dm_exec_text_query_plan**, un usuario debe ser un miembro de la **sysadmin** rol fijo de servidor o tener el permiso VIEW SERVER STATE en el servidor.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-retrieving-the-cached-query-plan-for-a-slow-running-transact-sql-query-or-batch"></a>A. Recuperar el plan de consulta en la memoria caché de una consulta o proceso por lotes de Transact-SQL de ejecución lenta  
 Si una consulta o lote [!INCLUDE[tsql](../../includes/tsql-md.md)] se ejecuta durante mucho tiempo en una conexión determinada con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], recupere el plan de ejecución de dicha consulta o lote para averiguar la causa de la demora. En los siguientes ejemplos se muestra cómo recuperar el plan de presentación de una consulta o lote de ejecución lenta.  
  
> [!NOTE]  
> Para ejecutar este ejemplo, reemplace los valores de *session_id* y *plan_handle* con valores específicos de su servidor.  
  
 Primero, recupere el SPID (Id. de proceso del servidor) para el proceso que está ejecutando la consulta o proceso por lotes mediante el uso del procedimiento almacenado `sp_who`:  
  
```sql  
USE master;  
GO  
EXEC sp_who;  
GO  
```  
  
 El conjunto de resultados que devuelve `sp_who` indica que el SPID es `54`. Puede utilizar el SPID con la vista de administración dinámica `sys.dm_exec_requests` para recuperar el identificador del plan mediante la siguiente consulta:  
  
```sql  
USE master;  
GO  
SELECT * FROM sys.dm_exec_requests  
WHERE session_id = 54;  
GO  
```  
  
 La tabla devuelta por **sys.dm_exec_requests** indica que el identificador del plan de consulta o lote de ejecución lenta es `0x06000100A27E7C1FA821B10600`. En el ejemplo siguiente se devuelve el plan de consulta del identificador del plan especificado y se usan los valores predeterminados 0 y -1 para devolver todas las instrucciones en la consulta o el lote.  
  
```sql  
USE master;  
GO  
SELECT query_plan   
FROM sys.dm_exec_text_query_plan (0x06000100A27E7C1FA821B10600,0,-1);  
GO  
```  
  
### <a name="b-retrieving-every-query-plan-from-the-plan-cache"></a>B. Recuperar todos los planes de consulta de caché del plan  
 Para recuperar una instantánea de todos los planes de consulta que residen en la caché del plan, recupere los identificadores de todos los planes de consulta de la caché; para ello, consulte la vista de administración dinámica `sys.dm_exec_cached_plans`. Los identificadores del plan se almacenan en la columna `plan_handle` de `sys.dm_exec_cached_plans`. Acto seguido, utilice el operador CROSS APPLY para pasar los identificadores del plan a `sys.dm_exec_text_query_plan` como se indica a continuación. El plan de presentación de salida de cada planes almacenados actualmente en la caché del plan se muestra en la `query_plan` columna de la tabla que se devuelve.  
  
```sql  
USE master;  
GO  
SELECT *   
FROM sys.dm_exec_cached_plans AS cp   
CROSS APPLY sys.dm_exec_text_query_plan(cp.plan_handle, DEFAULT, DEFAULT);  
GO  
```  
  
### <a name="c-retrieving-every-query-plan-for-which-the-server-has-gathered-query-statistics-from-the-plan-cache"></a>C. Recuperar todos los planes de consulta para los que el servidor ha reunido estadísticas de consultas procedentes de la memoria caché de plan  
 Para recuperar una instantánea de todos los planes de consulta para los que el servidor ha reunido estadísticas que residen actualmente en la caché del plan, recupere los identificadores de estos planes de la caché; para ello, consulte la vista de administración dinámica `sys.dm_exec_query_stats`. Los identificadores del plan se almacenan en la columna `plan_handle` de `sys.dm_exec_query_stats`. Acto seguido, utilice el operador CROSS APPLY para pasar los identificadores del plan a `sys.dm_exec_text_query_plan` como se indica a continuación. La salida del plan de presentación de cada plan está en la columna `query_plan` de la tabla que se devuelve.  
  
```sql  
USE master;  
GO  
SELECT * FROM sys.dm_exec_query_stats AS qs   
CROSS APPLY sys.dm_exec_text_query_plan(qs.plan_handle, qs.statement_start_offset, qs.statement_end_offset);  
GO  
```  
  
### <a name="d-retrieving-information-about-the-top-five-queries-by-average-cpu-time"></a>D. Al recuperar la información acerca de las cinco mejores consultas por promedio de tiempo de CPU  
 En el ejemplo siguiente se devuelven los planes de consulta y el promedio de tiempo de CPU de las cinco mejores consultas. El **sys.dm_exec_text_query_plan** función especifica los valores predeterminados 0 y -1 para devolver todas las instrucciones del lote en el plan de consulta.  
  
```sql  
SELECT TOP 5 total_worker_time/execution_count AS [Avg CPU Time],  
Plan_handle, query_plan   
FROM sys.dm_exec_query_stats AS qs  
CROSS APPLY sys.dm_exec_text_query_plan(qs.plan_handle, 0, -1)  
ORDER BY total_worker_time/execution_count DESC;  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [sys.dm_exec_query_plan &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-plan-transact-sql.md)  
