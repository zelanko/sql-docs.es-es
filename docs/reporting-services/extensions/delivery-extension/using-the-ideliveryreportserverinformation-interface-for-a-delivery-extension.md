---
title: "Uso de la interfaz IDeliveryReportServerInformation para una extensión de entrega | Microsoft Docs"
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
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- IDeliveryReportServerInformation interface
- delivery extensions [Reporting Services], retrieving report server information
ms.assetid: adbce647-18f3-470c-8114-42f8bcc95dc2
caps.latest.revision: "34"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 9f1acb146323a301d90c5c4f4ac1df6fd5b477d6
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2017
---
# <a name="using-the-ideliveryreportserverinformation-interface-for-a-delivery-extension"></a>Utilizar la interfaz IDeliveryReportServerInformation para una extensión de entrega
  La interfaz <xref:Microsoft.ReportingServices.Interfaces.IDeliveryReportServerInformation> expone varias propiedades que se pueden utilizar para recuperar información sobre un servidor de informes. Puede usar esta información para entregar notificaciones e informes. Al implementar la clase de extensión de entrega, implementa la propiedad <xref:Microsoft.ReportingServices.Interfaces.IDeliveryExtension.ReportServerInformation%2A> cuando lo requiere la interfaz <xref:Microsoft.ReportingServices.Interfaces.IDeliveryExtension>. La propiedad <xref:Microsoft.ReportingServices.Interfaces.IDeliveryExtension.ReportServerInformation%2A> devuelve un objeto que implementa la interfaz <xref:Microsoft.ReportingServices.Interfaces.IDeliveryReportServerInformation>. En este objeto puede obtener una lista de las extensiones de representación que admite actualmente el servidor de informes.  
  
 El bucle **for** siguiente se podría usar para almacenar una lista de extensiones de representación disponibles actualmente en el servidor de informes en un objeto **ArrayList**.  
  
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
  
 Para más información sobre la interfaz <xref:Microsoft.ReportingServices.Interfaces.IDeliveryReportServerInformation>, vea [Uso de la interfaz IDeliveryReportServerInformation para una extensión de entrega](../../../reporting-services/extensions/delivery-extension/using-the-ideliveryreportserverinformation-interface-for-a-delivery-extension.md).  
  
## <a name="see-also"></a>Vea también  
 <xref:Microsoft.ReportingServices.Interfaces>   
 [Implementar una extensión de entrega](../../../reporting-services/extensions/delivery-extension/implementing-a-delivery-extension.md)   
 [Biblioteca de extensiones de Reporting Services](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  
