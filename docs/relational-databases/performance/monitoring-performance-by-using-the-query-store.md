---
title: "Supervisión del rendimiento mediante el almacén de consultas | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 11/28/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Query Store
- Query Store, described
ms.assetid: e06344a4-22a5-4c67-b6c6-a7060deb5de6
caps.latest.revision: 38
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 727d9ccd8cd1e40d89cfe74291edae92988b407c
ms.openlocfilehash: 4650cfdda4eef32d1d09f4d4407b61f964832b8d
ms.contentlocale: es-es
ms.lasthandoff: 06/23/2017

---
# <a name="monitoring-performance-by-using-the-query-store"></a>Supervisión del rendimiento mediante el almacén de consultas
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  La característica del Almacén de consultas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ofrece datos detallados sobre el rendimiento y la elección del plan de consultas. Esta característica simplifica la solución de problemas de rendimiento al permitirle encontrar rápidamente las diferencias de rendimiento provocadas por cambios en los planes de consulta. El Almacén de consultas captura automáticamente un historial de consultas, planes y estadísticas en tiempo de ejecución y las conserva para su revisión. Además, separa los datos por ventanas de tiempo, lo que permite ver patrones de uso de la base de datos y comprender cuándo se produjeron cambios del plan de consultas en el servidor. El almacén de consultas se puede configurar con la opción [ALTER DATABASE SET](../../t-sql/statements/alter-database-transact-sql-set-options.md) . 
  
 Para obtener más información sobre cómo funciona el almacén de consultas en Base de datos SQL de Azure, vea [Funcionamiento del almacén de consultas de Base de datos SQL de Azure](https://azure.microsoft.com/documentation/articles/sql-database-operate-query-store/).  
  
##  <a name="Enabling"></a> Enabling the Query Store  
 El Almacén de consultas no está activo para nuevas bases de datos de manera predeterminada.  
  
#### <a name="use-the-query-store-page-in-management-studio"></a>Uso de la página Almacén de consultas en Management Studio  
  
1.  En el Explorador de objetos, haga clic con el botón derecho en una base de datos y, luego, haga clic en **Propiedades**.  
  
    > [!NOTE]  
    >  Se requiere al menos la versión [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] de [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)].  
  
2.  En el cuadro de diálogo **Propiedades de la base de datos** , seleccione la página **Almacén de consultas** .  
  
3.  En el cuadro **Modo de operación (solicitado)** seleccione **Activado**.  
  
#### <a name="use-transact-sql-statements"></a>Uso de instrucciones Transact-SQL  
  
1.  Use la instrucción **ALTER DATABASE** para habilitar el almacén de consultas. Por ejemplo:  
  
    ```tsql  
    ALTER DATABASE AdventureWorks2012 SET QUERY_STORE = ON;  
    ```  
  
     Para obtener más opciones de sintaxis relacionadas con el almacén de consultas, vea [Opciones de ALTER DATABASE SET &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md).  
  
> [!NOTE]  
>  No se puede habilitar el almacén de consultas para la base de datos **master** o **tempdb** .  
 
##  <a name="About"></a> Información del Almacén de consultas  
 Los planes de ejecución para cualquier consulta específica en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] suelen evolucionar con el tiempo debido a una serie de motivos diferentes, como cambios en las estadísticas, cambios de esquema, creación o eliminación de los índices, etc. La caché de procedimientos (donde se almacenan los planes de consulta almacenados en caché) solo almacena el plan de ejecución más reciente. Los planes también se eliminan de la caché de planes debido a la presión de memoria. Como resultado, es posible que las regresiones de rendimiento de consultas provocadas por los cambios de planes de ejecución no sean triviales y que su resolución lleve mucho tiempo.  
  
 Como el almacén de consultas conserva varios planes de ejecución por consulta, puede aplicar directivas para dirigir el procesador de consultas para que use un plan de ejecución concreto para una consulta. Esto se conoce como forzado de plan. El forzado de plan en la consulta de almacenes se ofrece mediante un mecanismo similar al de la sugerencia de consulta [USE PLAN](../../t-sql/queries/hints-transact-sql-query.md) , pero no requiere ningún cambio en las aplicaciones de usuario. El plan de forzado puede resolver una regresión del rendimiento de consultas provocado por un cambio de plan en un período de tiempo muy breve.  
  
 Entre los escenarios comunes para usar la característica Almacén de consultas se encuentran:  
  
-   Buscar y corregir rápidamente una regresión de rendimiento de plan forzando el plan de consulta anterior. Corregir las consultas de las que se ha realizado regresión recientemente en el rendimiento debido a cambios del plan de ejecución.  
  
-   Determinar el número de veces en que se ha ejecutado una consulta en una ventana de tiempo determinado, ayudando a un DBA en la solución de problemas de rendimiento de recursos.  
  
-   Identificar las principales *n* consultas (por tiempo de ejecución, consumo de memoria, etc.) en las últimas *x* horas.  
  
-   Auditar el historial de planes de consulta para una consulta determinada.  
  
-   Analizar los patrones de uso (CPU, E/S y memoria) de recursos para una base de datos determinada.  
  
 El almacén de consultas contiene dos almacenes: un **almacén de planes** para conservar la información del plan de ejecución y un **almacén de estadísticas de tiempo de ejecución** para conservar la información de estadísticas de ejecución. El número de planes únicos que se pueden almacenar para una consulta en el almacén de planes se limita por la opción de configuración **max_plans_per_query** . Para mejorar el rendimiento, la información se escribe en los dos almacenes de forma asincrónica. Para minimizar el uso del espacio, se agregan las estadísticas de ejecución en tiempo de ejecución en el almacén de estadísticas de tiempo de ejecución en una ventana de tiempo fijo. La información de estos almacenes se puede ver al consultar las vistas del catálogo del almacén de consultas.  
  
 La siguiente consulta devuelve información sobre las consultas y los planes del almacén de consultas.  
  
```tsql  
SELECT Txt.query_text_id, Txt.query_sql_text, Pl.plan_id, Qry.*  
FROM sys.query_store_plan AS Pl  
JOIN sys.query_store_query AS Qry  
    ON Pl.query_id = Qry.query_id  
JOIN sys.query_store_query_text AS Txt  
    ON Qry.query_text_id = Txt.query_text_id ;  
```  
 
##  <a name="Regressed"></a> Use the Regressed Queries Feature  
 Después de habilitar el Almacén de consultas, actualice la parte de la base de datos del panel del Explorador de objetos para agregar la sección **Almacén de consultas** .  
  
 ![Árbol de almacenamiento de consultas en el Explorador de objetos](../../relational-databases/performance/media/objectexplorerquerystore.PNG "Árbol de almacenamiento de consultas en el Explorador de objetos")  
  
 Seleccione **Regressed Queries** (Consultas devueltas) para abrir el panel del mismo nombre **** en [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]. En el panel Regressed Queries (Consultas devueltas) se muestran las consultas y los planes del Almacén de consultas. Los cuadros desplegables de la parte superior le permiten seleccionar consultas en función de varios criterios. Seleccione un plan para ver el plan de consulta gráfica. Los botones están disponibles para ver la consulta de origen, aplicar y eliminar la aplicación de un plan de consulta, y actualizar la pantalla.  
  
 ![Consultas retomadas en el explorador de objetos](../../relational-databases/performance/media/objectexplorerregressedqueries.PNG "Consultas retomadas en el explorador de objetos")  
  
 Para aplicar un plan, seleccione una consulta y el plan y luego haga clic en **Force Plan**(Forzar plan). Solo puede forzar planes que se guardaron mediante la característica del plan de consulta y que todavía se conservan en la caché del plan de consulta.  
 
##  <a name="Options"></a> Configuration Options 

Tiene disponibles las siguientes opciones para configurar los parámetros del almacén de consultas.

 `OPERATION_MODE`  
 Puede ser READ_WRITE (valor predeterminado) o READ_ONLY.  
  
 `CLEANUP_POLICY (STALE_QUERY_THRESHOLD_DAYS)`  
 Configure el argumento STALE_QUERY_THRESHOLD_DAYS para especificar el número de días en que se conservarán los datos en el almacén de consultas. El valor predeterminado es 30. En la edición básica de [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)] , el valor predeterminado es 7 días.
  
 `DATA_FLUSH_INTERVAL_SECONDS`  
 Determina la frecuencia con la que los datos escritos en el almacén de consultas se conservan en el disco. Para optimizar el rendimiento, los datos recopilados por el almacén de consultas se escriben de manera asincrónica en el disco. La frecuencia con la que se produce esta transferencia asincrónica se configura mediante DATA_FLUSH_INTERVAL_SECONDS. El valor predeterminado es 900 (15 minutos).  
  
 `MAX_STORAGE_SIZE_MB`  
 Configura el tamaño máximo del almacén de consultas. Si los datos del Almacén de consultas alcanzan el límite de MAX_STORAGE_SIZE_MB, el Almacén de consultas cambia automáticamente el estado de lectura-escritura a solo lectura y deja de recopilar datos nuevos.  El valor predeterminado es 100 Mb. Para la edición [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)] Premium, el valor predeterminado es 1 Gb y para la edición [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)] Basic, el valor predeterminado es 10 Mb.
  
 `INTERVAL_LENGTH_MINUTES`  
 Determina el intervalo de tiempo en el que se agregan los datos de estadísticas de ejecución en tiempo de ejecución al almacén de consultas. Para optimizar el uso del espacio, se agregan las estadísticas de ejecución en tiempo de ejecución en el almacén de estadísticas de tiempo de ejecución en una ventana de tiempo fijo. Esta ventana de tiempo fijo se configura mediante INTERVAL_LENGTH_MINUTES. El valor predeterminado es 60. 
  
 `SIZE_BASED_CLEANUP_MODE`  
 Controla si el proceso de limpieza se activará automáticamente cuando la cantidad total se acerque al tamaño máximo. Puede ser AUTO (valor predeterminado) u OFF.  
  
 `QUERY_CAPTURE_MODE`  
 Designa si el Almacén de consultas captura todas las consultas o las consultas pertinentes en función del consumo de recursos y el número de ejecuciones, o si deja de agregar nuevas consultas y solo realiza un seguimiento de las consultas actuales. Puede ser ALL (se capturan todas las consultas), AUTO (se omiten las consultas poco frecuentes y las consultas con una duración de compilación y ejecución insignificante) o NONE (se detiene la captura de nuevas consultas). El valor predeterminado en SQL Server 2016 es ALL, mientras que en Base de datos SQL de Azure es AUTO.
  
 `MAX_PLANS_PER_QUERY`  
 Entero que representa el número máximo de planes que se tienen para cada consulta. El valor predeterminado es 200.  
 
 `WAIT_STATS_CAPTURE_MODE`  
 Controla si el almacén de consultas captura espera información estadística. Puede ser OFF = 0 o en = 1 (valor predeterminado)  
 
 Consulte la vista **sys.database_query_store_options** para determinar las opciones actuales del almacén de consultas. Para obtener más información sobre los valores, vea [sys.database_query_store_options](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md).  
  
 Para obtener más información sobre el establecimiento de opciones mediante instrucciones [!INCLUDE[tsql](../../includes/tsql-md.md)] , vea [Administración de opciones](#OptionMgmt).  
  
##  <a name="Related"></a> Related Views, Functions, and Procedures  
 El Almacén de consultas se puede ver y administrar a través de [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] o usando las siguientes vistas y procedimientos.  

||| 
|-|-|  
|[sys.fn_stmt_sql_handle_from_sql_stmt &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-stmt-sql-handle-from-sql-stmt-transact-sql.md)|| 
  
### <a name="query-store-catalog-views"></a>Vistas de catálogo del almacén de consultas  
 Las vistas de catálogo presentan información sobre el Almacén de consultas.  

||| 
|-|-|  
|[sys.database_query_store_options &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md)|[sys.query_context_settings &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-context-settings-transact-sql.md)|  
|[sys.query_store_plan &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-plan-transact-sql.md)|[sys.query_store_query &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-query-transact-sql.md)|  
|[sys.query_store_query_text &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-query-text-transact-sql.md)|[sys.query_store_runtime_stats &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-transact-sql.md)|  
|[Sys.query_store_wait_stats &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-query-store-wait-stats-transact-sql.md)|[sys.query_store_runtime_stats_interval &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-interval-transact-sql.md)|  
  
### <a name="query-store-stored-procedures"></a>Procedimientos almacenados del almacén de consultas  
 Los procedimientos almacenados configuran el Almacén de consultas.  

||| 
|-|-|  
|[sp_query_store_flush_db &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-query-store-flush-db-transact-sql.md)|[sp_query_store_reset_exec_stats &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-query-store-reset-exec-stats-transact-sql.md)|  
|[sp_query_store_force_plan &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-query-store-force-plan-transact-sql.md)|[sp_query_store_unforce_plan &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-query-store-unforce-plan-transact-sql.md)|  
|[sp_query_store_remove_plan &#40;Transct-SQL&#41;](../../relational-databases/system-stored-procedures/sp-query-store-remove-plan-transct-sql.md)|[sp_query_store_remove_query &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-query-store-remove-query-transact-sql.md)|  
 
##  <a name="Scenarios"></a> Escenarios de uso clave  
  
###  <a name="OptionMgmt"></a> Option Management  
 En esta sección se ofrecen algunas directrices sobre la administración de la propia característica Almacén de consultas.  
  
 **¿Está el Almacén de consultas activo actualmente?**  
  
 El Almacén de consultas almacena sus datos dentro de la base de datos del usuario y ese es el motivo por el que tiene limitado el tamaño (configurado con `MAX_STORAGE_SIZE_MB`). Si los datos del Almacén de consultas alcanzan ese límite, el Almacén de consultas cambiará automáticamente el estado de lectura-escritura a solo lectura y dejará de recopilar datos nuevos.  
  
 Ejecute la consulta [sys.database_query_store_options](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md) para saber si el almacén de consultas está activo actualmente y si está recopilando estadísticas en tiempo de ejecución o no.  
  
```tsql  
SELECT actual_state, actual_state_desc, readonly_reason,   
    current_storage_size_mb, max_storage_size_mb  
FROM sys.database_query_store_options;  
```  
  
 El estado del Almacén de consultas viene determinado por la columna actual_state. Si es diferente al estado deseado, la columna `readonly_reason` puede proporcionar más información.   
Cuando el tamaño del Almacén de consultas supera la cuota, la característica cambiará al modo de readon_only.  
  
 **Obtener opciones del Almacén de consultas**  
  
 Para averiguar información detallada sobre el estado del Almacén de consultas, ejecute lo siguiente en una base de datos de usuario.  
  
```tsql  
SELECT * FROM sys.database_query_store_options;  
```  
  
 **Establecimiento del intervalo del Almacén de consultas**  
  
 Puede invalidar el intervalo para agregar estadísticas de tiempo de ejecución de consultas (el valor predeterminado es 60 minutos).  
  
```tsql  
ALTER DATABASE <database_name>   
SET QUERY_STORE (INTERVAL_LENGTH_MINUTES = 15);  
```  
  
 > [!NOTE]
 > No se admiten valores arbitrarios para `INTERVAL_LENGTH_MINUTES`. Use una de las siguientes opciones: 1, 5, 10, 15, 30, 60 o 1440 minutos.  
  
 El nuevo valor de intervalo se expone a través de la vista **sys.database_query_store_options** .  
  
 **Uso de espacio en el Almacén de consultas**  
  
 El límite y el tamaño del Almacén de consultas se pueden comprobar con la siguiente instrucción en la base de datos de usuario.  
  
```tsql  
SELECT current_storage_size_mb, max_storage_size_mb   
FROM sys.database_query_store_options;  
```  
  
 Si el almacenamiento del Almacén de consultas está completamente lleno, use la siguiente instrucción para ampliar el almacenamiento.  
  
```tsql  
ALTER DATABASE <database_name>   
SET QUERY_STORE (MAX_STORAGE_SIZE_MB = <new_size>);  
```  
  
 **Establecer todas las opciones del Almacén de consultas**  
  
 Puede establecer varias opciones del Almacén de consultas a la vez con una sola instrucción ALTER DATABASE.  
  
```tsql  
ALTER DATABASE <database name>   
SET QUERY_STORE (  
    OPERATION_MODE = READ_WRITE,  
    CLEANUP_POLICY = (STALE_QUERY_THRESHOLD_DAYS = 30),  
    DATA_FLUSH_INTERVAL_SECONDS = 3000,  
    MAX_STORAGE_SIZE_MB = 500,  
    INTERVAL_LENGTH_MINUTES = 15,  
    SIZE_BASED_CLEANUP_MODE = AUTO,  
    QUERY_CAPTURE_MODE = AUTO,  
    MAX_PLANS_PER_QUERY = 1000  
);  
```  
  
 **Limpieza del espacio**  
  
 Las tablas internas del Almacén de consultas se crean en el grupo de archivos PRIMARY durante la creación de la base de datos y esa configuración no se podrá cambiar más adelante. Si se está quedando sin espacio, puede que quiera borrar los datos más antiguos del Almacén de consultas con la siguiente instrucción.  
  
```tsql  
ALTER DATABASE <db_name> SET QUERY_STORE CLEAR;  
```  
  
 Como alternativa, puede que quiera borrar solo datos de consultas ad hoc, porque resulta menos relevantes para optimizaciones de consultas y análisis de plan, pero ocupa el mismo espacio.  
  
 **Eliminar consultas ad hoc** Se eliminan las consultas que solo se ejecutaron una vez y que tienen más de 24 horas de antigüedad.  
  
```tsql  
DECLARE @id int  
DECLARE adhoc_queries_cursor CURSOR   
FOR   
SELECT q.query_id  
FROM sys.query_store_query_text AS qt  
JOIN sys.query_store_query AS q   
    ON q.query_text_id = qt.query_text_id  
JOIN sys.query_store_plan AS p   
    ON p.query_id = q.query_id  
JOIN sys.query_store_runtime_stats AS rs   
    ON rs.plan_id = p.plan_id  
GROUP BY q.query_id  
HAVING SUM(rs.count_executions) < 2   
AND MAX(rs.last_execution_time) < DATEADD (hour, -24, GETUTCDATE())  
ORDER BY q.query_id ;  
  
OPEN adhoc_queries_cursor ;  
FETCH NEXT FROM adhoc_queries_cursor INTO @id;  
WHILE @@fetch_status = 0  
    BEGIN   
        PRINT @id  
        EXEC sp_query_store_remove_query @id  
        FETCH NEXT FROM adhoc_queries_cursor INTO @id  
    END   
CLOSE adhoc_queries_cursor ;  
DEALLOCATE adhoc_queries_cursor;  
```  
  
 Puede definir su propio procedimiento con una lógica diferente para borrar los datos que ya no necesite.  
  
 En el ejemplo anterior se usa el procedimiento almacenado extendido **sp_query_store_remove_query** para quitar datos innecesarios. También se puede usar:  
  
-   **sp_query_store_reset_exec_stats** : para borrar las estadísticas de tiempo de ejecución de un plan determinado.  
  
-   **sp_query_store_remove_plan** : para quitar un único plan.  
 
  
###  <a name="Peformance"></a> Performance Auditing and Troubleshooting  
 El Almacén de consultas mantiene un historial de las métricas de compilación y tiempo de ejecución en todas las ejecuciones de consulta, lo que le permite realizar preguntas sobre la carga de trabajo.  
  
 **¿Últimas *n* consultas ejecutadas en la base de datos?**  
  
```tsql  
SELECT TOP 10 qt.query_sql_text, q.query_id,   
    qt.query_text_id, p.plan_id, rs.last_execution_time  
FROM sys.query_store_query_text AS qt   
JOIN sys.query_store_query AS q   
    ON qt.query_text_id = q.query_text_id   
JOIN sys.query_store_plan AS p   
    ON q.query_id = p.query_id   
JOIN sys.query_store_runtime_stats AS rs   
    ON p.plan_id = rs.plan_id  
ORDER BY rs.last_execution_time DESC;  
```  
  
 **¿Número de ejecuciones de cada consulta?**  
  
```tsql  
SELECT q.query_id, qt.query_text_id, qt.query_sql_text,   
    SUM(rs.count_executions) AS total_execution_count  
FROM sys.query_store_query_text AS qt   
JOIN sys.query_store_query AS q   
    ON qt.query_text_id = q.query_text_id   
JOIN sys.query_store_plan AS p   
    ON q.query_id = p.query_id   
JOIN sys.query_store_runtime_stats AS rs   
    ON p.plan_id = rs.plan_id  
GROUP BY q.query_id, qt.query_text_id, qt.query_sql_text  
ORDER BY total_execution_count DESC;  
```  
  
 **¿El número de consultas con el mayor tiempo medio de ejecución durante la última hora?**  
  
```tsql  
SELECT TOP 10 rs.avg_duration, qt.query_sql_text, q.query_id,  
    qt.query_text_id, p.plan_id, GETUTCDATE() AS CurrentUTCTime,   
    rs.last_execution_time   
FROM sys.query_store_query_text AS qt   
JOIN sys.query_store_query AS q   
    ON qt.query_text_id = q.query_text_id   
JOIN sys.query_store_plan AS p   
    ON q.query_id = p.query_id   
JOIN sys.query_store_runtime_stats AS rs   
    ON p.plan_id = rs.plan_id  
WHERE rs.last_execution_time > DATEADD(hour, -1, GETUTCDATE())  
ORDER BY rs.avg_duration DESC;  
```  
  
 **¿El número de consultas que han tenido la media máxima de lecturas de E/S físicas durante las últimas 24 horas, con la correspondiente media del número de filas y el número de ejecuciones?**  
  
```tsql  
SELECT TOP 10 rs.avg_physical_io_reads, qt.query_sql_text,   
    q.query_id, qt.query_text_id, p.plan_id, rs.runtime_stats_id,   
    rsi.start_time, rsi.end_time, rs.avg_rowcount, rs.count_executions  
FROM sys.query_store_query_text AS qt   
JOIN sys.query_store_query AS q   
    ON qt.query_text_id = q.query_text_id   
JOIN sys.query_store_plan AS p   
    ON q.query_id = p.query_id   
JOIN sys.query_store_runtime_stats AS rs   
    ON p.plan_id = rs.plan_id   
JOIN sys.query_store_runtime_stats_interval AS rsi   
    ON rsi.runtime_stats_interval_id = rs.runtime_stats_interval_id  
WHERE rsi.start_time >= DATEADD(hour, -24, GETUTCDATE())   
ORDER BY rs.avg_physical_io_reads DESC;  
```  
  
 **¿Consultas con varios planes?** Estas consultas son especialmente interesantes porque son candidatas para las regresiones debido al cambio de elección del plan. La siguiente consulta identifica estas consultas junto con todos los planes:  
  
```tsql  
WITH Query_MultPlans  
AS  
(  
SELECT COUNT(*) AS cnt, q.query_id   
FROM sys.query_store_query_text AS qt  
JOIN sys.query_store_query AS q  
    ON qt.query_text_id = q.query_text_id  
JOIN sys.query_store_plan AS p  
    ON p.query_id = q.query_id  
GROUP BY q.query_id  
HAVING COUNT(distinct plan_id) > 1  
)  
  
SELECT q.query_id, object_name(object_id) AS ContainingObject,   
    query_sql_text, plan_id, p.query_plan AS plan_xml,  
    p.last_compile_start_time, p.last_execution_time  
FROM Query_MultPlans AS qm  
JOIN sys.query_store_query AS q  
    ON qm.query_id = q.query_id  
JOIN sys.query_store_plan AS p  
    ON q.query_id = p.query_id  
JOIN sys.query_store_query_text qt   
    ON qt.query_text_id = q.query_text_id  
ORDER BY query_id, plan_id;  
```  
  
 **¿Consultas que se han devuelto recientemente por motivo de rendimiento (en comparación con otro momento dado)?** El siguiente ejemplo de consulta devuelve todas las consultas para las que se duplicó el tiempo de ejecución en las últimas 48 horas debido a un cambio de elección del plan. La consulta compara todos los intervalos de estadísticas en tiempo de ejecución en paralelo.  
  
```tsql  
SELECT   
    qt.query_sql_text,   
    q.query_id,   
    qt.query_text_id,   
    rs1.runtime_stats_id AS runtime_stats_id_1,  
    rsi1.start_time AS interval_1,   
    p1.plan_id AS plan_1,   
    rs1.avg_duration AS avg_duration_1,   
    rs2.avg_duration AS avg_duration_2,  
    p2.plan_id AS plan_2,   
    rsi2.start_time AS interval_2,   
    rs2.runtime_stats_id AS runtime_stats_id_2  
FROM sys.query_store_query_text AS qt   
JOIN sys.query_store_query AS q   
    ON qt.query_text_id = q.query_text_id   
JOIN sys.query_store_plan AS p1   
    ON q.query_id = p1.query_id   
JOIN sys.query_store_runtime_stats AS rs1   
    ON p1.plan_id = rs1.plan_id   
JOIN sys.query_store_runtime_stats_interval AS rsi1   
    ON rsi1.runtime_stats_interval_id = rs1.runtime_stats_interval_id   
JOIN sys.query_store_plan AS p2   
    ON q.query_id = p2.query_id   
JOIN sys.query_store_runtime_stats AS rs2   
    ON p2.plan_id = rs2.plan_id   
JOIN sys.query_store_runtime_stats_interval AS rsi2   
    ON rsi2.runtime_stats_interval_id = rs2.runtime_stats_interval_id  
WHERE rsi1.start_time > DATEADD(hour, -48, GETUTCDATE())   
    AND rsi2.start_time > rsi1.start_time   
    AND p1.plan_id <> p2.plan_id  
    AND rs2.avg_duration > 2*rs1.avg_duration  
ORDER BY q.query_id, rsi1.start_time, rsi2.start_time;  
```  
  
 Si quiere ver el rendimiento de todas las regresiones (no solo de aquellas relacionadas con el cambio de elección de plan), solo tiene que eliminar la condición `AND p1.plan_id <> p2.plan_id` de la consulta anterior.  
  
 **¿Consultas que se han devuelto recientemente por motivo de rendimiento (comparando la ejecución de las recientes con las del historial)?** La siguiente consulta compara períodos de ejecución basados en ejecución de consultas. En este ejemplo concreto, la consulta compara la ejecución en el período reciente (1 hora) con el período del historial (último día) e identifica las que han especificado `additional_duration_workload`. Esta métrica se calcula como una diferencia entre la media de las ejecuciones recientes y la media de las ejecuciones del historial multiplicada por el número de ejecuciones recientes. En realidad representa la cantidad de ejecuciones recientes de duración adicional introducidas en comparación con el historial:  
  
```tsql  
--- "Recent" workload - last 1 hour  
DECLARE @recent_start_time datetimeoffset;  
DECLARE @recent_end_time datetimeoffset;  
SET @recent_start_time = DATEADD(hour, -1, SYSUTCDATETIME());  
SET @recent_end_time = SYSUTCDATETIME();  
  
--- "History" workload  
DECLARE @history_start_time datetimeoffset;  
DECLARE @history_end_time datetimeoffset;  
SET @history_start_time = DATEADD(hour, -24, SYSUTCDATETIME());  
SET @history_end_time = SYSUTCDATETIME();  
  
WITH  
hist AS  
(  
    SELECT   
        p.query_id query_id,   
        CONVERT(float, SUM(rs.avg_duration*rs.count_executions)) total_duration,   
        SUM(rs.count_executions) count_executions,  
        COUNT(distinct p.plan_id) num_plans   
     FROM sys.query_store_runtime_stats AS rs  
        JOIN sys.query_store_plan p ON p.plan_id = rs.plan_id  
    WHERE  (rs.first_execution_time >= @history_start_time   
               AND rs.last_execution_time < @history_end_time)  
        OR (rs.first_execution_time \<= @history_start_time   
               AND rs.last_execution_time > @history_start_time)  
        OR (rs.first_execution_time \<= @history_end_time   
               AND rs.last_execution_time > @history_end_time)  
    GROUP BY p.query_id  
),  
recent AS  
(  
    SELECT   
        p.query_id query_id,   
        CONVERT(float, SUM(rs.avg_duration*rs.count_executions)) total_duration,   
        SUM(rs.count_executions) count_executions,  
        COUNT(distinct p.plan_id) num_plans   
    FROM sys.query_store_runtime_stats AS rs  
        JOIN sys.query_store_plan p ON p.plan_id = rs.plan_id  
    WHERE  (rs.first_execution_time >= @recent_start_time   
               AND rs.last_execution_time < @recent_end_time)  
        OR (rs.first_execution_time \<= @recent_start_time   
               AND rs.last_execution_time > @recent_start_time)  
        OR (rs.first_execution_time \<= @recent_end_time   
               AND rs.last_execution_time > @recent_end_time)  
    GROUP BY p.query_id  
)  
SELECT   
    results.query_id query_id,  
    results.query_text query_text,  
    results.additional_duration_workload additional_duration_workload,  
    results.total_duration_recent total_duration_recent,  
    results.total_duration_hist total_duration_hist,  
    ISNULL(results.count_executions_recent, 0) count_executions_recent,  
    ISNULL(results.count_executions_hist, 0) count_executions_hist   
FROM  
(  
    SELECT  
        hist.query_id query_id,  
        qt.query_sql_text query_text,  
        ROUND(CONVERT(float, recent.total_duration/  
                   recent.count_executions-hist.total_duration/hist.count_executions)  
               *(recent.count_executions), 2) AS additional_duration_workload,  
        ROUND(recent.total_duration, 2) total_duration_recent,   
        ROUND(hist.total_duration, 2) total_duration_hist,  
        recent.count_executions count_executions_recent,  
        hist.count_executions count_executions_hist     
    FROM hist   
        JOIN recent   
            ON hist.query_id = recent.query_id   
        JOIN sys.query_store_query AS q   
            ON q.query_id = hist.query_id  
        JOIN sys.query_store_query_text AS qt   
            ON q.query_text_id = qt.query_text_id      
) AS results  
WHERE additional_duration_workload > 0  
ORDER BY additional_duration_workload DESC  
OPTION (MERGE JOIN);  
```  
 
  
###  <a name="Stability"></a> Maintaining Query Performance Stability  
 En las consultas ejecutadas varias veces, puede observar que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa diferentes planes que han generado diferente duración y uso de los recursos. Con el Almacén de consultas puede detectar cuándo se ha devuelto el rendimiento de las consultas y determinar el plan óptimo en un período de interés. Luego puede forzar ese plan óptimo para futuras ejecuciones de consultas.  
  
 También puede identificar el rendimiento incoherente de las consultas para una consulta con parámetros (ya sea con parámetros automáticos o con parámetros manuales). Entre los distintos planes puede identificar el plan que es lo suficientemente rápido y óptimo para todos o la mayoría de los valores de parámetros y forzar ese plan, manteniendo un rendimiento predecible para el conjunto más amplio de escenarios de usuario.  
  
 **Forzar o planear una consulta (aplicar directiva de forzado).** Cuando se fuerza un plan para una determinada consulta, cada vez que una consulta entra en ejecución, se ejecutará con el plan que se fuerza.  
  
```tsql  
EXEC sp_query_store_force_plan @query_id = 48, @plan_id = 49;  
```  
  
 Al usar **sp_query_store_force_plan** solo puede forzar los planes que se grabaron por el almacén de consultas como un plan para esa consulta. Es decir, los únicos planes disponibles para una consulta son aquellos que ya se han usado para ejecutar la consulta mientras el Almacén de consultas estaba activo.  
  
 **Quitar el forzado de un plan para una consulta.** Para volver a confiar en el optimizador de consultas [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para calcular el plan de consulta óptimo, use **sp_query_store_unforce_plan** para eliminar la aplicación del plan que se seleccionó para la consulta.  
  
```tsql  
EXEC sp_query_store_unforce_plan @query_id = 48, @plan_id = 49;  
```  
  
## <a name="see-also"></a>Vea también  
 [Procedimiento recomendado con el Almacén de consultas](../../relational-databases/performance/best-practice-with-the-query-store.md)   
 [Uso del almacén de consultas con OLTP en memoria](../../relational-databases/performance/using-the-query-store-with-in-memory-oltp.md)   
 [Escenarios de uso del Almacén de consultas](../../relational-databases/performance/query-store-usage-scenarios.md)   
 [Introducción a la recopilación de datos del almacén de consultas](../../relational-databases/performance/how-query-store-collects-data.md)   
 [Query Store Stored Procedures &#40;Transact-SQL&#41; (Procedimientos almacenados del Almacén de consultas &#40;Transact-SQL&#41;)](../../relational-databases/system-stored-procedures/query-store-stored-procedures-transact-sql.md)   
 [Query Store Catalog Views &#40;Transact-SQL&#41; (Vistas de catálogo del Almacén de consultas &#40;Transact-SQL&#41;)](../../relational-databases/system-catalog-views/query-store-catalog-views-transact-sql.md)   
 [Supervisar y optimizar el rendimiento](../../relational-databases/performance/monitor-and-tune-for-performance.md)   
 [Herramientas de supervisión y optimización del rendimiento](../../relational-databases/performance/performance-monitoring-and-tuning-tools.md)   
 [Abrir el Monitor de actividad &#40;SQL Server Management Studio&#41;](../../relational-databases/performance-monitor/open-activity-monitor-sql-server-management-studio.md)   
 [Estadísticas de consultas activas](../../relational-databases/performance/live-query-statistics.md)   
 [Monitor de actividad](../../relational-databases/performance-monitor/activity-monitor.md)   
 [sys.database_query_store_options &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md)  
 [Funcionamiento del almacén de consultas de Azure SQL Database](https://azure.microsoft.com/documentation/articles/sql-database-operate-query-store/) 
  

