---
title: Minigráficos y barras de datos (Generador de informes y SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.rtp.rptdesigner.sparklines.f1
- "10544"
ms.assetid: b287436b-fa48-4970-a1a7-1dbcb86e7411
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 28b981dfe725a42228f287bc7a02df836030f3d0
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/23/2019
ms.locfileid: "66104962"
---
# <a name="sparklines-and-data-bars-report-builder-and-ssrs"></a>Minigráficos y barras de datos (Generador de informes y SSRS)
  Los minigráficos y las barras de datos son gráficos simples y pequeños que contienen mucha información en poco espacio, a menudo conjuntamente con texto. Los minigráficos y las barras de datos se utilizan a menudo en las tablas y matrices. Su importancia radica en que permiten ver muchos datos juntos y compararlos rápidamente uno encima de otro, en lugar de verlos de forma individual. Facilitan la visualización de los valores atípicos, las filas que no se muestran como las demás. Aunque son pequeños, cada minigráfico suele representar varios puntos de datos, con frecuencia, a lo largo del tiempo. Las barras de datos representan varios puntos de datos, pero normalmente solo muestran uno. Cada minigráfico suele presentar una única serie. No puede agregar un minigráfico a un grupo de detalles en una tabla. Dado que los minigráficos presentan los datos agregados, deben estar en una celda que esté asociada a un grupo. Los minigráficos y las barras de datos tienen los mismos elementos de gráfico básicos de las categorías, series y valores, pero carecen de leyendas, líneas de eje, etiquetas o marcas de graduación.  
  
 ![rs_SparklineExample](../media/rs-sparklineexample.gif "rs_SparklineExample")  
  
 Para obtener información acerca de los minigráficos, vea [ Tutorial: Agregar un minigráfico a un informe &#40;Generador de informes&#41;](../tutorial-add-a-sparkline-to-your-report-report-builder.md) y los vídeos [ Crear un minigráfico en una tabla](https://go.microsoft.com/fwlink/?LinkId=197092) y [Minigráficos, gráficos de barras e indicadores en el Generador de informes](https://technet.microsoft.com/bi/video/ff877165).  
  
> [!NOTE]  
>  Puede publicar minigráficos y barras de datos con su lista, matriz o tabla primaria por separado de un informe como elementos de informe. [!INCLUDE[ssRBrptparts](../../includes/ssrbrptparts-md.md)]  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="KindsofSparklines"></a> Tipos de minigráficos  
 Puede crear casi tantos tipos de minigráficos como gráficos normales. En general, no puede crear minigráfico 3D. Puede crear versiones de minigráfico de estos gráficos completos:  
  
-   [Gráficos de columnas &#40;Generador de informes y SSRS&#41;](charts-report-builder-and-ssrs.md): Los gráficos de columnas básicas, apiladas y 100% apiladas.  
  
-   [Gráficos de líneas &#40;Generador de informes y SSRS&#41;](line-charts-report-builder-and-ssrs.md): Todos excepto el de 3D gráficos de líneas.  
  
-   [Gráficos de áreas &#40;Generador de informes y SSRS&#41;](area-charts-report-builder-and-ssrs.md): Todo excepto los gráficos de área 3D  
  
-   [Gráficos circulares &#40;Generador de informes y SSRS&#41;](pie-charts-report-builder-and-ssrs.md): Y los gráficos de anillos, planos y 3D, pero no las demás formas, como gráficos de embudo y piramidal.  
  
-   [Rangos de intervalos &#40;Generador de informes y SSRS&#41;](range-charts-report-builder-and-ssrs.md): Stock, vela japonesa, barras de error y los diagramas de caja.  
  
##  <a name="DataBars"></a> Barras de datos  
 Las barras de datos suelen representar un único punto de datos, aunque pueden representar varios, al igual que los gráficos de barras normales. A menudo contienen varias series sin categoría o tienen agrupaciones de serie.  
  
 ![rs_DataBars](../media/rs-databars.gif "rs_DataBars")  
  
 En este ejemplo que usa las barras de datos apiladas, cada una, aunque solo sea una barra, muestra más de un punto de datos. Por ejemplo, los tres colores diferentes de la barra podrían representar tareas de tres niveles de prioridad donde la longitud de la barra representa el número total de tareas asignado a cada persona. Si realizara barras de datos apiladas al 100% en su lugar, cada barra rellenaría la celda y los diferentes colores representarían el porcentaje del todo para cada nivel de prioridad.  
  
 Puede crear versiones de barras de datos de estos gráficos completos:  
  
-   [Gráficos de barras &#40;Generador de informes y SSRS&#41;](bar-charts-report-builder-and-ssrs.md): Gráficos de barras apiladas de básicas, apilada y 100%.  
  
-   [Gráficos de columnas &#40;Generador de informes y SSRS&#41;](charts-report-builder-and-ssrs.md): Gráficos de columnas básicas, apiladas y 100% apiladas. Los gráficos de columnas pueden ser minigráficos o barras de datos.  

##  <a name="AlignDatainTableMatrix"></a> Alinear los datos de minigráficos en una tabla o matriz  
 Al insertar un minigráfico en una tabla o matriz, suele ser importante que los puntos de datos de cada minigráfico se alineen con los puntos de datos de los demás minigráficos de esa columna. De lo contrario, es difícil comparar los datos de las distintas filas. Por ejemplo, al comparar los datos de ventas por mes para distintos vendedores de la empresa, sería aconsejable que los meses estuvieran alineados. Si un empleado no trabajó durante el mes de abril, no habría datos para ese empleado durante ese mes. Desearía ver un hueco durante ese mes y vería los datos de los meses subsiguientes alineados con los datos de los demás empleados. Puede hacer esto alineando el eje horizontal. Para más información, vea la sección sobre minigráficos en [Ámbito de expresión para los totales, agregados y colecciones integradas &#40;Generador de informes y SSRS&#41;](expression-scope-for-totals-aggregates-and-built-in-collections.md) y también [Alinear los datos en un gráfico en una tabla o una matriz &#40;Generador de informes y SSRS&#41;](align-the-data-in-a-chart-in-a-table-or-matrix-report-builder-and-ssrs.md).  
  
 De la misma forma, para que se puedan comparar por filas, los datos deben alinearse también verticalmente. Dicho de otro modo, el alto de las barras o líneas de un minigráfico o barra de datos debe estar en relación con el alto de las barras y líneas en todos los demás minigráficos o barras de datos. En caso contrario, no podrá comparar dos filas entre sí.  
  
 ![rs_SparklineAlignData](../media/rs-sparklinealigndata.gif "rs_SparklineAlignData")  
  
 En esta imagen, el gráfico de columnas muestra las ventas cotidianas para cada empleado. Tenga en cuenta que durante los días que un empleado no tiene ninguna venta, el gráfico deja un espacio en blanco y alinea los días subsiguientes. Es un ejemplo de alineación horizontal. Observe también que para algunos empleados, todas las barras son cortas y ninguna barra alcanza la parte superior de la celda. El siguiente es un ejemplo de alineación vertical; sin ella, en las filas sin barras altas, las barras cortas se expandirían para rellenar el alto de la celda.  

##  <a name="UnderstandScope"></a> Descripción de los datos proporcionados a un minigráfico o barra de datos  
 La adición de un minigráfico o barra de datos a una tabla o matriz se conoce como *anidar* una región de datos en otra. La anidación significa que los datos proporcionados a un minigráfico o barra de datos son controlados por el conjunto de datos en el que se basa la tabla o la matriz y por su ubicación en la tabla o matriz. Para más información, vea [Anidar regiones de datos &#40;Generador de informes y SSRS&#41;](nested-data-regions-report-builder-and-ssrs.md).  
  
##  <a name="ConvertSparklinetoChart"></a> Convertir un minigráfico o una barra de datos en un gráfico completo  
 Dado que los minigráficos y las barras de datos son un tipo de gráfico, si decide que prefiere tener toda la funcionalidad de un gráfico completo, puede realizar la conversión a un gráfico completo haciendo clic con el botón derecho en el gráfico y seleccionando **Convertir a gráfico completo**. Al hacerlo, las líneas de ejes, las etiquetas, las marcas de graduación y la leyenda se agregan automáticamente.  
  
> [!NOTE]  
>  No puede convertir un gráfico completo en minigráfico o barra de datos con un clic. Sin embargo, puede crear un minigráfico o barra de datos a partir de un gráfico completo eliminando todos los elementos de gráfico que no se encuentran en los minigráficos y barras de datos.  

##  <a name="HowTo"></a> Temas de procedimientos  
 [Agregar minigráficos y barras de datos &#40;Generador de informes y SSRS&#41;](sparklines-and-data-bars-report-builder-and-ssrs.md)  
  
 [Alinear los datos en un gráfico en una tabla o una matriz &#40;Generador de informes y SSRS&#41;](align-the-data-in-a-chart-in-a-table-or-matrix-report-builder-and-ssrs.md)  
  
### <a name="other-how-to-topics-for-charts"></a>Otros temas de procedimientos para los gráficos  
 Puesto que los minigráficos y las barras de datos son un tipo de gráfico, los siguientes temas de procedimientos para gráficos también podrían resultarle útiles:  
  
 [Agregar un gráfico a un informe &#40;Generador de informes y SSRS&#41;](add-a-chart-to-a-report-report-builder-and-ssrs.md)  
  
 [Agregar puntos vacíos al gráfico &#40;generador de informes y SSRS&#41;](add-empty-points-to-a-chart-report-builder-and-ssrs.md)  
  
 [Agregar o quitar márgenes de un gráfico &#40;Generador de informes y SSRS&#41;](add-or-remove-margins-from-a-chart-report-builder-and-ssrs.md)  
  
 [Cambiar un tipo de gráfico &#40;Generador de informes y SSRS&#41;](change-a-chart-type-report-builder-and-ssrs.md)  
  
 [Definir los colores de un gráfico mediante una paleta &#40;Generador de informes y SSRS&#41;](define-colors-on-a-chart-using-a-palette-report-builder-and-ssrs.md)  
  
 [Mostrar la información sobre herramientas en una serie &#40;Generador de informes y SSRS&#41;](show-tooltips-on-a-series-report-builder-and-ssrs.md)  
  
 [Especificar una escala logarítmica &#40;Generador de informes y SSRS&#41;](specify-a-logarithmic-scale-report-builder-and-ssrs.md)  
  
 [Especificar un intervalo de eje &#40;Generador de informes y SSRS&#41;](specify-an-axis-interval-report-builder-and-ssrs.md)  
  
 [Especificar colores coherentes en varios gráficos de formas &#40;Generador de informes y SSRS&#41;](shape-charts-report-builder-and-ssrs.md)  
  
## <a name="see-also"></a>Vea también  
 [Gráficos &#40;Generador de informes y SSRS&#41;](charts-report-builder-and-ssrs.md)   
 [Tutorial: Agregar un minigráfico a un informe &#40;generador de informes&#41;](../tutorial-add-a-sparkline-to-your-report-report-builder.md)   
 [Minigráficos, gráficos de barras e indicadores en el generador de informes (vídeo)](https://technet.microsoft.com/bi/video/ff877165)   
 [Cómo: Crear un minigráfico en una tabla (vídeo)](https://go.microsoft.com/fwlink/?LinkId=197092)  
