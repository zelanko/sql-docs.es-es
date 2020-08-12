---
title: Usar la clase Setting para una extensión de entrega | Microsoft Docs
description: Obtenga información sobre cómo las extensiones de entrega pueden usar la clase Setting, que almacena información que la extensión de entrega necesita para entregar notificaciones e informes.
ms.date: 03/06/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: extensions
ms.topic: reference
helpviewer_keywords:
- delivery extensions [Reporting Services], settings
- Setting class
ms.assetid: 50746639-da7c-46a5-ac7b-e87dd6b91880
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: d90728a83821575bd71c3fe93fb1a090beaf8bdb
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/08/2020
ms.locfileid: "84529101"
---
# <a name="using-the-setting-class-for-a-delivery-extension"></a>Usar la clase Setting para una extensión de entrega
  La clase <xref:Microsoft.ReportingServices.Interfaces.Setting> se encuentra en el espacio de nombres <xref:Microsoft.ReportingServices.Interfaces> y representa información sobre la configuración de una extensión de entrega. La clase <xref:Microsoft.ReportingServices.Interfaces.Setting> proporciona la infraestructura para almacenar información sobre la configuración que se requiere para que una extensión de entrega funcione correctamente. Por ejemplo, en la distribución por correo electrónico del servidor de informes, un usuario debe proporcionar la configuración específica para la entrega por correo electrónico, por ejemplo la dirección del destinatario, la dirección del remitente, la línea de asunto del correo electrónico, entre otras. Indudablemente, los proveedores de entrega personalizados exigirán al usuario que proporcione valores concretos para que la extensión de entrega entregue las notificaciones e informes.  
  
 La clase <xref:Microsoft.ReportingServices.Interfaces.Setting> se usa al implementar la propiedad <xref:Microsoft.ReportingServices.Interfaces.IDeliveryExtension.ExtensionSettings%2A> de la interfaz <xref:Microsoft.ReportingServices.Interfaces.IDeliveryExtension>. La clase <xref:Microsoft.ReportingServices.Interfaces.Setting> también se utiliza para procesar los datos de configuración de las extensiones que proporciona un usuario cuando se crea una suscripción o notificación.  
  
 Para obtener un ejemplo de cómo usar la clase <xref:Microsoft.ReportingServices.Interfaces.Setting>, vea [Ejemplos del producto SQL Server Reporting Services](https://go.microsoft.com/fwlink/?LinkId=177889).  
  
## <a name="see-also"></a>Consulte también  
 [Implementar una extensión de entrega](../../../reporting-services/extensions/delivery-extension/implementing-a-delivery-extension.md)   
 [Biblioteca de extensiones de Reporting Services](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  
