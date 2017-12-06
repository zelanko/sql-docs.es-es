---
title: 'rsServerConfigurationError: error de Reporting Services | Microsoft Docs'
ms.custom: 
ms.date: 03/20/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: troubleshooting
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: rsServerConfigurationError
ms.assetid: 0913afc2-34b4-4713-b570-cfd5718975ac
caps.latest.revision: "12"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: On Demand
ms.openlocfilehash: 1de7654a396ce163cf2bd0e8cb1303f57b156e64
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/05/2017
---
# <a name="rsserverconfigurationerror---reporting-services-error"></a>rsServerConfigurationError - Error de Reporting Services
    
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|Identificador del evento|rsServerConfiguration|  
|Origen del evento|Microsoft.ReportingServices.Diagnostics.Utilities.ErrorStrings|  
|Componente|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|  
|Texto del mensaje|El servidor de informes ha encontrado un error de configuración.|  
  
## <a name="explanation"></a>Explicación  
 Este es un error de uso general que se produce cuando el servidor de informes o una herramienta de creación de informes tienen valores de configuración no válidos. El error suele ir acompañado de un segundo mensaje que indica la causa real del error.  
  
 La lista siguiente resume las posibles causas:  
  
-   El archivo RSReportServer.config o RSReportDesigner.config no se puede encontrar o leer.  
  
-   Los elementos XML de cualquier archivo de configuración faltan o no son válidos.  
  
-   Los valores de uno o más elementos XML faltan o no son válidos.  
  
-   Los parámetros del Registro no son válidos.  
  
## <a name="user-action"></a>Acción del usuario  
 Si este error empezara a producirse después de editar manualmente un archivo de configuración, quite los cambios efectuados y especifique el valor anterior, o restaure una versión anterior si tiene una copia de seguridad.  
  
 Para revisar la información adicional del mensaje que acompaña al error **rsServerConfiguration**, revise los archivos de registro de seguimiento del servidor de informes, que se encuentran en \Microsoft SQL Server\MSRS12.\<nombreDeInstancia>\Reporting Services\LogFiles. Para más información, vea [Archivos de registro y orígenes de Reporting Services](../../reporting-services/report-server/reporting-services-log-files-and-sources.md).  
  
## <a name="internal-only"></a>Solo para uso interno  
  
## <a name="see-also"></a>Vea también  
 [Archivos de configuración de Reporting Services](../../reporting-services/report-server/reporting-services-configuration-files.md)   
 [Modificar un archivo de configuración de Reporting Services &#40;RSreportserver.config&#41;](../../reporting-services/report-server/modify-a-reporting-services-configuration-file-rsreportserver-config.md)  
  
  
