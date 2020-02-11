---
title: Propiedad Detail | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
helpviewer_keywords:
- Detail property
- SoapException class
ms.assetid: c1ddaeb6-c540-49fa-b06e-b6359d377ee8
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 27d9d7ab4cd29c6eb0ea7ae1c6bddbe8c1b7ef06
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "63046011"
---
# <a name="detail-property"></a>Propiedad Detail
  La propiedad **Detail** de la clase SoapException[!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] ** de ** tiene la estructura XML siguiente:  
  
## <a name="elements"></a>Elementos  
 **Detail**  
 Elemento de nivel superior que contiene todos los demás elementos de detalle de error.  
  
 **ErrorCode**  
 Código de error específico de [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)].  
  
 **HttpStatus**  
 El código de estado HTTP.  
  
 **Mensaje**  
 Mensaje de error y código de error asignados por el servidor de informes.  
  
 **HelpLink**  
 Dirección URL del vínculo de Ayuda a un sitio web en el que se puede encontrar más información sobre el error. Para más información, vea [Elemento HelpLink](helplink-element.md).  
  
 **LinkID**  
 Identificador asignado al vínculo.  
  
 **ProductName**  
 Nombre del producto. El valor predeterminado es **Microsoft SQL Server Reporting Services**.  
  
 **ProductVersion**  
 Versión de [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]. La longitud máxima es de 15 caracteres. El formato del número de versión debería ser como sigue: 8.00.0xxx.00.  
  
 **ProductLocaleId**  
 Identificador de configuración regional o de idioma de la DLL INTL de la aplicación (por ejemplo, 0x41A).  
  
 **Identifica**  
 Sistema operativo en el que está instalado [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]. Los valores válidos incluyen **0** para un sistema operativo independiente, **1** para [!INCLUDE[win2kfamily](../../../includes/win2kfamily-md.md)] y **16** para Windows XP.  
  
 **CountryLocaleId**  
 Identificador de configuración regional o de idioma del sistema operativo. Por ejemplo, el valor correspondiente a la versión en francés de Windows es 0x040c.  
  
 **MoreInformation**  
 Cadena XML que contiene las excepciones anidadas que se produjeron mientras el método se ejecutaba.  
  
 **Origen**  
 Elemento secundario de **MoreInformation**. Origen del error.  
  
 **Mensaje**  
 Elemento secundario de **MoreInformation**. Mensaje de error de una excepción anidada. Este elemento incluye atributos XML para **ErrorCode** y **HelpLink**.  
  
 **Advertencias**  
 Cadena XML que contiene las advertencias que se devolvieron al procesar el informe.  
  
## <a name="see-also"></a>Consulte también  
 [Introducción a la administración de excepciones en Reporting Services](../introducing-exception-handling-in-reporting-services.md)   
 [Clase SoapException de Reporting Services](reporting-services-soapexception-class.md)   
 [Uso de la propiedad Detail para administrar errores concretos](../best-practices/using-the-detail-property-to-handle-specific-errors.md)  
  
  
