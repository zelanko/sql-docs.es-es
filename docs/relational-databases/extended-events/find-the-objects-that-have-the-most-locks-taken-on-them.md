---
title: Búsqueda de los objetos con más bloqueos mediante eventos extendidos
description: En este artículo se muestra cómo buscar los objetos que han obtenido más bloqueos. Es posible que los administradores de bases de datos tengan que buscar los objetos que han obtenido más bloqueos para mejorar el rendimiento de la base de datos.
ms.date: 10/18/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xevents
ms.topic: tutorial
helpviewer_keywords:
- objects [SQL Server], extended events
- xe
- extended events [SQL Server], locks
- objects [SQL Server], locks
ms.assetid: fcbadbda-c91c-43f0-a1b5-601e40110e07
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 522017d6ced6039cd7e5b9a30cf60404eee9249a
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/14/2020
ms.locfileid: "97465506"
---
# <a name="find-the-objects-that-have-the-most-locks-taken-on-them"></a>Buscar los objetos que han obtenido más bloqueos

[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]

A menudo, los administradores de bases de datos necesitan identificar el origen de bloqueos que reducen el rendimiento de la base de datos.  
  
Por ejemplo, suponga que está supervisando posibles cuellos de botella en el servidor de producción. Sospecha que podría haber recursos muy disputados y desearía saber cuántos bloqueos se han realizado en esos objetos. Una vez identificados los objetos que se bloquean con más con frecuencia, se pueden tomar medidas para optimizar el acceso a dichos objetos.  
  
Para ello, utilice el Editor de consultas de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
### <a name="to-find-the-objects-that-have-the-most-locks"></a>Para buscar los objetos que han obtenido más bloqueos  
  
1. En el Editor de consultas, emita las instrucciones siguientes.

    ```sql
    -- Find objects in a particular database that have the most
    -- lock acquired. This sample uses AdventureWorksDW2012.
    -- Create the session and add an event and target.
    
    IF EXISTS(SELECT * FROM sys.server_event_sessions WHERE name='LockCounts')
        DROP EVENT session LockCounts ON SERVER;
    GO
    DECLARE @dbid int;
  
    SELECT @dbid = db_id('AdventureWorksDW2012');
  
    DECLARE @sql nvarchar(1024);
    SET @sql = '
        CREATE event session LockCounts ON SERVER
            ADD EVENT sqlserver.lock_acquired (WHERE database_id ='
                + CAST(@dbid AS nvarchar) +')
            ADD TARGET package0.histogram(
                SET filtering_event_name=''sqlserver.lock_acquired'',
                    source_type=0, source=''resource_0'')';
  
    EXEC (@sql);
    GO
    ALTER EVENT session LockCounts ON SERVER
        STATE=start;
    GO
    -- Create a simple workload that takes locks.
    
    USE AdventureWorksDW2012;
    GO
    SELECT TOP 1 * FROM dbo.vAssocSeqLineItems;
    GO
    -- The histogram target output is available from the
    -- sys.dm_xe_session_targets dynamic management view in
    -- XML format.
    -- The following query joins the bucketizing target output with
    -- sys.objects to obtain the object names.
    
    SELECT name, object_id, lock_count
        FROM
        (
        SELECT objstats.value('.','bigint') AS lobject_id,
            objstats.value('@count', 'bigint') AS lock_count
            FROM (
                SELECT CAST(xest.target_data AS XML)
                    LockData
                FROM     sys.dm_xe_session_targets xest
                    JOIN sys.dm_xe_sessions        xes  ON xes.address = xest.event_session_address
                    JOIN sys.server_event_sessions ses  ON xes.name    = ses.name
                WHERE xest.target_name = 'histogram' AND xes.name = 'LockCounts'
                 ) Locks
            CROSS APPLY LockData.nodes('//HistogramTarget/Slot') AS T(objstats)
        ) LockedObjects
        INNER JOIN sys.objects o  ON LockedObjects.lobject_id = o.object_id
        WHERE o.type != 'S' AND o.type = 'U'
        ORDER BY lock_count desc;
    GO
    
    -- Stop the event session.
    
    ALTER EVENT SESSION LockCounts ON SERVER
        state=stop;
    GO
    ```

> [!NOTE]
> El ejemplo de código de Transact-SQL anterior se ejecuta en SQL Server local, pero es posible que _no se ejecute bien en Azure SQL Database._ Las partes principales del ejemplo que afectan directamente a los eventos, como `ADD EVENT sqlserver.lock_acquired`, funcionan también en Azure SQL Database. Sin embargo, los elementos preliminares, como `sys.server_event_sessions`, se deben editar en sus homólogos de Azure SQL Database, como `sys.database_event_sessions`, para que se ejecute el ejemplo.
> Para obtener más información acerca de estas pequeñas diferencias entre SQL Server local y Azure SQL Database, consulte los siguientes artículos:
> - [Eventos extendidos en Azure SQL Database](/azure/sql-database/sql-database-xevent-db-diff-from-svr#transact-sql-differences)
> - [Objetos del sistema que admiten eventos extendidos](xevents-references-system-objects.md)

Una vez finalizadas las instrucciones del script de Transact-SQL anterior, en la pestaña **Resultados** del Editor de consultas se mostrarán las columnas siguientes:
  
- name
- object_id
- lock_count
  
## <a name="see-also"></a>Consulte también

[CREATE EVENT SESSION &#40;Transact-SQL&#41;](../../t-sql/statements/create-event-session-transact-sql.md)  
[ALTER EVENT SESSION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-event-session-transact-sql.md)  
[sys.dm_xe_session_targets &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-xe-session-targets-transact-sql.md)  
[sys.dm_xe_sessions &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-xe-sessions-transact-sql.md)  
[sys.server_event_sessions &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-event-sessions-transact-sql.md)  
