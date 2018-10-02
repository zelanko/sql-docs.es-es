---
title: Mostrar las etiquetas de los puntos de datos fuera de un gráfico circular (Generador de informes y SSRS) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: 959b7574-cf43-470b-b592-4944d8a9948f
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 9a398224ce57aa31e11e2956a7caf40ee73499a1
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47631083"
---
# <a name="display-data-point-labels-outside-a-pie-chart-report-builder-and-ssrs"></a>Mostrar las etiquetas de los puntos de datos fuera de un gráfico circular (Generador de informes y SSRS)
  En [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], el etiquetado de los gráficos circulares está optimizado, por lo que las etiquetas se muestran solo en varios segmentos de datos. Si el gráfico circular contiene demasiados segmentos, las etiquetas se pueden superponer. Una solución consiste en mostrar las etiquetas fuera del gráfico circular, lo que puede crear más espacio para las etiquetas de datos más largas. Si las etiquetas siguen solapándose, habilite 3D para crear más espacio. Esto reduce el diámetro del gráfico circular, lo que crea más espacio alrededor del gráfico.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-display-data-point-labels-inside-a-pie-chart"></a>Para mostrar las etiquetas de los puntos de datos dentro de un gráfico circular  
  
1.  Agregue un gráfico circular al informe. Para más información, vea [Agregar un gráfico a un informe &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/add-a-chart-to-a-report-report-builder-and-ssrs.md).  
  
2.  En la superficie de diseño, haga clic con el botón derecho en el gráfico y seleccione **Mostrar etiquetas de datos**.  
  
### <a name="to-display-data-point-labels-outside-a-pie-chart"></a>Para mostrar las etiquetas de los puntos de datos fuera de un gráfico circular  
  
1.  Cree un gráfico circular y muestre las etiquetas de datos.  
  
2.  Abra el panel de propiedades.  
  
3.  En la superficie de diseño, haga clic en el propio gráfico para mostrar las propiedades **Category** en el panel de propiedades.  
  
4.  Expanda el nodo **CustomAttributes** . Se muestra una lista de atributos para el gráfico circular.  
  
5.  Establezca la propiedad **PieLabelStyle** en **Externa**.  
  
6.  Establezca la propiedad **PieLineColor** en **Negro**. La propiedad PieLineColor define las líneas de llamada para cada etiqueta de punto de datos.  
  
### <a name="to-prevent-overlapping-labels-displayed-outside-a-pie-chart"></a>Para evitar que las etiquetas mostradas fuera de un gráfico circular se superpongan  
  
1.  Cree un gráfico circular con etiquetas externas.  
  
2.  En la superficie de diseño, haga clic con el botón derecho fuera del gráfico circular pero dentro de los límites del gráfico y seleccione **Propiedades del área de gráfico**. Aparecerá el cuadro de diálogo **Propiedades del área de gráfico** .  
  
3.  En la pestaña **Opciones 3D** , seleccione **Habilitar 3D**.  
  
4.  Si quiere que el gráfico tenga más espacio para las etiquetas, pero que siga pareciendo bidimensional, establezca las propiedades **Rotation** e **Inclination** en **0**.  
  
## <a name="see-also"></a>Ver también  
 [Gráficos circulares &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/pie-charts-report-builder-and-ssrs.md)   
 [Recopilar segmentos pequeños en un gráfico circular &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/collect-small-slices-on-a-pie-chart-report-builder-and-ssrs.md)   
 [Mostrar valores de porcentaje en un gráfico circular &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/display-percentage-values-on-a-pie-chart-report-builder-and-ssrs.md)  
  
  
