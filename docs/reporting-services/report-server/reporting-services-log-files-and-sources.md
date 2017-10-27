---
title: "Archivos de registro y orígenes de Reporting Services | Documentos de Microsoft"
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
- troubleshooting [Reporting Services], log files
- logs [Reporting Services]
- logs [Reporting Services], about log files
- report servers [Reporting Services], log files
- report server log files
- files [Reporting Services], logs
ms.assetid: 80ef0acc-cbef-49d0-87e7-844e3ce19604
caps.latest.revision: 49
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 08686f83b78c783e1d82c144e4a06f9ecd52bde0
ms.contentlocale: es-es
ms.lasthandoff: 08/09/2017

---
# <a name="reporting-services-log-files-and-sources"></a>Archivos de registro y orígenes de Reporting Services
  Los servidores de informes y los entornos de servidor de informes utilizan diversos destinos de archivos registro para registrar información sobre las operaciones y el estado del servidor. Hay dos categorías básicas de registro: registro de ejecución y registro de seguimiento. El registro de ejecución incluye información sobre las estadísticas de ejecución de informes, auditoría, diagnóstico de rendimiento y optimización. El registro de seguimiento es información sobre los mensajes de error y diagnósticos generales.  
  
 **[!INCLUDE[applies](../../includes/applies-md.md)]** Modo de SharePoint de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] | Modo nativo de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
 La tabla siguiente incluye vínculos a información adicional acerca de cada registro, incluida su ubicación y cómo ver su contenido.  
  
|Log|Description|  
|---------|-----------------|  
|[Registro de ejecución del servidor de informes y la vista ExecutionLog3](../../reporting-services/report-server/report-server-executionlog-and-the-executionlog3-view.md)|El registro de ejecución es una vista de SQL Server almacenada en la base de datos del servidor de informes.<br /><br /> El registro de ejecución del servidor de informes contiene datos acerca de informes específicos, como cuándo se ejecutó un informe, quién lo ejecutó, dónde se entregó y qué formato de representación se utilizó.|  
|Registro de seguimiento de SharePoint|Para los servidores de informes que se ejecutan en SharePoint, los registros de seguimiento de SharePoint contienen información de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . También puede configurar información concreta de [!INCLUDE[ssRS](../../includes/ssrs-md.md)] para el servicio de registro unificado de SharePoint. Para más información, vea [Activar eventos de Reporting Services para el registro de seguimiento de SharePoint &#40;ULS&#41;](../../reporting-services/report-server/turn-on-reporting-services-events-for-the-sharepoint-trace-log-uls.md)|  
|[Registro de seguimiento de servicio de servidor de informes](../../reporting-services/report-server/report-server-service-trace-log.md)|El registro de seguimiento de servicio contiene información muy detallada que resulta útil a la hora de depurar una aplicación o de investigar un problema o evento. Los archivos de registro de seguimiento son ReportServerService_\<timestamp > .log y están ubicados en la siguiente carpeta:<br /><br /> `C:\Program Files\Microsoft SQL Server\MSRS13.MSSQLSERVER\Reporting Services\LogFiles`|  
|[Registro HTTP del servidor de informes](../../reporting-services/report-server/report-server-http-log.md)|El archivo de registro de HTTP contiene un registro de todas las solicitudes HTTP y respuestas controladas por el servicio web del servidor de informes y el Administrador de informes.|  
|[Registro de aplicación Windows](../../reporting-services/report-server/windows-application-log.md)|El registro de aplicación de Microsoft Windows contiene información sobre los eventos del servidor de informes.|  
|Registros de rendimiento de Windows|Los registros de rendimiento de Windows contienen datos sobre el rendimiento del servidor de informes. Puede crear registros de rendimiento y después elegir contadores que establezcan los datos que se recopilarán. Para más información, consulte [Monitoring Report Server Performance](../../reporting-services/report-server/monitoring-report-server-performance.md).|  
|Archivos de registro de instalación de SQL Server|Los archivos de registros se crean también durante la instalación. Si el programa de instalación no se completa o lo hace con advertencias u otros mensajes, puede consultar los archivos de registro para solucionar el problema. Para obtener más información, vea [View and Read SQL Server Setup Log Files](../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md).|  
|Registros IIS|Archivos de registro creados por Microsoft Internet Information Services (IIS). Para más información, vea [Cómo habilitar el registro en los servicios de Internet Information Server (IIS)](http://support.microsoft.com/kb/313437) (http://support.microsoft.com/kb/313437).|  
  
## <a name="see-also"></a>Vea también  
 [Servidor de informes de Reporting Services &#40;modo nativo&#41;](../../reporting-services/report-server/reporting-services-report-server-native-mode.md)   
 [Errores y eventos referencia &#40; Reporting Services &#41;](../../reporting-services/troubleshooting/errors-and-events-reference-reporting-services.md)  
  
  

