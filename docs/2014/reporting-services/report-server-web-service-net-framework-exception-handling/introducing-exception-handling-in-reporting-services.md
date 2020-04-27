---
title: Introducción al control de excepciones en Reporting Services | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
helpviewer_keywords:
- Web service [Reporting Services], exception handling
- errors [Reporting Services]
- exceptions [Reporting Services]
- Report Server Web service, exception handling
- XML Web service [Reporting Services], exception handling
ms.assetid: 54381870-ce67-482b-aa83-6a838cdbf9b9
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 091b1f40d293515617e369b750a5f18dfe12951b
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "63012324"
---
# <a name="introducing-exception-handling-in-reporting-services"></a>Introducción a la administración de excepciones en Reporting Services
  Si una aplicación de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] envía una solicitud al servicio web del servidor de informes que el servicio no puede procesar, este devuelve una excepción SOAP al cliente. La administración de las excepciones iniciadas por el servicio web del servidor de informes constituye una parte importante de las aplicaciones que se desarrollan porque se puede devolver información útil a los usuarios cuando se producen errores.  
  
 Esta sección contiene información concreta sobre cómo administrar las excepciones, evitar los datos proporcionados por el usuario que no sean válidos y devolver información de errores significativa para los usuarios. Para obtener información general sobre el control de excepciones, vea "controlar y producir excepciones [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] " en la documentación del SDK de.  
  
## <a name="in-this-section"></a>En esta sección  
  
|Tema|Descripción|  
|-----------|-----------------|  
|[Administrar las excepciones en Reporting Services](handling-exceptions-in-reporting-services.md)|Proporciona información general sobre las excepciones en [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] y el rol de SOAP para devolver los errores de un servicio web.|  
|[Prácticas recomendadas para la administración de excepciones de Reporting Services](best-practices/best-practices-for-reporting-services-exception-handling.md)|Proporciona recomendaciones sobre cómo administrar las excepciones en [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].|  
|[Clase SoapException de Reporting Services](soapexception-class/reporting-services-soapexception-class.md)|Describe la clase **SoapException** en [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].|  
  
## <a name="see-also"></a>Consulte también  
 [Creación de aplicaciones con el servicio web y .NET Framework](../report-server-web-service/net-framework/building-applications-using-the-web-service-and-the-net-framework.md)  
  
  
