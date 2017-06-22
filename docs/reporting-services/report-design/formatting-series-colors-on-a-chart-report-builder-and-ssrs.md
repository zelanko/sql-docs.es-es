---
title: "Aplicar formato a los colores de serie de un gráfico (generador de informes y SSRS) | Documentos de Microsoft"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- "10245"
- "10252"
- sql13.rtp.rptdesigner.serieslabelproperties.borders.f1
- sql13.rtp.rptdesigner.seriesproperties.borders.f1
ms.assetid: fe541501-cac5-47b1-b95f-c410db789190
caps.latest.revision: 8
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 711b648b41294d6c32530407b31aec8401db389c
ms.contentlocale: es-es
ms.lasthandoff: 06/22/2017

---
# <a name="formatting-series-colors-on-a-chart-report-builder-and-ssrs"></a>Aplicar formato a los colores de serie de un gráfico (Generador de informes y SSRS)
  Reporting Services proporciona varias paletas integradas para los gráficos, pero también se puede definir una paleta personalizada. De forma predeterminada, los gráficos usan la paleta de colores integrada **Pacific** para rellenar las series. Estos colores también aparecen en la leyenda. Cuando se agregan varias series al gráfico, este asigna un color a cada serie siguiendo el orden en el que se han definido los colores en la paleta.  
  
 Si hay más series que colores en la paleta, el gráfico comenzará a repetir los colores, por lo que podría darse el caso de que dos series tuvieran el mismo color. Esto suele ser habitual en los gráficos de formas, donde cada punto de datos tiene asignado un color de la paleta. Para evitar confusiones, defina una paleta personalizada que tenga como mínimo tantos colores como series hay en el gráfico.  
  
 Puede seleccionar una nueva paleta o definir una paleta personalizada en el panel de propiedades. Para más información, vea [Definir los colores de un gráfico mediante una paleta &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/define-colors-on-a-chart-using-a-palette-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="using-built-in-palettes"></a>Usar las paletas integradas  
 Reporting Services proporciona una lista de paletas integradas predefinidas que podrá usar para definir un conjunto de colores para las series del gráfico. Todas las paletas integradas contienen entre 10 y 16 valores de color. No es posible ampliar la paleta integrada e incluir en ella más colores; si necesita más de 16 colores, deberá definir una paleta personalizada.  
  
 Si va a imprimir un informe, conviene que use la paleta **Greyscale** . Esta paleta usa tonos de blanco y negro para representar cada serie del gráfico.  
  
 La paleta denominada Predeterminado se usó como paleta de gráfico predeterminada en versiones anteriores de Reporting Services. Se ha conservado con el mismo nombre por coherencia. Aunque la paleta predeterminada permite actualizar los gráficos a la perfección, una vez actualizados, puede que desee cambiar de paleta.  
  
## <a name="using-custom-palettes"></a>Usar las paletas personalizadas  
 Si desea aplicar sus propios colores al gráfico, use una paleta personalizada. Con una paleta personalizada, podrá agregar sus propios colores en el orden en que desea que aparezcan en el gráfico. Las paletas personalizadas son especialmente útiles si se desconoce el número de series del gráfico en tiempo de diseño. Para más información, vea [Definir los colores de un gráfico mediante una paleta &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/define-colors-on-a-chart-using-a-palette-report-builder-and-ssrs.md).  
  
## <a name="using-a-color-fill-on-each-series"></a>Usar un relleno en color para cada serie  
 También puede definir sus propios colores para el gráfico especificando un color para cada serie. Para ello, abra el cuadro de diálogo **Propiedades de la serie** y establezca la propiedad **Color** para **Relleno**. Esto invalidará todas las paletas definidas. Normalmente, es mejor usar una paleta personalizada para definir los colores porque el número de series del conjunto de datos no se suele conocer hasta que se procesa el informe.  
  
 Esta opción resulta más conveniente si se desea establecer los colores de la serie de forma condicional en función de una expresión.  Para más información, vea [Aplicar formato a los puntos de datos de un gráfico &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/formatting-data-points-on-a-chart-report-builder-and-ssrs.md).  
  
## <a name="in-this-section"></a>En esta sección  
 [Especificar colores coherentes en varios gráficos de formas &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/specify-consistent-colors-across-multiple-shape-charts-report-builder-and-ssrs.md)  
  
 [Definir los colores de un gráfico mediante una paleta &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/define-colors-on-a-chart-using-a-palette-report-builder-and-ssrs.md)  
  
 [Resaltar datos en el gráfico agregando franjas &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/highlight-chart-data-by-adding-strip-lines-report-builder-and-ssrs.md)  
  
## <a name="see-also"></a>Vea también  
 [Aplicar formato a un gráfico &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/formatting-a-chart-report-builder-and-ssrs.md)   
 [Agregar estilos con bisel, relieve y textura a un gráfico &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/chart-effects-add-bevel-emboss-or-texture-report-builder.md)   
 [Gráficos &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/charts-report-builder-and-ssrs.md)   
 [Aplicar formato a la leyenda de un gráfico &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/chart-legend-formatting-report-builder.md)  
  
  
