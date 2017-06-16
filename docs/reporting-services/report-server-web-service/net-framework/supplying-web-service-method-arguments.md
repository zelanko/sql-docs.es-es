---
title: "Proporcionar argumentos de método de servicio Web | Documentos de Microsoft"
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
- Report Server Web service, methods
- Web service [Reporting Services], methods
- methods [Reporting Services], arguments
- XML Web service [Reporting Services], methods
ms.assetid: f7b9ca05-fc4c-4b30-8e5d-172dd0f4a832
caps.latest.revision: 38
author: sabotta
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 43fcfe6eecffdc237366eb7963a5582b1915d363
ms.contentlocale: es-es
ms.lasthandoff: 06/13/2017

---
# <a name="supplying-web-service-method-arguments"></a>Proporcionar argumentos de métodos de servicio web
  Un método de servicio web del servidor de informes envía una solicitud al servicio en una dirección URL determinada utilizando SOAP sobre HTTP. El servicio recibe la solicitud, la procesa y, a continuación, devuelve una respuesta. Estas solicitudes y respuestas tienen forma de documentos XML.  
  
## <a name="optional-parameters"></a>Parámetros opcionales  
 En algunos casos, un método de servicio web puede tener parámetros de entrada opcionales. Incluso si un parámetro de entrada para un método de servicio Web es opcional, debe incluirlo y establecer el valor del parámetro **null** (**nada** en [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)]). Establecer un valor de parámetro en **null** establece el valor del elemento para ese parámetro en la solicitud SOAP para **null**.  
  
 En el ejemplo siguiente se utiliza el método <xref:ReportService2010.ReportingService2010.CreateFolder%2A> para crear un carpeta nueva denominada Product Sales en la carpeta Sales. Si se suministra un **null** se proporcionó el valor para las propiedades de carpeta, ninguna propiedad específica del usuario para la carpeta:  
  
```  
// C#  
rs.CreateFolder("Product Sales", "/Sales", null);  
```  
  
## <a name="complex-data-types"></a>Tipos de data complejos  
 La clase principal del servicio web del servidor de informes es <xref:ReportService2010.ReportingService2010>, que se utiliza para invocar las operaciones SOAP o los métodos web de la clase de proxy. Para admitir esta clase y sus métodos, [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] incluye tipos de datos complejos definidos por el usuario que son específicos de los parámetros de entrada y salida de los métodos de servicio web. Estos tipos de datos complejos forman parte de la clase de proxy generada, que puede usar para el desarrollo en el [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] entorno.  
  
 Al generar una clase de proxy, los tipos de datos complejos que se definen en el archivo WSDL se representan mediante las clases de proxy, que incluyen las propiedades correspondientes a los diversos elementos de SOAP de los tipos de datos complejos. Las secuencias de estos tipos de datos se convierten en matrices de objetos que puede enumerar en el código. Esto evita tener que trabajar directamente con las estructuras XML que se envían en los mensajes SOAP. [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] realiza traducción en su lugar.  
  
## <a name="see-also"></a>Vea también  
 [Creación de aplicaciones con el servicio Web y .NET Framework](../../../reporting-services/report-server-web-service/net-framework/building-applications-using-the-web-service-and-the-net-framework.md)   
 [Servicio Web de servidor de informes](../../../reporting-services/report-server-web-service/report-server-web-service.md)   
 [Referencia técnica de &#40; SSRS &#41;](../../../reporting-services/technical-reference-ssrs.md)  
  
  
