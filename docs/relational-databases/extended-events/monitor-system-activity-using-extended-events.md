---
title: Supervisar la actividad del sistema mediante eventos extendidos
description: Use los eventos extendidos con el seguimiento de eventos para Windows a fin de supervisar la actividad del sistema. Obtenga información sobre CREATE EVENT SESSION, ALTER EVENT SESSION y DROP EVENT SESSION.
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xevents
ms.topic: tutorial
helpviewer_keywords:
- xe
- extended events [SQL Server], monitoring system activity
ms.assetid: d83ad88f-818c-49fe-a9a9-299f704fca53
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: b09dd7baae138fc559fd672ee43cad1761ca77c0
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/14/2020
ms.locfileid: "97481406"
---
# <a name="monitor-system-activity-using-extended-events"></a>Supervisar la actividad del sistema mediante eventos extendidos

[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]

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
    >  Para obtener ayuda sobre el comando **tracerpt** , escriba `tracerpt /?`en el símbolo del sistema.  
  
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
 [CREATE EVENT SESSION &#40;Transact-SQL&#41;](../../t-sql/statements/create-event-session-transact-sql.md)   
 [ALTER EVENT SESSION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-event-session-transact-sql.md)   
 [DROP EVENT SESSION &#40;Transact-SQL&#41;](../../t-sql/statements/drop-event-session-transact-sql.md)   
 [Vistas de catálogo de eventos extendidos &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/extended-events-catalog-views-transact-sql.md)   
 [Vistas de administración dinámica de eventos extendidos](../../relational-databases/system-dynamic-management-views/extended-events-dynamic-management-views.md)   
 [Destinos de SQL Server Extended Events](/previous-versions/sql/sql-server-2016/bb630339(v=sql.130))  
  
