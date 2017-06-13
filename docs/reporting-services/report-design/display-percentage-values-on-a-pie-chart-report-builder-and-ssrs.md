---
title: "Mostrar valores de porcentaje en un gráfico circular (generador de informes y SSRS) | Documentos de Microsoft"
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
ms.assetid: eb905fc1-5235-4773-a27e-b07be9318be5
caps.latest.revision: 9
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 6c0fdf9d1b694f2f6d49389e913d1c156ba77838
ms.contentlocale: es-es
ms.lasthandoff: 06/13/2017

---
# <a name="display-percentage-values-on-a-pie-chart-report-builder-and-ssrs"></a>Mostrar valores de porcentaje en un gráfico circular (Generador de informes y SSRS)
En [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] informes paginados, de forma predeterminada, la leyenda muestra las categorías. También puede ser conveniente porcentajes en la leyenda o los gráficos circulares a sí mismos.   

![report-builder-pie-chart-preview-percents](../../reporting-services/media/report-builder-pie-chart-preview-percents.png)

 El [Tutorial: agregar un gráfico circular al informe (generador de informes)](Tutorial:%20Add%20a%20Pie%20Chart%20to%20Your%20Report%20\(Report%20Builder\).md) se explica cómo agregar porcentajes para sectores del gráfico circular, si le gustaría pruebe esto con datos de ejemplo.
 
  
## <a name="to-display-percentage-values-as-labels-on-a-pie-chart"></a>Para mostrar los valores de porcentaje como etiquetas en un gráfico circular  
  
1.  Agregue un gráfico circular al informe. Para más información, vea [Agregar un gráfico a un informe &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/add-a-chart-to-a-report-report-builder-and-ssrs.md).  
  
2.  En la superficie de diseño, haga clic con el botón derecho en gráfico circular y seleccione **Mostrar etiquetas de datos**. Las etiquetas de datos aparecerán dentro de cada sector del gráfico circular.  
  
3.  En la superficie de diseño, haga clic con el botón secundario en las etiquetas y seleccione **Propiedades de la etiqueta de la serie**. Aparece el cuadro de diálogo **Propiedades de la etiqueta de la serie** .  
  
4.  Escriba **#PERCENT** para la opción **Datos de etiqueta** .  
  
5.  (Opcional) Para especificar cuántas posiciones decimales muestra la etiqueta, escriba "#PERCENT {P*n*}" donde  *n*  es el número de posiciones decimales que se van a mostrar. Por ejemplo, para no mostrar ninguna posición decimal, escriba "#PERCENT{P0}".  
  
## <a name="to-display-percentage-values-in-the-legend-of-a-pie-chart"></a>Para mostrar los valores de porcentaje en la leyenda de un gráfico circular  
  
1.  En la superficie de diseño, haga clic con el botón secundario en el gráfico circular y seleccione **Propiedades de la serie**. Aparece el cuadro de diálogo **Propiedades de la serie** .  
  
2.  En **Leyenda**, escriba **#PERCENT** para la propiedad **Texto de leyenda personalizado** .  
  
## <a name="see-also"></a>Vea también  
* [Tutorial: Agregar un gráfico circular al informe (generador de informes)](Tutorial:%20Add%20a%20Pie%20Chart%20to%20Your%20Report%20\(Report%20Builder\).md)
*  [Gráficos circulares &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/pie-charts-report-builder-and-ssrs.md)   
*  [Aplicar formato a la leyenda de un gráfico &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/chart-legend-formatting-report-builder.md)   
*  [Mostrar las etiquetas de los puntos de datos fuera de un gráfico circular &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/display-data-point-labels-outside-a-pie-chart-report-builder-and-ssrs.md)   
 
  
