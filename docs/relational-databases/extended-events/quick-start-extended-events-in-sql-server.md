---
title: "Inicio rápido: Eventos extendidos en SQL Server | Microsoft Docs"
ms.custom: 
ms.date: 09/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: extended-events
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
- xevents
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 7bb78b25-3433-4edb-a2ec-c8b2fa58dea1
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: b532bf37f99a3fc05b0f2999d0d3d301323457d6
ms.sourcegitcommit: 37f0b59e648251be673389fa486b0a984ce22c81
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/12/2018
---
# <a name="quick-start-extended-events-in-sql-server"></a>Quick Start: Extended Events in SQL Server (Inicio rápido: Eventos extendidos en SQL Server)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]


Este artículo tiene como objetivo prestar ayuda al desarrollador de SQL que no está familiarizado con los eventos extendidos y que quiere crear una sesión de eventos en tan solo unos minutos. Mediante el uso de eventos extendidos, puede ver información sobre las operaciones internas del sistema de SQL y de su aplicación. Cuando crea una sesión de eventos extendidos, indica al sistema:

- Las repeticiones que le interesan.
- Cómo quiere que el sistema le notifique los datos.


En este artículo se realizan las tareas siguientes:

- Usar capturas de pantalla para ilustrar los clics en SSMS.exe que crean una sesión de eventos.
- Correlacionar las capturas de pantalla con las instrucciones Transact-SQL equivalentes.
- Explicar en detalle los términos y conceptos relativos a los clics y T-SQL para las sesiones de eventos.
- Demostrar cómo probar la sesión de eventos.
- Describir las alternativas en torno a los resultados:
  - Captura de almacenamiento de los resultados.
  - Resultados procesados frente a los resultados sin procesar.
  - Herramientas para ver los resultados de diferentes maneras y en diferentes escalas de tiempo.
- Mostrar cómo puede buscar y detectar todos los eventos disponibles.
- Proporcionar las relaciones de clave externa y de clave principal que están implícitas entre las vistas de administración dinámica (DMV) de los eventos extendidos.
- Describir la información adicional que se puede obtener en los artículos relacionados.


A veces, los blogs y otras conversaciones informales hacen referencia a los eventos extendidos mediante la abreviatura *xevents*.


> [!NOTE]
> Para obtener más información sobre las diferencias de los eventos extendidos entre Microsoft SQL Server y Base de datos SQL de Azure, vea [Eventos extendidos en Base de datos SQL](http://azure.microsoft.com/documentation/articles/sql-database-xevent-db-diff-from-svr/).


## <a name="preparations-before-demo"></a>Preparativos antes de la demostración


Se necesitarán los siguientes pasos preliminares para realizar la próxima demostración.

1. [Descarga de SQL Server Management Studio (SSMS)](http://msdn.microsoft.com/library/mt238290.aspx)
  - Cada mes debe instalar la última actualización mensual de SSMS.
2. Inicie sesión en Microsoft SQL Server 2014 o posterior, o en una base de datos de Base de datos SQL de Azure donde `SELECT @@version` devuelve un valor cuyo primer nodo es 12 o superior.
3. Asegúrese de que su cuenta tenga el [permiso de servidor](../../t-sql/statements/grant-server-permissions-transact-sql.md) de **ALTER ANY EVENT SESSION**.
  - Si está interesado, puede encontrar más información disponible sobre seguridad y permisos relacionados con los eventos extendidos al final de este artículo en el [Apéndice](#appendix1).




## <a name="demo-of-ssms-integration"></a>Demostración de la integración de SSMS


SSMS.exe proporciona una excelente interfaz de usuario (IU) para los eventos extendidos. La interfaz de usuario es tan útil que muchos usuarios no necesitan usar los eventos extendidos mediante Transact-SQL ni las vistas de administración dinámica (DMV) que tienen como objetivo dichos eventos.

En esta sección, puede ver los pasos de la interfaz de usuario para crear un evento extendido, y para ver los datos que notifica. Después de estos pasos, puede obtener información sobre los conceptos implicados en los pasos para tener una mayor comprensión.


### <a name="steps-of-demo"></a>Pasos de la demostración


Puede comprender los pasos aunque decida no realizarlos. La demostración se inicia en el cuadro de diálogo **Nueva sesión** . Procesamos sus cuatro páginas denominadas:

- General
- Eventos
- Almacenamiento de datos
- Avanzadas


El texto y las capturas de pantalla de ayuda pueden ser ligeramente inexactas cuando la interfaz de usuario de SSMS se modifica con el paso de los meses o años. Aunque existan discrepancias o pequeñas diferencias, las capturas de pantalla siguen resultando útiles para la explicación.


1. Conéctese a SSMS.

2. En el Explorador de objetos, haga clic en **Administración** > **Eventos extendidos** > **Nueva sesión**. Es preferible usar el cuadro de diálogo **Nueva sesión** que el **Asistente para nueva sesión**, aunque ambos son similares.

3. En la parte superior izquierda, haga clic en la página **General** . Después, escriba *SuSesión*, o cualquier nombre que quiera, en el cuadro de texto **Nombre de sesión** . *No* pulse el botón **Aceptar** todavía, ya que aparece solo al final de la demostración.

    ![Nueva sesión > General > Nombre de sesión](../../relational-databases/extended-events/media/xevents-session-newsessions-10-general-ssms-yoursessionnode.png)

4. En la parte superior izquierda, haga clic en la página **Eventos** y, después, haga clic en el botón **Seleccionar** .

    ![Nueva sesión > Eventos > Seleccionar > Biblioteca de eventos, eventos seleccionados](../../relational-databases/extended-events/media/xevents-session-newsessions-14-events-ssms-rightclick-not-wizard.png)

5. En el área **Biblioteca de eventos**, en la lista desplegable, elija **Solo los nombres de evento**.
    - Dentro del cuadro de texto, escriba **sql**, que filtra y reduce la larga lista de eventos disponibles mediante un operador *contains* .
    - Desplácese y haga clic en el evento denominado **sql_statement_completed**.
    - Haga clic en el botón de flecha derecha **>** para mover el evento al cuadro **Eventos seleccionados** .

6. Siga en la página **Eventos** y haga clic en el botón **Configurar** en el extremo derecho.
    - Con el lateral izquierdo reducido para obtener una mejor visualización, en la siguiente captura de pantalla puede ver el área **Opciones de configuración de eventos**.

    ![Nueva sesión > Eventos > Configurar > Filtro (predicado) > Campo](../../relational-databases/extended-events/media/xevents-session-newsessions-20b-events-ssms-yoursessionnode.png)

7. Haga clic en la pestaña **Filtro (predicado)**. Después, haga clic en **Haga clic aquí para agregar una cláusula**para capturar todas las instrucciones SQL SELECT que tengan una cláusula HAVING.

8. En la lista desplegable **Campo** , elija **sqlserver.sql_text**.
   - En **Operador** , elija un operador LIKE.
   - En **Valor** , escriba **%SELECT%HAVING%**.

    > [!NOTE]
    > En este nombre de dos partes, *sqlserver* es el nombre del paquete y *sql_text* es el nombre del campo. El evento que hemos elegido anteriormente, *sql_statement_completed* , debe encontrarse en el mismo paquete que el campo que hemos elegido.

9. En la parte superior izquierda, haga clic en la página **Almacenamiento de datos** .

10. En el área **Destinos** , haga clic en **Haga clic aquí para agregar un destino**.
    - En la lista desplegable **Tipo** , elija **event_file**.
    - Esto significa que los datos del evento se almacenarán en un archivo que podamos ver.

    ![Nueva sesión > Almacenamiento de datos > Destinos > Tipo > event_file](../../relational-databases/extended-events/media/xevents-session-newsessions-30-datastorage-ssms-yoursessionnode.png)

11. En el área **Propiedades** , escriba una ruta de acceso completa y un nombre de archivo en el cuadro de texto **Nombre de archivo en el servidor** .
    - La extensión del nombre de archivo debe ser *.xel*.
    - Nuestra pequeña prueba necesitará menos de 1 MB de tamaño de archivo.

    ![Nueva sesión > Avanzado > Latencia máxima de envío > Aceptar](../../relational-databases/extended-events/media/xevents-session-newsessions-40-advanced-ssms-yoursessionnode.png)

12. En la parte superior izquierda, haga clic en la página **Advanced (Avanzado)**.
    - Reduce la **latencia máxima de envío** a 3 segundos.
    - Por último, haga clic en el botón **Aceptar** situado en la parte inferior.

13. Vuelva al **Explorador de objetos**, expanda **Administración** > **Sesiones** y verá el nuevo nodo de **SuSesión**.

    ![El nodo de su nueva *sesión de eventos* denominado SuSesión, en el Explorador de objetos, en Administración > Eventos extendidos > Sesiones](../../relational-databases/extended-events/media/xevents-session-newsessions-50-objectexplorer-ssms-yoursessionnode.png)


#### <a name="edit-your-event-session"></a>Editar la sesión de eventos


En el **Explorador de objetos**de SSMS, puede editar la sesión de eventos al hacer clic con el botón derecho en su nodo y, después, hacer clic en **Propiedades**. Se muestra el mismo cuadro de diálogo de varias páginas.


### <a name="corresponding-t-sql-for-your-event-session"></a>T-SQL correspondiente para la sesión de eventos


Ha usado la interfaz de usuario de SSMS para generar un script T-SQL que ha creado la sesión de eventos. A continuación, puede ver el script generado:

- Haga clic con el botón derecho en el nodo de la sesión, haga clic en **Incluir sesión como** > **CREATE to (CREATE para)** > **Portapapeles**.
- Péguelo en cualquier editor de texto.


A continuación, se encuentra la instrucción CREATE EVENT SESSION de T-SQL para *SuSesión*que se ha generado mediante sus clics en la interfaz de usuario:


```sql
CREATE EVENT SESSION [YourSession]
    ON SERVER 
    ADD EVENT sqlserver.sql_statement_completed
    (
        ACTION(sqlserver.sql_text)
        WHERE
        ( [sqlserver].[like_i_sql_unicode_string]([sqlserver].[sql_text], N'%SELECT%HAVING%')
        )
    )
    ADD TARGET package0.event_file
    (SET
        filename = N'C:\Junk\YourSession_Target.xel',
        max_file_size = (2),
        max_rollover_files = (2)
    )
    WITH (
        MAX_MEMORY = 2048 KB,
        EVENT_RETENTION_MODE = ALLOW_MULTIPLE_EVENT_LOSS,
        MAX_DISPATCH_LATENCY = 3 SECONDS,
        MAX_EVENT_SIZE = 0 KB,
        MEMORY_PARTITION_MODE = NONE,
        TRACK_CAUSALITY = OFF,
        STARTUP_STATE = OFF
    );
GO
```


> [!NOTE]
> Para Base de datos SQL de Azure, en la instrucción CREATE EVENT SESSION anterior, se encontraría la cláusula ON SERVER en lugar de ON DATABASE.
> 
> Para obtener más información sobre las diferencias de los eventos extendidos entre Microsoft SQL Server y Base de datos SQL de Azure, vea [Eventos extendidos en Base de datos SQL](http://azure.microsoft.com/documentation/articles/sql-database-xevent-db-diff-from-svr/).


#### <a name="pre-drop-of-the-event-session"></a>Instrucción DROP previa a la sesión de eventos


Antes de la instrucción CREATE EVENT SESSION, quizás quiera emitir de manera condicional una instrucción DROP EVENT SESSION en caso de que el nombre ya exista.


```sql
IF EXISTS (SELECT *
      FROM sys.server_event_sessions    -- If Microsoft SQL Server.
    --FROM sys.database_event_sessions  -- If Azure SQL Database in the cloud.
      WHERE name = 'YourSession')
BEGIN
    DROP EVENT SESSION YourSession
          ON SERVER;    -- If Microsoft SQL Server.
        --ON DATABASE;  -- If Azure SQL Database.
END
go
```


#### <a name="alter-to-start-and-stop-the-event-session"></a>Instrucción ALTER para iniciar o detener la sesión de eventos


Cuando crea una sesión de eventos, el valor predeterminado consiste en no iniciar la ejecución automáticamente. Puede iniciar o detener la sesión de eventos en cualquier momento mediante la siguiente instrucción ALTER EVENT SESSION de T-SQL.


```sql
ALTER EVENT SESSION [YourSession]
      ON SERVER
    --ON DATABASE
    STATE = START;   -- STOP;
```


Tiene la opción de indicar a la sesión de eventos que se inicie automáticamente cuando lo haga la instancia de SQL Server. Vea la palabra clave **STARTUP STATE = ON** en CREATE EVENT SESSION.

- La interfaz de usuario de SSMS ofrece una casilla correspondiente en la página **Nueva sesión** > **General** .


## <a name="test-your-event-session"></a>Probar la sesión de eventos


Pruebe la sesión de eventos con estos sencillos pasos:

1. En el **Explorador de objetos**de SSMS, haga clic con el botón derecho en el nodo de la sesión de eventos y, después, haga clic en **Iniciar sesión**.
2. Ejecute la instrucción `SELECT...HAVING` siguiente un par de veces.
    - Lo ideal sería que pudiera cambiar el valor `HAVING Count` entre las dos ejecuciones, alternando entre 2 y 3. Esto le permite ver las diferencias en los resultados.
3. Haga clic con el botón derecho en el nodo de la sesión y, después, haga clic en **Detener sesión**.
4. Lea la siguiente subsección sobre [cómo usar SELECT y ver los resultados](#select-the-full-results-xml-37).



```sql
SELECT
        c.name,
        Count(*)  AS [Count-Per-Column-Repeated-Name]
    FROM
             sys.syscolumns  AS c
        JOIN sys.sysobjects  AS o
    
            ON o.id = c.id
    WHERE
        o.type = 'V'
        AND
        c.name like '%event%'
    GROUP BY
        c.name
    HAVING
        Count(*) >= 3   --2     -- Try both values during session.
    ORDER BY
        c.name;
```


Para completar la información, aquí se muestra el resultado aproximado de la instrucción SELECT...HAVING anterior.


```
/*** Approximate output, 6 rows, all HAVING Count >= 3:
name                   Count-Per-Column-Repeated-Name
---------------------  ------------------------------
event_group_type       4
event_group_type_desc  4
event_session_address  5
event_session_id       5
is_trigger_event       4
trace_event_id         3
***/
```



<a name="select-the-full-results-xml-37"/>

### <a name="select-the-full-results-as-xml"></a>Instrucción SELECT para obtener los resultados completos como XML


En SSMS, ejecute la siguiente instrucción SELECT de T-SQL para devolver resultados donde cada fila proporciona los datos sobre una repetición de evento. La instrucción CAST AS XML facilita la visualización de los resultados.


> [!NOTE]
> El sistema de eventos siempre anexa un gran número al nombre de archivo event_file *.xel* que ha especificado. Antes de que pueda ejecutar la siguiente instrucción SELECT del archivo, debe copiar el nombre completo que ha proporcionado el sistema y pegarlo en la instrucción SELECT.


```sql
SELECT
        object_name,
        file_name,
        file_offset,
        event_data,
        'CLICK_NEXT_CELL_TO_BROWSE_XML RESULTS!'
                AS [CLICK_NEXT_CELL_TO_BROWSE_XML_RESULTS],
    
        CAST(event_data AS XML) AS [event_data_XML]
                -- TODO: In ssms.exe results grid, double-click this xml cell!
    FROM
        sys.fn_xe_file_target_read_file(
            'C:\Junk\YourSession_Target_0_131085363367310000.xel',
            null, null, null
        );
```


La instrucción SELECT anterior le proporciona dos maneras de ver los resultados completos de cualquier fila de evento determinada:

- Ejecute la instrucción SELECT en SSMS y, después, haga clic en una celda de la columna **event_data_XML** . Esto resulta muy práctico.
- Copie la larga cadena XML de una celda en la columna **event_data** . Péguela en un editor de texto sencillo como Notepad.exe y guarde la cadena en un archivo con extensión .XML. Después, abra el archivo .XML con un explorador.


#### <a name="display-of-results-for-one-event"></a>Mostrar los resultados de un evento


A continuación, podemos ver parte de los resultados que se encuentran en formato XML. Este XML aparece editado para que sea más corto para su visualización. Tenga en cuenta que `<data name="row_count">` muestra el valor de `6`, que coincide con nuestras 6 filas de resultados que hemos mostrado anteriormente. Y podemos ver la instrucción SELECT completa.


```xml
<event name="sql_statement_completed" package="sqlserver" timestamp="2016-05-24T04:06:08.997Z">
  <data name="duration">
    <value>111021</value>
  </data>
  <data name="cpu_time">
    <value>109000</value>
  </data>
  <data name="physical_reads">
    <value>0</value>
  </data>
  <data name="last_row_count">
    <value>6</value>
  </data>
  <data name="offset">
    <value>0</value>
  </data>
  <data name="offset_end">
    <value>584</value>
  </data>
  <data name="statement">
    <value>SELECT
        c.name,
        Count(*)  AS [Count-Per-Column-Repeated-Name]
    FROM
             sys.syscolumns  AS c
        JOIN sys.sysobjects  AS o

            ON o.id = c.id
    WHERE
        o.type = 'V'
        AND
        c.name like '%event%'
    GROUP BY
        c.name
    HAVING
        Count(*) &gt;= 3   --2     -- Try both values during session.
    ORDER BY
        c.name</value>
  </data>
</event>
```


## <a name="ssms-to-display-results"></a>SSMS para mostrar resultados


Existen varias características avanzadas en la interfaz de usuario de SSMS que puede usar para ver los datos que se han capturado de un evento extendido. Puede encontrar información en:

- [Advanced Viewing of Target Data from Extended Events in SQL Server (Visualización avanzada de datos de destino de eventos extendidos en SQL Server)](../../relational-databases/extended-events/advanced-viewing-of-target-data-from-extended-events-in-sql-server.md)


Los conceptos básicos comienzan con las opciones del menú contextual denominadas **View Target Data (Ver datos de destino)** y **Watch Live Data (Observar datos en directo)**.


### <a name="view-target-data"></a>View Target Data (Ver datos de destino)


En el **Explorador de objetos**de SSMS, puede hacer clic con el botón derecho en el nodo de destino que se encuentra debajo del nodo de la sesión de eventos. En el menú contextual, haga clic en **View Target Data (Ver datos de destino)**. SSMS muestra los datos.

La visualización no se actualiza ya que el evento notifica datos nuevos. Pero puede hacer clic en **View Target Data (Ver datos de destino)** de nuevo.


![View Target Data (Ver datos de destino), en SSMS, Administración > Eventos extendidos > Sesiones > SuSesión > package0.event_file, hacer clic con el botón derecho](../../relational-databases/extended-events/media/xevents-viewtargetdata-ssms-targetnode-61.png)


### <a name="watch-live-data"></a>Watch Live Data (Observar datos en directo)


En el **Explorador de objetos**de SSMS, puede hacer clic con el botón derecho en el nodo de la sesión de eventos. En el menú contextual, haga clic en **Watch Live Data (Observar datos en directo)**. SSMS muestra los datos entrantes a medida que llegan en tiempo real.


![Watch Live Data (Observar datos en directo), en SSMS, Administración > Eventos extendidos > Sesiones > SuSesión, hacer clic con el botón derecho](../../relational-databases/extended-events/media/xevents-watchlivedata-ssms-yoursessionnode-63.png)


## <a name="scenarios"></a>Escenarios


Existen incontables escenarios para el uso eficaz de los eventos extendidos. En los siguientes artículos se proporcionan escenarios de ejemplo que implican los bloqueos que se han realizado durante las consultas.


En los siguientes artículos se describen escenarios específicos para las sesiones de eventos que tienen como objetivo la evaluación de los bloqueos. En los artículos también se muestran algunas técnicas avanzadas, como el uso de **@dbid**y el de `EXECUTE (@YourSqlString)`dinámico:

- [Buscar los objetos que han obtenido más bloqueos](../../relational-databases/extended-events/find-the-objects-that-have-the-most-locks-taken-on-them.md)
  - En este escenario se usa package0.histogram de destino, que procesa los datos de eventos sin procesar antes de mostrárselos.
- [Determinar las consultas que mantienen bloqueos](../../relational-databases/extended-events/determine-which-queries-are-holding-locks.md)
  - En este escenario se usa [target package0.pair_matching](http://msdn.microsoft.com/library/3c87dcfb-543a-4bd8-a73d-1390bdf4ffa3), donde el par de eventos es sqlserver.lock_acquire y lock_release.


## <a name="terms-and-concepts-in-extended-events"></a>Términos y conceptos de los eventos extendidos


En la siguiente tabla se enumeran los términos que se usan en los eventos extendidos, y se describe su significado.


| Término | Description |
| :--- | :---------- |
| sesión de eventos | Una construcción que se centra en torno a uno o más eventos, además de elementos complementarios como acciones y destinos. La instrucción CREATE EVENT SESSION construye cada sesión de eventos. Puede modificar una sesión de eventos para iniciarla y detenerla a su voluntad. <br/> <br/> A veces, se hace referencia a una sesión de eventos solo como *sesión*, cuando el contexto lo aclara significa *sesión de eventos*. <br/> <br/> Puede encontrar más información sobre las sesiones de eventos en: [SQL Server Extended Events Sessions (Sesiones de eventos extendidos de SQL Server)](../../relational-databases/extended-events/sql-server-extended-events-sessions.md). |
| event | Una repetición específica en el sistema que se observa mediante una sesión de eventos activa. <br/> <br/> Por ejemplo, el evento *sql_statement_completed* representa el momento en que cualquier instrucción T-SQL se completa. El evento puede notificar su duración y otros datos. |
| target | Un elemento que recibe los datos de salida de un evento capturado. El destino le muestra los datos. <br/> <br/> Entre los ejemplos se incluye *event_file*, su elemento Cousin útil y ligero, y la memoria *ring_buffer*. El sofisticado destino *histogram* realiza un procesamiento de los datos antes de mostrarlos. <br/> <br/> Puede usarse cualquier destino para cualquier sesión de eventos. Para más información, consulte [Destinos para eventos extendidos en SQL Server](../../relational-databases/extended-events/targets-for-extended-events-in-sql-server.md). |
| action | Un campo conocido del evento. Los datos del campo se envían al destino. El campo de acción está estrechamente relacionado con el *filtro de predicado*. |
| filtro de predicado | Una prueba de datos en un campo de evento que se usa de forma que solo un subconjunto interesante de las repeticiones de evento se envíe al destino. <br/> <br/> Por ejemplo, un filtro podría incluir solo esas repeticiones del evento *sql_statement_completed* donde la instrucción T-SQL incluía la cadena *HAVING*. |
| paquete | Un calificador de nombre adjunto a cada elemento de un conjunto de elementos que se centra en torno al núcleo de los eventos. <br/> <br/> Por ejemplo, un paquete puede tener eventos sobre texto T-SQL. Un evento puede tratar todas las instrucciones T-SQL en un lote delimitado por la instrucción GO. Mientras tanto, otro evento más reducido trata sobre las instrucciones T-SQL individuales. Además, para cualquier instrucción T-SQL, existen eventos de inicio y eventos completados. <br/> <br/> Los campos apropiados para los eventos también se encuentran en el paquete con los eventos. La mayoría de los destinos se encuentran en *package0* y se usan con eventos de muchos otros paquetes. |


## <a name="how-to-discover-the-available-events-in-packages"></a>Cómo detectar los eventos disponibles en los paquetes


La siguiente instrucción SELECT de T-SQL devuelve una fila para cada evento disponible cuyo nombre contenga la cadena de tres caracteres "sql". Por supuesto, puede editar el valor LIKE para buscar diferentes nombres de evento. Las filas también denominan el paquete que contiene el evento.


```sql
SELECT   -- Find an event you want.
        p.name         AS [Package-Name],
        o.object_type,
        o.name         AS [Object-Name],
        o.description  AS [Object-Descr],
        p.guid         AS [Package-Guid]
    FROM
              sys.dm_xe_packages  AS p
        JOIN  sys.dm_xe_objects   AS o
    
                ON  p.guid = o.package_guid
    WHERE
        o.object_type = 'event'   --'action'  --'target'
        AND
        p.name LIKE '%'
        AND
        o.name LIKE '%sql%'
    ORDER BY
        p.name, o.object_type, o.name;
```


La siguiente visualización muestra la fila que se ha devuelto, editada aquí en el formato de nombre de columna = valor. Los datos provienen del evento *sql-statement_completed* que se ha usado en los pasos anteriores del ejemplo. La frase de la columna Object-Descr es particularmente útil.


```  
Package-Name = sqlserver
object_type  = event
Object-Name  = sql_statement_completed
Object-Descr = Occurs when a Transact-SQL statement has completed.
Package-Guid = 655FD93F-3364-40D5-B2BA-330F7FFB6491
```


#### <a name="ssms-ui-for-search"></a>Interfaz de usuario de SSMS para la búsqueda


Otra opción de búsqueda es usar la interfaz de usuario de SSMS en el cuadro de diálogo **Nueva sesión** > **Eventos** > **Biblioteca de eventos** que se muestra en una captura de pantalla anterior.



#### <a name="sql-trace-event-classes-with-extended-events"></a>Clases de evento de Seguimiento de SQL con eventos extendidos


Puede obtener una descripción de cómo usar eventos extendidos con las columnas y clases de evento de Seguimiento de SQL en: [Ver los eventos extendidos equivalentes a las clases de evento de Seguimiento de SQL Server](../../relational-databases/extended-events/view-the-extended-events-equivalents-to-sql-trace-event-classes.md).



#### <a name="event-tracing-for-windows-etw-with-extended-events"></a>Seguimiento de eventos para Windows (ETW) con eventos extendidos


Las descripciones de cómo usar eventos extendidos con Seguimiento de eventos para Windows (ETW) están disponibles en:

- [Seguimiento de eventos para Windows de destino](../../relational-databases/extended-events/event-tracing-for-windows-target.md)
- [Supervisar la actividad del sistema mediante eventos extendidos](../../relational-databases/extended-events/monitor-system-activity-using-extended-events.md)



Los eventos de ETW no están disponibles en los eventos extendidos de Base de datos SQL de Azure.



## <a name="additional-items"></a>Elementos adicionales


En esta sección se menciona brevemente un par de elementos varios.


### <a name="event-sessions-installed-with-sql-server"></a>Sesiones de eventos instaladas con SQL Server


SQL Server incluye algunos eventos extendidos que ya se han creado. Todos están configurados para iniciarse cuando se inicie el sistema de SQL. Estas sesiones de eventos recopilan datos que pueden resultar útiles si se produce un error del sistema. Al igual que todos los eventos extendidos, consumen solo una pequeña cantidad de recursos y Microsoft recomienda que se dejen como están para ejecutarse.

Puede ver estas sesiones de eventos en el **Explorador de objetos** de SSMS en **Administración** > **Eventos extendidos** > **Sesiones**.  En junio de 2016, la lista de estas sesiones de eventos instaladas es:

- AlwaysOn_health
- system_health
- telemetry_events



### <a name="powershell-provider-for-extended-events"></a>Proveedor de PowerShell para eventos extendidos


Puede administrar los eventos extendidos de SQL Server mediante el proveedor de SQL Server PowerShell. Puede obtener más información en: [Usar el proveedor de PowerShell para eventos extendidos](../../relational-databases/extended-events/use-the-powershell-provider-for-extended-events.md).


### <a name="system-views-for-extended-events"></a>Vistas del sistema para eventos extendidos


Las vistas del sistema para eventos extendidos incluyen:

- *Vistas de catálogo:* para obtener información sobre las sesiones de eventos que se han definido mediante CREATE EVENT SESSION.

- *Vistas de administración dinámica (DMV):* para obtener información sobre sesiones de eventos que se están ejecutando activamente en estos momentos.


[SELECTs and JOINs From System Views for Extended Events in SQL Server (Instrucciones SELECT y JOIN en vistas del sistema para eventos extendidos en SQL Server)](../../relational-databases/extended-events/selects-and-joins-from-system-views-for-extended-events-in-sql-server.md) proporciona información sobre:


- Cómo unir las vistas entre sí.


- Varias instrucciones SELECT útiles de las vistas.


- La correlación entre:
    - Las columnas de la vista.
    - Cláusulas CREATE EVENT SESSION.
    - Los controles de interfaz de usuario de SSMS.


<a name="appendix1"></a>
## <a name="appendix-selects-to-ascertain-permission-owner-in-advance"></a>Apéndice: instrucciones SELECT para averiguar el propietario del permiso por anticipado


Los permisos que se mencionan en este artículo son:

- ALTER ANY EVENT SESSION
- VIEW SERVER STATE
- CONTROL SERVER

Las siguientes instrucciones SELECT de Transact-SQL pueden notificar quién tiene estos permisos.


#### <a name="union-direct-permissions-plus-role-derived-permissions"></a>Permisos directos UNION más permisos derivados del rol


La siguiente instrucción SELECT...UNION ALL devuelve filas que muestran quién tiene los permisos necesarios para crear sesiones de eventos y consultar las vistas de catálogo del sistema de los eventos extendidos.


```sql
-- Ascertain who has the permissions listed in the ON clause.
-- 'CONTROL SERVER' permission includes the permissions
-- 'ALTER ANY EVENT SESSION' and 'VIEW SERVER STATE'.
SELECT
        'Owner-is-Principal'  AS [Type-That-Owns-Permission],
        NULL                  AS [Role-Name],
        prin.name             AS [Owner-Name],

        perm.permission_name
            COLLATE Latin1_General_CI_AS_KS_WS
            AS [Permission-Name]
    FROM
             sys.server_permissions  AS perm
        JOIN sys.server_principals   AS prin

            ON prin.principal_id = perm.grantee_principal_id
    WHERE
        perm.permission_name IN
            ('ALTER ANY EVENT SESSION',
            'VIEW SERVER STATE',
            'CONTROL SERVER')
UNION ALL

-- Plus check for members of the 'sysadmin' fixed server role,
-- because 'sysadmin' includes the 'CONTROL SERVER' permission.
SELECT
        'Owner-is-Role',
        prin.name,  -- [Role-Name]

        CAST( (IsNull(pri2.name, N'No members'))
            AS nvarchar(128)),

        NULL
    FROM
                         sys.server_role_members  AS rolm
        RIGHT OUTER JOIN sys.server_principals    AS prin

            ON prin.principal_id = rolm.role_principal_id

        LEFT OUTER JOIN sys.server_principals     AS pri2

            ON rolm.member_principal_id = pri2.principal_id
    WHERE
        prin.name = 'sysadmin'
    ORDER BY
        1,2,3,4;
```


#### <a name="haspermsbyname-function"></a>HAS_PERMS_BY_NAME, función


La siguiente instrucción SELECT notifica sus permisos. Se basa en la función integrada [HAS_PERMS_BY_NAME](../../t-sql/functions/has-perms-by-name-transact-sql.md).

Además, si tiene autoridad para *suplantar* temporalmente otras cuentas, puede quitar la marca del comentario de las instrucciones [EXECUTE AS LOGIN](../../t-sql/statements/execute-as-transact-sql.md) y REVERT para consultar otras cuentas.


```sql
--EXECUTE AS LOGIN = 'AccountNameHere';
SELECT HAS_PERMS_BY_NAME(
    null, null,
    'ALTER ANY EVENT SESSION'
    );
--REVERT;
```


#### <a name="security-links"></a>Vínculos de seguridad

Aquí se muestran vínculos a la documentación relacionada con estas instrucciones SELECT y con los permisos:

- Información de la función integrada [HAS_PERMS_BY_NAME (Transact-SQL)](../../t-sql/functions/has-perms-by-name-transact-sql.md)
- [sys.fn_my_permissions (Transact-SQL)](../../relational-databases/system-functions/sys-fn-my-permissions-transact-sql.md)
- [GRANT (permisos de servidor de Transact-SQL)](../../t-sql/statements/grant-server-permissions-transact-sql.md)
- [sys.server_principals (Transact-SQL)](http://msdn.microsoft.com/library/ms188786.aspx)
- Especialmente para Base de datos SQL de Azure, [sys.database_principals (Transact-SQL)](http://msdn.microsoft.com/library/ms187328.aspx)
- Blog: [Effective Database Engine Permissions (Permisos eficaces del motor de base de datos)](http://social.technet.microsoft.com/wiki/contents/articles/15180.effective-database-engine-permissions.aspx)
- [Póster](http://go.microsoft.com/fwlink/?LinkId=229142)que se puede acercar, en formato PDF, que muestra la jerarquía de todos los permisos de SQL Server.



## <a name="links-to-supporting-information"></a>Vínculos a información complementaria


- [sys.fn_xe_file_target_read_file (Transact-SQL)](../../relational-databases/system-functions/sys-fn-xe-file-target-read-file-transact-sql.md)


