---
title: "Autenticación del servicio de Web | Documentos de Microsoft"
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
- Web service [Reporting Services], authentication
- XML Web service [Reporting Services], authentication
- Report Server Web service, authentication
ms.assetid: 852b4947-a090-4e54-8555-5a503945ceab
caps.latest.revision: 33
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 727d9ccd8cd1e40d89cfe74291edae92988b407c
ms.openlocfilehash: be7e76aa26ca4b94afd2e32b40b9fbfbe92b170d
ms.contentlocale: es-es
ms.lasthandoff: 08/09/2017

---
# <a name="web-service-authentication"></a>Autenticación del servicio Web
  Puede utilizar la autenticación de Windows o la autenticación básica para autenticar las llamadas realizadas al servicio web del servidor de informes. Cualquier cliente que realice solicitudes SOAP al servidor de informes debe implementar la parte del cliente de uno de los protocolos de autenticación admitidos. Si usas el [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)], puede utilizar las clases HTTP de código administrado para implementar la autenticación. El uso de estas API facilita el envío de información de autenticación junto con las solicitudes SOAP.  
  
 Si no tiene las credenciales adecuadas antes de realizar una llamada al servicio web del servidor de informes, se produce un error en la llamada. En tiempo de ejecución, puede pasar credenciales al servicio Web estableciendo la **credenciales** propiedad del objeto de cliente que representa el servicio Web antes de llamar a sus métodos.  
  
 Las secciones siguientes contienen código de ejemplo que envía credenciales mediante [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)].  
  
## <a name="windows-authentication"></a>Autenticación de Windows  
 El código siguiente pasa las credenciales de Windows al servicio web.  
  
```vb  
Dim rs As New ReportingService()  
rs.Credentials = System.Net.CredentialCache.DefaultCredentials  
```  
  
```csharp  
ReportingService rs = new ReportingService();  
rs.Credentials = System.Net.CredentialCache.DefaultCredentials;  
```  
  
## <a name="basic-authentication"></a>Autenticación básica  
 El código siguiente pasa las credenciales básicas al servicio web.  
  
```vb  
Dim rs As New ReportingService()  
rs.Credentials = New System.Net.NetworkCredential("username", "password", "domain")  
```  
  
```csharp  
ReportingService service = new ReportingService();  
service.Credentials = new System.Net.NetworkCredential("username", "password", "domain");  
```  
  
 Se deben establecer las credenciales antes de llamar a cualquiera de los métodos del servicio web del servidor de informes. Si no establece las credenciales, recibe el código de error HTTP 401 Error: Acceso denegado. Debe autenticar el servicio antes de que se usa, pero después de que ha establecido las credenciales, no es necesario establecer nuevo mientras se sigue usando la misma variable de servicio (como *rs*).  
  
## <a name="custom-authentication"></a>Autenticación personalizada  
 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] incluye una API de programación que proporciona a los programadores la oportunidad de diseñar y desarrollar extensiones de autenticación personalizadas, conocidas como extensiones de seguridad. Para obtener más información, vea [Implementing a Security Extension](../../../reporting-services/extensions/security-extension/implementing-a-security-extension.md).  
  
## <a name="see-also"></a>Vea también  
 [Creación de aplicaciones con el servicio Web y .NET Framework](../../../reporting-services/report-server-web-service/net-framework/building-applications-using-the-web-service-and-the-net-framework.md)   
 [Servicio Web de servidor de informes](../../../reporting-services/report-server-web-service/report-server-web-service.md)  
  
  

