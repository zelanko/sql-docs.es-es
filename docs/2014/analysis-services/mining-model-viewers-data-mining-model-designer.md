---
title: (Diseñador de modelos de minería de datos) de visores de modelos de minería de datos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.dm.miningmodeleditor.viewers.f1
ms.assetid: 4ba391d5-c97b-4848-ba7c-7d096fa4b7dd
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 7890360221f3adae73efef7a58ae1179e19760a1
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62727941"
---
# <a name="mining-model-viewers-data-mining-model-designer"></a>Visores de modelos de minería de datos (Diseñador de modelos de minería de datos)
  Use la pestaña **Visor de modelos de minería de datos** para explorar los modelos de minería de datos que contiene una estructura de minería de datos.  
  
 Primero seleccione el modelo de minería de datos y, a continuación, seleccione un visor. Cada modelo siempre tiene dos visores disponibles: un visor personalizado, que puede incluir varias pestañas, y el visor genérico.  
  
 Para consultar un tutorial sobre cómo usar cada visor, vea [Visores de modelos de minería de datos](data-mining/data-mining-model-viewers.md).  
  
## <a name="common-options"></a>Opciones comunes  
 **Actualizar el contenido del Visor**  
 Vuelva a cargar el modelo de minería de datos en el visor.  
  
 **Modelo de minería de datos**  
 Elija esta opción para ver un modelo de minería de datos que se encuentra en la estructura de minería de datos actual. El modelo de minería de datos se abrirá primero en su visor personalizado asociado.  
  
 **Viewer**  
 Elija un visor para explorar el modelo de minería de datos seleccionado. En esta lista se incluyen los visores que [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] proporciona para cada modelo de minería de datos, el Visor de contenido de minería de datos de [!INCLUDE[msCoName](../includes/msconame-md.md)] y todos los visores de complemento.  
  
 El siguiente diagrama muestra un visor personalizado y el visor genérico para el mismo modelo.  
  
-   El diagrama superior muestra el visor de un modelo de minería de datos basado en el algoritmo de serie temporal de Microsoft. Este visor personalizado determinado crea automáticamente un gráfico de serie temporal y proporciona cinco predicciones.  
  
-   El diagrama inferior muestra el mismo modelo que se presenta mediante el **Visor de árbol de contenido genérico de Microsoft**. Este visor muestra el contenido del modelo de minería de datos según un esquema normalizado. Para más información, vea [Visor de árbol de contenido genérico de Microsoft &#40;minería de datos&#41;](microsoft-generic-content-tree-viewer-data-mining.md).  
  
 ![Información general del Diseñador de modelos de minería de datos](media/generic-mining-model-tab1.gif "información general del Diseñador de modelos de minería de datos")  
  
## <a name="viewers-and-their-components"></a>Visores y sus componentes  
 Según el modelo que seleccione, verá un visor personalizado, personalizado para el algoritmo que se usara para crear el modelo de minería de datos seleccionado. Cada visor personalizado tiene diversas herramientas y cuadros de diálogo para ayudarle a explorar las estadísticas y los patrones del modelo.  
  
 En la lista siguiente se describen las opciones de cada uno de los visores personalizados.  
  
### <a name="microsoft-association-rules-algorithm"></a>Algoritmo de reglas de asociación de Microsoft  
  
-   [Examinar un modelo usando el Visor de reglas de asociación de Microsoft](data-mining/browse-a-model-using-the-microsoft-association-rules-viewer.md)  
  
    -   [Pestaña conjuntos de elementos &#40;Visor de modelos de minería de datos&#41;](itemsets-tab-mining-model-viewer.md)  
  
    -   [Pestaña reglas &#40;Visor de modelos de minería de datos&#41;](rules-tab-mining-model-viewer.md)  
  
    -   [Pestaña red de dependencias &#40;Visor de modelos de minería de datos&#41;](dependency-network-tab-mining-model-viewer.md)  
  
### <a name="microsoft-clustering-algorithm"></a>Algoritmo de clústeres de Microsoft  
  
-   [Examinar un modelo usando el Visor de clústeres de Microsoft](data-mining/browse-a-model-using-the-microsoft-cluster-viewer.md)  
  
    -   [Pestaña diagrama del clúster &#40;Visor de modelos de minería de datos&#41;](cluster-diagram-tab-mining-model-viewer.md)  
  
    -   [Pestaña perfiles de clúster &#40;Visor de modelos de minería de datos&#41;](cluster-profiles-tab-mining-model-viewer.md)  
  
    -   [Pestaña características del clúster &#40;Visor de modelos de minería de datos&#41;](cluster-characteristics-tab-mining-model-viewer.md)  
  
    -   [Pestaña distinción del clúster &#40;Visor de modelos de minería de datos&#41;](cluster-discrimination-tab-mining-model-viewer.md)  
  
    -   [Cuadro de diálogo leyenda de minería de datos &#40;Visor de modelos de minería de datos&#41;](mining-legend-dialog-box-mining-model-viewer.md)  
  
### <a name="microsoft-decision-tree-algorithm"></a>Algoritmo de árboles de decisión de Microsoft  
  
-   [Examinar un modelo usando el Visor de árboles de Microsoft](data-mining/browse-a-model-using-the-microsoft-tree-viewer.md)  
  
    -   [Pestaña árbol de decisión &#40;Visor de modelos de minería de datos&#41;](decision-tree-tab-mining-model-viewer.md)  
  
    -   [Pestaña red de dependencias &#40;Visor de modelos de minería de datos&#41;](dependency-network-tab-mining-model-viewer.md)  
  
    -   [Cuadro de diálogo leyenda de minería de datos &#40;Visor de modelos de minería de datos&#41;](mining-legend-dialog-box-mining-model-viewer.md)  
  
### <a name="microsoft-linear-regression-algorithm"></a>Algoritmo de regresión lineal de Microsoft  
  
-   [Examinar un modelo usando el Visor de redes neuronales de Microsoft](data-mining/browse-a-model-using-the-microsoft-neural-network-viewer.md)  
  
    -   [Pestaña árbol de decisión &#40;Visor de modelos de minería de datos&#41;](decision-tree-tab-mining-model-viewer.md)  
  
    -   [Pestaña red de dependencias &#40;Visor de modelos de minería de datos&#41;](dependency-network-tab-mining-model-viewer.md)  
  
    -   [Cuadro de diálogo leyenda de minería de datos &#40;Visor de modelos de minería de datos&#41;](mining-legend-dialog-box-mining-model-viewer.md)  
  
### <a name="microsoft-logistic-regression-algorithm"></a>Algoritmo de regresión logística de Microsoft  
  
-   [Examinar un modelo usando el Visor de redes neuronales de Microsoft](data-mining/browse-a-model-using-the-microsoft-neural-network-viewer.md)  
  
### <a name="microsoft-nave-bayes-algorithm"></a>Algoritmo Bayes naive de Microsoft  
  
-   [Examinar un modelo usando el visor Bayes naive de Microsoft](data-mining/browse-a-model-using-the-microsoft-naive-bayes-viewer.md)  
  
    -   [Pestaña red de dependencias &#40;Visor de modelos de minería de datos&#41;](dependency-network-tab-mining-model-viewer.md)  
  
    -   [Atributo perfiles pestaña &#40;Visor de modelos de minería de datos&#41;](attribute-profiles-tab-mining-model-viewer.md)  
  
    -   [Pestaña características del atributo &#40;Visor de modelos de minería de datos&#41;](attribute-characteristics-tab-mining-model-viewer.md)  
  
    -   [Pestaña distinción del atributo &#40;Visor de modelos de minería de datos&#41;](attribute-discrimination-tab-mining-model-viewer.md)  
  
### <a name="microsoft-neural-network-algorithm"></a>Microsoft Neural Network Algorithm  
  
-   [Examinar un modelo usando el Visor de redes neuronales de Microsoft](data-mining/browse-a-model-using-the-microsoft-neural-network-viewer.md)  
  
    -   [Pestaña red de dependencias &#40;Visor de modelos de minería de datos&#41;](dependency-network-tab-mining-model-viewer.md)  
  
    -   [Red neuronal &#40;Visor de modelos de minería de datos&#41;](neural-network-mining-model-viewer.md)  
  
    -   [Nodo cuadro de diálogo Buscar &#40;Visor de modelos de minería de datos&#41;](find-node-dialog-box-mining-model-viewer.md)  
  
### <a name="microsoft-sequence-clustering-algorithm"></a>Algoritmo de clústeres de secuencia de Microsoft  
  
-   [Examinar un modelo usando el Visor de clústeres de secuencia de Microsoft](data-mining/browse-a-model-using-the-microsoft-sequence-cluster-viewer.md)  
  
    -   [Pestaña diagrama del clúster de clústeres de secuencia &#40;Visor de modelos de minería de datos](sequence-clustering-cluster-diagram-tab-mining-model-viewer.md)  
  
    -   [Pestaña perfiles de clúster de clústeres de secuencia &#40;Visor de modelos de minería de datos](sequence-clustering-cluster-profiles-tab-mining-model-viewer.md)  
  
    -   [Pestaña características del clúster de clústeres de secuencia &#40;Visor de modelos de minería de datos&#41;](sequence-clustering-cluster-characteristics-tab-mining-model-viewer.md)  
  
    -   [Pestaña distinción del clúster de clústeres de secuencia &#40;Visor de modelos de minería de datos&#41;](sequence-clustering-cluster-discrimination-tab-mining-model-viewer.md)  
  
    -   [Pestaña transiciones de estado de clústeres de secuencia &#40;Visor de modelos de minería de datos&#41;](sequence-clustering-cluster-transition-tab-mining-model-viewer.md)  
  
### <a name="microsoft-time-series-algorithm"></a>Algoritmo de serie temporal de Microsoft  
  
-   [Examinar un modelo usando el Visor de serie temporal de Microsoft](data-mining/browse-a-model-using-the-microsoft-time-series-viewer.md)  
  
    -   [Pestaña de modelo &#40;visores de modelos de minería de datos&#41;](model-tab-mining-model-viewers.md)  
  
    -   [Pestaña de gráfico &#40;visores de modelos de minería de datos&#41;](chart-tab-mining-model-viewers.md)  
  
    -   [Cuadro de diálogo leyenda de minería de datos &#40;Visor de modelos de minería de datos&#41;](mining-legend-dialog-box-mining-model-viewer.md)  
  
## <a name="see-also"></a>Vea también  
 [Vista de modelos de minería de datos &#40;Diseñador de modelos de minería de datos&#41;](mining-models-view-data-mining-model-designer.md)   
 [Vista de la estructura de minería de datos &#40;Diseñador de modelos de minería de datos&#41;](mining-structure-view-data-mining-model-designer.md)   
 [Diseñador gráfico de precisión de minería de datos &#40;minería de datos&#41;](mining-accuracy-chart-designer-data-mining.md)   
 [Generador de consultas de predicción &#40;minería de datos&#41;](prediction-query-builder-data-mining.md)  
  
  
