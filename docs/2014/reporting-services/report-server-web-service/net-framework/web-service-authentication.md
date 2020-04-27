---
title: Autenticación del servicio web | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
helpviewer_keywords:
- Web service [Reporting Services], authentication
- XML Web service [Reporting Services], authentication
- Report Server Web service, authentication
ms.assetid: 852b4947-a090-4e54-8555-5a503945ceab
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: aaccc593ea7e4baece132b759ca920018cdbe4b4
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "62518734"
---
# <a name="web-service-authentication"></a>Autenticación del servicio web
  Puede utilizar la autenticación de Windows o la autenticación básica para autenticar las llamadas realizadas al servicio web del servidor de informes. Cualquier cliente que realice solicitudes SOAP al servidor de informes debe implementar la parte del cliente de uno de los protocolos de autenticación admitidos. Si usa [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)], puede usar las clases http de código administrado para implementar la autenticación. El uso de estas API facilita el envío de información de autenticación junto con las solicitudes SOAP.  
  
 Si no tiene las credenciales adecuadas antes de realizar una llamada al servicio web del servidor de informes, se produce un error en la llamada. En tiempo de ejecución, se pueden pasar credenciales al servicio web estableciendo la propiedad **Credentials** del objeto del lado cliente que representa el servicio web antes de llamar a sus métodos.  
  
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
  
 Se deben establecer las credenciales antes de llamar a cualquiera de los métodos del servicio web del servidor de informes. Si no establece las credenciales, recibe el código de error HTTP 401 Error: Acceso denegado. Debe autenticar el servicio antes de utilizarlo, pero después de haber establecido las credenciales, no necesita establecerlas de nuevo siempre que continúe utilizando la misma variable de servicio (como *rs*).  
  
## <a name="custom-authentication"></a>Autenticación personalizada  
 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] incluye una API de programación que proporciona a los programadores la oportunidad de diseñar y desarrollar extensiones de autenticación personalizadas, conocidas como extensiones de seguridad. Para obtener más información, vea [Implementing a Security Extension](../../extensions/security-extension/implementing-a-security-extension.md).  
  
## <a name="see-also"></a>Consulte también  
 [Creación de aplicaciones con el servicio web y .NET Framework](building-applications-using-the-web-service-and-the-net-framework.md)   
 [Servicio web del servidor de informes](../report-server-web-service.md)  
  
  
