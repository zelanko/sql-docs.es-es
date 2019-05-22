---
title: sys.dm_exec_query_plan_stats (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/22/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: conceptual
f1_keywords:
- sys.dm_exec_query_plan_stats
- sys.dm_exec_query_plan_stats_TSQL
- dm_exec_query_plan_stats_TSQL
- dm_exec_query_plan_stats
helpviewer_keywords:
- sys.dm_exec_query_plan_stats management view
ms.assetid: fdc7659e-df41-488e-b2b5-0d79734dfacb
author: pmasl
ms.author: pelopes
manager: amitban
ms.openlocfilehash: 92e5aaf103c1c8d08b8527bf859415686fd5f4f8
ms.sourcegitcommit: be09f0f3708f2e8eb9f6f44e632162709b4daff6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/21/2019
ms.locfileid: "65993631"
---
# <a name="sysdmexecqueryplanstats-transact-sql"></a>sys.dm_exec_query_plan_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../../includes/tsql-appliesto-ssver15-asdb-xxxx-xxx.md)]

Devuelve el equivalente del último plan de ejecución real conocido para un plan de consulta previamente almacenado en caché.

## <a name="syntax"></a>Sintaxis

```
sys.dm_exec_query_plan_stats(plan_handle)  
``` 

## <a name="arguments"></a>Argumentos 
*plan_handle*  
Es un token que identifica de forma exclusiva un plan de ejecución de consulta para un lote que se ha ejecutado y su plan reside en la caché del plan o se está ejecutando actualmente. *plan_handle* es **varbinary (64)**.   

El *plan_handle* puede obtenerse de los objetos de administración dinámica siguientes:  
  
-   [sys.dm_exec_cached_plans &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-cached-plans-transact-sql.md)  
  
-   [sys.dm_exec_query_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md)  
  
-   [sys.dm_exec_requests &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)  

-   [sys.dm_exec_procedure_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-procedure-stats-transact-sql.md)  

-   [sys.dm_exec_trigger_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-trigger-stats-transact-sql.md)  

## <a name="table-returned"></a>Tabla devuelta

|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|
|**dbid**|**smallint**|Identificador de la base de datos de contexto que estaba activa al compilarse la instrucción [!INCLUDE[tsql](../../includes/tsql-md.md)] correspondiente a este plan. En el caso de instrucciones SQL ad hoc y preparadas, identificador de la base de datos en que se compilaron las instrucciones.<br /><br /> Esta columna acepta valores NULL.|  
|**objectid**|**int**|Identificador del objeto (por ejemplo, procedimiento almacenado o función definida por el usuario) de este plan de consulta. Para lotes ad hoc y preparados, esta columna es **null**.<br /><br /> Esta columna acepta valores NULL.|  
|**number**|**smallint**|Entero de procedimiento almacenado numerado. Por ejemplo, un grupo de procedimientos para la **pedidos** aplicación podría llamarse **orderproc; 1**, **orderproc; 2**, y así sucesivamente. Para lotes ad hoc y preparados, esta columna es **null**.<br /><br /> Esta columna acepta valores NULL.|  
|**encrypted**|**bit**|Indica si el procedimiento almacenado correspondiente está cifrado.<br /><br /> 0 = no cifrado<br /><br /> 1 = cifrado<br /><br /> La columna no acepta valores NULL.|  
|**query_plan**|**xml**|Contiene la representación del plan de presentación del plan de ejecución de consulta real que se especifica con último conocido del runtime *plan_handle*. El plan de presentación está en formato XML. Se genera un plan para cada lote que contiene, por ejemplo, instrucciones [!INCLUDE[tsql](../../includes/tsql-md.md)] "ad hoc", llamadas a procedimientos almacenados y llamadas a funciones definidas por el usuario.<br /><br /> Esta columna acepta valores NULL.| 

## <a name="remarks"></a>Comentarios
Esta función del sistema está disponible a partir de [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] CTP 2.4.

Se trata de una característica opcional que requiere que la [marca de seguimiento](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) 2451 esté habilitada. A partir de [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] 2.5 de CTP y en [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)], para realizar esta acción en el nivel de base de datos, vea la opción LAST_QUERY_PLAN_STATS en [ALTER DATABASE SCOPED CONFIGURATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md).

Esta función del sistema funciona bajo el **ligera** consultar las estadísticas de ejecución de generación de perfiles de infraestructura. Para obtener más información, vea [Infraestructura de generación de perfiles de consultas](../../relational-databases/performance/query-profiling-infrastructure.md).  

En las siguientes condiciones, un plan de presentación de salida **equivalente a un plan de ejecución real** se devuelve en el **query_plan** columna de la tabla devuelta para **sys.dm_exec_query_plan_ estadísticas**:  

-   El plan puede encontrarse en [sys.dm_exec_cached_plans](../../relational-databases/system-dynamic-management-views/sys-dm-exec-cached-plans-transact-sql.md).     
    **AND**    
-   La consulta que se está ejecutando es complejo o consumo de recursos.

En las siguientes condiciones, un **simplificada <sup>1</sup>**  de salida de Showplan se devuelve en el **query_plan** columna de la tabla devuelta para **sys.dm_exec_ query_plan_stats**:  

-   El plan puede encontrarse en [sys.dm_exec_cached_plans](../../relational-databases/system-dynamic-management-views/sys-dm-exec-cached-plans-transact-sql.md).     
    **AND**    
-   La consulta es bastante sencilla, generalmente se clasifican como parte de una carga de trabajo OLTP.

<sup>1</sup> a partir de [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] 2.5 de CTP, se refiere a un plan de presentación que solo contiene el operador de nodo raíz (SELECT). Para [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] CTP 2.4 se refiere al plan almacenado en caché como disponible a través de `sys.dm_exec_cached_plans`.

En las siguientes condiciones, **no se devuelve ningún resultado** desde **sys.dm_exec_query_plan_stats**:

-   El plan de consulta que se especifica mediante el uso de *plan_handle* se ha desalojado de la caché del plan.     
    **OR**    
-   El plan de consulta no era almacenable en caché en primer lugar. Para obtener más información, consulte [Plan de almacenamiento en caché en ejecución y volver a utilizar ](../../relational-databases/query-processing-architecture-guide.md#execution-plan-caching-and-reuse).
  
> [!NOTE] 
> Debido a una limitación en el número de niveles anidados permitidos en el **xml** tipo de datos, **sys.dm_exec_query_plan** no puede devolver los planes de consulta que tengan o superen los 128 niveles de elementos anidados. En versiones anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], esta condición impedía el plan de consulta de devolver y [el error 6335](../../relational-databases/errors-events/database-engine-events-and-errors.md#errors-6000-to-6999). En [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] Service Pack 2 y versiones posteriores, el **query_plan** columna devuelve NULL.  

## <a name="permissions"></a>Permisos  
 Requiere el permiso `VIEW SERVER STATE` en el servidor.  

## <a name="examples"></a>Ejemplos  
  
### <a name="a-looking-at-last-known-actual-query-execution-plan-for-a-specific-cached-plan"></a>A. Busca en la última plan de ejecución de consulta real conocido de un plan en caché específico  
 El ejemplo siguiente se consulta **sys.dm_exec_cached_plans** para encontrar el plan de interés y copiar su `plan_handle` desde la salida.  
  
```sql  
SELECT * FROM sys.dm_exec_cached_plans;  
GO  
```  
  
A continuación, para obtener el plan de ejecución de consulta real conocidos último, use el copiado `plan_handle` con la función del sistema **sys.dm_exec_query_plan_stats**.  
  
```sql  
SELECT * FROM sys.dm_exec_query_plan_stats(< copied plan_handle >);  
GO  
```   

### <a name="b-looking-at-last-known-actual-query-execution-plan-for-all-cached-plans"></a>b. Busca en la última plan de ejecución de consulta real conocido de todos los planes almacenados en caché
  
```sql  
SELECT *   
FROM sys.dm_exec_cached_plans AS cp
CROSS APPLY sys.dm_exec_sql_text(plan_handle) AS st
CROSS APPLY sys.dm_exec_query_plan_stats(plan_handle) AS qps;  
GO  
```   

### <a name="c-looking-at-last-known-actual-query-execution-plan-for-a-specific-cached-plan-and-query-text"></a>C. Busca en la última plan de ejecución de consulta real conocido de un plan almacenado en caché específico y el texto de consulta

```sql  
SELECT *   
FROM sys.dm_exec_cached_plans AS cp
CROSS APPLY sys.dm_exec_sql_text(plan_handle) AS st
CROSS APPLY sys.dm_exec_query_plan_stats(plan_handle) AS qps
WHERE st.text LIKE 'SELECT * FROM Person.Person%';  
GO  
```   

### <a name="d-look-at-cached-events-for-trigger"></a>D. Examine los eventos almacenados en caché para el desencadenador

```sql
SELECT *
FROM sys.dm_exec_cached_plans
CROSS APPLY sys.dm_exec_query_plan_stats(plan_handle)
WHERE objtype ='Trigger';
GO
```

## <a name="see-also"></a>Vea también
  [Marcas de seguimiento](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)  
 [Funciones y vistas de administración dinámica &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Vistas de administración dinámica relacionadas con ejecuciones &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)  

