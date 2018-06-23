---
title: Agregar quiebres de escala a un gráfico (Generador de informes y SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 84d66436-ed62-4967-bbbd-b457593ee787
caps.latest.revision: 9
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: 587aede5ae1d53e1f6960f69b56d4b7d41945f40
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36199847"
---
# <a name="add-scale-breaks-to-a-chart-report-builder-and-ssrs"></a>Agregar quiebres de escala a un gráfico (Generador de informes y SSRS)
  Un quiebre de escala es una franja dibujada a través del área de trazado de un gráfico para hacer ver una interrupción en la continuidad entre los valores altos y bajos de un eje de valores (habitualmente, el eje Y o eje vertical). Use un quiebre de escala para mostrar dos intervalos definidos dentro de la misma área del gráfico.  
  
 ![Gráfico con quiebre de escala](../media/rs-multipledatarangeschart-scalebreak.gif "Gráfico con quiebre de escala")  
  
> [!NOTE]  
>  No puede especificar dónde se debe colocar un quiebre de escala en un gráfico. El gráfico utiliza sus propios cálculos basados en los valores del conjunto de datos para determinar si hay separación suficiente entre los intervalos de datos para dibujar un quiebre de escala en el eje de valores (eje Y) en tiempo de ejecución.  
  
 Un ejemplo de un gráfico con quiebres de escala está disponible como informe de ejemplo. Para más información acerca de cómo descargar este y otros informes de ejemplo, consulte el tema sobre [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)][informes de ejemplo del Generador de informes y el Diseñador de informes](http://go.microsoft.com/fwlink/?LinkId=198283).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-enable-scale-breaks-on-the-chart"></a>Para habilitar quiebres de escala en el gráfico  
  
1.  Haga clic con el botón derecho en el eje vertical y, después, haga clic en **Propiedades del eje**. Se abrirá el cuadro de diálogo **Propiedades del eje vertical** .  
  
2.  Active la casilla **Habilitar quiebres de escala** .  
  
### <a name="to-change-the-style-of-the-scale-break"></a>Para cambiar el estilo del quiebre de escala  
  
1.  Abra el panel de propiedades.  
  
2.  En la superficie de diseño, haga clic con el botón secundario en el eje Y del gráfico. Las propiedades para el objeto del eje Y (que, de forma predeterminada, se denomina Eje del gráfico) se muestran en el panel Propiedades.  
  
3.  En la sección **Scale** , expanda la propiedad ScaleBreakStyle.  
  
4.  Cambie los valores de las propiedades de ScaleBreakStyle, como BreakLineType y Spacing. Para más información sobre las propiedades de quiebres de escala, vea [Mostrar una serie con varios rangos de datos en un gráfico &#40;Generador de informes y SSRS&#41;](displaying-a-series-with-multiple-data-ranges-on-a-chart.md).  
  
## <a name="see-also"></a>Vea también  
 [Gráficos &#40;Generador de informes y SSRS&#41;](charts-report-builder-and-ssrs.md)   
 [Aplicar formato a un gráfico &#40;Generador de informes y SSRS&#41;](formatting-a-chart-report-builder-and-ssrs.md)   
 [Cuadro de diálogo de propiedades de eje, opciones del eje &#40;el generador de informes SSRS&#41;](../axis-properties-dialog-box-axis-options-report-builder-and-ssrs.md)  
  
  