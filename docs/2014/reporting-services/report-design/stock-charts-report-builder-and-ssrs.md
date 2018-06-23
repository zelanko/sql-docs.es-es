---
title: Gráficos de cotizaciones (Generador de informes y SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: f75ca11e-b7f5-4ac0-ba17-fe6f82742dad
caps.latest.revision: 7
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: 8ea218a0b7b201d929fd03a1a208a2eb6019ebb2
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36107812"
---
# <a name="stock-charts-report-builder-and-ssrs"></a>Gráficos de cotizaciones (Generador de informes y SSRS)
  Los gráficos de cotizaciones están diseñados específicamente para datos financieros o científicos que usen hasta cuatro valores por punto de datos. Estos valores se corresponden con los valores máximo, mínimo, de apertura y de cierre que se usan para trazar datos de acciones financieras. Este tipo de gráfico muestra los valores de apertura y de cierre mediante marcadores, que son normalmente líneas o triángulos. En el ejemplo siguiente, los marcadores de la izquierda muestran los valores de apertura y los marcadores de la derecha muestran los valores de cierre.  
  
 ![Gráfico de cotizaciones](../media/rs-stockchart.gif "Gráfico de cotizaciones")  
  
 Un ejemplo de gráfico de cotizaciones está disponible como informe de ejemplo del Generador de informes de [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] . Para obtener más información acerca de cómo descargar este y otros informes de ejemplo, consulte el tema sobre [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)][informes de ejemplo del Generador de informes y el Diseñador de informes](http://go.microsoft.com/fwlink/?LinkId=198283).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="variations"></a>Variaciones  
  
-   **Vela japonesa**. El gráfico de vela japonesa es una variante especializada del gráfico de cotizaciones, en el que se usan cuadros para mostrar el intervalo existente entre los valores de apertura y de cierre. Al igual que el gráfico de cotizaciones, el gráfico de vela japonesa puede mostrar hasta cuatro valores por punto de datos.  
  
## <a name="data-considerations-for-stock-charts"></a>Consideraciones sobre los datos para los gráficos de cotizaciones  
  
-   Cuando se presentan muchos puntos de datos de acciones, como la tendencia anual del precio de las acciones, resulta difícil distinguir los valores máximo, mínimo, de apertura y de cierre de cada punto de datos. En este escenario, puede resultar más factible usar un gráfico de líneas en lugar de uno de cotizaciones.  
  
-   Cuando se generan las etiquetas del eje, normalmente se empieza por el cero.  En general, los precios de las acciones no fluctúan tanto como otros conjuntos de datos. Por esta razón, es posible que desee que las etiquetas del eje no empiecen por el cero con el fin de obtener una mejor perspectiva de los datos. Para ello, establezca **IncludeZero** en **false** en el cuadro de diálogo **Propiedades del eje** o en la ventana Propiedades. Para más información sobre cómo genera el gráfico etiquetas de eje, vea [Aplicar formato a las etiquetas de los ejes de un gráfico &#40;Generador de informes y SSRS&#41;](formatting-axis-labels-on-a-chart-report-builder-and-ssrs.md).  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] proporciona muchas fórmulas calculadas para su uso con los gráficos de cotizaciones, incluyendo indicadores de precio, indicadores de fuerza relativa, convergencia de media móvil, etc.  
  
## <a name="see-also"></a>Vea también  
 [Gráficos de intervalo &#40;el generador de informes SSRS&#41;](charts-report-builder-and-ssrs.md)   
 [Gráficos &#40;Generador de informes y SSRS&#41;](charts-report-builder-and-ssrs.md)   
 [Aplicar formato a un gráfico &#40;Generador de informes y SSRS&#41;](formatting-a-chart-report-builder-and-ssrs.md)   
 [Cuadro de diálogo de propiedades de eje, opciones del eje &#40;el generador de informes SSRS&#41;](../axis-properties-dialog-box-axis-options-report-builder-and-ssrs.md)  
  
  