---
title: "Configuración de la información del dispositivo XML | Microsoft Docs"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- XML [Reporting Services], rendering
- device information settings [Reporting Services], PDF rendering
ms.assetid: a32e83fe-c10e-4ebd-8975-5be7dcc422e7
caps.latest.revision: "43"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 1264d292be499cf8c70efeea1ef39beed325cd5f
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2017
---
# <a name="xml-device-information-settings"></a>Configuración de la información del dispositivo XML
  En la tabla siguiente se muestra la configuración de la información de los dispositivos para la representación en formato XML.  
  
|Configuración|Valores|Detalles|  
|-------------|------------|-------------|  
|**XSLT**|Ruta de acceso en el espacio de nombres del servidor de informes de un XSLT que se aplicará al archivo XML, por ejemplo, **/Transforms/myxslt**.|El archivo xsl debe ser un recurso publicado en el servidor de informes y debe tener acceso a él a través de una ruta de acceso al elemento del servidor de informes. El valor de esta opción se aplica después de cualquier XSLT que se especifique en el informe. Si se ha aplicado la configuración **XSLT** , se ignora **OmitSchema** .|  
|**MIMEType**|Tipo de Extensiones multipropósito de correo Internet (MIME) del archivo XML.||  
|**UseFormattedValues**|**true**<br /><br /> **false**|Indica si representar el valor con formato de un cuadro de texto al generar los datos XML.<br /><br /> El valor false indica que se utiliza el valor subyacente del cuadro de texto.|  
|**Indented**|**true**<br /><br /> **false**|Indica si generar XML con sangría. El valor predeterminado ( **False** ) genera un XML comprimido sin sangría.|  
|**OmitNamespace**|**true**<br /><br /> **false**|Indica si se va a omitir el espacio de nombres predeterminado en el código XML.<br /><br /> Si es true, el código XML no especifica un espacio de nombres predeterminado.<br /><br /> Si es false, el código XML especifica un espacio de nombres predeterminado con el valor de la propiedad DataSchema del informe. El valor predeterminado de la propiedad DataSchema es el nombre del informe.<br /><br /> El valor predeterminado es**false**.|  
|**OmitSchema**|**true**<br /><br /> **false**|Indica si se va a omitir la ubicación del esquema en el código XML. La ubicación es el atributo SchemaLocation.<br /><br /> El valor predeterminado de OmitSchema depende del valor de OmitNamespace:<br /><br /> Si OmitNamespace = False, OmitSchema = **False** de manera predeterminada. El usuario puede invalidar el valor predeterminado si establece OmitSchema = True.<br /><br /> Si OmitNamespace = True, OmitSchema funcionará como **True** independientemente del valor que se haya configurado explícitamente para OmitSchema.|  
|**Codificación**|Nombre del organismo Internet Assigned Numbers Authority (IANA) de una codificación de caracteres que es compatible con .NET Framework.|El valor predeterminado es **UTF-8**. Entre los ejemplos de otros valores se incluyen ASCII, UTF-7 y UTF-16.|  
|**FileExtension**|Extensión de archivo que se va a utilizar para el archivo generado.||  
|**Esquema**|El valor **True** indica que se representa un esquema XML. El valor predeterminado es **false**.|Indica si se representa la definición del esquema XML (XSD) o si se representan los datos XML reales.|  
  
## <a name="see-also"></a>Vea también  
 <xref:ReportExecution2005.ReportExecutionService.Render%2A>   
 [Pasar la configuración de información de dispositivo a las extensiones de representación](../reporting-services/report-server-web-service/net-framework/passing-device-information-settings-to-rendering-extensions.md)   
 [Personalizar los parámetros de extensión de representación en RSReportServer.Config](../reporting-services/customize-rendering-extension-parameters-in-rsreportserver-config.md)   
 [Referencia técnica &#40;SSRS&#41;](../reporting-services/technical-reference-ssrs.md)  
  
  
