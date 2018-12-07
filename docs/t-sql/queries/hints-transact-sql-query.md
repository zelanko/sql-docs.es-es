---
title: Sugerencias de consulta (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 10/22/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- Query_Hint_TSQL
- Query_TSQL
- Query
- Query Hint
- MAX_GRANT_PERCENT
- MAX_GRANT_PERCENT_TSQL
- MIN_GRANT_PERCENT
- MIN_GRANT_PERCENT_TSQL
- EXTERNALPUSHDOWN
- EXTERNALPUSHDOWN_TSQL
- NOLOCK_TSQL
- MAXDOP_TSQL
- USE_HINT_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- REPORT PLAN query hint
- FORCE ORDER query hint
- HASH JOIN query hint
- query hints [SQL Server]
- OPTIMIZE FOR query hint
- FORCESCAN query hint
- RECOMPILE query hint
- MAXRECURSION query hint
- MERGE JOIN query hint
- HASH GROUP query hint
- KEEP PLAN query hint
- UNION query hint
- FORCESEEK query hint
- ORDER GROUP query hint
- LOOP JOIN query hint
- KEEPFIXED PLAN query hint
- FAST query hint
- MAXDOP query hint
- PARAMETERIZATION query hint
- hints [SQL Server], query
- JOIN query hint
- USE PLAN query hint
- EXPAND VIEWS query hint
- MAX_GRANT_PERCENT query hint
- MIN_GRANT_PERCENT query hint
- EXTERNALPUSHDOWN query hint
- USE HINT query hint
- QUERY_PLAN_PROFILE query hint
ms.assetid: 66fb1520-dcdf-4aab-9ff1-7de8f79e5b2d
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 42247b11f00524ba08dd74f41f11da35fdcb2026
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/28/2018
ms.locfileid: "52530355"
---
# <a name="hints-transact-sql---query"></a>Sugerencias (Transact-SQL): consulta
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Sugerencias de consulta especifica que en toda la consulta se deben utilizar las sugerencias especificadas. Afectan a todos los operadores de la instrucción. Si hay un argumento UNION implicado en la consulta principal, solo la última consulta que implique una operación UNION puede contener la cláusula OPTION. Las sugerencias de consulta se especifican como parte de la [cláusula OPTION](../../t-sql/queries/option-clause-transact-sql.md). Si una o varias sugerencias de consulta provocan que el optimizador de consultas no genere un plan válido, se produce el error 8622.  
  
> [!CAUTION]  
> Como el optimizador de consultas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] suele seleccionar el mejor plan de ejecución para las consultas, se recomienda que solo los desarrolladores y administradores de bases de datos experimentados usen estas sugerencias y que lo hagan como último recurso.  
  
 **Se aplica a:**  
  
 [DELETE](../../t-sql/statements/delete-transact-sql.md)  
  
 [INSERT](../../t-sql/statements/insert-transact-sql.md)  
  
 [SELECT](../../t-sql/queries/select-transact-sql.md)  
  
 [UPDATE](../../t-sql/queries/update-transact-sql.md)  
  
 [MERGE](../../t-sql/statements/merge-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
<query_hint > ::=   
{ { HASH | ORDER } GROUP   
  | { CONCAT | HASH | MERGE } UNION   
  | { LOOP | MERGE | HASH } JOIN   
  | EXPAND VIEWS   
  | FAST number_rows   
  | FORCE ORDER   
  | { FORCE | DISABLE } EXTERNALPUSHDOWN  
  | IGNORE_NONCLUSTERED_COLUMNSTORE_INDEX  
  | KEEP PLAN   
  | KEEPFIXED PLAN  
  | MAX_GRANT_PERCENT = percent  
  | MIN_GRANT_PERCENT = percent  
  | MAXDOP number_of_processors   
  | MAXRECURSION number   
  | NO_PERFORMANCE_SPOOL   
  | OPTIMIZE FOR ( @variable_name { UNKNOWN | = literal_constant } [ , ...n ] )  
  | OPTIMIZE FOR UNKNOWN  
  | PARAMETERIZATION { SIMPLE | FORCED }   
  | RECOMPILE  
  | ROBUST PLAN   
  | USE HINT ( '<hint_name>' [ , ...n ] )
  | USE PLAN N'xml_plan'  | TABLE HINT ( exposed_object_name [ , <table_hint> [ [, ]...n ] ] )  
}  
  
<table_hint> ::=  
[ NOEXPAND ] {   
    INDEX ( index_value [ ,...n ] ) | INDEX = ( index_value )  
  | FORCESEEK [( index_value ( index_column_name [,... ] ) ) ]  
  | FORCESCAN  
  | HOLDLOCK   
  | NOLOCK   
  | NOWAIT  
  | PAGLOCK   
  | READCOMMITTED   
  | READCOMMITTEDLOCK   
  | READPAST   
  | READUNCOMMITTED   
  | REPEATABLEREAD   
  | ROWLOCK   
  | SERIALIZABLE   
  | SNAPSHOT  
  | SPATIAL_WINDOW_MAX_CELLS = integer  
  | TABLOCK   
  | TABLOCKX   
  | UPDLOCK   
  | XLOCK  
}  
```  
  
## <a name="arguments"></a>Argumentos  
 { HASH | ORDER } GROUP  
 Especifica que las agregaciones especificadas en la cláusula GROUP BY o DISTINCT de la consulta deben usar hash o un orden.  
  
 { MERGE | HASH | CONCAT } UNION  
 Especifica que todas las operaciones UNION se deben realizar mediante la mezcla, hash o concatenación de conjuntos UNION. Si se especifica más de una sugerencia UNION, el optimizador de consultas seleccionará la estrategia menos costosa entre las sugerencias especificadas.  
  
 { LOOP | MERGE | HASH } JOIN  
 Especifica que todas las operaciones de combinación se realicen mediante LOOP JOIN, MERGE JOIN o HASH JOIN en toda la consulta. Si se especifica más de una sugerencia de combinación, el optimizador seleccionará la estrategia menos costosa de entre las permitidas.  
  
 Si, en la misma consulta, en la cláusula FROM se especifica también una sugerencia de combinación para una pareja de tablas específica, la sugerencia de combinación tendrá prioridad en la combinación de las dos tablas aunque aún se deban respetar las sugerencias de consulta. Por tanto, es posible que la sugerencia de combinación para la pareja de tablas solo restrinja la selección de los métodos de combinación permitidos en la sugerencia de consulta. Para obtener más información, vea [Sugerencias de combinación &#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-join.md).  
  
 EXPAND VIEWS  
 Especifica que las vistas indizadas se expanden y que el optimizador de consultas no considerará ninguna vista indizada como sustituto de una parte de la consulta. Una vista se expande cuando se reemplaza el nombre de la vista por la definición de la vista en el texto de la consulta.  
  
 Esta sugerencia de consulta virtualmente no permite el uso directo de vistas indizadas ni índices en vistas indizadas en el plan de consulta.  
  
 La vista indexada no se expande únicamente si se hace referencia directa a la vista en la parte SELECT de la consulta y se especifica WITH (NOEXPAND) o WITH (NOEXPAND, INDEX( *index_value* [ **,**_...n_ ] ) ). Para más información sobre la sugerencia de consulta WITH (NOEXPAND), vea [FROM](../../t-sql/queries/from-transact-sql.md).  
  
 La sugerencia solo afecta a las vistas en la parte SELECT de las instrucciones, incluidas las vistas en las instrucciones INSERT, UPDATE, MERGE y DELETE.  
  
 FAST *number_rows*  
 Especifica que la consulta está optimizada para una recuperación rápida de las primeras *number_rows*. Es un entero no negativo. Después de que se devuelven las primeras *number_rows*, la consulta continúa la ejecución y presenta su conjunto de resultados completo.  
  
 FORCE ORDER  
 Especifica que el orden de combinación que indica la sintaxis de la consulta se mantenga durante la optimización de la consulta. El uso de FORCE ORDER no afecta al posible comportamiento de inversión de roles del optimizador de consultas.  
  
> [!NOTE]  
> En una instrucción MERGE, se obtiene acceso a la tabla de origen antes que a la tabla de destino como el orden de combinación predeterminado, a menos que se especifique la cláusula WHEN SOURCE NOT MATCHED. Al especificar FORCE ORDER, se conserva este comportamiento predeterminado.  
  
 { FORCE | DISABLE } EXTERNALPUSHDOWN  
 Fuerza o deshabilita la aplicación del cálculo de expresiones válidas en Hadoop. Solo se aplica a las consultas que usan PolyBase. No se aplicará a Azure Storage.  
  
 KEEP PLAN  
 Fuerza al optimizador de consultas a aumentar el umbral estimado para volver a compilar una consulta. El umbral estimado para volver a compilar es el punto en el que una consulta se vuelve a compilar automáticamente cuando se ha realizado el número estimado de cambios de columnas indizados en una tabla al ejecutar las instrucciones UPDATE, DELETE, MERGE o INSERT. Al especificar KEEP PLAN, se asegura de que no se volverá a compilar una consulta con tanta frecuencia cuando se producen varias actualizaciones en una tabla.  
  
 KEEPFIXED PLAN  
 Fuerza al optimizador de consultas a no compilar de nuevo una consulta debido a cambios en las estadísticas. Al especificar KEEPFIXED PLAN, se asegura de que solo se volverá a compilar una consulta si el esquema de las tablas subyacentes cambia o si **sp_recompile** se ejecuta en estas tablas.  
  
 IGNORE_NONCLUSTERED_COLUMNSTORE_INDEX  
 **Se aplica a**: desde [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Impide que la consulta use un índice no agrupado de almacén de columnas optimizado para memoria. Si la consulta contiene la sugerencia de consulta para evitar el uso del índice de almacén de columnas y una sugerencia de índice para usar un índice de almacén de columnas, las sugerencias están en conflicto y la consulta devuelve un error.  
  
 MAX_GRANT_PERCENT = *percent*  
 Tamaño de concesión de memoria máximo en PERCENT. Se garantiza que la consulta no superará este límite. El límite real puede ser menor si la configuración de Resource Governor es inferior al valor especificado por esta sugerencia. Los valores válidos están comprendidos entre 0,0 y 100,0.  
  
**Se aplica a**: desde [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 MIN_GRANT_PERCENT = *percent*  
 Tamaño de concesión de memoria mínimo en PERCENT = % del límite predeterminado. Se garantiza que la consulta obtendrá el valor MAX(required memory, min grant) porque se requiere al menos la memoria necesaria para iniciar una consulta. Los valores válidos están comprendidos entre 0,0 y 100,0.  
  
**Se aplica a**: desde [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 MAXDOP *number*  
 **Se aplica a**: desde [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Invalida la opción de configuración **Grado máximo de paralelismo** de **sp_configure** y Resource Governor para la consulta que especifica esta opción. La sugerencia de consulta MAXDOP puede superar el valor configurado con sp_configure. Si MAXDOP supera el valor configurado con Resource Governor, el [!INCLUDE[ssDE](../../includes/ssde-md.md)] usa el valor MAXDOP de Resource Governor, descrito en [ALTER WORKLOAD GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/alter-workload-group-transact-sql.md). Se pueden aplicar todas las reglas semánticas usadas con la opción de configuración **Grado máximo de paralelismo** cuando se usa la sugerencia de consulta MAXDOP. Para obtener más información, vea [Establecer la opción de configuración del servidor Grado máximo de paralelismo](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md).  
  
> [!WARNING]     
> Si MAXDOP se establece en cero, el servidor elige el grado máximo de paralelismo.  
  
 MAXRECURSION *number*     
 Especifica el número máximo de recursiones permitidas para esta consulta. *number* es un entero no negativo entre 0 y 32 767. Cuando se especifica 0, no se aplica ningún límite. Si no se especifica esta opción, el límite predeterminado para el servidor es 100.  
  
 Cuando se alcanza el número predeterminado o especificado para el límite de MAXRECURSION durante la ejecución de la consulta, la consulta finaliza y se devuelve un error.  
  
 Debido a este error, todos los efectos de la instrucción se revierten. Si la instrucción es una instrucción SELECT, es posible que no se devuelva ningún resultado o que los resultados sean parciales. Puede que los resultados parciales no incluyan todas las filas de los niveles de recursividad que superen el nivel de recursividad máximo especificado.  
  
 Para más información, vea [WITH common_table_expression &#40;Transact-SQL&#41;](../../t-sql/queries/with-common-table-expression-transact-sql.md).     
  
 NO_PERFORMANCE_SPOOL    
 **Se aplica a**: desde [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Impide que se agregue un operador de cola de impresión a planes de consulta (excepto a los planes en los que se requiere que la cola de impresión garantice una semántica de actualización válida). En algunos escenarios, el operador de cola de impresión puede reducir el rendimiento. Por ejemplo, la cola de impresión usa tempdb, y puede producirse la contención de tempdb si se ejecutan muchas consultas simultáneas con las operaciones de cola de impresión.  
  
 OPTIMIZE FOR ( *@variable_name* { UNKNOWN | = *literal_constant }* [ **,** ...*n* ] )     
 Indica al optimizador de consultas que utilice un valor concreto para una variable local cuando la consulta se compila y optimiza. El valor se utiliza solo durante la optimización de la consulta y no durante la ejecución de la misma.  
  
 *@variable_name*  
 Es el nombre de una variable local que se utiliza en una consulta, a la que se puede asignar un valor para utilizarlo con la sugerencia de consulta OPTIMIZE FOR.  
  
 *UNKNOWN*  
 Indica al optimizador de consultas que use datos estadísticos en lugar del valor inicial para determinar el valor de una variable local durante la optimización de la consulta.  
  
 *literal_constant*  
 Es un valor constante literal al que se asigna *@variable_name* para su uso con la sugerencia de consulta OPTIMIZE FOR. *literal_constant* se usa solo durante la optimización de la consulta y no como el valor de *@variable_name* durante la ejecución de la consulta. *literal_constant* puede tener cualquier tipo de datos de sistema de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que se pueda expresar como una constante literal. El tipo de datos de *literal_constant* debe convertirse de forma implícita al tipo de datos al que *@variable_name* hace referencia en la consulta.  
  
 OPTIMIZE FOR puede contrarrestar el comportamiento predeterminado de detección de parámetros del optimizador o puede utilizarse cuando se crean guías de plan. Para más información, vea [Volver a compilar un procedimiento almacenado](../../relational-databases/stored-procedures/recompile-a-stored-procedure.md).  
  
 OPTIMIZE FOR UNKNOWN  
 Indica al optimizador de consultas que use datos estadísticos en lugar de los valores iniciales para todas las variables locales al compilar y optimizar la consulta, incluidos los parámetros creados mediante parametrización forzada.  
  
 Si se usan OPTIMIZE FOR @variable_name = *literal_constant* y OPTIMIZE FOR UNKNOWN en la misma sugerencia de consulta, el optimizador de consultas usará el valor *literal_constant* especificado para un valor determinado y UNKNOWN para los valores de las variables restantes. Los valores se usan solo durante la optimización de la consulta y no durante la ejecución de la misma.  
  
 PARAMETERIZATION { SIMPLE | FORCED }     
 Especifica las reglas de parametrización que aplica el optimizador de consultas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cuando se compila la consulta.  
  
> [!IMPORTANT]  
> La sugerencia de consulta PARAMETERIZATION solo se puede especificar en una guía de plan para invalidar la configuración actual de la opción SET de base de datos PARAMETERIZATION. No se puede especificar directamente en una consulta.    
> Para más información, vea [Especificar el comportamiento de parametrización de consultas por medio de guías de plan](../../relational-databases/performance/specify-query-parameterization-behavior-by-using-plan-guides.md).
  
 SIMPLE indica al optimizador de consultas para que intente la parametrización simple. FORCED indica al optimizador de consultas que intente la parametrización forzada. Para más información, vea [Parametrización forzada en la guía de arquitectura de procesamiento de consultas](../../relational-databases/query-processing-architecture-guide.md#ForcedParam) y [Parametrización simple en la guía de arquitectura de procesamiento de consultas](../../relational-databases/query-processing-architecture-guide.md#SimpleParam).  

 RECOMPILE  
 Indica a [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] que genere un plan nuevo y temporal para la consulta y descarte de inmediato ese plan una vez que se completa la ejecución de la consulta. El plan de consulta generado no reemplaza un plan almacenado en caché cuando la misma consulta se ejecuta sin la sugerencia RECOMPILE. Sin especificar RECOMPILE, el [!INCLUDE[ssDE](../../includes/ssde-md.md)] almacena en la memoria caché planes de consulta y los reutiliza. Cuando se compilan planes de consulta, la sugerencia de consulta RECOMPILE utiliza los valores actuales de cualquier variable local de la consulta y, si la consulta está en un procedimiento almacenado, los valores actuales enviados a cualquier parámetro.  
  
 RECOMPILE es una alternativa útil a la creación de un procedimiento almacenado que utiliza la cláusula WITH RECOMPILE cuando solo se debe volver a compilar un subconjunto de consultas del procedimiento almacenado, en lugar de todo el procedimiento almacenado. Para más información, vea [Volver a compilar un procedimiento almacenado](../../relational-databases/stored-procedures/recompile-a-stored-procedure.md). RECOMPILE también es útil al crear guías de plan.  
  
 ROBUST PLAN  
 Fuerza al optimizador de consultas a intentar aplicar un plan que funcione para el tamaño máximo de fila posible en detrimento del rendimiento. Cuando se procesa la consulta, es posible que las tablas intermedias y los operadores necesiten guardar y procesar filas más anchas que las filas de entrada. Las filas pueden llegar a ser tan anchas que, en algunos casos, el operador especificado no puede procesar la fila. Si esto sucede, el [!INCLUDE[ssDE](../../includes/ssde-md.md)] genera un error durante la ejecución de la consulta. Mediante la utilización de ROBUST PLAN, puede indicar al optimizador de consultas que no tenga en cuenta los planes de consulta donde pueda ocurrir este problema.  
  
 Si no es posible realizar tal plan, el optimizador de consultas devuelve un error en lugar de diferir la detección de errores hasta la ejecución de la consulta. Las filas pueden contener columnas de longitud variable; el [!INCLUDE[ssDE](../../includes/ssde-md.md)] permite definir filas con un tamaño potencial máximo que supere la capacidad del [!INCLUDE[ssDE](../../includes/ssde-md.md)] para procesarlas. Normalmente, a pesar del tamaño potencial máximo, una aplicación almacena filas cuyo tamaño real se encuentra dentro de los límites que puede procesar el [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Si el [!INCLUDE[ssDE](../../includes/ssde-md.md)] encuentra una fila demasiado larga, devuelve un error de ejecución.  
 
<a name="use_hint"></a> USE HINT ( **'**_hint\_name_**'** )    
 **Se aplica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (a partir de [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1) y [!INCLUDE[ssSDS](../../includes/sssds-md.md)].
 
 Proporciona una o varias sugerencias adicionales para el procesador de consultas según lo especificado mediante un nombre de sugerencia **entre comillas simples**.   

 Se admiten los siguientes nombres de sugerencia:    
 
*  'ASSUME_JOIN_PREDICATE_DEPENDS_ON_FILTERS' <a name="use_hint_join_containment"></a>       
   Hace que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] genere un plan de consulta mediante la suposición de contención simple en lugar de la suposición de contención de base predeterminada para las combinaciones en el modelo de [estimación de la cardinalidad](../../relational-databases/performance/cardinality-estimation-sql-server.md) del [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] o versiones más recientes. Es equivalente a la [marca de seguimiento](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) 9476. 
*  'ASSUME_MIN_SELECTIVITY_FOR_FILTER_ESTIMATES' <a name="use_hint_correlation"></a>      
   Hace que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] genere un plan con una selectividad mínima al estimar predicados AND para que los filtros tengan en cuenta la correlación. Es equivalente a la [marca de seguimiento](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) 4137 cuando se usa con el modelo de estimación de la cardinalidad de [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] y versiones anteriores, y tiene un efecto similar cuando se usa la [marca de seguimiento](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) 9471 con el modelo de estimación de la cardinalidad de [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] o versiones posteriores.
*  "DISABLE_BATCH_MODE_ADAPTIVE_JOINS"       
   Deshabilita las combinaciones adaptables del modo por lotes. Para obtener más información, vea [Combinaciones adaptables del modo por lotes](../../relational-databases/performance/adaptive-query-processing.md#batch-mode-adaptive-joins).
*  "DISABLE_BATCH_MODE_MEMORY_GRANT_FEEDBACK"       
   Deshabilita los comentarios de concesión de memoria en modo por lotes. Para obtener más información, vea [Comentarios de concesión de memoria de modo de proceso por lotes](../../relational-databases/performance/adaptive-query-processing.md#batch-mode-memory-grant-feedback).
*  "DISABLE_INTERLEAVED_EXECUTION_TVF"      
   Deshabilita la ejecución intercalada de las funciones con valores de tabla de múltiples instrucciones. Para más información, consulte [Ejecución intercalada de funciones con valores de tabla de múltiples instrucciones](../../relational-databases/performance/adaptive-query-processing.md#interleaved-execution-for-multi-statement-table-valued-functions).
*  "DISABLE_OPTIMIZED_NESTED_LOOP"      
   Indica al procesador de consultas que no use una operación de ordenación (ordenación por lotes) para las combinaciones de bucle anidado optimizadas cuando se genera un plan de consulta. Es equivalente a la [marca de seguimiento](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) 2340.
*  'DISABLE_OPTIMIZER_ROWGOAL' <a name="use_hint_rowgoal"></a>      
   Hace que SQL Server genere un plan que no usa los ajustes de objetivo de filas con las consultas que contienen las palabras clave TOP, OPTION (FAST N), IN o EXISTS. Es equivalente a la [marca de seguimiento](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) 4138.
*  "DISABLE_PARAMETER_SNIFFING"      
   Indica al optimizador de consultas que use la distribución de datos media al compilar una consulta con uno o varios parámetros, lo que hace que el plan de consulta sea independiente del valor de parámetro usado en primer lugar al compilar la consulta. Es equivalente a la [marca de seguimiento](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) 4136 o a la opción de [configuración con ámbito de base de datos ](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md) PARAMETER_SNIFFING=OFF.
*  "ENABLE_HIST_AMENDMENT_FOR_ASC_KEYS"      
   Habilita las estadísticas rápidas generadas automáticamente (modificación de histograma) para las columnas de índice iniciales para las que se necesite la estimación de cardinalidad. El histograma usado para calcular la cardinalidad se ajustará en tiempo de compilación de la consulta para tener en cuenta el valor máximo o mínimo real de esta columna. Es equivalente a la [marca de seguimiento](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) 4139. 
*  "ENABLE_QUERY_OPTIMIZER_HOTFIXES"     
   Permite revisiones del optimizador de consultas (cambios publicados en las actualizaciones acumulativas y Service Packs de SQL Server). Es equivalente a la [marca de seguimiento](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) 4199 o a la opción de [configuración con ámbito de base de datos ](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md) QUERY_OPTIMIZER_HOTFIXES=ON.
*  "FORCE_DEFAULT_CARDINALITY_ESTIMATION"      
   Fuerza al optimizador de consultas a usar el modelo de [estimación de la cardinalidad](../../relational-databases/performance/cardinality-estimation-sql-server.md) que se corresponde con el nivel de compatibilidad de la base de datos actual. Use esta sugerencia para invalidar la opción de [configuración con ámbito de base de datos](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md) LEGACY_CARDINALITY_ESTIMATION=ON o la [marca de seguimiento](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) 9481.
*  'FORCE_LEGACY_CARDINALITY_ESTIMATION' <a name="use_hint_ce70"></a>      
   Fuerza al optimizador de consultas a usar el modelo de [estimación de la cardinalidad](../../relational-databases/performance/cardinality-estimation-sql-server.md) de [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] y versiones anteriores. Es equivalente a la [marca de seguimiento](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) 9481 o a la opción de [configuración con ámbito de base de datos ](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md) LEGACY_CARDINALITY_ESTIMATION=ON.
*  'QUERY_OPTIMIZER_COMPATIBILITY_LEVEL_n'          
 Fuerza el comportamiento del optimizador de consultas en un nivel de consulta, como si la consulta se compilara con nivel de compatibilidad de base de datos *n*, donde *n* es un nivel de compatibilidad de base de datos compatible. Consulte [sys.dm_exec_valid_use_hints](../../relational-databases/system-dynamic-management-views/sys-dm-exec-valid-use-hints-transact-sql.md) para ver una lista de los valores admitidos actualmente para *n*. **Se aplica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (a partir de [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] CU10).    

   > [!NOTE]
   > La sugerencia QUERY_OPTIMIZER_COMPATIBILITY_LEVEL_n no invalida la configuración de la estimación de cardinalidad heredada o predeterminada, si se fuerza a través de la configuración con ámbito de base de datos, marca de seguimiento u otra sugerencia de consulta como QUERYTRACEON.   
   > Esta sugerencia solo afecta al comportamiento del optimizador de consultas. No afecta a otras características de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que pueden depender del [nivel de compatibilidad de base de datos](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md), como la disponibilidad de determinadas características de base de datos.  
   > Para obtener más información sobre esta sugerencia, vea [Developer's Choice: Hinting Query Execution model](https://blogs.msdn.microsoft.com/sql_server_team/developers-choice-hinting-query-execution-model) (Elección del desarrollador: modelo de ejecución de consultas de sugerencias).
    
*  'QUERY_PLAN_PROFILE'      
 Habilita la generación de perfiles ligera para la consulta. Cuando finaliza una consulta que contiene esta nueva sugerencia, se activa un nuevo evento extendido: query_plan_profile. Este evento extendido expone las estadísticas de ejecución y el plan de ejecución real XML similar al evento extendido query_post_execution_showplan, pero solo para las consultas que contiene la nueva sugerencia. **Se aplica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (a partir de [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP2 CU3 y [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] CU11). 

  > [!NOTE]
  > Si habilita la recopilación del evento extendido query_post_execution_showplan, se agregará la infraestructura de generación de perfiles estándar para todas las consultas que se están ejecutando en el servidor, por lo que podría resultar afectado el rendimiento global del servidor.      
  > Si habilita la recopilación del evento extendido *query_thread_profile* para usar en su lugar la generación de perfiles ligera, habrá una sobrecarga de rendimiento mucho mejor, pero seguirá resultando afectado el rendimiento global del servidor.       
  > Si habilita el evento extendido query_plan_profile, solo se habilitará la infraestructura ligera de generación de perfiles para una consulta que se ejecutó con QUERY_PLAN_PROFILE, con lo que las otras cargas de trabajo del servidor no resultarán afectadas. Use esta sugerencia para generar perfiles de una consulta específica sin que esto afecte a otras partes de la carga de trabajo del servidor.
  > Para obtener más información sobre la generación de perfiles ligera, vea [Developers Choice: Query progress - anytime, anywhere](https://blogs.msdn.microsoft.com/sql_server_team/query-progress-anytime-anywhere/) (Elección de los desarrolladores: progreso de la consulta, en cualquier momento y en cualquier lugar).
 
Puede consultar la lista de todos los nombres de USE HINT compatibles mediante la vista de administración dinámica [sys.dm_exec_valid_use_hints](../../relational-databases/system-dynamic-management-views/sys-dm-exec-valid-use-hints-transact-sql.md).    

> [!TIP]
> Los nombres de sugerencia no distinguen mayúsculas de minúsculas.   
  
> [!IMPORTANT] 
> Algunas sugerencias USE HINT pueden entrar en conflicto con las marcas de seguimiento habilitadas a nivel global o de sesión, o con las opciones de configuración con ámbito de base de datos. En este caso, la sugerencia de nivel de consulta (USE HINT) siempre tiene prioridad. Si una sugerencia USE HINT entra en conflicto con otra sugerencia de consulta o una marca de seguimiento habilitada en el nivel de consulta (por ejemplo, mediante QUERYTRACEON), [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] generará un error al intentar ejecutar la consulta. 

 USE PLAN N **'**_xml\_plan_**'**     
 Fuerza al optimizador de consultas a usar un plan de consulta existente en una consulta especificada por **'**_xml\_plan_**'**. USE PLAN no puede especificarse con las instrucciones INSERT, UPDATE, MERGE ni DELETE.  
  
TABLE HINT **(**_exposed\_object\_name_ [ **,** \<table_hint> [ [**,** ]..._n_ ] ] **)** Aplica la sugerencia de la tabla especificada a la tabla o vista que corresponde a *exposed_object_name*. Se recomienda usar una sugerencia de tabla como una sugerencia de consulta únicamente en el contexto de una [guía de plan](../../relational-databases/performance/plan-guides.md).  
  
 *exposed_object_name* puede ser una de las referencias siguientes:  
  
-   Cuando se usa un alias para la tabla o vista en la cláusula [FROM](../../t-sql/queries/from-transact-sql.md) de la consulta, el alias es *exposed_object_name*.  
  
-   Cuando no se usa un alias, *exposed_object_name* es la coincidencia exacta de la tabla o vista a la que se hace referencia en la cláusula FROM. Por ejemplo, si se hace referencia a la tabla o vista con un nombre de dos partes, *exposed_object_name* es el mismo nombre de dos partes.  
  
 Cuando se especifica *exposed_object_name* sin especificar además una sugerencia de tabla, se omite cualquier índice especificado en la consulta como parte de una sugerencia de tabla para el objeto y el optimizador de consultas determina el uso de índices. Puede emplear esta técnica para eliminar el efecto de una sugerencia de tabla INDEX cuando no se puede modificar la consulta original. Vea el ejemplo J.  
  
**\<table_hint> ::=** { [ NOEXPAND ] { INDEX ( *index_value* [ ,...*n* ] ) | INDEX = ( *index_value* ) | FORCESEEK [**(**_index\_value_**(**_index\_column\_name_ [**,**... ] **))** ]| FORCESCAN | HOLDLOCK | NOLOCK | NOWAIT | PAGLOCK | READCOMMITTED | READCOMMITTEDLOCK | READPAST | READUNCOMMITTED | REPEATABLEREAD | ROWLOCK | SERIALIZABLE | SNAPSHOT | SPATIAL_WINDOW_MAX_CELLS | TABLOCK | TABLOCKX | UPDLOCK | XLOCK } Es la sugerencia de tabla que se aplica a la tabla o vista que corresponde a *exposed_object_name* como una sugerencia de consulta. Para obtener una descripción de estas sugerencias, vea [Sugerencias de tabla &#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-table.md).  
  
 Las sugerencias de tabla distintas de INDEX, FORCESCAN y FORCESEEK no están permitidas como sugerencias de consulta, a menos que la consulta ya tenga una cláusula WITH que especifique la sugerencia de tabla. Para obtener más información, vea la sección Comentarios.  
  
> [!CAUTION] 
> Al especificar FORCESEEK con parámetros se limita el número de planes que el optimizador puede considerar en comparación con cuando se especifica FORCESEEK sin parámetros. Esto puede producir un error "No se puede generar el plan" en más casos. En una versión futura, las modificaciones internas realizadas en el optimizador pueden permitir que se consideren más planes.  
  
## <a name="remarks"></a>Notas  
 No se pueden especificar sugerencias de consulta en una instrucción INSERT, excepto cuando se usa una cláusula SELECT en la instrucción.  
  
 Solo se pueden especificar sugerencias de consulta en la consulta de nivel superior, no en las subconsultas. Cuando se especifica una sugerencia de tabla como una sugerencia de consulta, la sugerencia se puede especificar en la consulta de nivel superior o en una subconsulta, pero el valor especificado para *exposed_object_name* en la cláusula TABLE HINT debe coincidir exactamente con el nombre expuesto en la consulta o subconsulta.  
  
## <a name="specifying-table-hints-as-query-hints"></a>Especificar sugerencias de tabla como sugerencias de consulta  
 Se recomienda usar la sugerencia de tabla INDEX, FORCESCAN o FORCESEEK como sugerencia de consulta únicamente en el contexto de una [guía de plan](../../relational-databases/performance/plan-guides.md). Las guías de plan son útiles cuando no se puede modificar la consulta original, por ejemplo, porque es una aplicación de otro fabricante. La sugerencia de consulta especificada en la guía de plan se agrega a la consulta antes de compilarla y optimizarla. Para las consultas ad hoc, utilice la cláusula TABLE HINT únicamente en las pruebas de instrucciones de guías de plan. Para todas las demás consultas ad hoc, se recomienda especificar estas sugerencias únicamente como sugerencias de tabla.  
  
 Cuando se especifican como una sugerencia de consulta, las sugerencias de tabla INDEX, FORCESCAN y FORCESEEK son válidas para los objetos siguientes:  
  
-   Tablas  
-   Vistas  
-   Vistas indizadas  
-   Expresiones de tabla comunes (la sugerencia se debe especificar en la instrucción SELECT cuyo conjunto de resultados rellena la expresión de tabla común)  
-   Vistas de administración dinámica  
-   Subconsultas con nombre  
  
Se pueden especificar las sugerencias de tabla INDEX, FORCESCAN y FORCESEEK como sugerencias de consulta para una consulta que no tenga ninguna sugerencia de tabla existente, o bien se pueden usar para reemplazar en la consulta las respectivas sugerencias INDEX, FORCESCAN o FORCESEEK existentes. Las sugerencias de tabla distintas de INDEX, FORCESCAN y FORCESEEK no están permitidas como sugerencias de consulta, a menos que la consulta ya tenga una cláusula WITH que especifique la sugerencia de tabla. En este caso, también se debe especificar una consulta coincidente como sugerencia de consulta mediante el uso de TABLE HINT en la cláusula OPTION para conservar la semántica de la consulta. Por ejemplo, si la consulta contiene la sugerencia de tabla NOLOCK, la cláusula OPTION del parámetro **@hints** de la guía de plan también debe contener la sugerencia NOLOCK. Vea el ejemplo K. Cuando se especifica una sugerencia de tabla distinta de INDEX, FORCESCAN o FORCESEEK mediante TABLE HINT en la cláusula OPTION sin una sugerencia de consulta coincidente, o viceversa, se genera el error 8702 (que indica que la cláusula OPTION puede hacer que la semántica de la consulte cambie) y se produce un error en la consulta.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-using-merge-join"></a>A. Usar MERGE JOIN  
 En el siguiente ejemplo se especifica que la operación JOIN de la consulta se realiza mediante una combinación MERGE JOIN. En el ejemplo se usa la base de datos [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)].  
  
```sql  
SELECT *   
FROM Sales.Customer AS c  
INNER JOIN Sales.CustomerAddress AS ca ON c.CustomerID = ca.CustomerID  
WHERE TerritoryID = 5  
OPTION (MERGE JOIN);  
GO    
```  
  
### <a name="b-using-optimize-for"></a>B. Usar OPTIMIZE FOR  
 En el ejemplo siguiente se indica al optimizador de consultas que use el valor `'Seattle'`para la variable local `@city_name` y que use datos estadísticos para determinar el valor de la variable local `@postal_code` al optimizar la consulta. En el ejemplo se usa la base de datos [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)].  
  
```sql  
DECLARE @city_name nvarchar(30);  
DECLARE @postal_code nvarchar(15);  
SET @city_name = 'Ascheim';  
SET @postal_code = 86171;  
SELECT * FROM Person.Address  
WHERE City = @city_name AND PostalCode = @postal_code  
OPTION ( OPTIMIZE FOR (@city_name = 'Seattle', @postal_code UNKNOWN) );  
GO  
```  
  
### <a name="c-using-maxrecursion"></a>C. Usar MAXRECURSION  
 MAXRECURSION se puede utilizar para impedir que una expresión de tabla común recursiva con formato incorrecto entre en un bucle infinito. En el ejemplo siguiente se crea un bucle infinito intencionadamente y se usa la sugerencia MAXRECURSION para limitar el número de niveles de recursividad a dos. En el ejemplo se usa la base de datos [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)].  
  
```sql  
--Creates an infinite loop  
WITH cte (CustomerID, PersonID, StoreID) AS  
(  
    SELECT CustomerID, PersonID, StoreID  
    FROM Sales.Customer  
    WHERE PersonID IS NOT NULL  
  UNION ALL  
    SELECT cte.CustomerID, cte.PersonID, cte.StoreID  
    FROM cte   
    JOIN  Sales.Customer AS e   
        ON cte.PersonID = e.CustomerID  
)  
--Uses MAXRECURSION to limit the recursive levels to 2  
SELECT CustomerID, PersonID, StoreID  
FROM cte  
OPTION (MAXRECURSION 2);  
GO  
```  
  
 Después de corregir el error de código, ya no se requiere MAXRECURSION.  
  
### <a name="d-using-merge-union"></a>D. Usar MERGE UNION  
 En el ejemplo siguiente se usa la sugerencia de consulta MERGE UNION. En el ejemplo se usa la base de datos [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)].  
  
```sql  
SELECT *  
FROM HumanResources.Employee AS e1  
UNION  
SELECT *  
FROM HumanResources.Employee AS e2  
OPTION (MERGE UNION);  
GO  
```  
  
### <a name="e-using-hash-group-and-fast"></a>E. Usar HASH GROUP y FAST  
 En el ejemplo siguiente se usan las sugerencias de consulta HASH GROUP y FAST. En el ejemplo se usa la base de datos [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)].  
  
```sql  
SELECT ProductID, OrderQty, SUM(LineTotal) AS Total  
FROM Sales.SalesOrderDetail  
WHERE UnitPrice < $5.00  
GROUP BY ProductID, OrderQty  
ORDER BY ProductID, OrderQty  
OPTION (HASH GROUP, FAST 10);  
GO    
```  
  
### <a name="f-using-maxdop"></a>F. Usar MAXDOP  
 En el ejemplo siguiente se usa la sugerencia de consulta MAXDOP. En el ejemplo se usa la base de datos [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)].  
  
**Se aplica a**: desde [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
```sql  
SELECT ProductID, OrderQty, SUM(LineTotal) AS Total  
FROM Sales.SalesOrderDetail  
WHERE UnitPrice < $5.00  
GROUP BY ProductID, OrderQty  
ORDER BY ProductID, OrderQty  
OPTION (MAXDOP 2);    
GO
```  
  
### <a name="g-using-index"></a>G. Usar INDEX  
 Los ejemplos siguientes usan la sugerencia INDEX. El primer ejemplo especifica un índice único. El segundo ejemplo especifica varios índices para obtener una única referencia de tabla. En ambos ejemplos, como la sugerencia INDEX se aplica a una tabla que usa un alias, la cláusula TABLE HINT también debe especificar el mismo alias que el nombre del objeto expuesto. En el ejemplo se usa la base de datos [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)].  
  
```sql  
EXEC sp_create_plan_guide   
    @name = N'Guide1',   
    @stmt = N'SELECT c.LastName, c.FirstName, e.Title  
              FROM HumanResources.Employee AS e   
              JOIN Person.Contact AS c ON e.ContactID = c.ContactID  
              WHERE e.ManagerID = 2;',   
    @type = N'SQL',  
    @module_or_batch = NULL,   
    @params = NULL,   
    @hints = N'OPTION (TABLE HINT(e, INDEX (IX_Employee_ManagerID)))';  
GO  
EXEC sp_create_plan_guide   
    @name = N'Guide2',   
    @stmt = N'SELECT c.LastName, c.FirstName, e.Title  
              FROM HumanResources.Employee AS e  
              JOIN Person.Contact AS c ON e.ContactID = c.ContactID  
              WHERE e.ManagerID = 2;',   
    @type = N'SQL',  
    @module_or_batch = NULL,   
    @params = NULL,   
    @hints = N'OPTION (TABLE HINT(e, INDEX(PK_Employee_EmployeeID, IX_Employee_ManagerID)))';  
GO    
```  
  
### <a name="h-using-forceseek"></a>H. Usar FORCESEEK  
 En el siguiente ejemplo se utiliza la sugerencia de tabla FORCESEEK. Como la sugerencia INDEX se aplica a una tabla que usa un nombre de dos partes, la cláusula TABLE HINT también debe especificar el mismo nombre de dos partes que el nombre del objeto expuesto. En el ejemplo se usa la base de datos [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)].  
  
```sql  
EXEC sp_create_plan_guide   
    @name = N'Guide3',   
    @stmt = N'SELECT c.LastName, c.FirstName, HumanResources.Employee.Title  
              FROM HumanResources.Employee  
              JOIN Person.Contact AS c ON HumanResources.Employee.ContactID = c.ContactID  
              WHERE HumanResources.Employee.ManagerID = 3  
              ORDER BY c.LastName, c.FirstName;',   
    @type = N'SQL',  
    @module_or_batch = NULL,   
    @params = NULL,   
    @hints = N'OPTION (TABLE HINT( HumanResources.Employee, FORCESEEK))';  
GO    
```  
  
### <a name="i-using-multiple-table-hints"></a>I. Usar varias sugerencias de tabla  
 El ejemplo siguiente aplica la sugerencia INDEX a una tabla y la sugerencia FORCESEEK a otra. En el ejemplo se usa la base de datos [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)].  
  
```sql  
EXEC sp_create_plan_guide   
    @name = N'Guide4',   
    @stmt = N'SELECT e.ManagerID, c.LastName, c.FirstName, e.Title  
              FROM HumanResources.Employee AS e   
              JOIN Person.Contact AS c ON e.ContactID = c.ContactID  
              WHERE e.ManagerID = 3;',   
    @type = N'SQL',  
    @module_or_batch = NULL,   
    @params = NULL,   
    @hints = N'OPTION (TABLE HINT (e, INDEX( IX_Employee_ManagerID))   
                       , TABLE HINT (c, FORCESEEK))';  
GO  
```  
  
### <a name="j-using-table-hint-to-override-an-existing-table-hint"></a>J. Usar TABLE HINT para invalidar una sugerencia de tabla existente  
 El ejemplo siguiente muestra cómo usar la sugerencia TABLE HINT sin especificar una sugerencia para anular temporalmente el comportamiento de la sugerencia de tabla INDEX que se especificó en la cláusula FROM de la consulta. En el ejemplo se usa la base de datos [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)].  
  
```sql  
EXEC sp_create_plan_guide   
    @name = N'Guide5',   
    @stmt = N'SELECT e.ManagerID, c.LastName, c.FirstName, e.Title  
              FROM HumanResources.Employee AS e WITH (INDEX (IX_Employee_ManagerID))  
              JOIN Person.Contact AS c ON e.ContactID = c.ContactID  
              WHERE e.ManagerID = 3;',   
    @type = N'SQL',  
    @module_or_batch = NULL,   
    @params = NULL,   
    @hints = N'OPTION (TABLE HINT(e))';  
GO    
```  
  
### <a name="k-specifying-semantics-affecting-table-hints"></a>K. Especificar sugerencias de tabla que afectan a la semántica  
 El ejemplo siguiente contiene dos sugerencias de tabla en la consulta: NOLOCK, que afecta a la semántica, e INDEX, que no la afecta. Para conservar la semántica de la consulta, la sugerencia NOLOCK se especifica en la cláusula OPTIONS de la guía de plan. Además de la sugerencia NOLOCK, las sugerencias INDEX y FORCESEEK se especifican y reemplazan la sugerencia INDEX que no afecta a la semántica en la consulta cuando la instrucción se compila y optimiza. En el ejemplo se usa la base de datos [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)].  
  
```sql  
EXEC sp_create_plan_guide   
    @name = N'Guide6',   
    @stmt = N'SELECT c.LastName, c.FirstName, e.Title  
              FROM HumanResources.Employee AS e   
                   WITH (NOLOCK, INDEX (PK_Employee_EmployeeID))  
              JOIN Person.Contact AS c ON e.ContactID = c.ContactID  
              WHERE e.ManagerID = 3;',  
    @type = N'SQL',  
    @module_or_batch = NULL,   
    @params = NULL,   
    @hints = N'OPTION (TABLE HINT (e, INDEX(IX_Employee_ManagerID), NOLOCK, FORCESEEK))';  
GO    
```  
  
 El ejemplo siguiente muestra un método alternativo para conservar la semántica de la consulta y permitir al optimizador elegir un índice distinto del índice que se especificó en la sugerencia de tabla. Esto se consigue especificando la sugerencia NOLOCK en la cláusula OPTIONS (porque afecta a la semántica) y especificando la palabra clave TABLE HINT solamente con una referencia de tabla y ninguna sugerencia INDEX. En el ejemplo se usa la base de datos [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)].  
  
```sql  
EXEC sp_create_plan_guide   
    @name = N'Guide7',   
    @stmt = N'SELECT c.LastName, c.FirstName, e.Title  
              FROM HumanResources.Employee AS e   
                   WITH (NOLOCK, INDEX (PK_Employee_EmployeeID))  
              JOIN Person.Contact AS c ON e.ContactID = c.ContactID  
              WHERE e.ManagerID = 2;',  
    @type = N'SQL',  
    @module_or_batch = NULL,   
    @params = NULL,   
    @hints = N'OPTION (TABLE HINT (e, NOLOCK))';  
GO  
```  
### <a name="l-using-use-hint"></a>L. Usar la sugerencia USE HINT  
 En el ejemplo siguiente se usan las sugerencias de consulta RECOMPILE y USE HINT. En el ejemplo se usa la base de datos [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)].  
  
**Se aplica a**: [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)], [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)].  
  
```sql  
SELECT * FROM Person.Address  
WHERE City = 'SEATTLE' AND PostalCode = 98104
OPTION (RECOMPILE, USE HINT ('ASSUME_MIN_SELECTIVITY_FOR_FILTER_ESTIMATES', 'DISABLE_PARAMETER_SNIFFING')); 
GO  
```  
    
## <a name="see-also"></a>Ver también  
 [Hints &#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql.md)   
 [sp_create_plan_guide &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql.md)   
 [sp_control_plan_guide &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-control-plan-guide-transact-sql.md)  
 [Marcas de seguimiento](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)       
 [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)      
  
