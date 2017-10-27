---
title: "Mostrar información sobre herramientas en una serie (generador de informes y SSRS) | Documentos de Microsoft"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 4c9606ff-e1c3-4cf7-a4e7-bb16f1a9e8ab
caps.latest.revision: 8
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 5e963b234c5c3babb4dd2302afca2ca06ac249b1
ms.contentlocale: es-es
ms.lasthandoff: 08/09/2017

---
# <a name="show-tooltips-on-a-series-report-builder-and-ssrs"></a>Mostrar la información sobre herramientas en una serie (Generador de informes y SSRS)
  Puede agregar una información sobre herramientas a cada uno de los puntos de datos de la serie de un gráfico para mostrar información relacionada con el punto de datos, como el nombre del grupo, el valor del punto de datos o el porcentaje del punto de datos en relación con el total de la serie. Cuando los usuarios mantengan el mouse sobre el punto de datos en un informe paginado representado, verán esta información.  
  
 No se puede agregar una información sobre herramientas a una serie calculada.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="to-specify-a-tooltip-on-each-data-point"></a>Para especificar una información sobre herramientas en cada punto de datos  
  
1.  Haga clic con el botón derecho en la serie o en el campo del área **Valores** y seleccione **Propiedades de la serie**.  
  
2.  Haga clic en **Datos de las series** y, para la propiedad **ToolTip** , escriba una cadena o una expresión. Puede usar cualquier palabra clave específica del gráfico para representar otro elemento del gráfico. Para más información, vea [Aplicar formato a los puntos de datos de un gráfico &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/formatting-data-points-on-a-chart-report-builder-and-ssrs.md).  
  
## <a name="see-also"></a>Vea también  
 [Aplicar formato a los puntos de datos de un gráfico &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/formatting-data-points-on-a-chart-report-builder-and-ssrs.md)   
 [Cambiar el texto de un elemento de leyenda &#40; El generador de informes y SSRS &#41;](../../reporting-services/report-design/chart-legend-change-item-text-report-builder.md)   
 [Aplicar formato a los colores de serie en un gráfico de &#40; El generador de informes y SSRS &#41;](../../reporting-services/report-design/formatting-series-colors-on-a-chart-report-builder-and-ssrs.md)   
 [Agregar una acción de obtención de detalles en un informe &#40; El generador de informes y SSRS &#41;](../../reporting-services/report-design/add-a-drillthrough-action-on-a-report-report-builder-and-ssrs.md)  
  
  

