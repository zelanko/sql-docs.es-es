---
title: Uso de la interfaz IDeliveryReportServerInformation para una extensión de entrega | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
helpviewer_keywords:
- IDeliveryReportServerInformation interface
- delivery extensions [Reporting Services], retrieving report server information
ms.assetid: adbce647-18f3-470c-8114-42f8bcc95dc2
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 2a94b6da8536ee0269a448b8a446fc0da3f3f576
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63164044"
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
  
  
