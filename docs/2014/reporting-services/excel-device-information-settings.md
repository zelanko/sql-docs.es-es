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
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 5d1ec9b650592be41c8ae2f7043649c91ea78442
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/22/2019
ms.locfileid: "59948331"
---
# <a name="excel-device-information-settings"></a>Configuración de la información del dispositivo Excel
  En la tabla siguiente se muestra la configuración de la información de los dispositivos para la representación en formato de [!INCLUDE[ofprexcel](../includes/ofprexcel-md.md)] .  
  
|Parámetro|Valor|  
|-------------|-----------|  
|**OmitDocumentMap**|Indica si omitir el mapa del documento para los informes que lo admiten. El valor predeterminado es `false`.|  
|**OmitFormulas**|Indica si omitir las fórmulas del informe representado. El valor predeterminado es `false`.|  
|`SimplePageHeade`rs|Indica si el encabezado de página del informe se representa en el encabezado de página de Excel. El valor `false` indica que el encabezado de página se representa en la primera fila de la hoja de cálculo. El valor predeterminado es `false`.|  
  
## <a name="see-also"></a>Vea también  
 <xref:ReportExecution2005.ReportExecutionService.Render%2A>   
 [Pasar la configuración de información de dispositivo a las extensiones de representación](report-server-web-service/net-framework/passing-device-information-settings-to-rendering-extensions.md)   
 [Personalizar los parámetros de extensión de representación en RSReportServer.Config](customize-rendering-extension-parameters-in-rsreportserver-config.md)   
 [Referencia técnica &#40;SSRS&#41;](../../2014/reporting-services/technical-reference-ssrs.md)  
  
  
