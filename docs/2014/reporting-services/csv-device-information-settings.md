---
title: Configuración de la información del dispositivo CSV | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- CSV [Reporting Services]
- device information settings [Reporting Services], CSV rendering
ms.assetid: f96f83a6-50bc-48ce-9fcd-fd9e1952d40a
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 123afc28db147118d10a66199364ca8b73afb34c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63265404"
---
# <a name="csv-device-information-settings"></a>Configuración de la información del dispositivo CSV
  La configuración de la información de dispositivo para la extensión de representación CSV permite cambiar los delimitadores y certificadores, y controlar el salto de línea que se va a especificar. También se puede enviar la extensión del archivo, así como la codificación e inclusión de filas de encabezado en la salida. Dado que es probable que los delimitadores sean caracteres especiales, debería codificarlos en una sección CDATA, si la configuración se escribe como XML.  
  
 En la tabla siguiente se muestra la configuración de la información de los dispositivos para la representación en formato de texto.  
  
|Parámetro|Valor|  
|-------------|-----------|  
|`Encoding`|Nombre del organismo Internet Assigned Numbers Authority (IANA) de una codificación de caracteres que es compatible con .NET Framework. El valor predeterminado es `UTF-8`. Entre los ejemplos de otros valores se incluyen ASCII, UTF-7 y UTF-16.|  
|`ExcelMode`|Especifica que la salida de destino es para Excel. El valor predeterminado es `true`.|  
|`FieldDelimiter`|La cadena de delimitación para colocar el resultado. El valor predeterminado es una coma (,). Debería codificar como URL el valor de esta información de dispositivo al pasarla en una dirección URL. Por ejemplo, un carácter de tabulación como delimitador debería ser "%09".<br /><br /> Puede cambiar el delimitador de campo predeterminado por cualquier carácter que desee, incluido TAB; para ello, solo tiene que cambiar la configuración de la información del dispositivo en el archivo de configuración. Por ejemplo, para usar TAB, actualice el valor FieldDelimiter a \<FieldDelimiter xml:space="preserve">[TAB]\</FieldDelimiter><br /><br /> En el ejemplo, [TAB] es un carácter de tabulación real, que significa que el espacio en blanco aparece en el archivo de configuración. El atributo "xml:space" indica a los analizadores que conserven el espacio en blanco.|  
|`FileExtension`|Extensión de archivo donde colocar el resultado. El valor predeterminado es `.CSV`. Si se especifican tanto `FileExtension` como `Extension`, `FileExtension` tendrá prioridad.|  
|**NoHeader**|Indica si la fila de encabezado se excluye de la salida. El valor predeterminado es `false`.|  
|`Qualifier`|Cadena del certificador donde colocar los resultados que contienen el delimitador de campo o de registro. Si los resultados contienen el certificador, este se repite. El valor `Qualifier` debe ser diferente de los valores `FieldDelimiter` y `RecordDelimiter`. El valor predeterminado es la comilla (").|  
|`RecordDelimiter`|El delimitador de registros que colocar al final de cada registro. El valor predeterminado es \<cr>\<lf>.|  
|**SuppressLineBreaks**|Indica si los saltos de línea se quitan de los datos incluidos en la salida. El valor predeterminado es `false`. Si el valor es `true`, `FieldDelimiter`, los valores `RecordDelimiter` y `Qualifier` no pueden ser un carácter de espacio en blanco.|  
|`UseFormattedValues`|Indica si las cadenas con formato se colocan en la salida CSV. El valor predeterminado es `true` cuando `ExcelMode` es `true`; de lo contrario es `false`.|  
  
## <a name="see-also"></a>Vea también  
 <xref:ReportExecution2005.ReportExecutionService.Render%2A>   
 [Pasar la configuración de información de dispositivo a las extensiones de representación](report-server-web-service/net-framework/passing-device-information-settings-to-rendering-extensions.md)   
 [Personalizar los parámetros de extensión de representación en RSReportServer.Config](customize-rendering-extension-parameters-in-rsreportserver-config.md)   
 [Referencia técnica &#40;SSRS&#41;](../../2014/reporting-services/technical-reference-ssrs.md)  
  
  
