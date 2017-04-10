---
title: "Caracter&#237;sticas de la colecci&#243;n de sitios Reporting Services | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: e05ae162-a4b2-489d-9853-d6b09414e632
caps.latest.revision: 8
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
---
# Caracter&#237;sticas de la colecci&#243;n de sitios Reporting Services
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint proporciona tres características de la colección de sitios de SharePoint. Las características admiten el entorno de informes de modo SharePoint de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] general, [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)], una característica del Complemento [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)][!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para [!INCLUDE[SPS2010](../../includes/sps2010-md.md)] Enterprise Edition, y las operaciones de administración para [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] en Administración central de SharePoint.  
  
## Características de la colección de sitios  
 En la siguiente tabla, se describen las características de la colección de sitios [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
|Característica|Description|  
|-------------|-----------------|  
|**Característica Administración central del servidor de informes**|Habilita las características para administrar la integración con un servidor de informes de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Esta característica solo se instala y se puede usar en la colección de sitios de Administración central de SharePoint.<br /><br /> La característica de integración del servidor de informes se activa de forma automática en la colección de sitios Administración central de SharePoint tras instalar el Complemento [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] para los productos de SharePoint. En algunas situaciones, tendrá que activar la característica de forma manual. Para activar la característica del servidor de informes, use las páginas de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] de la página Configuración de sitio de Administración central de SharePoint.<br /><br /> La versión de [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)][!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] o posterior de los productos del Complemento para SharePoint activará la característica de integración del servidor de informes para todas las colecciones de sitios existentes cuando se instale el complemento. Además, la característica estará activa automáticamente para las nuevas colecciones de sitios.|  
|**Característica de integración del servidor de informes**|Habilita el informe completo mediante [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]<br /><br /> Esta característica está activa de forma predeterminada.|  
|**Característica Power View Integration**|Habilita la exploración interactiva de los datos y la presentación visual de los libros [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] y las bases de datos tabulares de Analysis Services.<br /><br /> Se puede tener acceso a la característica en los menús contextuales de los siguientes orígenes de datos:<br /><br /> **.rdlx**<br /><br /> **.rsds**<br /><br /> archivo de conexión**.bism** <br /><br /> <br /><br /> Si [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] no aparece en los menús contextuales, compruebe que la **característica Power View Integration** está activada.<br /><br /> Esta característica está desactivada de forma predeterminada.|  
  
## Vea también  
 [Activar las características de integración del servidor de informes y Power View en SharePoint](../../reporting-services/report-server-sharepoint/activate-the-report-server-and-power-view-integration-features-in-sharepoint.md)   
 [Valores de configuración del sitio de Reporting Services y características del sitio &#40;modo de SharePoint&#41;](../../reporting-services/report-server-sharepoint/reporting-services-site-settings-and-site-features-sharepoint-mode.md)   
 [Activar la característica de sincronización de archivos del servidor de informes en Administración central de SharePoint](../../reporting-services/report-server-sharepoint/activate-the-report-server-file-sync-feature-in-sharepoint-ca.md)  
  
  