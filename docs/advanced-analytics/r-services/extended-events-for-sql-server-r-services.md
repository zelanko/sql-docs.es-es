---
title: "Eventos extendidos para SQL Server R Services | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "11/29/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 4e90e057-aacb-4adc-8da6-64861f4e87df
caps.latest.revision: 13
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 12
---
# Eventos extendidos para SQL Server R Services
  [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] Proporciona un conjunto de eventos extendidos que podrá usar para solucionar problemas de operaciones relacionadas con la [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] o trabajos de R enviados a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Para ver una lista de los eventos relacionados con SQL Server, ejecute la siguiente consulta en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
```  
select o.name as event_name, o.description  
  from sys.dm_xe_objects o  
  join sys.dm_xe_packages p  
    on o.package_guid = p.guid  
 where o.object_type = 'event'  
   and p.name = 'SQLSatellite';  
```  
  
 Sin embargo, algunos eventos extendidos adicionales para [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] solo se activan desde procesos externos, como [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)]y BXLServer, el proceso subsidiario que inicia el runtime de R. Para obtener más información sobre cómo capturar estos eventos, consulte [Collecting Events from External Processes](#bkmk_externalevents).  
  
 Para obtener información general sobre el uso de los eventos extendidos, consulte [SQL Server Extended Events Sessions](../../relational-databases/extended-events/sql-server-extended-events-sessions.md).  

  
##  <a name="a-namebkmkxeventtablea-table-of-extended-events"></a><a name="bkmk_xeventtable"></a> Tabla de eventos extendidos  
  
|Evento|Descripción|Utilice|  
|-----------|-----------------|---------|  
|connection_accept|Se produce cuando se acepta una conexión nueva. Este evento sirve para registrar todos los intentos de conexión.||  
|failed_launching|Error de inicio.|Indica un error.|  
|satellite_abort_connection|Anula el registro de conexión.||  
|satellite_abort_received|Se activa cuando se recibe un mensaje de anulación por una conexión subsidiaria.||  
|satellite_abort_sent|Se activa cuando se envía un mensaje de anulación a través de una conexión subsidiaria.||  
|satellite_authentication_completion|Se activa cuando se completa la autenticación para una conexión a través de TCP o una canalización con nombre.||  
|satellite_authorization_completion|Se activa cuando se completa la autorización para una conexión a través de TCP o una canalización con nombre.||  
|satellite_cleanup|Se activa cuando la instancia subsidiaria llama a la instrucción de limpieza.|Se activa solo desde procesos externos. Consulte las instrucciones sobre la colección de eventos desde procesos externos.|  
|satellite_data_chunk_sent|Se activa cuando la conexión subsidiaria termina de enviar un único fragmento de datos.|El evento notifica el número de filas en la que se envían, el número de columnas, el número de SNI paquetes usedm y el tiempo transcurrido en milisegundos al enviar el fragmento. La información puede ayudarle a entender cuánto tiempo se dedicó pasando distintos tipos de datos, y se usa el número de paquetes.|  
|satellite_data_receive_completion|Se activa cuando se reciben todos los datos que necesita una consulta a través de una conexión subsidiaria.|Se activa solo desde procesos externos. Consulte las instrucciones sobre la colección de eventos desde procesos externos.|  
|satellite_data_send_completion|Se activa cuando se envían todos los datos necesarios para una sesión a través de la conexión subsidiaria.||  
|satellite_data_send_start|Se activa cuando se inicia la transmisión de datos (justo antes de enviar el primer fragmento de datos).||  
|satellite_error|Se utiliza para realizar un seguimiento de un error en una instancia subsidiaria de SQL.||  
|satellite_invalid_sized_message|El tamaño del mensaje no es válido.||  
|satellite_message_coalesced|Se utiliza para realizar un seguimiento de la fusión de mensajes en la capa de red.||  
|satellite_message_ring_buffer_record|Registro de búfer en anillo del mensaje.||  
|satellite_message_summary|Información de resumen sobre la mensajería.||  
|satellite_message_version_mismatch|El campo de la versión del mensaje no coincide.||  
|satellite_messaging|Se utiliza para realizar un seguimiento de eventos de mensajería (vincular, desvincular, etc.).||  
|satellite_partial_message|Se utiliza para realizar un seguimiento de los mensajes parciales en la capa de red.||  
|satellite_schema_received|Se activa cuando SQL recibe y lee un mensaje de esquema.||  
|satellite_schema_sent|Se activa cuando se envía un mensaje de esquema a través de la conexión subsidiaria.|Se activa solo desde procesos externos. Consulte las instrucciones sobre la colección de eventos desde procesos externos.|  
|satellite_service_start_posted|Se activa cuando se publica en Launchpad un mensaje de inicio de servicio.|Así se indica a Launchpad que inicie el proceso externo y contiene un id. para la nueva sesión.|  
|satellite_unexpected_message_received|Se activa cuando se recibe un mensaje inesperado.|Indica un error.|  
|stack_trace|Se produce cuando se solicita un volcado de memoria del proceso.|Indica un error.|  
|trace_event|Se utiliza para realizar el seguimiento.|Estos eventos pueden contener mensajes de seguimiento de procesos externos, de Launchpad y de SQL Server. Se incluyen las salidas a stdout y stderr de R.|  
|launchpad_launch_start|Se activa cuando Launchpad empieza a iniciar una instancia subsidiaria.|Solo se activa desde Launchpad. Consulte las instrucciones sobre la recopilación de eventos desde launchpad.exe.|  
|launchpad_resume_sent|Se activa cuando Launchpad ha iniciado la instancia subsidiaria y enviado un mensaje de reanudación a SQL Server.|Solo se activa desde Launchpad. Consulte las instrucciones sobre la recopilación de eventos desde launchpad.exe.|  
|satellite_data_chunk_sent|Se activa cuando la conexión subsidiaria termina de enviar un único fragmento de datos.|Contiene información sobre el número de columnas, de filas y de paquetes, así como del tiempo necesitado para enviar el fragmento.|  
|satellite_sessionId_mismatch|No se esperaba el id. de sesión del mensaje.||  
  
###  <a name="a-namebkmkexternaleventsa-collecting-events-from-external-processes"></a><a name="bkmk_externalevents"></a> Recopilación de eventos desde procesos externos  
 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] inicia algunos servicios que se ejecutan fuera del proceso de SQL Server. Para capturar los eventos relacionados con estos procesos externos, debe crear un archivo de configuración de seguimiento de ingresos y colocarlo en el mismo directorio que el ejecutable del proceso.  
  
-   **[!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)]**   
  
     Para capturar los eventos relacionados con Launchpad, coloque la *config* archivo en el directorio Binn de la instancia de SQL Server.  En una instalación predeterminada, esto sería:   `C:\Program Files\Microsoft SQL Server\MSSQL_version_number.MSSQLSERVER\MSSQL\Binn`.  
  
-   **BXLServer** es el proceso subsidiario que respalda la extensibilidad SQL con R y otros lenguajes de script externo.  
  
     Para capturar los eventos relacionados con BXLServer, coloque la *config* archivo en el directorio de instalación de R.  En una instalación predeterminada, esto sería:   `C:\Program Files\Microsoft SQL Server\MSSQL_version_number.MSSQLSERVER\R_SERVICES\library\RevoScaleR\rxLibs\x64`.  
  
> [!IMPORTANT]   El archivo de configuración se debe llamar igual que el ejecutable, con el formato “[nombre].xevents.xml”. Dicho de otro modo, los archivos deben tener el siguiente nombre:  
>   
> - Launchpad.xevents.xml  
> - bxlserver.xevents.xml  
  
 El propio archivo de configuración presenta el siguiente formato:  
  
```  
<?xml version="1.0" encoding="utf-8"?>  
<event_sessions>  
<event_session name="[session name]" maxMemory="1" dispatchLatency="1" MaxDispatchLatency="2 SECONDS">  
    <description owner="you">Xevent for launchpad or bxl server.</description>  
    <event package="SQLSatellite" name="[XEvent Name 1]" />  
    <event package="SQLSatellite" name="[XEvent Name 2]" />  
    <target package="package0" name="event_file">  
      <parameter name="filename" value="[SessionName].xel" />  
      <parameter name="max_file_size" value="10" />  
      <parameter name="max_rollover_files" value="10" />  
    </target>  
  </event_session>  
</event_sessions>  
  
```  
  
 **Notas:**  
  
-   Para configurar el seguimiento, edite el *nombre de la sesión* marcador de posición, el marcador de posición para el nombre de archivo (`[SessionName].xel`) y los nombres de los eventos que desee capturar (como `[XEvent Name 1]`, `[XEvent Name 1]`).  
  
-   Cualquier número de `event package` etiquetas puede parecer y se recopilarán siempre que el atributo name sea correcto.  
  
### <a name="example-capturing-launchpad-events"></a>Ejemplo: Captura de eventos de Launchpad  
 En el siguiente ejemplo se muestra la definición de un seguimiento de eventos para el servicio Launchpad.  
  
```  
<?xml version="1.0" encoding="utf-8"?>  
<event_sessions>  
<event_session name="sqlsatelliteut" maxMemory="1" dispatchLatency="1" MaxDispatchLatency="2 SECONDS">  
    <description owner="hay">Xevent for sql tdd runner.</description>  
    <event package="SQLSatellite" name="launchpad_launch_start" />  
    <event package="SQLSatellite" name="launchpad_resume_sent" />  
    <target package="package0" name="event_file">  
      <parameter name="filename" value="launchpad_session.xel" />  
      <parameter name="max_file_size" value="10" />  
      <parameter name="max_rollover_files" value="10" />  
    </target>  
  </event_session>  
</event_sessions>  
  
```  
  
 **Notas:**  
  
-   Lugar la *config* archivo en el directorio Binn de la instancia de SQL Server.  
  
-   Este archivo se debe llamar *Launchpad.xevents.xml*.  
  
### <a name="example-capturing-bxlserver-events"></a>Ejemplo: Captura de eventos de BXLServer  
 En el siguiente ejemplo se muestra la definición de un seguimiento de eventos para el ejecutable BXLServer.  
  
```  
<?xml version="1.0" encoding="utf-8"?>  
<event_sessions>  
 <event_session name="sqlsatelliteut" maxMemory="1" dispatchLatency="1" MaxDispatchLatency="2 SECONDS">  
    <description owner="hay">Xevent for sql tdd runner.</description>  
    <event package="SQLSatellite" name="satellite_abort_received" />  
    <event package="SQLSatellite" name="satellite_authentication_completion" />  
    <event package="SQLSatellite" name="satellite_cleanup" />  
    <event package="SQLSatellite" name="satellite_data_receive_completion" />  
    <event package="SQLSatellite" name="satellite_data_send_completion" />  
    <event package="SQLSatellite" name="satellite_data_send_start" />  
    <event package="SQLSatellite" name="satellite_schema_sent" />   
    <event package="SQLSatellite" name="satellite_unexpected_message_received" />    
    <event package="SQLSatellite" name="satellite_data_chunk_sent" />   
    <target package="package0" name="event_file">  
      <parameter name="filename" value="satellite_session.xel" />  
      <parameter name="max_file_size" value="10" />  
      <parameter name="max_rollover_files" value="10" />  
    </target>  
  </event_session>  
</event_sessions>  
  
```  
  
 **Notas:**  
  
-   Lugar la *config* archivo en el mismo directorio que el ejecutable BXLServer.  
  
-   Este archivo se debe llamar *bxlserver.xevents.xml*.  
  
## <a name="see-also"></a>Vea también
[Informes de administración personalizado Studio para R Services](../../advanced-analytics/r-services/monitor-r-services-using-custom-reports-in-management-studio.md)  
 [SQL Server R Services](../../advanced-analytics/r-services/sql-server-r-services.md)   
 [Administración y supervisión de soluciones en R](../../advanced-analytics/r-services/managing-and-monitoring-r-solutions.md)  
  
  