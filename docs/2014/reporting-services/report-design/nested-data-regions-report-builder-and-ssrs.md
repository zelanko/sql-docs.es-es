---
title: Regiones de datos anidadas (Generador de informes y SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 15c2bc9b-428a-47ac-9630-8dde925d0595
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 293bfe1f270d32bc64d4344c5363a0be2cd74b84
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "66105521"
---
# <a name="nested-data-regions-report-builder-and-ssrs"></a>Anidar regiones de datos (Generador de informes y SSRS)
  Normalmente, una región de datos, como un gráfico, se anida dentro de otra, como una matriz, para mostrar resúmenes de los datos de una manera concisa o para mostrar los datos de forma gráfica, además de hacerlo en una tabla o una matriz.  
  
 Por ejemplo, en el caso de una matriz (también denominada *Tablix*) cuyas filas contienen pedidos de ventas agrupados por almacén y cuyas columnas contienen pedidos de ventas agrupados por trimestre, puede agregar una tabla o un gráfico en la celda de la esquina para resumir las ventas de todos los almacenes, o puede agregar un gráfico a un encabezado de columna de una matriz para mostrar la contribución a las ventas de los datos de la columna como porcentaje de todas las ventas.  
  
 ![rs_NestedDataRegion](../media/rs-nesteddataregion.gif "rs_NestedDataRegion")  
  
 En esta ilustración, el gráfico circular de la celda de la esquina y los gráficos sparkline de las filas son regiones de datos anidadas.  
  
 Por definición, las regiones de datos anidadas se basan en el mismo conjunto de datos de informe. No puede anidar regiones de datos basadas en conjuntos de datos diferentes. Para mostrar datos de conjuntos de datos diferentes, plantéese la posibilidad de usar informes o subinformes detallados. Para obtener más información, vea [Obtención de detalles, informes detallados, subinformes y regiones de datos anidadas &#40;Generador de informes y SSRS&#41;](drillthrough-drilldown-subreports-and-nested-data-regions.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="understanding-scope-for-a-nested-data-region"></a>Descripción del ámbito de una región de datos anidada  
 El ámbito de los datos de una región de datos anidada se define automáticamente mediante su posición en la región de datos primaria. Por ejemplo, el ámbito correspondiente a los datos de un gráfico que está anidado en la celda de la esquina de Tablix son los datos procedentes del conjunto de datos enlazado a la región de datos Tablix una vez aplicados los filtros para el conjunto de datos, la región de datos Tablix y la región de datos de gráfico. El ámbito de un Tablix anidado en una celda de Tablix es el mismo que el ámbito de la celda de la esquina pero, además, se sitúa en el ámbito de la pertenencia al grupo de filas y columnas de la celda en la que está anidado, con los correspondientes filtros de grupo aplicados. Para más información sobre el ámbito, vea [Ámbito de expresión para los totales, agregados y colecciones integradas &#40;Generador de informes y SSRS&#41;](expression-scope-for-totals-aggregates-and-built-in-collections.md).  
  
 En la lista siguiente, se describe el ámbito para las celdas de las áreas de Tablix siguientes:  
  
-   **Área de esquina de Tablix** : el ámbito son los datos de la región de datos vinculada a la región de datos Tablix, después de haber aplicado las expresiones de filtro y de ordenación para el conjunto de datos y el Tablix externo.  
  
-   **Grupo de columnas de Tablix** : son los datos del grupo de columnas más interior, después de haber aplicado las expresiones de filtro y de ordenación para el conjunto de datos, el Tablix externo y los grupos de columnas.  
  
-   **Grupo de filas del Tablix** : son los datos del grupo de filas más interior, después de haber aplicado las expresiones de filtro y de ordenación para el conjunto de datos, el Tablix externo y los grupos de filas.  
  
-   **Cuerpo del Tablix** : los datos del grupo más interior representado por la intersección de los grupos de filas y los grupos de columnas, después de haber aplicado las expresiones de filtro y de ordenación para el conjunto de datos, el Tablix externo, y los grupos de filas y de columnas.  
  
 Para obtener más información, vea [Describir las áreas de la región de datos Tablix &#40;Generador de informes y SSRS&#41](tablix-data-region-areas-report-builder-and-ssrs.md).  
  
## <a name="nesting-a-chart-sparkline-or-data-bar-in-a-tablix"></a>Anidar un gráfico, un minigráfico o una barra de datos en un Tablix  
 Cuando se agrega un gráfico (incluido un minigráfico o una barra de datos) a una fila de encabezado o pie de grupo de columnas de Tablix, o a una celda de cuerpo de Tablix, los datos que se pasan al gráfico pertenecen al ámbito del subconjunto de datos de esa celda. De forma predeterminada, al agregar un gráfico a una celda de Tablix, el gráfico aumenta de tamaño para rellenar la celda.  
  
> [!NOTE]  
>  Para tener un mayor control sobre el tamaño de un gráfico de una celda de Tablix, agregue primero el gráfico a un rectángulo y, a continuación, agregue el rectángulo a la celda de Tablix.  
  
 De forma predeterminada, los colores de los puntos de datos de la serie del gráfico determinan los colores de la leyenda. Si desea tener un mayor control sobre los colores a fin de que todas las regiones de datos anidadas del gráfico usen el mismo color para la misma categoría de datos, deberá usar colores personalizados y establecer expresiones de ordenación en los datos. Para más información, vea [Especificar colores uniformes en varios gráficos de formas &#40;Generador de informes y SSRS&#41;](charts-report-builder-and-ssrs.md) y [Ordenar datos en una región de datos &#40;Generador de informes y SSRS&#41;](sort-data-in-a-data-region-report-builder-and-ssrs.md).  
  
## <a name="nesting-a-gauge-or-an-indicator-in-a-tablix"></a>Anidar un medidor o un indicador en un Tablix  
 Puede anidar un medidor o un indicador dentro de una tabla, una matriz o una lista para mostrar un indicador clave de rendimiento (KPI). Cuando se sitúa un medidor o un indicador en una tabla, se representará para cada fila del Tablix. Para más información sobre cómo agregar indicadores a un Tablix, vea [Indicadores &#40;Generador de informes y SSRS&#41;](indicators-report-builder-and-ssrs.md).  
  
### <a name="adding-a-gauge-to-a-tablix"></a>Agregar un medidor a un Tablix  
 Hay dos maneras de agregar un medidor a una región de datos Tablix:  
  
-   Haga clic dentro de la celda de Tablix e inserte un medidor. Aparece el cuadro de diálogo **Seleccionar tipo de medidor** . Una vez seleccionado el tipo de medidor, la región de datos de medidor se sitúa dentro de la celda de Tablix seleccionada. Probablemente, necesitará cambiar el tamaño de Tablix para dar formato al medidor.  
  
-   Haga clic fuera de la tabla e inserte un medidor. Aparece el cuadro de diálogo **Seleccionar tipo de medidor** . Después de seleccionar un tipo de medidor, la región de datos de medidor se sitúa en la esquina superior izquierda del informe. Cuando haya agregado los datos y haya dado formato al medidor, arrástrelo y colóquelo dentro de la celda de Tablix.  
  
 Al igual que con el gráfico, el conjunto de datos que se pasa al medidor pertenece al ámbito del subconjunto de datos de esa celda. Cuando se coloca un medidor dentro de una celda de Tablix, el medidor siempre agrega una única fila de datos.  
  
 Si los datos de Tablix contienen grupos, la región de datos de medidor que está anidada en Tablix no los hereda de forma automática. Para mostrar la misma información que se muestra en el Tablix, deberá agregar al medidor una expresión de grupo coincidente. Por ejemplo, si los datos del Tablix están agrupados por producto, deberá agregar una expresión de grupo de producto al medidor para mostrar los mismos datos. Para más información, vea [Medidores &#40;Generador de informes y SSRS&#41;](gauges-report-builder-and-ssrs.md) y [Agregar o eliminar un grupo en una región de datos &#40;Generador de informes y SSRS&#41;](add-or-delete-a-group-in-a-data-region-report-builder-and-ssrs.md).  
  
 Debe establecer los valores máximo y mínimo que se mostrarán en la escala del medidor. Para especificar el valor máximo del medidor, puede usar una expresión, como `=Max!MyField.Value`. Sin embargo, dado que esta expresión solo se evaluará dentro del ámbito de los datos de la celda, el valor máximo de cada medidor no será el mismo para todas las filas de Tablix. Esto puede dificultar la comprensión de las comparaciones entre los medidores de Tablix. Como alternativa, puede especificar un valor estático para el valor máximo. Todas las filas de Tablix mostrarán un medidor con este valor máximo. Para más información, vea [Establecer un valor mínimo o máximo en un medidor &#40;Generador de informes y SSRS&#41;](set-a-minimum-or-maximum-on-a-gauge-report-builder-and-ssrs.md).  
  
 Si los datos se vuelven demasiado grandes en el medidor, plantéese la posibilidad de usar un multiplicador de escala para reducir el número de dígitos mostrados. Para especificar un multiplicador, puede hacer clic con el botón derecho en la escala y seleccionar **Propiedades de escala**. Cuando se abra el cuadro de diálogo **Propiedades de escala** , especifique un valor para **Multiplicador**.  
  
## <a name="nesting-a-table-or-matrix-and-a-chart-in-a-list"></a>Anidar una tabla o matriz y un gráfico en una lista  
 Para anidar varias regiones de datos en una lista, primero se agrega un rectángulo y, a continuación, se agregan las regiones de datos al rectángulo.  
  
 Puede definir un grupo para una región de datos de lista y, a continuación, agregar un Tablix y un gráfico para proporcionar vistas diferentes de los mismos datos. Para lograr este efecto, debe definir expresiones de grupo y de ordenación idénticas para el Tablix y el gráfico incrustados. Por definición, el Tablix y el gráfico usan datos procedentes del conjunto de datos de la región de datos de lista primaria.  
  
> [!NOTE]  
>  De forma predeterminada, al agregar una región de datos de lista a la superficie de diseño, la lista incluye una fila de detalles. Para cambiar este valor predeterminado, agregue una fila de grupos y quite la fila de detalles. Para más información, vea [Explorar la flexibilidad de una región de datos Tablix &#40;Generador de informes y SSRS&#41;](exploring-the-flexibility-of-a-tablix-data-region-report-builder-and-ssrs.md).  
  
 Para más información, vea [Descripción de los grupos &#40;Generador de informes y SSRS&#41;](understanding-groups-report-builder-and-ssrs.md) y [Agregar, mover o eliminar una tabla, matriz o lista &#40;Generador de informes y SSRS&#41;](add-move-or-delete-a-table-matrix-or-list-report-builder-and-ssrs.md).  
  
## <a name="see-also"></a>Consulte también  
 [Filtrar, agrupar y ordenar datos &#40;Generador de informes y SSRS&#41;](filter-group-and-sort-data-report-builder-and-ssrs.md)   
 [Enumera &#40;Generador de informes y SSRS&#41;](tables-matrices-and-lists-report-builder-and-ssrs.md)   
 [Gráficos &#40;Generador de informes y SSRS&#41;](charts-report-builder-and-ssrs.md)   
 [Medidores &#40;Generador de informes y SSRS&#41;](gauges-report-builder-and-ssrs.md)   
 [Expresiones &#40;Generador de informes y SSRS&#41;](expressions-report-builder-and-ssrs.md)   
 [Aplicar formato a los elementos de informe &#40;Generador de informes y SSRS&#41;](formatting-report-items-report-builder-and-ssrs.md)   
 [Tutorial: Agregar un KPI al informe &#40;Generador de informes&#41;](../tutorial-adding-a-kpi-to-your-report-report-builder.md)   
 [Aplicar formato a las escalas de un medidor &#40;Generador de informes y SSRS&#41;](formatting-scales-on-a-gauge-report-builder-and-ssrs.md)  
  
  
