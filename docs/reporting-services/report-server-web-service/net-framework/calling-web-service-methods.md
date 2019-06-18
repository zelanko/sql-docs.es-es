---
title: Llamar a métodos de servicio web | Microsoft Docs
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server-web-service
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
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 65da2d36c53f5f00851b36f47396b7bcbf6a6092
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63284604"
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
  
## <a name="see-also"></a>Consulte también  
 [Creación de aplicaciones con el servicio web y .NET Framework](../../../reporting-services/report-server-web-service/net-framework/building-applications-using-the-web-service-and-the-net-framework.md)   
 [Servicio web del servidor de informes](../../../reporting-services/report-server-web-service/report-server-web-service.md)   
 [Referencia técnica &#40;SSRS&#41;](../../../reporting-services/technical-reference-ssrs.md)  
  
  
