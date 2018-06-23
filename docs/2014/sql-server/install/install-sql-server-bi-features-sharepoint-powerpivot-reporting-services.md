---
title: Instalar las características de BI de SQL Server con SharePoint (Reporting Services y PowerPivot) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 3166107c-30c2-468e-bb1b-bb42b79b37c3
caps.latest.revision: 20
author: markingmyname
ms.author: maghan
manager: jhubbard
ms.openlocfilehash: 25c8c6d8c5d83ba3661d30ed85f560d0aa18a54d
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36106690"
---
# <a name="install-sql-server-bi-features-with-sharepoint-powerpivot-and-reporting-services"></a>Instalar las características de SQL Server BI con SharePoint (PowerPivot y Reporting Services)
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] y [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] pueden integrarse con una granja de SharePoint de Microsoft para habilitar las características de Business Intelligence (BI) en SharePoint. Las características se incluyen [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)], [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)], y [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] se utiliza para [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] acceso a datos en una granja de servidores de SharePoint. [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] es el motor de datos para los libros creados en [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para Excel y accesibles desde una biblioteca de SharePoint. Una vez que guarde un [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] libro en SharePoint, puede usar como origen de datos para [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] informes.  
  
 Algunos de los pasos de instalación y configuración necesarios para SharePoint 2010 son diferentes de los requeridos para SharePoint 2013. Algunos de los temas de esta sección se aplican a ambas versiones de SharePoint.  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  SharePoint 2013 &#124; SharePoint 2010|  
  
 ![Tenga en cuenta](../../../2014/reporting-services/media/rs-fyinote.png "Nota") para las notas de la versión actual, vea [notas de la versión de SQL server 2014](http://go.microsoft.com/fwlink/?LinkID=296445).  
  
##  <a name="bkmk_top"></a> En este tema  
  
-   [Escenarios de BI de SQL Server y SharePoint 2013](#bkmk_bi_scenarios)  
  
-   [Información general de instalación](#bkmk_install_sharepoint2013_overview)  
  
## <a name="in-this-section"></a>En esta sección  
 Además de la información de este tema, en esta sección de contenido se incluyen los temas relacionados siguientes.  
  
 [Topologías de implementación para las características de BI de SQL Server en SharePoint](deployment-topologies-for-sql-server-bi-features-in-sharepoint.md)  
  
 [Instrucciones para usar características de BI de SQL Server en una granja de servidores de SharePoint 2010](../../../2014/sql-server/install/guidance-for-using-sql-server-bi-features-in-a-sharepoint-2010-farm.md)  
  
 [Listas de comprobación para instalar las características de BI con SharePoint](../../../2014/sql-server/install/checklists-for-installing-bi-features-with-sharepoint.md)  
  
 [Instalación en modo de SharePoint de Reporting Services &#40;SharePoint 2010 y SharePoint 2013&#41;](../../reporting-services/install-windows/install-reporting-services-sharepoint-mode.md)  
  
 [PowerPivot para SharePoint 2013](../../analysis-services/instances/install-windows/install-analysis-services-in-power-pivot-mode.md)  
  
 [PowerPivot para SharePoint 2010](../../../2014/sql-server/install/powerpivot-for-sharepoint-2010-installation.md)  
  
##  <a name="bkmk_bi_scenarios"></a> Escenarios de BI de SQL Server y SharePoint 2013  
 En esta sección se resumen los distintos niveles de características de BI que puede instalar y configurar.  
  
 Excel Services en SharePoint 2013 incluye funcionalidad de modelo de datos para habilitar la interacción con un libro [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] en el explorador. Para la funcionalidad de modelo de datos básicos no es necesario implementar el [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] complemento 2013 en la granja de servidores. Solo se necesita instalar un servidor [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] en modo de SharePoint y registrarlo dentro de la configuración de **Modelo de datos** de Excel Services.  
  
 Implementar el [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] complemento 2013 habilita funcionalidad adicional y características en la granja de servidores de SharePoint. Las características adicionales se incluyen [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] galería, actualización de datos programada y el panel de administración de PowerPivot. Vea la tabla para obtener información adicional.  
  
||Nivel|Características|Instalar o configurar|  
|-|-----------|--------------|--------------------------|  
|1|Solo SharePoint|Características nativas de Excel Services|Excel Services y otros servicios incluidos con SharePoint Server 2013.|  
|**2**|SharePoint con Analysis Services en modo de SharePoint|Libros PowerPivot interactivos en el explorador|Instalar [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] en modo de SharePoint.<br /><br /> Registrar servidor de Analysis Services en Excel Services.|  
|**3**|SharePoint con Reporting Services en modo de SharePoint|Power View|Instalar [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] en modo de SharePoint.<br /><br /> Instalar [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] complemento **(rsSharePoint.msi)** para SharePoint. Para obtener más información, consulte [instalar o desinstalar el complemento de Reporting Services para SharePoint &#40;SharePoint 2010 y SharePoint 2013&#41;](../../reporting-services/install-windows/install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md)|  
|**4**|Todas las características de PowerPivot|Acceso a libros como un origen de datos desde fuera de la granja de servidores.<br /><br /> Programar actualizaciones de datos.<br /><br /> Galería de PowerPivot.<br /><br /> Panel de administración.<br /><br /> Tipo de contenido de archivo de vínculo de BISM.|Implementar el complemento PowerPivot para SharePoint 2013 **(spPowerPivot.msi)**. Para obtener más información, vea:<br /><br /> [Instalar o desinstalar PowerPivot para SharePoint complemento &#40;SharePoint 2013&#41;](../../analysis-services/instances/install-windows/install-or-uninstall-the-power-pivot-for-sharepoint-add-in-sharepoint-2013.md)<br /><br /> Para obtener información sobre cómo descargar **spPowerPivot.msi**, vea [Descargar SQL Server 2014 PowerPivot para SharePoint](http://go.microsoft.com/fwlink/?LinkID=296473).|  
  
 Para obtener información adicional acerca de cómo habilitar [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] características, consulte [The SQL Server BI historia para SharePoint 2013](http://blogs.msdn.com/b/analysisservices/archive/2012/07/27/introducing-the-bi-light-up-story-for-sharepoint-2013.aspx) (http://blogs.msdn.com/b/analysisservices/archive/2012/07/27/introducing-the-bi-light-up-story-for-sharepoint-2013.aspx).  
  
##  <a name="bkmk_install_sharepoint2013_overview"></a> Información general de instalación  
 Si desea utilizar ambas [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] y [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], ejecute dos veces el Asistente para la instalación de SQL Server. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] y [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] son opciones diferentes en el **rol de instalación** página del Asistente de instalación de SQL Server.  
  
 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] admite SharePoint 2010 y SharePoint 2013; Sin embargo se utiliza un proceso de instalación y arquitectura diferente según la versión de SharePoint.  
  
 A continuación se muestra un resumen de los pasos de instalación para implementar características de BI de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] en un único servidor:  
  
 **[!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 2013**  
  
 Para **SharePoint 2013**, el [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] instalación se puede ejecutar en un servidor que no tiene instalado un producto de SharePoint. El [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] arquitectura que se usa para SharePoint 2013, se ejecuta **fuera** la granja de servidores de SharePoint y puede instalar en un servidor que también contiene una instalación de SharePoint o puede ser instalado en un servidor que no contiene una Instalación de SharePoint.  
  
1.  Instale SharePoint Server 2013 y habilite Excel Services.  
  
2.  Instale [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] en modo de SharePoint y conceda a las cuentas de servicios y de granja de SharePoint derechos de administrador del servidor en [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
     En ambas versiones de SharePoint, el [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] proceso de instalación se inicia con la selección de la instalación del rol **SQL Server PowerPivot para SharePoint** en el Asistente para la instalación de SQL Server o utilice un símbolo del sistema de SQL Server instalación.  
  
     ![Rol de instalación](../../../2014/sql-server/install/media/gmni-setupui-featurerole-sql2012sp1.gif "rol de instalación")  
  
3.  Para SharePoint 2013, puede ampliar el [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] características y la experiencia. Descargue y ejecute **spPowerPivot.msi** para agregar compatibilidad de procesamiento, colaboración y administración de actualización de datos del lado servidor para [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] libro. Para obtener más información, vea [Microsoft SQL Server 2014 PowerPivot para Microsoft® SharePoint](http://go.microsoft.com/fwlink/?LinkID=324854).  
  
     Ejecute el [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] paquete de instalación de 2013 **spPowerPivot.msi** en cada servidor de la granja de SharePoint para asegurarse de la versión correcta de los datos se instalan proveedores.  
  
4.  Para configurar [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint 2013, use **PowerPivot para SharePoint 2013** herramienta.  
  
     El Asistente para la instalación de SQL Server instala dos [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] herramientas de configuración. Una de las herramientas de configuración admite SharePoint 2013 y la otra admite SharePoint 2010.  
  
     ![dos herramientas de configuración de PowerPivot](../../../2014/analysis-services/media/as-powerpivot-configtools-bothicons.gif "dos herramientas de configuración de PowerPivot")  
  
5.  Configure Excel Services en SharePoint Server 2013 para usar la instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Para obtener más información, vea la sección "Configurar la integración básica de Analysis Services SharePoint" en [PowerPivot para SharePoint 2013 Installation](../../analysis-services/instances/install-windows/install-analysis-services-in-power-pivot-mode.md)y [(SharePoint Server de la configuración del modelo de datos de administrar servicios de Excel 2013)](http://technet.microsoft.com/library/jj219780.aspx) (http://technet.microsoft.com/library/jj219780.aspx).  
  
6.  Para obtener más información, consulte [PowerPivot para SharePoint 2013 Installation](../../analysis-services/instances/install-windows/install-analysis-services-in-power-pivot-mode.md).  
  
 **[!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 2010**  
  
 En SharePoint 2010, es necesario que la instalación de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint se ejecute en un servidor en el que se instalará SharePoint 2010 o que ya lo tenga instalado. El [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] arquitectura para SharePoint 2010 se ejecuta **en** la granja y requiere SharePoint en el servidor que [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint está instalado.  
  
1.  Instale [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] en modo de SharePoint y conceda a las cuentas de servicios y de granja de SharePoint derechos de administrador del servidor en [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
     Las implementaciones de SharePoint 2010 no admiten spPowerPivot.msi, y el archivo .msi **no** es necesario con SharePoint 2010.  
  
     En ambas versiones de SharePoint, el [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] proceso de instalación se inicia con la selección de la instalación del rol **SQL Server PowerPivot para SharePoint** en el Asistente para la instalación de SQL Server o utilice un símbolo del sistema de SQL Server instalación.  
  
2.  El Asistente para la instalación de SQL Server instala dos [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] herramientas de configuración. Una de las herramientas de configuración admite SharePoint 2013 y la otra admite SharePoint 2010.  
  
     Para configurar [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint 2010, use la **herramienta de configuración de PowerPivot** .  
  
3.  Para obtener más información, vea [PowerPivot for SharePoint 2010 Installation](../../../2014/sql-server/install/powerpivot-for-sharepoint-2010-installation.md).  
  
 **[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]**  para SharePoint 2010 y 2013  
  
1.  La instalación de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] en SharePoint, modo ha cambiado desde la versión anterior.  
  
     El [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] pasos de instalación para SharePoint 2010 y SharePoint 2013 son muy similares. Notas importantes con respecto a las versiones de SharePoint:  
  
    -   Vea las combinaciones admitidas de lo siguiente:  
  
        -   Versión de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
        -   El complemento [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para productos de SharePoint.  
  
        -   La versión de idioma del producto SharePoint.  
  
         [Combinaciones admitidas de SharePoint y Reporting Services Server y el complemento &#40;SQL Server 2014&#41;](../../reporting-services/install-windows/supported-combinations-of-sharepoint-and-reporting-services-server.md)  
  
    -   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] en SharePoint 2010 requiere SharePoint 2010 Service Pack 2 (SP2).  
  
    1.  Instalar [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] en modo de SharePoint. [Instalación en modo de SharePoint de Reporting Services &#40;SharePoint 2010 y SharePoint 2013&#41; ](../../reporting-services/install-windows/install-reporting-services-sharepoint-mode.md) y [instalar Reporting Services el modo de SharePoint para SharePoint 2010](../../../2014/sql-server/install/install-reporting-services-sharepoint-mode-for-sharepoint-2010.md).  
  
    2.  Instalar el complemento [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para productos de SharePoint (rsSharePoint.msi). Vea [instalar o desinstalar el complemento Servicios de informes para SharePoint &#40;SharePoint 2010 y SharePoint 2013&#41;](../../reporting-services/install-windows/install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md). Para la versión actual de la [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] complemento para SharePoint, consulte [dónde encontrar el complemento de Reporting Services para productos de SharePoint](../../reporting-services/install-windows/where-to-find-the-reporting-services-add-in-for-sharepoint-products.md).  
  
    3.  Configurar la [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] servicio de SharePoint y al menos un [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] aplicación de servicio. Para obtener más información, vea la sección "Crear una aplicación Reporting Services Service" en [instalar Reporting Services SharePoint Mode for SharePoint 2013](../../../2014/sql-server/install/install-reporting-services-sharepoint-mode-for-sharepoint-2013.md).  
  
##  <a name="bkm_database_attach"></a> Información general de adjuntar la base de datos de actualización y SharePoint 2013  
 SharePoint 2013 no admite la actualización en contexto. Sin embargo, **se admite actualizar y adjuntar la base de datos**.  
  
 Si tiene una instalación existente de PowerPivot integrada con SharePoint 2010, no puede realizar una actualización en contexto del servidor de SharePoint.  Sin embargo, puede completar los pasos siguientes como parte del procedimiento de actualizar y adjuntar una base de datos de SharePoint:  
  
1.  Instale una nueva granja de servidores de SharePoint Server 2013.  
  
2.  Complete el procedimiento para actualizar y adjuntar una base de datos de SharePoint, y migre las bases de datos de contenido de PowerPivot a la granja de SharePoint 2013.  
  
3.  Instale una instancia de SQL Server Analysis Services en modo de SharePoint y conceda a las cuentas de servicios y de granja de SharePoint derechos de administrador del servidor en [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
4.  Instale el paquete de instalación de PowerPivot para SharePoint 2013 **spPowerPivot.msi** en todos los servidores de la granja de SharePoint.  
  
5.  En Administración central de SharePoint 2013, configure Excel Services para que use el servidor de Analysis Services que se ejecuta en modo de SharePoint creado en el paso 3.  
  
     Para migrar las programaciones de actualización, configure la aplicación de servicio PowerPivot.  
  
> [!NOTE]  
>  Para obtener más información acerca de PowerPivot y cómo actualizar y adjuntar la base de datos de SharePoint, vea lo siguiente:  
  
-   [Migrar PowerPivot para SharePoint 2013](../../analysis-services/instances/install-windows/migrate-power-pivot-to-sharepoint-2013.md)  
  
-   [Información general del proceso de actualización a SharePoint 2013](http://go.microsoft.com/fwlink/p/?LinkId=256688).  
  
-   [Limpiar un entorno antes de realizar una actualización a SharePoint 2013](http://go.microsoft.com/fwlink/p/?LinkId=256689).  
  
-   [Actualizar bases de datos de SharePoint 2010 a SharePoint 2013](http://go.microsoft.com/fwlink/p/?LinkId=256690).  
  
## <a name="see-also"></a>Vea también  
 [Dónde encontrar el complemento Reporting Services para Productos de SharePoint](../../reporting-services/install-windows/where-to-find-the-reporting-services-add-in-for-sharepoint-products.md)   
 [Combinaciones admitidas de SharePoint y Reporting Services Server y el complemento &#40;SQL Server 2014&#41;](../../reporting-services/install-windows/supported-combinations-of-sharepoint-and-reporting-services-server.md)   
 [Instalar o desinstalar el complemento Servicios de informes para SharePoint &#40;SharePoint 2010 y SharePoint 2013&#41;](../../reporting-services/install-windows/install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md)  
  
  