---
title: DBCC FREEPROCCACHE (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 10/13/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- FREEPROCCACHE_TSQL
- FREEPROCCACHE
- DBCC_FREEPROCCACHE_TSQL
- DBCC FREEPROCCACHE
dev_langs:
- TSQL
helpviewer_keywords:
- freeing procedure cache
- removing procedure cache elements
- deleting procedure cache elements
- DBCC FREEPROCCACHE statement
- procedure cache [SQL Server]
- clearing procedure cache
ms.assetid: 0e09d210-6f23-4129-aedb-3d56b2980683
caps.latest.revision: 61
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 54e4c8309c290255cb2885fab04bb394bc453046
ms.openlocfilehash: 58eed9c590594f8c2cff402418aa2ebebd0c65db
ms.contentlocale: es-es
ms.lasthandoff: 10/16/2017

---
# <a name="dbcc-freeproccache-transact-sql"></a>DBCC FREEPROCCACHE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw_md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

Quita todos los elementos de la memoria caché del plan, quita un plan concreto de la misma especificando un identificador de plan o un identificador SQL, o quita todas las entradas de caché asociadas a un grupo de recursos de servidor especificado.

>[!NOTE]
>DBCC FREEPROCCACHE no borra las estadísticas de ejecución para los procedimientos almacenados compilados de forma nativa. La memoria caché de procedimientos no contiene información sobre los procedimientos almacenados compilados de forma nativa. Las estadísticas de ejecución recopiladas de ejecuciones de procedimientos aparecerán en las DMV de estadísticas de ejecución: [sys.dm_exec_procedure_stats & #40; Transact-SQL & #41; ](../../relational-databases/system-dynamic-management-views/sys-dm-exec-procedure-stats-transact-sql.md) y [sys.dm_exec_query_plan & #40; Transact-SQL & #41; ](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-plan-transact-sql.md).  
  
![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxis  
Sintaxis para SQL Server:

```sql
DBCC FREEPROCCACHE [ ( { plan_handle | sql_handle | pool_name } ) ] [ WITH NO_INFOMSGS ]  
```  

Sintaxis de almacenamiento de datos SQL Azure y almacenamiento de datos en paralelo:
  
```sql
DBCC FREEPROCCACHE [ ( COMPUTE | ALL ) ] 
     [ WITH NO_INFOMSGS ]   
[;]  
```  
  
## <a name="arguments"></a>Argumentos  
 ({ *plan_handle* | *sql_handle* | *pool_name* })  
*plan_handle* identifica de forma única un plan de consulta de un lote que se ha ejecutado y cuyo plan reside en la caché del plan. *plan_handle* es **varbinary(64)** y puede obtenerse de los siguientes objetos de administración dinámica:  
 -   [Sys.dm_exec_cached_plans](../../relational-databases/system-dynamic-management-views/sys-dm-exec-cached-plans-transact-sql.md)  
 -   [Sys.dm_exec_requests](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)  
 -   [Sys.dm_exec_query_memory_grants](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-memory-grants-transact-sql.md)  
 -   [Sys.dm_exec_query_stats](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md)  

*sql_handle* es el identificador SQL del lote se va a borrar. *sql_handle* es **varbinary(64)** y puede obtenerse de los siguientes objetos de administración dinámica:  
 -   [Sys.dm_exec_query_stats](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md)  
 -   [Sys.dm_exec_requests](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)  
 -   [Sys.dm_exec_cursors](../../relational-databases/system-dynamic-management-views/sys-dm-exec-cursors-transact-sql.md)  
 -   [Sys.dm_exec_xml_handles](../../relational-databases/system-dynamic-management-views/sys-dm-exec-xml-handles-transact-sql.md)  
 -   [Sys.dm_exec_query_memory_grants](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-memory-grants-transact-sql.md)  

*pool_name* es el nombre de un grupo de recursos regulador de recursos. *pool_name* es **sysname** y puede obtenerse consultando la [sys.dm_resource_governor_resource_pools](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-resource-pools-transact-sql.md) vista de administración dinámica.  
 Para asociar un grupo de cargas de trabajo del regulador de recursos a un grupo de recursos, consultar la [sys.dm_resource_governor_workload_groups](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-workload-groups-transact-sql.md) vista de administración dinámica. Para obtener información acerca del grupo de cargas de trabajo para una sesión, consulte el [sys.dm_exec_sessions](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sessions-transact-sql.md) vista de administración dinámica.  

  
 WITH NO_INFOMSGS  
 Suprime todos los mensajes de información.  
  
 COMPUTE  
 Purgar la caché del plan de consulta de cada nodo de ejecución. Es el valor predeterminado.  
  
 ALL  
 Purgar la caché del plan de consulta de cada nodo de ejecución y desde el nodo de Control.  

> [!NOTE]
> A partir de [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], `ALTER DATABASE SCOPED CONFIGURATION CLEAR PROCEDURE_CACHE` para borrar la caché de procedimientos (plan) para la base de datos en el ámbito.

## <a name="remarks"></a>Comentarios  
Use DBCC FREEPROCCACHE con precaución para borrar la caché del plan. Borrar el procedimiento (plan) caché hace que todos los planes que se expulsen y consulta entrante ejecuciones compilarán un nuevo plan, en lugar de volver a usar cualquier plan previamente almacenado en caché. 

Esto puede ocasionar una disminución repentina y temporal en el rendimiento de las consultas como el número de incrementos nuevas compilaciones. Para cada almacén de caché borrado de la caché del plan, el registro de errores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] contendrá el siguiente mensaje informativo: "[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ha detectado %d instancias de vaciado del almacén de caché '%s' (parte de la caché del plan) debidas a operaciones 'DBCC FREEPROCCACHE' o 'DBCC FREESYSTEMCACHE'". Este mensaje se registra cada cinco minutos siempre que se vacíe la memoria caché dentro de ese intervalo de tiempo.

Las siguientes operaciones de reconfiguración también borran la caché de procedimientos:
-   access check cache bucket count  
-   access check cache quota  
-   clr enabled  
-   cost threshold for parallelism  
-   cross db ownership chaining  
-   index create memory  
-   max degree of parallelism  
-   memoria de servidor máxima  
-   max text repl size  
-   max worker threads  
-   memoria mínima por consulta  
-   memoria de servidor mínima  
-   query governor cost limit  
-   query wait  
-   remote query timeout  
-   user options  
  
## <a name="result-sets"></a>Conjuntos de resultados  
Se devuelve cuando no se especifica la cláusula WITH NO_INFOMSGS, DBCC FREEPROCCACHE: "ejecución de DBCC completada. Si DBCC imprime algún mensaje de error, póngase en contacto con su administrador del sistema."
  
## <a name="permissions"></a>Permissions  
Se aplica a: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)],[!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 
- Requiere el permiso ALTER SERVER STATE en el servidor.  

Se aplica a:[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]
- Requiere la pertenencia al rol fijo de servidor DB_OWNER.  

## <a name="general-remarks-for-includesssdwincludessssdw-mdmd-and-includesspdwincludessspdw-mdmd"></a>Notas generales para [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] y[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
Se pueden ejecutar simultáneamente varios comandos DBCC FREEPROCCACHE.
En [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] o [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], borrar la caché del plan puede ocasionar una disminución temporal en el rendimiento de las consultas como las consultas entrantes compilan un nuevo plan, en lugar de volver a usar cualquier previamente plan almacenado en caché. 

Hace que DBCC FREEPROCCACHE (proceso) solo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a compilar las consultas cuando se ejecutan en los nodos de proceso. Esto no provoca [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] o [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] para volver a compilar el plan de consulta paralelo se genera en el nodo de Control.
DBCC FREEPROCCACHE se puede cancelar durante la ejecución.
  
## <a name="limitations-and-restrictions-for-includesssdwincludessssdw-mdmd-and-includesspdwincludessspdw-mdmd"></a>Limitaciones y restricciones para [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] y[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
No se puede ejecutar DBCC FREEPROCCACHE dentro de una transacción.
DBCC FREEPROCCAHCE no se admite en una instrucción de explicación.
  
## <a name="metadata-for-includesssdwincludessssdw-mdmd-and-includesspdwincludessspdw-mdmd"></a>Metadatos de [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] y[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
Se agrega una fila nueva a la vista del sistema sys.pdw_exec_requests cuando se ejecuta DBCC FREEPROCCACHE.

## <a name="examples-includessnoversionincludesssnoversion-mdmd"></a>Ejemplos:[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
### <a name="a-clearing-a-query-plan-from-the-plan-cache"></a>A. Borrar un plan de consulta de la memoria caché del plan  
En el ejemplo siguiente se especifica el identificador de plan de consulta para borrar el plan de consulta de la caché del plan. Para asegurarse de que la consulta del ejemplo está en la caché del plan, la consulta se ejecuta primero. El `sys.dm_exec_cached_plans` y `sys.dm_exec_sql_text` se consultan las vistas de administración dinámica para devolver el identificador del plan de la consulta. 

A continuación, el valor del identificador de plan del conjunto de resultados se inserta en la instrucción `DBCC FREEPROCACHE` para borrar únicamente dicho plan de la memoria caché del plan.
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT * FROM Person.Address;  
GO  
SELECT plan_handle, st.text  
FROM sys.dm_exec_cached_plans   
CROSS APPLY sys.dm_exec_sql_text(plan_handle) AS st  
WHERE text LIKE N'SELECT * FROM Person.Address%';  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]

```
plan_handle                                         text  
--------------------------------------------------  -----------------------------  
0x060006001ECA270EC0215D05000000000000000000000000  SELECT * FROM Person.Address;  
  
(1 row(s) affected)
 ```
 
```sql  
-- Remove the specific plan from the cache.  
DBCC FREEPROCCACHE (0x060006001ECA270EC0215D05000000000000000000000000);  
GO  
```  
  
### <a name="b-clearing-all-plans-from-the-plan-cache"></a>B. Borrar todos los planes de la memoria caché del plan  
En el ejemplo siguiente se borran todos los elementos de la memoria caché del plan. WITH `NO_INFOMSGS` cláusula se especifica para evitar que aparezca el mensaje de información.
  
```sql  
DBCC FREEPROCCACHE WITH NO_INFOMSGS;  
```  
  
### <a name="c-clearing-all-cache-entries-associated-with-a-resource-pool"></a>C. Borrar todas las entradas de caché asociadas a un grupo de recursos  
En el ejemplo siguiente se borran todas las entradas de caché asociadas a un grupo de recursos de servidor especificado. El `sys.dm_resource_governor_resource_pools` primero se consulta la vista para obtener el valor de *pool_name*.
  
```sql  
SELECT * FROM sys.dm_resource_governor_resource_pools;  
GO  
DBCC FREEPROCCACHE ('default');  
GO  
```  
  
## <a name="examples-includesssdwincludessssdw-mdmd-and-includesspdwincludessspdw-mdmd"></a>Ejemplos: [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] y[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="d-dbcc-freeproccache-basic-syntax-examples"></a>D. Ejemplos de sintaxis básica de DBCC FREEPROCCACHE  
En el ejemplo siguiente se quita todas las cachés de plan de consulta existente de los nodos de proceso. Aunque el contexto se establece en UserDbSales, las cachés de plan de consulta de nodo de proceso para todas las bases de datos se quitará. La cláusula WITH NO_INFOMSGS impide que los mensajes informativos que aparecen en los resultados.  
  
```sql
USE UserDbSales;  
DBCC FREEPROCCACHE (COMPUTE) WITH NO_INFOMSGS;
```  
  
 En el ejemplo siguiente tiene los mismos resultados que el ejemplo anterior, salvo que los mensajes informativos se mostrarán en los resultados.  
  
```sql
USE UserDbSales;  
DBCC FREEPROCCACHE (COMPUTE);  
```  
  
Cuando se solicitan mensajes informativos y la ejecución finaliza correctamente, los resultados de la consulta tendrá una línea por nodo de proceso.
  
### <a name="e-granting-permission-to-run-dbcc-freeproccache"></a>E. Conceder permiso para ejecutar DBCC FREEPROCCACHE  
En el ejemplo siguiente se proporciona el inicio de sesión permiso de David para ejecutar DBCC FREEPROCCACHE.  
  
```sql
GRANT ALTER SERVER STATE TO David; 
GO
```  
  
## <a name="see-also"></a>Vea también  
[DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)  
[Regulador de recursos](../../relational-databases/resource-governor/resource-governor.md)  
[MODIFICAR la configuración en el ámbito de base de datos & #40; Transact-SQL & #41;](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md)
  
  

