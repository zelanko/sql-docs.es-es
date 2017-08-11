---
title: Registro de seguimiento de servicio de servidor de informes | Documentos de Microsoft
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- logs [Reporting Services], trace
- traces [Reporting Services]
- system information [Reporting Services]
- versions [Reporting Services]
ms.assetid: 2fde08b2-137d-4f4b-88e5-216030216e0d
caps.latest.revision: 52
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 37d44eeb29ad4e2acfd4f9618c755f2c5d8b9b28
ms.contentlocale: es-es
ms.lasthandoff: 08/09/2017

---
# <a name="report-server-service-trace-log"></a>Registro de seguimiento del servicio del servidor de informes
  El [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] registros de seguimiento del servidor de informes son un archivo de texto ASCII que contienen información detallada para las operaciones del servicio servidor de informes.  Ther información de los archivos se incluyen las operaciones realizadas por el servicio Web del servidor de informes, el portal web y el procesamiento en segundo plano. El archivo de registro de seguimiento incluye información redundante que contienen otros archivos de registro, así como información adicional que no está disponible en ningún otro archivo. La información del registro de seguimiento resulta útil si se está depurando una aplicación que incluye un servidor de informes o se investiga un problema específico que se ha incluido en el registro de eventos o de ejecución. Por ejemplo, cuando existen problemas con las suscripciones.  
 
##  <a name="bkmk_view_log"></a> ¿Dónde están los archivos de registro del servidor de informes?  
 Los archivos de registro de seguimiento `ReportServerService_<timestamp>.log` y `Microsoft.ReportingServices.Portal.WebHost_<timestamp>.log` y se encuentran en la siguiente carpeta:  
  
 `C:\Program Files\Microsoft SQL Server\MSRS13.MSSQLSERVER\Reporting Services\LogFiles`  
  
 Los registros de seguimiento se crean todos los días, a partir de la primera entrada que se produce después de la medianoche (hora local), y cada vez que se reinicia el servicio. La marca de tiempo se basa en la hora universal coordinada (UTC). El archivo está en formato EN-US. De forma predeterminada, los registros de seguimiento están limitados a 32 megabytes y se eliminan transcurridos 14 días.  
  
 Vea un breve vídeo que muestra el uso de Microsoft Power Query para ver archivos de registro de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
[![vea un vídeo que muestra Power Query y los archivos de registro de SSRS](../../reporting-services/report-server/media/generic-video-thumbnail.png)](https://technet.microsoft.com/library/sql-server-reporting-services-log-files-and-microsoft-power-query.aspx)  [Usar Microsoft Power Query para ver los archivos de registro de Reporting Services](https://technet.microsoft.com/library/sql-server-reporting-services-log-files-and-microsoft-power-query.aspx)
  
##  <a name="bkmk_trace_configuration_settings"></a> Configuración de seguimiento  
 Comportamiento de registro de seguimiento se administra en el archivo de configuración **ReportingServicesService.exe.config**. El archivo de configuración se encuentra en la ruta de la carpeta siguiente:  
  
 `\Program Files\Microsoft SQL Server\MSRS13.<instance name>\Reporting Services\ReportServer\bin`.  
  
 El ejemplo siguiente muestra la estructura XML de la configuración de **RStrace** . El valor de **DefaultTraceSwitch** determina el tipo de información agregada al registro. Excepto para el atributo **Components** , los valores de **RStrace** son los mismos en todos los archivos de configuración.  
  
```  
  \<system.diagnostics>
    <switches>
      <add name="DefaultTraceSwitch" value="3" />
    </switches>
  \</system.diagnostics>
  <RStrace>
    <add name="FileName" value="ReportServerService_" />
    <add name="FileSizeLimitMb" value="32" />
    <add name="KeepFilesForDays" value="14" />
    <add name="Prefix" value="appdomain, tid, time" />
    <add name="TraceListeners" value="file" />
    <add name="TraceFileMode" value="unique" />
    <add name="Components" value="all:3" />
  </RStrace>
```  
  
 En la tabla siguiente se proporciona información acerca de cada parámetro.  
  
|Configuración|Description|Valores|  
|-------------|-----------------|------------|  
|**RStrace**|Especifica espacios de nombres utilizados para errores y traza.||  
|**DefaultTraceSwitch**|Especifica el nivel de información que se incluye en el registro de seguimiento de ReportServerService. Cada nivel incluye la información proporcionada para todos los niveles inferiores. No se recomienda deshabilitar la traza.|Los valores válidos son:<br /><br /> <br /><br /> 0= Deshabilita el seguimiento. El archivo de registro ReportServerService está habilitado de forma predeterminada. Para desactivarlo, establezca el nivel de seguimiento en 0.<br /><br /> 1= Excepciones y reinicios<br /><br /> 2= Excepciones, reinicios y advertencias<br /><br /> 3= Excepciones, reinicios, advertencias y mensajes de estado (predeterminado)<br /><br /> 4= Modo detallado|  
|**FileName**|Especifica la primera parte del nombre del archivo de registro. El valor especificado en **Prefix** completa el resto del nombre.||  
|**FileSizeLimitMb**|Especifica un límite superior para el tamaño del registro de seguimiento. El tamaño del archivo se indica en megabytes.<br /><br /> Puede controlar el tamaño de archivo si establece niveles de seguimiento (de 0 a 4) para controlar cuánto contenido debe registrarse. También puede especificar los componentes a los que se realizó el seguimiento. Si se alcanza el valor máximo del archivo de registro antes de la fecha de expiración de 14 días, las entradas nuevas reemplazarán a las más antiguas.|Los valores válidos son de 0 a un número entero definido como máximo. El valor predeterminado es 32. Si especifica 0 o un número negativo, el servidor de informes trata el valor como 1.|  
|**KeepFilesForDays**|Especifica los días tras los que se elimina un archivo de registro de seguimiento.|Los valores válidos son de 0 a un número entero definido como máximo. El valor predeterminado es 14. Si especifica 0 o un número negativo, el servidor de informes trata el valor como 1.|  
|**Prefix**|Especifica un valor generado que distingue una instancia de registro de otra.|De manera predeterminada, se anexan valores de marca de tiempo a los nombres de los archivos de registro de seguimiento. Este valor se establece en "appdomain, tid, el tiempo". No modifique este parámetro.|  
|**TraceListeners**|Especifica un destino de salida para el contenido del registro de seguimiento. Se pueden especificar varios destinos separados por comas.|Los valores válidos son:<br /><br /> <br /><br /> DebugWindow<br /><br /> File (predeterminado)<br /><br /> StdOut|  
|**TraceFileMode**|Especifica si los registros de seguimiento incluyen datos de un período de 24 horas. Es recomendable tener un único registro de seguimiento para cada componente y día.|Este valor se establece en "Unique (default)". No modifique este valor.|  
|**Categoría de componentes**|Especifica los componentes para los cuales se genera la información de registro de seguimiento y el nivel de seguimiento en este formato.<br /><br /> \<categoría de componente >:\<tracelevel ><br /><br /> Puede especificar todos los componentes o algunos de ellos (**all**, **RunningJobs**, **SemanticQueryEngine**, **SemanticModelGenerator**). Si no desea generar información para un componente específico, puede deshabilitar el seguimiento para el mismo (por ejemplo, "SemanticModelGenerator:0"). No deshabilite el seguimiento para **all**.<br /><br /> Puede establecer "SemanticQueryEngine:4" si desea ver las instrucciones Transact-SQL generadas para cada consulta semántica. Las instrucciones Transact-SQL se registran en el registro de seguimiento. El ejemplo siguiente muestra el valor de configuración que agrega las instrucciones Transact-SQL al registro:<br /><br /> \<Agregar nombre = "Componentes" value = "all, semanticqueryengine: 4" / >|Las categorías de componentes se pueden establecer en:<br /><br /> <br /><br /> **All** se utiliza para realizar un seguimiento de la actividad general del servidor de informes para todos los procesos que no están divididos en las categorías específicas.<br /><br /> **RunningJobs** se usa para realizar un seguimiento de una operación de suscripción o informe en curso.<br /><br /> **SemanticQueryEngine** se usa para realizar un seguimiento de una consulta semántica procesada cuando un usuario realiza una exploración de datos ad hoc en un informe basado en un modelo.<br /><br /> **SemanticModelGenerator** se utiliza para realizar un seguimiento de generación de modelos.<br /><br /> **http** se utiliza para habilitar el archivo de registro HTTP del servidor de informes. Para obtener más información, vea [Report Server HTTP Log](../../reporting-services/report-server/report-server-http-log.md).|  
|Valor de**tracelevel** de categorías de componentes|\<categoría de componente >:\<tracelevel ><br /><br /> <br /><br /> Si no anexa un nivel de seguimiento al componente, se utiliza el valor especificado para **DefaultTraceSwitch** . Por ejemplo, si especifica "all,RunningJobs,SemanticQueryEngine,SemanticModelGenerator", todos los componentes utilizan el nivel de seguimiento predeterminado.|Los valores válidos del nivel de seguimiento son:<br /><br /> <br /><br /> 0= Deshabilita la traza<br /><br /> 1= Excepciones y reinicios<br /><br /> 2= Excepciones, reinicios y advertencias<br /><br /> 3= Excepciones, reinicios, advertencias y mensajes de estado (predeterminado)<br /><br /> 4= Modo detallado<br /><br /> El valor predeterminado del servidor de informes es "todo:3"|  
  
##  <a name="bkmk_add_custom"></a> Agregar un valor de configuración personalizado para especificar una ubicación del archivo de volcado  
 Puede agregar una configuración personalizada para establecer la ubicación que utiliza la herramienta Dr. Watson para Windows para almacenar archivos de volcado. El valor predeterminado es **Directory**. El ejemplo siguiente muestra cómo se especifica esta configuración en la sección **RStrace** :  
  
```  
<add name="Directory" value="U:\logs\" />  
```  
  
 Para obtener más información, vea el [artículo 913046 de Knowledge Base](http://support.microsoft.com/?kbid=913046) en el sitio web de Microsoft [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
##  <a name="bkmk_log_file_fields"></a> Campos del archivo de registro  
 Los registros de seguimiento contienen los siguientes archivos:  
  
-   Información del sistema, incluido el sistema operativo, la versión, el número de procesadores y la memoria.  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
-   Eventos incluidos en el registro de aplicación.  
  
-   Excepciones generadas por el servidor de informes.  
  
-   Advertencias de recursos reducidos registradas por un servidor de informes.  
  
-   Sobres SOAP entrantes y sobres SOAP salientes resumidos.  
  
-   Información de seguimiento de depuración, seguimiento de pila y encabezados HTTP.  
  
 Puede revisar los registros de información de registro para determinar si se ha llevado a cabo la entrega de un informe, quién lo recibió y cuántos intentos de entrega se realizaron. Los registros de seguimiento también incluyen información sobre la actividad de ejecución de informes y las variables de entorno que están en vigor durante el procesamiento de informes. Además, incluyen los errores y las excepciones. Por ejemplo, puede encontrar errores de tiempo de espera de informes (indicados como una entrada **ThreadAbortExceptions** ).  

## <a name="previous-versions"></a>Versiones anteriores
En versiones anteriores de [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)], hubo varios archivos de registro de seguimiento, uno para cada aplicación. Los siguientes archivos están desusados y ya no se crean en [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ni en las versiones posteriores.
+ ReportServerWebApp_*\<timestamp >*.log
+ ReportServer_*\<timestamp >*.log
+ ReportServerService_main_*\<timestamp >*.log
  
## <a name="see-also"></a>Vea también  
 [Los archivos de registro y orígenes de Reporting](../../reporting-services/report-server/reporting-services-log-files-and-sources.md)   
 [Errores y eventos referencia &#40; Reporting Services &#41;](../../reporting-services/troubleshooting/errors-and-events-reference-reporting-services.md)  
 ¿Más preguntas? [Pruebe el foro de Reporting Services](http://go.microsoft.com/fwlink/?LinkId=620231)
  

