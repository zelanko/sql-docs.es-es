---
title: Registro HTTP del servidor de informes | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- HTTP [Reporting Services]
ms.assetid: 6cc433b7-165c-4b16-9034-79256dd6735f
caps.latest.revision: 15
author: markingmyname
ms.author: maghan
manager: mblythe
ms.openlocfilehash: 83d48cf33405988c9aedaceccc677ee238a7ea5e
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36107129"
---
# <a name="report-server-http-log"></a>Registro HTTP del servidor de informes
  Los archivos de registro HTTP del servidor de informes de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] mantienen un registro de cada solicitud y respuesta HTTP administradas por el servidor de informes. Dado que los errores de desbordamiento y de tiempo de espera de la solicitud no alcanzan el servidor de informes, no se graban en el archivo de registro.  
  
 El registro HTTP está deshabilitado de forma predeterminada. Para habilitar el registro HTTP, modifique el archivo de configuración **ReportingServicesService.exe.config** para utilizar esta característica en su instalación.  
  
## <a name="viewing-log-information"></a>Ver la información del registro  
 El registro es un archivo de texto ASCII. Para ver el archivo se puede usar cualquier editor de texto. El archivo de registro HTTP del servidor de informes es equivalente al archivo de registro extendido W3C de IIS y utiliza campos similares para que pueda utilizar los visores del archivo de registro de IIS existentes con el fin de leer el archivo de registro HTTP del servidor de informes. La tabla siguiente proporciona información adicional sobre el archivo de registro HTTP:  
  
|||  
|-|-|  
|**Nombre de archivo**|De forma predeterminada, los nombres de los archivos de registro son<br /><br /> `ReportServerService_HTTP_<timestamp>.log.`<br /><br /> Puede personalizar el prefijo del nombre de archivo si modifica el atributo HttpTraceFileName en el archivo ReportingServicesService.exe.config. La marca de tiempo se basa en la hora universal coordinada (UTC).|  
|**Ubicación del archivo**|Los archivos se escriben en la siguiente ubicación:<br /><br /> `\Microsoft SQL Server\<SQL Server Instance>\Reporting Services\LogFiles`|  
|**Formato de archivo**|El archivo está en formato EN-US. Es un archivo de texto ASCII.|  
|**Creación de archivos y retención**|El registro HTTP se crea tras habilitarlo en el archivo de configuración, de reiniciar el servicio y de que el servidor de informes procese una solicitud HTTP. Si configura los valores pero no ve el archivo de registro, abra un informe o inicie una aplicación de servidor de informes (como el Administrador de informes) para generar una solicitud HTTP y crear el archivo.<br /><br /> Se creará una nueva instancia del archivo de registro después de cada reinicio del servicio y de la solicitud HTTP subsiguiente al servidor de informes.<br /><br /> De manera predeterminada, los registros de seguimiento están limitados a 32 megabytes y se eliminan transcurridos 14 días.|  
  
## <a name="configuration-settings-for-report-server-http-log"></a>Parámetros de configuración para el registro HTTP del servidor de informes  
 Para configurar el registro HTTP del servidor de informes, utilice el Bloc de notas para modificar el archivo **ReportingServicesService.exe.config** . El archivo de configuración se encuentra en la carpeta \Archivos de programa\Microsoft SQL Server\MSSQL.n\Reporting Services\ReportServer\Bin.  
  
 Para habilitar el servidor HTTP, agregue `http:4` a la sección RStrace del archivo ReportingServicesService.exe.config. Las restantes entradas del archivo de registro HTTP son opcionales. El ejemplo siguiente incluye todos los valores para que pueda pegar la sección entera sobre la sección RStrace y, a continuación, eliminar los valores que no sean necesarios.  
  
```  
   <RStrace>  
         <add name="FileName" value="ReportServerService_" />  
         <add name="FileSizeLimitMb" value="32" />  
         <add name="KeepFilesForDays" value="14" />  
         <add name="Prefix" value="tid, time" />  
         <add name="TraceListeners" value="debugwindow, file" />  
         <add name="TraceFileMode" value="unique" />  
         <add name="HttpTraceFileName" value="ReportServerService_HTTP_" />  
         <add name="HttpTraceSwitches" value="date,time, clientip,username,serverip,serverport,host,method,uristem,uriquery,protocolstatus,bytesreceived,timetaken,protocolversion,useragent,cookiereceived,cookiesent,referrer" />  
         <add name="Components" value="all:3,http:4" />  
   </RStrace>  
```  
  
## <a name="log-file-fields"></a>Campos del archivo de registro  
 En la tabla siguiente se describen los campos disponibles en el registro. La lista de campos es configurable; puede especificar qué campos desea incluir mediante el `HTTPTraceSwitches` de configuración. El **predeterminado** columna indica si el campo se incluirá en el archivo de registro automáticamente si no se especifica `HTTPTraceSwitches`.  
  
|Campo|Descripción|Valor predeterminado|  
|-----------|-----------------|-------------|  
|HttpTraceFileName|Este valor es opcional. El valor predeterminado es ReportServerServiceHTTP_. Puede especificar un valor diferente si desea utilizar una convención de nomenclatura de archivos diferente (por ejemplo, para incluir el nombre de servidor si guarda los archivos de registro en una ubicación central).|Sí|  
|HTTPTraceSwitches|Este valor es opcional. Si lo especifica, puede configurar los campos utilizados en el archivo de registro con un formato separado por comas.|no|  
|date|Fecha en que se produjo la actividad.|no|  
|Time|Hora en que se produjo la actividad.|no|  
|ClientIp|Dirección IP del cliente que tiene acceso al servidor de informes.|Sí|  
|UserName|Nombre del usuario que tuvo acceso al servidor de informes.|no|  
|ServerPort|Número de puerto utilizado para la conexión.|no|  
|Host|Contenido del encabezado de host.|no|  
|Método|Acción o método SOAP llamado desde el cliente.|Sí|  
|UriStem|Recurso al que se obtuvo acceso.|Sí|  
|UriQuery|Consulta utilizada para tener acceso al recurso.|no|  
|ProtocolStatus|Código de estado HTTP.|Sí|  
|BytesReceived|Número de bytes recibidos por el servidor.|no|  
|TimeTaken|Tiempo transcurrido (en milisegundos) desde que el HTTP.SYS instantáneo devuelve los datos de la solicitud hasta que el servidor finaliza el último envío, excluido el tiempo de transmisión por la red.|no|  
|ProtocolVersion|Versión de protocolo utilizada por el cliente.|no|  
|UserAgent|Tipo de explorador utilizado por el cliente.|no|  
|CookieReceived|Contenido de la cookie recibida por el servidor.|no|  
|CookieSent|Contenido de la cookie enviada por el servidor.|no|  
|Referrer|Sitio anterior visitado por el cliente.|no|  
  
## <a name="see-also"></a>Vea también  
 [Registro de seguimiento de servicio de servidor de informes](report-server-service-trace-log.md)   
 [Archivos de registro y orígenes de Reporting Services](../report-server/reporting-services-log-files-and-sources.md)   
 [Referencia de errores y eventos &#40;Reporting Services&#41;](../troubleshooting/errors-and-events-reference-reporting-services.md)  
  
  