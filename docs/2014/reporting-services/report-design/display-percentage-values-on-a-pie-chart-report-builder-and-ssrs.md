---
title: Mostrar valores de porcentaje en un gráfico circular (Generador de informes y SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: eb905fc1-5235-4773-a27e-b07be9318be5
caps.latest.revision: 6
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: 744cfd4600c58d0c5f9508243e2635d108f7fd73
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36201091"
---
# <a name="display-percentage-values-on-a-pie-chart-report-builder-and-ssrs"></a>Mostrar valores de porcentaje en un gráfico circular (Generador de informes y SSRS)
  De forma predeterminada, las categorías se muestran en la leyenda para identificar cada valor. Si ha etiquetado el gráfico circular con etiquetas de categoría, es probable que le interese mostrar los porcentajes en la leyenda.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-display-percentage-values-as-labels-on-a-pie-chart"></a>Para mostrar los valores de porcentaje como etiquetas en un gráfico circular  
  
1.  Agregue un gráfico circular al informe. Para más información, vea [Agregar un gráfico a un informe &#40;Generador de informes y SSRS&#41;](add-a-chart-to-a-report-report-builder-and-ssrs.md).  
  
2.  En la superficie de diseño, haga clic con el botón derecho en gráfico circular y seleccione **Mostrar etiquetas de datos**. Las etiquetas de datos aparecerán dentro de cada sector del gráfico circular.  
  
3.  En la superficie de diseño, haga clic con el botón secundario en las etiquetas y seleccione **Propiedades de la etiqueta de la serie**. Aparece el cuadro de diálogo **Propiedades de la etiqueta de la serie** .  
  
4.  Tipo de `#PERCENT` para el **etiquetar los datos** opción.  
  
5.  (Opcional) Para especificar el número de posiciones decimales que se deben mostrar en la etiqueta, escriba "#PERCENT{P*n*}", donde *n* es el número de posiciones decimales que se deben mostrar. Por ejemplo, para no mostrar ninguna posición decimal, escriba "#PERCENT{P0}".  
  
### <a name="to-display-percentage-values-in-the-legend-of-a-pie-chart"></a>Para mostrar los valores de porcentaje en la leyenda de un gráfico circular  
  
1.  En la superficie de diseño, haga clic con el botón secundario en el gráfico circular y seleccione **Propiedades de la serie**. Aparece el cuadro de diálogo **Propiedades de la serie** .  
  
2.  En **leyenda**, tipo `#PERCENT` para el **texto de leyenda personalizado** propiedad.  
  
## <a name="see-also"></a>Vea también  
 [Los gráficos circulares &#40;el generador de informes SSRS&#41;](charts-report-builder-and-ssrs.md)   
 [Aplicar formato a la leyenda en un gráfico &#40;el generador de informes SSRS&#41;](chart-legend-formatting-report-builder.md)   
 [Las etiquetas de punto de datos de visualización fuera de un gráfico circular &#40;el generador de informes SSRS&#41;](display-data-point-labels-outside-a-pie-chart-report-builder-and-ssrs.md)   
 [Recopilar sectores pequeños en un gráfico circular &#40;el generador de informes SSRS&#41;](collect-small-slices-on-a-pie-chart-report-builder-and-ssrs.md)  
  
  