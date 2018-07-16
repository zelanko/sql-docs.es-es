---
title: Gráficos de columnas (Generador de informes y SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: ae8c138b-e356-4ad8-862c-a4a8d0c04149
caps.latest.revision: 8
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: ba88d7a078889de09af4bd33e484ae69519721c7
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37246203"
---
# <a name="column-charts-report-builder-and-ssrs"></a>Gráficos de columnas (Generador de informes y SSRS)
  Un gráfico de columnas muestra una serie como un conjunto de barras verticales agrupadas por categorías. Los gráficos de columnas resultan de gran utilidad para mostrar los cambios que se producen en los datos a lo largo del tiempo o para ilustrar comparaciones entre elementos. El gráfico de columnas sencillo está estrechamente relacionado con el gráfico de barras, que muestra las series como conjuntos de barras horizontales, y con el gráfico de intervalos de columnas, que muestra las series como conjuntos de barras verticales con puntos iniciales y finales que varían. Para obtener más información, consulte [gráficos de barras &#40;generador de informes y SSRS&#41; ](charts-report-builder-and-ssrs.md) y [rangos &#40;generador de informes y SSRS&#41;](range-charts-report-builder-and-ssrs.md).  
  
 El gráfico de columnas se adapta perfectamente a estos datos porque las tres series comparten un período de tiempo común, lo que permite llevar a cabo comparaciones válidas.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="variations-of-a-column-chart"></a>Variaciones de un gráfico de columnas  
  
-   **Barra apilada**: Gráfico de columnas donde varias series se apilan verticalmente. Si solo hay una serie en el gráfico; la columna apilada se mostrará igual que un gráfico de columnas.  
  
-   **Barra 100% apilada**: Gráfico de columnas donde varias series se apilan verticalmente para ajustarse al 100% del área del gráfico. Si solo hay una serie en el gráfico, todas las barras de columna se ajustarán al 100% del área del gráfico.  
  
-   **Barra 3D en clúster**: Gráfico de columnas que muestra series individuales en filas independientes en un gráfico 3D.  
  
-   **Cilindro 3D**: Gráfico de columnas cuyas barras tienen forma de cilindro en un gráfico 3D.  
  
-   `Histogram`. Gráfico de columnas que se calcula para que las barras se organicen en una distribución normal.  
  
-   `Pareto`. Gráfico de columnas cuyas barras se organizan de mayor a menor.  
  
## <a name="data-considerations-for-a-column-chart"></a>Consideraciones sobre los datos para un gráfico de columnas  
  
-   Los gráficos de barras y de columnas se usan normalmente para mostrar comparaciones entre grupos. Si en un gráfico hay más de tres series, plantéese la posibilidad de usar un gráfico de barra apilada o un gráfico de columna apilada. Si tiene varias series en el gráfico, también puede combinar gráficos de barra apilada o de columna apilada en varios en grupos. Para obtener más información, consulte [gráficos de barras &#40;generador de informes y SSRS&#41; ](charts-report-builder-and-ssrs.md) y *gráficos de columnas*.  
  
-   En un gráfico de columnas, dispone de menos espacio para mostrar horizontalmente las etiquetas del eje de categorías. Si las etiquetas son largas, considere la posibilidad de usar un gráfico de barras o de cambiar el ángulo de giro de las etiquetas.  
  
-   Puede agregar estilos de dibujo especiales a las barras de un gráfico de columnas para aumentar su impacto visual. Los estilos de dibujo incluyen cuñas, relieves, cilindros y degradados. Estos efectos han sido diseñados para mejorar el aspecto de los gráficos 2D. Si su gráfico es un gráfico 3D, se aplicarán los estilos de dibujo, pero el efecto puede no ser el mismo. Para obtener más información acerca de cómo agregar un estilo de dibujo a un gráfico de barras, vea [agregar estilos con bisel, relieve y textura a un gráfico &#40;generador de informes y SSRS&#41;](chart-effects-add-bevel-emboss-or-texture-report-builder.md).  
  
-   Una característica exclusiva de los gráficos de columnas es su capacidad para mostrarse como un histograma o gráfico de Pareto. Para ello, establezca la propiedad ShowColumnAs `Histogram` o `Pareto` en la ventana Propiedades para `true`.  
  
## <a name="see-also"></a>Vea también  
 [Gráficos &#40;Generador de informes y SSRS&#41;](charts-report-builder-and-ssrs.md)   
 [Tipos de gráficos &#40;Generador de informes y SSRS&#41;](chart-types-report-builder-and-ssrs.md)   
 [Los gráficos de barras &#40;generador de informes y SSRS&#41;](charts-report-builder-and-ssrs.md)   
 [Rangos de intervalos &#40;generador de informes y SSRS&#41;](range-charts-report-builder-and-ssrs.md)   
 [Tutorial: Agregar un gráfico de barras a un informe &#40;Generador de informes&#41;](../tutorial-add-a-bar-chart-to-your-report-report-builder.md)   
 [Puntos de datos en los gráficos vacíos y nulos &#40;generador de informes y SSRS&#41;](empty-and-null-data-points-in-charts-report-builder-and-ssrs.md)  
  
  
