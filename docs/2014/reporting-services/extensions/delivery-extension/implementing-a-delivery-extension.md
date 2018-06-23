---
title: Implementar una extensión de entrega | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- delivery [Reporting Services]
- custom delivery extensions [Reporting Services]
- extensions [Reporting Services], delivery
- delivery extensions [Reporting Services]
ms.assetid: 600cd229-efcd-480e-8c95-3c3c39ff4e7a
caps.latest.revision: 31
author: douglaslM
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: aa4c6da130cf1e616a3d1cb43aa8c0aea863384d
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36204767"
---
# <a name="implementing-a-delivery-extension"></a>Implementar una extensión de entrega
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] permite a los usuarios crear y publicar informes que, una vez creados y publicados, se pueden entregar en varias ubicaciones. Además, [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] incluye varias extensiones de entrega y una API de entrega que permite a los programadores crear extensiones de entrega adicionales para extender aún más la funcionalidad de entrega en [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)].  
  
 Para obtener una implementación de ejemplo de una extensión de entrega, vea [Ejemplos del producto SQL Server Reporting Services](http://go.microsoft.com/fwlink/?LinkId=177889).  
  
## <a name="in-this-section"></a>En esta sección  
 [Introducción a las extensiones entrega] entrega-extensiones-overview.md)  
 Introduce cómo escribir una extensión de entrega personalizada para [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)].  
  
 [Preparación de la ejecución de una extensión de entrega](preparing-to-implement-a-delivery-extension.md)  
 Describe las interfaces y clases disponibles al implementar una extensión de entrega de [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)], así como cuestiones que hay que considerar antes de la implementación.  
  
 [Creación de una biblioteca de extensiones de entrega](creating-a-delivery-extension-library.md)  
 Describe cómo asignar un espacio de nombres para su extensión de entrega de [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] y cómo compilarla en una biblioteca DLL.  
  
 [Ejecución de la interfaz IDeliveryExtension para una extensión de entrega](implementing-the-ideliveryextension-interface-for-a-delivery-extension.md)  
 Describe los atributos de una extensión de entrega y cómo implementar su propia clase de extensión de entrega.  
  
 [Uso de una clase Notification para una extensión de entrega](using-a-notification-class-for-a-delivery-extension.md)  
 Describe los atributos de una clase **Notification** y cómo usarla en la implementación de la extensión de entrega.  
  
 [Uso de la clase Setting para una extensión de entrega](using-the-setting-class-for-a-delivery-extension.md)  
 Describe los atributos de una clase **Setting** y cómo usarla en la implementación de la extensión de entrega.  
  
 [Uso de la interfaz IDeliveryReportServerInformation para una extensión de entrega](using-the-ideliveryreportserverinformation-interface-for-a-delivery-extension.md)  
 Describe los atributos de una interfaz **IDeliveryReportServerInformation** y cómo usarla en la implementación de la extensión de entrega.  
  
 [Uso de la clase Report para una extensión de entrega](using-the-report-class-for-a-delivery-extension.md)  
 Describe los atributos de una clase **Report** y cómo usarla en la implementación de la extensión de entrega.  
  
 [Uso de la clase RenderedOutputFile para una extensión de entrega](using-the-renderedoutputfile-class-for-a-delivery-extension.md)  
 Describe los atributos de una clase **RenderedOutputFile** y cómo usarla en la implementación de la extensión de entrega.  
  
 [Implementar la interfaz ISubscriptionBaseUIUserControl para una extensión de entrega](implementing-the-isubscriptionbaseuiusercontrol-interface.md)  
 Describe los atributos de un control de usuario de extensión de entrega y cómo implementar su propia interfaz de usuario para una suscripción.  
  
 [Implementación de una extensión de entrega](deploying-a-delivery-extension.md)  
 Describe cómo implementar una extensión de entrega.  
  
 [Depuración del código de extensiones de entrega](debugging-delivery-extension-code.md)  
 Describe cómo depurar el código en una extensión de entrega.  
  
 [Eliminación de una extensión de entrega](removing-a-delivery-extension.md)  
 Describe cómo quitar una extensión de entrega de un servidor de informes.  
  
## <a name="see-also"></a>Vea también  
 [Extensiones de Reporting Services](../reporting-services-extensions.md)   
 [Biblioteca de extensiones de Reporting Services](../reporting-services-extension-library.md)  
  
  