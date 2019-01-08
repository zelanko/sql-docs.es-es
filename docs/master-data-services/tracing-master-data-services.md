---
title: Seguimiento (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: 45823fc8-723a-49f2-9a11-94d241245cfd
author: leolimsft
ms.author: lle
manager: erikre
ms.openlocfilehash: c291ad016664cf8ac7dcbe2deb9cc04680a707c0
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/03/2018
ms.locfileid: "52765027"
---
# <a name="tracing-master-data-services"></a>Seguimiento (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  El archivo Web.config contiene una sección de seguimiento, como se muestra a continuación. Esta sección es nueva en [!INCLUDE[ssSQL15](../includes/sssql15-md.md)][!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]  
  
```  
<sources>  
      <!-- Adjust the switch value to control the types of messages that should be logged.   
           https://msdn.microsoft.com/library/system.diagnostics.sourcelevels  
           Use the a switchValue of Verbose to generate a full log. Please be aware that   
           the trace file can get quite large very quickly -->  
      <source name="MDS" switchType="System.Diagnostics.SourceSwitch" switchValue="Warning, ActivityTracing">  
        <listeners>  
          <!-- Set a directory path where the service account you chose while setting up Master Data Services has read and write privileges.  
               Default path is Logs in WebApplication folder, for example C:\Program Files\Microsoft SQL Server\130\Master Data Services\WebApplication  
               New log file will be created every day or every 10 mb.  
               When directory size hits the 200mb limitation, the oldest file will be deleted.-->  
          <add name="FileTraceListener"  
               type="Microsoft.MasterDataServices.Core.Logging.FileTraceListener, Microsoft.MasterDataServices.Core"   
               initializeData="DirectoryPath = Logs; FileSizeInMb = 10; MaxDirectorySizeInMb = 200"/>  
          <remove name="Default"/>  
        </listeners>  
      </source>  
    </sources>  
  
```  
  
 Este es el comportamiento de seguimiento predeterminado.  
  
-   El seguimiento está habilitado para los mensajes de advertencia y ActivityTracing.  
  
     Para más información, consulte [SourceLevels (Enumeración)](https://msdn.microsoft.com/library/system.diagnostics.sourcelevels).  
  
-   Los registros se guardan en la carpeta Registros en la carpeta WebApplication. La ubicación predeterminada es C:\Archivos de programa\Microsoft SQL Server\130\Master Data Services\WebApplication\Logs.  
  
-   El archivo se crea cada día o cada 10 MB.  
  
-   Cuando el tamaño del directorio llega a 200 MB, se elimina el registro más antiguo.  
  
-   El formato de registro es CSV. En la tabla siguiente se describe el formato de registro.  
  
    |Elemento|Descripción|  
    |-------------|-----------------|  
    |Time|Cuando se produce la entrada de seguimiento.|  
    |CorrelationID|Se asigna un identificador de correlación para cada solicitud. Todos los seguimientos desencadenados por esta solicitud compartirán el mismo identificador de correlación.<br /><br /> Cuando se produce un error en la interfaz de usuario, aparece el identificador de correlación en el mensaje de error.|  
    |Operación|Nombre de la operación de solicitud. Si la solicitud es una solicitud de interfaz de usuario web, el nombre de la operación es la dirección URL. Si la solicitud es una solicitud de API, el nombre de la operación es el nombre del servicio.|  
    |Nivel|Nivel de esta entrada de seguimiento.|  
    |de mensaje|Cuerpo del mensaje de seguimiento.|  
  
## <a name="external-resources"></a>Recursos externos  
 Entrada de blog [Troubleshooting Logging Improvement](https://go.microsoft.com/fwlink/p/?LinkId=615377)(Solución de problemas de mejora del registro), en msdn.com.  
  
  
