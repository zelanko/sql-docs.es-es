---
title: Supervisión del rendimiento de los procedimientos almacenados compilados de forma nativa | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 55548cb2-77a8-4953-8b5a-f2778a4f13cf
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: fa8a92b3727bf4c06a5b5a85c8359f96b592cd44
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/13/2018
ms.locfileid: "53359757"
---
# <a name="monitoring-performance-of-natively-compiled-stored-procedures"></a>Supervisar el rendimiento de los procedimientos almacenados compilados de forma nativa
  En este tema se describe cómo supervisar el rendimiento de los procedimientos almacenados compilados de forma nativa.  
  
## <a name="using-extended-events"></a>Utilizar eventos extendidos  
 Utilice el evento extendido `sp_statement_completed` para realizar el seguimiento de la ejecución de una consulta. Cree una sesión de eventos extendidos con este evento, opcionalmente con un filtro en object_id para un procedimiento almacenado compilado de forma nativa específico. El evento extendido se genera tras la ejecución de cada consulta. El tiempo de CPU y la duración notificados por el evento extendido indican cuánta CPU utilizó la consulta y el tiempo de ejecución. Un procedimiento almacenado compilado de forma nativa que utiliza mucho tiempo de CPU puede tener problemas de rendimiento.  
  
 Se puede utilizar `line_number` junto con el `object_id` del evento extendido para investigar la consulta. La siguiente consulta se puede utilizar para recuperar la definición del procedimiento. El número de línea se puede utilizar para identificar la consulta dentro de la definición:  
  
```tsql  
select [definition] from sys.sql_modules where object_id=object_id  
```  
  
 Para obtener más información sobre la `sp_statement_completed` evento extendido, vea [cómo recuperar la instrucción que produjo un evento](https://blogs.msdn.com/b/extended_events/archive/2010/05/07/making-a-statement-how-to-retrieve-the-t-sql-statement-that-caused-an-event.aspx).  
  
## <a name="using-data-management-views"></a>Utilizar vistas de administración de datos  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] admite la recopilación de estadísticas de ejecución para los procedimientos almacenados compilados de forma nativa, tanto en el nivel de procedimiento como en el nivel de consulta. La recopilación de estadísticas de ejecución no está habilitada de forma predeterminada debido al impacto que tiene sobre el rendimiento.  
  
 Puede habilitar y deshabilitar la recopilación de estadísticas en los procedimientos almacenados compilados de forma nativa con [sys.sp_xtp_control_proc_exec_stats &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sys-sp-xtp-control-proc-exec-stats-transact-sql).  
  
 Cuando está habilitada la recopilación de estadísticas con [sys.sp_xtp_control_proc_exec_stats &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sys-sp-xtp-control-proc-exec-stats-transact-sql), puede usar [sys.dm_exec_procedure_stats &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-exec-procedure-stats-transact-sql) para supervisar el rendimiento de un procedimiento almacenado compilado de forma nativa.  
  
 Cuando está habilitada la recopilación de estadísticas con [sys.sp_xtp_control_query_exec_stats &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sys-sp-xtp-control-query-exec-stats-transact-sql), puede usar [sys.dm_exec_query_stats &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql) para supervisar el rendimiento de un procedimiento almacenado compilado de forma nativa.  
  
 Al inicio de la recopilación, habilite la recopilación de estadísticas. Después, ejecute el procedimiento almacenado compilado de forma nativa. Al final de la recopilación, deshabilite la recopilación de estadísticas. A continuación, analice las estadísticas de ejecución devueltas por las DMV.  
  
 Después de recopilar las estadísticas, se pueden consultar las estadísticas de ejecución de los procedimientos almacenados compilados de forma nativa de un procedimiento con [sys.dm_exec_procedure_stats &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-exec-procedure-stats-transact-sql) y de las consultas con [sys.dm_exec_query_stats &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql).  
  
> [!NOTE]  
>  En los procedimientos almacenados compilados de forma nativa, cuando la recopilación de estadísticas está habilitada, el tiempo de trabajo se recopila en milisegundos. Si la consulta se ejecuta en menos de un milisegundo, el valor será 0. Para los procedimientos almacenados compilados de forma nativa, **total_worker_time** puede no ser exacto si varias ejecuciones tardan menos de 1 milisegundo.  
  
 La consulta siguiente devuelve los nombres de los procedimientos y las estadísticas de ejecución para los procedimientos almacenados compilados de forma nativa de la base de datos actual, después de la recopilación de estadísticas:  
  
```tsql  
select object_id,  
       object_name(object_id) as 'object name',  
       cached_time,  
       last_execution_time,  
       execution_count,  
       total_worker_time,  
       last_worker_time,  
       min_worker_time,  
       max_worker_time,  
       total_elapsed_time,  
       last_elapsed_time,  
       min_elapsed_time,  
       max_elapsed_time   
from sys.dm_exec_procedure_stats  
where database_id=db_id() and object_id in (select object_id   
from sys.sql_modules where uses_native_compilation=1)  
order by total_worker_time desc  
```  
  
 La consulta siguiente devuelve el texto de la consulta y las estadísticas de ejecución para todas las consultas de procedimientos almacenados compilados de forma nativa de la base de datos actual para la que se han recopilado estadísticas, ordenadas por tiempo total de trabajo, en orden descendente:  
  
```tsql  
select st.objectid,   
       object_name(st.objectid) as 'object name',   
       SUBSTRING(st.text, (qs.statement_start_offset/2) + 1, ((qs.statement_end_offset-qs.statement_start_offset)/2) + 1) as 'query text',   
       qs.creation_time,  
       qs.last_execution_time,  
       qs.execution_count,  
       qs.total_worker_time,  
       qs.last_worker_time,  
       qs.min_worker_time,  
       qs.max_worker_time,  
       qs.total_elapsed_time,  
       qs.last_elapsed_time,  
       qs.min_elapsed_time,  
       qs.max_elapsed_time  
from sys.dm_exec_query_stats qs cross apply sys.dm_exec_sql_text(sql_handle) st  
where  st.dbid=db_id() and st.objectid in (select object_id   
from sys.sql_modules where uses_native_compilation=1)  
order by qs.total_worker_time desc  
```  
  
 Los procedimientos almacenados compilados de forma nativa admiten SHOWPLAN_XML (plan de ejecución estimado). El plan de ejecución estimado se puede utilizar para inspeccionar el plan de consulta con el fin de detectar cualquier problema de plan incorrecto. Los motivos más frecuentes de los planes no válidos son:  
  
-   Las estadísticas no se actualizaron antes de que se creara el procedimiento.  
  
-   Faltan índices  
  
 Showplan XML se obtiene ejecutando la instrucción [!INCLUDE[tsql](../../includes/tsql-md.md)]siguiente:  
  
```tsql  
SET SHOWPLAN_XML ON  
GO  
EXEC my_proc   
GO  
SET SHOWPLAN_XML OFF  
GO  
```  
  
 O bien, en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], seleccione el nombre del procedimiento y haga clic en **Mostrar plan de ejecución estimado**.  
  
 El plan de ejecución estimado para los procedimientos almacenados compilados de forma nativa muestra los operadores y las expresiones de consulta para las consultas del procedimiento. [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] no admite todos los atributos SHOWPLAN_XML para los procedimientos almacenados compilados de forma nativa. Por ejemplo, los atributos relacionados con el costo del optimizador de consultas no forman parte de SHOWPLAN_XML para el procedimiento.  
  
## <a name="see-also"></a>Vea también  
 [Procedimientos almacenados compilados de forma nativa](natively-compiled-stored-procedures.md)  
  
  
