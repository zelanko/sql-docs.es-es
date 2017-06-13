---
title: Control de excepciones en Reporting Services | Documentos de Microsoft
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
- SOAP [Reporting Services], exceptions
- .NET Framework [Reporting Services]
- exceptions [Reporting Services], about exception handling
- SoapException object
ms.assetid: 1a443432-2db5-48c5-bc29-433b4688082f
caps.latest.revision: 31
author: sabotta
ms.author: carlasab
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 1cf3ca01075260274b363736bd53c245809e521c
ms.contentlocale: es-es
ms.lasthandoff: 06/13/2017

---
# <a name="handling-exceptions-in-reporting-services"></a>Administrar las excepciones en Reporting Services
  Cuando una solicitud de cliente de la API SOAP de Reporting Services no puede completarse, el servidor de informes devuelve un error en lugar de los resultados esperados de la llamada. Cuando no se puede completar una llamada, se devuelve un error para el servicio Web del servidor de informes como un SOAP **error** elemento XML. El elemento descriptivo clave del error es el **detalle** elemento, que incluye toda la información de error proporcionada por el servidor de informes, así como cualquier información de error adicional del servicio Web. La información de clave en el **detalle** elemento es el código de error del servidor de informes. Según el mensaje y el código de error, puede determinar la siguiente acción adecuada que llevar a cabo en las aplicaciones. Para obtener más información acerca de los errores de SOAP, vea el sitio web de World Wide Web Consortium (W3C) en http://www.w3.org/TR/SOAP.  
  
## <a name="soap-faults-and-the-net-framework"></a>Errores de SOAP y .NET Framework  
 En el [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)], si se produce un error en una solicitud de cliente al servicio Web, el servidor de informes comunica el error en el código de cliente que llama al servicio Web iniciando un **SoapException** objeto. El **SoapException** ajusta la información contenida en un error de SOAP. El **detalle** propiedad de la **SoapException** se asigna a la **detalle** elemento en el error de SOAP. Las aplicaciones deberían detectar el **SoapException** objeto con un bloque try/catch y utilizar el **detalle** propiedad de la **SoapException** para tomar las medidas adecuadas. Para obtener más información sobre la **SoapException** clase y la **detalle** propiedad en [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], consulte [Reporting Services SoapException (clase)](../../reporting-services/report-server-web-service-net-framework-exception-handling/soapexception-class/reporting-services-soapexception-class.md). Para obtener más información sobre la **SoapException** de clases, consulte la [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] documentación del SDK.  
  
## <a name="see-also"></a>Vea también  
 [Propiedad Detail](../../reporting-services/report-server-web-service-net-framework-exception-handling/soapexception-class/detail-property.md)   
 [Introducción a control de excepciones en Reporting Services](../../reporting-services/report-server-web-service-net-framework-exception-handling/introducing-exception-handling-in-reporting-services.md)   
 [Clase SoapException de Reporting Services](../../reporting-services/report-server-web-service-net-framework-exception-handling/soapexception-class/reporting-services-soapexception-class.md)  
  
  
