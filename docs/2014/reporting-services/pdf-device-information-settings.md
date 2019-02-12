---
title: Configuración de la información del dispositivo PDF | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- device information settings [Reporting Services], PDF rendering
- PDF [Reporting Services]
ms.assetid: 9a4aabe5-dbdc-4884-b999-1200983fee47
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 185b7c9119dbd5a6105152aadcf1241abc6b82ce
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/11/2019
ms.locfileid: "56025046"
---
# <a name="pdf-device-information-settings"></a>Configuración de la información del dispositivo PDF
  En la tabla siguiente se muestra la configuración de la información de los dispositivos para representar informes en formato PDF.  
  
|Parámetro|Valor|  
|-------------|-----------|  
|**Columnas**|Número de columnas que se van a establecer para el informe. Este valor invalida la configuración original del informe.|  
|**ColumnSpacing**|Espacio entre las columnas que se va a establecer para el informe. Este valor invalida la configuración original del informe.|  
|**DpiX**|La resolución del dispositivo de salida en la dirección de x.|  
|**DpiY**|La resolución del dispositivo de salida en la dirección de y.|  
|**EndPage**|Última página del informe que se va a representar. El valor predeterminado es el de `StartPage`.|  
|`HumanReadablePDF`|Indica si se debería comprimir el PDF que permite que el origen sea más legible. El valor predeterminado es `false.`|  
|**MarginBottom**|Valor del margen inferior, en pulgadas, que se va a establecer para el informe. Debe incluir un valor entero o un valor decimal seguido de "in" (por ejemplo, 1in). Este valor invalida la configuración original del informe.|  
|**MarginLeft**|El valor del margen izquierdo, en pulgadas, que se va a establecer para el informe. Debe incluir un valor entero o un valor decimal seguido de "in" (por ejemplo, 1in). Este valor invalida la configuración original del informe.|  
|**MarginRight**|El valor del margen derecho, en pulgadas, que se va a establecer para el informe. Debe incluir un valor entero o un valor decimal seguido de "in" (por ejemplo, 1in). Este valor invalida la configuración original del informe.|  
|**MarginTop**|El valor del margen superior, en pulgadas, que se va a establecer para el informe. Debe incluir un valor entero o un valor decimal seguido de "in" (por ejemplo, 1in). Este valor invalida la configuración original del informe.|  
|**PageHeight**|El alto de la página, en pulgadas, que se va a establecer para el informe. Debe incluir un valor entero o decimal seguido de "in" (por ejemplo, 11in). Este valor invalida la configuración original del informe.|  
|**PageWidth**|El ancho de la página, en pulgadas, que se va a establecer para el informe. Debe incluir un entero o el valor decimal seguido de "en" (por ejemplo, 8.5in). Este valor invalida la configuración original del informe.|  
|`StartPage`|Primera página del informe que se va a representar. El valor `0` indica que se representan todas las páginas. El valor predeterminado es `1`.|  
  
## <a name="see-also"></a>Vea también  
 [Pasar la configuración de información de dispositivo a las extensiones de representación](report-server-web-service/net-framework/passing-device-information-settings-to-rendering-extensions.md)   
 [Personalizar los parámetros de extensión de representación en RSReportServer.Config](customize-rendering-extension-parameters-in-rsreportserver-config.md)   
 [Referencia técnica &#40;SSRS&#41;](../../2014/reporting-services/technical-reference-ssrs.md)  
  
  
