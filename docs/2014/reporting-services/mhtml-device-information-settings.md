---
title: Configuración de la información del dispositivo MHTML | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- device information settings [Reporting Services], MHTML rendering
- MHTML [Reporting Services]
ms.assetid: 60b85dd8-b4fb-4ad9-be6a-e7c89ac076fe
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 196afebcabea54fda1b315b1c2f17c0029842f07
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/22/2019
ms.locfileid: "59949801"
---
# <a name="mhtml-device-information-settings"></a>Configuración de la información del dispositivo MHTML
  En la tabla siguiente se muestra una lista de la configuración de información de dispositivos para representar los informes en formato de archivo web (MHTML).  
  
|Parámetro|Valor|  
|-------------|-----------|  
|**JavaScript**|Indica si JavaScript se admite en el informe representado.|  
|**OutlookCompat**|Indica si la representación se va a realizar con metadatos adicionales que hacen que el informe tenga una apariencia mejorada en Outlook. El valor predeterminado es `true`.|  
|**Fragmento MHTML**|Indica si un fragmento MHTML se crea en lugar de un documento MHTML completo. Un fragmento MHTML incluye el contenido del informe en un elemento TABLE y omite los elementos BODY y HTML. El valor predeterminado es `false`.|  
|**DataVisualizationFitSizing**|Indica el comportamiento de ajuste para la visualización de datos cuando se esté dentro de un Tablix. Esto incluye un gráfico, un medidor y un mapa.<br /><br /> Los valores posibles son **Aproximado** y **Exacto**.<br /><br /> El valor predeterminado es **Aproximado**. Si se quita el valor de configuración del archivo **rsreportserver.config** , el comportamiento predeterminado es **Exacto**.<br /><br /> Si se habilita **Exacto** , podría afectar al rendimiento porque el procesamiento necesario para determinar el tamaño exacto puede tardar más tiempo.|  
  
## <a name="see-also"></a>Vea también  
 <xref:ReportExecution2005.ReportExecutionService.Render%2A>   
 [Pasar la configuración de información de dispositivo a las extensiones de representación](report-server-web-service/net-framework/passing-device-information-settings-to-rendering-extensions.md)   
 [Personalizar los parámetros de extensión de representación en RSReportServer.Config](customize-rendering-extension-parameters-in-rsreportserver-config.md)   
 [Referencia técnica &#40;SSRS&#41;](../../2014/reporting-services/technical-reference-ssrs.md)  
  
  
