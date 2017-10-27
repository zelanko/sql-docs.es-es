---
title: "Forma de gráficos (generador de informes y SSRS) | Documentos de Microsoft"
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
ms.assetid: 4b8404c1-aa89-4350-8bd6-203bc0446ee4
caps.latest.revision: 8
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 84ee7a9030bb27725994a33860b26b8754034cd9
ms.contentlocale: es-es
ms.lasthandoff: 08/09/2017

---
# <a name="shape-charts-report-builder-and-ssrs"></a>Gráficos de formas (Generador de informes y SSRS)
  Los gráficos de formas muestran los datos de valores como porcentajes de un total. Los gráficos de formas se usan normalmente para mostrar comparaciones proporcionales entre distintos valores de un conjunto. Las categorías se representan mediante segmentos individuales de la forma. El tamaño del segmento lo determina el valor. Los gráficos de formas son similares en cuanto a uso a los gráficos circulares, excepto en que los primeros ordenan las categorías de mayor a menor.  
  
 Un gráfico de embudo muestra los valores como proporciones que van decreciendo de forma progresiva. El tamaño del área lo determina el valor de la serie como un porcentaje del total de todos los valores. Por ejemplo, puede usar un gráfico de embudo para mostrar las tendencias de los visitantes de un sitio web. Es probable que el gráfico de embudo muestre un área amplia en la parte superior para indicar que la página más visitada es la página principal, y que las demás áreas sean proporcionalmente menores. Para más información sobre cómo agregar datos a un gráfico de embudo, vea [Gráficos &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/charts-report-builder-and-ssrs.md).  
  
 En la ilustración siguiente se muestra un ejemplo de gráfico de embudo.  
  
 ![Gráfico de embudo](../../reporting-services/report-design/media/rs-funnelchart.gif "gráfico de embudo")  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="variations"></a>Variaciones  
  
-   **Pirámide**: gráfico que muestra datos proporcionales y tiene forma de pirámide.  
  
## <a name="data-considerations-for-shape-charts"></a>Consideraciones sobre los datos para los gráficos de formas  
  
-   Los gráficos de formas son frecuentes en informes debido a su impacto visual. Sin embargo, los gráficos de formas son un tipo de gráfico muy simplificado que no siempre representa los datos de la mejor manera posible. Plantéese el uso de un gráfico de formas solo después de que los datos se hayan agregado en siete puntos de datos o menos. En general, use un gráfico de formas para mostrar solamente una categoría por cada región de datos.  
  
-   Los gráficos de formas muestran cada grupo de datos como un segmento independiente del gráfico. Debe agregar al menos un campo de datos y un campo de categorías. Si se agrega más de un campo de datos a un gráfico de formas, éste mostrará los campos de datos en el mismo gráfico.  
  
-   Los gráficos de formas son muy efectivos para mostrar porcentajes proporcionales ordenados. Sin embargo, para mantener la coherencia, el gráfico no ordena los valores del conjunto de datos de forma predeterminada. Piense en la posibilidad de ordenar los valores de mayor a menor para representar con mayor precisión los datos con forma de embudo o de pirámide. Para más información, vea [Filtrar, agrupar y ordenar datos &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/filter-group-and-sort-data-report-builder-and-ssrs.md).  
  
-   Los valores Null, los valores vacíos y los valores negativos no tienen ningún efecto a la hora de calcular las proporciones. Por esta razón, estos valores no se muestran en un gráfico de formas. Si desea indicar visualmente estos tipos de valores en el gráfico, cambie el gráfico de formas por otro tipo de gráfico. Para obtener más información acerca de cómo agregar puntos vacíos a un gráfico de forma distinta, vea [puntos vacíos de agregar a un gráfico de &#40; El generador de informes y SSRS &#41; ](../../reporting-services/report-design/add-empty-points-to-a-chart-report-builder-and-ssrs.md).  
  
-   Si va a definir sus propios colores en un gráfico de formas con una paleta personalizada, asegúrese de que dispone de colores suficientes para resaltar cada punto de datos con su propio color. Para obtener más información, vea [Aplicar formato a los colores de serie de un gráfico &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/formatting-series-colors-on-a-chart-report-builder-and-ssrs.md).  
  
-   A diferencia de todos los demás tipos de gráficos, un gráfico de formas muestra los puntos de datos, y no las series individuales, en su leyenda.  
  
-   No se tiene en cuenta la configuración de los ejes de valores y de categorías en los gráficos de embudo. Si tiene varios grupos de categorías o series, las etiquetas de grupo se muestran en la leyenda del gráfico.  
  
-   Los tipos de gráficos de formas no se pueden combinar con ningún otro tipo de gráfico en la misma área de gráfico. Si tiene que mostrar comparaciones entre los datos mostrados en un gráfico de formas y los datos mostrados en otro tipo de gráfico, necesitará agregar una segunda área de gráfico.  
  
-   Puede aplicar estilos de dibujo adicionales a los gráficos circulares y de anillos para aumentar su impacto visual. Vea [formato colores de serie de un gráfico de &#40; El generador de informes y SSRS &#41; ](../../reporting-services/report-design/formatting-series-colors-on-a-chart-report-builder-and-ssrs.md) para obtener más información.  
  
## <a name="see-also"></a>Vea también  
 [Gráficos &#40; El generador de informes y SSRS &#41;](../../reporting-services/report-design/charts-report-builder-and-ssrs.md)   
 [Aplicar formato a un gráfico de &#40; El generador de informes y SSRS &#41;](../../reporting-services/report-design/formatting-a-chart-report-builder-and-ssrs.md)   
 [Puntos de datos en los gráficos de &#40; vacíos y nulos El generador de informes y SSRS &#41;](../../reporting-services/report-design/empty-and-null-data-points-in-charts-report-builder-and-ssrs.md)   
 [Los gráficos circulares &#40; El generador de informes y SSRS &#41;](../../reporting-services/report-design/pie-charts-report-builder-and-ssrs.md)  
  
  

