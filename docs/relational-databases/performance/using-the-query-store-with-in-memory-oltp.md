---
title: Uso del almacén de consultas con OLTP en memoria | Microsoft Docs
ms.custom: ''
ms.date: 03/29/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Query Store, in-memory
ms.assetid: aae5ae6d-7c90-4661-a1c5-df704319888a
author: julieMSFT
ms.author: jrasnick
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: db274ccde27abf92617e0eadf95b1971e740705a
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "72251296"
---
# <a name="using-the-query-store-with-in-memory-oltp"></a>Uso del almacén de consultas con OLTP en memoria
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] El almacén de consultas permite supervisar el rendimiento del código compilado de forma nativa para cargas de trabajo que ejecuten OLTP en memoria.  
Las estadísticas de compilación y de runtime se recopilan y exponen de la misma manera que en el caso de cargas de trabajo basadas en disco.   
Al migrar a OLTP en memoria, podrá seguir usando las vistas del almacén de consultas en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] , así como los scripts personalizados que haya desarrollado para cargas de trabajo basadas en disco antes de la migración. De este modo, no habrá desperdiciado el tiempo invertido en familiarizarse con la tecnología del almacén de consultas y podrá usarlo de forma más generalizada para solucionar problemas de todos los tipos de cargas de trabajo.  
Para obtener información general sobre cómo utilizar el almacén de consultas, consulte [Monitoring Performance By Using the Query Store](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md).  
  
 Para usar el almacén de consultas con OLTP en memoria, no hay que configurar ninguna característica adicional. Una vez que lo habilite en la base de datos, funcionará para todos los tipos de cargas de trabajo.   
Sin embargo, existen algunos aspectos específicos que los usuarios deben tener en cuenta a la hora de utilizar el almacén de consultas con OLTP en memoria:  
  
-   Cuando se habilita el almacén de consultas, se recopilan de manera predeterminada las consultas, los planes y las estadísticas de tiempo de compilación. Pero no se activa la recopilación de estadísticas de runtime, a menos que la habilite explícitamente con [sys.sp_xtp_control_query_exec_stats &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-xtp-control-query-exec-stats-transact-sql.md).  
  
-   Al establecer *\@new_collection_value* en 0, el almacén de consultas dejará de recopilar estadísticas en tiempo de ejecución para el procedimiento afectado o para toda la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   El valor configurado con [sys.sp_xtp_control_query_exec_stats &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-xtp-control-query-exec-stats-transact-sql.md) no se conserva. Asegúrese de comprobar y volver a configurar la recopilación de estadísticas después de reiniciar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   Como sucede con la recopilación de estadísticas de consulta habitual, el rendimiento puede disminuir si se utiliza el almacén de consultas para efectuar un seguimiento de la ejecución de la carga de trabajo. Habilitar la recopilación de estadísticas únicamente para un subconjunto importante de procedimientos almacenados compilados de forma nativa supone una buena idea.  
  
-   Las consultas y los planes se capturan y almacenan en la primera compilación nativa y se actualizan con cada recompilación.  
  
-   Si ha habilitado el almacén de consulta o borrado su contenido después de que se compilaran todos los procedimientos almacenados nativos, tendrá que volver a compilarlos manualmente para que el almacén de consultas pueda capturarlos. Esto es igualmente válido si ha quitado consultas manualmente con [sp_query_store_remove_query &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-query-store-remove-query-transact-sql.md) o [sp_query_store_remove_plan &#40;Transct-SQL&#41;](../../relational-databases/system-stored-procedures/sp-query-store-remove-plan-transct-sql.md). Use [sp_recompile &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-recompile-transact-sql.md) para forzar la recompilación del procedimiento.  
  
-   El almacén de consultas aprovecha mecanismos de generación de planes de OLTP en memoria para capturar el plan de ejecución de la consulta durante la compilación. El plan almacenado es equivalente, desde el punto de vista semántico, al que obtendría usando `SET SHOWPLAN_XML ON` ; con una diferencia: los planes del almacén de consultas se dividen y almacenan por cada instrucción individual.  
    
-   Si ejecuta un almacén de consultas en una base de datos con una carga de trabajo mixta, podrá usar el campo **is_natively_compiled** de [sys.query_store_plan &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-plan-transact-sql.md) para encontrar rápidamente los planes de consulta que haya generado la compilación de código nativa.  
  
-   El modo de captura del almacén de consultas no (el parámetro*QUERY_CAPTURE_MODE* de la instrucción **ALTER TABLE** ) no afecta a las consultas de módulos compilados de forma nativa, ya que estas se capturan siempre, con independencia del valor configurado. Esto incluye la opción `QUERY_CAPTURE_MODE = NONE`.  
  
-   En la duración de la compilación de la consulta que captura el almacén de consultas se incluye únicamente el tiempo dedicado a la optimización de la consulta, antes de la generación del código nativo. Más concretamente, no incluye el tiempo de compilación de código de C y la generación de las estructuras internas necesarias para la generación de código de C.  
  
-   Las métricas de concesiones de memoria dentro de [sys.query_store_runtime_stats &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-transact-sql.md) no se rellenan en las consultas compiladas de manera nativa; sus valores siempre son 0. Estas son las columnas de concesión de memoria: avg_query_max_used_memory, last_query_max_used_memory, min_query_max_used_memory, max_query_max_used_memory y stdev_query_max_used_memory.  
  
## <a name="enabling-and-using-query-store-with-in-memory-oltp"></a>Habilitación y uso del almacén de consultas con OLTP en memoria  
 En el ejemplo siguiente se demuestra el uso del almacén de consultas con OLTP en memoria en un escenario de usuario integral. En este ejemplo, se supone que una base de datos (`MemoryOLTP`) está habilitada para OLTP en memoria.  
    Para obtener más información sobre los requisitos previos de las tablas optimizadas para memoria, vea [Crear una tabla optimizada para memoria y un procedimiento almacenado compilado de forma nativa](../../relational-databases/in-memory-oltp/creating-a-memory-optimized-table-and-a-natively-compiled-stored-procedure.md).  
  
```  
USE MemoryOLTP;  
GO  
  
-- Create a simple memory-optimized table   
CREATE TABLE dbo.Ord  
   (OrdNo INTEGER not null PRIMARY KEY NONCLUSTERED,   
    OrdDate DATETIME not null,   
    CustCode NVARCHAR(5) not null)   
WITH (MEMORY_OPTIMIZED=ON);  
GO  
  
-- Enable Query Store before native module compilation  
ALTER DATABASE MemoryOLTP SET QUERY_STORE = ON;  
GO  
  
-- Create natively compiled stored procedure  
CREATE PROCEDURE dbo.OrderInsert(@OrdNo integer, @CustCode nvarchar(5))  
WITH NATIVE_COMPILATION, SCHEMABINDING  
AS   
    BEGIN ATOMIC WITH  
    (TRANSACTION ISOLATION LEVEL = SNAPSHOT,  
    LANGUAGE = N'English')  
  
    DECLARE @OrdDate DATETIME = GETDATE();  
    INSERT INTO dbo.Ord (OrdNo, CustCode, OrdDate)   
        VALUES (@OrdNo, @CustCode, @OrdDate);  
END;  
GO  
  
-- Enable runtime stats collection for queries from dbo.OrderInsert stored procedure  
DECLARE @db_id INT = DB_ID()  
DECLARE @proc_id INT = OBJECT_ID('dbo.OrderInsert');  
DECLARE @collection_enabled BIT;  
  
EXEC [sys].[sp_xtp_control_query_exec_stats] @new_collection_value = 1,   
    @database_id = @db_id, @xtp_object_id = @proc_id;  
  
-- Check the state of the collection flag  
EXEC sp_xtp_control_query_exec_stats @database_id = @db_id,   
    @xtp_object_id = @proc_id,   
    @old_collection_value= @collection_enabled output;  
SELECT @collection_enabled AS 'collection status';  
  
-- Execute natively compiled workload  
EXEC dbo.OrderInsert 1, 'A';  
EXEC dbo.OrderInsert 2, 'B';  
EXEC dbo.OrderInsert 3, 'C';  
EXEC dbo.OrderInsert 4, 'D';  
EXEC dbo.OrderInsert 5, 'E';  
  
-- Check Query Store Data  
-- Compile time data  
SELECT q.query_id, plan_id, object_id, query_hash, p.query_plan,  
    p.initial_compile_start_time, p.last_compile_start_time,   
    p.last_execution_time, p.avg_compile_duration,  
    p.last_force_failure_reason, p.force_failure_count  
FROM sys.query_store_query AS q  
JOIN sys.query_store_plan AS p   
    ON q.query_id = p.plan_id  
WHERE q.object_id = OBJECT_ID('dbo.OrderInsert');  
  
-- Get runtime stats  
-- Check count_executions field to verify that runtime statistics   
-- have been collected by the Query Store  
SELECT q.query_id, p.plan_id, object_id, rsi.start_time, rsi.end_time,    
    p.last_force_failure_reason, p.force_failure_count, rs.*  
FROM sys.query_store_query AS q  
JOIN sys.query_store_plan AS p   
    ON q.query_id = p.plan_id  
JOIN sys.query_store_runtime_stats AS rs   
    ON rs.plan_id = p.plan_id  
JOIN sys.query_store_runtime_stats_interval AS rsi   
    ON rs.runtime_stats_interval_id = rsi.runtime_stats_interval_id  
WHERE q.object_id = OBJECT_ID('dbo.OrderInsert');  
```  
  
## <a name="see-also"></a>Consulte también  
 [Monitoring Performance By Using the Query Store](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)   
 [Crear una tabla con optimización para memoria y un procedimiento almacenado compilado de forma nativa](../../relational-databases/in-memory-oltp/creating-a-memory-optimized-table-and-a-natively-compiled-stored-procedure.md)   
 [Procedimiento recomendado con el Almacén de consultas](../../relational-databases/performance/best-practice-with-the-query-store.md)   
 [Query Store Stored Procedures &#40;Transact-SQL&#41; (Procedimientos almacenados del Almacén de consultas &#40;Transact-SQL&#41;)](../../relational-databases/system-stored-procedures/query-store-stored-procedures-transact-sql.md)   
 [Query Store Catalog Views (Vistas de catálogo del almacén de consultas) &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/query-store-catalog-views-transact-sql.md)  
  
  
