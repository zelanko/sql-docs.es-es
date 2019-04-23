---
title: Administrar las excepciones en Reporting Services | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
helpviewer_keywords:
- SOAP [Reporting Services], exceptions
- .NET Framework [Reporting Services]
- exceptions [Reporting Services], about exception handling
- SoapException object
ms.assetid: 1a443432-2db5-48c5-bc29-433b4688082f
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 1d887853b475f7b4d673d7b04343ae9bc71644d3
ms.sourcegitcommit: b87c384e10d6621cf3a95ffc79d6f6fad34d420f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/22/2019
ms.locfileid: "60157321"
---
# <a name="handling-exceptions-in-reporting-services"></a>Administrar las excepciones en Reporting Services
  Cuando una solicitud de cliente de la API SOAP de Reporting Services no puede completarse, el servidor de informes devuelve un error en lugar de los resultados esperados de la llamada. Cuando una llamada no puede completarse, un error para el servicio web del servidor de informes se devuelve como elemento XML **Fault** de SOAP. El elemento descriptivo clave del error es **detail**, que incluye toda la información de error proporcionada por el servidor de informes así como cualquier información de error adicional del servicio web. La información clave del elemento **detail** es el código de error del servidor de informes. Según el mensaje y el código de error, puede determinar la siguiente acción adecuada que llevar a cabo en las aplicaciones. Para obtener más información acerca de los errores de SOAP, vea el sitio web de World Wide Web Consortium (W3C) en http://www.w3.org/TR/SOAP.  
  
## <a name="soap-faults-and-the-net-framework"></a>Errores de SOAP y .NET Framework  
 En [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)], si se produce un error en una solicitud de cliente al servicio web, el servidor de informes comunica el error al código de cliente que llama al servicio web iniciando un objeto **SoapException**. **SoapException** ajusta la información contenida en un error de SOAP. La propiedad **Detail** de **SoapException** se asigna al elemento **detail** en el error de SOAP. Las aplicaciones deberían detectar el objeto **SoapException** con un bloque try/catch y utilizar la propiedad **Detail** de **SoapException** para tomar las medidas apropiadas. Para más información sobre la clase **SoapException** y la propiedad **Detail** en [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], vea [Clase SoapException de Reporting Services](soapexception-class/reporting-services-soapexception-class.md). Para más información sobre la clase **SoapException**, vea la documentación del SDK de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)].  
  
## <a name="see-also"></a>Vea también  
 [Propiedad Detail](soapexception-class/detail-property.md)   
 [Introducción a la administración de excepciones en Reporting Services](introducing-exception-handling-in-reporting-services.md)   
 [Clase SoapException de Reporting Services](soapexception-class/reporting-services-soapexception-class.md)  
  
  
