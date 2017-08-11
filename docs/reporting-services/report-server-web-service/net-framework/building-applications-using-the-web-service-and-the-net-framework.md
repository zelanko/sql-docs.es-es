---
title: "Creación de aplicaciones mediante el servicio Web y .NET Framework | Documentos de Microsoft"
ms.custom: 
ms.date: 03/16/2017
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
- Report Server Web service, application building
- .NET Framework [Reporting Services]
- XML Web service [Reporting Services], client creation
- reports [Reporting Services], building
- Web service [Reporting Services], application building
- Report Server Web service, client creation
- client configuration [Reporting Services]
- XML Web service [Reporting Services], application building
- Web service [Reporting Services], client creation
ms.assetid: 92a9678c-bc4f-4d7a-ba44-85989bfe27ca
caps.latest.revision: 38
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 727d9ccd8cd1e40d89cfe74291edae92988b407c
ms.openlocfilehash: e228d60a4ae01aa345f007be91109b7bccb76f5a
ms.contentlocale: es-es
ms.lasthandoff: 08/09/2017

---
# <a name="building-applications-using-the-web-service-and-the-net-framework"></a>Generar aplicaciones utilizando el servicio web y .NET Framework
  Con el [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)], puede utilizar construcciones de programación conocidas, como métodos, los tipos primitivos y tipos complejos definidos por el usuario para trabajar con los servicios Web. [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] contiene una infraestructura y herramientas que puede utilizar para crear clientes de servicios web que pueden llamar a cualquier servicio web que cumpla los estándares del World Wide Web Consortium (W3C).  
  
 Un cliente del servicio web del servidor de informes es cualquier componente o aplicación que se comunica con un servidor de informes utilizando los mensajes del Protocolo simple de acceso a objetos (SOAP).  
  
 **Para crear a un cliente de servicio Web del servidor de informes mediante .NET Framework, siga estos pasos básicos:**  
  
1.  Cree una clase de proxy para el servicio web.  
  
     Para ello, agregue una clase de proxy o referencia web al proyecto de desarrollo, haga referencia a la clase de proxy en el código de cliente y cree una instancia de ese proxy. Para obtener más información, consulte [crear el Proxy del servicio Web](../../../reporting-services/report-server-web-service/net-framework/creating-the-web-service-proxy.md).  
  
2.  Autentique al cliente de servicios web con el servidor de informes.  
  
     Para ello, establezca la propiedad <xref:System.Web.Services.Protocols.WebClientProtocol.Credentials%2A> del objeto de servicio igual a las credenciales de un usuario autenticado en el servidor de informes. Para obtener más información, consulte [autenticación del servicio Web](../../../reporting-services/report-server-web-service/net-framework/web-service-authentication.md).  
  
3.  Llame al método de la clase de proxy que corresponde a la operación del servicio web que desea invocar.  
  
     Para ello, llame a un método de servicio web y proporcione los argumentos necesarios. Para obtener más información acerca de los métodos de servicio Web, consulte [métodos de servicio Web de servidor de informes](../../../reporting-services/report-server-web-service/methods/report-server-web-service-methods.md). Para obtener más información acerca de las llamadas, vea [al llamar a métodos del servicio Web](../../../reporting-services/report-server-web-service/net-framework/calling-web-service-methods.md).  
  
## <a name="in-this-section"></a>En esta sección  
  
|Tema|Description|  
|-----------|-----------------|  
|[Creación del proxy del servicio web](../../../reporting-services/report-server-web-service/net-framework/creating-the-web-service-proxy.md)|Describe las maneras de agregar una clase de proxy para el proyecto con [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)].|  
|[Autenticación del servicio web](../../../reporting-services/report-server-web-service/net-framework/web-service-authentication.md)|Describe cómo se autentican las llamadas al servicio web del servidor de informes.|  
|[Llamada a métodos de servicio web](../../../reporting-services/report-server-web-service/net-framework/calling-web-service-methods.md)|Describe cómo usar la API SOAP para llamar a métodos de servicio Web [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)].|  
|[Definición de la propiedad Url del servicio web](../../../reporting-services/report-server-web-service/net-framework/setting-the-url-property-of-the-web-service.md)|Explica cómo dirigir mediante programación el proxy del servicio web a una dirección URL de un servidor nuevo después de haber creado su referencia web.|  
|[Proporcionar argumentos de métodos de servicio web](../../../reporting-services/report-server-web-service/net-framework/supplying-web-service-method-arguments.md)|Describe cómo invocar un método de servicio web y proporcionar los argumentos del método.|  
|[Omisión de valores para objetos de servicio web opcionales](../../../reporting-services/report-server-web-service/net-framework/omitting-values-for-optional-web-service-objects.md)|Describe cómo omitir los valores para los objetos de servicio web opcionales.|  
|[Uso de métodos de servicio web seguros](../../../reporting-services/report-server-web-service/net-framework/using-secure-web-service-methods.md)|Describe la **SecureConnectionLevel** y la manera en que afecta a la utilización de la API de SOAP de Reporting Services.|  
|[Transferencia de la configuración de la información de dispositivo a las extensiones de representación](../../../reporting-services/report-server-web-service/net-framework/passing-device-information-settings-to-rendering-extensions.md)|Describe la configuración de la información de dispositivos que se utiliza para representar los informes en formatos diferentes.|  
|[Configuración de la extensión de entrega de Reporting Services](../../../reporting-services/report-server-web-service/net-framework/reporting-services-delivery-extension-settings.md)|Describe la configuración que se utiliza para entregar informes mediante el correo electrónico del servidor de informes.|  
|[Usar Reporting Services encabezados SOAP](../../../reporting-services/report-server-web-service-net-framework-soap-headers/using-reporting-services-soap-headers.md)|Explica el uso de encabezados SOAP en [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)].|  
|[Introducción a control de excepciones en Reporting Services](../../../reporting-services/report-server-web-service-net-framework-exception-handling/introducing-exception-handling-in-reporting-services.md)|Proporciona información sobre la manera en la que [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] administra los errores.|  
  
## <a name="see-also"></a>Vea también  
 [Servicio Web de servidor de informes](../../../reporting-services/report-server-web-service/report-server-web-service.md)   
 [Referencia técnica de &#40; SSRS &#41;](../../../reporting-services/technical-reference-ssrs.md)  
  
  
