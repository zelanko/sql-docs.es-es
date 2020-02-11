---
title: Instalación en modo de Reporting Services SharePoint (SharePoint 2010 y SharePoint 2013) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- default configuration [Reporting Services]
- installing Reporting Services, SharePoint integrated mode
- installation options [Reporting Services]
ms.assetid: ac6cba68-2665-4a39-8fa3-cb7d7e6723c0
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: ef049b4ded6408e651d5ec2c3db99c10bf7c27b6
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "66108764"
---
# <a name="reporting-services-sharepoint-mode-installation-sharepoint-2010-and-sharepoint-2013"></a>Instalación del modo de SharePoint de Reporting Services (SharePoint 2010 y SharePoint 2013)
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]en modo de SharePoint es una colección de componentes de servidor que proporcionan generación y entrega de informes [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] basada [!INCLUDE[msCoName](../../includes/msconame-md.md)] en y productos de SharePoint.  
  
 La ejecución de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] en modo de SharePoint proporciona las características de [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] y de alertas de datos. Para obtener más información sobre las características del modo de SharePoint, vea la sección "diferencias de compatibilidad de características y comportamiento por modo de servidor" en [Reporting Services servidor de informes](../reporting-services-report-server.md) .  
  
 Hay dos instalaciones fundamentales necesarias para [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] en modo de SharePoint:  
  
|Instalación|Descripción|  
|------------------|-----------------|  
|[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] El [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] complemento para productos de SharePoint.|El complemento instala las características y las páginas de la interfaz de usuario (IU) de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] en un servidor front-end web de SharePoint. Entre las características de la interfaz de usuario se encuentran [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)], páginas de administración en Administración central de SharePoint, páginas de características utilizadas en las bibliotecas de documentos de SharePoint y páginas de alertas de datos de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .|  
|[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] El [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] servidor de informes instalado en modo de SharePoint|El servidor de informes administra el procesamiento y la representación de datos e informes así como la suscripción y el procesamiento de alertas de datos. El servidor de informes en modo de SharePoint se configura e instala como un servicio compartido de SharePoint.|  
  
 Para instalar [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], utilice el disco de instalación de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Para obtener instrucciones sobre escenarios de implementación avanzada, consulte lista de comprobación de la [implementación: Reporting Services, Power View y PowerPivot para SharePoint](../../sql-server/install/deployment-checklist-reporting-services-power-view-power-pivot-for-sharepoint.md) y lista de comprobación de la [implementación: instalar Reporting Services en una granja de servidores de SharePoint existente](../../sql-server/install/deployment-checklist-install-reporting-services-existing-sharepoint-farm.md).  
  
## <a name="in-this-section"></a>En esta sección  
 [Combinaciones admitidas de SharePoint y Reporting Services Server y el complemento &#40;SQL Server 2014&#41;](supported-combinations-of-sharepoint-and-reporting-services-server.md)  
  
 [Instalar el modo de SharePoint de Reporting Services para SharePoint 2013](../../sql-server/install/install-reporting-services-sharepoint-mode-for-sharepoint-2013.md)  
  
 [Instalar el modo de SharePoint de Reporting Services para SharePoint 2010](../../sql-server/install/install-reporting-services-sharepoint-mode-for-sharepoint-2010.md)  
  
 [Instalar o desinstalar el complemento de Reporting Services para SharePoint &#40;SharePoint 2010 y SharePoint 2013&#41;](install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md)  
  
 [Dónde encontrar el complemento de Reporting Services para productos de SharePoint](where-to-find-the-reporting-services-add-in-for-sharepoint-products.md)  
  
 [Agregar un servidor de informes adicional a una granja de servidores &#40;la escalabilidad horizontal de SSRS&#41;](add-an-additional-report-server-to-a-farm-ssrs-scale-out.md)  
  
 [Agregar un front-end web adicional de Reporting Services a una granja de servidores](add-an-additional-reporting-services-web-front-end-to-a-farm.md)  
  
 [Configurar el correo electrónico para una aplicación de servicio de Reporting Services &#40;SharePoint 2010 y SharePoint 2013&#41;](configure-e-mail-for-a-reporting-services-service-application.md)  
  
 [Aprovisionar Subscripciones y alertas para aplicaciones de servicio SSRS](provision-subscriptions-and-alerts-for-ssrs-service-applications.md)  
  
 [Notificaciones del servicio de token de Windows &#40;C2WTS&#41; y Reporting Services](../../sql-server/install/claims-to-windows-token-service-c2wts-and-reporting-services.md)  
  
## <a name="see-also"></a>Consulte también  
 [Arquitectura y flujo de trabajo de alertas de datos](../reporting-services-data-alerts.md#AlertingWF)   
 [Administrador de alertas de datos para administradores de alertas](../data-alert-manager-for-alerting-administrators.md)  
  
  
