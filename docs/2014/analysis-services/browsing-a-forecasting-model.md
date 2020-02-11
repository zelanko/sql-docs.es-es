---
title: Examinar un modelo de previsión | Microsoft Docs
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "66088488"
---
# <a name="browsing-a-forecasting-model"></a>Examinar un modelo de pronóstico
  Al abrir un modelo de previsión mediante **examinar**, el modelo se muestra en un visor interactivo, similar al visor de modelos de serie temporal de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. El visor sirve para explorar las tendencias, comparar series, crear predicciones y obtener información sobre el modelo y los datos subyacentes.  
  
##  <a name="bkmk_Top"></a>Explorar el modelo  
 El visor de **búsqueda** de modelos de predicción proporciona una vista de gráfico, que muestra las tendencias a lo largo del tiempo y permite crear predicciones, y una vista de modelo, que representa la serie temporal como un árbol de decisión o un árbol de regresión.  
  
-   [Vista de gráfico](#bkmk_charts)  
  
-   [Vista de modelo](#bkmk_Model)  
  
 Para experimentar con un modelo de predicción, puede utilizar los datos de ejemplo de la pestaña Previsión del libro de datos de ejemplo y generar un modelo de serie temporal mediante el [Asistente para previsión &#40;complementos de minería de datos para excel&#41;](forecast-wizard-data-mining-add-ins-for-excel.md) en la cinta de opciones **minería de datos** o [previsión &#40;herramientas de análisis de tabla para Excel&#41;](forecast-table-analysis-tools-for-excel.md) en la cinta de opciones **analizar** .  
  
###  <a name="bkmk_charts"></a>Gráfica  
 La pestaña **gráfico** muestra la tendencia de la serie de datos a lo largo del tiempo, junto con los valores de predicción. El eje vertical del gráfico representa los valores de la serie y el eje horizontal representa el tiempo.  
  
##### <a name="explore-the-forecasting-chart"></a>Explorar el gráfico de predicción  
  
1.  Este modelo contiene varias series temporales pero, para simplificar el gráfico, puede mostrar una sola serie o algunas series relacionadas.  
  
     ![predicciones históricas en el modelo de predicción](media/dm13-forecast-chart-historicpredictions.gif "predicciones históricas en el modelo de predicción")  
  
     Utilice las casillas para seleccionar la predicción solo para Norteamérica y solo para la cantidad de ventas.  
  
2.  Haga clic en **pasos de predicción** y escriba un nuevo valor para controlar cuántos valores de hora futuros desea ver en el gráfico.  
  
     El valor predeterminado es 5.  
  
3.  Haga clic en cualquier punto de la línea, ya sea historial o futuro, para ver los valores exactos de ese momento en el tiempo, que se muestra en la **leyenda de minería de datos**.  
  
4.  El gráfico muestra tanto los datos históricos como los futuros. Observe la línea de puntos con un fondo sombreado. Estos valores son las predicciones futuras, según el modelo.  
  
     Los datos históricos (que usó para generar el modelo) se muestran en el lado izquierdo del gráfico.  
  
5.  Seleccione la opción **Mostrar predicciones históricas** para tener una idea de la estabilidad de la serie temporal.  
  
     ![predicciones para una única serie del modelo](media/dm13-forecast-chart-singleseries.gif "predicciones para una única serie del modelo")  
  
     Las predicciones históricas son los valores previstos en función de las series hasta ese punto, que se comparan con los valores históricos reales. Si la línea de puntos (con los valores previstos) se aparta de la línea continua (los valores reales), significa que la primera parte de la serie quizás no predice con precisión los valores posteriores. Podría necesitar más datos o podría ser simplemente un indicador de la volatilidad en el ciclo.  
  
6.  Seleccione la opción **Mostrar desviaciones** para mostrar las barras de error en el gráfico.  
  
     Las barras de error permiten evaluar visualmente la variabilidad de las predicciones. La calidad de las predicciones varía en función de los datos de origen pero a medida que aumenta el número de pasos de predicción, debería ver las desviaciones en constante aumento.  
  
 **Útiles**  
  
-   Para alternar la presentación de la **leyenda de minería de datos**, haga clic con el botón secundario en cualquier punto del gráfico.  
  
     Puede ver un intervalo específico de tiempo; para ello, haga clic en el gráfico, arrastre una selección temporal sobre el gráfico y, a continuación, haga clic de nuevo para acercarse al intervalo seleccionado.  
  
-   Para obtener una copia del gráfico actual, haga clic en **copiar a Excel**y, a continuación, haga clic en una hoja de cálculo en Excel. Un gráfico se inserta en la hoja con todas las opciones que hubiera establecido, incluida una leyenda.  
  
     Sin embargo, este gráfico es estático, por lo que no se puede editar la leyenda ni ver los datos subyacentes. Si necesita una vista de gráfico más interactiva, use los [visores de Visio](viewing-data-mining-models-in-visio-data-mining-add-ins.md).  
  
-   Haga clic en **ABS** en la barra de menús del visor para alternar entre las curvas absolutas y relativas.  
  
     Esta opción es útil si el gráfico contiene varios modelos pero la escala de los datos de cada modelo es muy distinta.  
  
     Por ejemplo, si los almacenes de la región del Pacífico eran nuevos y las ventas eran bajas, y se utilizan valores absolutos, la línea que muestra las ventas del Pacífico podría parecer plana, dificultando la visualización de los cambios reales, mientras que los otros modelos se muestran en una escala más normal.  
  
     Al cambiar la vista para usar valores relativos, puede normalizar la escala de modelos diferentes y mostrar las diferencias como un porcentaje de cambio. Cuando el cambio es relativo a cada modelo, puede mostrarse en el mismo gráfico sin una distorsión significativa.  
  
 [Explorar el modelo](#bkmk_Top)  
  
###  <a name="bkmk_Model"></a>Modela  
 Un modelo de predicción también se puede representar como un árbol de decisión o bien, si la serie es básicamente lineal, un modelo de regresión.  
  
 Por ejemplo, en este modelo hay una diferencia en la fórmula de regresión según cierta condición, por lo que el árbol se divide en dos bifurcaciones, cada una con una fórmula de regresión distinta.  
  
 ![Filtrar una única serie del modelo de predicción](media/dm13-forecast-model-northamerica.gif "Filtrar una única serie del modelo de predicción")  
  
##### <a name="explore-the-forecasting-model-as-a-tree"></a>Explorar el modelo de predicción como un árbol  
  
1.  Haga clic en la lista desplegable **árbol** y elija el modelo que desea mostrar.  
  
     Se muestra un árbol independiente o un nodo de regresión para cada atributo de predicción. Por ejemplo, si los datos contienen las ventas para Europa, América del Norte y el Pacífico, habría tres modelos distintos, uno para cada serie de datos.  
  
2.  Arrastre el control deslizante **Mostrar nivel** para filtrar los niveles inferiores del árbol y céntrese en las divisiones más importantes.  
  
3.  Haga clic en cada nodo para ver algunas estadísticas descriptivas en la **leyenda de minería de datos**.  
  
     A medida que pausa el mouse sobre un nodo con el mouse, la información sobre herramientas también muestra las mismas estadísticas, así como la fórmula completa que describe el nodo.  
  
4.  Si desea copiar la información de la leyenda de **minería de datos**, haga clic con el botón secundario en la **leyenda de minería de datos**, seleccione **copiar**y haga clic dentro de la hoja de cálculo de Excel. La opción **Copiar en Excel** copia el gráfico, no las estadísticas.  
  
 [Explorar el modelo](#bkmk_Top)  
  
## <a name="see-also"></a>Consulte también  
 [Examinar modelos en Excel &#40;SQL Server complementos de minería de datos&#41;](browsing-models-in-excel-sql-server-data-mining-add-ins.md)  
  
  
