---
title: Características de la colección de sitios de Reporting Services | Microsoft Docs
ms.date: 09/25/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server-sharepoint
ms.topic: conceptual
author: maggiesMSFT
ms.author: maggies
monikerRange: '>=sql-server-2016 <=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: e13654a38738c84095cc284a24fb723aa2b05327
ms.sourcegitcommit: dda9a1a7682ade466b8d4f0ca56f3a9ecc1ef44e
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 05/14/2019
ms.locfileid: "65580501"
---
# <a name="reporting-services-site-collection-features"></a>Características de la colección de sitios de Reporting Services

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016](../../includes/ssrs-appliesto-2016.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)] [!INCLUDE[ssrs-appliesto-not-pbirsi](../../includes/ssrs-appliesto-not-pbirs.md)]

[!INCLUDE [ssrs-previous-versions](../../includes/ssrs-previous-versions.md)]

El modo de SharePoint de Reporting Services proporciona tres características de la colección de sitios de SharePoint. Las características admiten el entorno de informes del modo de SharePoint de Reporting Services general, [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)], una característica del Complemento SQL Server 2016 Reporting Services y las operaciones de administración para Reporting Services en Administración central de SharePoint.

> [!NOTE]
> La integración de Reporting Services con SharePoint ya no está disponible a partir de SQL Server 2016.
  
## <a name="site-collection-features"></a>Características de la colección de sitios

 En la tabla siguiente se describen las características de la colección de sitios de Reporting Services.  
  
|Característica|Descripción|  
|-------------|-----------------|  
|**Característica Administración central del servidor de informes**|Habilita las características para administrar la integración con un servidor de informes de Reporting Services. Esta característica solo se instala y se puede usar en la colección de sitios de Administración central de SharePoint.<br /><br /> La característica de integración del servidor de informes se activa de forma automática en la colección de sitios Administración central de SharePoint tras instalar el Complemento [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] para los productos de SharePoint. En algunas situaciones, tendrá que activar la característica de forma manual. Para activar la característica del servidor de informes, use las páginas de Reporting Services de la página Configuración del sitio de Administración central de SharePoint.<br /><br /> La versión de [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] Reporting Services y posterior del complemento para productos de SharePoint activa la característica de integración del servidor de informes para todas las colecciones de sitios existentes cuando se instala el complemento. Además, la característica se activa automáticamente para las nuevas colecciones de sitios.|  
|**Característica de integración del servidor de informes**|Permite la creación de informes avanzados mediante [!INCLUDE[msCoName](../../includes/msconame-md.md)] Reporting Services<br /><br /> Esta característica está activa de forma predeterminada.|  
|**Característica Power View Integration**|Habilita la exploración interactiva de los datos y la presentación visual de los libros [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] y las bases de datos tabulares de Analysis Services.<br /><br /> Se puede tener acceso a la característica en los menús contextuales de los siguientes orígenes de datos:<br /><br /> **.rdlx**<br /><br /> **.rsds**<br /><br /> archivo de conexión **.bism** <br /><br /> <br /><br /> Si [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] no aparece en los menús contextuales, compruebe que la **característica Power View Integration** está activada.<br /><br /> Esta característica está desactivada de forma predeterminada.|  

## <a name="next-steps"></a>Pasos siguientes

[Activar las características de integración del servidor de informes y Power View en SharePoint](../../reporting-services/report-server-sharepoint/site-collection-features-report-server-and-power-view.md)   
[Valores de configuración del sitio de Reporting Services y características del sitio &#40;modo de SharePoint&#41;](../../reporting-services/report-server-sharepoint/site-settings-and-features-reporting-services.md)   
[Activar la característica de sincronización de archivos del servidor de informes en Administración central de SharePoint](../../reporting-services/report-server-sharepoint/activate-the-report-server-file-sync-feature-in-sharepoint-ca.md)  

¿Tiene alguna pregunta más? [Puede plantear sus dudas en el foro de Reporting Services](https://go.microsoft.com/fwlink/?LinkId=620231).
