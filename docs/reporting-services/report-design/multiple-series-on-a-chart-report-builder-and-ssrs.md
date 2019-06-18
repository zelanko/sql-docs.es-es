---
title: Mostrar varias series en un gráfico (Generador de informes y SSRS) | Microsoft Docs
ms.date: 03/07/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: b99e4398-1fba-4824-958f-5c75d10485ea
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 8aedfd50c591f3a8aef4855854eed760ce093a7a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "65580625"
---
# <a name="multiple-series-on-a-chart-report-builder-and-ssrs"></a>Mostrar varias series en un gráfico (Generador de informes y SSRS)
  Cuando hay varias series en un gráfico, es necesario determinar la mejor manera de compararlas. Puede usar un gráfico apilado para mostrar las proporciones relativas de cada serie. Si está comparando únicamente dos series que comparten un eje de categoría común (X), use el eje secundario. Esto es útil cuando se muestran dos series de datos relacionadas, por ejemplo, el precio y el volumen, o los ingresos y los impuestos. Si el gráfico se vuelve ilegible, considere la posibilidad de usar varias áreas de gráfico para crear una mayor separación visual entre una serie y otra.  
  
 Además de usar las características de los gráficos, es importante decidir qué tipo de gráfico se debe usar para los datos. Si los campos del conjunto de datos están relacionados, considere la posibilidad de usar un gráfico de intervalos.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="using-stacked-and-100-stacked-charts"></a>Usar gráficos apilados y 100% apilados  
 Los gráficos apilados se usan normalmente para mostrar varias series en un área de gráfico. Considere la posibilidad de usar gráficos apilados cuando los datos que intenta mostrar están estrechamente relacionados. También es recomendable no mostrar más de cuatro series en un gráfico apilado. Si desea comparar la proporción con la que contribuye cada serie al todo, use un gráfico de áreas, de barras o de columnas 100% apiladas. Estos gráficos calculan el porcentaje relativo con el que cada serie contribuye a la categoría. Para más información, vea [Gráficos de áreas &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/area-charts-report-builder-and-ssrs.md), [Gráficos de barras &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/bar-charts-report-builder-and-ssrs.md) y [Gráficos de columnas &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/column-charts-report-builder-and-ssrs.md).  
  
## <a name="using-the-secondary-axis"></a>Usar el eje secundario  
 Cuando se agrega una nueva serie al gráfico, se seguimiento usando los ejes X e Y principales. Si desea comparar valores pertenecientes a distintas unidades de medida, considere la posibilidad de usar el *eje secundario* para poder trazar dos series en ejes independientes. El eje secundario es útil cuando se comparan valores de unidades de medida diferentes. El eje secundario se dibuja en el lado contrario del eje principal. El gráfico solo admite un eje principal y un eje secundario. El eje secundario tiene las mismas propiedades que el eje principal. Para más información, vea [Trazar datos en un eje secundario &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/plot-data-on-a-secondary-axis-report-builder-and-ssrs.md).  
  
 Si desea mostrar más de dos series que tienen intervalos de datos diferentes, considere la posibilidad de colocarlas en áreas de gráfico independientes.  
  
## <a name="using-chart-areas"></a>Usar áreas de gráfico  
 El gráfico es el contenedor de nivel superior que incluye el borde exterior, el título del gráfico y la leyenda. De forma predeterminada, el gráfico contiene un área de gráfico predeterminada. El área de gráfico no está visible en la superficie del gráfico, pero puede imaginarla como un contenedor que incluye únicamente las etiquetas del eje, el título del eje y el área de trazado de una o más series. En la ilustración siguiente se muestra el concepto de áreas de gráfico dentro de un único gráfico.  
  
 ![Muestra un diagrama de un área de gráfico](../../reporting-services/report-design/media/chartareasdiagram.gif "Muestra un diagrama de un área de gráfico")  
  
 El cuadro de diálogo **Propiedades del área de gráfico** le permite especificar la orientación en 2D y 3D de todas las series incluidas en el área de gráfico, alinear varias áreas de gráfico dentro del mismo gráfico y dar formato a los colores del área de trazado. Cuando se define una nueva área de gráfico en un gráfico que solo contiene un área de gráfico predeterminada, el espacio disponible para ésta se divide horizontalmente en dos y la nueva área de gráfico se coloca debajo de la primera.  
  
 Cada serie solo se puede conectar a un área de gráfico. De forma predeterminada, todas las series se agregan al área de gráfico predeterminada. Cuando se usan gráficos de áreas, de columnas, de líneas y de dispersión, cualquier combinación de estas series se puede mostrar en la misma área de gráfico. Por ejemplo, puede mostrar una serie de columnas y una serie de líneas en la misma área de gráfico. La ventaja de usar la misma área de gráfico para varias series es que los usuarios finales pueden realizar comparaciones con facilidad.  
  
 Los gráficos de barras, de formas y radiales no se pueden combinar con ningún otro tipo de gráfico en la misma área de gráfico. Si desea realizar comparaciones con varias series que son de tipo barras, radial o de formas, deberá llevar a cabo una de estas acciones:  
  
-   Cambiar todas las series del área de gráfico para que sean del mismo tipo de gráfico.  
  
-   Crear una nueva área de gráfico y mover al menos una de las series del área de gráfico predeterminada a la nueva área de gráfico.  
  
 La característica que permite incluir varias áreas de gráfico en un único gráfico también resulta útil si intenta comparar datos que tienen distintas escalas de valores. Por ejemplo, si la primera serie contiene datos en el intervalo de 10 a 20 y la segunda contiene datos en el intervalo de 400 a 800, los valores de la primera serie pueden quedar ocultos. Considere la posibilidad de separar cada serie en un área de gráfico diferente. Para más información, vea [Especificar un área de gráfico para una serie &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/specify-a-chart-area-for-a-series-report-builder-and-ssrs.md).  
  
## <a name="using-range-charts"></a>Usar gráficos de intervalos  
 Los gráficos de intervalos tienen dos valores por cada punto de datos. Si el gráfico contiene dos series que comparten el mismo eje de categorías (X), puede usar un gráfico de intervalos para mostrar la diferencia entre ambas. Los gráficos de intervalos son los más adecuados para mostrar información en formato máximo-mínimo o superior-inferior. Por ejemplo, si la primera serie contiene la venta de mayor importe para cada día durante el mes de enero, y la segunda serie contiene la venta de menor importe para cada día durante el mismo período, puede usar un gráfico de intervalos para mostrar la diferencia entre ambas ventas para cada día. Para más información, vea [Gráficos de intervalos &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/range-charts-report-builder-and-ssrs.md).  
  
## <a name="see-also"></a>Consulte también  
 [Gráficos &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/charts-report-builder-and-ssrs.md)   
 [Mostrar una serie con varios rangos de datos en un gráfico &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/displaying-a-series-with-multiple-data-ranges-on-a-chart.md)   
 [Tipos de gráficos &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/chart-types-report-builder-and-ssrs.md)  
  
  
