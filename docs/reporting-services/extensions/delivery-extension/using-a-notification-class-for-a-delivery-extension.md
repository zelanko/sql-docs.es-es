---
title: "Utilizar una clase de notificación para una extensión de entrega | Documentos de Microsoft"
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
- delivery extensions [Reporting Services], notifications
- notifications [Reporting Services]
- retry queues
- Nofication class
ms.assetid: 549c40c4-d33d-46c2-9d6a-7bbb671ac67a
caps.latest.revision: 33
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: a6aab5e722e732096e9e4ffdf458ac25088e09ae
ms.openlocfilehash: 064d5556dca130324f69dd49d14f3caa76c8eec8
ms.contentlocale: es-es
ms.lasthandoff: 08/03/2017

---
# <a name="using-a-notification-class-for-a-delivery-extension"></a>Usar una clase Notification para una extensión de entrega
  La clase <xref:Microsoft.ReportingServices.Interfaces.Notification> se encuentra en el espacio de nombres <xref:Microsoft.ReportingServices.Interfaces> y representa información de suscripción que las extensiones de entrega utilizan para entregar los informes. La clase <xref:Microsoft.ReportingServices.Interfaces.Notification> proporciona varias propiedades que se pueden utilizar para representar los informes para la entrega, determinar el estado de la notificación y establecer los datos de usuario.  
  
 ![Proceso de notificación de informes](../../../reporting-services/extensions/delivery-extension/media/bk-ext-03.gif "proceso de notificación de informes")  
La notificación es el objeto central de cualquier entrega  
  
 Cuando se desencadena un evento que está asociado a una suscripción que utiliza la extensión de entrega personalizada, se crea una notificación que contiene un objeto <xref:Microsoft.ReportingServices.Interfaces.Report>. El objeto <xref:Microsoft.ReportingServices.Interfaces.Report> encapsula la funcionalidad que se necesita para representar un informe determinado en un formato de representación admitido y contiene las propiedades específicas del informe, como la dirección URL del informe en el servidor y su nombre. Para obtener más información sobre la <xref:Microsoft.ReportingServices.Interfaces.Report> de clases, consulte [mediante la clase de informe para una extensión de entrega](../../../reporting-services/extensions/delivery-extension/using-the-report-class-for-a-delivery-extension.md).  
  
 Se pasa el objeto <xref:Microsoft.ReportingServices.Interfaces.Notification> al método <xref:Microsoft.ReportingServices.Interfaces.IDeliveryExtension.Deliver%2A> de la extensión de entrega. El método <xref:Microsoft.ReportingServices.Interfaces.IDeliveryExtension.Deliver%2A> debería contener código concreto para procesar la notificación y entregar el informe.  
  
 Para obtener un ejemplo de cómo usar el <xref:Microsoft.ReportingServices.Interfaces.Notification> de clases, consulte [muestras de producto de SQL Server Reporting Services](http://go.microsoft.com/fwlink/?LinkId=177889).  
  
## <a name="retry-functionality"></a>Funcionalidad de reintento  
 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] le permite crear una cola de reintento para las notificaciones que no se pueden entregar inmediatamente. Una vez que el servidor de informes invoca el método <xref:Microsoft.ReportingServices.Interfaces.IDeliveryExtension.Deliver%2A> de una extensión de entrega, esta puede solicitar que el servidor de informes vuelva a intentar la entrega más adelante. Si ocurre esto, el servidor de informes coloca la notificación en una cola interna y reintenta la entrega cuando transcurra un período concreto. Los administradores pueden configurar el número máximo de reintentos que realiza el servidor de informes y el período entre los intentos en la sección de extensión de entrega del archivo RSReportServer.config utilizando la **MaxNumberOfRetries** elemento XML y el **PeriodBetweenRetries** elemento XML. Las notificaciones se quitan de la cola de reintento si la entrega posterior tiene éxito o si se alcanza el número máximo de reintentos. Si se produce un error en la entrega después del número máximo de reintentos, se descarta la notificación.  
  
## <a name="see-also"></a>Vea también  
 [Implementar una extensión de entrega](../../../reporting-services/extensions/delivery-extension/implementing-a-delivery-extension.md)   
 [Biblioteca de extensión de Reporting Services](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  
