---
title: Características desusadas de SQL Server Reporting Services en SQL Server 2014 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- Reporting Services, backward compatibility
- deprecated features [Reporting Services]
- HTML OWC rendering extension [Reporting Services]
- Report Server Web service, endpoints
ms.assetid: 3876c01e-f81d-4cce-9104-5106a8c369e6
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: d5cbef64cbed910018e7d2f8dae1844074aaa3f5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66109350"
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
 Las siguientes características de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] no se admitirán en la **próxima** versión de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. No utilice estas características en nuevos trabajos de desarrollo y modifique lo antes posible las aplicaciones que las utilizan actualmente.  
  
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
 Extensiones de representación BIFF8 de[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] , informes de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] para el formato de archivo de intercambio binario de [!INCLUDE[msCoName](../includes/msconame-md.md)] Word y [!INCLUDE[msCoName](../includes/msconame-md.md)] Excel 1997-2003. [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] Incluye extensiones que se procesan en el [!INCLUDE[msCoName](../includes/msconame-md.md)] formato XML abierto de Office 2007-2010.  
  
#### <a name="report-definition-language-rdl-2005-and-earlier"></a>Lenguaje RDL 2005 y anterior  
 Lenguaje RDL 2005 y anterior está desusado. Para obtener más información acerca de RDL, vea [Report Definition Language &#40;SSRS&#41;](reports/report-definition-language-ssrs.md).  
  
 Para obtener más información acerca de la actualización de informes, vea [Upgrade Reports](install-windows/upgrade-reports.md).  
  
#### <a name="sql-server-2005-and-earlier-custom-report-items"></a>SQL Server 2005 y elementos de informe personalizados anteriores  
 Los elementos de informe personalizados (CRI) compilados para [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 2005 y anterior están desusados.  
  
#### <a name="reporting-services-snapshots-2005-and-earlier"></a>Instantáneas de Reporting Services 2005 y anterior  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] representadas con [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 2005 y anterior están desusados.  
  
#### <a name="report-models"></a>Modelos de informe  
 Los modelos de informe del lenguaje semántico modelado (SMDL) han quedado desusados. Aunque puede continuar usando los modelos de informe existentes como orígenes de datos en [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] informes, debe considerar la actualización de los informes para quitar su dependencia de los modelos de informe.  
  
 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] no incluye las herramientas para crear o actualizar los modelos de informe. Para obtener más información, consulte [cambios substanciales de SQL Server Reporting Services en SQL Server 2014](breaking-changes-in-sql-server-reporting-services-in-sql-server-2016.md).  
  
#### <a name="deprecated-methods-in-the-web-service-endpoint"></a>Métodos desusados en el extremo del servicio web  
 Las operaciones siguientes han quedado en desuso en el extremo de servicios web de <xref:ReportService2010.ReportingService2010>:  
  
-   <xref:ReportService2010.ReportingService2010.GetProperties%2A>  
  
-   <xref:ReportService2010.ReportingService2010.IsSSLRequired%2A>  
  
#### <a name="sharepoint-web-parts"></a>Elementos web de SharePoint  
 El archivo contenedor de instalación **RSWebParts.cab** y los elementos web de SharePoint que se pueden extraer del archivo .cab, están en desuso. Los elementos web en desuso son el Explorador de informes (**SPExplorer.dwp**) y el Visor de informes (**SPViewer.dwp**).  
  
 Para obtener más información sobre los elementos web en desuso, vea [Ver y explorar los informes en modo nativo usando elementos web de SharePoint (SSRS)](https://msdn.microsoft.com/library/ms159772.aspx)  
  
### <a name="features-not-supported-in-a-future-version-of-sql-server"></a>Características no admitidas en una versión futura de SQL Server  
 Las características del [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] siguientes se admiten en la próxima versión de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], pero se quitarán en una versión posterior. No se ha determinado la versión específica de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .  
  
 Ninguna característica de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] ha quedado en desuso en [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)].  
  
##  <a name="bkmk_2012sp1"></a> Características desusadas de SQL Server 2012 SP1 Reporting Services  
 En esta sección se describen las características de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] desusadas en [!INCLUDE[ssSQL11SP1](../includes/sssql11sp1-md.md)]. Las características del [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] siguientes se admiten en la próxima versión de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)], pero se quitarán en una versión posterior. No se ha determinado la versión específica de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] .  
  
### <a name="sharepoint-web-parts"></a>Elementos web de SharePoint  
 El archivo contenedor de instalación **RSWebParts.cab** y los elementos web de SharePoint que se pueden extraer del archivo .cab, están en desuso. Los elementos web en desuso son el Explorador de informes (**SPExplorer.dwp**) y el Visor de informes (**SPViewer.dwp**).  
  
 Para obtener más información sobre los elementos web en desuso, vea [Ver y explorar los informes en modo nativo usando elementos web de SharePoint (SSRS)](https://msdn.microsoft.com/library/ms159772.aspx)  
  
##  <a name="bkmk_2012"></a> Características desusadas de SQL Server 2012 Reporting Services  
 En esta sección se describen las características de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] desusadas en [!INCLUDE[ssSQL11](../includes/sssql11-md.md)].  
  
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
 Extensiones de representación BIFF8 de[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] , informes de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] para el formato de archivo de intercambio binario de [!INCLUDE[msCoName](../includes/msconame-md.md)] Word y [!INCLUDE[msCoName](../includes/msconame-md.md)] Excel 1997-2003. [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] Incluye extensiones que se procesan en el [!INCLUDE[msCoName](../includes/msconame-md.md)] formato XML abierto de Office 2007-2010.  
  
### <a name="report-definition-language-rdl-2005-and-earlier"></a>Lenguaje RDL 2005 y anterior  
 Lenguaje RDL 2005 y anterior está desusado. Para obtener más información acerca de RDL, vea [Report Definition Language &#40;SSRS&#41;](reports/report-definition-language-ssrs.md).  
  
 Para obtener más información acerca de la actualización de informes, vea [Upgrade Reports](install-windows/upgrade-reports.md).  
  
### <a name="sql-server-2005-and-earlier-custom-report-items"></a>SQL Server 2005 y elementos de informe personalizados anteriores  
 Los elementos de informe personalizados (CRI) compilados para [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 2005 y anterior están desusados.  
  
### <a name="reporting-services-snapshots-2005-and-earlier"></a>Instantáneas de Reporting Services 2005 y anterior  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] representadas con [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 2005 y anterior están desusados.  
  
### <a name="report-models"></a>Modelos de informe  
 Los modelos de informe del lenguaje semántico modelado (SMDL) han quedado desusados. Aunque puede continuar usando los modelos de informe existentes como orígenes de datos en [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] informes, debe considerar la actualización de los informes para quitar su dependencia de los modelos de informe.  
  
 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] no incluye las herramientas para crear o actualizar los modelos de informe. Para obtener más información, consulte [cambios substanciales de SQL Server Reporting Services en SQL Server 2014](breaking-changes-in-sql-server-reporting-services-in-sql-server-2016.md).  
  
### <a name="deprecated-methods-in-the-web-service-endpoint"></a>Métodos desusados en el extremo del servicio web  
 Las operaciones siguientes han quedado en desuso en el extremo de servicios web de <xref:ReportService2010.ReportingService2010>:  
  
-   <xref:ReportService2010.ReportingService2010.GetProperties%2A>  
  
-   <xref:ReportService2010.ReportingService2010.IsSSLRequired%2A>  
  
##  <a name="bkmk_kj"></a> Características desusadas de SQL Server 2008 R2 Reporting Services  
  
> [!NOTE]  
>  Dado que SQL Server 2008 R2 es una actualización de versión menor de SQL Server 2008, recomendamos también revisar el contenido en la sección de SQL Server 2008.  
  
### <a name="report-server-web-service-endpoints"></a>Extremos de servicios web del servidor de informes  
 Los servicios web <xref:ReportService2005.ReportingService2005> y <xref:ReportService2006.ReportingService2006> están obsoletos en esta versión. Un nuevo extremo ha reemplazado estos extremos: <xref:ReportService2010.ReportingService2010>.  
  
 El nuevo extremo incluye toda la funcionalidad disponible en los extremos desusados y las nuevas características introducidas en SQL Server 2008 R2.  
  
## <a name="see-also"></a>Vea también  
 [¿Qué novedades &#40;Reporting Services&#41;](what-s-new-reporting-services.md)   
 [Compatibilidad con versiones anteriores](../getting-started/backward-compatibility.md)   
 [Cambios de comportamiento en SQL Server Reporting Services en SQL Server 2014](behavior-changes-to-sql-server-reporting-services-in-sql-server-2016.md)   
 [Funcionalidad de SQL Server Reporting Services descontinuada en SQL Server 2014](discontinued-functionality-to-sql-server-reporting-services-in-sql-server.md)  
  
  
