---
title: Instrucciones para usar las características de SQL Server BI en una granja de servidores de SharePoint 2010 | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 5f9a94c4-854b-4577-a8b1-7142f19904e3
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 02aaab5056d5e2b095d9440f696edcc77475323e
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "78172564"
---
# <a name="guidance-for-using-sql-server-bi-features-in-a-sharepoint-2010-farm"></a>Instrucciones para usar las características de SQL Server BI en una granja de servidores de SharePoint 2010
  En este tema se resume la disponibilidad de las características según las versiones y las ediciones del software que utiliza. También se explican los requisitos de instalación de SharePoint 2010 para usar determinadas características de SQL Server. Para obtener información relacionada con SharePoint 2013, vea [topologías de implementación para las características de SQL Server BI en SharePoint](deployment-topologies-for-sql-server-bi-features-in-sharepoint.md).

 En este tema:

-   [Requisitos generales de SharePoint 2010](#bkmk_generalsharepoint)

-   [SharePoint 2010 Service Pack 1 (SP1)](#bkmk_sp1)

-   [Ediciones de SharePoint y compatibilidad con la característica BI](#bkmk_vers)

-   [Herramienta de preparación de Productos de SharePoint 2010](#bkmk_prereq)

-   [Requisitos y sugerencias para ejecutar el programa de instalación de SharePoint](#bkmk_install)

##  <a name="general-sharepoint-2010-requirements"></a><a name="bkmk_generalsharepoint"></a>Requisitos generales de SharePoint 2010

-   Los productos de SharePoint 2010 solo son de 64 bits. Si tiene una instalación de 32 bits de una versión anterior de SharePoint y [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] instalado en modo integrado de SharePoint, no podrá actualizar a SharePoint 2010. Para obtener más información, consulte la documentación del producto de SharePoint.

-   Reporting Services incluye un complemento para los Productos de SharePoint. Las configuraciones admitidas para el complemento y el servidor de informes están disponibles en un nivel más específico del que se indica aquí. Para obtener más información, vea [combinaciones admitidas de SharePoint y Reporting Services Server y el complemento &#40;SQL Server 2014&#41;](../../reporting-services/install-windows/supported-combinations-of-sharepoint-and-reporting-services-server.md).

-   Las herramientas de desarrollo de SharePoint solo admiten una configuración de SharePoint independiente.  Para obtener más información, vea la documentación de SharePoint: [requisitos para desarrollar soluciones de SharePoint](https://msdn.microsoft.com/library/ee231582.aspx).

##  <a name="sharepoint-editions-and-bi-feature-support"></a><a name="bkmk_vers"></a>Ediciones de SharePoint y compatibilidad con las características de BI
 Algunas características de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Business Intelligence solo se admiten en ediciones concretas de los Productos de SharePoint.

|Características admitidas|Producto de SharePoint|
|------------------------|------------------------|
|[!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)], una característica del [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] complemento para [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[SPS2010](../../includes/sps2010-md.md)] Enterprise Edition.<br /><br /> Alertas de datos de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].<br /><br /> [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)].|[!INCLUDE[SPS2010](../../includes/sps2010-md.md)] Enterprise Edition.|
|Presentación general de informes de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e integración de características con SharePoint.|[!INCLUDE[SPS2010](../../includes/sps2010-md.md)] Standard y Enterprise Edition.<br /><br /> [!INCLUDE[SPF2010](../../includes/spf2010-md.md)].|

 Para obtener más información, vea [características compatibles con las ediciones de SQL Server 2012](https://go.microsoft.com/fwlink/?linkid=232473).

##  <a name="sharepoint-2010-service-pack-1-sp1"></a><a name="bkmk_sp1"></a>SharePoint 2010 Service Pack 1 (SP1)
 Se recomienda actualizar la instalación de SharePoint 2010 a SharePoint 2010 Service Pack 1 (SP1). SharePoint SP1 se requiere en los siguientes casos:

-   Desea usar la versión [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] del motor de base de datos para las bases de datos de contenido de SharePoint o para las bases de datos del catálogo de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].

-   Desea usar [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] y la herramienta de configuración de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)].

 Una de las principales razones por las que se requiere SP1 para las [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] instalaciones de SharePoint que se ejecutan con es la característica del motor de base de datos **sp_dboption**, que quedó en [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] desuso en una versión anterior, no se ha suspendido en la versión. Para obtener más información, vea [funcionalidad de motor de base de datos no incluida en SQL Server 2014](../../database-engine/discontinued-database-engine-functionality-in-sql-server-2016.md)

### <a name="sharepoint-2010-sp1-installation-guidance"></a>Orientación de instalación de SharePoint 2010 SP1
 [Descargue SharePoint Server 2010 SP1](https://go.microsoft.com/fwlink/?LinkID=219697) y aplíquelo en todos los servidores de la granja.

> [!NOTE]
>  En una granja de servidores existente, deberá usar uno de los siguientes pasos **adicionales** para completar la actualización de SharePoint SP1. Para obtener más información, vea [problemas conocidos al instalar Office 2010 SP1 y sharepoint 2010 SP1](https://support.microsoft.com/kb/2532126) y la [Descripción de SharePoint Server 2010 SP1](https://support.microsoft.com/kb/2460045):

-   **Asistente para configuración de productos de SharePoint:** Ejecute el Asistente para completar la actualización y configuración de SP1.

-   **Complete la actualización con psconfig:** Ejecutar el comando `psconfig -upgrade` para completar la actualización de SP1

 Para obtener más información, vea la sección "actualización" de [(SharePoint Server 2010)](https://technet.microsoft.com/library/cc263093.aspx) y [centro de recursos: actualizaciones de productos de SharePoint 2010](https://technet.microsoft.com/sharepoint/ff800847.aspx)

## <a name="sharepoint-installation-with-sql-server-bi-features"></a>Instalación de SharePoint con características de SQL Server BI

###  <a name="sharepoint-2010-products-preparation-tool"></a><a name="bkmk_prereq"></a>Herramienta de preparación de productos de SharePoint 2010
 La Herramienta de preparación de Productos de SharePoint habilita los roles de servidor en el sistema operativo e instala otro software como requisito previo requerido por una instalación de SharePoint. En la siguiente tabla se identifican los pasos adicionales para configurar un servidor para [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].

|Componente|Acción|
|---------------|------------|
|Complemento Reporting Services|La herramienta de preparación de Productos de SharePoint 2010 instala la versión [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] del complemento Reporting Services. [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] incluye una versión más reciente del complemento necesario para las características de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. El complemento se puede instalar mediante el Asistente de instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y descargar de MSDN. Para obtener más información sobre dónde obtener la versión actual del complemento y cómo instalarlo, vea [dónde encontrar el complemento de Reporting Services para productos de SharePoint](../../reporting-services/install-windows/where-to-find-the-reporting-services-add-in-for-sharepoint-products.md) e [instalar o desinstalar el complemento Reporting Services para sharepoint &#40;SharePoint 2010 y SharePoint 2013&#41;](../../reporting-services/install-windows/install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md).|
|Proveedor OLE DB Analysis Services (MSOLAP)|SharePoint 2010 instala la versión de SQL Server 2008 del proveedor OLE DB como parte de una implementación de Excel Services. Esta versión no admite el acceso a datos de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]. Debe instalar versiones posteriores del proveedor en los servidores de SharePoint que admitan conexiones de datos de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]. Para obtener más información, vea [instalar el proveedor OLE DB de Analysis Services en servidores de SharePoint](../../../2014/sql-server/install/install-the-analysis-services-ole-db-provider-on-sharepoint-servers.md) .|
|Servicios ADO.NET|SharePoint 2010 enumera los servicios ADO.NET en la lista de requisitos previos, pero el instalador de requisitos previos no lo instala. Para agregar los servicios ADO.NET, debe instalarlos manualmente. Es necesario instalar los servicios ADO.NET si desea usar las listas de SharePoint como fuentes de distribución de datos para libros de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] o informes de Reporting Services. Para obtener instrucciones, vea [instalar ADO.NET Data Services para admitir las exportaciones de fuentes de distribución de datos de las listas de SharePoint](../../../2014/sql-server/install/install-ado-net-data-services-to-support-data-feed-exports-of-sharepoint-lists.md).|

###  <a name="requirements-and-suggestions-for-running-the-sharepoint-installation"></a><a name="bkmk_install"></a>Requisitos y sugerencias para ejecutar la instalación de SharePoint
 Las características de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] que instale y el orden de instalación de las mismas determinará qué niveles de integración con SharePoint son posibles. Por ejemplo, aunque se dispone de cierto grado de integración de características a través de Reporting Services en un servidor de SharePoint que use una base de datos integrada, la mayoría de los escenarios de integración de características requieren la instalación de una granja de SharePoint, porque solo la instalación de una granja proporciona la infraestructura requerida para algunas características BI.

 Una granja de SharePoint puede ser un servidor único o varios servidores. Lo que establece una granja aparte de una instalación independiente es la presencia de infraestructura adicional, como Notificaciones al servicio de token de Windows.

 Una granja de servidores se habilita al elegir la opción **granja de servidores** del programa de instalación de SharePoint. Debe tener una instalación de granja de servidores si desea usar [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint o [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)]. La instalación de SharePoint independiente se admite y es común en los entornos de desarrollo de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Sin embargo, en un entorno de producción se recomienda la instalación de una granja de SharePoint.

 ![GMNI_SetupUI_SharePoint2010InstallType](../../../2014/sql-server/install/media/gmni-setupui-sharepoint2010installtype.gif "GMNI_SetupUI_SharePoint2010InstallType")

 También se requiere una instalación de servidor completa de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint o para el servicio compartido [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].

 ![GMNI_SetupUI_SharePoint2010ServerType](../../../2014/sql-server/install/media/gmni-setupui-sharepoint2010servertype.gif "GMNI_SetupUI_SharePoint2010ServerType")

 La última página del asistente de instalación le solicita que configure la granja y que, si lo desea, configure una aplicación web predeterminada y una colección de sitios raíz. La mayoría de los usuarios de la instalación siguen esta forma de instalación. Si, por alguna razón, no ha configurado la granja de servidores, puede usar la opción de configuración de la granja en la Herramienta de configuración de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para configurarla.

 En las versiones anteriores se recomienda dejar la granja de servidores sin configurar para instalar [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] porque reducía los pasos necesarios si se usaban las opciones de instalación de SQL Server para instalar [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint en un estado listo para usar. En esta versión esto ya no importa. Puede usar la Herramienta de configuración de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para ajustar una granja de servidores existente para que use los valores recomendados para una instalación de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint.

 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] se puede instalar en una granja de servidores de SharePoint existente. Puede instalar [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] o SharePoint en cualquier orden, pero la configuración de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] variará en función del orden. Para obtener más información, vea [Agregar un servidor de informes adicional a una granja &#40;&#41;de escalado horizontal de SSRS](../../reporting-services/install-windows/add-an-additional-report-server-to-a-farm-ssrs-scale-out.md) e [instalar Reporting Services modo de sharepoint para SharePoint 2010](../../../2014/sql-server/install/install-reporting-services-sharepoint-mode-for-sharepoint-2010.md)

 ![GMNI_SetupUI_DoNotConfigureMOSS](../../../2014/sql-server/install/media/gmni-setupui-donotconfiguremoss.gif "GMNI_SetupUI_DoNotConfigureMOSS")

## <a name="see-also"></a>Consulte también
 [Instalación e implementación para SharePoint server 2010](https://technet.microsoft.com/sharepoint/ee518643.aspx) [varios servidores para una granja de tres niveles (SharePoint Server 2010)](https://go.microsoft.com/fwlink/?linkID=219834)


