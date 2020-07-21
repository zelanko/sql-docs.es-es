---
title: Instalación de Reporting Services 2016 en modo de SharePoint | Microsoft Docs
ms.date: 12/20/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint
ms.topic: conceptual
helpviewer_keywords:
- default configuration [Reporting Services]
- installing Reporting Services, SharePoint integrated mode
- installation options [Reporting Services]
ms.assetid: ac6cba68-2665-4a39-8fa3-cb7d7e6723c0
author: maggiesMSFT
ms.author: maggies
monikerRange: '>=sql-server-2016 <=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: c0ffb0df6ee5e64e79cd232e07f8ab124dfee530
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/29/2020
ms.locfileid: "62514480"
---
# <a name="install-reporting-services-2016-in-sharepoint-mode"></a>Instalación de Reporting Services 2016 en modo de SharePoint

[!INCLUDE [ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE [ssrs-appliesto-2016](../../includes/ssrs-appliesto-2016.md)] [!INCLUDE [ssrs-appliesto-not-2017](../../includes/ssrs-appliesto-not-2017.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)] [!INCLUDE [ssrs-appliesto-not-pbirs](../../includes/ssrs-appliesto-not-pbirs.md)]

[!INCLUDE [ssrs-previous-versions](../../includes/ssrs-previous-versions.md)]

SQL Server Reporting Services en SharePoint permite crear y visualizar informes en las bibliotecas de documentos, entregar de informes de suscripciones de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] a través de correo electrónico, [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)], alertas de datos y características de administración de informes, todo en una implementación basada en [!INCLUDE[msCoName](../../includes/msconame-md.md)] SharePoint. Para obtener más información sobre las características del modo de SharePoint, vea la sección "Diferencias de compatibilidad de características y comportamiento por modo de servidor" en [Servidor de informes de Reporting Services](../../reporting-services/report-server-sharepoint/reporting-services-report-server.md).

> [!NOTE]
> La integración de Reporting Services con SharePoint ya no está disponible a partir de SQL Server 2016.

Hay dos componentes principales de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] que se instalarán para [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] en modo de SharePoint:  

|Instalación|Descripción|  
|------------------|-----------------|  
|**Servidor de informes:** el servidor de informes de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] instalado en modo de SharePoint|El servidor de informes administra el procesamiento y la representación de datos e informes así como la suscripción y el procesamiento de alertas de datos. El servidor de informes en modo de SharePoint se diseña e instala como un servicio compartido de SharePoint.<br /><br /> **Cómo:** Uso del soporte de instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para instalar el servidor de informes.|  
|**Complemento:** el complemento de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para productos de SharePoint, **rssharepoint.msi**.|El complemento instala las características y las páginas de la interfaz de usuario (IU) de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] en un servidor front-end web de SharePoint. Entre las características de la interfaz de usuario se encuentran [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)], páginas de administración en Administración central de SharePoint, páginas de características utilizadas en las bibliotecas de documentos de SharePoint y páginas de alertas de datos de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .<br /><br /> **Cómo:**  El complemento se puede instalar desde una descarga web o desde un soporte de instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obtener más información, vea [Dónde encontrar el complemento Reporting Services para Productos de SharePoint](../../reporting-services/install-windows/where-to-find-the-reporting-services-add-in-for-sharepoint-products.md).|  
  
## <a name="in-this-section"></a>En esta sección

 [Combinaciones admitidas del servidor y el complemento de SharePoint y Reporting Services &#40;SQL Server 2016&#41;](../../reporting-services/install-windows/supported-combinations-of-sharepoint-and-reporting-services-server.md)  
  
 [Dónde encontrar el complemento Reporting Services para Productos de SharePoint](../../reporting-services/install-windows/where-to-find-the-reporting-services-add-in-for-sharepoint-products.md)  
  
 [Instalación del primer servidor de informes en modo de SharePoint](../../reporting-services/install-windows/install-the-first-report-server-in-sharepoint-mode.md)  
  
 [Instalar o desinstalar el complemento Reporting Services para SharePoint](../../reporting-services/install-windows/install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md)  
  
 [Agregar un servidor de informes adicional a una granja de servidores &#40;escalado horizontal de SSRS&#41;](../../reporting-services/install-windows/add-an-additional-report-server-to-a-farm-ssrs-scale-out.md)  
  
 [Incorporación de un front-end web adicional de Reporting Services a una granja de servidores](../../reporting-services/install-windows/add-an-additional-reporting-services-web-front-end-to-a-farm.md)  
  
 [Configurar el correo electrónico para una aplicación de servicio de Reporting Services &#40;SharePoint 2013 y SharePoint 2016&#41;](https://msdn.microsoft.com/38fc34a6-aae7-4dde-9ad2-f1eee0c42a9f)  
  
 [Aprovisionamiento de subscripciones y alertas para aplicaciones de servicio de SSRS](../../reporting-services/install-windows/provision-subscriptions-and-alerts-for-ssrs-service-applications.md)  
  
 [Notificaciones del servicio de token de Windows &#40;c2WTS&#41; y Reporting Services](../../reporting-services/install-windows/claims-to-windows-token-service-c2wts-and-reporting-services.md)  

## <a name="next-steps"></a>Pasos siguientes

 [Arquitectura y flujo de trabajo de alertas de datos](../../reporting-services/reporting-services-data-alerts.md#AlertingWF)   
 [Administrador de alertas de datos para administradores de alertas](../../reporting-services/data-alert-manager-for-alerting-administrators.md)  

¿Tiene alguna pregunta más? [Puede plantear sus dudas en el foro de Reporting Services](https://go.microsoft.com/fwlink/?LinkId=620231).
