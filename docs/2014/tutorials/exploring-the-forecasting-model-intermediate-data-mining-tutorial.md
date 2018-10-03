---
title: Explorar el modelo de previsión (Tutorial de minería de datos intermedios) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: 0a00f409-050f-4b92-9763-ba31a6aa3052
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 4ff9743774a9c05f4369cb2d24fde592bf011225
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48151021"
---
# <a name="exploring-the-forecasting-model-intermediate-data-mining-tutorial"></a>Explorar el modelo de previsión (tutorial intermedio de minería de datos)
  Ahora que ha creado el modelo de minería de datos de pronóstico, puede explorar los resultados utilizando la **Visor de modelos de minería de datos** ficha del Diseñador de minería de datos. El [!INCLUDE[msCoName](../includes/msconame-md.md)] Visor de Series temporales contiene dos pestañas: **gráficos** y **modelo**.  
  
 Además, puede usar el visor de árboles genérico de Microsoft con todos los modelos. Cada vista presenta una imagen ligeramente diferente de la información del modelo de series temporales.  
  
-   [Pestaña gráficos](#bkmk_Charts)  
  
-   [Pestaña modelo](#bkmk_Model)  
  
-   [Visor de contenido genérico de Microsoft](#bkmk_Content)  
  
##  <a name="bkmk_Charts"></a> Pestaña gráficos  
 El **gráficos** pestaña de la [!INCLUDE[msCoName](../includes/msconame-md.md)] Visor de Series temporales gráfica cada una de las series, incluidos los datos históricos y predicciones. Cada línea del gráfico de serie temporal representa una combinación única de producto, región y atributo de predicción.  
  
 La leyenda del lado derecho del visor muestra las series temporales disponibles, basándose en las selecciones en la lista desplegable. Puede activar y desactivar las casillas de la leyenda para controlar las series temporales que se muestran en el gráfico.  
  
 También puede cambiar las opciones de presentación, como los colores que se utilizan en cada serie temporal, o si los valores se muestran en puntos del gráfico.  
  
#### <a name="to-select-a-time-series"></a>Para seleccionar una serie temporal  
  
1.  Haga clic en el **gráficos** pestaña de la **Visor de modelos de minería de datos** ficha, si no está visible.  
  
2.  Haga clic en la lista desplegable situada a la derecha de la vista del gráfico y seleccione todas las casillas. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
     El gráfico debe contener ahora 24 líneas de series diferentes.  
  
3.  En las casillas situadas a la derecha del gráfico, desactive las casillas para ocultar temporalmente las líneas de todas las series relacionadas con Amount.  
  
     A continuación, desactive las casillas relacionadas con las bicicletas R250 y R750.  
  
     Ahora el gráfico contiene únicamente las seis líneas de serie siguientes, lo que le permite comparar con mayor facilidad las bicicletas T1000 y M200.  
  
    -   **M200 Europe: Quantity**  
  
    -   **M200 Norteamérica: cantidad**  
  
    -   **M200 Pacífico: cantidad**  
  
    -   **T1000 Europe: Quantity**  
  
    -   **T1000 Norteamérica: cantidad**  
  
    -   **T1000 Pacífico: cantidad**  
  
 ![Serie que predice la cantidad de M200 y T1000](../../2014/tutorials/media/6series-defaultforecasting.gif "serie que predice la cantidad de M200 y T1000")  
  
 El gráfico que se muestra en el visor incluye datos históricos y previstos. Los datos previstos aparecen sombreados para diferenciarlos de los históricos. Para que resulte más sencillo comparar series diferentes, también puede cambiar los colores asociados a cada línea del gráfico. Para más información, vea [Cambiar los colores usados en los visores de minería de datos](../../2014/analysis-services/data-mining/change-the-colors-used-in-the-data-mining-viewer.md).  
  
 A partir de las líneas de tendencia, puede ver que las ventas totales de todas las regiones están aumentando en general, y que alcanzan su valor más alto cada 12 meses, en diciembre. A partir del gráfico, también puede constatar que los datos de la bicicleta T1000 comienzan mucho más tarde que los datos de otras series de productos. Esto se debe a que es un producto más reciente, pero dado que esta serie se basa en menos datos, las predicciones podrían no ser tan precisas.  
  
 De forma predeterminada, en cada serie temporal se muestran cinco pasos de predicción, que aparecen como líneas de puntos. Este valor se puede modificar para ver más o menos predicciones. También se puede ver de forma gráfica la desviación estándar de las predicciones mediante la incorporación de barras de error al gráfico.  
  
#### <a name="to-change-prediction-and-display-options-in-the-chart-view"></a>Para cambiar las opciones de predicción y presentación de la vista Gráfico  
  
1.  Intente cambiar el valor de **pasos de predicción** aumentándolo de **5** a **10**y luego volver a **6**.  
  
     Cuando los datos históricos tienen una gran fluctuación, las fluctuaciones tienden a repetirse o incluso a amplificarse a medida que aumenta el número de predicciones. Probablemente necesitará investigar este aspecto para entender la causa del mayor aumento de datos históricos y decidir si desea aceptar estos resultados, buscar algún tipo de corrección de los datos de origen o aplicar algún tipo de suavizado en el modelo.  
  
2.  Seleccione el **mostrar desviaciones** casilla de verificación.  
  
     Esta opción muestra el error estimado para cada valor previsto.  
  
3.  Tenga en cuenta la escala del eje X. Los cambios en los datos históricos y previstos se expresan siempre como porcentaje, pero los valores reales se ajustan automáticamente para dar cabida a todos los valores del gráfico. Por consiguiente, al comparar modelos debe tener cuidado de no confiar solamente en las representaciones visuales. Para obtener exactamente el valor, o el aumento de porcentaje y el valor para las predicciones, sitúe el mouse sobre la línea de puntos o las líneas llenas, o haga clic en las líneas para ver los valores en el **leyenda de minería de datos**.  
  
     **Sugerencia**: si el **leyenda de minería de datos** no está visible, cambie a **modelo** ver, haga clic en cualquier nodo y seleccione **Mostrar leyenda**.  
  
 Al observar estas tendencias, le preocupa la ausencia de datos para una parte de la serie y se pregunta si puede obtener predicciones más confiables calculando el promedio de ventas por modelo o quizás el promedio de ventas por región. Explorará este método en una lección posterior de este tutorial.  
  
 [Volver al principio](#bkmk_Charts)  
  
##  <a name="bkmk_Model"></a> Pestaña modelo  
 El **modelo** pestaña de la [!INCLUDE[msCoName](../includes/msconame-md.md)] Visor de Series temporales en el Diseñador de minería de datos le permite ver el modelo de previsión en forma de un gráfico de árbol.  
  
 Primero, observe que, debido a que los datos describen dos medidas distintas (importe y cantidad) para las ventas de varias líneas de productos (T1000, etc.) de tres regiones diferentes (Europa, Norteamérica y el Pacífico), el modelo que creó contiene realmente 24 árboles distintos. Cada árbol representa un modelo de patrones de venta para una combinación diferente de región, producto y atributo de predicción.  
  
 Puede elegir qué combinación de la línea de productos, región y ventas métrica que desea ver seleccionando una serie de la **árbol** lista desplegable el **modelo** ficha.  
  
 ¿Qué puede saber al ver el modelo como un árbol? Por ejemplo, comparemos dos modelos, uno con varios niveles del árbol y otro que tiene un único nodo.  
  
-   Cuando un gráfico de árbol contiene un solo nodo, significa que la tendencia encontrada en el modelo es básicamente homogénea en el tiempo. Puede usar este nodo único, etiquetado **todas**, para ver la fórmula que describe la relación entre las variables de entrada y el resultado.  
  
-   Cuando un gráfico de árbol para una serie temporal tiene varias bifurcaciones, significa que la serie temporal que se detectó es demasiado compleja para representarse como una sola ecuación. En su lugar, el gráfico de árbol puede contener varias bifurcaciones, cada bifurcación etiquetada con las condiciones que ha provocado el árbol para *dividir*. Cuando se divide el árbol, cada bifurcación representa un segmento de tiempo diferente, en el que la tendencia puede describirse como una sola ecuación.  
  
     Por ejemplo, si mira el gráfico y ve un salto súbito en el volumen de ventas a partir de algún día de septiembre y continúa hasta las vacaciones Navidad, puede cambiar a la **modelo** vista para ver la fecha exacta donde cambió la tendencia. Las bifurcaciones del árbol que representan 'antes de septiembre' y 'después de septiembre' contendrían fórmulas diferentes: una fórmula que describe matemáticamente las tendencias de ventas hasta la división y otra fórmula que describe las tendencias de ventas de septiembre hasta las vacaciones de Navidad.  
  
#### <a name="to-explore-the-decision-tree-for-a-time-series-model"></a>Para explorar el árbol de decisión de un modelo de series temporales  
  
1.  En el **árbol** lista el **modelo** ficha del Visor, seleccione el **T1000 Europe: cantidad** serie.  
  
     Haga clic en el nodo con la etiqueta **todas**.  
  
     Para un **todas** nodo, la información sobre herramientas que aparece incluye información como el número de casos de las series completas y las ecuaciones de series temporales derivan del análisis de los datos.  
  
2.  Si el **leyenda de minería de datos** no está visible, haga clic en el nodo y seleccione **Mostrar leyenda**.  
  
     El **leyenda de minería de datos** proporciona casi la misma información que se encuentra en la información sobre herramientas. Si ninguna de las variables independientes son discretas, también aparecerá un histograma que muestra la distribución de variables en el nodo.  
  
3.  Ahora seleccione una serie temporal diferente para verla. Mediante el **árbol** lista el **modelo** ficha del Visor, seleccione el **M200 North America: cantidad** serie.  
  
     El gráfico de árbol contiene ahora un **todas** nodo y dos nodos secundarios. Si examina las etiquetas de los nodos secundarios, puede saber en qué momento cambió la línea de tendencia.  
  
     Para cada nodo secundario, la descripción en el **leyenda de minería de datos** también incluye el recuento de casos de cada rama del árbol.  
  
 En la siguiente lista se describen algunas características adicionales del visor de árbol:  
  
-   Puede cambiar la variable que se representa en el gráfico utilizando el **en segundo plano** control. De forma predeterminada, los nodos que son más oscuros contienen más casos, dado que el valor de **en segundo plano** está establecido en **rellenado**. Para ver solo cuántos casos hay en un nodo, sitúe el mouse sobre un nodo y ver la información sobre herramientas que aparece, o haga clic en el nodo y ver los números de la **leyenda del nodo** ventana.  
  
-   La fórmula de regresión para el nodo se puede ver también en la información sobre herramientas o haciendo clic en el nodo. Si ha creado un modelo mixto, puede ver dos fórmulas, una para ARTXP (en los nodos hoja) y otra para el modelo ARIMA (en el nodo raíz del árbol).  
  
-   Los pequeños rombos se usan en los nodos que representan números continuos. El rango de atributos se muestra en la barra en la que se basa el rombo. El rombo está centrado en medio del nodo y su ancho representa la varianza del atributo en ese nodo.  
  
 [Volver al principio](#bkmk_Charts)  
  
##  <a name="bkmk_Content"></a> (Opcional) Visor de árbol de contenido genérico  
 Además del visor personalizado de serie temporal, [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] proporciona el **MicrosoftGeneric Visor de árbol de contenido** para su uso con todos los modelos de minería de datos. Este visor proporciona algunas ventajas:  
  
-   **Visor de Series temporales de Microsoft**: esta vista combina los resultados de los dos algoritmos. Aunque puede ver cada serie por separado, no puede determinar cómo se combinan los resultados de cada algoritmo. Asimismo, en esta vista, la información sobre herramientas y la leyenda de minería de datos muestran solo las estadísticas más importantes.  
  
-   **Visor de árbol de contenido genérico**: le permite examinar y ver todas las series de datos que se usaron en el modelo al mismo tiempo y si ha creado una combinación de modelo, tanto el ARIMA y se muestran los árboles ARTXP en el mismo gráfico.  
  
     Puede usar este visor para obtener todas las estadísticas de ambos algoritmos, así como las asignaciones de los valores.  
  
     Recomendado para usuarios avanzados de minería de datos que desean conocer más información sobre los análisis de ARIMA y ARTXP.  
  
#### <a name="to-view-details-for-a-particular-data-series-in-the-generic-content-viewer"></a>Para ver los detalles de una determinada serie de datos en el visor de contenido genérico  
  
1.  En el **Visor de modelos de minería de datos** ficha, seleccione **Visor de árbol de contenido genérico de Microsoft** desde el **Visor** lista desplegable.  
  
2.  En el **título del nodo** panel, haga clic en el primer nodo (todos).  
  
3.  En el **detalles del nodo** panel, vea el valor de ATTRIBUTE_NAME.  
  
     Este valor indica qué serie, o qué combinación de producto y región, está incluida en este nodo. En el ejemplo de AdventureWorks, el primer nodo es el de la serie M200 Europe.  
  
4.  En el **título del nodo** panel, busque el primer nodo que tiene nodos secundarios.  
  
     Si un nodo de serie tiene nodos secundarios, la vista de árbol que aparece en el **modelo** ficha del Visor de Series temporales de Microsoft también tendrá una estructura de bifurcación.  
  
5.  Expanda el nodo y haga clic en uno de los nodos secundarios.  
  
     La columna NODE_DESCRIPTION del esquema contiene la condición que hizo que el árbol se dividiera.  
  
6.  En el **título del nodo** panel, haga clic en el primer nodo de ARIMA y expanda el nodo hasta que todos los nodos secundarios están visibles.  
  
7.  En el **detalles del nodo** panel, vea el valor de ATTRIBUTE_NAME.  
  
     Este valor indica qué serie temporal está incluida en este nodo. El primer nodo de la sección ARIMA debería coincidir con el primer nodo de la sección (Todos). En el ejemplo de AdventureWorks, este nodo contiene el análisis ARIMA de la serie M200 Europa.  
  
 Para más información, vea [Contenido del modelo de minería de datos para los modelos de serie temporal &#40;Analysis Services - Minería de datos&#41;](../../2014/analysis-services/data-mining/mining-model-content-for-time-series-models-analysis-services-data-mining.md).  
  
 [Volver al principio](#bkmk_Charts)  
  
## <a name="next-task-in-lesson"></a>Siguiente tarea de la lección  
 [Crear predicciones de serie temporal &#40;intermedio de Tutorial de minería de datos&#41;](../../2014/tutorials/creating-time-series-predictions-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>Vea también  
 [Ejemplos de consultas de modelo de serie temporal](../../2014/analysis-services/data-mining/time-series-model-query-examples.md)   
 [Referencia técnica del algoritmo de serie temporal de Microsoft](../../2014/analysis-services/data-mining/microsoft-time-series-algorithm-technical-reference.md)  
  
  
