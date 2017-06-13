---
title: "Configuración de información del dispositivo MHTML | Documentos de Microsoft"
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
- device information settings [Reporting Services], MHTML rendering
- MHTML [Reporting Services]
ms.assetid: 60b85dd8-b4fb-4ad9-be6a-e7c89ac076fe
caps.latest.revision: 39
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: c80135a9fa4f9cec547ffa3f837e7af37f4bf89a
ms.contentlocale: es-es
ms.lasthandoff: 06/13/2017

---
# <a name="mhtml-device-information-settings"></a>Configuración de la información del dispositivo MHTML
  En la tabla siguiente se muestra una lista de la configuración de información de dispositivos para representar los informes en formato de archivo web (MHTML).  
  
|Configuración|Value|  
|-------------|-----------|  
|**JavaScript**|Indica si JavaScript se admite en el informe representado.|  
|**OutlookCompat**|Indica si la representación se va a realizar con metadatos adicionales que hacen que el informe tenga una apariencia mejorada en Outlook. El valor predeterminado es **true**.|  
|**Fragmento MHTML**|Indica si un fragmento MHTML se crea en lugar de un documento MHTML completo. Un fragmento MHTML incluye el contenido del informe en un elemento TABLE y omite los elementos BODY y HTML. El valor predeterminado es **false**.|  
|**DataVisualizationFitSizing**|Indica el comportamiento de ajuste para la visualización de datos cuando se esté dentro de un Tablix. Esto incluye un gráfico, un medidor y un mapa.<br /><br /> Los valores posibles son **Aproximado** y **Exacto**.<br /><br /> El valor predeterminado es **Aproximado**. Si se quita el valor de configuración del archivo **rsreportserver.config** , el comportamiento predeterminado es **Exacto**.<br /><br /> Si se habilita **Exacto** , podría afectar al rendimiento porque el procesamiento necesario para determinar el tamaño exacto puede tardar más tiempo.|  
  
## <a name="see-also"></a>Vea también  
 <xref:ReportExecution2005.ReportExecutionService.Render%2A>   
 [Pasar la configuración de información de dispositivo a las extensiones de representación](../reporting-services/report-server-web-service/net-framework/passing-device-information-settings-to-rendering-extensions.md)   
 [Personalizar los parámetros de extensión de representación en RSReportServer.Config](../reporting-services/customize-rendering-extension-parameters-in-rsreportserver-config.md)   
 [Referencia técnica &#40;SSRS&#41;](../reporting-services/technical-reference-ssrs.md)  
  
  
