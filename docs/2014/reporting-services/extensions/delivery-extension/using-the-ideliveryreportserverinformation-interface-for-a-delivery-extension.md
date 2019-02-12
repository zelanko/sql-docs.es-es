---
title: Uso de la interfaz IDeliveryReportServerInformation para una extensión de entrega | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.topic: reference
helpviewer_keywords:
- IDeliveryReportServerInformation interface
- delivery extensions [Reporting Services], retrieving report server information
ms.assetid: adbce647-18f3-470c-8114-42f8bcc95dc2
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: d211842a43af771e953fd74a15403ba9321f2860
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/11/2019
ms.locfileid: "56028006"
---
# <a name="using-the-ideliveryreportserverinformation-interface-for-a-delivery-extension"></a>Utilizar la interfaz IDeliveryReportServerInformation para una extensión de entrega
  La interfaz <xref:Microsoft.ReportingServices.Interfaces.IDeliveryReportServerInformation> expone varias propiedades que se pueden utilizar para recuperar información sobre un servidor de informes. Puede usar esta información para entregar notificaciones e informes. Al implementar la clase de extensión de entrega, implementa la propiedad <xref:Microsoft.ReportingServices.Interfaces.IDeliveryExtension.ReportServerInformation%2A> cuando lo requiere la interfaz <xref:Microsoft.ReportingServices.Interfaces.IDeliveryExtension>. La propiedad <xref:Microsoft.ReportingServices.Interfaces.IDeliveryExtension.ReportServerInformation%2A> devuelve un objeto que implementa la interfaz <xref:Microsoft.ReportingServices.Interfaces.IDeliveryReportServerInformation>. En este objeto puede obtener una lista de las extensiones de representación que admite actualmente el servidor de informes.  
  
 La siguiente `for` bucle podría usarse para almacenar una lista de extensiones de representación disponibles actualmente en el servidor de informes en un **ArrayList** objeto.  
  
```vb  
Dim renderFormats As New ArrayList()  
Dim e As Microsoft.ReportingServices.Interfaces.Extension  
For Each e In  ReportServerInformation.RenderingExtension  
   If e.Visible Then  
      renderFormats.Add(e.Name)  
   End If  
Next e  
```  
  
```csharp  
ArrayList renderFormats = new ArrayList();  
foreach (Microsoft.ReportingServices.Interfaces.Extension e in ReportServerInformation.RenderingExtension)  
{   
   if (e.Visible)  
   {  
      renderFormats.Add(e.Name);  
   }  
}  
```  
  
 Para más información sobre la interfaz <xref:Microsoft.ReportingServices.Interfaces.IDeliveryReportServerInformation>, vea [Uso de la interfaz IDeliveryReportServerInformation para una extensión de entrega](using-the-ideliveryreportserverinformation-interface-for-a-delivery-extension.md).  
  
## <a name="see-also"></a>Vea también  
 <xref:Microsoft.ReportingServices.Interfaces>   
 [Implementar una extensión de entrega](implementing-a-delivery-extension.md)   
 [Biblioteca de extensiones de Reporting Services](../reporting-services-extension-library.md)  
  
  
