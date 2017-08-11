---
title: "Usar la clase RenderedOutputFile para una extensión de entrega | Documentos de Microsoft"
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
- RenderedOutputFile class
- data streams [Reporting Services]
- delivery extensions [Reporting Services], data streams
ms.assetid: 8b591801-42d5-49fa-b710-bf7e6917accf
caps.latest.revision: 34
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: a6aab5e722e732096e9e4ffdf458ac25088e09ae
ms.openlocfilehash: 35fa7b98c43bb20ef6df30f27ca74a5f2ada1792
ms.contentlocale: es-es
ms.lasthandoff: 08/03/2017

---
# <a name="using-the-renderedoutputfile-class-for-a-delivery-extension"></a>Usar la clase RenderedOutputFile para una extensión de entrega
  La clase <xref:Microsoft.ReportingServices.Interfaces.RenderedOutputFile> representa un flujo de datos e información sobre las propiedades asociadas del mismo. El **datos** propiedad de la <xref:Microsoft.ReportingServices.Interfaces.RenderedOutputFile> clase se utiliza para representar un informe representado o recurso de informe como un **flujo** objeto.  
  
 El <xref:Microsoft.ReportingServices.Interfaces.Report.Render%2A> método de la **informe** object devuelve una matriz de uno o varios <xref:Microsoft.ReportingServices.Interfaces.RenderedOutputFile> objetos que constituyen un único informe representado. El primer objeto <xref:Microsoft.ReportingServices.Interfaces.RenderedOutputFile> es el informe representado. Cualquier otro objeto <xref:Microsoft.ReportingServices.Interfaces.RenderedOutputFile> son los recursos que se deben entregar junto con los datos del informe (por ejemplo, un archivo HTML e imágenes asociadas). Las extensiones de representación que son extensiones de un único flujo (IMAGE, PDF, MHTML y EXCEL) devuelven solo un objeto <xref:Microsoft.ReportingServices.Interfaces.RenderedOutputFile> en la matriz.  
  
 Para obtener un ejemplo de cómo usar el <xref:Microsoft.ReportingServices.Interfaces.RenderedOutputFile> de clases, consulte [muestras de producto de SQL Server Reporting Services](http://go.microsoft.com/fwlink/?LinkId=177889).  
  
## <a name="see-also"></a>Vea también  
 [Implementar una extensión de entrega](../../../reporting-services/extensions/delivery-extension/implementing-a-delivery-extension.md)   
 [Biblioteca de extensión de Reporting Services](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  
