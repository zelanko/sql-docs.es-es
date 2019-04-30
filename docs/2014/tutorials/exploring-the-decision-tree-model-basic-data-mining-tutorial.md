---
title: Explorar el modelo de árbol de decisión (Tutorial de minería de datos básicos) | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 2e1472c2-3f3e-4dae-acb3-62fca374d397
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: e7b77b445ff8cbef8be3acb72ef9cdb6fa3af159
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63224597"
---
# <a name="exploring-the-decision-tree-model-basic-data-mining-tutorial"></a>Explorar el modelo de árbol de decisión (tutorial básico de minería de datos)
  El algoritmo de árboles de decisión de [!INCLUDE[msCoName](../includes/msconame-md.md)] predice qué columnas influyen en la decisión de comprar una bicicleta en función de las columnas restantes del conjunto de entrenamiento.  
  

  
##  <a name="Decision_Tree_Tab"></a> Pestaña árbol de decisión  
 En el **árbol de decisión** ficha, puede ver árboles de decisión para cada atributo de predicción en el conjunto de datos.  
  
 En este caso, el modelo predice solo una columna, Bike Buyer, por lo que hay un único árbol para ver. Si hubiera más árboles, podría utilizar el **árbol** para elegir otro árbol.  
  
 Cuando se ve el `TM_Decision_Tree` modelo en el Visor de árbol de decisión, puede ver los atributos más importantes en el lado izquierdo del gráfico. "Más importantes" significa que estos atributos tienen mayor influencia en el resultado. Los atributos situados más abajo en el árbol (a la derecha del gráfico) tiene menos efecto.  
  
 En este ejemplo, la edad es el factor único más importante para predecir la compra de bicicletas. El modelo agrupa los clientes por edad y, a continuación, muestra el siguiente atributo más importante para cada grupo de edad. Por ejemplo, en el grupo de clientes de entre 34 y 40 años, el número de automóviles en propiedad es el factor de predicción más seguro después de la edad.  
  
#### <a name="to-explore-the-model-in-the-decision-tree-tab"></a>Para explorar el modelo en la pestaña Árbol de decisión  
  
1.  Seleccione la pestaña **Visor de modelo de minería de datos** en **Diseñador de minería de datos**.  
  
     De forma predeterminada, el diseñador se abre en el primer modelo que se ha agregado a la estructura, en este caso, `TM_Decision_Tree`.  
  
2.  Utilice los botones de lupa para ajustar el tamaño de presentación del árbol.  
  
     De manera predeterminada, el Visor de árboles de [!INCLUDE[msCoName](../includes/msconame-md.md)] solo muestra los primeros tres niveles del árbol. Si el árbol contiene menos de tres niveles, el visor mostrará solo los niveles existentes. Puede ver más niveles mediante la **Mostrar nivel** control deslizante o el **expansión predeterminada** lista.  
  
3.  Deslice **Mostrar nivel** hasta la cuarta barra.  
  
4.  Cambiar el **en segundo plano** valor `1`.  
  
     Cambiando el **en segundo plano** establecer, puede ver rápidamente el número de casos de cada nodo que tiene el valor de destino `1` para [Bike Buyer]. Recuerde que en este escenario en concreto, cada caso representa un cliente. El valor `1` indica que el cliente compró anteriormente una bicicleta; el valor **0** indica que el cliente no ha comprado una bicicleta. Cuanto más oscuro sea el sombreado del nodo, mayor será el porcentaje de casos del nodo que tienen el valor de destino.  
  
5.  Coloque el cursor sobre el nodo con la etiqueta **todas**. Se mostrará información sobre herramientas con los siguientes datos:  
  
    -   Número total de casos  
  
    -   Número de casos de personas que no han comprado bicicletas  
  
    -   Número de casos de personas que han comprado bicicletas  
  
    -   Número de casos con valores que faltan para [Bike Buyer]  
  
     También puede colocar el cursor sobre cualquier nodo del árbol para ver la condición necesaria para alcanzar ese nodo desde el nodo anterior. También puede ver esta misma información en el **leyenda de minería de datos**.  
  
6.  Haga clic en el nodo de **Age > = 34 y < 41**. El histograma se muestra como una barra horizontal delgada a lo largo del nodo y representa la distribución de los clientes con este intervalo de edad que anteriormente compraron (rosa) o no compraron (azul) una bicicleta. El visor nos muestra que es probable que los clientes con edades comprendidas entre 34 y 40 años sin automóvil o con uno compren una bicicleta. Si vamos un poco más lejos, vemos que la probabilidad de comprar una bicicleta aumenta si el cliente tiene una edad comprendida entre 38 y 40 años.  
  
 Como habilitó la obtención de detalles cuando creó la estructura y el modelo, puede recuperar información detallada de los casos del modelo y de la estructura de minería de datos, incluidas las columnas que no se incluyeron en el modelo de minería de datos (por ejemplo, emailAddress y FirstName).  
  
 Para obtener más información, vea [Consultas de obtención de detalles &#40;minería de datos&#41;](../../2014/analysis-services/data-mining/drillthrough-queries-data-mining.md).  
  
#### <a name="to-drill-through-to-case-data"></a>Para obtener información detallada de los datos del caso  
  
1.  Haga clic en un nodo y seleccione **Drill Through** , a continuación, **solo columnas de modelos**.  
  
     Los detalles de cada caso de entrenamiento se muestran en formato de hoja de cálculo. Estos detalles proceden de la vista vTargetMail que seleccionó como la tabla de casos al generar la estructura de minería de datos.  
  
2.  Haga clic en un nodo y seleccione **Drill Through** , a continuación, **columnas de modelo y estructura**.  
  
     Se muestra la misma hoja de cálculo con las columnas de estructura anexadas al final.  
  
  
###  <a name="Dependency_Network_Tab"></a> Pestaña red de dependencias  
 El **red de dependencias** ficha muestra las relaciones entre los atributos que contribuyen a la capacidad de predicción del modelo de minería de datos. El visor Red de dependencias reafirma nuestra conclusión de que la edad y la región son factores importantes para predecir la compra de bicicletas.  
  
##### <a name="to-explore-the-model-in-the-dependency-network-tab"></a>Para explorar el modelo en la pestaña Red de dependencias  
  
1.  Haga clic en el `Bike Buyer` nodo para identificar sus dependencias.  
  
     El nodo central de la red de dependencias, `Bike Buyer`, representa el atributo de predicción del modelo de minería de datos. En el gráfico se resaltan todos los nodos conectados que afectan al atributo de predicción.  
  
2.  Ajustar el **todos los vínculos** control deslizante para identificar el atributo más influyente.  
  
     Al arrastrar hacia abajo el control deslizante, los atributos que tengan solo un efecto débil en la columna [Bike Buyer] se quitan del gráfico. Ajustando el control deslizante, descubrirá que la edad y la región son los factores más importantes para predecir si alguien va a comprar una bicicleta.  
  
## <a name="related-tasks"></a>Related Tasks  
 Vea estos temas para explorar los datos con las demás clases de modelos.  
  
-   [Explorar el modelo de agrupación en clústeres &#40;Tutorial de minería de datos básicos&#41;](../../2014/tutorials/exploring-the-clustering-model-basic-data-mining-tutorial.md)  
  
-   [Explorar el modelo Bayes Naive &#40;Tutorial de minería de datos básicos&#41;](../../2014/tutorials/exploring-the-naive-bayes-model-basic-data-mining-tutorial.md)  
  
## <a name="next-task-in-lesson"></a>Siguiente tarea de la lección  
 [Explorar el modelo de agrupación en clústeres &#40;Tutorial de minería de datos básicos&#41;](../../2014/tutorials/exploring-the-clustering-model-basic-data-mining-tutorial.md)  
  
## <a name="see-also"></a>Vea también  
 [Tareas y procedimientos del Visor de modelos de minería de datos](../../2014/analysis-services/data-mining/mining-model-viewer-tasks-and-how-tos.md)   
 [Pestaña árbol de decisión &#40;Visor de modelos de minería de datos&#41;](../../2014/analysis-services/decision-tree-tab-mining-model-viewer.md)   
 [Pestaña red de dependencias &#40;Visor de modelos de minería de datos&#41;](../../2014/analysis-services/dependency-network-tab-mining-model-viewer.md)   
 [Examinar un modelo usando el Visor de árboles de Microsoft](../../2014/analysis-services/data-mining/browse-a-model-using-the-microsoft-tree-viewer.md)  
  
  
