---
title: Topologías de implementación para características de BI de SQL Server en SharePoint Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 39f76bc7-94e6-4dbc-bfa5-d56f4430bb26
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 2ba357fc3910779573ffa36f3070b55c08ced8ee
ms.sourcegitcommit: a3f5c3742d85d21f6bde7c6ae133060dcf1ddd44
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/15/2020
ms.locfileid: "81388727"
---
# <a name="deployment-topologies-for-sql-server-bi-features-in-sharepoint"></a>Topologías de implementación para las características BI de SQL Server en SharePoint
  En este tema se describen las topologías comunes para instalar las características [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] y [!INCLUDE[ssGeminiShortvnext](../../includes/ssgeminishortvnext-md.md)] de SQL Server Business Intelligence en entornos de SharePoint 2010 y SharePoint 2013. Por ejemplo, instalaciones de un solo servidor y tres niveles.  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]** SharePoint 2013 &#124; SharePoint 2010|  
  
 **En este tema:**  
  
-   [Topologías de implementación de ejemplo de SharePoint 2013](#bkmk_example_deployments_2013)  
  
    -   [Implementación en tres servidores de PowerPivot para SharePoint 2013 y Reporting Services](#bkmk_bi_Sharepoint2013_3tier)  
  
    -   [Implementación en un solo servidor de PowerPivot para SharePoint 2013](#bkmk_powerpivot_sharepoint2013_1server)  
  
    -   [Implementación en dos servidores de PowerPivot para SharePoint 2013](#bkmk_powerpivot_sharepoint2013_2server)  
  
    -   [Implementación en tres servidores de PowerPivot para SharePoint 2013](#bkmk_powerpivot_sharepoint2013_3server)  
  
    -   [Implementación en un solo servidor de PowerPivot para SharePoint 2013 y Reporting Services](#bkmk_powerpivot_ssrs_sharepoint2013_1server)  
  
    -   [Implementación en dos servidores de PowerPivot para SharePoint 2013 y Reporting Services](#bkmk_powerpivot_ssrs_sharepoint2013_2server)  
  
-   [Topologías de implementación de ejemplo de SharePoint 2010](#bkmk_example_deployments_2010)  
  
    -   [Implementaciones de un solo servidor](#bkmk_sharepoint2010_1server)  
  
    -   [Implementación en dos niveles](#bkmk_sharepoint2010_2server)  
  
    -   [Implementación de tres niveles](#bkmk_sharepoint2010_3server)  
  
    -   [Implementación escalada de tres niveles](#bkmk_sharepoint2010_scaleserver)  
  
##  <a name="sharepoint-2013-example-deployment-topologies"></a><a name="bkmk_example_deployments_2013"></a>Topologías de implementación de ejemplo de SharePoint 2013  
 La opción de instalación de SQL Server **PowerPivot para SharePoint** no tiene ninguna dependencia en SharePoint. No usa el modelo de objetos ni las interfaces de SharePoint para admitir la integración. Por tanto, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] se puede instalar en cualquier equipo que ejecute Windows Server 2008 R2 o una versión posterior. No obstante, el equipo no puede ser un servidor de aplicaciones de una granja de SharePoint. Uno de los pasos de configuración consiste en que Excel Services apunte al servidor que ejecuta [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Para lograr equilibrio de carga y tolerancia a errores, se recomienda instalar y registrar varios servidores de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que se ejecuten en modo de SharePoint.  
  
 El modo de SharePoint requiere SharePoint Server 2013 y utiliza la arquitectura de aplicación de servicio de SharePoint. ** [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] **  
  
 En las próximas secciones se muestran topologías típicas de implementación:  
  
###  <a name="powerpivot-for-sharepoint-2013-and-reporting-services-three-server-deployment"></a><a name="bkmk_bi_Sharepoint2013_3tier"></a>PowerPivot para SharePoint 2013 y Reporting Services 2 Server Deployment  
 En la siguiente implementación en tres servidores, el motor de base de datos de SQL Server, el servidor de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] en modo de SharePoint y SharePoint se ejecutan cada uno en un servidor diferente. El paquete del instalador de [!INCLUDE[ssGeminiShortvnext](../../includes/ssgeminishortvnext-md.md)] 2013 (**spPowerPivot.msi**) se debe ejecutar en el servidor de SharePoint.  
  
 ![Modo 3 de implementación de servidores de SSAS y de SSRS de SharePoint](../../../2014/sql-server/install/media/as-and-rs-3server-deployment.gif "Modo 3 de implementación de servidores de SSAS y de SSRS de SharePoint")  
  
|||  
|-|-|  
|**(1)**|Aplicación de servicio de Excel. La aplicación de servicio se crea como parte de la instalación de SharePoint.|  
|**(2)**|[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]Aplicación de servicio. El nombre predeterminado es **Aplicación de servicio PowerPivot predeterminada**.|  
|**(3)**|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .|  
|**(4)**|Instale el complemento Reporting Services para SharePoint desde el disco de instalación de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] o Feature Pack de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] .|  
|**(5)**|Ejecute **spPowerPivot.msi** para instalar proveedores de datos, la [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] herramienta de configuración, [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] la Galería y programar la actualización de datos.|  
|**(6)**|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]Servidor en modo SharePoint. Configure el valor de **Configuración del modelo de datos** de la aplicación Excel Services para usar este servidor.|  
|**(7)**|Bases de datos de contenido, configuración y aplicación de servicio de SharePoint.|  
  
 ![Configuración de SharePoint](../../analysis-services/media/as-sharepoint2013-settings-gear.gif "Configuración de SharePoint") [Enviar comentarios e información](https://connect.microsoft.com/SQLServer/Feedback) de contacto a través de Microsoft SQL Server Connect (https://connect.microsoft.com/SQLServer/Feedback).  
  
###  <a name="powerpivot-for-sharepoint-2013-single-server-deployment"></a><a name="bkmk_powerpivot_sharepoint2013_1server"></a>PowerPivot para la implementación de servidor único de SharePoint 2013  
 Una implementación en un solo servidor es útil para realizar pruebas, pero no se recomienda en implementaciones de producción.  
  
 En el diagrama siguiente se muestran los componentes que forman parte de una implementación de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] de un solo servidor.  
  
 ![Implementación de un solo servidor de PowerPivot para SharePoint](../../../2014/sql-server/install/media/as-powerpivot-mode-1server-deployment.gif "Implementación de un solo servidor de PowerPivot para SharePoint")  
  
|||  
|-|-|  
|**(1)**|Aplicación de servicio de Excel. La aplicación de servicio se crea como parte de la instalación de SharePoint.|  
|**(2)**|[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]Aplicación de servicio. El nombre predeterminado es **Aplicación de servicio PowerPivot predeterminada**.|  
|**(3)**|Bases de datos de contenido, configuración y aplicación de servicio de SharePoint.|  
|**(4)**|Servidor de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] en modo de SharePoint. Configure el valor de **Configuración del modelo de datos** de la aplicación Excel Services para usar este servidor.|  
  
###  <a name="powerpivot-for-sharepoint-2013-two-server-deployment"></a><a name="bkmk_powerpivot_sharepoint2013_2server"></a>PowerPivot para SharePoint 2013 Implementación de dos servidores  
 En la siguiente implementación en dos servidores, el motor de base de datos de SQL Server y [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] en modo de SharePoint se ejecutan en un servidor diferente que SharePoint. Para SharePoint 2013, el paquete del instalador de [!INCLUDE[ssGeminiLongvnext](../../includes/ssgeminilongvnext-md.md)] (**spPowerPivot.msi**) se instala en el servidor de SharePoint.  
  
 [!INCLUDE[ssGeminiShortvnext](../../includes/ssgeminishortvnext-md.md)]extiende SharePoint Server 2013 para agregar procesamiento de actualización [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] de datos del [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] lado del servidor, proveedores de datos, Galería y compatibilidad de administración para libros de trabajo y libros de Excel con modelos de datos avanzados.  
  
 El paquete del instalador está disponible como parte de [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Feature Pack. El paquete de características se [!INCLUDE[msCoName](../../includes/msconame-md.md)] puede descargar desde el centro de descargas de [Microsoft® SQL Server® 2014 PowerPivot® para Microsoft® SharePoint®](https://go.microsoft.com/fwlink/?LinkID=296473) ( HYPERLINK "<https://go.microsoft.com/fwlink/?LinkID=296473>" " "_blank" <https://go.microsoft.com/fwlink/?LinkID=296473>).  
  
 ![Modo 2 de implementación de servidores SSAS PowerPivot](../../analysis-services/media/as-powerpivot-mode-2server-deployment.gif "Modo 2 de implementación de servidores SSAS PowerPivot")  
  
|||  
|-|-|  
|**(1)**|Aplicación de servicio de Excel. La aplicación de servicio se crea como parte de la instalación de SharePoint.|  
|**(2)**|[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]Aplicación de servicio. El nombre predeterminado es **Aplicación de servicio PowerPivot predeterminada**.|  
|**(3)**|EJECUTE el archivo **spPowerPivot.msi** para instalar proveedores de datos, la herramienta de configuración de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] , la Galería de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] y la actualización de datos programada.|  
|**(4)**|Servidor de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] en modo de SharePoint. Configure el valor de **Configuración del modelo de datos** de la aplicación Excel Services para usar este servidor.|  
|**(5)**|Bases de datos de contenido, configuración y aplicación de servicio de SharePoint.|  
  
###  <a name="powerpivot-for-sharepoint-2013-three-server-deployment"></a><a name="bkmk_powerpivot_sharepoint2013_3server"></a>PowerPivot para SharePoint 2013 Implementación de tres servidores  
 En la siguiente implementación en tres servidores, el motor de base de datos de SQL Server, el servidor de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] en modo de SharePoint y SharePoint se ejecutan cada uno en un servidor diferente. El paquete del instalador de [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 2013 (spPowerPivot.msi) se debe instalar en el servidor de SharePoint.  
  
 ![Modo 3 de implementación de servidores AS PowerPivot](../../../2014/sql-server/install/media/as-powerpivot-mode-3server-deployment.gif "Modo 3 de implementación de servidores AS PowerPivot")  
  
|||  
|-|-|  
|**(1)**|Aplicación de servicio de Excel. La aplicación de servicio se crea como parte de la instalación de SharePoint.|  
|**(2)**|[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]Aplicación de servicio. El nombre predeterminado es **Aplicación de servicio PowerPivot predeterminada**.|  
|**(3)**|EJECUTE el archivo spPowerPivot.msi para instalar proveedores de datos, la herramienta de configuración de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] , la Galería de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] y la actualización de datos programada.|  
|**(4)**|Servidor de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] en modo de SharePoint. Configure el valor de **Configuración del modelo de datos** de la aplicación Excel Services para usar este servidor.|  
|**(5)**|Bases de datos de contenido, configuración y aplicación de servicio de SharePoint.|  
  
###  <a name="powerpivot-for-sharepoint-2013-and-reporting-services-single-server-deployment"></a><a name="bkmk_powerpivot_ssrs_sharepoint2013_1server"></a>PowerPivot para SharePoint 2013 y Implementación de servidor único de Reporting ServicesReporting Services  
 Una implementación en un solo servidor es útil para realizar pruebas, pero no se recomienda en implementaciones de producción.  
  
 ![Implementación de servidor sSAS y SSRS SharePoint mode 1](../../../2014/sql-server/install/media/as-and-rs-1server-deployment.gif "Implementación de servidor sSAS y SSRS SharePoint mode 1")  
  
|||  
|-|-|  
|**(1)**|Aplicación de servicio de Excel. La aplicación de servicio se crea como parte de la instalación de SharePoint.|  
|**(2)**|Aplicación de servicio PowerPivot. El nombre predeterminado es **Aplicación de servicio PowerPivot predeterminada**.|  
|**(3)**|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .|  
|**(4)**|Instale el complemento Reporting Services para SharePoint desde el disco de instalación de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] o Feature Pack de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] .|  
|**(5)**|Bases de datos de contenido, configuración y aplicación de servicio de SharePoint.|  
|**(6)**|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]Servidor en modo SharePoint. Configure el valor de **Configuración del modelo de datos** de la aplicación Excel Services para usar este servidor.|  
  
###  <a name="powerpivot-for-sharepoint-2013-and-reporting-services-two-server-deployment"></a><a name="bkmk_powerpivot_ssrs_sharepoint2013_2server"></a>PowerPivot para SharePoint 2013 y Reporting Services 2 Server Deployment  
 En la implementación siguiente en dos servidores, el motor de base de datos de SQL Server y el servidor de Analysis Services en modo de SharePoint se ejecutan en un servidor diferente que SharePoint. El paquete del instalador de PowerPivot para SharePoint 2013 **(spPowerPivot.msi)** se debe ejecutar en el servidor de SharePoint.  
  
 ![Modo 2 de implementación de servidores de SSAS y de SSRS de SharePoint](../../../2014/sql-server/install/media/as-and-rs-2server-deployment.gif "Modo 2 de implementación de servidores de SSAS y de SSRS de SharePoint")  
  
|||  
|-|-|  
|**(1)**|Aplicación de servicio de Excel. La aplicación de servicio se crea como parte de la instalación de SharePoint.|  
|**(2)**|Aplicación de servicio PowerPivot. El nombre predeterminado es **Aplicación de servicio PowerPivot predeterminada**.|  
|**(3)**|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .|  
|**(4)**|Instale el complemento Reporting Services para SharePoint desde el disco de instalación de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] o Feature Pack de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] .|  
|**(5)**|Ejecute el archivo **spPowerPivot.msi** para instalar proveedores de datos, la herramienta de configuración de PowerPivot, la galería de PowerPivot y la actualización de datos programada.|  
|**(6)**|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]Servidor en modo SharePoint. Configure el valor de **Configuración del modelo de datos** de la aplicación Excel Services para usar este servidor.|  
|**(7)**|Bases de datos de contenido, configuración y aplicación de servicio de SharePoint.|  
  
##  <a name="sharepoint-2010-example-deployment-topologies"></a><a name="bkmk_example_deployments_2010"></a>Topologías de implementación de ejemplo de SharePoint 2010  
 El diagrama siguiente presenta qué servicios y proveedores se ejecutan en cada nivel. Observe que el diagrama incluye varios servicios integrados; estos servicios se requieren en algunos escenarios BI de SQL Server. Excel Services, Servicio de almacenamiento seguro y Notificaciones al servicio de token de Windows se requieren o se recomiendan en una implementación de Reporting Services o PowerPivot para SharePoint en SharePoint. Además, los proveedores OLE DB MSOLAP y Servicios ADO.NET se requieren en algunos escenarios de acceso a datos PowerPivot. Opcionalmente, puede instalar Analysis Services en el nivel de datos, si desea compilar informes de [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] basados en las bases de datos de modelos tabulares que se hospedan fuera de SharePoint.  
  
 ![Diagrama de arquitectura lógica](../../../2014/sql-server/install/media/sql11bisetup.gif "Diagrama de arquitectura lógica")  
  
##  <a name="single-server-deployments"></a><a name="bkmk_sharepoint2010_1server"></a>Implementaciones de servidor único  
 Puede instalar todos los componentes de servidor, incluso el nivel de datos, en un único equipo. Esta configuración de implementación resulta útil para evaluar el software o desarrollar aplicaciones personalizadas con Reporting Services en el modo de SharePoint. Esta implementación es la más sencilla de configurar. Puesto que todos los componentes se instalan en el mismo equipo, también utiliza el menor número de licencias. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] y el [!INCLUDE[ssDE](../../includes/ssde-md.md)] se instalan como una única copia con licencia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Para instalar todas las características en un único servidor, instale [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] y [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] secuencialmente en el mismo servidor físico. Para obtener instrucciones sobre una configuración de servidor independiente, vea Lista de comprobación de [implementación: Reporting ServicesReporting Services, Power View y PowerPivot para SharePoint](deployment-checklist-reporting-services-power-view-power-pivot-for-sharepoint.md).  
  
##  <a name="two-tier-deployment"></a><a name="bkmk_sharepoint2010_2server"></a>Despliegue de dos niveles  
 Una implementación en dos niveles suele ser SharePoint Server 2010 en un equipo y el Motor de base de datos de SQL Server en el otro. Mover el nivel de datos a un servidor dedicado es la configuración más común para una granja de dos equipos. En una granja de dos niveles, se instala [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] y [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] en el servidor de SharePoint. Todos los servicios web en los servicios front-end y compartidos del nivel de aplicación se ejecutan en el mismo servidor físico. Los pasos de instalación para una implementación de dos niveles son muy similares a una implementación independiente, en el sentido de que se instala [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] y [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] secuencialmente en el mismo servidor físico.  
  
##  <a name="three-tier-deployment"></a><a name="bkmk_sharepoint2010_3server"></a>Despliegue de tres niveles  
 Una implementación de tres niveles normalmente separa los servicios front-end web de las aplicaciones que utilizan mucha memoria o de proceso. En esta topología, se instala [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] y [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] solo en el servidor de aplicaciones. Los servicios web que se ejecutan en el front-end web se instalan a través de soluciones que se implementan en las aplicaciones de la granja, durante la configuración del servidor, como una tarea posterior a la instalación. El siguiente diagrama muestra una implementación de tres niveles.  
  
 ![Toplogía de 3 servidores](../../../2014/sql-server/install/media/sql11bisetup-3server.gif "Toplogía de 3 servidores")  
  
##  <a name="three-tier-scale-out-deployment"></a><a name="bkmk_sharepoint2010_scaleserver"></a>Despliegue de escalabilidad horizontal de tres niveles  
 Esta topología muestra una implementación escalada que ejecuta el mismo servicio compartido en varios servidores, atiende un volumen mayor de solicitudes y proporciona una capacidad de procesamiento mayor para los datos PowerPivot o los informes de Reporting Services. En el diagrama siguiente, hay tres clústeres de servidor de aplicaciones y cada uno ejecuta una combinación diferente de servicios compartidos. En un entorno de SharePoint, la detección de servicios y la disponibilidad están integradas en la granja. El equilibrio de carga entre varios servidores físicos que ejecutan la misma aplicación de servicio compartida forma parte de la arquitectura compartida del servicio.  
  
 Al implementar una granja multiservidor, asegúrese de seguir las indicaciones de este artículo de SharePoint: [Varios servidores para una granja de tres niveles (SharePoint Server 2010)](https://go.microsoft.com/fwlink/?linkID=219834).  
  
 ![Topología de 5 servidores](../../../2014/sql-server/install/media/sql11bisetup-5server.gif "Topología de 5 servidores")  
  
## <a name="see-also"></a>Consulte también  
 [Instalación en modo SharePoint de Reporting ServicesReporting Services &#40;SharePoint 2010 y SharePoint 2013&#41;](../../reporting-services/install-windows/install-reporting-services-sharepoint-mode.md)   
 [Instalación de PowerPivot para SharePoint 2013](https://docs.microsoft.com/analysis-services/instances/install-windows/install-analysis-services-in-power-pivot-mode)   
 [Instalación de PowerPivot para SharePoint 2010](../../../2014/sql-server/install/powerpivot-for-sharepoint-2010-installation.md)  
  
  
