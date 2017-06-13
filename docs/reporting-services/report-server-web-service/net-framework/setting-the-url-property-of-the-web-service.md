---
title: "Establecer la propiedad de dirección Url del servicio Web | Documentos de Microsoft"
ms.custom: 
ms.date: 03/14/2017
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
- Url property
- Report Server Web service, proxies
- proxies [Reporting Services]
- XML Web service [Reporting Services], proxies
- Web service [Reporting Services], proxies
- Web references [Reporting Services]
ms.assetid: 4eac4e40-dafb-4403-acde-13df317c8ec8
caps.latest.revision: 36
author: sabotta
ms.author: carlasab
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 515c8d244e6dfb090ef6993e34fa26efeee9df1e
ms.contentlocale: es-es
ms.lasthandoff: 06/13/2017

---
# <a name="setting-the-url-property-of-the-web-service"></a>Establecer la propiedad Url del servicio web
  En cualquier momento en el [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] aplicaciones, puede modificar la dirección URL base del servicio Web del servidor de informes a la que se dirige la aplicación. Para ello, basta con establecer la **Url** propiedad del objeto de servicio. Por ejemplo:  
  
```vb  
Dim rs As New ReportingService2010()  
rs.Credentials = System.Net.CredentialCache.DefaultCredentials  
rs.Url = "http://<Server Name>/reportserver/ReportService2010.asmx"  
```  
  
```csharp  
ReportingService2010 service = new ReportingService2010();  
rs.Credentials = System.Net.CredentialCache.DefaultCredentials;  
rs.Url = "http://<Server Name>/reportserver/ReportService2010.asmx";  
```  
  
 El ejemplo siguiente recupera una definición de informe de un servidor de informes y utiliza esa definición para crear un informe idéntico en un servidor de informes diferente:  
  
```vb  
Imports System  
Imports System.Web.Services.Protocols  
  
Class Sample  
   Public Shared Sub Main()  
      Dim rs As New ReportingService2010()  
      rs.Credentials = System.Net.CredentialCache.DefaultCredentials  
      ' Set the base Web service URL of the source server  
      rs.Url = "http://<Server Name>/reportserver/ReportService2010.asmx"  
  
      Dim reportName As String = "/SampleReports/Company Sales"  
      Dim reportDefinition As Byte() = Nothing  
  
      Try  
         ' Get the report definition of a report on a source server  
         reportDefinition = rs.GetItemDefinition(reportName)  
         ' Set the base Web service URL of the destination server  
         rs.Url = "http://<Server Name>/reportserver/ReportService2010.asmx"  
         ' Create a copy of the report on the destination server  
         Dim warnings As Warning() = {}  
         rs.CreateCatalogItem("Report", "Company Sales Copy", "/", False, reportDefinition, Nothing, warnings)        
      Catch e As SoapException  
         Console.WriteLine(e.Detail.InnerXml.ToString())  
      End Try  
   End Sub 'Main  
End Class 'Sample  
```  
  
```csharp  
using System;  
using System.Web.Services.Protocols;  
  
class Sample  
{  
   public static void Main()  
   {  
      ReportingService2010 rs = new ReportingService2010();  
      rs.Credentials = System.Net.CredentialCache.DefaultCredentials;  
      // Set the base Web service URL of the source server  
      rs.Url = "http://<Server Name>/reportserver/reportservice2010.asmx";  
  
      string reportName = "/SampleReports/Company Sales";  
      byte[] reportDefinition = null;  
  
      try  
      {  
         reportDefinition = rs.GetItemDefinition(reportName);  
         // Set the base Web service URL of the destination server  
         rs.Url = "http://<Server Name>/reportserver/ReportService2010.asmx";  
         // Create a copy of the report on the destination server  
         Warning[] warnings = {};  
         rs.CreateCatalogItem("Report", "Company Sales Copy", "/", false, reportDefinition, null, out warnings);  
      }  
  
      catch (SoapException e)  
      {  
         Console.WriteLine(e.Detail.InnerXml.ToString());   
      }  
   }  
}  
```  
  
 Para obtener más información acerca de cómo crear el proxy del servicio Web inicial, vea [crear el Proxy del servicio Web](../../../reporting-services/report-server-web-service/net-framework/creating-the-web-service-proxy.md).  
  
## <a name="see-also"></a>Vea también  
 <xref:ReportService2010.ReportingService2010.CreateCatalogItem%2A>   
 <xref:ReportService2010.ReportingService2010.GetItemDefinition%2A>   
 [Creación de aplicaciones con el servicio Web y .NET Framework](../../../reporting-services/report-server-web-service/net-framework/building-applications-using-the-web-service-and-the-net-framework.md)   
 [Servicio Web de servidor de informes](../../../reporting-services/report-server-web-service/report-server-web-service.md)  
  
  
