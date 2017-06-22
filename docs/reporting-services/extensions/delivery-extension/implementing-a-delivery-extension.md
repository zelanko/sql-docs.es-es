---
title: "Implementar una extensión de entrega | Documentos de Microsoft"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- delivery [Reporting Services]
- custom delivery extensions [Reporting Services]
- extensions [Reporting Services], delivery
- delivery extensions [Reporting Services]
ms.assetid: 600cd229-efcd-480e-8c95-3c3c39ff4e7a
caps.latest.revision: 32
author: sabotta
ms.author: carlasab
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 9909a4711eb5b1ffde9b865411bd552e6b409bc6
ms.contentlocale: es-es
ms.lasthandoff: 06/22/2017

---
# <a name="implementing-a-delivery-extension"></a>Implementar una extensión de entrega
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)][!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] permite a los usuarios crear y publicar informes que, una vez creado y publicado, se pueden entregar en varias ubicaciones. Además, [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] incluye varias extensiones de entrega y una API de entrega que permite a los programadores crear extensiones de entrega adicionales para extender aún más la funcionalidad de entrega en [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)].  
  
 Para una implementación de ejemplo de una extensión de entrega, consulte [muestras de producto de SQL Server Reporting Services](http://go.microsoft.com/fwlink/?LinkId=177889).  
  
## <a name="in-this-section"></a>En esta sección  
 [Información general de las extensiones de entrega](../../../reporting-services/extensions/delivery-extension/delivery-extensions-overview.md)  
 Introduce cómo escribir una extensión de entrega personalizada para [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)].  
  
 [Preparación para implementar una extensión de entrega](../../../reporting-services/extensions/delivery-extension/preparing-to-implement-a-delivery-extension.md)  
 Describe las interfaces y clases disponibles al implementar una extensión de entrega de [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)], así como cuestiones que hay que considerar antes de la implementación.  
  
 [Crear una biblioteca de extensión de entrega](../../../reporting-services/extensions/delivery-extension/creating-a-delivery-extension-library.md)  
 Describe cómo asignar un espacio de nombres para su extensión de entrega de [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] y cómo compilarla en una biblioteca DLL.  
  
 [Implementar la interfaz IDeliveryExtension para una extensión de entrega](../../../reporting-services/extensions/delivery-extension/implementing-the-ideliveryextension-interface-for-a-delivery-extension.md)  
 Describe los atributos de una extensión de entrega y cómo implementar su propia clase de extensión de entrega.  
  
 [Utilizar una clase de notificación para una extensión de entrega](../../../reporting-services/extensions/delivery-extension/using-a-notification-class-for-a-delivery-extension.md)  
 Describe los atributos de un **notificación** clase y cómo utilizarlo en la implementación de extensión de entrega.  
  
 [Usar la clase Setting para una extensión de entrega](../../../reporting-services/extensions/delivery-extension/using-the-setting-class-for-a-delivery-extension.md)  
 Describe los atributos de un **configuración** clase y cómo utilizarlo en la implementación de extensión de entrega.  
  
 [Utilizar la interfaz IDeliveryReportServerInformation para una extensión de entrega](../../../reporting-services/extensions/delivery-extension/using-the-ideliveryreportserverinformation-interface-for-a-delivery-extension.md)  
 Describe los atributos de un **IDeliveryReportServerInformation** interfaz y cómo utilizarlo en la implementación de extensión de entrega.  
  
 [Usar la clase de informe para una extensión de entrega](../../../reporting-services/extensions/delivery-extension/using-the-report-class-for-a-delivery-extension.md)  
 Describe los atributos de un **informe** clase y cómo utilizarlo en la implementación de extensión de entrega.  
  
 [Usar la clase RenderedOutputFile para una extensión de entrega](../../../reporting-services/extensions/delivery-extension/using-the-renderedoutputfile-class-for-a-delivery-extension.md)  
 Describe los atributos de un **RenderedOutputFile** clase y cómo utilizarlo en la implementación de extensión de entrega.  
  
 [Implementar la interfaz ISubscriptionBaseUIUserControl para una extensión de entrega](../../../reporting-services/extensions/delivery-extension/implementing-the-isubscriptionbaseuiusercontrol-interface.md)  
 Describe los atributos de un control de usuario de extensión de entrega y cómo implementar su propia interfaz de usuario para una suscripción.  
  
 [Implementar una extensión de entrega](../../../reporting-services/extensions/delivery-extension/deploying-a-delivery-extension.md)  
 Describe cómo implementar una extensión de entrega.  
  
 [Depurar código de extensión de entrega](../../../reporting-services/extensions/delivery-extension/debugging-delivery-extension-code.md)  
 Describe cómo depurar el código en una extensión de entrega.  
  
 [Quitar una extensión de entrega](../../../reporting-services/extensions/delivery-extension/removing-a-delivery-extension.md)  
 Describe cómo quitar una extensión de entrega de un servidor de informes.  
  
## <a name="see-also"></a>Vea también  
 [Extensiones de Reporting Services](../../../reporting-services/extensions/reporting-services-extensions.md)   
 [Biblioteca de extensión de Reporting Services](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  
