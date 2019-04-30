---
title: Opción Replay (herramienta de administración de Distributed Replay) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
ms.assetid: d7bce6a5-d414-488d-a3cd-50c1c62019c4
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 5a709d4badbd270d9ddffedd62ff040e8ca6c628
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63149469"
---
# <a name="replay-option-distributed-replay-administration-tool"></a>Opción Replay (herramienta de administración de Distributed Replay)
  El [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] herramienta de administración de Distributed Replay, `DReplay.exe`, es una herramienta de línea de comandos que puede usar para comunicarse con distributed replay controller. En este tema se describe la opción de la línea de comandos **replay** y la sintaxis correspondiente.  
  
 La opción **replay** inicia la fase de reproducción de eventos, en la que el controlador envía los datos de reproducción a los clientes especificados, inicia la reproducción distribuida y sincroniza los clientes. Opcionalmente, cada cliente que participa en la reproducción puede grabar la actividad de reproducción y guardar un archivo de seguimiento del resultado localmente.  
  
 ![Icono de vínculo de tema](../../database-engine/media/topic-link.gif "Icono de vínculo de tema") Para obtener más información sobre las convenciones de sintaxis que se usan con la sintaxis de la herramienta de administración, vea [Convenciones de sintaxis de Transact-SQL &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/transact-sql-syntax-conventions-transact-sql).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
      dreplay replay [-mcontroller] -dcontroller_working_dir [-o]  
    [-starget_server] -wclients [-cconfig_file]  
    [-fstatus_interval]  
```  
  
#### <a name="parameters"></a>Parámetros  
 **-m** *controller*  
 Especifica el nombre del equipo que se va a controlar. Puede utilizar "`localhost`" o "`.`" para hacer referencia al equipo local.  
  
 Si no se especifica el parámetro **-m** , se usará el equipo local.  
  
 **-d** *controller_working_dir*  
 Especifica el directorio del controlador donde se almacenará el archivo intermedio. El parámetro **-d** es obligatorio.  
  
 Se aplican los siguientes requisitos:  
  
-   El directorio debe residir en el controlador.  
  
-   Debe especificar la ruta de acceso completa, comenzando por una letra de unidad (por ejemplo, `c:\WorkingDir`).  
  
-   La ruta de acceso no debe finalizar con una barra diagonal inversa "`\`".  
  
-   No se admiten las rutas de acceso UNC.  
  
 **-o**  
 Captura la actividad de reproducción de los clientes y la guarda en un archivo de seguimiento de resultados en la ruta de acceso especificada por el elemento `<ResultDirectory>` en el archivo de configuración del cliente, `DReplayClient.xml`.  
  
 Cuando no se especifica el parámetro **-o**, no se genera el archivo de seguimiento de resultados. La salida de la consola devuelve información de resumen al final de la reproducción, pero no hay ninguna otra estadística de reproducción disponible.  
  
 **-s** *target_server*  
 Especifica la instancia de destino de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] en la que se debería volver a reproducir la carga de trabajo distribuida. Debe especificar este parámetro con el formato **nombre_servidor[\nombre de instancia]**.  
  
 No se puede utilizar "`localhost`" ni "`.`" como servidor de destino.  
  
 El parámetro **-s** no es necesario si se especifica el elemento `<Server>` en la sección `<ReplayOptions>` del archivo de configuración de reproducción, `DReplay.exe.replay.config`.  
  
 Si se usa el parámetro **-s** , se omitirá el elemento `<Server>` de la sección `<ReplayOptions>` del archivo de configuración de reproducción.  
  
 **-w** *clients*  
 Este parámetro obligatorio es una lista separada por comas (sin espacios) que especifica los nombres de equipo de clientes que deberían participar en la reproducción distribuida. No se permiten direcciones IP. Tenga en cuenta que los clientes ya deben estar registrados con el controlador.  
  
> [!NOTE]  
>  Cada cliente se registra con el controlador especificado en el archivo de configuración del cliente cuando se inicia el servicio del cliente.  
  
 **-c** *config_file*  
 Es la ruta de acceso completa del archivo de configuración de reproducción; se usa para especificar la ubicación cuando está almacenado en una ubicación diferente.  
  
 No se requiere el parámetro **-c** si pretende usar los valores predeterminados del archivo de configuración de reproducción, `DReplay.exe.replay.config`.  
  
 **-f** *status_interval*  
 Especifica la frecuencia (en segundos) con la que se muestra el estado.  
  
 Si no se especifica **-f** , el intervalo predeterminado es de 30 segundos.  
  
## <a name="examples"></a>Ejemplos  
 En este ejemplo, la reproducción distribuida deriva gran parte de su comportamiento de un archivo de configuración de reproducción modificado, `DReplay.exe.replay.config`.  
  
-   El parámetro **-m** especifica que un equipo denominado `controller1` actúa como controlador. Se debe especificar el nombre de equipo cuando el servicio del controlador se está ejecutando en un equipo diferente.  
  
-   El parámetro **-d** especifica la ubicación del archivo intermedio en el controlador, `c:\WorkingDir`.  
  
-   El parámetro **-o** establece que cada cliente especificado captura la actividad de reproducción y la guarda en un archivo de seguimiento de resultados. Nota: El elemento `<ResultTrace>` del archivo de configuración se puede usar para especificar si se registran el recuento de filas y el conjunto de resultados.  
  
-   El parámetro **-w** especifica que los equipos de `client1` a `client4` participan como clientes en la reproducción distribuida.  
  
-   El parámetro **-c** se usa para apuntar al archivo de configuración modificado, `DReplay.exe.replay.config`.  
  
-   El parámetro **-s** no es necesario porque el elemento `<Server>` se especifica en el elemento `<ReplayOptions>` del archivo de configuración de reproducción, `DReplay.exe.replay.config`.  
  
 La fase de reproducción de eventos se inicia con la siguiente sintaxis cuando la herramienta de administración se ejecuta en un equipo diferente al controlador:  
  
```  
dreplay replay -m controller1 -d c:\WorkingDir -o -w client1,client2,client3,client4 -c c:\DReplay.exe.replay.config  
```  
  
 Para especificar un modo secuenciación sincrónico, el elemento `<SequencingMode>` del archivo `DReplay.exe.replay.config` se establece igual que el valor `synchronization`. La sección `<ResultTrace>` del archivo de configuración de reproducción se modifica para especificar que se registre el recuento de filas. Estos cambios se muestran en el siguiente ejemplo de XML:  
  
```  
<?xml version='1.0'?>  
<Options>  
    <ReplayOptions>  
        <Server>server_name\replay_target_instance</Server>  
        <SequencingMode>synchronization</SequencingMode>  
        <ConnectTimeScale></ConnectTimeScale>  
        <ThinkTimeScale></ThinkTimeScale>  
        <HealthmonInterval>60</HealthmonInterval>  
        <QueryTimeout>3600</QueryTimeout>  
        <ThreadsPerClient></ThreadsPerClient>  
    </ReplayOptions>  
    <OutputOptions>  
        <ResultTrace>  
            <RecordRowCount>Yes</RecordRowCount>  
            <RecordResultSet>No</RecordResultSet>  
        </ResultTrace>  
    </OutputOptions>  
</Options>  
```  
  
 Para especificar un modo de secuenciación de esfuerzo, el elemento `<SequencingMode>` del archivo `DReplay.exe.replay.config` se establece igual que el valor `stress`. Los elementos `<ConnectTimeScale>` y `<ThinkTimeScale>` se establecen en el valor `50` (para especificar el 50 por ciento). Para obtener más información sobre el tiempo de conexión y tiempo de reflexión, vea [Configure Distributed Replay](configure-distributed-replay.md). Estos cambios se muestran en el siguiente ejemplo de XML:  
  
```  
<?xml version='1.0'?>  
<Options>  
    <ReplayOptions>  
        <Server>server_name\replay_target_instance_name</Server>  
        <SequencingMode>stress</SequencingMode>  
        <ConnectTimeScale>50</ConnectTimeScale>  
        <ThinkTimeScale>50</ThinkTimeScale>  
        <HealthmonInterval>60</HealthmonInterval>  
        <QueryTimeout>3600</QueryTimeout>  
        <ThreadsPerClient></ThreadsPerClient>  
    </ReplayOptions>  
    <OutputOptions>  
        <ResultTrace>  
            <RecordRowCount>Yes</RecordRowCount>  
            <RecordResultSet>No</RecordResultSet>  
        </ResultTrace>  
    </OutputOptions>  
</Options>  
```  
  
## <a name="permissions"></a>Permisos  
 Debe ejecutar la herramienta de administración como un usuario interactivo, como un usuario local o una cuenta de usuario de dominio. Para utilizar una cuenta de usuario local, la herramienta de administración y el controlador se deben estar ejecutando en el mismo equipo.  
  
 Para más información, consulte [Distributed Replay Security](distributed-replay-security.md).  
  
## <a name="see-also"></a>Vea también  
 [Reproducir datos de seguimiento](replay-trace-data.md)   
 [Revisar los resultados de la reproducción](review-the-replay-results.md)   
 [SQL Server Distributed Replay](sql-server-distributed-replay.md)   
 [Configure Distributed Replay](configure-distributed-replay.md)   
 [Foro de SQL Server Distributed Replay](https://social.technet.microsoft.com/Forums/sl/sqldru/)   
 [Usar Distributed Replay para la prueba de carga de SQL Server, parte 2](https://blogs.msdn.com/b/mspfe/archive/2012/11/14/using-distributed-replay-to-load-test-your-sql-server-part-2.aspx)   
 [Usar Distributed Replay para la prueba de carga de SQL Server, parte 1](https://blogs.msdn.com/b/mspfe/archive/2012/11/08/using-distributed-replay-to-load-test-your-sql-server-part-1.aspx)  
  
  
