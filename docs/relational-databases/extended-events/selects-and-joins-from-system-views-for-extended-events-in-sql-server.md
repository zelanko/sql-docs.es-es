---
title: Instrucciones SELECT y JOIN en vistas del sistema para eventos extendidos en SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 08/02/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xevents
ms.topic: tutorial
ms.assetid: 04521d7f-588c-4259-abc2-1a2857eb05ec
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: dac049477fad134aa3cf8776c8ffa13f33e111ee
ms.sourcegitcommit: 715683b5fc7a8e28a86be8949a194226b72ac915
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/26/2019
ms.locfileid: "58478150"
---
# <a name="selects-and-joins-from-system-views-for-extended-events-in-sql-server"></a>Instrucciones SELECT y JOIN en vistas del sistema para eventos extendidos en SQL Server

[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]


En este artículo se explican los dos conjuntos de vistas del sistema relacionadas con eventos extendidos en Microsoft SQL Server y en el servicio en la nube de Base de datos SQL de Azure. En este artículo se describe lo siguiente:

- Cómo combinar varias vistas del sistema.
- Cómo seleccionar determinada información de las vistas del sistema.
- Cómo la misma información de sesión de eventos se representa desde diferentes perspectivas tecnológicas, lo que le permite entender mejor cada perspectiva.


La mayoría de los ejemplos están escritos para SQL Server, pero con pequeños cambios podrían ejecutarse en Base de datos SQL.



## <a name="a-foundational-information"></a>A. Información básica


Hay dos conjuntos de vistas del sistema para eventos extendidos:


#### <a name="catalog-views"></a>Vistas de catálogo:

- Estas vistas almacenan información sobre la *definición* de cada sesión de eventos creada por [CREATE EVENT SESSION](../../t-sql/statements/create-event-session-transact-sql.md)o por una interfaz de usuario de SSMS equivalente. Pero estas vistas no saben si las sesiones empezaron a ejecutarse en algún momento.
    - Por ejemplo, si el **Explorador de objetos** de SSMS no muestra ninguna sesión de eventos definida, el uso de una instrucción SELECT en la vista *sys.server_event_session_targets* no devolverá ninguna fila.


- El prefijo del nombre es el siguiente:
    - *sys.server\_event\_session\** es el prefijo del nombre en SQL Server.
    - *sys.database\_event\_session\** es el prefijo del nombre en Base de datos SQL.


#### <a name="dynamic-management-views-dmvs"></a>Vistas de administración dinámica (DMV):

- Almacenan información sobre la *actividad actual* de las sesiones de eventos en ejecución, pero tienen poca información sobre la definición de las sesiones.
    - Aunque todas las sesiones de eventos estén detenidas, el uso de una instrucción SELECT en la vista *sys.dm_xe_packages* devuelve filas, ya que al iniciarse el servidor se cargan varios paquetes en la memoria activa.
    - Por la misma razón, *sys.dm_xe_objects* *sys.dm_xe_object_columns* would also still return rows.


- El prefijo del nombre de las DMV de eventos extendidos es el siguiente:
    - *sys.dm\_xe\_\** es el prefijo del nombre en SQL Server.
    - *sys.dm\_xe\_database\_\** es generalmente el prefijo del nombre en SQL Database.


#### <a name="permissions"></a>Permisos:


Para seleccionar entre las vistas del sistema, se necesita el permiso siguiente:

- VIEW SERVER STATE en Microsoft SQL Server.
- VIEW DATABASE STATE en Base de datos SQL de Azure.


<a name="section_B_catalog_views"></a>

## <a name="b-catalog-views"></a>B. Vistas de catálogo


En esta sección se demuestra que tres perspectivas tecnológicas diferentes coinciden perfectamente en la misma sesión de eventos definida. La sesión se ha definido en el **Explorador de objetos** de SQL Server Management Studio (SSMS.exe) y es visible en dicho explorador, pero no se está ejecutando actualmente.

Se recomienda [instalar la actualización más reciente de SSMS](https://msdn.microsoft.com/library/mt238290.aspx)todos los meses para evitar errores inesperados.


Encontrará documentación de referencia sobre las vistas de catálogo para eventos extendidos en [Vistas de catálogo de eventos extendidos (Transact-SQL)](../../relational-databases/system-catalog-views/extended-events-catalog-views-transact-sql.md).


&nbsp;



#### <a name="the-sequence-in-this-section-b"></a>Secuencia de esta sección B:


- [B.1 Perspectiva de la interfaz de usuario de SSMS](#section_B_1_SSMS_UI_perspective)
    - Cree la definición de la sesión de eventos mediante la interfaz de usuario de SSMS. Se muestran capturas de pantalla que indican todos los pasos.


- [B.2 Perspectiva de Transact-SQL](#section_B_2_TSQL_perspective)
    - Use el menú contextual de SSMS para aplicar técnicas de ingeniería inversa a la sesión de eventos definida y convertirla en la instrucción **CREATE EVENT SESSION** equivalente de Transact-SQL. La instrucción de T-SQL coincide perfectamente con las opciones de las capturas de pantalla de SSMS.


- [B.3 Perspectiva de SELECT JOIN UNION de la vista de catálogo](#section_B_3_Catalog_view_S_J_UNION)
    - Emita una instrucción SELECT de T-SQL desde las vistas de catálogo del sistema para esta sesión de eventos. Los resultados coinciden con las especificaciones de la instrucción **CREATE EVENT SESSION** .


&nbsp;



<a name="section_B_1_SSMS_UI_perspective"></a>

### <a name="b1-ssms-ui-perspective"></a>B.1 Perspectiva de la interfaz de usuario de SSMS


Para iniciar el cuadro de diálogo **Nueva sesión**en el **Explorador de objetos** de SSMS, expanda **Administración** > **Eventos extendidos**y haga clic con el botón derecho en **Sesiones** > **Nueva sesión**.

En el cuadro de diálogo grande de **Nueva sesión**, vemos en la primera sección con la etiqueta **General** que se ha seleccionado la opción para **Iniciar la sesión de eventos al iniciar el servidor**.

![Nueva sesión &gt; General, Iniciar la sesión de eventos al iniciar el servidor.](../../relational-databases/extended-events/media/xevents-ssms-ac105-eventname-startup.png)


En la sección **Eventos**, vemos que se ha elegido el evento **lock_deadlock**. Para ese evento, vemos que se han seleccionado tres **Acciones** . Esto significa que se ha hecho clic en el botón **Configurar** , que aparece en gris después de que se haga clic en él.

![Nueva sesión > Eventos, Campos globales (acciones)](../../relational-databases/extended-events/media/xevents-ssms-ac110-actions-global.png)


<a name="resource_type_PAGE_cat_view"></a>

Después, todavía en la sección **eventos** > **configurar**, vemos que [**resource_type** se ha establecido en **PAGE**](#resource_type_dmv_actual_row). Esto significa que los datos de evento no se enviarán del motor de eventos al destino si el valor de **resource_type** es distinto de **PAGE**.

Podemos ver filtros de predicado adicionales para el nombre de la base de datos y para un contador.

![Nueva sesión > Eventos, Filtro (predicado)](../../relational-databases/extended-events/media/xevents-ssms-ac115-predicate-db.png)


Después, en la sección **Almacenamiento de datos**, vemos que se ha elegido como destino **event_file**. Además, se ha seleccionado la opción **Habilitar sustitución incremental de archivos**.

![Nueva sesión > Almacenamiento de datos, event_file, Habilitar sustitución incremental de archivos](../../relational-databases/extended-events/media/xevents-ssms-ac120-target-eventfile.png)


Por último, en la sección **Avanzadas**, vemos que el valor de **Latencia máxima de envío** se ha reducido a 4 segundos.

![Nueva sesión > Avanzadas, Latencia máxima de envío](../../relational-databases/extended-events/media/xevents-ssms-ac125-latency4.png)


Con esto se completa la perspectiva de la interfaz de usuario de SSMS en una definición de sesión de eventos.


<a name="section_B_2_TSQL_perspective"></a>

### <a name="b2-transact-sql-perspective"></a>B.2 Perspectiva de Transact-SQL


Independientemente de cómo se haya creado una definición de sesión de eventos, es posible aplicar técnicas de ingeniería inversa a la sesión desde la interfaz de usuario de SSMS para convertirla en un script de Transact-SQL que coincida perfectamente. Puede examinar las capturas de pantalla de la nueva sesión anterior y comparar las especificaciones visibles con las cláusulas del script siguiente de T-SQL generado, **CREATE EVENT SESSION** .

Para aplicar técnicas de ingeniería inversa a una sesión de eventos, en el **Explorador de objetos** , haga clic con el botón derecho en el nodo de sesión y elija **Incluir sesión como** > **Crear en** > **Portapapeles**.

El script de T-SQL siguiente se creó aplicando técnicas de ingeniería inversa con SSMS. Después, se aplicó sangría al script manualmente manipulando de manera estratégica el espacio en blanco.


```sql
CREATE EVENT SESSION [event_session_test3]
    ON SERVER  -- Or, if on Azure SQL Database, ON DATABASE.

    ADD EVENT sqlserver.lock_deadlock
    (
        SET
            collect_database_name = (1)
        ACTION
        (
            package0  .collect_system_time,
            package0  .event_sequence,
            sqlserver .client_hostname
        )
        WHERE
        (
            [database_name]           = N'InMemTest2'
            AND [package0].[counter] <= (16)
            AND [resource_type]       = (6)
        )
    )

    ADD TARGET package0.event_file
    (
        SET
            filename           = N'C:\Junk\event_session_test3_EF.xel',
            max_file_size      = (20),
            max_rollover_files = (2)
    )

    WITH
    (
        MAX_MEMORY            = 4096 KB,
        EVENT_RETENTION_MODE  = ALLOW_SINGLE_EVENT_LOSS,
        MAX_DISPATCH_LATENCY  = 4 SECONDS,
        MAX_EVENT_SIZE        = 0 KB,
        MEMORY_PARTITION_MODE = NONE,
        TRACK_CAUSALITY       = OFF,
        STARTUP_STATE         = ON
    );
```


Con esto se completa la perspectiva de T-SQL.


<a name="section_B_3_Catalog_view_S_J_UNION"></a>

### <a name="b3-catalog-view-select-join-union-perspective"></a>B.3 Perspectiva de SELECT JOIN UNION de la vista de catálogo


No se deje impresionar. La siguiente instrucción SELECT de T-SQL es larga simplemente porque combina varias instrucciones SELECT pequeñas. Todas las instrucciones SELECT pequeñas se pueden ejecutar de manera independiente. Dichas instrucciones muestran cómo se deben combinar varias vistas de catálogo del sistema.


```sql
SELECT
        s.name        AS [Session-Name],
        '1_EVENT'     AS [Clause-Type],
        'Event-Name'  AS [Parameter-Name],
        e.name        AS [Parameter-Value]
    FROM
              sys.server_event_sessions         AS s
        JOIN  sys.server_event_session_events   AS e

            ON  e.event_session_id = s.event_session_id
    WHERE
        s.name = 'event_session_test3'

UNION ALL
SELECT
        s.name         AS [Session-Name],
        '2_EVENT_SET'  AS [Clause-Type],
        f.name         AS [Parameter-Name],
        f.value        AS [Parameter-Value]
    FROM
              sys.server_event_sessions         AS s
        JOIN  sys.server_event_session_events   AS e

            ON  e.event_session_id = s.event_session_id

        JOIN  sys.server_event_session_fields   As f

            ON  f.event_session_id = s.event_session_id
            AND f.object_id        = e.event_id
    WHERE
        s.name = 'event_session_test3'

UNION ALL
SELECT
        s.name              AS [Session-Name],
        '3_EVENT_ACTION'    AS [Clause-Type],

        e.package + '.' + a.name
                            AS [Parameter-Name],

        '(Not_Applicable)'  AS [Parameter-Value]
    FROM
              sys.server_event_sessions         AS s
        JOIN  sys.server_event_session_events   AS e

            ON  e.event_session_id = s.event_session_id

        JOIN  sys.server_event_session_actions  As a

            ON  a.event_session_id = s.event_session_id
            AND a.event_id         = e.event_id
    WHERE
        s.name = 'event_session_test3'

UNION ALL
SELECT
        s.name                AS [Session-Name],
        '4_EVENT_PREDICATES'  AS [Clause-Type],
        e.predicate           AS [Parameter-Name],
        '(Not_Applicable)'    AS [Parameter-Value]
    FROM
              sys.server_event_sessions         AS s
        JOIN  sys.server_event_session_events   AS e

            ON  e.event_session_id = s.event_session_id
    WHERE
        s.name = 'event_session_test3'

UNION ALL
SELECT
        s.name              AS [Session-Name],
        '5_TARGET'          AS [Clause-Type],
        t.name              AS [Parameter-Name],
        '(Not_Applicable)'  AS [Parameter-Value]
    FROM
              sys.server_event_sessions         AS s
        JOIN  sys.server_event_session_targets  AS t

            ON  t.event_session_id = s.event_session_id
    WHERE
        s.name = 'event_session_test3'

UNION ALL
SELECT
        s.name          AS [Session-Name],
        '6_TARGET_SET'  AS [Clause-Type],
        f.name          AS [Parameter-Name],
        f.value         AS [Parameter-Value]
    FROM
              sys.server_event_sessions         AS s
        JOIN  sys.server_event_session_targets  AS t

            ON  t.event_session_id = s.event_session_id

        JOIN  sys.server_event_session_fields   As f

            ON  f.event_session_id = s.event_session_id
            AND f.object_id        = t.target_id
    WHERE
        s.name = 'event_session_test3'

UNION ALL
SELECT
        s.name               AS [Session-Name],
        '7_WITH_MAX_MEMORY'  AS [Clause-Type],
        'max_memory'         AS [Parameter-Name],
        s.max_memory         AS [Parameter-Value]
    FROM
              sys.server_event_sessions  AS s
    WHERE
        s.name = 'event_session_test3'

UNION ALL
SELECT
        s.name                  AS [Session-Name],
        '7_WITH_STARTUP_STATE'  AS [Clause-Type],
        'startup_state'         AS [Parameter-Name],
        s.startup_state         AS [Parameter-Value]
    FROM
              sys.server_event_sessions  AS s
    WHERE
        s.name = 'event_session_test3'

ORDER BY
    [Session-Name],
    [Clause-Type],
    [Parameter-Name]
;
```


#### <a name="output"></a>Salida


A continuación se muestra la salida real de la ejecución de la anterior instrucción SELECT JOIN UNION. Los nombres y los valores del parámetro de salida se asignan a lo que es visible en la anterior instrucción CREATE EVENT SESSION.


```
Session-Name          Clause-Type            Parameter-Name                  Parameter-Value
------------          -----------            --------------                  ---------------
event_session_test3   1_EVENT                Event-Name                      lock_deadlock
event_session_test3   2_EVENT_SET            collect_database_name           1
event_session_test3   3_EVENT_ACTION         sqlserver.client_hostname       (Not_Applicable)
event_session_test3   3_EVENT_ACTION         sqlserver.collect_system_time   (Not_Applicable)
event_session_test3   3_EVENT_ACTION         sqlserver.event_sequence        (Not_Applicable)
event_session_test3   4_EVENT_PREDICATES     ([sqlserver].[equal_i_sql_unicode_string]([database_name],N'InMemTest2') AND [package0].[counter]<=(16))   (Not_Applicable)
event_session_test3   5_TARGET               event_file                      (Not_Applicable)
event_session_test3   6_TARGET_SET           filename                        C:\Junk\event_session_test3_EF.xel
event_session_test3   6_TARGET_SET           max_file_size                   20
event_session_test3   6_TARGET_SET           max_rollover_files              2
event_session_test3   7_WITH_MAX_MEMORY      max_memory                      4096
event_session_test3   7_WITH_STARTUP_STATE   startup_state                   1
```


Con esto se completa la sección sobre vistas de catálogo.



<a name="section_C_DMVs"></a>

## <a name="c-dynamic-management-views-dmvs"></a>C. Vistas de administración dinámica (DMV)


Ahora pasamos a las DMV. En esta sección se proporcionan varias instrucciones SELECT de Transact-SQL que sirven para una finalidad práctica específica del entorno empresarial. Además, las instrucciones SELECT muestran cómo se pueden combinar las DMV para todos los usos nuevos que se le ocurran.


Encontrará documentación de referencia sobre las DMV en [Vistas de administración dinámica de eventos extendidos](../../relational-databases/system-dynamic-management-views/extended-events-dynamic-management-views.md)


En este artículo, las filas de salida real de las instrucciones SELECT siguientes son de SQL Server 2016, a menos que se indique lo contrario.


Esta es una lista de las instrucciones SELECT de esta sección sobre DMV:

- [C.1 Lista de todos los paquetes](#section_C_1_list_packages)
- [C.2 Recuento de todos los tipos de objetos](#section_C_2_count_object_type)
- [C.3 Selección de todos los elementos disponibles ordenados por tipo](#section_C_3_select_all_available_objects)
- [C.4 Campos de datos disponibles para el evento](#section_C_4_data_fields)
- [C.5 *sys.dm_xe_map_values* y campos de evento](#section_C_5_map_values_fields)
- [C.6 Parámetros para los destinos](#section_C_6_parameters_targets)
- [C.7 Instrucción SELECT de DMV para convertir la columna target_data a XML](#section_C_7_dmv_select_target_data_column)
- [C.8 Seleccionar una función para recuperar datos de event_file de una unidad de disco](#section_C_8_select_function_disk)



<a name="section_C_1_list_packages"></a>

### <a name="c1-list-of-all-packages"></a>C.1 Lista de todos los paquetes


Todos los objetos que se pueden usar en el área de eventos extendidos proceden de los paquetes que se han cargado en el sistema. En esta sección se enumeran todos los paquetes y sus descripciones.


```sql
SELECT  --C.1
        p.name         AS [Package],
        p.description  AS [Package-Description]
    FROM
        sys.dm_xe_packages  AS p
    ORDER BY
        p.name;
```


#### <a name="output"></a>Salida

Esta es una lista de los paquetes.


```
/***  (The unique p.guid values are not shown.)
Package        Package-Description
-------        -------------------
filestream     Extended events for SQL Server FILESTREAM and FileTable
package0       Default package. Contains all standard types, maps, compare operators, actions and targets
qds            Extended events for Query Store
SecAudit       Security Audit Events
sqlclr         Extended events for SQL CLR
sqlos          Extended events for SQL Operating System
SQLSatellite   Extended events for SQL Satellite
sqlserver      Extended events for Microsoft SQL Server
sqlserver      Extended events for Microsoft SQL Server
sqlserver      Extended events for Microsoft SQL Server
sqlsni         Extended events for Microsoft SQL Server
ucs            Extended events for Unified Communications Stack
XtpCompile     Extended events for the XTP Compile
XtpEngine      Extended events for the XTP Engine
XtpRuntime     Extended events for the XTP Runtime
***/
```


*Definiciones de las siglas anteriores:*

- clr = Common Language Runtime de .NET
- qds = Almacén de datos de consultas
- sni = Interfaz de red de servidor
- ucs = Pila de comunicaciones unificadas
- xtp = Procesamiento de transacciones extremo


<a name="section_C_2_count_object_type"></a>

### <a name="c2-count-of-every-object-type"></a>C.2 Recuento de todos los tipos de objetos


En esta sección se indica el tipo de objetos contenidos en los paquetes de eventos. Se muestra una lista completa de todos los tipos de objetos que se encuentran en *sys.dm\_xe\_objects*, junto con el número de cada tipo.


```sql
SELECT  --C.2
        Count(*)  AS [Count-of-Type],
        o.object_type
    FROM
        sys.dm_xe_objects  AS o
    GROUP BY
        o.object_type
    ORDER BY
        1  DESC;
```


#### <a name="output"></a>Salida

Este es el número de objetos por tipo de objeto. Hay aproximadamente 1915 objetos.


```
/***  Actual output, sum is about 1915:

Count-of-Type   object_type
-------------   -----------
1303            event
351             map
84              message
77              pred_compare
53              action
46              pred_source
28              type
17              target
***/
```


<a name="section_C_3_select_all_available_objects"></a>

### <a name="c3-select-all-available-items-sorted-by-type"></a>C.3 Selección de todos los elementos disponibles ordenados por tipo


La siguiente instrucción SELECT devuelve aproximadamente 1915 filas, una para cada objeto.



```sql
SELECT  --C.3
        o.object_type  AS [Type-of-Item],
        p.name         AS [Package],
        o.name         AS [Item],
        o.description  AS [Item-Description]
    FROM
             sys.dm_xe_objects  AS o
        JOIN sys.dm_xe_packages AS p  ON o.package_guid = p.guid
    WHERE
        o.object_type IN ('action' , 'target' , 'pred_source')
        AND
        (
            (o.capabilities & 1) = 0
            OR
            o.capabilities IS NULL
        )
    ORDER BY
        [Type-of-Item],
        [Package],
        [Item];
```


#### <a name="output"></a>Salida

Para despertar su curiosidad, a continuación se recoge un muestreo arbitrario de los objetos devueltos por la anterior instrucción SELECT.


```
/***
Type-of-Item   Package        Item                          Item-Description
------------   -------        ----                          ----------------
action         package0       callstack                     Collect the current call stack
action         package0       debug_break                   Break the process in the default debugger
action         sqlos          task_time                     Collect current task execution time
action         sqlserver      sql_text                      Collect SQL text
event          qds            query_store_aprc_regression   Fired when Query Store detects regression in query plan performance
event          SQLSatellite   connection_accept             Occurs when a new connection is accepted. This event serves to log all connection attempts.
event          XtpCompile     cgen                          Occurs at start of C code generation.
map            qds            aprc_state                    Query Store Automatic Plan Regression Correction state
message        package0       histogram_event_required      A value is required for the parameter 'filtering_event_name' when source type is 0.
pred_compare   package0       equal_ansi_string             Equality operator between two ANSI string values
pred_compare   sqlserver      equal_i_sql_ansi_string       Equality operator between two SQL ANSI string values
pred_source    sqlos          task_execution_time           Get current task execution time
pred_source    sqlserver      client_app_name               Get the current client application name
target         package0       etw_classic_sync_target       Event Tracing for Windows (ETW) Synchronous Target
target         package0       event_counter                 Use the event_counter target to count the number of occurrences of each event in the event session.
target         package0       event_file                    Use the event_file target to save the event data to an XEL file, which can be archived and used for later analysis and review. You can merge multiple XEL files to view the combined data from separate event sessions.
target         package0       histogram                     Use the histogram target to aggregate event data based on a specific event data field or action associated with the event. The histogram allows you to analyze distribution of the event data over the period of the event session.
target         package0       pair_matching                 Pairing target
target         package0       ring_buffer                   Asynchronous ring buffer target.
type           package0       xml                           Well formed XML fragment
***/
```



<a name="section_C_4_data_fields"></a>

### <a name="c4-data-fields-available-for-your-event"></a>C.4 Campos de datos disponibles para el evento


La siguiente instrucción SELECT devuelve todos los campos de datos específicos del tipo de evento.

- Observe el elemento de la cláusula WHERE: *column_type = 'data'*.
- Además, tendrá que modificar el valor de la cláusula WHERE para *o.name =*.


```sql
SELECT  -- C.4
        p.name         AS [Package],
        c.object_name  AS [Event],
        c.name         AS [Column-for-Predicate-Data],
        c.description  AS [Column-Description]
    FROM
              sys.dm_xe_object_columns  AS c
        JOIN  sys.dm_xe_objects         AS o

            ON  o.name = c.object_name

        JOIN  sys.dm_xe_packages        AS p

            ON  p.guid = o.package_guid
    WHERE
        c.column_type = 'data'
        AND
        o.object_type = 'event'
        AND
        o.name        = '\<EVENT-NAME-HERE!>'  --'lock_deadlock'
    ORDER BY
        [Package],
        [Event],
        [Column-for-Predicate-Data];
```


#### <a name="output"></a>Salida

La anterior instrucción SELECT, WHERE `o.name = 'lock_deadlock'`devolvió las filas siguientes:

- Cada fila representa un filtro opcional para el evento *sqlserver.lock_deadlock* .
- En la pantalla siguiente se omite la columna *\[Column-Description\]* , que suele tener un valor NULL.


```
/***
Actual output, except for the omitted Description column which is often NULL.
These rows are where object_type = 'lock_deadlock'.

Package     Event           Column-for-Predicate-Data
-------     -----           -------------------------
sqlserver   lock_deadlock   associated_object_id
sqlserver   lock_deadlock   database_id
sqlserver   lock_deadlock   database_name
sqlserver   lock_deadlock   deadlock_id
sqlserver   lock_deadlock   duration
sqlserver   lock_deadlock   lockspace_nest_id
sqlserver   lock_deadlock   lockspace_sub_id
sqlserver   lock_deadlock   lockspace_workspace_id
sqlserver   lock_deadlock   mode
sqlserver   lock_deadlock   object_id
sqlserver   lock_deadlock   owner_type
sqlserver   lock_deadlock   resource_0
sqlserver   lock_deadlock   resource_1
sqlserver   lock_deadlock   resource_2
sqlserver   lock_deadlock   resource_description
sqlserver   lock_deadlock   resource_type
sqlserver   lock_deadlock   transaction_id
***/
```



<a name="section_C_5_map_values_fields"></a>

### <a name="c5-sysdmxemapvalues-and-event-fields"></a>C.5 *sys.dm_xe_map_values* y campos de evento


La siguiente instrucción SELECT incluye una instrucción JOIN en la vista denominada *sys.dm_xe_map_values*, que es más complicada.

El propósito de la instrucción SELECT es mostrar los numerosos campos entre los que puede elegir para la sesión de eventos. Los campos de evento se pueden usar de dos maneras:

- Para elegir qué valores de campo se escribirán en el destino para cada repetición del evento.
- Para filtrar qué repeticiones de eventos se enviarán desde el destino y cuáles se conservarán.


```sql
SELECT  --C.5
        dp.name         AS [Package],
        do.name         AS [Object],
        do.object_type  AS [Object-Type],
        'o--c'     AS [O--C],
        dc.name         AS [Column],
        dc.type_name    AS [Column-Type-Name],
        dc.column_type  AS [Column-Type],
        dc.column_value AS [Column-Value],
        'c--m'     AS [C--M],
        dm.map_value    AS [Map-Value],
        dm.map_key      AS [Map-Key]
    FROM
              sys.dm_xe_objects         AS do
        JOIN  sys.dm_xe_object_columns  AS dc

            ON  dc.object_name = do.name

        JOIN  sys.dm_xe_map_values      AS dm

            ON  dm.name = dc.type_name

        JOIN  sys.dm_xe_packages        AS dp

            ON  dp.guid = do.package_guid
    WHERE
        do.object_type = 'event'
        AND
        do.name        = '\<YOUR-EVENT-NAME-HERE!>'  --'lock_deadlock'
    ORDER BY
        [Package],
        [Object],
        [Column],
        [Map-Value];
```


#### <a name="output"></a>Salida

<a name="resource_type_dmv_actual_row"></a>

A continuación se recoge un muestreo de las 153 filas reales de la salida de la anterior instrucción SELECT de T-SQL. La fila de **resource_type** es [pertinente](#resource_type_PAGE_cat_view) para el filtrado de predicados usado en el ejemplo **event_session_test3** en otra parte de este artículo.


```
/***  5 sampled rows from the actual 153 rows returned.
    NOTE:  'resource_type' under 'Column'.

Package     Object          Object-Type   O--C   Column          Column-Type-Name     Column-Type   Column-Value   C--M   Map-Value        Map-Key
-------     ------          -----------   ----   ------          ----------------     -----------   ------------   ----   ---------        -------
sqlserver   lock_deadlock   event         o--c   CHANNEL         etw_channel          readonly      2              c--m   Operational      4
sqlserver   lock_deadlock   event         o--c   KEYWORD         keyword_map          readonly      16             c--m   access_methods   1024
sqlserver   lock_deadlock   event         o--c   mode            lock_mode            data          NULL           c--m   IX               8
sqlserver   lock_deadlock   event         o--c   owner_type      lock_owner_type      data          NULL           c--m   Cursor           2
sqlserver   lock_deadlock   event         o--c   resource_type   lock_resource_type   data          NULL           c--m   PAGE             6

Therefore, on your CREATE EVENT SESSION statement, in its ADD EVENT WHERE clause,
you could put:
    WHERE( ... resource_type = 6 ...)  -- Meaning:  6 = PAGE.
***/
```


<a name="section_C_6_parameters_targets"></a>

### <a name="c6-parameters-for-targets"></a>C.6 Parámetros para los destinos


La siguiente instrucción SELECT devuelve todos los parámetros para el destino. Cada parámetro tiene una etiqueta para indicar si es obligatorio. Los valores que asigne a los parámetros afectarán al comportamiento del destino.

- Observe el elemento de la cláusula WHERE: *object_type = 'customizable'*.
- Además, tendrá que modificar el valor de la cláusula WHERE para *o.name =*.


```sql
SELECT  --C.6
        p.name        AS [Package],
        o.name        AS [Target],
        c.name        AS [Parameter],
        c.type_name   AS [Parameter-Type],

        CASE c.capabilities_desc
            WHEN 'mandatory' THEN 'YES_Mandatory'
            ELSE 'Not_mandatory'
        END  AS [IsMandatoryYN],

        c.description AS [Parameter-Description]
    FROM
              sys.dm_xe_objects   AS o
        JOIN  sys.dm_xe_packages  AS p

            ON  o.package_guid = p.guid

        LEFT OUTER JOIN  sys.dm_xe_object_columns  AS c

            ON  o.name        = c.object_name
            AND c.column_type = 'customizable'  -- !
    WHERE
        o.object_type = 'target'
        AND
        o.name     LIKE '%'    -- Or '\<YOUR-TARGET-NAME-HERE!>'.
    ORDER BY
        [Package],
        [Target],
        [IsMandatoryYN]  DESC,
        [Parameter];
```


#### <a name="output"></a>Salida

Las filas de parámetros siguientes son un subconjunto de los devueltos por la instrucción SELECT anterior, en SQL Server 2016.


```
/***  Actual output, all rows, where target name = 'event_file'.
Package    Target       Parameter            Parameter-Type       IsMandatoryYN   Parameter-Description
-------    ------       ---------            --------------       -------------   ---------------------
package0   event_file   filename             unicode_string_ptr   YES_Mandatory   Specifies the location and file name of the log
package0   event_file   increment            uint64               Not_mandatory   Size in MB to grow the file
package0   event_file   lazy_create_blob     boolean              Not_mandatory   Create blob upon publishing of first event buffer, not before.
package0   event_file   max_file_size        uint64               Not_mandatory   Maximum file size in MB
package0   event_file   max_rollover_files   uint32               Not_mandatory   Maximum number of files to retain
package0   event_file   metadatafile         unicode_string_ptr   Not_mandatory   Not used
***/
```


<a name="section_C_7_dmv_select_target_data_column"></a>

### <a name="c7-dmv-select-casting-targetdata-column-to-xml"></a>C.7 Instrucción SELECT de DMV para convertir la columna target_data a XML


Esta instrucción SELECT de DMV devuelve filas de datos del destino de la sesión de eventos activa. Los datos se convierten a XML, lo que permite hacer clic en las celdas devueltas para mostrarlas fácilmente en SSMS.

- Si se detiene la sesión de eventos, esta instrucción SELECT no devolverá ninguna fila.
- Tendrá que modificar el valor de la cláusula WHERE para *s.name =*.


```sql
SELECT  --C.7
        s.name,
        t.target_name,
        CAST(t.target_data AS XML)  AS [XML-Cast]
    FROM
              sys.dm_xe_session_targets  AS t
        JOIN  sys.dm_xe_sessions         AS s

            ON s.address = t.event_session_address
    WHERE
        s.name = '\<Your-Session-Name-Here!>';
```


#### <a name="output-the-only-row-including-its-xml-cell"></a>Salida, la única fila, incluida la celda XML

Esta es la única fila que tiene como salida la anterior instrucción SELECT. La columna *XML-Cast* contiene una cadena de XML que SSMS entiende como XML. Por lo tanto, SSMS sabe que debe permitir hacer clic en la celda XML-Cast.


Para esta ejecución:

- El valor *s.name =* se estableció en una sesión de eventos para el evento *checkpoint_begin* .
- El destino era *ring_buffer*.


```XML
name                              target_name   XML-Cast
----                              -----------   --------
checkpoint_session_ring_buffer2   ring_buffer   <RingBufferTarget truncated="0" processingTime="0" totalEventsProcessed="2" eventCount="2" droppedCount="0" memoryUsed="104"><event name="checkpoint_begin" package="sqlserver" timestamp="2016-07-09T01:28:23.508Z"><data name="database_id"><type name="uint32" package="package0" /><value>5</value></data></event><event name="checkpoint_begin" package="sqlserver" timestamp="2016-07-09T01:28:26.975Z"><data name="database_id"><type name="uint32" package="package0" /><value>5</value></data></event></RingBufferTarget>
```


#### <a name="output-xml-displayed-pretty-when-cell-is-clicked"></a>Salida, XML con sangría cuando se hace clic en la celda


Cuando se hace clic en la celda XML-Cast, aparece la siguiente pantalla con sangría.


```xml
<RingBufferTarget truncated="0" processingTime="0" totalEventsProcessed="2" eventCount="2" droppedCount="0" memoryUsed="104">
  <event name="checkpoint_begin" package="sqlserver" timestamp="2016-07-09T01:28:23.508Z">
    <data name="database_id">
      <type name="uint32" package="package0" />
      <value>5</value>
    </data>
  </event>
  <event name="checkpoint_begin" package="sqlserver" timestamp="2016-07-09T01:28:26.975Z">
    <data name="database_id">
      <type name="uint32" package="package0" />
      <value>5</value>
    </data>
  </event>
</RingBufferTarget>
```


<a name="section_C_8_select_function_disk"></a>

### <a name="c8-select-from-a-function-to-retrieve-eventfile-data-from-disk-drive"></a>C.8 Seleccionar una función para recuperar datos de event_file de una unidad de disco


Supongamos que la sesión de eventos recopiló algunos datos y después se detuvo. Si la sesión estaba definida para usar el destino event_file, puede recuperar los datos mediante una llamada a la función *sys.fn_xe_target_read_file*.

- Debe modificar la ruta de acceso y el nombre de archivo en el parámetro de la llamada de función antes de ejecutar esta instrucción SELECT.
    - Ignore los dígitos adicionales que el sistema SQL inserta en los nombres de archivo .XEL reales cada vez que reinicie la sesión. Simplemente asigne el nombre de raíz y la extensión normales.


```sql
SELECT  --C.8
        f.module_guid,
        f.package_guid,
        f.object_name,
        f.file_name,
        f.file_offset,
        CAST(f.event_data AS XML)  AS [Event-Data-As-XML]
    FROM
        sys.fn_xe_file_target_read_file(

            '\<YOUR-PATH-FILE-NAME-ROOT-HERE!>*.xel',
            --'C:\Junk\Checkpoint_Begins_ES*.xel',  -- Example.

            NULL, NULL, NULL
        )  AS f;
```


#### <a name="output-rows-returned-by-select-from-the-function"></a>Salida, filas devueltas al aplicar la instrucción SELECT FROM en la función


A continuación se muestran las filas devueltas al aplicar la anterior instrucción SELECT FROM en la función. La columna XML del extremo derecho contiene los datos que tratan específicamente sobre la repetición de eventos.


```
module_guid                            package_guid                           object_name        file_name                                                           file_offset   Event-Data-As-XML
-----------                            ------------                           -----------        ---------                                                           -----------   -----------------
D5149520-6282-11DE-8A39-0800200C9A66   03FDA7D0-91BA-45F8-9875-8B6DD0B8E9F2   checkpoint_begin   C:\Junk\Checkpoint_Begins_ES_20160615bb-_0_131125086091700000.xel   5120          <event name="checkpoint_begin" package="sqlserver" timestamp="2016-07-09T03:30:14.023Z"><data name="database_id"><value>5</value></data><action name="session_id" package="sqlserver"><value>60</value></action><action name="database_id" package="sqlserver"><value>5</value></action></event>
D5149520-6282-11DE-8A39-0800200C9A66   03FDA7D0-91BA-45F8-9875-8B6DD0B8E9F2   checkpoint_end     C:\Junk\Checkpoint_Begins_ES_20160615bb-_0_131125086091700000.xel   5120          <event name="checkpoint_end" package="sqlserver" timestamp="2016-07-09T03:30:14.025Z"><data name="database_id"><value>5</value></data></event>
D5149520-6282-11DE-8A39-0800200C9A66   03FDA7D0-91BA-45F8-9875-8B6DD0B8E9F2   checkpoint_begin   C:\Junk\Checkpoint_Begins_ES_20160615bb-_0_131125086091700000.xel   5632          <event name="checkpoint_begin" package="sqlserver" timestamp="2016-07-09T03:30:17.704Z"><data name="database_id"><value>5</value></data><action name="session_id" package="sqlserver"><value>60</value></action><action name="database_id" package="sqlserver"><value>5</value></action></event>
D5149520-6282-11DE-8A39-0800200C9A66   03FDA7D0-91BA-45F8-9875-8B6DD0B8E9F2   checkpoint_end     C:\Junk\Checkpoint_Begins_ES_20160615bb-_0_131125086091700000.xel   5632          <event name="checkpoint_end" package="sqlserver" timestamp="2016-07-09T03:30:17.709Z"><data name="database_id"><value>5</value></data></event>
```


#### <a name="output-one-xml-cell"></a>Salida, una celda XML


Aquí se muestra el contenido de la primera celda XML del conjunto de filas devuelto anteriormente.


```xml
<event name="checkpoint_begin" package="sqlserver" timestamp="2016-07-09T03:30:14.023Z">
  <data name="database_id">
    <value>5</value>
  </data>
  <action name="session_id" package="sqlserver">
    <value>60</value>
  </action>
  <action name="database_id" package="sqlserver">
    <value>5</value>
  </action>
</event>
```


