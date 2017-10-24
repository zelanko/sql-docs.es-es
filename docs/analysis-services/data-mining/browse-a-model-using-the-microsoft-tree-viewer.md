---
title: "Examinar un modelo usando el Visor de árboles de Microsoft | Documentos de Microsoft"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Tree Viewer [Analysis Services]
- predictions [Analysis Services], discrete attributes
- mining model content, viewing
- predictions [Analysis Services], continuous attributes
- mining legend [Analysis Services]
- discrete attributes [Analysis Services]
- Microsoft Decision Trees algorithm [Analysis Services]
- decision tree algorithms [Analysis Services]
- Microsoft Tree Viewer
- decision trees [Analysis Services]
- dependencies [Analysis Services]
- continuous attributes
ms.assetid: 0c96d518-ed20-40b7-8d62-b26ad6244287
caps.latest.revision: 46
author: Minewiskan
ms.author: owend
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: cf93bd7a9be8f6de5e4f807730fcaa4bcb60ab5c
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="browse-a-model-using-the-microsoft-tree-viewer"></a>Examinar un modelo usando el Visor de árboles de Microsoft
  El Visor de árboles de [!INCLUDE[msCoName](../../includes/msconame-md.md)] en [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] muestra los árboles de decisión que se generan con el algoritmo de árboles de decisión de [!INCLUDE[msCoName](../../includes/msconame-md.md)] . El algoritmo de árboles de decisión de [!INCLUDE[msCoName](../../includes/msconame-md.md)] es un algoritmo del árbol de decisión híbrido que admite clasificación y regresión. Por consiguiente, también puede usar este visor para ver modelos basados en el algoritmo de regresión lineal de [!INCLUDE[msCoName](../../includes/msconame-md.md)] . El algoritmo de árboles de decisión de [!INCLUDE[msCoName](../../includes/msconame-md.md)] se usa para el modelo de predicción de los atributos discretos y continuos. Para obtener más información acerca de este algoritmo, vea [Microsoft Decision Trees Algorithm](../../analysis-services/data-mining/microsoft-decision-trees-algorithm.md).  
  
> [!NOTE]  
>  Para ver información detallada sobre las ecuaciones utilizadas en el modelo y los modelos que se detectaron, utilice el Visor de árbol de contenido genérico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] . Para más información, vea [Examinar un modelo usando el Visor de árbol de contenido genérico de Microsoft](../../analysis-services/data-mining/browse-a-model-using-the-microsoft-generic-content-tree-viewer.md) o [Visor de árbol de contenido genérico de Microsoft &#40;Minería de datos&#41;](http://msdn.microsoft.com/library/751b4393-f6fd-48c1-bcef-bdca589ce34c).  
  
##  <a name="BKMK_TabsPanes"></a> Fichas del visor  
 Cuando se explora un modelo de minería de datos en [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], el modelo aparece en la pestaña **Visor de modelos de minería de datos** del visor del diseñador de minería de datos apropiado para el modelo. El Visor de árboles de [!INCLUDE[msCoName](../../includes/msconame-md.md)] incluye los siguientes paneles y pestañas:  
  
-   [Árbol de decisión](#BKMK_DecisionTree)  
  
-   [Red de dependencias](#BKMK_DependencyNetwork)  
  
-   [Leyenda de minería de datos](#BKMK_MiningLegend)  
  
###  <a name="BKMK_DecisionTree"></a> Árbol de decisión  
 Cuando se genera un modelo de árbol de decisión, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] genera un árbol independiente por cada atributo de predicción. Puede ver un árbol individual seleccionándolo en la lista **Árbol** de la pestaña **Árbol de decisión** del visor.  
  
 Un árbol de decisión está compuesto por una serie de divisiones, con la división más importante, determinada por el algoritmo, a la izquierda del visor en el nodo **Todos** . Las divisiones adicionales se muestran a la derecha. La división del nodo **Todos** es la más importante, ya que contiene la condición más determinante de división del conjunto de datos y, por lo tanto, la que ocasiona la primera división.  
  
 Puede expandir o contraer nodos individuales en el árbol para mostrar u ocultar las divisiones que ocurren en cada nodo. También puede usar las opciones de la ficha **Árbol de decisión** para influir en el modo en que se muestra el árbol. Use el control deslizante **Mostrar nivel** para ajustar el número de niveles que muestra el árbol. Use **Expansión predeterminada** para configurar el número predeterminado de niveles que van a aparecer en todos los árboles del modelo.  
  
#### <a name="predicting-discrete-attributes"></a>Predecir atributos discretos  
 Cuando un árbol se genera con un atributo de predicción discreto, el visor muestra lo siguiente en cada nodo del árbol:  
  
-   La condición que provocó la división.  
  
-   Un histograma que representa la distribución de los estados del atributo de predicción, ordenados por popularidad.  
  
 Puede utilizar la opción **Histograma** para cambiar el número de estados que aparecen en los histogramas del árbol. Esto resulta útil si el atributo de predicción tiene muchos estados. Los estados aparecen en un histograma por orden de popularidad de izquierda a derecha; si el número de estados que elige que se muestren es menor que el número total de estados del atributo, los estados menos populares se muestran de forma conjunta en color gris. Para ver el recuento exacto de cada estado de un nodo, sitúe el puntero sobre el nodo para ver un recuadro informativo o seleccione el nodo para ver sus detalles en la **Leyenda de minería de datos**.  
  
 El color de fondo de cada nodo representa la concentración de casos del estado del atributo concreto que selecciona utilizando la opción **Fondo** . Puede utilizar esta opción para resaltar los nodos que contengan un destino concreto en el que esté interesado.  
  
#### <a name="predicting-continuous-attributes"></a>Predecir atributos continuos  
 Cuando un árbol se genera con un atributo de predicción continuo, el visor muestra un gráfico en forma de rombo, en lugar de un histograma, por cada nodo del árbol. El gráfico en forma de rombo tiene una línea que representa el intervalo del atributo. El rombo está ubicado en la media del nodo y su ancho representa la varianza del atributo en ese nodo. Un rombo más estrecho indica que el nodo puede crear una predicción más exacta. El visor también muestra la ecuación de regresión, que se emplea para determinar la división del nodo.  
  
#### <a name="additional-decision-tree-display-options"></a>Opciones de presentación adicionales del árbol de decisión  
 Cuando la obtención de detalles está habilitada para un modelo de árbol de decisión, puede acceder a los casos de aprendizaje compatibles con un nodo si hace clic con el botón derecho en el nodo en el árbol y selecciona **Obtener detalles**. Puede habilitar la obtención de detalles en el Asistente para minería de datos o ajustando la propiedad de obtención de detalles del modelo de minería de datos en la pestaña **Modelos de minería de datos** .  
  
 Puede utilizar las opciones de zoom de la pestaña **Árbol de decisión** para acercar o alejar el árbol, o utilizar **Ajustar tamaño al contenido** para que en la pantalla del visor se muestre el modelo completo. Si el árbol es demasiado grande para ajustar su contenido al tamaño de la pantalla, puede utilizar la opción **Navegación**para navegar por el árbol. Al hacer clic en **Navegación** se abre una ventana de navegación independiente que se puede utilizar para seleccionar secciones del modelo que se muestra.  
  
 También puede copiar la imagen de la vista del árbol en el Portapapeles, de modo que pueda pegarla en documentos o en programas de manipulación de imágenes. Utilice **Copiar vista del gráfico** para copiar solo la sección del árbol que se muestra en el visor o **Copiar todo el gráfico** para copiar todos los nodos expandidos del árbol.  
  
 [Volver al principio](#BKMK_TabsPanes)  
  
###  <a name="BKMK_DependencyNetwork"></a> Red de dependencias  
 La **Red de dependencias** muestra las dependencias entre los atributos de entrada y los atributos de predicción del modelo. El control deslizante de la izquierda del visor se comporta como un filtro que está asociado a la importancia de las dependencias. Si desplaza el control deslizante hacia abajo, solamente se muestran en el visor los vínculos de mayor importancia.  
  
 Cuando se selecciona un nodo, el visor resalta las dependencias específicas de dicho nodo. Por ejemplo, si elige un nodo de predicción, el visor también resalta cada uno de los nodos que ayudan a predecir el nodo de predicción.  
  
 Si el visor contiene numerosos nodos, puede buscar nodos específicos mediante el botón **Buscar nodo** . Al hacer clic en **Buscar nodo** se abre el cuadro de diálogo **Buscar nodo** , en el que puede utilizar un filtro para buscar y seleccionar nodos específicos.  
  
 La leyenda de la parte inferior del visor vincula códigos de color con el tipo de dependencia en el gráfico. Por ejemplo, cuando selecciona un nodo de predicción, este nodo se sombrea en color turquesa y los nodos que predicen el nodo seleccionado aparecen sombreados en color naranja.  
  
 [Volver al principio](#BKMK_TabsPanes)  
  
###  <a name="BKMK_MiningLegend"></a> Leyenda de minería de datos  
 La **Leyenda de minería de datos** muestra la siguiente información al seleccionar un nodo en el modelo de árbol de decisión:  
  
-   El número de casos del nodo, dividido en los estados del atributo de predicción.  
  
-   La probabilidad de cada caso del atributo de predicción del nodo.  
  
-   Un histograma que incluye un recuento de cada estado del atributo de predicción.  
  
-   Las condiciones que se requieren para alcanzar un nodo específico, que también se conocen como *ruta del nodo*.  
  
-   Para los modelos de regresión lineal, la fórmula de la regresión.  
  
 Puede acoplar la **Leyenda de minería de datos** y trabajar con ella de manera similar a como se hace con el Explorador de soluciones.  
  
 [Volver al principio](#BKMK_TabsPanes)  
  
## <a name="see-also"></a>Vea también  
 [Microsoft Decision Trees Algorithm](../../analysis-services/data-mining/microsoft-decision-trees-algorithm.md)   
 [Visores de modelos de minería de datos &#40; el Diseñador de modelo de minería de datos &#41;](http://msdn.microsoft.com/library/4ba391d5-c97b-4848-ba7c-7d096fa4b7dd)   
 [Tareas y procedimientos del Visor de modelos de minería de datos](../../analysis-services/data-mining/mining-model-viewer-tasks-and-how-tos.md)   
 [Herramientas de minería de datos](../../analysis-services/data-mining/data-mining-tools.md)   
 [Visores de modelos de minería de datos](../../analysis-services/data-mining/data-mining-model-viewers.md)  
  
  

