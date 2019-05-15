---
title: Configuración de la información del dispositivo PPTX | Microsoft Docs
ms.date: 09/11/2015
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
helpviewer_keywords:
- render
- powerpoint
- pptx
- export
ms.assetid: 4dc2045f-8025-41a3-8f9d-5635fb24cf4a
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 53f5e080a4ce654eb133aed340034e547f247737
ms.sourcegitcommit: e4794943ea6d2580174d42275185e58166984f8c
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 05/09/2019
ms.locfileid: "65503332"
---
# <a name="pptx-device-information-settings"></a>Configuración de la información del dispositivo PPTX
  En la tabla siguiente se muestra la configuración de la información de los dispositivos para representar informes de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] en formato PPTX.  
  
|Configuración|Valor|  
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
|**PageHeight**|El alto de la página, en pulgadas, que se va a establecer para el informe. Debe incluir un valor entero o decimal seguido de "in" (por ejemplo, **11in**). Este valor invalida la configuración original del informe.|  
|**PageWidth**|El ancho de la página, en pulgadas, que se va a establecer para el informe. Debe incluir un valor entero o decimal seguido de "in" (por ejemplo, **8,5in**). Este valor invalida la configuración original del informe.|  
|**StartPage**|Primera página del informe que se va a representar. El valor **0** indica que se representan todas las páginas. El valor predeterminado es **1**.|  
|**UseReportPageSize**|Si UseReportPageSize =**false**, el tamaño de diapositiva predeterminado es el valor predeterminado de PowerPoint de 13,333" x 7,5" (relación de aspecto 16:9). Si UseReportPageSize =true, el tamaño de diapositiva predeterminado es el tamaño de la página de definición del informe.<br /><br /> El valor predeterminado es **False**.<br /><br /> Nota: La configuración de PageWidth y de PageHeight invalida el ancho y alto predeterminados.|  
  
## <a name="see-also"></a>Consulte también  
 <xref:ReportExecution2005.ReportExecutionService.Render%2A>   
 [Pasar la configuración de información de dispositivo a las extensiones de representación](../reporting-services/report-server-web-service/net-framework/passing-device-information-settings-to-rendering-extensions.md)   
 [Personalizar los parámetros de extensión de representación en RSReportServer.Config](../reporting-services/customize-rendering-extension-parameters-in-rsreportserver-config.md)   
 [Referencia técnica &#40;SSRS&#41;](../reporting-services/technical-reference-ssrs.md)  
  
  
