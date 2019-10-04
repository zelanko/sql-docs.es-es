---
title: Instalación de características de SQL Server BI con SharePoint (PowerPivot y Reporting Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 3166107c-30c2-468e-bb1b-bb42b79b37c3
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 42bc370a4e1eebddb3293afe6843f3ed19338656
ms.sourcegitcommit: ffe2fa1b22e6040cdbd8544fb5a3083eed3be852
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/04/2019
ms.locfileid: "71952137"
---
# <a name="install-sql-server-bi-features-with-sharepoint-powerpivot-and-reporting-services"></a>Instalar las características de SQL Server BI con SharePoint (PowerPivot y Reporting Services)
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] y [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] se pueden integrar con una granja de Microsoft SharePoint para habilitar las características de Business Intelligence (BI) en SharePoint. Entre las características se incluyen [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)], [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)]y [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] se usa para el acceso a datos [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] en una granja de servidores de SharePoint. [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] es el motor de datos para los libros creados en [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para Excel y accesibles desde una biblioteca de SharePoint. Una vez que guarde un libro de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] en SharePoint, puede utilizarlo como origen de datos para los informes de [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] .  
  
 Algunos de los pasos de instalación y configuración necesarios para SharePoint 2010 son diferentes de los requeridos para SharePoint 2013. Algunos de los temas de esta sección se aplican a ambas versiones de SharePoint.  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  SharePoint 2013 &#124; SharePoint 2010|  
  
 ![Nota:](../../../2014/reporting-services/media/rs-fyinote.png "para obtener") las notas de la versión actuales, consulte las notas de la [versión de SQL Server 2014](https://go.microsoft.com/fwlink/?LinkID=296445).  
  
##  <a name="bkmk_top"></a> En este tema  
  
-   [Escenarios de SQL Server BI y SharePoint 2013](#bkmk_bi_scenarios)  
  
-   [Información general sobre la instalación](#bkmk_install_sharepoint2013_overview)  
  
## <a name="in-this-section"></a>En esta sección  
 Además de la información de este tema, en esta sección de contenido se incluyen los temas relacionados siguientes.  
  
 [Topologías de implementación para las características de SQL Server BI en SharePoint](deployment-topologies-for-sql-server-bi-features-in-sharepoint.md)  
  
 [Instrucciones para usar las características de SQL Server BI en una granja de servidores de SharePoint 2010](../../../2014/sql-server/install/guidance-for-using-sql-server-bi-features-in-a-sharepoint-2010-farm.md)  
  
 [Listas de comprobación para instalar características de BI con SharePoint](../../../2014/sql-server/install/checklists-for-installing-bi-features-with-sharepoint.md)  
  
 [Instalación &#40;del modo de sharepoint de Reporting Services SharePoint 2010 y SharePoint 2013&#41;](../../reporting-services/install-windows/install-reporting-services-sharepoint-mode.md)  
  
 [Instalación de PowerPivot para SharePoint 2013](https://docs.microsoft.com/analysis-services/instances/install-windows/install-analysis-services-in-power-pivot-mode)  
  
 [Instalación de PowerPivot para SharePoint 2010](../../../2014/sql-server/install/powerpivot-for-sharepoint-2010-installation.md)  
  
##  <a name="bkmk_bi_scenarios"></a>Escenarios de SQL Server BI y SharePoint 2013  
 En esta sección se resumen los distintos niveles de características de BI que puede instalar y configurar.  
  
 Excel Services en SharePoint 2013 incluye funcionalidad de modelo de datos para habilitar la interacción con un libro [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] en el explorador. Para la funcionalidad básica de modelo de datos no es necesario implementar el complemento [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 2013 en la granja. Solo se necesita instalar un servidor [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] en modo de SharePoint y registrarlo dentro de la configuración de **Modelo de datos** de Excel Services.  
  
 La implementación del complemento [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 2013 habilita funcionalidad y características adicionales en la granja de servidores de SharePoint. Entre las características adicionales se incluyen Galería de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] , Actualización de datos programada y Panel de administración de PowerPivot. Vea la tabla para obtener información adicional.  
  
||Nivel|Características|Instalar o configurar|  
|-|-----------|--------------|--------------------------|  
|1|Solo SharePoint|Características nativas de Excel Services|Excel Services y otros servicios incluidos con SharePoint Server 2013.|  
|**2**|SharePoint con Analysis Services en modo de SharePoint|Libros PowerPivot interactivos en el explorador|Instalar [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] en modo de SharePoint.<br /><br /> Registrar servidor de Analysis Services en Excel Services.|  
|**3**|SharePoint con Reporting Services en modo de SharePoint|Power View|Instalar [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] en modo de SharePoint.<br /><br /> Instalar el complemento [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] **(rsSharePoint.msi)** para SharePoint. Para obtener más información, vea [instalar o desinstalar el complemento de Reporting Services para SharePoint &#40;SharePoint 2010 y SharePoint 2013&#41; ](../../reporting-services/install-windows/install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md)|  
|**4**|Todas las características de PowerPivot|Acceso a libros como un origen de datos desde fuera de la granja de servidores.<br /><br /> Programar actualizaciones de datos.<br /><br /> Galería de PowerPivot.<br /><br /> Panel de administración.<br /><br /> Tipo de contenido de archivo de vínculo de BISM.|Implementar el complemento PowerPivot para SharePoint 2013 **(spPowerPivot.msi)** . Para obtener más información, vea:<br /><br /> [Instalar o desinstalar el complemento de PowerPivot para SharePoint de &#40;SharePoint 2013&#41;](https://docs.microsoft.com/analysis-services/instances/install-windows/install-or-uninstall-the-power-pivot-for-sharepoint-add-in-sharepoint-2013)<br /><br /> Para obtener información sobre cómo descargar **spPowerPivot.msi**, vea [Descargar SQL Server 2014 PowerPivot para SharePoint](https://go.microsoft.com/fwlink/?LinkID=296473).|  
  
 Para obtener información adicional sobre cómo habilitar las características de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], consulte [el artículo sobre la SQL Server BI para SharePoint 2013](https://blogs.msdn.com/b/analysisservices/archive/2012/07/27/introducing-the-bi-light-up-story-for-sharepoint-2013.aspx) (@no__t 2.  
  
##  <a name="bkmk_install_sharepoint2013_overview"></a>Información general sobre la instalación  
 Si desea usan tanto [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] como [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], ejecute dos veces el Asistente para la instalación de SQL Server. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] y [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] son opciones independientes en la página **rol de instalación** del Asistente para la instalación de SQL Server.  
  
 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] admite SharePoint 2010 y SharePoint 2013; sin embargo, se utilizan una arquitectura y un proceso de instalación distintos en función de la versión de SharePoint.  
  
 A continuación se muestra un resumen de los pasos de instalación para implementar características de BI de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] en un único servidor:  
  
 **[!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 2013**  
  
 En **SharePoint 2013**, la instalación de [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] se puede ejecutar en un servidor que no tiene productos SharePoint instalados. La arquitectura de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] que se usa para SharePoint 2013 se ejecuta **fuera** de la granja de servidores de SharePoint y se puede instalar en un servidor que también contiene una instalación de SharePoint o bien se puede instalar en un servidor que NO contenga una instalación de SharePoint.  
  
1.  Instale SharePoint Server 2013 y habilite Excel Services.  
  
2.  Instale [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] en modo de SharePoint y conceda a las cuentas de servicios y de granja de SharePoint derechos de administrador del servidor en [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
     En ambas versiones de SharePoint, el proceso de instalación de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] se inicia con la selección de la instalación del rol **SQL Server PowerPivot para SharePoint** en el Asistente para la instalación de SQL Server o utilizando una instalación desde el símbolo del sistema de SQL Server.  
  
     ![](../../../2014/sql-server/install/media/gmni-setupui-featurerole-sql2012sp1.gif "Rol") de configuración de rol de instalación  
  
3.  Para SharePoint 2013, puede ampliar las características y la experiencia de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . Descargue y ejecute **spPowerPivot.msi** para agregar compatibilidad con procesamiento, colaboración y administración de actualización de datos del servidor para los libros [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . Para obtener más información, vea [Microsoft SQL Server 2014 PowerPivot para Microsoft® SharePoint](https://go.microsoft.com/fwlink/?LinkID=324854).  
  
     Ejecute el paquete de instalación de [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 2013 **spPowerPivot.msi** en cada servidor de la granja de SharePoint para asegurarse de que se instala la versión correcta de los proveedores de datos.  
  
4.  Para configurar [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint 2013, use la herramienta **Configuración de PowerPivot para SharePoint 2013** .  
  
     El asistente para la instalación de SQL Server instala dos herramientas de configuración de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . Una de las herramientas de configuración admite SharePoint 2013 y la otra admite SharePoint 2010.  
  
     ![dos herramientas de configuración de PowerPivot](https://docs.microsoft.com/analysis-services/analysis-services/media/as-powerpivot-configtools-bothicons.gif "dos herramientas de configuración de PowerPivot")  
  
5.  Configure Excel Services en SharePoint Server 2013 para usar la instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Para obtener más información, vea la sección "configurar la integración de SharePoint básica Analysis Services SharePoint" en [PowerPivot para SharePoint 2013 instalación](https://docs.microsoft.com/analysis-services/instances/install-windows/install-analysis-services-in-power-pivot-mode). y [administrar la configuración del modelo de datos de servicios de Excel (SharePoint Server 2013)](https://technet.microsoft.com/library/jj219780.aspx) (https://technet.microsoft.com/library/jj219780.aspx).  
  
6.  Para obtener más información, vea [PowerPivot for SharePoint 2013 Installation](https://docs.microsoft.com/analysis-services/instances/install-windows/install-analysis-services-in-power-pivot-mode).  
  
 **[!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 2010**  
  
 En SharePoint 2010, es necesario que la instalación de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint se ejecute en un servidor en el que se instalará SharePoint 2010 o que ya lo tenga instalado. La arquitectura de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint 2010 se ejecuta **dentro** de la granja y requiere SharePoint en el servidor en el que se ha instalado [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint.  
  
1.  Instale [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] en modo de SharePoint y conceda a las cuentas de servicios y de granja de SharePoint derechos de administrador del servidor en [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
     Las implementaciones de SharePoint 2010 no admiten spPowerPivot.msi, y el archivo .msi **no** es necesario con SharePoint 2010.  
  
     En ambas versiones de SharePoint, el proceso de instalación de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] se inicia con la selección de la instalación del rol **SQL Server PowerPivot para SharePoint** en el Asistente para la instalación de SQL Server o utilizando una instalación desde el símbolo del sistema de SQL Server.  
  
2.  El asistente para la instalación de SQL Server instala dos herramientas de configuración de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . Una de las herramientas de configuración admite SharePoint 2013 y la otra admite SharePoint 2010.  
  
     Para configurar [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint 2010, use la **Herramienta de configuración de PowerPivot** .  
  
3.  Para obtener más información, vea [PowerPivot for SharePoint 2010 Installation](../../../2014/sql-server/install/powerpivot-for-sharepoint-2010-installation.md).  
  
 **[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]**  para SharePoint 2010 y 2013  
  
1.  La instalación de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] en el modo de SharePoint no ha cambiado respecto a la versión anterior.  
  
     Los pasos de instalación de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para SharePoint 2010 y SharePoint 2013 son muy similares. Notas importantes con respecto a las versiones de SharePoint:  
  
    -   Vea las combinaciones admitidas de lo siguiente:  
  
        -   Versión de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
        -   El complemento [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para productos de SharePoint.  
  
        -   La versión de idioma del producto SharePoint.  
  
         [Combinaciones admitidas de SharePoint y Reporting Services Server y el complemento &#40;SQL Server 2014&#41;](../../reporting-services/install-windows/supported-combinations-of-sharepoint-and-reporting-services-server.md)  
  
    -   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] en SharePoint 2010 requiere SharePoint 2010 Service Pack 2 (SP2).  
  
    1.  Instalar [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] en modo de SharePoint. [Reporting Services la &#40;instalación del modo de SharePoint de SharePoint&#41; 2010 y SharePoint 2013](../../reporting-services/install-windows/install-reporting-services-sharepoint-mode.md) e [instalar el modo de SharePoint de Reporting Services para SharePoint 2010](../../../2014/sql-server/install/install-reporting-services-sharepoint-mode-for-sharepoint-2010.md).  
  
    2.  Instalar el complemento [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para productos de SharePoint (rsSharePoint.msi). Vea [instalar o desinstalar el complemento de Reporting Services para SharePoint &#40;SharePoint 2010 y SharePoint 2013&#41;](../../reporting-services/install-windows/install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md). Para obtener la versión actual del complemento [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para SharePoint, consulte [dónde encontrar el complemento de Reporting Services para productos de SharePoint](../../reporting-services/install-windows/where-to-find-the-reporting-services-add-in-for-sharepoint-products.md).  
  
    3.  Configurar el servicio SharePoint de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] y crear al menos una aplicación de servicio de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Para obtener más información, vea la sección "crear una aplicación de servicio de Reporting Services" en [instalar Reporting Services modo de SharePoint para sharepoint 2013](../../../2014/sql-server/install/install-reporting-services-sharepoint-mode-for-sharepoint-2013.md).  
  
##  <a name="bkm_database_attach"></a>Información general de la actualización de base de datos adjunta y SharePoint 2013  
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
  
-   [Migración de PowerPivot a SharePoint 2013](https://docs.microsoft.com/analysis-services/instances/install-windows/migrate-power-pivot-to-sharepoint-2013)  
  
-   [Información general del proceso de actualización a SharePoint 2013](https://go.microsoft.com/fwlink/p/?LinkId=256688).  
  
-   [Limpiar un entorno antes de realizar una actualización a SharePoint 2013](https://go.microsoft.com/fwlink/p/?LinkId=256689).  
  
-   [Actualizar bases de datos de SharePoint 2010 a SharePoint 2013](https://go.microsoft.com/fwlink/p/?LinkId=256690).  
  
## <a name="see-also"></a>Vea también  
 [Dónde encontrar el complemento Reporting Services para Productos de SharePoint](../../reporting-services/install-windows/where-to-find-the-reporting-services-add-in-for-sharepoint-products.md)   
 [Combinaciones admitidas de SharePoint y Reporting Services Server y el complemento &#40;SQL Server 2014&#41;](../../reporting-services/install-windows/supported-combinations-of-sharepoint-and-reporting-services-server.md)   
 [Instalar o desinstalar el complemento de Reporting Services para SharePoint &#40;SharePoint 2010 y SharePoint 2013&#41;](../../reporting-services/install-windows/install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md)  
  
  
