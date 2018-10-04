---
title: Crear una sesión de eventos extendidos mediante el Editor de consultas | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- create extended events session
- extended events [SQL Server], create session
ms.assetid: cba0e02b-b201-4863-bf1b-9164e68e5fa8
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 6e0c243dcacf653167477137e26f0767985f6fa3
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48150875"
---
# <a name="create-an-extended-events-session-using-query-editor"></a>Crear una sesión de eventos extendidos mediante el Editor de consultas
  Puede crear una sesión de eventos extendidos utilizando el Editor de consultas o puede crear una sesión en el Explorador de objetos. En el Explorador de objetos, los eventos extendidos disponen de dos interfaces de usuario que puede utilizar para crear, modificar y ver los datos de la sesión de eventos. Un asistente le guía en el proceso de creación de la sesión de eventos, y una interfaz de usuario de nueva sesión que proporciona más opciones de configuración avanzadas. Puede crear sesiones de eventos extendidos para diagnosticar el seguimiento de SQL Server, lo cual le permite resolver problemas como el siguiente:  
  
-   Encontrar las consultas más caras  
  
-   Encontrar las causas principales de la contención de bloqueos temporales  
  
-   Encontrar una consulta que esté bloqueando otras consultas  
  
-   Solucionar problemas de uso excesivo de la CPU producido por la recompilación de consultas  
  
-   Solucionar problemas de interbloqueos  
  
 Para obtener más información sobre cómo crear una sesión de eventos extendidos con el Asistente para nueva sesión, vea [Crear una sesión de Extended Events utilizando el asistente &#40;Explorador de objetos&#41;](../ssms/object/object-explorer.md). Para obtener más información sobre cómo crear una sesión de eventos extendidos con la interfaz de usuario de nueva sesión, vea [Crear una sesión de eventos extendidos utilizando el cuadro de diálogo Nueva sesión](../../2014/database-engine/create-an-extended-events-session-using-the-new-session-dialog.md).  
  
##  <a name="BeforeYouBegin"></a> Permisos  
 Para crear una sesión de eventos extendidos, debe disponer del permiso ALTER ANY EVENT SESSION.  
  
## <a name="creating-an-extended-events-session-using-query-editor"></a>Crear una sesión de eventos extendidos mediante el Editor de consultas  
  
#### <a name="to-create-an-extended-events-session"></a>Para crear una sesión de eventos extendidos  
  
1.  En el siguiente procedimiento se muestra cómo crear una sesión de eventos extendidos utilizando el Editor de consultas en [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)].  
  
     Determine los eventos que desea utilizar en la sesión. Para ver todos los eventos disponibles, junto con la palabra clave y el canal, utilice la siguiente consulta:  
  
    > [!NOTE]  
    >  Para obtener más información sobre las palabras clave y los canales, vea [Paquetes de SQL Server Extended Events](../relational-databases/extended-events/sql-server-extended-events-packages.md).  
  
    ```  
    SELECT p.name, c.event, k.keyword, c.channel, c.description FROM  
       (  
       SELECT event_package = o.package_guid, o.description,   
       event=c.object_name, channel = v.map_value  
       FROM sys.dm_xe_objects o  
       LEFT JOIN sys.dm_xe_object_columns c ON o.name = c.object_name  
       INNER JOIN sys.dm_xe_map_values v ON c.type_name = v.name   
       AND c.column_value = cast(v.map_key AS nvarchar)  
       WHERE object_type = 'event' AND (c.name = 'CHANNEL' or c.name IS NULL)  
       ) c LEFT JOIN   
       (  
       SELECT event_package = c.object_package_guid, event = c.object_name,   
       keyword = v.map_value  
       FROM sys.dm_xe_object_columns c INNER JOIN sys.dm_xe_map_values v   
       ON c.type_name = v.name AND c.column_value = v.map_key   
       AND c.type_package_guid = v.object_package_guid  
       INNER JOIN sys.dm_xe_objects o ON o.name = c.object_name   
       AND o.package_guid = c.object_package_guid  
       WHERE object_type = 'event' AND c.name = 'KEYWORD'   
       ) k  
       ON  
       k.event_package = c.event_package AND (k.event=c.event or k.event IS NULL)  
       INNER JOIN sys.dm_xe_packages p ON p.guid = c.event_package  
    ORDER BY keyword desc, channel, event  
    ```  
  
2.  En una nueva ventana de consulta, agregue las siguientes instrucciones para crear una sesión de eventos, reemplazando *session_name* por el nombre de la sesión que quiera usar:  
  
    > [!IMPORTANT]  
    >  En los pasos 2 a 6 de este procedimiento se describe cada sección de la definición de la sesión de eventos. Debe agregar todas las instrucciones en una sola ventana de consulta antes de la ejecución. Para obtener un ejemplo completo, vea la sección Ejemplo de este tema.  
  
    ```  
    CREATE EVENT SESSION session_name   
    ON SERVER  
    ```  
  
3.  Agregue los eventos que quiere supervisar, en formato *package_name*.*event_name*. Para cada evento, agregue una línea similar a la siguiente:  
  
    ```  
    ADD EVENT package_name.event_name  
    ```  
  
     Por ejemplo:  
  
    ```  
    ADD EVENT sqlserver.file_read_completed,  
    ADD EVENT sqlserver.file_write_completed  
    ```  
  
4.  (Opcional) Después de agregar un evento, puede agregar las acciones que se han de realizar. También puede agregar predicados. Los predicados se utilizan para establecer los criterios para saber en qué momento la información de eventos se debe usar en el destino. Las acciones se agregan utilizando una cláusula ACTION y los predicados se agregan utilizando una cláusula WHERE. Por ejemplo, para agregar una acción y un predicado donde se captura el texto de [!INCLUDE[tsql](../includes/tsql-md.md)] para el evento sqlserver.file_read_completed, siendo el identificador de archivo igual a 1, también debe incluir la siguiente instrucción:  
  
    ```  
    ADD EVENT sqlserver.file_read_completed  
       (ACTION (sqlserver.sql_text)  
       WHERE file_id = 1),  
    ```  
  
    -   Para ver qué acciones están disponibles, utilice la siguiente consulta:  
  
        ```  
        SELECT p.name AS 'package_name', xo.name AS 'action_name', xo.description, xo.object_type  
        FROM sys.dm_xe_objects AS xo  
        JOIN sys.dm_xe_packages AS p  
           ON xo.package_guid = p.guid  
        WHERE xo.object_type = 'action'  
        AND (xo.capabilities & 1 = 0   
        OR xo.capabilities IS NULL)  
        ORDER BY p.name, xo.name  
        ```  
  
    -   Para ver los predicados disponibles para un evento, use la consulta siguiente, reemplazando *event_name* por el nombre del evento para el que quiere agregar un predicado:  
  
        ```  
        SELECT *  
        FROM sys.dm_xe_object_columns  
        WHERE object_name = 'event_name'  
        AND column_type = 'data'  
        ```  
  
         Por ejemplo:  
  
        ```  
        SELECT *   
        FROM sys.dm_xe_object_columns   
        WHERE object_name = 'file_read_completed'  
        AND column_type = 'data'  
        ```  
  
         Tenga en cuenta que también puede agregar orígenes globales de predicado. Un origen global de predicado se puede utilizar en cualquier expresión de predicado. Para ver qué orígenes globales de predicado están disponibles, utilice la siguiente consulta:  
  
        ```  
        SELECT p.name AS package_name, xo.name AS predicate_name  
           , xo.description, xo.object_type  
        FROM sys.dm_xe_objects AS xo  
        JOIN sys.dm_xe_packages AS p  
           ON xo.package_guid = p.guid  
        WHERE xo.object_type = 'pred_source'  
        ORDER BY p.name, xo.name  
        ```  
  
         Por ejemplo, puede usar la expresión de predicado siguiente para especificar que se deben recopilar únicamente datos para un evento las cinco primeras veces que se produce el citado evento.  
  
        ```  
        WHERE package0.counter <= 5  
        ```  
  
5.  Agregue el destino deseado donde se procesarán y utilizarán los datos de evento. Utilice el siguiente formato:  
  
    ```  
    ADD TARGET package_name.target_name  
    ```  
  
     En el ejemplo siguiente se agrega el destino de archivo asincrónico:  
  
    ```  
    ADD TARGET package0.asynchronous_file_target  
       (SET filename = 'c:\temp\xelog.xel', metadatafile = 'c:\temp\xelog.xem')  
    ```  
  
     Para ver la lista de destinos disponibles, utilice la siguiente consulta:  
  
    ```  
    SELECT p.name AS 'package_name', xo.name AS 'target_name'  
       , xo.description, xo.object_type   
    FROM sys.dm_xe_objects AS xo  
    JOIN sys.dm_xe_packages AS p  
       ON xo.package_guid = p.guid  
    WHERE xo.object_type = 'target'  
    AND (xo.capabilities & 1 = 0  
    OR xo.capabilities IS NULL)  
    ORDER BY p.name, xo.name  
    ```  
  
    > [!NOTE]  
    >  Para obtener más información sobre los diferentes tipos de destino, vea [Destinos de SQL Server Extended Events](../../2014/database-engine/sql-server-extended-events-targets.md).  
  
6.  Revise y agregue las opciones de configuración adicionales que desee. Por ejemplo, puede configurar opciones tales como el modo de retención de eventos, el tiempo que los eventos se almacenan en búfer en memoria, o si la sesión de eventos debe iniciarse automáticamente cuando se inicie [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Las opciones se describen en el tema [ALTER EVENT SESSION &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-event-session-transact-sql). Tenga en cuenta que se asignan los valores predeterminados si no se especifican estas opciones.  
  
7.  Inicie la sesión.  
  
    > [!NOTE]  
    >  Para obtener más información sobre cómo se pueden ver los resultados de una sesión, vea el tema correspondiente al tipo de destino usado en el nodo [Destinos de SQL Server Extended Events](../../2014/database-engine/sql-server-extended-events-targets.md) de los Libros en pantalla.  
  
 En el ejemplo siguiente se crea una sesión de eventos extendidos denominada IOActivity que captura la información siguiente:  
  
-   Los datos de evento para lecturas de archivos completadas, incluido el texto de [!INCLUDE[tsql](../includes/tsql-md.md)] asociado para las lecturas de archivos en que el identificador de archivo es igual a 1.  
  
-   Los datos de evento para escrituras de archivos completadas.  
  
-   Los datos de evento para los casos en que los datos se escriben de la memoria caché del registro al archivo de registro físico.  
  
 La sesión envía la salida a un archivo de destino.  
  
```  
CREATE EVENT SESSION IOActivity  
ON SERVER  
  
ADD EVENT sqlserver.file_read_completed  
   (  
   ACTION (sqlserver.sql_text)  
   WHERE file_id = 1),  
ADD EVENT sqlserver.file_write_completed,  
ADD EVENT sqlserver.databases_log_flush  
  
ADD TARGET package0.asynchronous_file_target   
   (SET filename = 'c:\temp\xelog.xel', metadatafile = 'c:\temp\xelog.xem')  
```  
  
## <a name="see-also"></a>Vea también  
 [CREATE EVENT SESSION &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-event-session-transact-sql)   
 [Destinos de SQL Server Extended Events](../../2014/database-engine/sql-server-extended-events-targets.md)   
 [Paquetes de SQL Server Extended Events](../relational-databases/extended-events/sql-server-extended-events-packages.md)  
  
  
