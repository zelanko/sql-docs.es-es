---
title: "Usar la clase Setting para una extensión de entrega | Documentos de Microsoft"
ms.custom: 
ms.date: 03/06/2017
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
- delivery extensions [Reporting Services], settings
- Setting class
ms.assetid: 50746639-da7c-46a5-ac7b-e87dd6b91880
caps.latest.revision: 32
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: a6aab5e722e732096e9e4ffdf458ac25088e09ae
ms.openlocfilehash: e7be89798bb881fa189b2a902efb34cbfdc6b6ad
ms.contentlocale: es-es
ms.lasthandoff: 08/12/2017

---
# <a name="using-the-setting-class-for-a-delivery-extension"></a>Usar la clase Setting para una extensión de entrega
  La clase <xref:Microsoft.ReportingServices.Interfaces.Setting> se encuentra en el espacio de nombres <xref:Microsoft.ReportingServices.Interfaces> y representa información sobre la configuración de una extensión de entrega. La clase <xref:Microsoft.ReportingServices.Interfaces.Setting> proporciona la infraestructura para almacenar información sobre la configuración que se requiere para que una extensión de entrega funcione correctamente. Por ejemplo, en la distribución por correo electrónico del servidor de informes, un usuario debe proporcionar la configuración específica para la entrega por correo electrónico, por ejemplo la dirección del destinatario, la dirección del remitente, la línea de asunto del correo electrónico, entre otras. Indudablemente, los proveedores de entrega personalizados exigirán al usuario que proporcione valores concretos para que la extensión de entrega entregue las notificaciones e informes.  
  
 La clase <xref:Microsoft.ReportingServices.Interfaces.Setting> se usa al implementar la propiedad <xref:Microsoft.ReportingServices.Interfaces.IDeliveryExtension.ExtensionSettings%2A> de la interfaz <xref:Microsoft.ReportingServices.Interfaces.IDeliveryExtension>. La clase <xref:Microsoft.ReportingServices.Interfaces.Setting> también se utiliza para procesar los datos de configuración de las extensiones que proporciona un usuario cuando se crea una suscripción o notificación.  
  
 Para obtener un ejemplo de cómo usar el <xref:Microsoft.ReportingServices.Interfaces.Setting> de clases, consulte [muestras de producto de SQL Server Reporting Services](http://go.microsoft.com/fwlink/?LinkId=177889).  
  
## <a name="see-also"></a>Vea también  
 [Implementar una extensión de entrega](../../../reporting-services/extensions/delivery-extension/implementing-a-delivery-extension.md)   
 [Biblioteca de extensión de Reporting Services](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  
