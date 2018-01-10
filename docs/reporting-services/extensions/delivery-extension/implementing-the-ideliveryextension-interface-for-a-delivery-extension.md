---
title: "Implementar la interfaz IDeliveryExtension para una extensión de entrega | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.service: 
ms.component: extensions
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- delivery extensions [Reporting Services], attributes
- delivery extensions [Reporting Services], class creation
- IDeliveryExtension interface
ms.assetid: ab0344db-510b-403f-8dbf-b9831553765d
caps.latest.revision: "37"
author: markingmyname
ms.author: maghan
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: d8f260fd9191fc84a41d4626514fda1deb9f141a
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/09/2018
---
# <a name="implementing-the-ideliveryextension-interface-for-a-delivery-extension"></a>Implementar la interfaz IDeliveryExtension para una extensión de entrega
  La clase de extensión de entrega se utiliza para entregar las notificaciones de informes a los usuarios según el contenido de las notificaciones. La clase de extensión de entrega también proporciona la infraestructura para validar la configuración del usuario que se pasa a la extensión de entrega. Además, la clase de extensión de entrega debería contener las propiedades específicas que los clientes puedan utilizar para obtener información sobre el nombre de la extensión, la configuración que la extensión admite y los formatos de representación que están disponibles para la extensión de entrega.  
  
 ![Proceso de la interfaz IDeliveryExtension](../../../reporting-services/extensions/delivery-extension/media/bk-ext-02.gif "Proceso de la interfaz IDeliveryExtension")  
La interfaz IDeliveryExtension permite la validación de los datos del usuario así como que los clientes obtengan información sobre la configuración de entrega necesaria  
  
 Para crear una clase de extensión de entrega, implemente <xref:Microsoft.ReportingServices.Interfaces.IDeliveryExtension> y <xref:Microsoft.ReportingServices.Interfaces.IExtension>. La interfaz **IDeliveryExtension** permite a la extensión de entrega entregar notificaciones de informe mediante el método <xref:Microsoft.ReportingServices.Interfaces.IDeliveryExtension.Deliver%2A> y validar la configuración de la extensión entrante mediante el método <xref:Microsoft.ReportingServices.Interfaces.IDeliveryExtension.ValidateUserData%2A>. La interfaz **IExtension** permite que la extensión de entrega implemente un nombre traducido y procese la información de configuración específica de la extensión almacenada en el archivo de configuración de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Al implementar **IExtension**, la extensión de entrega contiene la propiedad <xref:Microsoft.ReportingServices.Interfaces.Extension.LocalizedName%2A>. Se recomienda encarecidamente que las extensiones de entrega de [!INCLUDE[ssRS](../../../includes/ssrs-md.md)] admitan la propiedad **LocalizedName**, de forma que los usuarios encuentren un nombre conocido para la extensión en una interfaz de usuario, como el Administrador de informes.  
  
 La extensión de entrega también debe implementar la propiedad **ExtensionSettings** de la interfaz **IDeliveryExtension**. El servidor de informes utiliza el valor devuelto por la propiedad <xref:Microsoft.ReportingServices.Interfaces.IDeliveryExtension.ExtensionSettings%2A> para evaluar los valores que una extensión de entrega requiere. Los clientes que interactúan con extensiones de entrega utilizan el método <xref:ReportService2010.ReportingService2010.GetExtensionSettings%2A> del servicio web del servidor de informes para devolver una lista de valores para la extensión de entrega.  
  
 También puede utilizar su clase de extensión de entrega para recuperar y procesar los datos de configuración personalizados almacenados en el archivo RSReportServer.config. Para obtener más información acerca de cómo procesar los datos de configuración personalizados, vea el método <xref:Microsoft.ReportingServices.Interfaces.IExtension.SetConfiguration%2A>.  
  
 Para obtener una muestra de implementación de la clase **IDeliveryExtension**, vea [Muestras de productos de SQL Server Reporting Services](http://go.microsoft.com/fwlink/?LinkId=177889).  
  
## <a name="see-also"></a>Ver también  
 [Implementar una extensión de entrega](../../../reporting-services/extensions/delivery-extension/implementing-a-delivery-extension.md)   
 [Biblioteca de extensiones de Reporting Services](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  
