---
title: Configuración de la información del dispositivo XML | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- XML [Reporting Services], rendering
- device information settings [Reporting Services], PDF rendering
ms.assetid: a32e83fe-c10e-4ebd-8975-5be7dcc422e7
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 404ab37f00cd738e619286a3133b906acbbcd06d
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63206248"
---
# <a name="xml-device-information-settings"></a>Configuración de la información del dispositivo XML
  En la tabla siguiente se muestra la configuración de la información de los dispositivos para la representación en formato XML.  
  
|Parámetro|Valor|  
|-------------|-----------|  
|`XSLT`|Ruta de acceso en el espacio de nombres del servidor de informes de un XSLT que se aplicará al archivo XML, por ejemplo `/Transforms/myxslt`. El archivo xsl debe ser un recurso publicado en el servidor de informes y debe tener acceso a él a través de una ruta de acceso al elemento del servidor de informes. El valor de esta opción se aplica después de cualquier XSLT que se especifique en el informe. Si se aplica el valor `XSLT`, se omite el valor `OmitSchema`.|  
|**MIMEType**|Tipo de Extensiones multipropósito de correo Internet (MIME) del archivo XML.|  
|**UseFormattedValues**|Indica si representar el valor con formato de un cuadro de texto al generar los datos XML. El valor false indica que se utiliza el valor subyacente del cuadro de texto.|  
|**Indented**|Indica si generar XML con sangría. El valor predeterminado de `false` genera XML comprimido sin sangría.|  
|`OmitNamespace`|Indica si se va a omitir el espacio de nombres predeterminado en el código XML.<br /><br /> Si es true, el código XML no especifica un espacio de nombres predeterminado.<br /><br /> Si es false, el código XML especifica un espacio de nombres predeterminado con el valor de la propiedad DataSchema del informe. El valor predeterminado de la propiedad DataSchema es el nombre del informe.<br /><br /> El valor predeterminado es `false`.|  
|`OmitSchema`|Indica si se va a omitir la ubicación del esquema en el código XML. La ubicación es el atributo SchemaLocation. El valor predeterminado de OmitSchema depende del valor de OmitNamespace:<br /><br /> Si OmitNamespace = False, OmitSchema = `False` de forma predeterminada. El usuario puede invalidar el valor predeterminado si establece OmitSchema = True.<br /><br /> Si OmitNamespace = True, OmitSchema funcionará como `True` independientemente del valor que se haya configurado explícitamente para OmitSchema.|  
|**Codificación**|Nombre del organismo Internet Assigned Numbers Authority (IANA) de una codificación de caracteres que es compatible con .NET Framework. El valor predeterminado es `UTF-8`. Entre los ejemplos de otros valores se incluyen ASCII, UTF-7 y UTF-16.|  
|**FileExtension**|Extensión de archivo que se va a utilizar para el archivo generado.|  
|**Esquema**|Indica si se representa la definición del esquema XML (XSD) o si se representan los datos XML reales. El valor `true` indica que se representa un esquema XML. El valor predeterminado es `false`.|  
  
## <a name="see-also"></a>Vea también  
 <xref:ReportExecution2005.ReportExecutionService.Render%2A>   
 [Pasar la configuración de información de dispositivo a las extensiones de representación](report-server-web-service/net-framework/passing-device-information-settings-to-rendering-extensions.md)   
 [Personalizar los parámetros de extensión de representación en RSReportServer.Config](customize-rendering-extension-parameters-in-rsreportserver-config.md)   
 [Referencia técnica &#40;SSRS&#41;](../../2014/reporting-services/technical-reference-ssrs.md)  
  
  
