---
title: Características desusadas en SQL Server Reporting Services en SQL Server 2014 | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Reporting Services, backward compatibility
- deprecated features [Reporting Services]
- HTML OWC rendering extension [Reporting Services]
- Report Server Web service, endpoints
ms.assetid: 3876c01e-f81d-4cce-9104-5106a8c369e6
caps.latest.revision: 49
author: markingmyname
ms.author: maghan
manager: mblythe
ms.openlocfilehash: a52d82f4a2126c12dad3ec19cde3cc93ff22368d
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36199623"
---
# <a name="deprecated-features-in-sql-server-reporting-services-in-sql-server-2014"></a>Características desusadas de SQL Server Reporting Services en SQL Server 2014
  En este tema se describen las características de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] desusadas. Las características siguen estando disponibles en la versión en que están desusadas; no obstante, las características están programadas para quitarlas en una versión futura de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Las características en desuso no se deben usar en nuevas aplicaciones.  
  
 En este tema:  
  
-   [Características desusadas de SQL Server 2014 Reporting Services](#bkmk_2014)  
  
-   [Características desusadas de SQL Server 2012 SP1 Reporting Services](#bkmk_2012sp1)  
  
-   [Características desusadas de SQL Server 2012 Reporting Services](#bkmk_2012)  
  
-   [Características desusadas de SQL Server 2008 R2 Reporting Services](#bkmk_kj)  
  
##  <a name="bkmk_2014"></a> Características desusadas de SQL Server 2014 Reporting Services  
  
### <a name="features-not-supported-in-the-next-version-of-sql-server"></a>Características no admitidas en la siguiente versión de SQL Server  
 El siguiente [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] características no se admitirán en la **siguiente** versión de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. No utilice estas características en nuevos trabajos de desarrollo y modifique lo antes posible las aplicaciones que las utilizan actualmente.  
  
#### <a name="html-rendering-extension-device-information-settings"></a>Configuración de información de dispositivo de extensión de representación HTML  
 La siguiente configuración de información de dispositivo para la extensión de representación de HTML está desusada.  
  
-   ActionScript  
  
-   ActiveXControls  
  
-   GetImage  
  
-   OnlyVisibleStyles  
  
-   ReplacementRoot  
  
-   ResourceStreamRoot  
  
-   StreamRoot  
  
-   UsePx  
  
-   Zoom  
  
 Para obtener más información sobre la extensión de representación HTML, vea [HTML Device Information Settings](html-device-information-settings.md)  
  
#### <a name="microsoft-word-and-microsoft-excel-1997-2003-rendering"></a>Representación de Microsoft Word y Microsoft Excel 1997-2003  
 El[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] extensiones de representación BIFF8 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] notifica a la [!INCLUDE[msCoName](../includes/msconame-md.md)] Word y [!INCLUDE[msCoName](../includes/msconame-md.md)] formato de archivo de intercambio binario de Excel 1997-2003. [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] incluye las extensiones que se procesan en el [!INCLUDE[msCoName](../includes/msconame-md.md)] formato XML abierto de Office 2007-2010.  
  
#### <a name="report-definition-language-rdl-2005-and-earlier"></a>Lenguaje RDL 2005 y anterior  
 Lenguaje RDL 2005 y anterior está desusado. Para obtener más información acerca de RDL, vea [Report Definition Language &#40;SSRS&#41;](reports/report-definition-language-ssrs.md).  
  
 Para obtener más información acerca de la actualización de informes, consulte [Upgrade Reports](install-windows/upgrade-reports.md).  
  
#### <a name="sql-server-2005-and-earlier-custom-report-items"></a>SQL Server 2005 y elementos de informe personalizados anteriores  
 Elementos de informe personalizados (CRI) compilados para [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 2005 y anterior están desusados.  
  
#### <a name="reporting-services-snapshots-2005-and-earlier"></a>Instantáneas de Reporting Services 2005 y anterior  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] representadas con [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 2005 y anterior están desusados.  
  
#### <a name="report-models"></a>Modelos de informe  
 Los modelos de informe del lenguaje semántico modelado (SMDL) han quedado desusados. Aunque puede seguir utilizar modelos de informe existentes como orígenes de datos en [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] informes, debe considerar la actualización de los informes para quitar su dependencia de modelos de informe.  
  
 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] no incluye las herramientas para crear o actualizar los modelos de informe. Para obtener más información, consulte [Breaking Changes in SQL Server Reporting Services en SQL Server 2014](breaking-changes-in-sql-server-reporting-services-in-sql-server-2016.md).  
  
#### <a name="deprecated-methods-in-the-web-service-endpoint"></a>Métodos desusados en el extremo del servicio web  
 Las operaciones siguientes han quedado obsoletas en la <xref:ReportService2010.ReportingService2010> extremo del servicio Web:  
  
-   <xref:ReportService2010.ReportingService2010.GetProperties%2A>  
  
-   <xref:ReportService2010.ReportingService2010.IsSSLRequired%2A>  
  
#### <a name="sharepoint-web-parts"></a>Elementos web de SharePoint  
 El archivo contenedor de instalación **RSWebParts.cab** y los elementos web de SharePoint que se pueden extraer del archivo .cab, están en desuso. Los elementos web en desuso son el Explorador de informes (**SPExplorer.dwp**) y el Visor de informes (**SPViewer.dwp**).  
  
 Para obtener más información sobre los elementos web en desuso, vea [Ver y explorar los informes en modo nativo usando elementos web de SharePoint (SSRS)](http://msdn.microsoft.com/library/ms159772.aspx)  
  
### <a name="features-not-supported-in-a-future-version-of-sql-server"></a>Características no admitidas en una versión futura de SQL Server  
 Las características del [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] siguientes se admiten en la próxima versión de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], pero se quitarán en una versión posterior. No se ha determinado la versión específica de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .  
  
 Ya no [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] características están desusadas en [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)].  
  
##  <a name="bkmk_2012sp1"></a> Características desusadas de SQL Server 2012 SP1 Reporting Services  
 Esta sección se describen [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] características en desuso en [!INCLUDE[ssSQL11SP1](../includes/sssql11sp1-md.md)]. Las características del [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] siguientes se admiten en la próxima versión de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)], pero se quitarán en una versión posterior. No se ha determinado la versión específica de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] .  
  
### <a name="sharepoint-web-parts"></a>Elementos web de SharePoint  
 El archivo contenedor de instalación **RSWebParts.cab** y los elementos web de SharePoint que se pueden extraer del archivo .cab, están en desuso. Los elementos web en desuso son el Explorador de informes (**SPExplorer.dwp**) y el Visor de informes (**SPViewer.dwp**).  
  
 Para obtener más información sobre los elementos web en desuso, vea [Ver y explorar los informes en modo nativo usando elementos web de SharePoint (SSRS)](http://msdn.microsoft.com/library/ms159772.aspx)  
  
##  <a name="bkmk_2012"></a> Características desusadas de SQL Server 2012 Reporting Services  
 Esta sección se describen [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] características en desuso en [!INCLUDE[ssSQL11](../includes/sssql11-md.md)].  
  
### <a name="html-rendering-extension-device-information-settings"></a>Configuración de información de dispositivo de extensión de representación HTML  
 La siguiente configuración de información de dispositivo para la extensión de representación de HTML está desusada.  
  
-   ActionScript  
  
-   ActiveXControls  
  
-   GetImage  
  
-   OnlyVisibleStyles  
  
-   ReplacementRoot  
  
-   ResourceStreamRoot  
  
-   StreamRoot  
  
-   UsePx  
  
-   Zoom  
  
 Para obtener más información sobre la extensión de representación HTML, vea [HTML Device Information Settings](html-device-information-settings.md)  
  
### <a name="microsoft-word-and-microsoft-excel-1997-2003-rendering"></a>Representación de Microsoft Word y Microsoft Excel 1997-2003  
 El[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] extensiones de representación BIFF8 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] notifica a la [!INCLUDE[msCoName](../includes/msconame-md.md)] Word y [!INCLUDE[msCoName](../includes/msconame-md.md)] formato de archivo de intercambio binario de Excel 1997-2003. [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] incluye las extensiones que se procesan en el [!INCLUDE[msCoName](../includes/msconame-md.md)] formato XML abierto de Office 2007-2010.  
  
### <a name="report-definition-language-rdl-2005-and-earlier"></a>Lenguaje RDL 2005 y anterior  
 Lenguaje RDL 2005 y anterior está desusado. Para obtener más información acerca de RDL, vea [Report Definition Language &#40;SSRS&#41;](reports/report-definition-language-ssrs.md).  
  
 Para obtener más información acerca de la actualización de informes, consulte [Upgrade Reports](install-windows/upgrade-reports.md).  
  
### <a name="sql-server-2005-and-earlier-custom-report-items"></a>SQL Server 2005 y elementos de informe personalizados anteriores  
 Elementos de informe personalizados (CRI) compilados para [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 2005 y anterior están desusados.  
  
### <a name="reporting-services-snapshots-2005-and-earlier"></a>Instantáneas de Reporting Services 2005 y anterior  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] representadas con [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 2005 y anterior están desusados.  
  
### <a name="report-models"></a>Modelos de informe  
 Los modelos de informe del lenguaje semántico modelado (SMDL) han quedado desusados. Aunque puede seguir utilizar modelos de informe existentes como orígenes de datos en [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] informes, debe considerar la actualización de los informes para quitar su dependencia de modelos de informe.  
  
 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] no incluye las herramientas para crear o actualizar los modelos de informe. Para obtener más información, consulte [Breaking Changes in SQL Server Reporting Services en SQL Server 2014](breaking-changes-in-sql-server-reporting-services-in-sql-server-2016.md).  
  
### <a name="deprecated-methods-in-the-web-service-endpoint"></a>Métodos desusados en el extremo del servicio web  
 Las operaciones siguientes han quedado obsoletas en la <xref:ReportService2010.ReportingService2010> extremo del servicio Web:  
  
-   <xref:ReportService2010.ReportingService2010.GetProperties%2A>  
  
-   <xref:ReportService2010.ReportingService2010.IsSSLRequired%2A>  
  
##  <a name="bkmk_kj"></a> Características desusadas de SQL Server 2008 R2 Reporting Services  
  
> [!NOTE]  
>  Dado que SQL Server 2008 R2 es una actualización de versión menor de SQL Server 2008, recomendamos también revisar el contenido en la sección de SQL Server 2008.  
  
### <a name="report-server-web-service-endpoints"></a>Extremos de servicios web del servidor de informes  
 Los servicios Web <xref:ReportService2005.ReportingService2005> y <xref:ReportService2006.ReportingService2006> han quedado obsoletas en esta versión. Estos puntos de conexión se han reemplazado por un nuevo extremo: <xref:ReportService2010.ReportingService2010>.  
  
 El nuevo extremo incluye toda la funcionalidad disponible en los extremos desusados y las nuevas características introducidas en SQL Server 2008 R2.  
  
## <a name="see-also"></a>Vea también  
 [' S New &#40;Reporting Services&#41;](what-s-new-reporting-services.md)   
 [Compatibilidad con versiones anteriores](../getting-started/backward-compatibility.md)   
 [Cambios de comportamiento en SQL Server Reporting Services en SQL Server 2014](behavior-changes-to-sql-server-reporting-services-in-sql-server-2016.md)   
 [Funcionalidad no incluida en SQL Server Reporting Services en SQL Server 2014](discontinued-functionality-to-sql-server-reporting-services-in-sql-server.md)  
  
  