---
title: Instalación en modo de SharePoint (SharePoint 2010 y SharePoint 2013) de Reporting Services | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- default configuration [Reporting Services]
- installing Reporting Services, SharePoint integrated mode
- installation options [Reporting Services]
ms.assetid: ac6cba68-2665-4a39-8fa3-cb7d7e6723c0
caps.latest.revision: 30
author: markingmyname
ms.author: maghan
manager: jhubbard
ms.openlocfilehash: f0e75a75ffb14f720f2b421d659fa6142b579019
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36103048"
---
# <a name="reporting-services-sharepoint-mode-installation-sharepoint-2010-and-sharepoint-2013"></a>Instalación del modo de SharePoint de Reporting Services (SharePoint 2010 y SharePoint 2013)
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] en SharePoint, el modo es una colección de componentes de servidor que proporcionan la generación de informes y la entrega, tomando como base [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y [!INCLUDE[msCoName](../../includes/msconame-md.md)] productos de SharePoint.  
  
 La ejecución de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] en modo de SharePoint proporciona las características de [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] y de alertas de datos. Para obtener más información sobre las características del modo de SharePoint, vea la sección "Diferencias de compatibilidad de características y comportamiento por modo de servidor" en [Servidor de informes de Reporting Services](../reporting-services-report-server.md).  
  
 Hay dos instalaciones fundamentales necesarias para [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] en modo de SharePoint:  
  
|Installation|Descripción|  
|------------------|-----------------|  
|El [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] complemento para productos de SharePoint.|El complemento instala las características y las páginas de la interfaz de usuario (IU) de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] en un servidor front-end web de SharePoint. Entre las características de la interfaz de usuario se encuentran [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)], páginas de administración en Administración central de SharePoint, páginas de características utilizadas en las bibliotecas de documentos de SharePoint y páginas de alertas de datos de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .|  
|El [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] servidor de informes instalado en modo de SharePoint|El servidor de informes administra el procesamiento y la representación de datos e informes así como la suscripción y el procesamiento de alertas de datos. El servidor de informes en modo de SharePoint se configura e instala como un servicio compartido de SharePoint.|  
  
 Para instalar [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], utilice el disco de instalación de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Para obtener instrucciones sobre escenarios de implementación avanzada, consulte [lista de comprobación de implementación: Reporting Services, Power View y PowerPivot para SharePoint](../../sql-server/install/deployment-checklist-reporting-services-power-view-power-pivot-for-sharepoint.md) y [lista de comprobación de implementación: instalar Reporting Services en una existente Granja de SharePoint](../../sql-server/install/deployment-checklist-install-reporting-services-existing-sharepoint-farm.md).  
  
## <a name="in-this-section"></a>En esta sección  
 [Combinaciones admitidas de SharePoint y Reporting Services Server y el complemento &#40;SQL Server 2014&#41;](supported-combinations-of-sharepoint-and-reporting-services-server.md)  
  
 [Instalar el modo de SharePoint de Reporting Services para SharePoint 2013](../../sql-server/install/install-reporting-services-sharepoint-mode-for-sharepoint-2013.md)  
  
 [Instalar el modo de SharePoint de Reporting Services para SharePoint 2010](../../sql-server/install/install-reporting-services-sharepoint-mode-for-sharepoint-2010.md)  
  
 [Instalar o desinstalar el complemento Servicios de informes para SharePoint &#40;SharePoint 2010 y SharePoint 2013&#41;](install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md)  
  
 [Dónde encontrar el complemento de Reporting Services para productos de SharePoint](where-to-find-the-reporting-services-add-in-for-sharepoint-products.md)  
  
 [Agregar un servidor de informes adicional a una granja de servidores &#40;escalado horizontal de SSRS&#41;](add-an-additional-report-server-to-a-farm-ssrs-scale-out.md)  
  
 [Incorporación de un front-end web adicional de Reporting Services a una granja de servidores](add-an-additional-reporting-services-web-front-end-to-a-farm.md)  
  
 [Configurar el correo electrónico para la aplicación de servicio de Reporting Services &#40;SharePoint 2010 y SharePoint 2013&#41;](configure-e-mail-for-a-reporting-services-service-application.md)  
  
 [Aprovisionamiento de subscripciones y alertas para aplicaciones de servicio de SSRS](provision-subscriptions-and-alerts-for-ssrs-service-applications.md)  
  
 [Servicio de Token de notificaciones a Windows &#40;C2WTS&#41; y Reporting Services](../../sql-server/install/claims-to-windows-token-service-c2wts-and-reporting-services.md)  
  
## <a name="see-also"></a>Vea también  
 [Arquitectura y flujo de trabajo alertas de datos](../reporting-services-data-alerts.md#AlertingWF)   
 [Administrador de alertas de datos para administradores de alertas](../data-alert-manager-for-alerting-administrators.md)  
  
  