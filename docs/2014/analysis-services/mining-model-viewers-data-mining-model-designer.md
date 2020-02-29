---
title: Visores de modelos de minería de datos (diseñador de modelos de minería de datos) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.dm.miningmodeleditor.viewers.f1
ms.assetid: 4ba391d5-c97b-4848-ba7c-7d096fa4b7dd
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 9458f2c1fb3d170bf1b4a2887acae94b55ed877e
ms.sourcegitcommit: 2d4067fc7f2157d10a526dcaa5d67948581ee49e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/28/2020
ms.locfileid: "78175810"
---
# <a name="mining-model-viewers-data-mining-model-designer"></a>Visores de modelos de minería de datos (Diseñador de modelos de minería de datos)
  Use la pestaña **Visor de modelos de minería de datos** para explorar los modelos de minería de datos que contiene una estructura de minería de datos.

 Primero seleccione el modelo de minería de datos y, a continuación, seleccione un visor. Cada modelo siempre tiene dos visores disponibles: un visor personalizado, que puede incluir varias pestañas, y el visor genérico.

 Para consultar un tutorial sobre cómo usar cada visor, vea [Visores de modelos de minería de datos](data-mining/data-mining-model-viewers.md).

## <a name="common-options"></a>Opciones comunes
 **Actualizar contenido del visor** Vuelva a cargar el modelo de minería de datos en el visor.

 **Modelo de minería de datos** Elija un modelo de minería de datos para ver que se encuentra en la estructura de minería de datos actual. El modelo de minería de datos se abrirá primero en su visor personalizado asociado.

 **Visor** de Elija un visor para explorar el modelo de minería de datos seleccionado. Esta lista [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] incluye los visores que proporciona para cada modelo de minería de datos [!INCLUDE[msCoName](../includes/msconame-md.md)] , el visor de contenido de minería de datos y los visores de complementos.

 El siguiente diagrama muestra un visor personalizado y el visor genérico para el mismo modelo.

-   El diagrama superior muestra el visor de un modelo de minería de datos basado en el algoritmo de serie temporal de Microsoft. Este visor personalizado determinado crea automáticamente un gráfico de serie temporal y proporciona cinco predicciones.

-   El diagrama inferior muestra el mismo modelo que se presenta mediante el **Visor de árbol de contenido genérico de Microsoft**. Este visor muestra el contenido del modelo de minería de datos según un esquema normalizado. Para más información, vea [Visor de árbol de contenido genérico de Microsoft &#40;minería de datos&#41;](microsoft-generic-content-tree-viewer-data-mining.md).

 ![Información general del diseñador del modelo de minería de datos](media/generic-mining-model-tab1.gif "Información general del diseñador del modelo de minería de datos")

## <a name="viewers-and-their-components"></a>Visores y sus componentes
 Según el modelo que seleccione, verá un visor personalizado, personalizado para el algoritmo que se usara para crear el modelo de minería de datos seleccionado. Cada visor personalizado tiene diversas herramientas y cuadros de diálogo para ayudarle a explorar las estadísticas y los patrones del modelo.

 En la lista siguiente se describen las opciones de cada uno de los visores personalizados.

### <a name="microsoft-association-rules-algorithm"></a>Algoritmo de reglas de asociación de Microsoft

-   [Examinar un modelo usando el Visor de reglas de asociación de Microsoft](data-mining/browse-a-model-using-the-microsoft-association-rules-viewer.md)

    -   [Pestaña conjuntos &#40;visor de modelos de minería de datos&#41;](itemsets-tab-mining-model-viewer.md)

    -   [Pestaña reglas &#40;visor de modelos de minería de datos&#41;](rules-tab-mining-model-viewer.md)

    -   [Pestaña red de dependencias &#40;visor de modelos de minería de datos&#41;](dependency-network-tab-mining-model-viewer.md)

### <a name="microsoft-clustering-algorithm"></a>Algoritmo de clústeres de Microsoft

-   [Examinar un modelo usando el Visor de clústeres de Microsoft](data-mining/browse-a-model-using-the-microsoft-cluster-viewer.md)

    -   [Pestaña diagrama del clúster &#40;visor de modelos de minería de datos&#41;](cluster-diagram-tab-mining-model-viewer.md)

    -   [Pestaña perfiles del clúster &#40;visor de modelos de minería de datos&#41;](cluster-profiles-tab-mining-model-viewer.md)

    -   [Pestaña características del clúster &#40;visor de modelos de minería de datos&#41;](cluster-characteristics-tab-mining-model-viewer.md)

    -   [Pestaña distinción del clúster &#40;visor de modelos de minería de datos&#41;](cluster-discrimination-tab-mining-model-viewer.md)

    -   [Cuadro de diálogo leyenda de minería de datos &#40;visor de modelos de minería de datos&#41;](mining-legend-dialog-box-mining-model-viewer.md)

### <a name="microsoft-decision-tree-algorithm"></a>Algoritmo de árboles de decisión de Microsoft

-   [Examinar un modelo usando el Visor de árboles de Microsoft](data-mining/browse-a-model-using-the-microsoft-tree-viewer.md)

    -   [Pestaña árbol de decisión &#40;visor de modelos de minería de datos&#41;](decision-tree-tab-mining-model-viewer.md)

    -   [Pestaña red de dependencias &#40;visor de modelos de minería de datos&#41;](dependency-network-tab-mining-model-viewer.md)

    -   [Cuadro de diálogo leyenda de minería de datos &#40;visor de modelos de minería de datos&#41;](mining-legend-dialog-box-mining-model-viewer.md)

### <a name="microsoft-linear-regression-algorithm"></a>Algoritmo de regresión lineal de Microsoft

-   [Examinar un modelo usando el Visor de redes neuronales de Microsoft](data-mining/browse-a-model-using-the-microsoft-neural-network-viewer.md)

    -   [Pestaña árbol de decisión &#40;visor de modelos de minería de datos&#41;](decision-tree-tab-mining-model-viewer.md)

    -   [Pestaña red de dependencias &#40;visor de modelos de minería de datos&#41;](dependency-network-tab-mining-model-viewer.md)

    -   [Cuadro de diálogo leyenda de minería de datos &#40;visor de modelos de minería de datos&#41;](mining-legend-dialog-box-mining-model-viewer.md)

### <a name="microsoft-logistic-regression-algorithm"></a>Algoritmo de regresión logística de Microsoft

-   [Examinar un modelo usando el Visor de redes neuronales de Microsoft](data-mining/browse-a-model-using-the-microsoft-neural-network-viewer.md)

### <a name="microsoft-nave-bayes-algorithm"></a>Algoritmo Bayes naive de Microsoft

-   [Examinar un modelo usando el visor Bayes naive de Microsoft](data-mining/browse-a-model-using-the-microsoft-naive-bayes-viewer.md)

    -   [Pestaña red de dependencias &#40;visor de modelos de minería de datos&#41;](dependency-network-tab-mining-model-viewer.md)

    -   [Pestaña perfiles de atributo &#40;el visor de modelos de minería de datos&#41;](attribute-profiles-tab-mining-model-viewer.md)

    -   [Pestaña características del atributo &#40;visor de modelos de minería de datos&#41;](attribute-characteristics-tab-mining-model-viewer.md)

    -   [Pestaña distinción de atributos &#40;visor de modelos de minería de datos&#41;](attribute-discrimination-tab-mining-model-viewer.md)

### <a name="microsoft-neural-network-algorithm"></a>Microsoft Neural Network Algorithm

-   [Examinar un modelo usando el Visor de redes neuronales de Microsoft](data-mining/browse-a-model-using-the-microsoft-neural-network-viewer.md)

    -   [Pestaña red de dependencias &#40;visor de modelos de minería de datos&#41;](dependency-network-tab-mining-model-viewer.md)

    -   [Visor de modelos de minería de datos &#40;de red neuronal&#41;](neural-network-mining-model-viewer.md)

    -   [Cuadro de diálogo Buscar nodo &#40;el visor de modelos de minería de datos&#41;](find-node-dialog-box-mining-model-viewer.md)

### <a name="microsoft-sequence-clustering-algorithm"></a>Algoritmo de clústeres de secuencia de Microsoft

-   [Examinar un modelo usando el Visor de clústeres de Microsoft](data-mining/browse-a-model-using-the-microsoft-sequence-cluster-viewer.md)

    -   [Pestaña diagrama de clústeres de secuencia &#40;visor de modelos de minería de datos](sequence-clustering-cluster-diagram-tab-mining-model-viewer.md)

    -   [Pestaña perfiles del clúster de clústeres de secuencia &#40;visor de modelos de minería de datos](sequence-clustering-cluster-profiles-tab-mining-model-viewer.md)

    -   [Pestaña características del clúster de clústeres de secuencia &#40;visor de modelos de minería de datos&#41;](sequence-clustering-cluster-characteristics-tab-mining-model-viewer.md)

    -   [Pestaña distinción del clúster de secuencia de clústeres &#40;visor de modelos de minería de datos&#41;](sequence-clustering-cluster-discrimination-tab-mining-model-viewer.md)

    -   [Pestaña transición del clúster de clústeres de secuencia &#40;visor de modelos de minería de datos&#41;](sequence-clustering-cluster-transition-tab-mining-model-viewer.md)

### <a name="microsoft-time-series-algorithm"></a>Algoritmo de serie temporal de Microsoft

-   [Examinar un modelo usando el Visor de serie temporal de Microsoft](data-mining/browse-a-model-using-the-microsoft-time-series-viewer.md)

    -   [Pestaña modelo &#40;visores de modelos de minería de datos&#41;](model-tab-mining-model-viewers.md)

    -   [Pestaña gráfico &#40;visores de modelos de minería de datos&#41;](chart-tab-mining-model-viewers.md)

    -   [Cuadro de diálogo leyenda de minería de datos &#40;visor de modelos de minería de datos&#41;](mining-legend-dialog-box-mining-model-viewer.md)

## <a name="see-also"></a>Consulte también
 [Modelos de minería de datos vista &#40;diseñador de modelos de minería de datos&#41;](mining-models-view-data-mining-model-designer.md) [vista estructura de minería de datos &#40;diseñador de modelos de minería](mining-structure-view-data-mining-model-designer.md) de datos&#41;el diseñador de gráficos de precisión de minería de [datos](mining-accuracy-chart-designer-data-mining.md) &#40;[predicción](prediction-query-builder-data-mining.md)&#41;generador de consultas &#40;de minería de datos


