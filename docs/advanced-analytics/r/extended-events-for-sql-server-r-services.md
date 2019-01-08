---
title: Eventos extendidos para la supervisión de procesos de R y Python - SQL Server Machine Learning Services
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: aefc4fd3ba5fa1ba69e8e29575037f5e7ac6789a
ms.sourcegitcommit: ee76332b6119ef89549ee9d641d002b9cabf20d2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/20/2018
ms.locfileid: "53644884"
---
# <a name="extended-events-for-sql-server-machine-learning-services"></a>Eventos extendidos para SQL Server Machine Learning Services
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

SQL Server proporciona un conjunto de eventos extendidos que podrá usar para solucionar problemas de las operaciones relacionadas con la [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)], así como Python o R trabajos enviados a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].

**Se aplica a:**  SQL Server 2016 R Services, SQL Server 2017 Machine Learning Services

## <a name="sql-server-events-for-machine-learning"></a>Eventos de SQL Server para el aprendizaje automático

Para ver una lista de los eventos relacionados con SQL Server, ejecute la siguiente consulta en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].

```sql
SELECT o.name AS event_name, o.description
FROM sys.dm_xe_objects o
JOIN sys.dm_xe_packages p
ON o.package_guid = p.guid
WHERE o.object_type = 'event'
AND p.name = 'SQLSatellite';
```

Para obtener información general sobre el uso de eventos extendidos, vea [herramientas de eventos extendidos](https://docs.microsoft.com/sql/relational-databases/extended-events/extended-events-tools).

> [!TIP]
> Evento extendido generados por SQL Server, pruebe la nueva [SSMS XEvent profiler](https://docs.microsoft.com/sql/relational-databases/extended-events/use-the-ssms-xe-profiler). Esta nueva característica en Management Studio muestra un visor de eventos extendidos en vivo y es menos intrusiva para SQL Server que un seguimiento de Profiler similar.

## <a name="additional-events-specific-to-machine-learning-components"></a>Eventos adicionales específicos de componentes de aprendizaje automático

Eventos extendidos adicionales están disponibles para los componentes que están relacionados con y usa SQL Server Machine Learning Services, como la [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)]y BXLServer, el proceso subsidiario que inicia el runtime de R. Estos eventos extendidos adicionales se activan desde los procesos externos y, por tanto, se deben capturar mediante una herramienta externa.

Para obtener más información acerca de cómo hacerlo, vea la sección [recopilar eventos desde procesos externos](#bkmk_externalevents).

##  <a name="bkmk_xeventtable"></a> Tabla de eventos extendidos

|Evento|Descripción|Notas|  
|-----------|-----------------|---------|  
|connection_accept|Se produce cuando se acepta una conexión nueva. Este evento sirve para registrar todos los intentos de conexión.||  
|failed_launching|Error de inicio.|Indica un error.|  
|satellite_abort_connection|Anula el registro de conexión.||  
|satellite_abort_received|Se activa cuando se recibe un mensaje de anulación por una conexión subsidiaria.||  
|satellite_abort_sent|Se activa cuando se envía un mensaje de anulación a través de una conexión subsidiaria.||  
|satellite_authentication_completion|Se activa cuando se completa la autenticación para una conexión a través de TCP o una canalización con nombre.||  
|satellite_authorization_completion|Se activa cuando se completa la autorización para una conexión a través de TCP o una canalización con nombre.||  
|satellite_cleanup|Se activa cuando la instancia subsidiaria llama a la instrucción de limpieza.|Se activa solo desde procesos externos. Consulte las instrucciones sobre la colección de eventos desde procesos externos.|  
|satellite_data_chunk_sent|Se activa cuando la conexión subsidiaria termina de enviar un único fragmento de datos.|El evento notifica el número de filas enviadas, el número de columnas, el número de paquetes SNI usados y el tiempo transcurrido en milisegundos al enviar el fragmento. La información puede ayudarle a comprender cuánto tiempo se dedicó a pasar distintos tipos de datos, y cuántos paquetes se usaron.|  
|satellite_data_receive_completion|Se activa cuando se reciben todos los datos que necesita una consulta a través de una conexión subsidiaria.|Se activa solo desde procesos externos. Consulte las instrucciones sobre la colección de eventos desde procesos externos.|  
|satellite_data_send_completion|Se activa cuando se envían todos los datos necesarios para una sesión a través de la conexión subsidiaria.||  
|satellite_data_send_start|Se desencadena cuando se inicia la transmisión de datos.| Transmisión de datos se inicia antes de que se envía el primer fragmento de datos.|  
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
  
###  <a name="bkmk_externalevents"></a> Recopilar eventos desde procesos externos

SQL Server Machine Learning Services inicia algunos servicios que se ejecutan fuera del proceso de SQL Server. Para capturar los eventos relacionados con estos procesos externos, debe crear un archivo de configuración de seguimiento de eventos y coloque el archivo en el mismo directorio que el ejecutable del proceso.  
  
+ **[!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)]**   
  
    Para capturar los eventos relacionados con Launchpad, coloque el archivo *.config* en el directorio Binn de la instancia de SQL Server.  En una instalación predeterminada, esto sería:

    `C:\Program Files\Microsoft SQL Server\MSSQL_version_number.MSSQLSERVER\MSSQL\Binn`   
  
+ **BXLServer** es el proceso subsidiario que respalda la extensibilidad SQL con los lenguajes de script externos, como R o Python. Se inicia una instancia independiente de BxlServer para cada instancia de lenguaje externo.
  
    Para capturar los eventos relacionados con BXLServer, coloque el *.config* archivo en el directorio de instalación de R o Python.  En una instalación predeterminada, esto sería:
     
    **R:** `C:\Program Files\Microsoft SQL Server\MSSQL_version_number.MSSQLSERVER\R_SERVICES\library\RevoScaleR\rxLibs\x64`.  

    **Python:** `C:\Program Files\Microsoft SQL Server\MSSQL_version_number.MSSQLSERVER\PYTHON_SERVICES\library\RevoScaleR\rxLibs\x64`.

El archivo de configuración debe ser el mismo nombre que el ejecutable, mediante el formato "[nombre] xevents". Dicho de otro modo, los archivos deben tener el siguiente nombre:

+ `Launchpad.xevents.xml`
+ `bxlserver.xevents.xml`

El propio archivo de configuración presenta el siguiente formato:

```xml
\<?xml version="1.0" encoding="utf-8"?>  
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

+ Para configurar el seguimiento, edite el *nombre de la sesión* marcador de posición, el marcador de posición para el nombre de archivo (`[SessionName].xel`) y los nombres de los eventos que desee capturar, por ejemplo, `[XEvent Name 1]`, `[XEvent Name 1]`).  
+ Puede aparecer cualquier número de etiquetas de paquete de eventos y se recopilarán siempre que el atributo name sea correcto.

### <a name="example-capturing-launchpad-events"></a>Ejemplo: Captura de eventos de Launchpad

El ejemplo siguiente muestra la definición de un seguimiento de eventos para el servicio Launchpad:

```xml
\<?xml version="1.0" encoding="utf-8"?>  
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

+ Coloque el archivo *.config* en el directorio Binn de la instancia de SQL Server.
+ Este archivo debe denominarse `Launchpad.xevents.xml`.

### <a name="example-capturing-bxlserver-events"></a>Ejemplo: Captura de eventos de BXLServer  

En el siguiente ejemplo se muestra la definición de un seguimiento de eventos para el ejecutable BXLServer.
  
```xml
\<?xml version="1.0" encoding="utf-8"?>  
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

+ Coloque el archivo *.config* en el mismo directorio que el ejecutable BXLServer.
+ Este archivo debe denominarse `bxlserver.xevents.xml`.

## <a name="see-also"></a>Vea también

[Informes de Studio personalizado administración de Machine Learning Services](../../advanced-analytics/r/monitor-r-services-using-custom-reports-in-management-studio.md)
