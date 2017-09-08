---
title: Implementar la interfaz ISubscriptionBaseUIUserControl | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
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
- user controls [Reporting Services]
- ISubscriptionBaseUIUserControl interface
- delivery extensions [Reporting Services], user controls
ms.assetid: a1e9122c-aa0b-45de-b536-4f1202875ab1
caps.latest.revision: 35
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: a6aab5e722e732096e9e4ffdf458ac25088e09ae
ms.openlocfilehash: 4e76edaa727df1694a5903e1cc9870c20581c9a0
ms.contentlocale: es-es
ms.lasthandoff: 08/12/2017

---
# <a name="implementing-the-isubscriptionbaseuiusercontrol-interface"></a>Implementar la interfaz ISubscriptionBaseUIUserControl
  Las extensiones de entrega de [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] pueden contener la implementación de una interfaz de usuario (UI) de suscripción para recopilar información específica de la extensión en el Administrador de informes. La UI se invoca cuando un usuario crea una nueva suscripción o modifica una existente. Cuando se crea una suscripción nueva, la UI muestra los valores predeterminados adecuados y permite a los usuarios interactuar con el proveedor de entrega. Cuando se modifica una suscripción, la UI se rellena de antemano con la información en la suscripción actual.  
  
 Las extensiones de entrega proporcionan la UI de suscripción como un control de usuario de ASP.NET. El servidor de informes incorpora el control de usuario definido por la extensión de entrega al mostrar la UI de suscripciones. La interfaz base que proporciona métodos abstractos que habilitan esta funcionalidad es <xref:Microsoft.ReportingServices.Interfaces.ISubscriptionBaseUIUserControl>. Esta interfaz se asegura de que se realizan correctamente las operaciones comunes, como la validación de los valores de entrada. Además, el control de usuario base proporciona un conjunto de propiedades predeterminadas que usa el servidor de informes para mantener la coherencia a través de las suscripciones. Las extensiones de entrega que se integran con el Administrador de informes requieren estas propiedades.  
  
 Puede implementar la interfaz <xref:Microsoft.ReportingServices.Interfaces.ISubscriptionBaseUIUserControl> en un proveedor de entrega con el fin de poder construir una UI de suscripción para el Administrador de informes. La interfaz <xref:Microsoft.ReportingServices.Interfaces.ISubscriptionBaseUIUserControl> proporciona la infraestructura para permitir que los usuarios especifiquen los valores para la configuración de suscripción, procesen los valores necesarios para la extensión de entrega y validen los valores.  
  
> [!NOTE]  
>  No es necesario que implemente la interfaz <xref:Microsoft.ReportingServices.Interfaces.ISubscriptionBaseUIUserControl> como parte de la extensión de entrega. Las suscripciones que utilizan la extensión de entrega siempre se pueden crear en cambio a través de los métodos <xref:ReportService2010.ReportingService2010.CreateSubscription%2A> y <xref:ReportService2010.ReportingService2010.CreateDataDrivenSubscription%2A> de la API SOAP. Para obtener más información acerca de las características de API de SOAP para administrar la suscripción y entrega, consulte [métodos de suscripción y entrega](../../../reporting-services/report-server-web-service/methods/subscription-and-delivery-methods.md).  
  
 La interfaz <xref:Microsoft.ReportingServices.Interfaces.ISubscriptionBaseUIUserControl> extiende a <xref:Microsoft.ReportingServices.Interfaces.IExtension>. El control de usuario que implementa <xref:Microsoft.ReportingServices.Interfaces.ISubscriptionBaseUIUserControl> también debe heredar de **System.Web.UI.WebControls.WebControl**. Para obtener más información sobre la **WebControl** de clases, consulte la [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] Guía del desarrollador.  
  
 Para obtener un ejemplo de cómo usar el <xref:Microsoft.ReportingServices.Interfaces.ISubscriptionBaseUIUserControl> de la interfaz, vea [muestras de producto de SQL Server Reporting Services](http://go.microsoft.com/fwlink/?LinkId=177889).  
  
## <a name="see-also"></a>Vea también  
 [Implementar una extensión de entrega](../../../reporting-services/extensions/delivery-extension/implementing-a-delivery-extension.md)   
 [Biblioteca de extensión de Reporting Services](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  
