---
title: Word Device Information Settings | Documentos de Microsoft
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
- Word [Reporting Services]
- device information settings [Reporting Services], Word
ms.assetid: 28146498-fae7-4b13-b47f-6ec05aa8e057
caps.latest.revision: 7
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 491940329df26ba67f447aacb6a32f5d6578c4a5
ms.contentlocale: es-es
ms.lasthandoff: 08/09/2017

---
# <a name="word-device-information-settings"></a>Configuración de la información del dispositivo web
  En la tabla siguiente se muestra la configuración de la información de los dispositivos para la representación en formato de [!INCLUDE[ofprword](../includes/ofprword-md.md)] .  
  
|Configuración|Value|  
|-------------|-----------|  
|**AutoFit**|**False**. AutoFit está establecido en **false** en cualquier tabla de Word.<br /><br /> **True**. AutoaFit está establecido en **true** en cada tabla de Word.<br /><br /> **Never**. Los valores de AutoFit no están establecidos en ninguna tabla de Word y el comportamiento revierte al predeterminado de Word.<br /><br /> **Default**. AutoFit se establece en las tablas que son más estrechas que el área física de dibujo (ancho de página física excepto los márgenes) por la página lógica.|  
|**ExpandToggles**|Indica si todos los elementos que se pueden alternar deberían representarse en su estado totalmente expandido. El valor predeterminado es **false**.|  
|**FixedPageWidth**|Indica si el ancho de página escrito en el archivo DOC crecerá para alojar el ancho de la página más grande en el cuerpo del informe. El valor predeterminado es **false**.|  
|**OmitHyperlinks**|Indica si omitir la acción Hyperlink en todos los elementos donde se establezca. El valor predeterminado es **False**.|  
|**OmitDrillthroughs**|Indica si omitir la acción de obtención de detalles en todos los elementos donde se establezca. El valor predeterminado es **False**.|  
  
## <a name="see-also"></a>Vea también  
 <xref:ReportExecution2005.ReportExecutionService.Render%2A>   
 [Pasar la configuración de información de dispositivo para las extensiones de representación](../reporting-services/report-server-web-service/net-framework/passing-device-information-settings-to-rendering-extensions.md)   
 [Personalizar los parámetros de extensión de representación en RSReportServer.Config](../reporting-services/customize-rendering-extension-parameters-in-rsreportserver-config.md)   
 [Referencia técnica de &#40; SSRS &#41;](../reporting-services/technical-reference-ssrs.md)  
  
  
