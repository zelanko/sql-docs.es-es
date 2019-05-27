---
title: Examinar un modelo de pronóstico | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- mining models, browsing
- forecasting [data mining]
- mining models, viewing
- mining model, time series
- time series [data mining]
ms.assetid: ad35a528-1949-4048-8678-3b9760c1c88c
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 830aea002e8000feeda061f42af9084696ed6fe8
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/23/2019
ms.locfileid: "66088488"
---
# <a name="browsing-a-forecasting-model"></a>Examinar un modelo de pronóstico
  Al abrir un modelo de previsión con **examinar**, el modelo se muestra en un visor interactivo, similar al Visor de modelos de serie de tiempo en [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. El visor sirve para explorar las tendencias, comparar series, crear predicciones y obtener información sobre el modelo y los datos subyacentes.  
  
##  <a name="bkmk_Top"></a> Explorar el modelo  
 El **examinar** Visor de modelos de predicción proporciona una vista de gráfico, que muestra las tendencias a lo largo de tiempo y le permite crear predicciones y una vista de modelo, que representa la serie temporal como un árbol de decisión o un árbol de regresión.  
  
-   [Vista de gráfico](#bkmk_charts)  
  
-   [Vista de modelo](#bkmk_Model)  
  
 Para experimentar con un modelo de pronóstico, puede usar los datos de ejemplo en la pestaña predicción de libro de ejemplo y generar un modelo de serie de tiempo utilizando la [Asistente para pronóstico &#40;complementos minería de datos para Excel&#41; ](forecast-wizard-data-mining-add-ins-for-excel.md) en el  **Minería de datos** cinta de opciones, o [previsión &#40;herramientas de análisis de tabla para Excel&#41; ](forecast-table-analysis-tools-for-excel.md) en el **analizar** cinta de opciones.  
  
###  <a name="bkmk_charts"></a> Gráfico  
 El **gráfico** pestaña muestra la tendencia de la serie de datos con el tiempo, junto con los valores de predicción. El eje vertical del gráfico representa los valores de la serie y el eje horizontal representa el tiempo.  
  
##### <a name="explore-the-forecasting-chart"></a>Explorar el gráfico de predicción  
  
1.  Este modelo contiene varias series temporales pero, para simplificar el gráfico, puede mostrar una sola serie o algunas series relacionadas.  
  
     ![predicciones históricas en el modelo de pronóstico](media/dm13-forecast-chart-historicpredictions.gif "predicciones históricas en el modelo de pronóstico")  
  
     Utilice las casillas para seleccionar la predicción solo para Norteamérica y solo para la cantidad de ventas.  
  
2.  Haga clic en **pasos de predicción** y escriba un nuevo valor para controlar valores de cuántos hora futuros desea ver en el gráfico.  
  
     El valor predeterminado es 5.  
  
3.  Haga clic en cualquier punto de la línea, histórica o futura, para ver los valores exactos para ese punto en el tiempo, aparece en el **leyenda de minería de datos**.  
  
4.  El gráfico muestra tanto los datos históricos como los futuros. Observe la línea de puntos con un fondo sombreado. Estos valores son las predicciones futuras, según el modelo.  
  
     Los datos históricos (que usó para generar el modelo) se muestran en el lado izquierdo del gráfico.  
  
5.  Seleccione el **Mostrar predicciones históricas** opción para hacerse una idea de la estabilidad de la serie temporal.  
  
     ![las previsiones de una sola serie en el modelo](media/dm13-forecast-chart-singleseries.gif "las previsiones de una sola serie en el modelo")  
  
     Las predicciones históricas son los valores previstos en función de las series hasta ese punto, que se comparan con los valores históricos reales. Si la línea de puntos (con los valores previstos) se aparta de la línea continua (los valores reales), significa que la primera parte de la serie quizás no predice con precisión los valores posteriores. Podría necesitar más datos o podría ser simplemente un indicador de la volatilidad en el ciclo.  
  
6.  Seleccione el **mostrar desviaciones** opción para mostrar las barras de error en el gráfico.  
  
     Las barras de error permiten evaluar visualmente la variabilidad de las predicciones. La calidad de las predicciones varía en función de los datos de origen pero a medida que aumenta el número de pasos de predicción, debería ver las desviaciones en constante aumento.  
  
 **Sugerencias**  
  
-   Para mostrar u ocultar de la **leyenda de minería de datos**, haga clic en cualquier punto del gráfico.  
  
     Puede ver un intervalo específico de tiempo; para ello, haga clic en el gráfico, arrastre una selección temporal sobre el gráfico y, a continuación, haga clic de nuevo para acercarse al intervalo seleccionado.  
  
-   Para obtener una copia del gráfico actual, haga clic en **copiar a Excel**, a continuación, haga clic en una hoja de cálculo de Excel. Un gráfico se inserta en la hoja con todas las opciones que hubiera establecido, incluida una leyenda.  
  
     Sin embargo, este gráfico es estático para que no se puede editar la leyenda o ver los datos subyacentes; Si tiene una vista más interactiva del gráfico, use el [visores de Visio](viewing-data-mining-models-in-visio-data-mining-add-ins.md).  
  
-   Haga clic en **Abs** en la barra de menús del Visor para cambiar entre curvas absolutas y relativas.  
  
     Esta opción es útil si el gráfico contiene varios modelos pero la escala de los datos de cada modelo es muy distinta.  
  
     Por ejemplo, si los almacenes de la región del Pacífico eran nuevos y las ventas eran bajas, y se utilizan valores absolutos, la línea que muestra las ventas del Pacífico podría parecer plana, dificultando la visualización de los cambios reales, mientras que los otros modelos se muestran en una escala más normal.  
  
     Al cambiar la vista para usar valores relativos, puede normalizar la escala de modelos diferentes y mostrar las diferencias como un porcentaje de cambio. Cuando el cambio es relativo a cada modelo, puede mostrarse en el mismo gráfico sin una distorsión significativa.  
  
 [Explorar el modelo](#bkmk_Top)  
  
###  <a name="bkmk_Model"></a> Modelo  
 Un modelo de predicción también se puede representar como un árbol de decisión o bien, si la serie es básicamente lineal, un modelo de regresión.  
  
 Por ejemplo, en este modelo hay una diferencia en la fórmula de regresión según cierta condición, por lo que el árbol se divide en dos bifurcaciones, cada una con una fórmula de regresión distinta.  
  
 ![Filtrar una única serie en el modelo de pronóstico](media/dm13-forecast-model-northamerica.gif "filtrar una única serie en el modelo de pronóstico")  
  
##### <a name="explore-the-forecasting-model-as-a-tree"></a>Explorar el modelo de predicción como un árbol  
  
1.  Haga clic en el **árbol** lista desplegable lista y elija un modelo para mostrar.  
  
     Se muestra un árbol independiente o un nodo de regresión para cada atributo de predicción. Por ejemplo, si los datos contienen las ventas para Europa, América del Norte y el Pacífico, habría tres modelos distintos, uno para cada serie de datos.  
  
2.  Arrastre el **Mostrar nivel** control deslizante para filtrar los niveles inferiores del árbol y centrarse en las divisiones más importantes.  
  
3.  Haga clic en cada nodo para ver algunas estadísticas descriptivas en el **leyenda de minería de datos**.  
  
     A medida que pausa el mouse sobre un nodo con el mouse, la información sobre herramientas también muestra las mismas estadísticas, así como la fórmula completa que describe el nodo.  
  
4.  Si desea copiar la información de la **leyenda de minería de datos**, haga clic en el **leyenda de minería de datos**, seleccione **copia**y haga clic en la hoja de cálculo de Excel. El **copiar a Excel** opción copia el gráfico, no las estadísticas.  
  
 [Explorar el modelo](#bkmk_Top)  
  
## <a name="see-also"></a>Vea también  
 [Examinar modelos en Excel &#40;complementos de minería de datos de SQL Server&#41;](browsing-models-in-excel-sql-server-data-mining-add-ins.md)  
  
  
