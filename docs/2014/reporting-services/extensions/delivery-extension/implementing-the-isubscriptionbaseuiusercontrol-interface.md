---
title: Implementar la interfaz ISubscriptionBaseUIUserControl para una extensión de entrega | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.topic: reference
helpviewer_keywords:
- user controls [Reporting Services]
- ISubscriptionBaseUIUserControl interface
- delivery extensions [Reporting Services], user controls
ms.assetid: a1e9122c-aa0b-45de-b536-4f1202875ab1
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: f87046df4e41f40bc5de5f2a720247738841ff24
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/13/2018
ms.locfileid: "53376347"
---
# <a name="implementing-the-isubscriptionbaseuiusercontrol-interface-for-a-delivery-extension"></a>Implementar la interfaz ISubscriptionBaseUIUserControl para una extensión de entrega
  Las extensiones de entrega de [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] pueden contener la implementación de una interfaz de usuario (UI) de suscripción para recopilar información específica de la extensión en el Administrador de informes. La UI se invoca cuando un usuario crea una nueva suscripción o modifica una existente. Cuando se crea una suscripción nueva, la UI muestra los valores predeterminados adecuados y permite a los usuarios interactuar con el proveedor de entrega. Cuando se modifica una suscripción, la UI se rellena de antemano con la información en la suscripción actual.  
  
 Las extensiones de entrega proporcionan la UI de suscripción como un control de usuario de ASP.NET. El servidor de informes incorpora el control de usuario definido por la extensión de entrega al mostrar la UI de suscripciones. La interfaz base que proporciona métodos abstractos que habilitan esta funcionalidad es <xref:Microsoft.ReportingServices.Interfaces.ISubscriptionBaseUIUserControl>. Esta interfaz se asegura de que se realizan correctamente las operaciones comunes, como la validación de los valores de entrada. Además, el control de usuario base proporciona un conjunto de propiedades predeterminadas que usa el servidor de informes para mantener la coherencia a través de las suscripciones. Las extensiones de entrega que se integran con el Administrador de informes requieren estas propiedades.  
  
 Puede implementar la interfaz <xref:Microsoft.ReportingServices.Interfaces.ISubscriptionBaseUIUserControl> en un proveedor de entrega con el fin de poder construir una UI de suscripción para el Administrador de informes. La interfaz <xref:Microsoft.ReportingServices.Interfaces.ISubscriptionBaseUIUserControl> proporciona la infraestructura para permitir que los usuarios especifiquen los valores para la configuración de suscripción, procesen los valores necesarios para la extensión de entrega y validen los valores.  
  
> [!NOTE]  
>  No es necesario que implemente la interfaz <xref:Microsoft.ReportingServices.Interfaces.ISubscriptionBaseUIUserControl> como parte de la extensión de entrega. Las suscripciones que utilizan la extensión de entrega siempre se pueden crear en cambio a través de los métodos <xref:ReportService2010.ReportingService2010.CreateSubscription%2A> y <xref:ReportService2010.ReportingService2010.CreateDataDrivenSubscription%2A> de la API SOAP. Para más información sobre las características de la API de SOAP para administrar la suscripción y la entrega, vea [Métodos de suscripción y entrega](../../report-server-web-service/methods/subscription-and-delivery-methods.md).  
  
 La interfaz <xref:Microsoft.ReportingServices.Interfaces.ISubscriptionBaseUIUserControl> extiende a <xref:Microsoft.ReportingServices.Interfaces.IExtension>. El control de usuario que implementa <xref:Microsoft.ReportingServices.Interfaces.ISubscriptionBaseUIUserControl> también debe heredar de **System.Web.UI.WebControls.WebControl**. Para más información sobre la clase **WebControl**, vea la Guía del desarrollador de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)].  
  
 Para obtener un ejemplo de cómo usar la interfaz <xref:Microsoft.ReportingServices.Interfaces.ISubscriptionBaseUIUserControl>, vea [Ejemplos del producto SQL Server Reporting Services](https://go.microsoft.com/fwlink/?LinkId=177889).  
  
## <a name="see-also"></a>Vea también  
 [Implementar una extensión de entrega](implementing-a-delivery-extension.md)   
 [Biblioteca de extensiones de Reporting Services](../reporting-services-extension-library.md)  
  
  
