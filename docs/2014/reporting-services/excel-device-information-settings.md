---
title: Configuración de la información del dispositivo Excel | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- device information settings [Reporting Services], Excel rendering
- Excel [Reporting Services], rendering
ms.assetid: bb5f3566-f033-4470-be87-1f52fb7a4ab6
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: f9a7213b59e435f797609a7abb7fcd560c4890e5
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48116211"
---
# <a name="excel-device-information-settings"></a>Configuración de la información del dispositivo Excel
  En la tabla siguiente se muestra la configuración de la información de los dispositivos para la representación en formato de [!INCLUDE[ofprexcel](../includes/ofprexcel-md.md)] .  
  
|Parámetro|Valor|  
|-------------|-----------|  
|**OmitDocumentMap**|Indica si omitir el mapa del documento para los informes que lo admiten. El valor predeterminado es `false`.|  
|**OmitFormulas**|Indica si omitir las fórmulas del informe representado. El valor predeterminado es `false`.|  
|`SimplePageHeade`RS|Indica si el encabezado de página del informe se representa en el encabezado de página de Excel. Un valor de `false` indica que el encabezado de página se representa en la primera fila de la hoja de cálculo. El valor predeterminado es `false`.|  
  
## <a name="see-also"></a>Vea también  
 <xref:ReportExecution2005.ReportExecutionService.Render%2A>   
 [Pasar la configuración de información de dispositivo a las extensiones de representación](report-server-web-service/net-framework/passing-device-information-settings-to-rendering-extensions.md)   
 [Personalizar los parámetros de extensión de representación en RSReportServer.Config](customize-rendering-extension-parameters-in-rsreportserver-config.md)   
 [Referencia técnica &#40;SSRS&#41;](../../2014/reporting-services/technical-reference-ssrs.md)  
  
  
