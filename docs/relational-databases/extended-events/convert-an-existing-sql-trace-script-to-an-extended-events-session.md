---
title: Conversión de un script de seguimiento de SQL en una sesión de eventos extendidos
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xevents
ms.topic: tutorial
helpviewer_keywords:
- SQL Trace, convert script to extended events
- extended events [SQL Server], convert SQL Trace script
ms.assetid: 4c8f29e6-0a37-490f-88b3-33493871b3f9
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: b41947e50cd2cdd283af77a8d3ee4168f208f57e
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/19/2019
ms.locfileid: "75255754"
---
# <a name="convert-an-existing-sql-trace-script-to-an-extended-events-session"></a>Convertir un script de seguimiento de SQL existente en una sesión de eventos extendidos.

[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  Si tiene un script existente de Seguimiento de SQL que desea convertir a una sesión de eventos extendidos, puede usar los procedimientos de este tema para crear una sesión de eventos extendidos equivalente. Con la información de las tablas del sistema trace_xe_action_map y trace_xe_event_map, puede recopilar la información que necesita para realizar la conversión.  
  
 Los pasos son los siguientes:  
  
1.  Ejecute el script existente para crear una sesión de Seguimiento de SQL y obtener después el identificador del seguimiento.  
  
2.  Ejecute una consulta que use la función fn_trace_geteventinfo para buscar los eventos y acciones equivalentes de eventos extendidos para cada clase de eventos de Seguimiento de SQL y sus columnas asociadas.  
  
3.  Use la función fn_trace_getfilterinfo para enumerar los filtros y las acciones equivalentes de eventos extendidos que vaya a usar.  
  
4.  Cree manualmente una sesión de eventos extendidos utilizando los eventos, acciones, y predicados (filtros) equivalentes de eventos extendidos.  

## <a name="to-obtain-the-trace-id"></a>Para obtener el identificador de seguimiento  
  
1.  Abra el script de Seguimiento de SQL en el Editor de consultas y, a continuación, ejecute el script para crear la sesión de seguimiento. Tenga en cuenta que no es necesario que la sesión de seguimiento esté ejecutándose para completar este procedimiento.  
  
2.  Obtenga el identificador del seguimiento. Para ello, utilice la consulta siguiente:  
  
    ```sql
    SELECT * FROM sys.traces;  
    GO  
    ```  
  
    > [!NOTE]  
    >  El identificador de seguimiento 1 indica normalmente el seguimiento predeterminado.  
  
## <a name="to-determine-the-extended-events-equivalents"></a>Para determinar los equivalentes de eventos extendidos  
  
1.  Para determinar los eventos y acciones equivalentes de eventos extendidos, ejecute la consulta siguiente, donde *trace_id* se establece en el valor del identificador de seguimiento obtenido en el procedimiento anterior.  
  
    > [!NOTE]  
    >  En este ejemplo, se utiliza el identificador de seguimiento para el seguimiento predeterminado (1).  
  
    ```sql
    USE MASTER;  
    GO  
    DECLARE @trace_id int;  
    SET @trace_id = 1;  
    SELECT DISTINCT el.eventid, em.package_name, em.xe_event_name AS 'event'  
       , el.columnid, ec.xe_action_name AS 'action'  
    FROM (sys.fn_trace_geteventinfo(@trace_id) AS el  
       LEFT OUTER JOIN sys.trace_xe_event_map AS em  
          ON el.eventid = em.trace_event_id)  
    LEFT OUTER JOIN sys.trace_xe_action_map AS ec  
       ON el.columnid = ec.trace_column_id  
    WHERE em.xe_event_name IS NOT NULL AND ec.xe_action_name IS NOT NULL;  
    ```  
  
     Se devuelven el identificador de evento, nombre de paquete, nombre de evento, identificador de columna y nombre de acción equivalentes de eventos extendidos. Utilizará esta salida en el procedimiento "Para crear la sesión de eventos extendidos" más adelante en este tema.  
  
     En algunos casos, la columna filtrada se asigna a un campo de datos de evento que se incluye de forma predeterminada en el evento de eventos extendidos. Por consiguiente, la columna "Extended_Events_action_name" será NULL. Si esto se produce, debe realizar lo siguiente para determinar qué campo de datos es equivalente a la columna filtrada:  
  
    1.  Para las acciones que devuelven NULL, identifique qué clases de eventos de Seguimiento de SQL en el script contienen la columna que se está filtrando.  
  
         Por ejemplo, puede haber usado la clase de eventos SP:StmtCompleted y especificado un filtro en el nombre de columna de seguimiento Duration (identificador 45 de la clase de eventos de Seguimiento de SQL e identificador 13 de la columna de Seguimiento de SQL). En este caso, el nombre de acción aparecerá como NULL en los resultados de la consulta.  
  
    2.  Para cada clase de eventos de Seguimiento de SQL identificada en el paso anterior, busque el nombre de evento equivalente de eventos extendidos. (Si no está seguro del nombre de evento equivalente, use la consulta del tema [Ver los eventos extendidos equivalentes a las clases de evento de Seguimiento de SQL Server](../../relational-databases/extended-events/view-the-extended-events-equivalents-to-sql-trace-event-classes.md)).  
  
    3.  Utilice la consulta siguiente para identificar los campos de datos correctos que va a utilizar para los eventos identificados en el paso anterior. La consulta muestra los campos de datos de eventos extendidos en la columna "event_field". En la consulta, reemplace *<nombre_evento>* por el nombre de un evento especificado en el paso anterior.  
  
        ```sql
        SELECT xp.name package_name, xe.name event_name  
           ,xc.name event_field, xc.description  
        FROM sys.trace_xe_event_map AS em  
        INNER JOIN sys.dm_xe_objects AS xe  
           ON em.xe_event_name = xe.name  
        INNER JOIN sys.dm_xe_packages AS xp  
           ON xe.package_guid = xp.guid AND em.package_name = xp.name  
        INNER JOIN sys.dm_xe_object_columns AS xc  
           ON xe.name = xc.object_name  
        WHERE xe.object_type = 'event' AND xc.column_type <> 'readonly'  
           AND em.xe_event_name = '<event_name>';  
        ```  
  
         Por ejemplo, la clase de eventos SP:StmtCompleted se asigna al evento sp_statement_completed de eventos extendidos. Si especifica sp_statement_completed como nombre de evento en la consulta, la columna "event_field" muestra los campos que se incluyen de forma predeterminada con el evento. Examinando los campos, puede ver que hay un campo de "duración". Para crear el filtro en la sesión equivalente de eventos extendidos, agregaría un predicado como "WHERE duration > 0". Para obtener un ejemplo, vea el procedimiento "Para crear la sesión de eventos extendidos" en este tema.  
  
## <a name="to-create-the-extended-events-session"></a>Para crear la sesión de eventos extendidos  
 Utilice el Editor de consultas para crear la sesión de eventos extendidos y para escribir la salida en un destino de archivo. Los siguientes pasos describen una consulta única con explicaciones que le muestran cómo se genera la consulta. Para obtener el ejemplo completo de la consulta, vea la sección "Ejemplo" de este tema.  
  
1.  Agregue instrucciones para crear la sesión de eventos, reemplazando *nombre_de_sesión* por el nombre que quiere usar para la sesión de eventos extendidos.  
  
    ```sql
    IF EXISTS(SELECT * FROM sys.server_event_sessions WHERE name='session_name')  
       DROP EVENT SESSION [Session_Name] ON SERVER;  
    CREATE EVENT SESSION [Session_Name]  
    ON SERVER;  
    ```  
  
2.  Agregue los eventos y acciones de eventos extendidos que se devolvieron como salida en el procedimiento "Para determinar los equivalentes de eventos extendidos" y agregue los predicados (filtros) identificados en el procedimiento "Para determinar los filtros que se utilizan en el script".  
  
     En el ejemplo siguiente se usa un script de Seguimiento de SQL que incluye las clases de eventos SQL:StmtStarting y SP:StmtCompleted, con filtros para el identificador y la duración de la sesión. La salida de ejemplo para la consulta del procedimiento "Para determinar los equivalentes de eventos extendidos" devolvió el siguiente conjunto de resultados:  
  
    ```  
    Eventid  package_name  event                   columnid  action  
    44       sqlserver     sp_statement_starting   6         nt_username  
    44       sqlserver     sp_statement_starting   9         client_pid  
    44       sqlserver     sp_statement_starting   10        client_app_name  
    44       sqlserver     sp_statement_starting   11        server_principal_name  
    44       sqlserver     sp_statement_starting   12        session_id  
    45       sqlserver     sp_statement_completed  6         nt_username  
    45       sqlserver     sp_statement_completed  9         client_pid  
    45       sqlserver     sp_statement_completed  10        client_app_name  
    45       sqlserver     sp_statement_completed  11        server_principal_name  
    45       sqlserver     sp_statement_completed  12        session_id  
    ```  
  
     Para convertir esto en el equivalente de eventos extendidos, se agregan los eventos sqlserver.sp_statement_starting y sqlserver.sp_statement_completed con una lista de acciones. Las instrucciones de predicado se incluyen como cláusulas WHERE.  
  
    ```sql
    ADD EVENT sqlserver.sp_statement_starting  
       (ACTION  
          (  
          sqlserver.nt_username,  
          sqlserver.client_pid,  
          sqlserver.client_app_name,  
          sqlserver.server_principal_name,  
          sqlserver.session_id  
          )  
       WHERE sqlserver.session_id = 59   
       ),  
  
    ADD EVENT sqlserver.sp_statement_completed  
       (ACTION  
          (  
          sqlserver.nt_username,  
          sqlserver.client_pid,  
          sqlserver.client_app_name,  
          sqlserver.server_principal_name,  
          sqlserver.session_id  
          )  
       WHERE sqlserver.session_id = 59 AND duration > 0  
       )  
    ```  
  
3.  Agregue el destino de archivo asincrónico, reemplazando las rutas de acceso de archivo por la ubicación donde quiere guardar la salida. Cuando especifique el destino de archivo, debe incluir una ruta de acceso del archivo de registro y del archivo de metadatos.  
  
    ```sql
    ADD TARGET package0.asynchronous_file_target(  
       SET filename='c:\temp\ExtendedEventsStoredProcs.xel', metadatafile='c:\temp\ExtendedEventsStoredProcs.xem');  
    ```  
  
## <a name="to-view-the-results"></a>Para ver los resultados  
  
1.  Puede usar la función sys.fn_xe_file_target_read_file para ver la salida. Para ello, ejecute la consulta siguiente, reemplazando las rutas de acceso de archivo por las rutas de acceso que haya especificado:  
  
    ```sql
    SELECT *, CAST(event_data as XML) AS 'event_data_XML'  
    FROM sys.fn_xe_file_target_read_file('c:\temp\ExtendedEventsStoredProcs*.xel', 'c:\temp\ExtendedEventsStoredProcs*.xem', NULL, NULL);  
  
    ```  
  
    > [!NOTE]  
    >  La conversión de los datos de evento como XML es opcional.  
  
     Para obtener más información sobre la función sys.fn_xe_file_target_read_file, vea [sys.fn_xe_file_target_read_file &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-xe-file-target-read-file-transact-sql.md).  
  
    ```sql
    IF EXISTS(SELECT * FROM sys.server_event_sessions WHERE name='session_name')  
       DROP EVENT SESSION [session_name] ON SERVER;  
    CREATE EVENT SESSION [session_name]  
    ON SERVER  
  
    ADD EVENT sqlserver.sp_statement_starting  
       (ACTION  
       (  
          sqlserver.nt_username,  
          sqlserver.client_pid,  
          sqlserver.client_app_name,  
          sqlserver.server_principal_name,  
          sqlserver.session_id  
       )  
       WHERE sqlserver.session_id = 59   
       ),  
  
    ADD EVENT sqlserver.sp_statement_completed  
       (ACTION  
       (  
          sqlserver.nt_username,  
          sqlserver.client_pid,  
          sqlserver.client_app_name,  
          sqlserver.server_principal_name,  
          sqlserver.session_id  
       )  
       WHERE sqlserver.session_id = 59 AND duration > 0  
       );  
  
    ADD TARGET package0.asynchronous_file_target  
       (SET filename='c:\temp\ExtendedEventsStoredProcs.xel', metadatafile='c:\temp\ExtendedEventsStoredProcs.xem');  
    ```  
  
## <a name="example"></a>Ejemplo  
  
```sql
IF EXISTS(SELECT * FROM sys.server_event_sessions WHERE name='session_name')  
   DROP EVENT SESSION [session_name] ON SERVER;  
CREATE EVENT SESSION [session_name]  
ON SERVER  
  
ADD EVENT sqlserver.sp_statement_starting  
   (ACTION  
   (  
      sqlserver.nt_username,  
      sqlserver.client_pid,  
      sqlserver.client_app_name,  
      sqlserver.server_principal_name,  
      sqlserver.session_id  
   )  
   WHERE sqlserver.session_id = 59   
   ),  
  
ADD EVENT sqlserver.sp_statement_completed  
   (ACTION  
   (  
      sqlserver.nt_username,  
      sqlserver.client_pid,  
      sqlserver.client_app_name,  
      sqlserver.server_principal_name,  
      sqlserver.session_id  
   )  
   WHERE sqlserver.session_id = 59 AND duration > 0  
   )  
  
ADD TARGET package0.asynchronous_file_target  
   (SET filename='c:\temp\ExtendedEventsStoredProcs.xel', metadatafile='c:\temp\ExtendedEventsStoredProcs.xem');  
```  
  
## <a name="see-also"></a>Consulte también  
 [Ver los eventos extendidos equivalentes a las clases de evento de Seguimiento de SQL](../../relational-databases/extended-events/view-the-extended-events-equivalents-to-sql-trace-event-classes.md)  
  
  
