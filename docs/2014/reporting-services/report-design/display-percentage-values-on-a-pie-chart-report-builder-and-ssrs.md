---
title: Mostrar valores de porcentaje en un gráfico circular (Generador de informes y SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: eb905fc1-5235-4773-a27e-b07be9318be5
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 0853b168b4b7728ffe18e5562b84887205a7cdef
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48059061"
---
# <a name="display-percentage-values-on-a-pie-chart-report-builder-and-ssrs"></a>Mostrar valores de porcentaje en un gráfico circular (Generador de informes y SSRS)
  De forma predeterminada, las categorías se muestran en la leyenda para identificar cada valor. Si ha etiquetado el gráfico circular con etiquetas de categoría, es probable que le interese mostrar los porcentajes en la leyenda.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-display-percentage-values-as-labels-on-a-pie-chart"></a>Para mostrar los valores de porcentaje como etiquetas en un gráfico circular  
  
1.  Agregue un gráfico circular al informe. Para más información, vea [Agregar un gráfico a un informe &#40;Generador de informes y SSRS&#41;](add-a-chart-to-a-report-report-builder-and-ssrs.md).  
  
2.  En la superficie de diseño, haga clic con el botón derecho en gráfico circular y seleccione **Mostrar etiquetas de datos**. Las etiquetas de datos aparecerán dentro de cada sector del gráfico circular.  
  
3.  En la superficie de diseño, haga clic con el botón secundario en las etiquetas y seleccione **Propiedades de la etiqueta de la serie**. Aparece el cuadro de diálogo **Propiedades de la etiqueta de la serie** .  
  
4.  Tipo `#PERCENT` para el **etiquetar datos** opción.  
  
5.  (Opcional) Para especificar el número de posiciones decimales que se deben mostrar en la etiqueta, escriba "#PERCENT{P*n*}", donde *n* es el número de posiciones decimales que se deben mostrar. Por ejemplo, para no mostrar ninguna posición decimal, escriba "#PERCENT{P0}".  
  
### <a name="to-display-percentage-values-in-the-legend-of-a-pie-chart"></a>Para mostrar los valores de porcentaje en la leyenda de un gráfico circular  
  
1.  En la superficie de diseño, haga clic con el botón secundario en el gráfico circular y seleccione **Propiedades de la serie**. Aparece el cuadro de diálogo **Propiedades de la serie** .  
  
2.  En **leyenda**, tipo `#PERCENT` para el **texto de leyenda personalizado** propiedad.  
  
## <a name="see-also"></a>Vea también  
 [Los gráficos circulares &#40;generador de informes y SSRS&#41;](charts-report-builder-and-ssrs.md)   
 [Aplicar formato a la leyenda en un gráfico &#40;generador de informes y SSRS&#41;](chart-legend-formatting-report-builder.md)   
 [Punto de datos para mostrar las etiquetas fuera de un gráfico circular &#40;generador de informes y SSRS&#41;](display-data-point-labels-outside-a-pie-chart-report-builder-and-ssrs.md)   
 [Recopilar segmentos pequeños en un gráfico circular &#40;generador de informes y SSRS&#41;](collect-small-slices-on-a-pie-chart-report-builder-and-ssrs.md)  
  
  
