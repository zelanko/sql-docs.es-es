---
title: Instrucciones para usar características de BI de SQL Server en una granja de servidores de SharePoint 2010 | Documentos de Microsoft
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 5f9a94c4-854b-4577-a8b1-7142f19904e3
caps.latest.revision: 30
author: markingmyname
ms.author: maghan
manager: jhubbard
ms.openlocfilehash: 42502473536215297cb047d4e5e563433b66c67b
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36199845"
---
# <a name="guidance-for-using-sql-server-bi-features-in-a-sharepoint-2010-farm"></a>Instrucciones para usar las características de SQL Server BI en una granja de servidores de SharePoint 2010
  En este tema se resume la disponibilidad de las características según las versiones y las ediciones del software que utiliza. También se explican los requisitos de instalación de SharePoint 2010 para usar determinadas características de SQL Server. Para obtener información relacionada con SharePoint 2013, vea [topologías de implementación para las características de BI de SQL Server en SharePoint](deployment-topologies-for-sql-server-bi-features-in-sharepoint.md).  
  
 En este tema:  
  
-   [Requisitos de general SharePoint 2010](#bkmk_generalsharepoint)  
  
-   [SharePoint 2010 Service Pack 1 (SP1)](#bkmk_sp1)  
  
-   [Compatibilidad con las ediciones de SharePoint y características de BI](#bkmk_vers)  
  
-   [Herramienta de preparación de productos de SharePoint 2010](#bkmk_prereq)  
  
-   [Requisitos y sugerencias para ejecutar la instalación de SharePoint](#bkmk_install)  
  
##  <a name="bkmk_generalsharepoint"></a> Requisitos de general SharePoint 2010  
  
-   Los productos de SharePoint 2010 solo son de 64 bits. Si tiene una instalación de 32 bits de una versión anterior de SharePoint y [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] instalado en modo integrado de SharePoint, no podrá actualizar a SharePoint 2010. Para obtener más información, consulte la documentación del producto de SharePoint.  
  
-   Reporting Services incluye un complemento para los Productos de SharePoint. Las configuraciones admitidas para el complemento y el servidor de informes están disponibles en un nivel más específico del que se indica aquí. Para obtener más información, consulte [admite combinaciones de SharePoint y servidor de Reporting Services y complemento &#40;SQL Server 2014&#41;](../../reporting-services/install-windows/supported-combinations-of-sharepoint-and-reporting-services-server.md).  
  
-   Las herramientas de desarrollo de SharePoint solo admiten una configuración de SharePoint independiente.  Para obtener más información, consulte la documentación de SharePoint: [requisitos para desarrollar soluciones de SharePoint](http://msdn.microsoft.com/library/ee231582.aspx).  
  
##  <a name="bkmk_vers"></a> Compatibilidad con las ediciones de SharePoint y características de BI  
 Algunas características de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Business Intelligence solo se admiten en ediciones concretas de los Productos de SharePoint.  
  
|Características admitidas|Producto de SharePoint|  
|------------------------|------------------------|  
|[!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)], una característica de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] complemento para [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[SPS2010](../../includes/sps2010-md.md)] Enterprise Edition.<br /><br /> Alertas de datos de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].<br /><br /> [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)].|[!INCLUDE[SPS2010](../../includes/sps2010-md.md)] Enterprise Edition.|  
|Presentación general de informes de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e integración de características con SharePoint.|[!INCLUDE[SPS2010](../../includes/sps2010-md.md)] Standard y Enterprise Edition.<br /><br /> [!INCLUDE[SPF2010](../../includes/spf2010-md.md)].|  
  
 Para obtener más información, consulte [características compatibles con las ediciones de SQL Server 2012](http://go.microsoft.com/fwlink/?linkid=232473).  
  
##  <a name="bkmk_sp1"></a> SharePoint 2010 Service Pack 1 (SP1)  
 Se recomienda actualizar la instalación de SharePoint 2010 a SharePoint 2010 Service Pack 1 (SP1). SharePoint SP1 se requiere en los siguientes casos:  
  
-   Desea usar la versión [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] del motor de base de datos para las bases de datos de contenido de SharePoint o para las bases de datos del catálogo de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
-   Desea usar [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] y la herramienta de configuración de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)].  
  
 Se requiere para las instalaciones de SharePoint que se ejecuta con una de las razones principales SP1 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] es la característica del motor de base de datos **sp_dboption**, que ha quedado obsoleta en una versión anterior, no se incluye en el [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] la versión. Para obtener más información, vea [funcionalidad del motor de base de datos no incluida en SQL Server 2014](../../database-engine/discontinued-database-engine-functionality-in-sql-server-2016.md)  
  
### <a name="sharepoint-2010-sp1-installation-guidance"></a>Orientación de instalación de SharePoint 2010 SP1  
 [Descargar SharePoint Server 2010 SP1](http://go.microsoft.com/fwlink/?LinkID=219697) y aplíquelo en todos los servidores de la granja de servidores.  
  
> [!NOTE]  
>  En una granja existente, debe usar uno de los siguientes **adicionales** actualizan pasos para completar el SharePoint SP1. Para obtener más información, consulte [problemas conocidos al instalar Office 2010 SP1 y SharePoint 2010 SP1](http://support.microsoft.com/kb/2532126) y [descripción de SharePoint Server 2010 SP1](http://support.microsoft.com/kb/2460045):  
  
-   **Asistente para configuración de productos de SharePoint:** ejecutar el Asistente para completar la actualización de SP1 y la configuración.  
  
-   **Completar la actualización con psconfig:** ejecute el comando `psconfig –upgrade` para completar la actualización de SP1  
  
 Para obtener más información, vea la sección "actualización" de [(SharePoint Server 2010)](http://technet.microsoft.com/library/cc263093.aspx) y [centro de recursos: actualizaciones de productos de SharePoint 2010](http://technet.microsoft.com/sharepoint/ff800847.aspx)  
  
## <a name="sharepoint-installation-with-sql-server-bi-features"></a>Instalación de SharePoint con características de SQL Server BI  
  
###  <a name="bkmk_prereq"></a> Herramienta de preparación de productos de SharePoint 2010  
 La Herramienta de preparación de Productos de SharePoint habilita los roles de servidor en el sistema operativo e instala otro software como requisito previo requerido por una instalación de SharePoint. En la siguiente tabla se identifican los pasos adicionales para configurar un servidor para [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
|Componente|Acción|  
|---------------|------------|  
|Complemento Reporting Services|La herramienta de preparación de Productos de SharePoint 2010 instala la versión [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] del complemento Reporting Services. [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] incluye una versión más reciente del complemento necesario para las características de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. El complemento se puede instalar mediante el Asistente de instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y descargar de MSDN. Para obtener más información sobre dónde obtener la versión actual del complemento y cómo instalarlo, consulte [dónde encontrar el complemento de Reporting Services para productos de SharePoint](../../reporting-services/install-windows/where-to-find-the-reporting-services-add-in-for-sharepoint-products.md) y [instalar o desinstalar Reporting Services Complemento para SharePoint &#40;SharePoint 2010 y SharePoint 2013&#41;](../../reporting-services/install-windows/install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md).|  
|Proveedor OLE DB Analysis Services (MSOLAP)|SharePoint 2010 instala la versión de SQL Server 2008 del proveedor OLE DB como parte de una implementación de Excel Services. Esta versión no admite el acceso a datos de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]. Debe instalar versiones posteriores del proveedor en los servidores de SharePoint que admitan conexiones de datos de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]. Para obtener más información, vea [instalar el proveedor OLE DB de Analysis Services en servidores de SharePoint](../../../2014/sql-server/install/install-the-analysis-services-ole-db-provider-on-sharepoint-servers.md)|  
|Servicios ADO.NET|SharePoint 2010 enumera los servicios ADO.NET en la lista de requisitos previos, pero el instalador de requisitos previos no lo instala. Para agregar los servicios ADO.NET, debe instalarlos manualmente. Es necesario instalar los servicios ADO.NET si desea usar las listas de SharePoint como fuentes de distribución de datos para libros de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] o informes de Reporting Services. Para obtener instrucciones, consulte [instalar ADO.NET Data Services para admitir datos fuente exportaciones de las listas de SharePoint](../../../2014/sql-server/install/install-ado-net-data-services-to-support-data-feed-exports-of-sharepoint-lists.md).|  
  
###  <a name="bkmk_install"></a> Requisitos y sugerencias para ejecutar la instalación de SharePoint  
 Las características de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] que instale y el orden de instalación de las mismas determinará qué niveles de integración con SharePoint son posibles. Por ejemplo, aunque se dispone de cierto grado de integración de características a través de Reporting Services en un servidor de SharePoint que use una base de datos integrada, la mayoría de los escenarios de integración de características requieren la instalación de una granja de SharePoint, porque solo la instalación de una granja proporciona la infraestructura requerida para algunas características BI.  
  
 Una granja de SharePoint puede ser un servidor único o varios servidores. Lo que establece una granja aparte de una instalación independiente es la presencia de infraestructura adicional, como Notificaciones al servicio de token de Windows.  
  
 Una granja de servidores está habilitado cuando se elige la **granja de servidores** opción en el programa de instalación de SharePoint. Debe tener una instalación de granja de servidores si desea usar [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint o [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)]. La instalación de SharePoint independiente se admite y es común en los entornos de desarrollo de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Sin embargo, en un entorno de producción se recomienda la instalación de una granja de SharePoint.  
  
 ![GMNI_SetupUI_SharePoint2010InstallType](../../../2014/sql-server/install/media/gmni-setupui-sharepoint2010installtype.gif "GMNI_SetupUI_SharePoint2010InstallType")  
  
 También se requiere una instalación de servidor completa de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint o para el servicio compartido [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
 ![GMNI_SetupUI_SharePoint2010ServerType](../../../2014/sql-server/install/media/gmni-setupui-sharepoint2010servertype.gif "GMNI_SetupUI_SharePoint2010ServerType")  
  
 La última página del asistente de instalación le solicita que configure la granja y que, si lo desea, configure una aplicación web predeterminada y una colección de sitios raíz. La mayoría de los usuarios de la instalación siguen esta forma de instalación. Si, por alguna razón, no ha configurado la granja de servidores, puede usar la opción de configuración de la granja en la Herramienta de configuración de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para configurarla.  
  
 En las versiones anteriores se recomienda dejar la granja de servidores sin configurar para instalar [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] porque reducía los pasos necesarios si se usaban las opciones de instalación de SQL Server para instalar [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint en un estado listo para usar. En esta versión esto ya no importa. Puede usar la Herramienta de configuración de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para ajustar una granja de servidores existente para que use los valores recomendados para una instalación de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint.  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] se puede instalar en una granja de servidores de SharePoint existente. Puede instalar [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] o SharePoint en cualquier orden, pero la configuración de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] variará en función del orden. Para obtener más información, consulte [agregar un servidor de informes adicional a una granja de servidores &#40;escalado horizontal de SSRS&#41; ](../../reporting-services/install-windows/add-an-additional-report-server-to-a-farm-ssrs-scale-out.md) y [instalar Reporting Services SharePoint Mode for SharePoint 2010](../../../2014/sql-server/install/install-reporting-services-sharepoint-mode-for-sharepoint-2010.md)  
  
 ![GMNI_SetupUI_DoNotConfigureMOSS](../../../2014/sql-server/install/media/gmni-setupui-donotconfiguremoss.gif "GMNI_SetupUI_DoNotConfigureMOSS")  
  
## <a name="see-also"></a>Vea también  
 [Instalación e implementación de SharePoint Server 2010](http://technet.microsoft.com/sharepoint/ee518643.aspx)   
 [Varios servidores para una granja de servidores de tres niveles (SharePoint Server 2010)](http://go.microsoft.com/fwlink/?linkID=219834)  
  
  