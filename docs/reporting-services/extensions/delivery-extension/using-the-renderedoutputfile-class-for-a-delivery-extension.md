---
title: "Usar la clase RenderedOutputFile para una extensión de entrega | Microsoft Docs"
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
- RenderedOutputFile class
- data streams [Reporting Services]
- delivery extensions [Reporting Services], data streams
ms.assetid: 8b591801-42d5-49fa-b710-bf7e6917accf
caps.latest.revision: "34"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 1bd538d180668bdc6d4e99fb1d8246f8c4cbefaa
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2017
---
# <a name="using-the-renderedoutputfile-class-for-a-delivery-extension"></a>Usar la clase RenderedOutputFile para una extensión de entrega
  La clase <xref:Microsoft.ReportingServices.Interfaces.RenderedOutputFile> representa un flujo de datos e información sobre las propiedades asociadas del mismo. La propiedad **Data** de la clase <xref:Microsoft.ReportingServices.Interfaces.RenderedOutputFile> se usa para representar un informe representado o un recurso de informe como un objeto **Stream**.  
  
 El método <xref:Microsoft.ReportingServices.Interfaces.Report.Render%2A> del objeto **Report** devuelve una matriz de uno o varios objetos <xref:Microsoft.ReportingServices.Interfaces.RenderedOutputFile> que constituyen en conjunto un único informe representado. El primer objeto <xref:Microsoft.ReportingServices.Interfaces.RenderedOutputFile> es el informe representado. Cualquier otro objeto <xref:Microsoft.ReportingServices.Interfaces.RenderedOutputFile> son los recursos que se deben entregar junto con los datos del informe (por ejemplo, un archivo HTML e imágenes asociadas). Las extensiones de representación que son extensiones de un único flujo (IMAGE, PDF, MHTML y EXCEL) devuelven solo un objeto <xref:Microsoft.ReportingServices.Interfaces.RenderedOutputFile> en la matriz.  
  
 Para obtener un ejemplo de cómo usar la clase <xref:Microsoft.ReportingServices.Interfaces.RenderedOutputFile>, vea [Ejemplos del producto SQL Server Reporting Services](http://go.microsoft.com/fwlink/?LinkId=177889).  
  
## <a name="see-also"></a>Vea también  
 [Implementar una extensión de entrega](../../../reporting-services/extensions/delivery-extension/implementing-a-delivery-extension.md)   
 [Biblioteca de extensiones de Reporting Services](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  
