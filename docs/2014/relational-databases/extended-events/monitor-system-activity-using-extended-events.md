---
title: Supervisión de la actividad del sistema mediante eventos extendidos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xevents
ms.topic: conceptual
helpviewer_keywords:
- xe
- extended events [SQL Server], monitoring system activity
ms.assetid: d83ad88f-818c-49fe-a9a9-299f704fca53
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 0a15a6e9a04c64e6e277d37a86d8e6f198b81906
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/01/2020
ms.locfileid: "82706614"
---
# <a name="monitor-system-activity-using-extended-events"></a>Supervisar la actividad del sistema mediante eventos extendidos
  En el siguiente procedimiento se muestra el uso de Extended Events con el Seguimiento de eventos para Windows (ETW) para supervisar la actividad del sistema. El procedimiento también muestra el uso de las instrucciones CREATE EVENT SESSION, ALTER EVENT SESSION y DROP EVENT SESSION.  
  
 Para realizar estas tareas debe usar el Editor de consultas de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] y llevar a cabo el siguiente procedimiento. El procedimiento también utiliza el símbolo del sistema para ejecutar los comandos ETW.  
  
### <a name="to-monitor-system-activity-using-extended-events"></a>Para supervisar la actividad del sistema mediante Extended Events  
  
1.  En el Editor de consultas, emita las instrucciones siguientes para crear una sesión de eventos y agregar dos eventos. Estos eventos, checkpoint_begin y checkpoint_end, se activan al principio y al final de un punto de comprobación de la base de datos.  
  
    ```  
    CREATE EVENT SESSION test0  
    ON SERVER  
    ADD EVENT sqlserver.checkpoint_begin,  
    ADD EVENT sqlserver.checkpoint_end  
    WITH (MAX_DISPATCH_LATENCY = 1 SECONDS)  
    go  
    ```  
  
2.  Agregue el destino de creación de depósitos con 32 depósitos para contar el número de puntos de comprobación en función del identificador de base de datos.  
  
    ```  
    ALTER EVENT SESSION test0  
    ON SERVER  
    ADD TARGET package0.histogram  
    (  
          SET slots = 32, filtering_event_name = 'sqlserver.checkpoint_end', source_type = 0, source = 'database_id'  
    )  
    go  
    ```  
  
3.  Emita las instrucciones siguientes para agregar el destino ETW. Esto le permitirá ver los eventos inicial y final, utilizados para determinar el tiempo que tarda el punto de comprobación.  
  
    ```  
    ALTER EVENT SESSION test0  
    ON SERVER  
    ADD TARGET package0.etw_classic_sync_target  
    go  
    ```  
  
4.  Emita las instrucciones siguientes para iniciar la sesión y comenzar la recopilación de eventos.  
  
    ```  
    ALTER EVENT SESSION test0  
    ON SERVER  
    STATE = start  
    go  
    ```  
  
5.  Emita las instrucciones siguientes para activar tres eventos.  
  
    ```  
    USE tempdb  
          checkpoint  
    go  
    USE master  
          checkpoint  
          checkpoint  
    go  
    ```  
  
6.  Emita las instrucciones siguientes para ver los recuentos de eventos.  
  
    ```  
    SELECT CAST(xest.target_data AS xml) Bucketizer_Target_Data_in_XML  
    FROM sys.dm_xe_session_targets xest  
    JOIN sys.dm_xe_sessions xes ON xes.address = xest.event_session_address  
    JOIN sys.server_event_sessions ses ON xes.name = ses.name  
    WHERE xest.target_name = 'histogram' AND xes.name = 'test0'  
    go  
    ```  
  
7.  En el símbolo del sistema, ejecute los comandos siguientes para ver los datos ETW.  
  
    > [!NOTE]  
    >   Para obtener ayuda sobre el comando **tracerpt** , en el símbolo del sistema, escriba `tracerpt /?`.  
  
    ```  
    logman query -ets --- List the ETW sessions. This is optional.  
    logman update XE_DEFAULT_ETW_SESSION -fd -ets --- Flush the ETW log.  
    tracerpt %temp%\xeetw.etl -o xeetw.txt --- Dump the events so they can be seen.  
    ```  
  
8.  Emita las instrucciones siguientes para detener la sesión de eventos y quitarla del servidor.  
  
    ```  
    ALTER EVENT SESSION test0  
    ON SERVER  
    STATE = STOP  
    go  
  
    DROP EVENT SESSION test0  
    ON SERVER  
    go  
    ```  
  
## <a name="see-also"></a>Consulte también  
 [CREAR sesión de eventos &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-event-session-transact-sql)   
 [ALTER EVENT SESSION &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-event-session-transact-sql)   
 [DROP EVENT SESSION &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-event-session-transact-sql)   
 [Vistas de catálogo de eventos extendidos &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/extended-events-catalog-views-transact-sql)  
 [Vistas de administración dinámica de eventos extendidos](../views/views.md)   
 [Destinos de SQL Server Extended Events](../../database-engine/sql-server-extended-events-targets.md)  
  
  
