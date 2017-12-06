---
title: Clase SoapException de Reporting Services | Microsoft Docs
ms.custom: 
ms.date: 03/16/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.service: 
ms.component: report-server-web-service-net-framework-exception-handling
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- exceptions [Reporting Services], SoapException class
- SoapException class
ms.assetid: 2cec49ee-20b1-40eb-a75b-0908d9c05b34
caps.latest.revision: "33"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: d7b2e5015be3a9044469057b1ff498ddc09f42e8
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/05/2017
---
# <a name="reporting-services-soapexception-class"></a>Clase SoapException de Reporting Services
  Debería solucionar cualquier error concreto de [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] que podría producirse. Por ejemplo, en una aplicación en la que pida al usuario que cree una carpeta, podría ser posible que el usuario intente crear una que ya exista. Como programador, no tiene control sobre lo que el usuario escribe en los campos de ruta de acceso y nombre de la carpeta de la aplicación, pero tiene puede controlar su experiencia cuando alguien intenta a propósito crear un elemento que ya existe.  
  
 Para facilitar la detección de condiciones de error concretas, [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] clasifica un código de error para la excepción y devuelve la clasificación del error utilizando las propiedades de la clase **SoapException**. Para más información, vea "Clase SoapException" en la documentación del SDK de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)].  
  
 En la siguiente tabla se muestran las propiedades públicas de la clase **SoapException**.  
  
|Propiedad pública|Description|  
|---------------------|-----------------|  
|**Actor**|Código que ha producido la excepción. El valor es la dirección URL del método de servicio web.|  
|**Detail**|Información de error específica de la aplicación. El servidor de informes establece el valor y está en formato XML. Para más información, vea [Propiedad Detail](../../../reporting-services/report-server-web-service-net-framework-exception-handling/soapexception-class/detail-property.md) y [Usar la propiedad Detail para administrar errores concretos](../../../reporting-services/report-server-web-service-net-framework-exception-handling/best-practices/using-the-detail-property-to-handle-specific-errors.md).|  
|**HelpLink**|Una dirección URL o URN a un archivo de Ayuda asociado al error. Normalmente, el servicio web establece el valor y una dirección URL a la Ayuda y soporte técnico de [!INCLUDE[msCoName](../../../includes/msconame-md.md)]. Dado que [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] admite varios vínculos de ayuda para los errores que se producen, el servidor de informes establece la información del vínculo de la ayuda como parte de la propiedad **Detail**. Para más información, vea [Elemento HelpLink](../../../reporting-services/report-server-web-service-net-framework-exception-handling/soapexception-class/helplink-element.md).|  
|**de mensaje**|Mensaje descriptivo y localizado que describe el error. Este texto podría aparecer en la UI de la aplicación.|  
  
## <a name="see-also"></a>Vea también  
 [Introducción a la administración de excepciones en Reporting Services](../../../reporting-services/report-server-web-service-net-framework-exception-handling/introducing-exception-handling-in-reporting-services.md)   
 [Tabla de errores de SoapException](../../../reporting-services/report-server-web-service-net-framework-exception-handling/soapexception-class/soapexception-errors-table.md)  
  
  
