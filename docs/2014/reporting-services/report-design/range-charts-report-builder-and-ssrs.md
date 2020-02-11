---
title: Rangos de intervalos (Generador de informes y SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 48e351d3-ac5b-4eda-a4bd-32a0de206a30
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: e44e658d2aaf8be9a9e591f627f60798f6ba4121
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "66105399"
---
# <a name="range-charts-report-builder-and-ssrs"></a>Rangos de intervalos (Generador de informes y SSRS)
  Un tipo de gráfico de intervalos muestra un conjunto de puntos de datos en el que cada uno de ellos se define mediante varios valores para la misma categoría. Los valores se representan mediante el alto de los marcadores con relación al eje de valores. Las etiquetas de las categorías se muestran en el eje de categorías. El gráfico de intervalos sencillo rellena el área situada entre el valor superior y el valor inferior de cada punto de datos.  
  
 En la ilustración siguiente se muestra un gráfico de intervalos sencillo con tres series.  
  
 ![Gráfico de intervalos](../media/rs-rangechart.gif "Gráfico de intervalos")  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="variations"></a>Variaciones  
  
-   **Intervalo suavizado**. Un gráfico de intervalos suavizados muestra las líneas curvas en lugar de rectas.  
  
-   **Rango de columnas**. Un gráfico de intervalos de columnas usa columnas en lugar de áreas para mostrar los intervalos.  
  
-   **Intervalo de barras**. Un gráfico de intervalos de barras usa barras en lugar de áreas para mostrar los intervalos.  
  
## <a name="data-considerations-for-range-charts"></a>Consideraciones sobre los datos para los gráficos de intervalos  
  
-   Los tipos de gráficos de intervalos requieren dos valores para cada punto de datos. Estos valores se corresponden con un valor alto y un valor bajo que definen el intervalo para cada punto de datos.  
  
-   Los gráficos de intervalos son útiles para realizar análisis solo si los valores superiores son siempre más altos que los inferiores. Si este no es el caso, considere la posibilidad de usar un gráfico de líneas. Si el valor alto es más bajo que el valor bajo, el gráfico de intervalos mostrará el valor absoluto de la diferencia entre estos valores.  
  
-   Si se especifica solo un valor, el gráfico de intervalos se mostrará como si se tratara de un gráfico de áreas normal, con un valor por cada punto de datos.  
  
-   Los gráficos de intervalos se suelen usar para representar gráficamente datos que contienen valores mínimos y máximos para cada grupo de categorías del conjunto de datos.  
  
-   En un gráfico de intervalos no es posible mostrar marcadores en cada punto de datos.  
  
-   Al igual que en un gráfico de áreas, si en un gráfico de intervalos sencillo los valores de varias series son similares, las series se superpondrán. En este escenario, es posible que prefiera usar un gráfico de intervalos de columnas o un gráfico de intervalos de barras en lugar de un gráfico de intervalos sencillo.  
  
-   Se pueden crear diagramas de Gantt usando un gráfico de intervalos de barras.  
  
## <a name="see-also"></a>Consulte también  
 [Gráficos &#40;Generador de informes y SSRS&#41;](charts-report-builder-and-ssrs.md)   
 [Tipos de gráficos &#40;Generador de informes y SSRS&#41;](chart-types-report-builder-and-ssrs.md)   
 [Aplicar formato a un gráfico &#40;Generador de informes y SSRS&#41;](formatting-a-chart-report-builder-and-ssrs.md)  
  
  
