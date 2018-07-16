---
title: Características de colección de sitios Reporting Services | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: e05ae162-a4b2-489d-9853-d6b09414e632
caps.latest.revision: 5
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: eb321258a8dc87a499479d66ced85b95ce643b6d
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37294125"
---
# <a name="reporting-services-site-collection-features"></a>Características de la colección de sitios Reporting Services
  El modo de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] SharePoint proporciona tres características de la colección de sitios de SharePoint. Las características admiten el general [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] informes entorno, de modo SharePoint [!INCLUDE[ssCrescent](../includes/sscrescent-md.md)], una característica de la [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] complemento para [!INCLUDE[SPS2010](../includes/sps2010-md.md)] Enterprise Edition y las operaciones de administración para [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] en Administración Central de SharePoint.  
  
## <a name="site-collection-features"></a>Características de la colección de sitios  
 En la siguiente tabla, se describen las características de la colección de sitios [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)].  
  
|Característica|Descripción|  
|-------------|-----------------|  
|**Característica Administración central del servidor de informes**|Habilita las características para administrar la integración con un servidor de informes de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] . Esta característica solo se instala y se puede usar en la colección de sitios de Administración central de SharePoint.<br /><br /> La característica de integración del servidor de informes se activa automáticamente en la colección de sitios de Administración Central de SharePoint después de instalar el [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssRSCurrent](../includes/ssrscurrent-md.md)] complemento para productos de SharePoint. En algunas situaciones, tendrá que activar la característica de forma manual. Para activar la característica del servidor de informes, use las páginas de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] de la página Configuración de sitio de Administración central de SharePoint.<br /><br /> El [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] versión o posterior del complemento para SharePoint productos activará la característica de integración del servidor de informes para todas las colecciones de sitios existentes cuando se instala el complemento. Además, la característica estará activa automáticamente para las nuevas colecciones de sitios.|  
|**Característica de integración del servidor de informes**|Habilita el informe completo mediante [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]<br /><br /> Esta característica está activa de forma predeterminada.|  
|**Característica Power View Integration**|Habilita la exploración interactiva de los datos y la presentación visual de los libros de trabajo PowerPivot y las bases de datos tabulares de Analysis Services.<br /><br /> Se puede tener acceso a la característica en los menús contextuales de los siguientes orígenes de datos:<br /><br /> .rdlx<br /><br /> .rsds<br /><br /> archivo de conexión .bism<br /><br /> <br /><br /> Si [!INCLUDE[ssCrescent](../includes/sscrescent-md.md)] no aparece en los menús contextuales, compruebe que la **característica Power View Integration** está activada.<br /><br /> Esta característica está desactivada de forma predeterminada.|  
  
## <a name="see-also"></a>Vea también  
 [Activar el servidor de informes y Power View Integration Features in SharePoint](activate-the-report-server-and-power-view-integration-features-in-sharepoint.md)   
 [Configuración del sitio de servicios y características del sitio de informes&#40;el modo de SharePoint&#41;](../../2014/reporting-services/reporting-services-site-settings-and-site-features-sharepoint-mode.md)   
 [Activar la característica de sincronización de archivos del servidor de informes en Administración central de SharePoint](../../2014/reporting-services/activate-report-server-file-sync-feature-sharepoint-central-administration.md)  
  
  
