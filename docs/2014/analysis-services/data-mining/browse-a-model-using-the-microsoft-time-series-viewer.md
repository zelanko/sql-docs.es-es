---
title: Examinar un modelo usando el Visor de Series temporales de Microsoft | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- data mining [Analysis Services], continuous columns
- mining model content, viewing
- Microsoft Time Series Viewer
- charts [Analysis Services]
- Time Series Viewer [Analysis Services]
- continuous columns
- regression algorithms [Analysis Services]
ms.assetid: a77c16cd-1cd0-4fc5-afeb-d1dab30d1e25
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: b05aec565feb655f9c66df928656ecef4bc675f1
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48137565"
---
# <a name="browse-a-model-using-the-microsoft-time-series-viewer"></a>Examinar un modelo usando el Visor de serie temporal de Microsoft
  El Visor de series temporales de [!INCLUDE[msCoName](../../includes/msconame-md.md)] de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] muestra los modelos de minería de datos que se generan con el algoritmo de serie temporal de [!INCLUDE[msCoName](../../includes/msconame-md.md)] . Este algoritmo de [!INCLUDE[msCoName](../../includes/msconame-md.md)] es un algoritmo de regresión que crea modelos de minería de datos para predecir columnas continuas como las ventas de productos, en un escenario de previsión. Estos modelos de serie temporal pueden incluir información basada en algoritmos diferentes:  
  
-   El algoritmo ARTxp, que se optimiza para la predicción a corto plazo.  
  
-   El algoritmo ARIMA, que se optimiza para la predicción a largo plazo.  
  
-   Una mezcla de los algoritmos ARTxp y ARIMA.  
  
 Para obtener más información sobre estos algoritmos, vea [Microsoft Time Series Algorithm](microsoft-time-series-algorithm.md) y [Microsoft Time Series Algorithm Technical Reference](microsoft-time-series-algorithm-technical-reference.md).  
  
> [!NOTE]  
>  Para ver información detallada sobre las ecuaciones utilizadas en el modelo y los modelos que se detectaron, utilice el Visor de árbol de contenido genérico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] . Para obtener más información, vea [Examinar un modelo usando el Visor de árbol de contenido genérico de Microsoft](browse-a-model-using-the-microsoft-generic-content-tree-viewer.md) o [Visor de árbol de contenido genérico de Microsoft &#40;Minería de datos&#41;](../microsoft-generic-content-tree-viewer-data-mining.md).  
  
##  <a name="BKMK_ViewerTabs"></a> Fichas del visor  
 Cuando se explora un modelo de minería de datos en [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], el modelo aparece en la pestaña **Visor de modelos de minería de datos** del visor del diseñador de minería de datos apropiado para el modelo. El Visor de series temporales de [!INCLUDE[msCoName](../../includes/msconame-md.md)] ofrece las siguientes pestañas:  
  
-   [Modelo](#BKMK_Tree)  
  
-   [Gráficos](#BKMK_Charts)  
  
 **Nota** : la información mostrada para el contenido del modelo y en la Leyenda de minería de datos depende del algoritmo que utiliza dicho modelo. Sin embargo, las pestañas **Modelo** y **Gráficos** son iguales independientemente de la mezcla del algoritmo.  
  
###  <a name="BKMK_Tree"></a> Modelo  
 Al generar un modelo de serie temporal, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] presenta el modelo completado como un árbol. Si sus datos contienen varias series de casos, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] genera un árbol independiente para cada serie. Por ejemplo, quiere predecir las ventas para las regiones del Pacífico, América del Norte y Europa. Las predicciones para cada una de estas regiones son series de casos. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] genera un árbol independiente para cada una de estas series. Para ver una serie determinada, selecciónela en la lista **Árbol** .  
  
 Para cada árbol, el modelo de serie temporal contiene un nodo **All** y, a continuación, lo divide en una serie de nodos que representan las estructuras periódicas detectadas por el algoritmo. Puede hacer clic en cada nodo para mostrar estadísticas como el número de casos y la ecuación.  
  
 Si para crear el modelo utilizó ARTxp únicamente, la **Leyenda de minería de datos** para el nodo raíz contiene solo el número total de casos. Para cada nodo no raíz, la **Leyenda de minería de datos** contiene información más detallada sobre la división del árbol (por ejemplo, podría mostrar la ecuación para el nodo y el número de casos). La *regla* en la leyenda contiene información que identifica la serie y el intervalo de tiempo al que se aplica la regla. Por ejemplo, el texto de la leyenda `M200 Europe Amount -2` indica que el nodo representa el modelo para la serie M200 Europe, en un período de hace dos intervalos de tiempo.  
  
 Si para crear el modelo utilizó ARIMA únicamente, la pestaña **Modelo** contiene un único nodo con el título **Todos**. La **Leyenda de minería de datos** para el nodo raíz contiene la ecuación ARIMA.  
  
 Si creó un modelo mixto, el nodo raíz solo contiene el número de casos y la ecuación ARIMA. Después del nodo raíz, el árbol se divide en nodos independientes para cada estructura periódica. Para cada nodo no raíz, la Leyenda de minería de datos contiene los algoritmos ARTxp y ARIMA, la ecuación para el nodo, y el número de casos del nodo. La ecuación ARTxp aparece en primer lugar y se etiqueta como la ecuación del nodo de árbol. A continuación aparece la ecuación ARIMA. Para obtener más información acerca de cómo interpretar esta información, vea [Microsoft Time Series Algorithm Technical Reference](microsoft-time-series-algorithm-technical-reference.md).  
  
 En general, el gráfico del árbol de decisión muestra la división más importante, el nodo **All** , a la izquierda del visor. En los árboles de decisión, la división situada después del nodo **All** es la más importante porque contiene la condición que separa más firmemente los casos en los datos de entrenamiento. En un modelo de serie temporal, la bifurcación principal indica el ciclo periódico más probable. Las divisiones situadas tras el nodo **All** aparecen a la derecha de la rama.  
  
 Puede expandir o contraer nodos individuales en el árbol para mostrar u ocultar las divisiones que ocurren en cada nodo. También puede usar las opciones de la ficha **Árbol de decisión** para influir en el modo en que se muestra el árbol. Use el control deslizante **Mostrar nivel** para ajustar el número de niveles que muestra el árbol. Use **Expansión predeterminada** para configurar el número predeterminado de niveles que van a aparecer en todos los árboles del modelo.  
  
 El sombreado del color de fondo de cada nodo indica el número de casos que existen en el nodo. Para averiguar el número exacto de casos de un nodo, coloque el puntero durante un momento sobre el nodo para que aparezca un recuadro informativo del nodo.  
  
 [Volver al principio](#BKMK_ViewerTabs)  
  
###  <a name="BKMK_Charts"></a> Gráficos  
 La pestaña **Gráficos** contiene un gráfico que muestra el comportamiento del atributo predicho a lo largo del tiempo, junto con cinco valores futuros predichos. El eje vertical del gráfico representa el valor de la serie y el eje horizontal representa el tiempo.  
  
> [!NOTE]  
>  Los intervalos de tiempo utilizados en el eje de tiempo dependen de las unidades que se usan en los datos: podrían representar los días, los meses o incluso los segundos.  
  
 Use el botón **Abs** para cambiar entre curvas absolutas y relativas. Si el gráfico contiene varios modelos, la escala de los datos de cada modelo puede ser muy distinta. Si utiliza una curva absoluta, un modelo puede aparecer como una línea plana, mientras que otro muestra los cambios significativos. Esto ocurre porque la escala de un modelo es mayor que la del otro. Al cambiar a una curva relativa, cambia la escala para mostrar el porcentaje de cambio en lugar de los valores absolutos. Ello hace que resulte más fácil comparar modelos basados en escalas distintas.  
  
 Si el modelo de minería contiene varias series temporales, puede seleccionar una o varias para que se muestren en el gráfico. Solo tiene que hacer clic en la lista situada a la derecha del visor y seleccionar la serie que desea. Si el gráfico se vuelve demasiado complejo, puede filtrar la serie que se muestra si selecciona o desactiva las casillas de la serie en la leyenda.  
  
 El gráfico muestra tanto los datos históricos como los futuros. Los datos futuros aparecen sombreados, para diferenciarlos de los históricos. Los valores de datos aparecen como líneas sólidas para los datos históricos y como líneas de puntos para las predicciones. Para cambiar el color de las líneas que se usan para cada serie, puede establecer las propiedades en [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Para más información, vea [Cambiar los colores usados en los visores de minería de datos](change-the-colors-used-in-the-data-mining-viewer.md).  
  
 Puede ajustar el intervalo de tiempo que aparece en el gráfico mediante las opciones de zoom. También puede ver un intervalo específico de tiempo; para ello, haga clic en el gráfico, arrastre una selección temporal sobre el gráfico y, a continuación, haga clic de nuevo para acercarse al intervalo seleccionado.  
  
 Puede seleccionar el número de **pasos** temporales futuros que desea ver en el modelo mediante **Pasos de predicción**. Si activa la casilla **Mostrar desviaciones** , el visor proporciona barras de error de forma que puede ver el grado de precisión del valor de predicción.  
  
 [Volver al principio](#BKMK_ViewerTabs)  
  
## <a name="see-also"></a>Vea también  
 [Tareas del Visor de modelo de minería de datos y procedimientos](mining-model-viewer-tasks-and-how-tos.md)   
 [Algoritmo de serie temporal de Microsoft](microsoft-time-series-algorithm.md)   
 [Ejemplos de consultas de modelo de serie temporal](time-series-model-query-examples.md)   
 [Visores de modelos de minería de datos](data-mining-model-viewers.md)  
  
  
