---
title: Proporcionar argumentos de métodos de servicio web | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.component: report-server-web-service
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
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
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: a273ce7fb8ddcb53545c4fe95db8e6062a1e5b45
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "33025412"
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
  
## <a name="see-also"></a>Ver también  
 [Creación de aplicaciones con el servicio web y .NET Framework](../../../reporting-services/report-server-web-service/net-framework/building-applications-using-the-web-service-and-the-net-framework.md)   
 [Servicio web del servidor de informes](../../../reporting-services/report-server-web-service/report-server-web-service.md)   
 [Referencia técnica &#40;SSRS&#41;](../../../reporting-services/technical-reference-ssrs.md)  
  
  
