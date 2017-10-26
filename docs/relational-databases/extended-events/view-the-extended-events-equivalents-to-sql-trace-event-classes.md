---
title: Ver los eventos extendidos equivalentes a las clases de evento de Seguimiento de SQL | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
- xevents
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQL Trace, extended events equivalents
- extended events [SQL Server], SQL Trace equivalents
- extended events [SQL Server], user configurable events
ms.assetid: 7f24104c-201d-4361-9759-f78a27936011
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: HT
ms.sourcegitcommit: 54e4c8309c290255cb2885fab04bb394bc453046
ms.openlocfilehash: 008cdb3fc158b36793f7d4b42ee4b24fd2b56ea5
ms.contentlocale: es-es
ms.lasthandoff: 10/16/2017

---
# <a name="view-the-extended-events-equivalents-to-sql-trace-event-classes"></a>Ver los eventos extendidos equivalentes a las clases de evento de Seguimiento de SQL Server
[!INCLUDE[tsql-appliesto-ss2014-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2014-asdb-xxxx-xxx-md.md)]

  Si desea utilizar los eventos extendidos para recopilar datos de evento que son equivalentes a clases de eventos de Seguimiento de SQL y columnas, es útil saber cómo los eventos de Seguimiento de SQL se asignan a eventos y acciones de eventos extendidos.  
  
 Puede utilizar el procedimiento siguiente para ver los eventos y acciones de eventos extendidos que son equivalentes a cada evento de Seguimiento de SQL y sus columnas asociadas.  
  
## <a name="to-view-the-extended-events-equivalents-to-sql-trace-events-using-query-editor"></a>Para ver los equivalentes de eventos extendidos a los eventos de Seguimiento de SQL mediante el Editor de consultas  
  
-   En el Editor de consultas de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], ejecute la consulta siguiente:  
  
    ```  
    USE MASTER;  
    GO  
    SELECT DISTINCT  
       tb.trace_event_id,  
       te.name AS 'Event Class',  
       em.package_name AS 'Package',  
       em.xe_event_name AS 'XEvent Name',  
       tb.trace_column_id,  
       tc.name AS 'SQL Trace Column',  
       am.xe_action_name as 'Extended Events action'  
    FROM (sys.trace_events te LEFT OUTER JOIN sys.trace_xe_event_map em  
       ON te.trace_event_id = em.trace_event_id) LEFT OUTER JOIN sys.trace_event_bindings tb  
       ON em.trace_event_id = tb.trace_event_id LEFT OUTER JOIN sys.trace_columns tc  
       ON tb.trace_column_id = tc.trace_column_id LEFT OUTER JOIN sys.trace_xe_action_map am  
       ON tc.trace_column_id = am.trace_column_id  
    ORDER BY te.name, tc.name  
    ```  
  
 Cuando vea los resultados, tenga en cuenta lo siguiente:  
  
-   Si todas las columnas devuelven NULL a excepción de la columna Event Class, indica que la clase de eventos no se ha migrado desde el Seguimiento de SQL.  
  
-   Si solo el valor de la columna de acción Extended Events es NULL, indica que una de las siguientes condiciones es cierta:  
  
    -   La columna de Seguimiento de SQL se asigna a uno de los campos de datos asociado al evento de eventos extendidos.  
  
        > [!NOTE]  
        >  Cada evento de eventos extendidos tiene un conjunto predeterminado de campos de datos que se incluyen automáticamente en el conjunto de resultados.  
  
    -   La columna de acción no tiene un equivalente significativo de eventos extendidos. Un ejemplo de esto es la columna EventClass de Seguimiento de SQL. Esta columna no es necesaria en eventos extendidos porque el nombre del evento sirve para el mismo fin.  
  
-   Para las clases de eventos de Seguimiento de SQL configurables por el usuario (de UserConfigurable:1 a UserConfigurable:9), los eventos extendidos usan un solo evento para reemplazarlos. El evento se denomina user_event. Este evento se produce al usar sp_trace_generateevent, que es el mismo procedimiento almacenado usado por el Seguimiento de SQL. El evento user_event se devuelve independientemente del identificador de evento que se pase al procedimiento almacenado. Pero un campo event_id se devuelve como parte de los datos de evento. Esto permite generar un predicado basado en el identificador de evento. Por ejemplo, si usa UserConfigurable:0 (event_id = 82) en el código, puede agregar el evento user_event a la sesión y especificar un predicado de "event_id = 82". Por tanto, no tiene que cambiar el código porque el procedimiento almacenado sp_trace_generateevent genera el evento user_event de eventos extendidos y la clase de eventos de Seguimiento de SQL equivalente.  
  
## <a name="see-also"></a>Vea también  
 [sp_trace_generateevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-generateevent-transact-sql.md)  
  
  

