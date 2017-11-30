---
title: "Configuración de la información del dispositivo de imagen | Microsoft Docs"
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
- images [Reporting Services], rendering
- device information settings [Reporting Services], IMAGE rendering
ms.assetid: edad9498-69f7-4726-8699-fa615f704dff
caps.latest.revision: "39"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 130ae748ace51189f43da7e7c3c2a8b33a64857a
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2017
---
# <a name="image-device-information-settings"></a>Configuración de la información del dispositivo de imagen
  En la tabla siguiente se muestra la configuración de la información de los dispositivos para la representación en formato IMAGE.  
  
|Configuración|Value|  
|-------------|-----------|  
|**Columnas**|Número de columnas que se van a establecer para el informe. Este valor invalida la configuración original del informe.|  
|**ColumnSpacing**|Espacio entre las columnas que se va a establecer para el informe. Este valor invalida la configuración original del informe.|  
|**DpiX**|Resolución horizontal de la imagen de salida. El valor predeterminado es **96**. Se aplica a los formatos de salida **BMP**, **GIF**, **PNG**y **TIFF** .|  
|**DpiY**|Resolución vertical de la imagen de salida. El valor predeterminado es **96**. Se aplica a los formatos de salida **BMP**, **GIF**, **PNG**y **TIFF** .|  
|**EndPage**|Última página del informe que se va a representar. El valor predeterminado es el de **StartPage**.|  
|**MarginBottom**|Valor del margen inferior, en pulgadas, que se va a establecer para el informe. Debe incluir un valor entero o decimal seguido de "in" (por ejemplo, **1in**). Este valor invalida la configuración original del informe.|  
|**MarginLeft**|El valor del margen izquierdo, en pulgadas, que se va a establecer para el informe. Debe incluir un valor entero o decimal seguido de "in" (por ejemplo, **1in**). Este valor invalida la configuración original del informe.|  
|**MarginRight**|El valor del margen derecho, en pulgadas, que se va a establecer para el informe. Debe incluir un valor entero o decimal seguido de "in" (por ejemplo, **1in**). Este valor invalida la configuración original del informe.|  
|**MarginTop**|El valor del margen superior, en pulgadas, que se va a establecer para el informe. Debe incluir un valor entero o decimal seguido de "in" (por ejemplo, **1in**). Este valor invalida la configuración original del informe.|  
|**OutputFormat**|Uno de los formatos de salida compatibles con [!INCLUDE[ndptecgdiexpanded](../includes/ndptecgdiexpanded-md.md)] ([!INCLUDE[ndptecgdi](../includes/ndptecgdi-md.md)]): **BMP**, **EMF**, **GIF**, **JPEG**, **PNG**o **TIFF**.|  
|**PageHeight**|El alto de la página, en pulgadas, que se va a establecer para el informe. Debe incluir un valor entero o decimal seguido de "in" (por ejemplo, **11in**). Este valor invalida la configuración original del informe.|  
|**PageWidth**|El ancho de la página, en pulgadas, que se va a establecer para el informe. Debe incluir un valor entero o decimal seguido de "in" (por ejemplo, **8,5in**). Este valor invalida la configuración original del informe.|  
|**PrintDpiX**|Resolución horizontal de la imagen de salida. El valor predeterminado es **300**. Se aplica al formato de salida de metarchivo mejorado (**EMF**).|  
|**PrintDpiY**|Resolución vertical de la imagen de salida. El valor predeterminado es **300**. Se aplica al formato de salida de metarchivo mejorado (**EMF**).|  
|**StartPage**|Primera página del informe que se va a representar. El valor **0** indica que se representan todas las páginas. El valor predeterminado es **1**.|  
  
## <a name="see-also"></a>Vea también  
 <xref:ReportExecution2005.ReportExecutionService.Render%2A>   
 [Pasar la configuración de información de dispositivo a las extensiones de representación](../reporting-services/report-server-web-service/net-framework/passing-device-information-settings-to-rendering-extensions.md)   
 [Personalizar los parámetros de extensión de representación en RSReportServer.Config](../reporting-services/customize-rendering-extension-parameters-in-rsreportserver-config.md)   
 [Referencia técnica &#40;SSRS&#41;](../reporting-services/technical-reference-ssrs.md)  
  
  
