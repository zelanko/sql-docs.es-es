---
title: Configuración de la información del dispositivo de imagen | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- images [Reporting Services], rendering
- device information settings [Reporting Services], IMAGE rendering
ms.assetid: edad9498-69f7-4726-8699-fa615f704dff
caps.latest.revision: 40
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 17c7a8f084db4c252da7f235762a60078ef39214
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37315475"
---
# <a name="image-device-information-settings"></a>Configuración de la información del dispositivo de imagen
  En la tabla siguiente se muestra la configuración de la información de los dispositivos para la representación en formato IMAGE.  
  
|Configuración|Valor|  
|-------------|-----------|  
|**Columnas**|Número de columnas que se van a establecer para el informe. Este valor invalida la configuración original del informe.|  
|**ColumnSpacing**|Espacio entre las columnas que se va a establecer para el informe. Este valor invalida la configuración original del informe.|  
|`DpiX`|Resolución horizontal de la imagen de salida. El valor predeterminado es **96**. Se aplica a `BMP`, `GIF`, `PNG`, y `TIFF` formatos de salida.|  
|`DpiY`|Resolución vertical de la imagen de salida. El valor predeterminado es **96**. Se aplica a `BMP`, `GIF`, `PNG`, y `TIFF` formatos de salida.|  
|**EndPage**|Última página del informe que se va a representar. El valor predeterminado es el de `StartPage`.|  
|**MarginBottom**|Valor del margen inferior, en pulgadas, que se va a establecer para el informe. Debe incluir un valor entero o decimal seguido de "in" (por ejemplo, `1in`). Este valor invalida la configuración original del informe.|  
|**MarginLeft**|El valor del margen izquierdo, en pulgadas, que se va a establecer para el informe. Debe incluir un valor entero o decimal seguido de "in" (por ejemplo, `1in`). Este valor invalida la configuración original del informe.|  
|**MarginRight**|El valor del margen derecho, en pulgadas, que se va a establecer para el informe. Debe incluir un valor entero o decimal seguido de "in" (por ejemplo, `1in`). Este valor invalida la configuración original del informe.|  
|**MarginTop**|El valor del margen superior, en pulgadas, que se va a establecer para el informe. Debe incluir un valor entero o decimal seguido de "in" (por ejemplo, `1in`). Este valor invalida la configuración original del informe.|  
|**OutputFormat**|Uno de los [!INCLUDE[ndptecgdiexpanded](../includes/ndptecgdiexpanded-md.md)] ([!INCLUDE[ndptecgdi](../includes/ndptecgdi-md.md)]) admite los formatos de salida: `BMP`, `EMF`, `GIF`, `JPEG`, `PNG`, o `TIFF`.|  
|**PageHeight**|El alto de la página, en pulgadas, que se va a establecer para el informe. Debe incluir un valor entero o decimal seguido de "in" (por ejemplo, `11in`). Este valor invalida la configuración original del informe.|  
|**PageWidth**|El ancho de la página, en pulgadas, que se va a establecer para el informe. Debe incluir un valor entero o decimal seguido de "in" (por ejemplo, `8.5in`). Este valor invalida la configuración original del informe.|  
|**PrintDpiX**|Resolución horizontal de la imagen de salida. El valor predeterminado es `300`. Se aplica a metarchivo mejorado (`EMF`) formato de salida.|  
|**PrintDpiY**|Resolución vertical de la imagen de salida. El valor predeterminado es `300`. Se aplica a metarchivo mejorado (`EMF`) formato de salida.|  
|`StartPage`|Primera página del informe que se va a representar. El valor `0` indica que se representan todas las páginas. El valor predeterminado es `1`.|  
  
## <a name="see-also"></a>Vea también  
 [Pasar la configuración de información de dispositivo a las extensiones de representación](report-server-web-service/net-framework/passing-device-information-settings-to-rendering-extensions.md)   
 [Personalizar los parámetros de extensión de representación en RSReportServer.Config](customize-rendering-extension-parameters-in-rsreportserver-config.md)   
 [Referencia técnica &#40;SSRS&#41;](../../2014/reporting-services/technical-reference-ssrs.md)  
  
  
