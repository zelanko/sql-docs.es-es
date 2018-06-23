---
title: Explorar el modelo de Bayes Naive (Tutorial de minería de datos básicos) | Documentos de Microsoft
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: b06708d5-4477-4a51-bf8d-0b1e3c1f9ebb
caps.latest.revision: 25
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: ce01a9d352513e4b69bb4a9e735f30cc657a9c97
ms.sourcegitcommit: 8c040e5b4e8c7d37ca295679410770a1af4d2e1f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/21/2018
ms.locfileid: "36311863"
---
# <a name="exploring-the-naive-bayes-model-basic-data-mining-tutorial"></a>Explorar el modelo Bayes naive (Tutorial básico de minería de datos)
  El [!INCLUDE[msCoName](../includes/msconame-md.md)] algoritmo Bayes Naive proporciona varios métodos para mostrar la interacción entre los atributos de entrada y compra de bicicletas.  
  
 El [!INCLUDE[msCoName](../includes/msconame-md.md)] Visor Bayes Naive ofrece las siguientes pestañas para explorar los modelos de minería de datos Bayes Naive:  
  
 
  
##  <a name="DependencyNetwork"></a> Red de dependencias  
 El **red de dependencias** pestaña funciona de la misma manera que el **red de dependencias** pestaña para el [!INCLUDE[msCoName](../includes/msconame-md.md)] Visor de árbol. Cada nodo del visor representa un atributo y las líneas entre los nodos representan relaciones. En el visor, puede ver todos los atributos que afectan al estado del atributo de predicción, Bike Buyer.  
  
#### <a name="to-explore-the-model-in-the-dependency-network-tab"></a>Para explorar el modelo en la pestaña Red de dependencias  
  
1.  Use la **Mining Model** lista en la parte superior de la **Visor de modelos de minería de datos** ficha para cambiar a la `TM_NaiveBayes` modelo.  
  
2.  Use la **Visor** lista para cambiar a **Visor Bayes Naive de Microsoft**.  
  
3.  Haga clic en el `Bike Buyer` nodo para identificar sus dependencias.  
  
     El sombreado rosa indica que todos los atributos influyen en la compra de bicicletas.  
  
4.  Ajuste el control deslizante para identificar el atributo más influyente.  
  
     Conforme baja el control deslizante, solamente permanecen los atributos que afectan en mayor medida a la columna [Bike Buyer]. Ajustando el control deslizante, puede detectar que algunos de los atributos más influyentes son el número de automóviles que se posee, la distancia al lugar de trabajo y el número total de hijos.  
 
  
##  <a name="AttributeProfiles"></a> Perfiles del atributo  
 El **perfiles del atributo** ficha describe cómo los diferentes Estados del efecto de los atributos de entrada el resultado del atributo de predicción.  
  
#### <a name="to-explore-the-model-in-the-attribute-profiles-tab"></a>Para explorar el modelo en la pestaña Perfiles del atributo  
  
1.  En el **Predictable** cuadro, compruebe que `Bike Buyer` está seleccionada.  
  
2.  Si el **leyenda de minería de datos** está bloqueando la presentación de la **perfiles del atributo**, muévalo fuera de la vista.  
  
3.  En el **histograma** cuadro de barras, seleccione **5**.  
  
     En nuestro modelo, 5 es el número máximo de estados para cualquier variable.  
  
     Los atributos que afectan al estado de este atributo de predicción aparecen enumerados junto a los valores de cada estado de los atributos de entrada y sus distribuciones en cada estado del atributo de predicción.  
  
4.  En el **atributos** columna, buscar **Number Cars Owned**.  Observe las diferencias en los histogramas de los compradores de bicicletas (la columna con la etiqueta 1) y los no compradores (la columna con la etiqueta 0). Una persona que no tenga automóvil o que tenga uno tiene mucha más probabilidad de comprar una bicicleta.  
  
5.  Haga doble clic en el **Number Cars Owned** celda de la bicicleta columna (columna con la etiqueta 1).  
  
     El **leyenda de minería de datos** muestra una vista más detallada.  
  
  
##  <a name="AttributeCharacteristics"></a> Características del atributo  
 Con el **características del atributo** ficha, puede seleccionar un atributo y un valor para averiguar con qué frecuencia aparecen los valores para otros atributos en el caso de los valores seleccionados.  
  
#### <a name="to-explore-the-model-in-the-attribute-characteristics-tab"></a>Para explorar el modelo en la pestaña Características del atributo  
  
1.  En el **atributo** lista, compruebe que `Bike Buyer` está seleccionada.  
  
2.  Establecer el **valor** a **1**.  
  
     En el visor, verá que los clientes que no tienen ningún hijo conviviendo con ellos, una distancia corta al trabajo y que viven en la región de Norteamérica tienen más probabilidad de comprar una bicicleta.  
  
  
##  <a name="AttributeDiscrimination"></a> Distinción del atributo  
 Con el **distinción del atributo** ficha, puede investigar la relación entre dos valores discretos de compra de bicicletas y otros valores de atributo. Dado que el `TM_NaiveBayes` modelo tiene sólo dos Estados, 1 y 0, no es necesario realizar ningún cambio en el Visor.  
  
 En el visor, podrá ver que las personas que no tienen un automóvil tienden a comprar bicicletas y las personas que tienen dos no suelen comprarlas.  
  
## <a name="related-tasks"></a>Related Tasks  
 Vea los temas siguientes para explorar los demás modelos de minería de datos.  
  
-   [Explorar el modelo de árbol de decisión &#40;Tutorial de minería de datos básicos&#41;](../../2014/tutorials/exploring-the-decision-tree-model-basic-data-mining-tutorial.md)  
  
-   [Explorar el modelo de agrupación en clústeres &#40;Tutorial de minería de datos básicos&#41;](../../2014/tutorials/exploring-the-clustering-model-basic-data-mining-tutorial.md)  
  
## <a name="next-lesson"></a>Lección siguiente  
 [Lección 5: Probar los modelos &#40;Tutorial de minería de datos básicos&#41;](../../2014/tutorials/lesson-5-testing-models-basic-data-mining-tutorial.md)  
  
## <a name="previous-task-in-lesson"></a>Tarea anterior de la lección  
 [Explorar el modelo de agrupación en clústeres &#40;Tutorial de minería de datos básicos&#41;](../../2014/tutorials/exploring-the-clustering-model-basic-data-mining-tutorial.md)  
  
## <a name="see-also"></a>Vea también  
 [Examinar un modelo usando el Visor Bayes Naive de Microsoft](../../2014/analysis-services/data-mining/browse-a-model-using-the-microsoft-naive-bayes-viewer.md)   
 [Pestaña distinción del atributo &#40;Visor de modelos de minería de datos&#41;](../../2014/analysis-services/attribute-discrimination-tab-mining-model-viewer.md)   
 [Atributo perfiles pestaña &#40;Visor de modelos de minería de datos&#41;](../../2014/analysis-services/attribute-profiles-tab-mining-model-viewer.md)   
 [Pestaña características del atributo &#40;Visor de modelos de minería de datos&#41;](../../2014/analysis-services/attribute-characteristics-tab-mining-model-viewer.md)   
 [Pestaña red de dependencias &#40;Visor de modelos de minería de datos&#41;](../../2014/analysis-services/dependency-network-tab-mining-model-viewer.md)  
  
  