---
title: Proporcionar argumentos de métodos de servicio web | Microsoft Docs
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server-web-service
ms.topic: reference
helpviewer_keywords:
- Report Server Web service, methods
- Web service [Reporting Services], methods
- methods [Reporting Services], arguments
- XML Web service [Reporting Services], methods
ms.assetid: f7b9ca05-fc4c-4b30-8e5d-172dd0f4a832
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: ad5251471fe9be594bf0ffb09c13f5f9afc35990
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63128956"
---
# <a name="supplying-web-service-method-arguments"></a>Proporcionar argumentos de métodos de servicio web
  Un método de servicio web del servidor de informes envía una solicitud al servicio en una dirección URL determinada utilizando SOAP sobre HTTP. El servicio recibe la solicitud, la procesa y, a continuación, devuelve una respuesta. Estas solicitudes y respuestas tienen forma de documentos XML.  
  
## <a name="optional-parameters"></a>Parámetros opcionales  
 En algunos casos, un método de servicio web puede tener parámetros de entrada opcionales. Incluso aunque un parámetro de entrada para un método de servicio web sea opcional, todavía debe incluirlo y establecer el valor del parámetro en **null** (**Nothing** en [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)]). Al establecer un valor de parámetro en **null**, el valor de elemento para ese parámetro en la solicitud SOAP se establece en **null**.  
  
 En el ejemplo siguiente se utiliza el método <xref:ReportService2010.ReportingService2010.CreateFolder%2A> para crear un carpeta nueva denominada Product Sales en la carpeta Sales. Al ofrecer un valor **null** para las propiedades de la carpeta, no se proporciona ninguna propiedad específica del usuario para la carpeta:  
  
```  
// C#  
rs.CreateFolder("Product Sales", "/Sales", null);  
```  
  
## <a name="complex-data-types"></a>Tipos de data complejos  
 La clase principal del servicio web del servidor de informes es <xref:ReportService2010.ReportingService2010>, que se utiliza para invocar las operaciones SOAP o los métodos web de la clase de proxy. Para admitir esta clase y sus métodos, [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] incluye tipos de datos complejos definidos por el usuario que son específicos de los parámetros de entrada y salida de los métodos de servicio web. Estos tipos de datos complejos forman parte de la clase de proxy generada, que puede usar al desarrollar en el entorno de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)].  
  
 Al generar una clase de proxy, los tipos de datos complejos que se definen en el archivo WSDL se representan mediante las clases de proxy, que incluyen las propiedades correspondientes a los diversos elementos de SOAP de los tipos de datos complejos. Las secuencias de estos tipos de datos se convierten en matrices de objetos que puede enumerar en el código. Esto evita tener que trabajar directamente con las estructuras XML que se envían en los mensajes SOAP. [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] realiza traducción en su lugar.  
  
## <a name="see-also"></a>Consulte también  
 [Creación de aplicaciones con el servicio web y .NET Framework](../../../reporting-services/report-server-web-service/net-framework/building-applications-using-the-web-service-and-the-net-framework.md)   
 [Servicio web del servidor de informes](../../../reporting-services/report-server-web-service/report-server-web-service.md)   
 [Referencia técnica &#40;SSRS&#41;](../../../reporting-services/technical-reference-ssrs.md)  
  
  
