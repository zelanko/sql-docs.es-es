---
title: Explorar el modelo Bayes Naive (tutorial básico de minería de datos) | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: b06708d5-4477-4a51-bf8d-0b1e3c1f9ebb
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: eb35c829b798335a27a37629711acf299ac2c7c9
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "62472889"
---
# <a name="exploring-the-naive-bayes-model-basic-data-mining-tutorial"></a>Explorar el modelo Bayes naive (Tutorial básico de minería de datos)
  El [!INCLUDE[msCoName](../includes/msconame-md.md)] algoritmo Bayes Naive de proporciona varios métodos para mostrar la interacción entre la compra de bicicletas y los atributos de entrada.  
  
 El [!INCLUDE[msCoName](../includes/msconame-md.md)] visor Bayes Naive de proporciona las siguientes pestañas para la exploración de modelos de minería de datos Bayes Naive:  
  
 
  
##  <a name="DependencyNetwork"></a>Red de dependencias  
 La pestaña **red de dependencias** funciona de la misma forma que la pestaña red de [!INCLUDE[msCoName](../includes/msconame-md.md)] **dependencias** del visor de árboles. Cada nodo del visor representa un atributo y las líneas entre los nodos representan relaciones. En el visor, puede ver todos los atributos que afectan al estado del atributo de predicción, Bike Buyer.  
  
#### <a name="to-explore-the-model-in-the-dependency-network-tab"></a>Para explorar el modelo en la pestaña Red de dependencias  
  
1.  Utilice la lista **modelo de minería de datos** en la parte superior de la pestaña visor de modelos de minería de **datos** para cambiar al `TM_NaiveBayes` modelo.  
  
2.  Use la lista de **visores** para cambiar al **visor Bayes Naive de Microsoft**.  
  
3.  Haga clic `Bike Buyer` en el nodo para identificar sus dependencias.  
  
     El sombreado rosa indica que todos los atributos influyen en la compra de bicicletas.  
  
4.  Ajuste el control deslizante para identificar el atributo más influyente.  
  
     Conforme baja el control deslizante, solamente permanecen los atributos que afectan en mayor medida a la columna [Bike Buyer]. Ajustando el control deslizante, puede detectar que algunos de los atributos más influyentes son el número de automóviles que se posee, la distancia al lugar de trabajo y el número total de hijos.  
 
  
##  <a name="AttributeProfiles"></a>Perfiles de atributo  
 La pestaña **perfiles de atributo** describe el modo en que los distintos Estados de los atributos de entrada afectan al resultado del atributo de predicción.  
  
#### <a name="to-explore-the-model-in-the-attribute-profiles-tab"></a>Para explorar el modelo en la pestaña Perfiles del atributo  
  
1.  En el cuadro **predicción** , compruebe que `Bike Buyer` está seleccionado.  
  
2.  Si la **leyenda de minería de datos** está bloqueando la presentación de los **perfiles de atributo**, muévalo fuera del camino.  
  
3.  En el cuadro barras de **histograma** , seleccione **5**.  
  
     En nuestro modelo, 5 es el número máximo de estados para cualquier variable.  
  
     Los atributos que afectan al estado de este atributo de predicción aparecen enumerados junto a los valores de cada estado de los atributos de entrada y sus distribuciones en cada estado del atributo de predicción.  
  
4.  En la columna **atributos** , busque **número de automóviles propiedad**.  Observe las diferencias en los histogramas de los compradores de bicicletas (la columna con la etiqueta 1) y los no compradores (la columna con la etiqueta 0). Una persona que no tenga automóvil o que tenga uno tiene mucha más probabilidad de comprar una bicicleta.  
  
5.  Haga doble clic en la celda **Number Cars propiedad** de la columna Bike Buyer (columna con la etiqueta 1).  
  
     La **leyenda de minería de datos** muestra una vista más detallada.  
  
  
##  <a name="AttributeCharacteristics"></a>Características del atributo  
 Con la pestaña **características del atributo** , puede seleccionar un atributo y un valor para ver la frecuencia con que aparecen los valores de otros atributos en los casos de valor seleccionado.  
  
#### <a name="to-explore-the-model-in-the-attribute-characteristics-tab"></a>Para explorar el modelo en la pestaña Características del atributo  
  
1.  En la lista de **atributos** , compruebe `Bike Buyer` que está seleccionado.  
  
2.  Establezca el **valor** en **1**.  
  
     En el visor, verá que los clientes que no tienen ningún hijo conviviendo con ellos, una distancia corta al trabajo y que viven en la región de Norteamérica tienen más probabilidad de comprar una bicicleta.  
  
  
##  <a name="AttributeDiscrimination"></a>Distinción de atributos  
 Con la pestaña **distinción de atributo** , puede investigar la relación entre dos valores discretos de compra de bicicletas y otros valores de atributo. Dado que `TM_NaiveBayes` el modelo solo tiene dos Estados: 1 y 0, no es necesario realizar ningún cambio en el visor.  
  
 En el visor, podrá ver que las personas que no tienen un automóvil tienden a comprar bicicletas y las personas que tienen dos no suelen comprarlas.  
  
## <a name="related-tasks"></a>Related Tasks  
 Vea los temas siguientes para explorar los demás modelos de minería de datos.  
  
-   [Explorar el modelo de árbol de decisión &#40;tutorial básico de minería de datos&#41;](../../2014/tutorials/exploring-the-decision-tree-model-basic-data-mining-tutorial.md)  
  
-   [Explorar el modelo de agrupación en clústeres &#40;tutorial básico de minería de datos&#41;](../../2014/tutorials/exploring-the-clustering-model-basic-data-mining-tutorial.md)  
  
## <a name="next-lesson"></a>Lección siguiente  
 [Lección 5: probar los modelos &#40;tutorial básico de minería de datos&#41;](../../2014/tutorials/lesson-5-testing-models-basic-data-mining-tutorial.md)  
  
## <a name="previous-task-in-lesson"></a>Tarea anterior de la lección  
 [Explorar el modelo de agrupación en clústeres &#40;tutorial básico de minería de datos&#41;](../../2014/tutorials/exploring-the-clustering-model-basic-data-mining-tutorial.md)  
  
## <a name="see-also"></a>Consulte también  
 [Examinar un modelo usando el visor Bayes Naive de Microsoft](../../2014/analysis-services/data-mining/browse-a-model-using-the-microsoft-naive-bayes-viewer.md)   
 [Pestaña distinción de atributos &#40;visor de modelos de minería de datos&#41;](../../2014/analysis-services/attribute-discrimination-tab-mining-model-viewer.md)   
 [Pestaña perfiles de atributo &#40;el visor de modelos de minería de datos&#41;](../../2014/analysis-services/attribute-profiles-tab-mining-model-viewer.md)   
 [Pestaña características del atributo &#40;visor de modelos de minería de datos&#41;](../../2014/analysis-services/attribute-characteristics-tab-mining-model-viewer.md)   
 [Pestaña red de dependencias &#40;visor de modelos de minería de datos&#41;](../../2014/analysis-services/dependency-network-tab-mining-model-viewer.md)  
  
  
