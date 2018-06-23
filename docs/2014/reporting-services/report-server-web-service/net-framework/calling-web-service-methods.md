---
title: Llamar a métodos de servicio web | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- Web service [Reporting Services], SOAP
- Web service [Reporting Services], calls
- calling Web service
- Report Server Web service, SOAP
- XML Web service [Reporting Services], calls
- Report Server Web service, calls
- XML Web service [Reporting Services], SOAP
- SOAP [Reporting Services], calls
ms.assetid: f6f0c6e3-8bb5-4c44-9d19-1872edc72746
caps.latest.revision: 37
author: douglaslM
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: fce65cf5ed4e8342005e058aec793fa88e6aa182
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36106898"
---
# <a name="calling-web-service-methods"></a>Llamar a métodos de servicio web
  Al utilizar una clase de proxy de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] para llamar a las operaciones de servicio web, se usan los métodos de esa clase. Estos métodos responden como cualquier otro de una clase de la biblioteca de clases de [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)]. Todos los métodos de servicio web tienen acceso público y necesitan que se proporcione el número y tipos adecuados de argumentos. Después de crear una instancia de la clase de proxy en el proyecto, puede llamar a los métodos para realizar las operaciones del informe de errores a través del servidor de informes. En el código de C# siguiente se ilustra el uso del método <xref:ReportService2010.ReportingService2010.ListChildren%2A> de la clase de proxy de <xref:ReportService2010.ReportingService2010>. El código se utiliza para realizar una llamada recursiva al servicio web que devuelve una matriz de objetos <xref:ReportService2010.CatalogItem> que contiene una lista de todos los elementos de la base de datos del servidor de informes:  
  
```vb  
Dim rs As New ReportingService2010()  
rs.Credentials = System.Net.CredentialCache.DefaultCredentials  
Dim items As CatalogItem() = rs.ListChildren("/", True)  
```  
  
```csharp  
ReportingService2010 rs = new ReportingService2010();  
rs.Credentials = System.Net.CredentialCache.DefaultCredentials;  
CatalogItem[] items = rs.ListChildren("/", true);  
```  
  
## <a name="see-also"></a>Vea también  
 [Creación de aplicaciones con el servicio web y .NET Framework](building-applications-using-the-web-service-and-the-net-framework.md)   
 [Servicio web del servidor de informes](../report-server-web-service.md)   
 [Referencia técnica &#40;SSRS&#41;](../../technical-reference-ssrs.md)  
  
  