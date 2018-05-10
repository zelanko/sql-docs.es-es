---
title: Introducción al control de excepciones en Reporting Services | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.component: report-server-web-service-net-framework-exception-handling
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- Web service [Reporting Services], exception handling
- errors [Reporting Services]
- exceptions [Reporting Services]
- Report Server Web service, exception handling
- XML Web service [Reporting Services], exception handling
ms.assetid: 54381870-ce67-482b-aa83-6a838cdbf9b9
caps.latest.revision: 29
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 589a7350778afea966db0ce7754ad196ed28fc5f
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="introducing-exception-handling-in-reporting-services"></a>Introducción a la administración de excepciones en Reporting Services
  Si una aplicación de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] envía una solicitud al servicio web del servidor de informes que el servicio no puede procesar, este devuelve una excepción SOAP al cliente. La administración de las excepciones iniciadas por el servicio web del servidor de informes constituye una parte importante de las aplicaciones que se desarrollan porque se puede devolver información útil a los usuarios cuando se producen errores.  
  
 Esta sección contiene información concreta sobre cómo administrar las excepciones, evitar los datos proporcionados por el usuario que no sean válidos y devolver información de errores significativa para los usuarios. Para información general sobre el tratamiento de excepciones, vea los temas que tratan sobre la administración y el inicio de excepciones en la documentación del SDK de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)].  
  
## <a name="in-this-section"></a>En esta sección  
  
|Tema|Description|  
|-----------|-----------------|  
|[Administración de las excepciones en Reporting Services](../../reporting-services/report-server-web-service-net-framework-exception-handling/handling-exceptions-in-reporting-services.md)|Proporciona información general sobre las excepciones en [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] y el rol de SOAP para devolver los errores de un servicio web.|  
|[Procedimientos recomendados para el control de excepciones de Reporting Services](../../reporting-services/report-server-web-service-net-framework-exception-handling/best-practices/best-practices-for-reporting-services-exception-handling.md)|Proporciona recomendaciones sobre cómo administrar las excepciones en [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].|  
|[Clase SoapException de Reporting Services](../../reporting-services/report-server-web-service-net-framework-exception-handling/soapexception-class/reporting-services-soapexception-class.md)|Describe la clase **SoapException** en [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].|  
  
## <a name="see-also"></a>Ver también  
 [Creación de aplicaciones con el servicio web y .NET Framework](../../reporting-services/report-server-web-service/net-framework/building-applications-using-the-web-service-and-the-net-framework.md)  
  
  
