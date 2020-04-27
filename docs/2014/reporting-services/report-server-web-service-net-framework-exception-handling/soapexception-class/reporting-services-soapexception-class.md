---
title: Clase SoapException de Reporting Services | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
helpviewer_keywords:
- exceptions [Reporting Services], SoapException class
- SoapException class
ms.assetid: 2cec49ee-20b1-40eb-a75b-0908d9c05b34
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 6f6efdfac89014116957990ef2db21cf52e76a4f
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "63046037"
---
# <a name="reporting-services-soapexception-class"></a>Clase SoapException de Reporting Services
  Debería solucionar cualquier error concreto de [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] que podría producirse. Por ejemplo, en una aplicación en la que pida al usuario que cree una carpeta, podría ser posible que el usuario intente crear una que ya exista. Como programador, no tiene control sobre lo que el usuario escribe en los campos de ruta de acceso y nombre de la carpeta de la aplicación, pero tiene puede controlar su experiencia cuando alguien intenta a propósito crear un elemento que ya existe.  
  
 Para facilitar la detección de condiciones de error concretas, [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] clasifica un código de error para la excepción y devuelve la clasificación del error utilizando las propiedades de la clase **SoapException**. Para obtener más información, vea "SoapException (clase) [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] " en la documentación del SDK.  
  
 En la siguiente tabla se muestran las propiedades públicas de la clase **SoapException**.  
  
|Propiedad pública|Descripción|  
|---------------------|-----------------|  
|**Actor**|Código que ha producido la excepción. El valor es la dirección URL del método de servicio web.|  
|**Detail**|Información de error específica de la aplicación. El servidor de informes establece el valor y está en formato XML. Para más información, vea [Propiedad Detail](detail-property.md) y [Usar la propiedad Detail para administrar errores concretos](../best-practices/using-the-detail-property-to-handle-specific-errors.md).|  
|**HelpLink**|Una dirección URL o URN a un archivo de Ayuda asociado al error. Normalmente, el servicio web establece el valor y una dirección URL a la Ayuda y soporte técnico de [!INCLUDE[msCoName](../../../includes/msconame-md.md)]. Dado que [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] admite varios vínculos de ayuda para los errores que se producen, el servidor de informes establece la información del vínculo de la ayuda como parte de la propiedad **Detail**. Para más información, vea [Elemento HelpLink](helplink-element.md).|  
|**Mensaje**|Mensaje descriptivo y localizado que describe el error. Este texto podría aparecer en la UI de la aplicación.|  
  
## <a name="see-also"></a>Consulte también  
 [Introducción al control de excepciones en Reporting Services](../introducing-exception-handling-in-reporting-services.md)   
 [Tabla de errores de SoapException](soapexception-errors-table.md)  
  
  
