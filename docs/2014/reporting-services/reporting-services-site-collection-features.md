---
title: Características de colección de sitios Reporting Services | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: e05ae162-a4b2-489d-9853-d6b09414e632
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 43b45b7e1bd2d8a4ba10870cc442e73aecbbc618
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63283588"
---
# <a name="reporting-services-site-collection-features"></a>Características de la colección de sitios Reporting Services
  [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] SharePoint proporciona tres características de la colección de sitios de SharePoint. Las características admiten el entorno de informes de modo SharePoint de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] general, [!INCLUDE[ssCrescent](../includes/sscrescent-md.md)], una característica del Complemento [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)][!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] para [!INCLUDE[SPS2010](../includes/sps2010-md.md)] Enterprise Edition, y las operaciones de administración para [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] en Administración central de SharePoint.  
  
## <a name="site-collection-features"></a>Características de la colección de sitios  
 En la siguiente tabla, se describen las características de la colección de sitios [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] .  
  
|Característica|Descripción|  
|-------------|-----------------|  
|**Característica Administración central del servidor de informes**|Habilita las características para administrar la integración con un servidor de informes de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] . Esta característica solo se instala y se puede usar en la colección de sitios de Administración central de SharePoint.<br /><br /> La característica de integración del servidor de informes se activa de forma automática en la colección de sitios Administración central de SharePoint tras instalar el Complemento [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssRSCurrent](../includes/ssrscurrent-md.md)] para los productos de SharePoint. En algunas situaciones, tendrá que activar la característica de forma manual. Para activar la característica del servidor de informes, use las páginas de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] de la página Configuración de sitio de Administración central de SharePoint.<br /><br /> La versión de [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)][!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] o posterior de los productos del Complemento para SharePoint activará la característica de integración del servidor de informes para todas las colecciones de sitios existentes cuando se instale el complemento. Además, la característica estará activa automáticamente para las nuevas colecciones de sitios.|  
|**Característica de integración del servidor de informes**|Habilita el informe completo mediante [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]<br /><br /> Esta característica está activa de forma predeterminada.|  
|**Característica Power View Integration**|Habilita la exploración interactiva de los datos y la presentación visual de los libros de trabajo PowerPivot y las bases de datos tabulares de Analysis Services.<br /><br /> Se puede tener acceso a la característica en los menús contextuales de los siguientes orígenes de datos:<br /><br /> .rdlx<br /><br /> .rsds<br /><br /> archivo de conexión .bism<br /><br /> <br /><br /> Si [!INCLUDE[ssCrescent](../includes/sscrescent-md.md)] no aparece en los menús contextuales, compruebe que la **característica Power View Integration** está activada.<br /><br /> Esta característica está desactivada de forma predeterminada.|  
  
## <a name="see-also"></a>Vea también  
 [Activar las características de integración del servidor de informes y Power View en SharePoint](activate-the-report-server-and-power-view-integration-features-in-sharepoint.md)   
 [Valores de configuración del sitio de Reporting Services y características del sitio &#40;modo de SharePoint&#41;](../../2014/reporting-services/reporting-services-site-settings-and-site-features-sharepoint-mode.md)   
 [Activar la característica de sincronización de archivos del servidor de informes en Administración central de SharePoint](../../2014/reporting-services/activate-report-server-file-sync-feature-sharepoint-central-administration.md)  
  
  
