---
title: Usar la propiedad Detail para administrar errores concretos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- exceptions [Reporting Services], Detail property
- Detail property
- InnerText property
ms.assetid: 4392633d-b46b-41e6-bc12-efb64e166704
caps.latest.revision: 29
author: douglaslM
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 08f109483a1b9aa39046316920ac84dbd8022438
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36198606"
---
# <a name="using-the-detail-property-to-handle-specific-errors"></a>Usar la propiedad Detail para administrar errores concretos
  Para clasificar más las excepciones, [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] devuelve información de error adicional en la propiedad **InnerText** de los elementos secundarios en la propiedad **Detail** de la excepción SOAP. Dado que la propiedad **Detail** es un objeto **XmlNode**, puede tener acceso al texto interno del elemento secundario **Message** utilizando el código siguiente.  
  
 Para obtener una lista de todos los elementos secundarios disponibles contenidos en la propiedad **Detail**, vea [Propiedad Detail](../soapexception-class/detail-property.md). Para más información, vea "Propiedad Detail" en la documentación del SDK de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)].  
  
```vb  
Try  
' Code for accessing the report server  
Catch ex As SoapException  
   ' The exception is a SOAP exception, so use  
   ' the Detail property's Message element.  
   Console.WriteLine(ex.Detail("Message").InnerXml)  
End Try  
```  
  
```csharp  
try  
{  
   // Code for accessing the report server  
}  
catch (SoapException ex)  
{  
   // The exception is a SOAP exception, so use  
   // the Detail property's Message element.  
   Console.WriteLine(ex.Detail["Message"].InnerXml);  
}  
```  
  
```vb  
Try  
' Code for accessing the report server  
Catch ex As SoapException  
   If ex.Detail("ErrorCode").InnerXml = "rsInvalidItemName" Then  
   End If ' Perform an action based on the specific error code  
End Try  
```  
  
```csharp  
try  
{  
   // Code for accessing the report server  
}  
catch (SoapException ex)  
{  
   if (ex.Detail["ErrorCode"].InnerXml == "rsInvalidItemName")  
   {  
      // Perform an action based on the specific error code  
   }  
}  
```  
  
 La línea de código siguiente escribe el código de error concreto que se va a devolver en la excepción SOAP para la consola. Podría evaluar también el código de error y realizar acciones específicas.  
  
```vb  
Console.WriteLine(ex.Detail("ErrorCode").InnerXml)  
```  
  
```csharp  
Console.WriteLine(ex.Detail["ErrorCode"].InnerXml);  
```  
  
## <a name="see-also"></a>Vea también  
 [Introducción a la administración de excepciones en Reporting Services](../introducing-exception-handling-in-reporting-services.md)   
 [Clase SoapException de Reporting Services](../soapexception-class/reporting-services-soapexception-class.md)   
 [Tabla de errores de SoapException](../soapexception-class/soapexception-errors-table.md)  
  
  