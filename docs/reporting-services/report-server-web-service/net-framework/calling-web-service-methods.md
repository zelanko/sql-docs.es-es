---
title: Llamar a métodos de servicio web | Microsoft Docs
description: Llame a los métodos de una clase de proxy para realizar operaciones de informes en el servidor de informes. Los métodos de servicio web tienen acceso público y requieren los argumentos adecuados.
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
ms.openlocfilehash: 0e7347bfcb93d327bc6e56eb91c903bbc5e1f38f
ms.sourcegitcommit: d1f6da6f0f5e9630261cf733c64958938a3eb859
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/12/2020
ms.locfileid: "79198332"
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
  
  
