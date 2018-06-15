---
title: Examinar un modelo usando el Visor Bayes Naive de Microsoft | Documentos de Microsoft
ms.date: 05/01/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: e7afe60ffa61af8e2c1ae5b60deb596230738a78
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
ms.locfileid: "34014782"
---
# <a name="browse-a-model-using-the-microsoft-naive-bayes-viewer"></a>Examinar un modelo usando el visor Bayes naive de Microsoft
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  El Visor Bayes naive de [!INCLUDE[msCoName](../../includes/msconame-md.md)] incluido en [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] muestra los modelos de minería de datos que se generan con el algoritmo Bayes naive de [!INCLUDE[msCoName](../../includes/msconame-md.md)] . El algoritmo Bayes naive de [!INCLUDE[msCoName](../../includes/msconame-md.md)] es un algoritmo de clasificación que se adapta muy bien a las tareas de modelado de predicción. Para obtener más información acerca de este algoritmo, vea [Microsoft Naive Bayes Algorithm](../../analysis-services/data-mining/microsoft-naive-bayes-algorithm.md).  
  
 Como uno de los principales propósitos de un modelo Bayes naive es ofrecer una manera rápida de explorar los datos de un conjunto de datos, el Visor Bayes naive de [!INCLUDE[msCoName](../../includes/msconame-md.md)] proporciona varios métodos para mostrar la interacción entre los atributos de predicción y los atributos de entrada.  
  
> [!NOTE]  
>  Si desea ver información detallada acerca de las ecuaciones que se usan en el modelo y los patrones detectados, puede cambiar al Visor de árbol de contenido genérico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] . Para más información, vea [Examinar un modelo usando el Visor de árbol de contenido genérico de Microsoft](../../analysis-services/data-mining/browse-a-model-using-the-microsoft-generic-content-tree-viewer.md) o [Visor de árbol de contenido genérico de Microsoft &#40;Minería de datos&#41;](http://msdn.microsoft.com/library/751b4393-f6fd-48c1-bcef-bdca589ce34c).  
  
##  <a name="BKMK_ViewerTabs"></a> Fichas del visor  
 Cuando se explora un modelo de minería de datos en [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], el modelo aparece en la pestaña **Visor de modelos de minería de datos** del visor del diseñador de minería de datos apropiado para el modelo. El Visor Bayes naive de [!INCLUDE[msCoName](../../includes/msconame-md.md)] dispone de las siguientes pestañas para explorar datos:  
  
-   [Red de dependencias](#BKMK_Dependency)  
  
-   [Perfiles del atributo](#BKMK_Profiles)  
  
-   [Características del atributo](#BKMK_Characteristics)  
  
-   [Distinción del atributo](#BKMK_Discrimination)  
  
##  <a name="BKMK_Dependency"></a> Red de dependencias  
 La pestaña **Red de dependencias** muestra las dependencias entre los atributos de entrada y los atributos de predicción de un modelo. El control deslizante de la izquierda del visor se comporta como un filtro que está asociado a la importancia de las dependencias. Si desplaza el control deslizante hacia abajo, sólo se verán los vínculos más similares.  
  
 Cuando se selecciona un nodo, el visor resalta las dependencias específicas de dicho nodo. Por ejemplo, si elige un nodo de predicción, el visor también resalta cada uno de los nodos que ayudan a predecir el nodo de predicción.  
  
 La leyenda de la parte inferior del visor vincula códigos de color con el tipo de dependencia en el gráfico. Por ejemplo, cuando selecciona un nodo de predicción, este nodo se sombrea en color turquesa y los nodos que predicen el nodo seleccionado aparecen sombreados en color naranja.  
  
 [Volver al principio](#BKMK_ViewerTabs)  
  
##  <a name="BKMK_Profiles"></a> Perfiles del atributo  
 La pestaña **Perfiles del atributo** muestra histogramas en una cuadrícula. Puede utilizar esta cuadrícula para comparar el atributo de predicción seleccionado en el cuadro **De predicción** con los demás atributos del modelo. Cada columna de la pestaña representa un estado del atributo de predicción. Si el atributo de predicción tiene muchos estados, puede cambiar el número de estados que aparecen en el histograma ajustando las **Barras de histograma**. Si el número que elige es menor que el número total de estados del atributo, los estados se enumerarán en orden de compatibilidad, con los estados restantes recopilados en un único depósito deshabilitado.  
  
 Para mostrar una leyenda de minería de datos que relaciona los colores del histograma con los estados de un atributo, active la casilla **Mostrar leyenda** . La Leyenda de minería de datos también muestra la distribución de casos para cada par de atributo-valor que seleccione.  
  
 Para copiar el contenido de la cuadrícula en el Portapapeles como una tabla HTML, haga clic con el botón derecho en la pestaña **Perfiles del atributo** y seleccione **Copiar**.  
  
 [Volver al principio](#BKMK_ViewerTabs)  
  
##  <a name="BKMK_Characteristics"></a> Características del atributo  
 Para usar la pestaña **Características del atributo** , seleccione un atributo de predicción en la lista **Atributo** y elija un estado del atributo seleccionado en la lista **Valor** . Al establecer estas variables, la pestaña **Características del atributo** muestra los estados de los atributos que están asociados con el caso seleccionado del atributo seleccionado. Los atributos se ordenan por importancia.  
  
 [Volver al principio](#BKMK_ViewerTabs)  
  
##  <a name="BKMK_Discrimination"></a> Distinción del atributo  
 Para usar la pestaña **Distinción del atributo** , seleccione un atributo de predicción y dos de sus estados en las listas **Atributo**, **Valor 1**y **Valor 2** . La cuadrícula de la pestaña **Distinción del atributo** mostrará entonces la siguiente información en columnas:  
  
 **Atributo**  
 Muestra otros atributos del conjunto de datos que contienen un estado que favorece claramente un estado del atributo de predicción.  
  
 **Valores**  
 Muestra el valor del atributo en la columna **Atributo** .  
  
 **Favorece \<valor 1 >**  
 Muestra una barra coloreada que indica la intensidad con la que el valor de atributo favorece el valor de atributo predecible mostrado en **Valor 1**.  
  
 **Favorece \<valor 2 >**  
 Muestra una barra coloreada que indica la intensidad con la que el valor de atributo favorece el valor de atributo predecible mostrado en **Valor 2**.  
  
 [Volver al principio](#BKMK_ViewerTabs)  
  
## <a name="see-also"></a>Vea también  
 [Algoritmo Bayes Naive de Microsoft](../../analysis-services/data-mining/microsoft-naive-bayes-algorithm.md)   
 [Tareas y tareas del Visor de modelo de minería de datos](../../analysis-services/data-mining/mining-model-viewer-tasks-and-how-tos.md)   
 [Herramientas de minería de datos](../../analysis-services/data-mining/data-mining-tools.md)   
 [Visores de modelos de minería de datos](../../analysis-services/data-mining/data-mining-model-viewers.md)  
  
  
