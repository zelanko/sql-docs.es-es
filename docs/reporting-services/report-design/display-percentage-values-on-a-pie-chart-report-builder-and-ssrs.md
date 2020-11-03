---
title: Visualización de valores de porcentaje en un gráfico circular (Generador de informes) | Microsoft Docs
description: Obtenga información sobre cómo mostrar valores de porcentaje en un gráfico circular, en la leyenda o en los sectores de un gráfico circular en el Generador de informes.
ms.date: 12/09/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: eb905fc1-5235-4773-a27e-b07be9318be5
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 6068c871bd96908e501c552e0388050aedfa47bf
ms.sourcegitcommit: ea0bf89617e11afe85ad85309e0ec731ed265583
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/28/2020
ms.locfileid: "92907233"
---
# <a name="display-percentage-values-on-a-pie-chart-report-builder-and-ssrs"></a>Mostrar valores de porcentaje en un gráfico circular (Generador de informes y SSRS)
En informes paginados de [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)], de forma predeterminada, la leyenda muestra las categorías. Es posible que también quiera ver porcentajes en la leyenda o los propios segmentos del gráfico circular.   

![Captura de pantalla de un gráfico circular que muestra los porcentajes de sus segmentos.](../../reporting-services/media/report-builder-pie-chart-preview-percents.png)

 El [Tutorial: Agregar un gráfico circular a un informe (Generador de informes)](../tutorial-add-a-pie-chart-to-your-report-report-builder.md) le guía a lo largo del proceso de adición de porcentajes a segmentos del gráfico circular, si primero quiere probar esto con datos de ejemplo.
 
  
## <a name="to-display-percentage-values-as-labels-on-a-pie-chart"></a>Para mostrar los valores de porcentaje como etiquetas en un gráfico circular  
  
1.  Agregue un gráfico circular al informe. Para más información, vea [Agregar un gráfico a un informe &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/add-a-chart-to-a-report-report-builder-and-ssrs.md).  
  
2.  En la superficie de diseño, haga clic con el botón derecho en gráfico circular y seleccione **Mostrar etiquetas de datos**. Las etiquetas de datos aparecerán dentro de cada sector del gráfico circular.  
  
3.  En la superficie de diseño, haga clic con el botón secundario en las etiquetas y seleccione **Propiedades de la etiqueta de la serie**. Aparece el cuadro de diálogo **Propiedades de la etiqueta de la serie** .  
  
4.  Escriba **#PERCENT** para la opción **Datos de etiqueta** .  
  
5.  (Opcional) Para especificar el número de posiciones decimales que se deben mostrar en la etiqueta, escriba "#PERCENT{P *n* }", donde *n* es el número de posiciones decimales que se deben mostrar. Por ejemplo, para no mostrar ninguna posición decimal, escriba "#PERCENT{P0}".  
  
## <a name="to-display-percentage-values-in-the-legend-of-a-pie-chart"></a>Para mostrar los valores de porcentaje en la leyenda de un gráfico circular  
  
1.  En la superficie de diseño, haga clic con el botón secundario en el gráfico circular y seleccione **Propiedades de la serie**. Aparece el cuadro de diálogo **Propiedades de la serie** .  
  
2.  En **Leyenda** , escriba **#PERCENT** para la propiedad **Texto de leyenda personalizado** .  
  
## <a name="see-also"></a>Consulte también  
* [Tutorial: Agregar un gráfico circular a un informe (generador de informes)](../tutorial-add-a-pie-chart-to-your-report-report-builder.md)
*  [Gráficos circulares &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/pie-charts-report-builder-and-ssrs.md)   
*  [Aplicar formato a la leyenda de un gráfico &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/chart-legend-formatting-report-builder.md)   
*  [Mostrar las etiquetas de los puntos de datos fuera de un gráfico circular &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/display-data-point-labels-outside-a-pie-chart-report-builder-and-ssrs.md)   
 
  
