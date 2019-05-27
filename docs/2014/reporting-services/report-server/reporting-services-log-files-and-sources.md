---
title: Archivos de registro y orígenes de Reporting Services | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- troubleshooting [Reporting Services], log files
- logs [Reporting Services]
- logs [Reporting Services], about log files
- report servers [Reporting Services], log files
- report server log files
- files [Reporting Services], logs
ms.assetid: 80ef0acc-cbef-49d0-87e7-844e3ce19604
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 2c0e935cc3d5264a1d2f5569b62db416d85b0427
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/23/2019
ms.locfileid: "66103378"
---
# <a name="reporting-services-log-files-and-sources"></a>Archivos de registro y orígenes de Reporting Services
  Los servidores de informes y los entornos de servidor de informes de [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] admiten diversos destinos de archivos registro para registrar información sobre las operaciones y el estado del servidor. Hay dos categorías básicas de registro: registro de ejecución y registro de seguimiento. El registro de ejecución incluye información sobre las estadísticas de ejecución de informes, auditoría, diagnóstico de rendimiento y optimización. El registro de seguimiento es información sobre los mensajes de error y diagnósticos generales.  
  
 **[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] | Modo nativo de [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]   
  
 La tabla siguiente incluye vínculos a información adicional acerca de cada registro, incluida su ubicación y cómo ver su contenido.  
  
|Log|Descripción|  
|---------|-----------------|  
|[Registro de ejecución del servidor de informes y la vista ExecutionLog3](report-server-executionlog-and-the-executionlog3-view.md)|El registro de ejecución es una vista de SQL Server almacenada en la base de datos del servidor de informes.<br /><br /> El registro de ejecución del servidor de informes contiene datos acerca de informes específicos, como cuándo se ejecutó un informe, quién lo ejecutó, dónde se entregó y qué formato de representación se utilizó.|  
|Registro de seguimiento de SharePoint|Para los servidores de informes que se ejecutan en SharePoint, los registros de seguimiento de SharePoint contienen información de [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] . También se puede configurar información concreta de [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] para el servicio de registro unificado de SharePoint. Para obtener más información, vea [Activar eventos de Reporting Services para el registro de seguimiento de SharePoint &#40;ULS&#41;](turn-on-reporting-services-events-for-the-sharepoint-trace-log-uls.md)|  
|[Registro de seguimiento del servicio del servidor de informes](report-server-service-trace-log.md)|El registro de seguimiento de servicio contiene información muy detallada que resulta útil a la hora de depurar una aplicación o de investigar un problema o evento.<br /><br /> `C:\Program Files\Microsoft SQL Server\MSRS12.MSSQLSERVER\Reporting Services\LogFiles`|  
|[Registro HTTP del servidor de informes](report-server-http-log.md)|El archivo de registro de HTTP contiene un registro de todas las solicitudes HTTP y respuestas controladas por el servicio web del servidor de informes y el Administrador de informes.|  
|[Registro de aplicación Windows](windows-application-log.md)|El registro de aplicación de Microsoft Windows contiene información sobre los eventos del servidor de informes.|  
|Registros de rendimiento de Windows|Los registros de rendimiento de Windows contienen datos sobre el rendimiento del servidor de informes. Puede crear registros de rendimiento y después elegir contadores que establezcan los datos que se recopilarán. Para más información, consulte [Supervisar el rendimiento del servidor de informes](monitoring-report-server-performance.md).|  
|Archivos de registro del programa de instalación|Los archivos de registros se crean también durante la instalación. Si el programa de instalación no se completa o lo hace con advertencias u otros mensajes, puede consultar los archivos de registro para solucionar el problema. Para obtener más información, vea [View and Read SQL Server Setup Log Files](../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md).|  
|Registros IIS|Archivos de registro creados por Microsoft Internet Information Services (IIS). Para obtener más información, consulte [cómo habilitar el registro en Internet Information Services (IIS)](https://support.microsoft.com/kb/313437).|  
|Vídeo|Vea un breve vídeo que muestra el uso de Microsoft Power Query para ver archivos de registro de [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] .<br /><br /> ![ver un vídeo sobre los registros de Power Query y SSRS](../media/generic-video-thumbnail.png "ver un vídeo sobre los registros de Power Query y SSRS")|  
  
## <a name="see-also"></a>Vea también  
 [Servidor de informes de Reporting Services &#40;modo nativo&#41;](reporting-services-report-server-native-mode.md)   
 [Referencia de errores y eventos &#40;Reporting Services&#41;](../troubleshooting/errors-and-events-reference-reporting-services.md)  
  
  
