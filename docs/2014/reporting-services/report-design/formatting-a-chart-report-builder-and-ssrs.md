---
title: Aplicar formato a un gráfico (Generador de informes y SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- "10214"
- sql12.rtp.rptdesigner.calculatedseriesproperties.fill.f1
- sql12.rtp.rptdesigner.serieslabelproperties.fill.f1
- sql12.rtp.rptdesigner.legendproperties.fill.f1
- "10149"
- sql12.rtp.rptdesigner.seriesproperties.shadow.f1
- sql12.rtp.rptdesigner.seriesproperties.markers.f1
- "10255"
- sql12.rtp.rptdesigner.charttitleproperties.fill.f1
- "10154"
- "10170"
- "10173"
- sql12.rtp.rptdesigner.seriesproperties.fill.f1
- "10169"
- "10158"
- sql12.rtp.rptdesigner.chartareaproperties.fill.f1
- sql12.rtp.rptdesigner.charttitleproperties.shadow.f1
- "10246"
- "10150"
- sql12.rtp.rptdesigner.calculatedseriesproperties.borders.f1
- sql12.rtp.rptdesigner.chartproperties.fill.f1
- "10159"
- sql12.rtp.rptdesigner.majorgridlineproperties.gridlineoptions.f1
- "10160"
- sql12.rtp.rptdesigner.serieslabelproperties.font.f1
- "10182"
- "10163"
- "10164"
- "10253"
- "10216"
- "10171"
- "10257"
- sql12.rtp.rptdesigner.chartareaproperties.border.f1
- sql12.rtp.rptdesigner.calculatedseriesproperties.shadow.f1
- sql12.rtp.rptdesigner.chartproperties.border.f1
- sql12.rtp.rptdesigner.minorgridlineproperties.gridlineoptions.f1
- sql12.rtp.rptdesigner.chartareaproperties.shadow.f1
- sql12.rtp.rptdesigner.charttitleproperties.borders.f1
- sql12.rtp.rptdesigner.charttitleproperties.font.f1
- "10247"
ms.assetid: d3984300-c766-42f8-b7c4-863123d67c99
caps.latest.revision: 6
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: 0022ba1d4fcd107464db1af3e5852c25719fb2fe
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36113965"
---
# <a name="formatting-a-chart-report-builder-and-ssrs"></a>Aplicar formato a un gráfico (Generador de informes y SSRS)
  Después de definir los datos para el gráfico y su aspecto, puede aplicar formato para mejorar su aspecto general y resaltar los puntos de datos clave. Las opciones de formato más comunes se pueden modificar desde el cuadro de diálogo de propiedades; estas opciones se muestran al hacer clic con el botón secundario en un elemento de gráfico para ver su menú contextual. Cada elemento de gráfico dispone de su propio cuadro de diálogo. Para más información sobre los elementos de gráfico, vea [Gráficos &#40;Generador de informes y SSRS&#41;](charts-report-builder-and-ssrs.md).  
  
 Aunque todas las propiedades relacionadas con el gráfico se encuentran en el panel de propiedades, muchas de estas propiedades también se pueden establecer desde un cuadro de diálogo. Mientras da formato a la serie, puede usar atributos personalizados para especificar propiedades específicas de la serie (estos atributos solo se encuentran en la categoría de propiedades **CustomAttributes** , situada en el panel de propiedades).  
  
 Para dar formato al gráfico de forma eficaz con el menor número posible de pasos, cambie el estilo de borde, la paleta y el estilo de dibujo predeterminados. Estas tres características son las que posibilitan el cambio visual más notable en el gráfico. Los estilos de dibujo solo se pueden aplicar a los gráficos circulares, de anillos, de barras y de columnas.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="in-this-section"></a>En esta sección  
 [Aplicar formato a los colores de serie de un gráfico &#40;Generador de informes y SSRS&#41;](formatting-series-colors-on-a-chart-report-builder-and-ssrs.md)  
 Describe cómo se definen los colores con una paleta, cómo puede definir su propia paleta de colores, y cómo se definen los colores basándose en una expresión.  
  
 [Aplicar formato a las etiquetas de los ejes de un gráfico &#40;Generador de informes y SSRS&#41;](formatting-axis-labels-on-a-chart-report-builder-and-ssrs.md)  
 Describe cómo mostrar líneas de cuadrícula, marcas de graduación y títulos, y cómo dar formato a los números y a las fechas de la escala del eje.  
  
 [Aplicar formato a la leyenda de un gráfico &#40;Generador de informes y SSRS&#41;](chart-legend-formatting-report-builder.md)  
 Describe cómo volver a ordenar y a dar formato a los elementos de la leyenda del gráfico.  
  
 [Aplicar formato a los puntos de datos de un gráfico &#40;Generador de informes y SSRS&#41;](formatting-data-points-on-a-chart-report-builder-and-ssrs.md)  
 Describe cómo situar etiquetas de puntos de datos y cómo dar formato a los marcadores de los puntos de datos para cada serie del gráfico.  
  
 [Aplicar 3D, bisel y otros efectos a un gráfico &#40;Generador de informes y SSRS&#41;](chart-effects-3d-bevel-and-other-report-builder.md)  
 Describe varios efectos 3D que puede aplicar a un gráfico.  
  
 [Agregar un marco de borde a un gráfico &#40;Generador de informes y SSRS&#41;](add-a-border-frame-to-a-chart-report-builder-and-ssrs.md)  
 Explica cómo agregar un marco de borde a un gráfico.  
  
## <a name="see-also"></a>Vea también  
 [Gráficos &#40;Generador de informes y SSRS&#41;](charts-report-builder-and-ssrs.md)   
 [Agregar un marco de borde a un gráfico &#40;Generador de informes y SSRS&#41;](add-a-border-frame-to-a-chart-report-builder-and-ssrs.md)   
 [Definir los colores de un gráfico mediante una paleta &#40;Generador de informes y SSRS&#41;](define-colors-on-a-chart-using-a-palette-report-builder-and-ssrs.md)   
 [Agregar estilos con bisel, relieve y textura a un gráfico &#40;Generador de informes y SSRS&#41;](chart-effects-add-bevel-emboss-or-texture-report-builder.md)  
  
  