---
title: "Características de colección de sitios Reporting Services | Documentos de Microsoft"
ms.custom: 
ms.date: 05/30/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: e05ae162-a4b2-489d-9853-d6b09414e632
caps.latest.revision: 8
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: b68204ab4c9a008db7c43d2c568d1c3ccedbcb7a
ms.contentlocale: es-es
ms.lasthandoff: 06/22/2017

---

# <a name="site-collection-features---reporting-services"></a>Características de colección de sitios - Reporting Services

[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint proporciona tres características de la colección de sitios de SharePoint. Las características admiten la ficha general [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] informes entorno, de modo de SharePoint [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)], una característica del SQL Server 2016 Reporting Services Add-de y operaciones de administración para [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] en Administración Central de SharePoint.  
  
## <a name="site-collection-features"></a>Características de la colección de sitios  
 En la siguiente tabla, se describen las características de la colección de sitios [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
|Característica|Description|  
|-------------|-----------------|  
|**Característica Administración central del servidor de informes**|Habilita las características para administrar la integración con un servidor de informes de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Esta característica solo se instala y se puede usar en la colección de sitios de Administración central de SharePoint.<br /><br /> La característica de integración del servidor de informes se activa de forma automática en la colección de sitios Administración central de SharePoint tras instalar el Complemento [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] para los productos de SharePoint. En algunas situaciones, tendrá que activar la característica de forma manual. Para activar la característica del servidor de informes, use las páginas de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] de la página Configuración de sitio de Administración central de SharePoint.<br /><br /> La versión de [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)][!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] o posterior de los productos del Complemento para SharePoint activará la característica de integración del servidor de informes para todas las colecciones de sitios existentes cuando se instale el complemento. Además, la característica estará activa automáticamente para las nuevas colecciones de sitios.|  
|**Característica de integración del servidor de informes**|Habilita el informe completo mediante [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]<br /><br /> Esta característica está activa de forma predeterminada.|  
|**Característica Power View Integration**|Habilita la exploración interactiva de los datos y la presentación visual de los libros [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] y las bases de datos tabulares de Analysis Services.<br /><br /> Se puede tener acceso a la característica en los menús contextuales de los siguientes orígenes de datos:<br /><br /> **.rdlx**<br /><br /> **.rsds**<br /><br /> archivo de conexión**.bism** <br /><br /> <br /><br /> Si [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] no aparece en los menús contextuales, compruebe que la **característica Power View Integration** está activada.<br /><br /> Esta característica está desactivada de forma predeterminada.|  

## <a name="next-steps"></a>Pasos siguientes

[Activar las características de integración del servidor de informes y Power View en SharePoint](../../reporting-services/report-server-sharepoint/site-collection-features-report-server-and-power-view.md)   
[Configuración del sitio y características del sitio &#40; de Reporting Services Modo de SharePoint &#41;](../../reporting-services/report-server-sharepoint/site-settings-and-features-reporting-services.md)   
[Activar la característica de sincronización de archivos del servidor de informes en Administración central de SharePoint](../../reporting-services/report-server-sharepoint/activate-the-report-server-file-sync-feature-in-sharepoint-ca.md)  

¿Más preguntas? [Pruebe a formular el foro de Reporting Services](http://go.microsoft.com/fwlink/?LinkId=620231)
