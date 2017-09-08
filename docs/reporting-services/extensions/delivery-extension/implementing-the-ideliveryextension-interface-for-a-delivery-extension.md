---
title: "Implementar la interfaz IDeliveryExtension para una extensión de entrega | Documentos de Microsoft"
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
- delivery extensions [Reporting Services], attributes
- delivery extensions [Reporting Services], class creation
- IDeliveryExtension interface
ms.assetid: ab0344db-510b-403f-8dbf-b9831553765d
caps.latest.revision: 37
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: a6aab5e722e732096e9e4ffdf458ac25088e09ae
ms.openlocfilehash: ac54345b14ba3ff84a755e0ce4e8b1c4e9acab13
ms.contentlocale: es-es
ms.lasthandoff: 08/12/2017

---
# <a name="implementing-the-ideliveryextension-interface-for-a-delivery-extension"></a>Implementar la interfaz IDeliveryExtension para una extensión de entrega
  La clase de extensión de entrega se utiliza para entregar las notificaciones de informes a los usuarios según el contenido de las notificaciones. La clase de extensión de entrega también proporciona la infraestructura para validar la configuración del usuario que se pasa a la extensión de entrega. Además, la clase de extensión de entrega debería contener las propiedades específicas que los clientes puedan utilizar para obtener información sobre el nombre de la extensión, la configuración que la extensión admite y los formatos de representación que están disponibles para la extensión de entrega.  
  
 ![Proceso de la interfaz IDeliveryExtension](../../../reporting-services/extensions/delivery-extension/media/bk-ext-02.gif "proceso de la interfaz IDeliveryExtension")  
La interfaz IDeliveryExtension permite la validación de los datos del usuario así como que los clientes obtengan información sobre la configuración de entrega necesaria  
  
 Para crear una clase de extensión de entrega, implemente <xref:Microsoft.ReportingServices.Interfaces.IDeliveryExtension> y <xref:Microsoft.ReportingServices.Interfaces.IExtension>. El **IDeliveryExtension** interfaz permite que la extensión de entrega entregar notificaciones de informe mediante el <xref:Microsoft.ReportingServices.Interfaces.IDeliveryExtension.Deliver%2A> método y validar la configuración de extensión entrante mediante el <xref:Microsoft.ReportingServices.Interfaces.IDeliveryExtension.ValidateUserData%2A> método. El **IExtension** interfaz permite que la extensión de entrega para implementar un nombre de extensión localizado y procesar la información de configuración específica de la extensión almacenada en el [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] archivo de configuración. Implementando **IExtension**, contiene la extensión de entrega el <xref:Microsoft.ReportingServices.Interfaces.Extension.LocalizedName%2A> propiedad. Se recomienda que [!INCLUDE[ssRS](../../../includes/ssrs-md.md)] compatibilidad con las extensiones de entrega el **LocalizedName** propiedad, por lo que los usuarios encuentren un nombre conocido para la extensión en una interfaz de usuario, por ejemplo, el Administrador de informes.  
  
 La extensión de entrega también debe implementar la **ExtensionSettings** propiedad de la **IDeliveryExtension** interfaz. El servidor de informes utiliza el valor devuelto por la propiedad <xref:Microsoft.ReportingServices.Interfaces.IDeliveryExtension.ExtensionSettings%2A> para evaluar los valores que una extensión de entrega requiere. Los clientes que interactúan con extensiones de entrega utilizan el método <xref:ReportService2010.ReportingService2010.GetExtensionSettings%2A> del servicio web del servidor de informes para devolver una lista de valores para la extensión de entrega.  
  
 También puede utilizar su clase de extensión de entrega para recuperar y procesar los datos de configuración personalizados almacenados en el archivo RSReportServer.config. Para obtener más información acerca de cómo procesar los datos de configuración personalizados, vea el método <xref:Microsoft.ReportingServices.Interfaces.IExtension.SetConfiguration%2A>.  
  
 Para obtener un ejemplo **IDeliveryExtension** implementación de la clase, vea [muestras de producto de SQL Server Reporting Services](http://go.microsoft.com/fwlink/?LinkId=177889).  
  
## <a name="see-also"></a>Vea también  
 [Implementar una extensión de entrega](../../../reporting-services/extensions/delivery-extension/implementing-a-delivery-extension.md)   
 [Biblioteca de extensión de Reporting Services](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  
