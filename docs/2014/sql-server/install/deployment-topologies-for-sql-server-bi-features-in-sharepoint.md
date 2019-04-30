---
title: Topologías de implementación para las características SQL Server BI en SharePoint | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
ms.assetid: 39f76bc7-94e6-4dbc-bfa5-d56f4430bb26
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 2bcb706eda464730d978d0098281c2ebcd2336ed
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63192270"
---
# <a name="deployment-topologies-for-sql-server-bi-features-in-sharepoint"></a>Topologías de implementación para las características BI de SQL Server en SharePoint
  En este tema se describen las topologías comunes para instalar las características [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] y [!INCLUDE[ssGeminiShortvnext](../../includes/ssgeminishortvnext-md.md)] de SQL Server Business Intelligence en entornos de SharePoint 2010 y SharePoint 2013. Por ejemplo, instalaciones de un solo servidor y tres niveles.  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  SharePoint 2013 &#124; SharePoint 2010|  
  
 **En este tema:**  
  
-   [Topologías de implementación de ejemplo de SharePoint 2013](#bkmk_example_deployments_2013)  
  
    -   [Implementación en tres servidores de PowerPivot para SharePoint 2013 y Reporting Services](#bkmk_bi_Sharepoint2013_3tier)  
  
    -   [PowerPivot para SharePoint 2013 solo servidor de implementación](#bkmk_powerpivot_sharepoint2013_1server)  
  
    -   [PowerPivot para SharePoint 2013 implementación en dos servidores](#bkmk_powerpivot_sharepoint2013_2server)  
  
    -   [PowerPivot para SharePoint 2013 implementación en tres servidores](#bkmk_powerpivot_sharepoint2013_3server)  
  
    -   [PowerPivot para SharePoint 2013 y Reporting Services implementación de servidor único](#bkmk_powerpivot_ssrs_sharepoint2013_1server)  
  
    -   [Implementación en dos servidores de PowerPivot para SharePoint 2013 y Reporting Services](#bkmk_powerpivot_ssrs_sharepoint2013_2server)  
  
-   [Topologías de implementación de ejemplo de SharePoint 2010](#bkmk_example_deployments_2010)  
  
    -   [Implementaciones de servidor único](#bkmk_sharepoint2010_1server)  
  
    -   [Implementación de dos niveles](#bkmk_sharepoint2010_2server)  
  
    -   [Implementación de tres niveles](#bkmk_sharepoint2010_3server)  
  
    -   [Implementación escalada de tres niveles](#bkmk_sharepoint2010_scaleserver)  
  
##  <a name="bkmk_example_deployments_2013"></a> Topologías de implementación de ejemplo de SharePoint 2013  
 La opción de instalación de SQL Server **PowerPivot para SharePoint** no tiene ninguna dependencia en SharePoint. No usa el modelo de objetos ni las interfaces de SharePoint para admitir la integración. Por tanto, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] se puede instalar en cualquier equipo que ejecute Windows Server 2008 R2 o una versión posterior. No obstante, el equipo no puede ser un servidor de aplicaciones de una granja de SharePoint. Uno de los pasos de configuración consiste en que Excel Services apunte al servidor que ejecuta [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Para lograr equilibrio de carga y tolerancia a errores, se recomienda instalar y registrar varios servidores de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que se ejecuten en modo de SharePoint.  
  
 **[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] El modo de SharePoint** requiere SharePoint server 2013 y usa la arquitectura de aplicación de servicio de SharePoint.  
  
 En las próximas secciones se muestran topologías típicas de implementación:  
  
###  <a name="bkmk_bi_Sharepoint2013_3tier"></a> Implementación en tres servidores de PowerPivot para SharePoint 2013 y Reporting Services  
 En la siguiente implementación en tres servidores, el motor de base de datos de SQL Server, el servidor de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] en modo de SharePoint y SharePoint se ejecutan cada uno en un servidor diferente. El paquete del instalador de [!INCLUDE[ssGeminiShortvnext](../../includes/ssgeminishortvnext-md.md)] 2013 (**spPowerPivot.msi**) se debe ejecutar en el servidor de SharePoint.  
  
 ![Modo SSAS y SSRS SharePoint 3 implementación de servidor](../../../2014/sql-server/install/media/as-and-rs-3server-deployment.gif "modo SSAS y SSRS SharePoint 3 implementación de servidor")  
  
|||  
|-|-|  
|**(1)**|Aplicación de servicio de Excel. La aplicación de servicio se crea como parte de la instalación de SharePoint.|  
|**(2)**|[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] Aplicación de servicio. El nombre predeterminado es **Aplicación de servicio PowerPivot predeterminada**.|  
|**(3)**|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .|  
|**(4)**|Instale el complemento Reporting Services para SharePoint desde el disco de instalación de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] o Feature Pack de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] .|  
|**(5)**|Ejecute el archivo **spPowerPivot.msi** para instalar proveedores de datos, la herramienta de configuración de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] , la Galería de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] y la actualización de datos programada.|  
|**(6)**|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Servidor en modo de SharePoint. Configure el valor de **Configuración del modelo de datos** de la aplicación Excel Services para usar este servidor.|  
|**(7)**|Bases de datos de contenido, configuración y aplicación de servicio de SharePoint.|  
  
 ![Configuración de SharePoint](../../../2014/analysis-services/media/as-sharepoint2013-settings-gear.gif "configuración de SharePoint") [enviar comentarios e información de contacto a través de Microsoft SQL Server Connect](https://connect.microsoft.com/SQLServer/Feedback) (https://connect.microsoft.com/SQLServer/Feedback).  
  
###  <a name="bkmk_powerpivot_sharepoint2013_1server"></a> PowerPivot para SharePoint 2013 solo servidor de implementación  
 Una implementación en un solo servidor es útil para realizar pruebas, pero no se recomienda en implementaciones de producción.  
  
 En el diagrama siguiente se muestran los componentes que forman parte de una implementación de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] de un solo servidor.  
  
 ![PowerPivot para la implementación de servidor único de SharePoint](../../../2014/sql-server/install/media/as-powerpivot-mode-1server-deployment.gif "PowerPivot para la implementación de servidor único de SharePoint")  
  
|||  
|-|-|  
|**(1)**|Aplicación de servicio de Excel. La aplicación de servicio se crea como parte de la instalación de SharePoint.|  
|**(2)**|[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] Aplicación de servicio. El nombre predeterminado es **Aplicación de servicio PowerPivot predeterminada**.|  
|**(3)**|Bases de datos de contenido, configuración y aplicación de servicio de SharePoint.|  
|**(4)**|Servidor de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] en modo de SharePoint. Configure el valor de **Configuración del modelo de datos** de la aplicación Excel Services para usar este servidor.|  
  
###  <a name="bkmk_powerpivot_sharepoint2013_2server"></a> PowerPivot para SharePoint 2013 implementación en dos servidores  
 En la siguiente implementación en dos servidores, el motor de base de datos de SQL Server y [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] en modo de SharePoint se ejecutan en un servidor diferente que SharePoint. Para SharePoint 2013, el paquete del instalador de [!INCLUDE[ssGeminiLongvnext](../../includes/ssgeminilongvnext-md.md)] (**spPowerPivot.msi**) se instala en el servidor de SharePoint.  
  
 [!INCLUDE[ssGeminiShortvnext](../../includes/ssgeminishortvnext-md.md)] extiende SharePoint Server 2013 para agregar la actualización de datos del servidor de procesamiento, los proveedores de datos, [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] galería y la posibilidad de administrar para [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] libros y libros de Excel con modelos de datos avanzados.  
  
 El paquete del instalador está disponible como parte de [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Feature Pack. El feature pack se puede descargar desde el [!INCLUDE[msCoName](../../includes/msconame-md.md)] centro de descarga en [Microsoft® SQL Server® 2014 PowerPivot® para Microsoft® SharePoint®](https://go.microsoft.com/fwlink/?LinkID=296473) (HYPERLINK "<https://go.microsoft.com/fwlink/?LinkID=296473>" \t "_blank" <https://go.microsoft.com/fwlink/?LinkID=296473>).  
  
 ![Implementación del servidor de modo 2 de PowerPivot SSAS](../../../2014/analysis-services/media/as-powerpivot-mode-2server-deployment.gif "implementación del servidor de modo 2 de PowerPivot SSAS")  
  
|||  
|-|-|  
|**(1)**|Aplicación de servicio de Excel. La aplicación de servicio se crea como parte de la instalación de SharePoint.|  
|**(2)**|[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] Aplicación de servicio. El nombre predeterminado es **Aplicación de servicio PowerPivot predeterminada**.|  
|**(3)**|EJECUTE el archivo **spPowerPivot.msi** para instalar proveedores de datos, la herramienta de configuración de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] , la Galería de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] y la actualización de datos programada.|  
|**(4)**|Servidor de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] en modo de SharePoint. Configure el valor de **Configuración del modelo de datos** de la aplicación Excel Services para usar este servidor.|  
|**(5)**|Bases de datos de contenido, configuración y aplicación de servicio de SharePoint.|  
  
###  <a name="bkmk_powerpivot_sharepoint2013_3server"></a> PowerPivot para SharePoint 2013 implementación en tres servidores  
 En la siguiente implementación en tres servidores, el motor de base de datos de SQL Server, el servidor de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] en modo de SharePoint y SharePoint se ejecutan cada uno en un servidor diferente. El paquete del instalador de [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 2013 (spPowerPivot.msi) se debe instalar en el servidor de SharePoint.  
  
 ![COMO la implementación de servidor de modo 3 de PowerPivot](../../../2014/sql-server/install/media/as-powerpivot-mode-3server-deployment.gif "como implementación de servidor de modo 3 de PowerPivot")  
  
|||  
|-|-|  
|**(1)**|Aplicación de servicio de Excel. La aplicación de servicio se crea como parte de la instalación de SharePoint.|  
|**(2)**|[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] Aplicación de servicio. El nombre predeterminado es **Aplicación de servicio PowerPivot predeterminada**.|  
|**(3)**|EJECUTE el archivo spPowerPivot.msi para instalar proveedores de datos, la herramienta de configuración de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] , la Galería de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] y la actualización de datos programada.|  
|**(4)**|Servidor de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] en modo de SharePoint. Configure el valor de **Configuración del modelo de datos** de la aplicación Excel Services para usar este servidor.|  
|**(5)**|Bases de datos de contenido, configuración y aplicación de servicio de SharePoint.|  
  
###  <a name="bkmk_powerpivot_ssrs_sharepoint2013_1server"></a> PowerPivot para SharePoint 2013 y Reporting Services implementación de servidor único  
 Una implementación en un solo servidor es útil para realizar pruebas, pero no se recomienda en implementaciones de producción.  
  
 ![Modo SSAS y SSRS SharePoint 1 implementación del servidor](../../../2014/sql-server/install/media/as-and-rs-1server-deployment.gif "modo SSAS y SSRS SharePoint 1 implementación del servidor")  
  
|||  
|-|-|  
|**(1)**|Aplicación de servicio de Excel. La aplicación de servicio se crea como parte de la instalación de SharePoint.|  
|**(2)**|Aplicación de servicio PowerPivot. El nombre predeterminado es **Aplicación de servicio PowerPivot predeterminada**.|  
|**(3)**|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .|  
|**(4)**|Instale el complemento Reporting Services para SharePoint desde el disco de instalación de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] o Feature Pack de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] .|  
|**(5)**|Bases de datos de contenido, configuración y aplicación de servicio de SharePoint.|  
|**(6)**|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Servidor en modo de SharePoint. Configure el valor de **Configuración del modelo de datos** de la aplicación Excel Services para usar este servidor.|  
  
###  <a name="bkmk_powerpivot_ssrs_sharepoint2013_2server"></a> Implementación en dos servidores de PowerPivot para SharePoint 2013 y Reporting Services  
 En la implementación siguiente en dos servidores, el motor de base de datos de SQL Server y el servidor de Analysis Services en modo de SharePoint se ejecutan en un servidor diferente que SharePoint. El paquete del instalador de PowerPivot para SharePoint 2013 **(spPowerPivot.msi)** se debe ejecutar en el servidor de SharePoint.  
  
 ![SSAS y la implementación de servidor SSRS SharePoint modo 2](../../../2014/sql-server/install/media/as-and-rs-2server-deployment.gif "SSAS e implementación de servidores de SharePoint de modo 2 de SSRS")  
  
|||  
|-|-|  
|**(1)**|Aplicación de servicio de Excel. La aplicación de servicio se crea como parte de la instalación de SharePoint.|  
|**(2)**|Aplicación de servicio PowerPivot. El nombre predeterminado es **Aplicación de servicio PowerPivot predeterminada**.|  
|**(3)**|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .|  
|**(4)**|Instale el complemento Reporting Services para SharePoint desde el disco de instalación de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] o Feature Pack de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] .|  
|**(5)**|Ejecute el archivo **spPowerPivot.msi** para instalar proveedores de datos, la herramienta de configuración de PowerPivot, la galería de PowerPivot y la actualización de datos programada.|  
|**(6)**|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Servidor en modo de SharePoint. Configure el valor de **Configuración del modelo de datos** de la aplicación Excel Services para usar este servidor.|  
|**(7)**|Bases de datos de contenido, configuración y aplicación de servicio de SharePoint.|  
  
##  <a name="bkmk_example_deployments_2010"></a> Topologías de implementación de ejemplo de SharePoint 2010  
 El diagrama siguiente presenta qué servicios y proveedores se ejecutan en cada nivel. Observe que el diagrama incluye varios servicios integrados; estos servicios se requieren en algunos escenarios BI de SQL Server. Excel Services, Servicio de almacenamiento seguro y Notificaciones al servicio de token de Windows se requieren o se recomiendan en una implementación de Reporting Services o PowerPivot para SharePoint en SharePoint. Además, los proveedores OLE DB MSOLAP y Servicios ADO.NET se requieren en algunos escenarios de acceso a datos PowerPivot. Opcionalmente, puede instalar Analysis Services en el nivel de datos, si desea compilar informes de [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] basados en las bases de datos de modelos tabulares que se hospedan fuera de SharePoint.  
  
 ![Diagrama de arquitectura lógica](../../../2014/sql-server/install/media/sql11bisetup.gif "diagrama de arquitectura lógica")  
  
##  <a name="bkmk_sharepoint2010_1server"></a> Implementaciones de servidor único  
 Puede instalar todos los componentes de servidor, incluso el nivel de datos, en un único equipo. Esta configuración de implementación resulta útil para evaluar el software o desarrollar aplicaciones personalizadas con Reporting Services en el modo de SharePoint. Esta implementación es la más sencilla de configurar. Puesto que todos los componentes se instalan en el mismo equipo, también utiliza el menor número de licencias. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] y el [!INCLUDE[ssDE](../../includes/ssde-md.md)] se instalan como una única copia con licencia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Para instalar todas las características en un único servidor, instale [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] y [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] secuencialmente en el mismo servidor físico. Para obtener instrucciones acerca de una configuración de servidor independiente, consulte [lista de comprobación de implementación: Reporting Services, Power View y PowerPivot para SharePoint](deployment-checklist-reporting-services-power-view-power-pivot-for-sharepoint.md).  
  
##  <a name="bkmk_sharepoint2010_2server"></a> Implementación de dos niveles  
 Una implementación en dos niveles suele ser SharePoint Server 2010 en un equipo y el Motor de base de datos de SQL Server en el otro. Mover el nivel de datos a un servidor dedicado es la configuración más común para una granja de dos equipos. En una granja de dos niveles, se instala [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] y [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] en el servidor de SharePoint. Todos los servicios web en los servicios front-end y compartidos del nivel de aplicación se ejecutan en el mismo servidor físico. Los pasos de instalación para una implementación de dos niveles son muy similares a una implementación independiente, en el sentido de que se instala [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] y [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] secuencialmente en el mismo servidor físico.  
  
##  <a name="bkmk_sharepoint2010_3server"></a> Implementación de tres niveles  
 Una implementación de tres niveles normalmente separa los servicios front-end web de las aplicaciones que utilizan mucha memoria o de proceso. En esta topología, se instala [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] y [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] solo en el servidor de aplicaciones. Los servicios web que se ejecutan en el front-end web se instalan a través de soluciones que se implementan en las aplicaciones de la granja, durante la configuración del servidor, como una tarea posterior a la instalación. El siguiente diagrama muestra una implementación de tres niveles.  
  
 ![topología de servidor de 3](../../../2014/sql-server/install/media/sql11bisetup-3server.gif "topología de servidor de 3")  
  
##  <a name="bkmk_sharepoint2010_scaleserver"></a> Implementación escalada de tres niveles  
 Esta topología muestra una implementación escalada que ejecuta el mismo servicio compartido en varios servidores, atiende un volumen mayor de solicitudes y proporciona una capacidad de procesamiento mayor para los datos PowerPivot o los informes de Reporting Services. En el diagrama siguiente, hay tres clústeres de servidor de aplicaciones y cada uno ejecuta una combinación diferente de servicios compartidos. En un entorno de SharePoint, la detección de servicios y la disponibilidad están integradas en la granja. El equilibrio de carga entre varios servidores físicos que ejecutan la misma aplicación de servicio compartida forma parte de la arquitectura compartida del servicio.  
  
 Al implementar una granja multiservidor, asegúrese de seguir las instrucciones de este artículo de SharePoint: [Varios servidores para una granja de tres niveles (SharePoint Server 2010)](https://go.microsoft.com/fwlink/?linkID=219834).  
  
 ![topología de 5 servidores](../../../2014/sql-server/install/media/sql11bisetup-5server.gif "topología de 5 servidores")  
  
## <a name="see-also"></a>Vea también  
 [Instalación en modo de SharePoint de Reporting Services &#40;SharePoint 2010 y SharePoint 2013&#41;](../../reporting-services/install-windows/install-reporting-services-sharepoint-mode.md)   
 [PowerPivot para SharePoint 2013 Installation](../../analysis-services/instances/install-windows/install-analysis-services-in-power-pivot-mode.md)   
 [Instalación de PowerPivot para SharePoint 2010](../../../2014/sql-server/install/powerpivot-for-sharepoint-2010-installation.md)  
  
  
