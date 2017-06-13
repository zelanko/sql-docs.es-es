---
title: Instalar Reporting Services el modo de SharePoint | Documentos de Microsoft
ms.custom:
- SQL2016_New_Updated
ms.date: 06/01/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
ms.tgt_pltfrm: 
ms.topic: get-started-article
helpviewer_keywords:
- default configuration [Reporting Services]
- installing Reporting Services, SharePoint integrated mode
- installation options [Reporting Services]
ms.assetid: ac6cba68-2665-4a39-8fa3-cb7d7e6723c0
caps.latest.revision: 35
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: b2c77f21304b04b5349691b6c464026fe944a4eb
ms.contentlocale: es-es
ms.lasthandoff: 06/13/2017

---
# <a name="install-reporting-services-sharepoint-mode"></a>Instalar el modo de SharePoint de Reporting Services
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] en SharePoint permite crear y visualizar informes en las bibliotecas de documentos, entregar de informes de suscripciones de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] a través de correo electrónico,  [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)], alertas de datos y características de administración de informes, todo en una implementación basada en [!INCLUDE[msCoName](../../includes/msconame-md.md)] SharePoint. Para obtener más información sobre las características del modo de SharePoint, vea la sección "Diferencias de compatibilidad de características y comportamiento por modo de servidor" en [Servidor de informes de Reporting Services](../../reporting-services/report-server-sharepoint/reporting-services-report-server.md).  
  
 Hay dos componentes principales de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] que se instalarán para [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] en modo de SharePoint:  
  
|Installation|Descripción|  
|------------------|-----------------|  
|**Servidor de informes:** el servidor de informes de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] instalado en modo de SharePoint|El servidor de informes administra el procesamiento y la representación de datos e informes así como la suscripción y el procesamiento de alertas de datos. El servidor de informes en modo de SharePoint se diseña e instala como un servicio compartido de SharePoint.<br /><br /> **Cómo:** utilice el disco de instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para instalar el servidor de informes.|  
|**Add-in:** The [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] add-in for SharePoint products, **rssharepoint.msi**.|El complemento instala las características y las páginas de la interfaz de usuario (IU) de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] en un servidor front-end web de SharePoint. Entre las características de la interfaz de usuario se encuentran [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)], páginas de administración en Administración central de SharePoint, páginas de características utilizadas en las bibliotecas de documentos de SharePoint y páginas de alertas de datos de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .<br /><br /> **Cómo:**  el complemento se puede instalar desde una descarga web o desde un disco de instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para obtener más información, vea [Dónde encontrar el complemento Reporting Services para Productos de SharePoint](../../reporting-services/install-windows/where-to-find-the-reporting-services-add-in-for-sharepoint-products.md).|  
  
## <a name="in-this-section"></a>En esta sección  
 [Combinaciones admitidas del servidor y el complemento de SharePoint y Reporting Services &#40;SQL Server 2016&#41;](../../reporting-services/install-windows/supported-combinations-of-sharepoint-and-reporting-services-server.md)  
  
 [Dónde encontrar el complemento Reporting Services para Productos de SharePoint](../../reporting-services/install-windows/where-to-find-the-reporting-services-add-in-for-sharepoint-products.md)  
  
 [Instalación del primer servidor de informes en modo de SharePoint](../../reporting-services/install-windows/install-the-first-report-server-in-sharepoint-mode.md)  
  
 [Instalar o desinstalar el complemento Reporting Services para SharePoint](../../reporting-services/install-windows/install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md)  
  
 [Agregar un servidor de informes adicional a una granja de servidores &#40;escalado horizontal de SSRS&#41;](../../reporting-services/install-windows/add-an-additional-report-server-to-a-farm-ssrs-scale-out.md)  
  
 [Agregar un front-end web adicional de Reporting Services a una granja de servidores](../../reporting-services/install-windows/add-an-additional-reporting-services-web-front-end-to-a-farm.md)  
  
 [Configurar el correo electrónico para una aplicación de servicio de Reporting Services &#40;SharePoint 2013 y SharePoint 2016&#41;](http://msdn.microsoft.com/en-us/38fc34a6-aae7-4dde-9ad2-f1eee0c42a9f)  
  
 [Aprovisionar Subscripciones y alertas para aplicaciones de servicio SSRS](../../reporting-services/install-windows/provision-subscriptions-and-alerts-for-ssrs-service-applications.md)  
  
 [Notificaciones del servicio de token de Windows &#40;c2WTS&#41; y Reporting Services](../../reporting-services/install-windows/claims-to-windows-token-service-c2wts-and-reporting-services.md)  
  
## <a name="see-also"></a>Vea también  
 [Arquitectura y flujo de trabajo de alertas de datos](../../reporting-services/reporting-services-data-alerts.md#AlertingWF)   
 [Administrador de alertas de datos para administradores de alertas](../../reporting-services/data-alert-manager-for-alerting-administrators.md)  
  
  

