---
title: Propiedades de minería de datos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- ClusterCount property
- AllowedProvidersInOpenRowset property
- MinimumSeriesValue property
- ScoreMethod property
- MinimumImportance property
- ModellingCardinality property
- BrentTolerance property
- ComplexityPenalty property
- MaximumItemsetCount property
- MinimumSupport property
- AllowSessionMiningModels property
- HoldoutPercentage property
- ClusterCountPrior property
- MaximumSequenceStates property
- OptimizedPredictionCount property
- data mining [Analysis Services], properties
- MaximumStates property
- MaximumContinuousInputAttributes property
- MaximumOutputAttributes property
- AllowAdHocOpenRowsetQueries property
- Enabled property
- HistoricModelGap property
- SampleSize property
- MaximumInputAttributes property
- PeriodicityHint property
- MissingValueSubstitution property
- SplitMethod property
- ForceRegressor property
- MaximumBucketsForContinuousSplit property
- MaxConcurrentPredictionQueries property
- MinimumItemsetSize property
- AcyclicGraph property
- HoldoutMethod property
- StoppingTolerance property
- properties [data mining]
- AutoDetectPeriodicity property
- HoldoutTolerance property
- MinimumLeafCases property
- HoldoutSeed property
- MinimumClusterCases property
- ClusterCountDeviation property
- MinimumDependencyProbability property
- ClusteringMethod property
- MaximumItemsetSize property
- HiddenNodeRatio property
- MaximumSeriesValue property
ms.assetid: 9bc9abed-180a-4bd8-b2eb-89c62fa88110
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 96106fc8bc50a2a1b19c54a6970eeeb72952d82d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "66069058"
---
# <a name="data-mining-properties"></a>Propiedades de minería de datos
  
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] admite las propiedades de servidor de minería de datos descritas en las siguientes tablas. Para obtener más información sobre las propiedades de servidor adicionales y cómo establecerlas, vea [Configure Server Properties in Analysis Services](server-properties-in-analysis-services.md).  
  
 **Se aplica a:** Modo de servidor multidimensional únicamente  
  
## <a name="non-specific-category"></a>Categoría no específica  
 `AllowSessionMiningModels`  
 Una propiedad booleana que indica si se pueden crear modelos de minería de datos de sesión.  
  
 El valor predeterminado para esta propiedad es False, que indica que no se pueden crear modelos de minería de datos de sesión.  
  
 `AllowAdHocOpenRowsetQueries`  
 Una propiedad booleana que indica si se permiten consultas ad hoc de conjuntos de filas abiertos.  
  
 El valor predeterminado para esta propiedad es False, que indica que las consultas de conjuntos de filas abiertos no están permitidas durante una sesión.  
  
 `AllowedProvidersInOpenRowset`  
 Una propiedad de cadena que identifica los proveedores que están permitidos en un conjunto de filas abierto; se compone de una lista separada por comas/puntos y coma de ProgID de proveedor, o en caso contrario [All].  
  
 `MaxConcurrentPredictionQueries`  
 Una propiedad de entero de 32 bits con signo que define el máximo de consultas de predicción simultáneas.  
  
## <a name="algorithms-category"></a>Categoría Algoritmos  
 `Microsoft_Association_Rules\ Enabled`  
 Una propiedad booleana que indica si el algoritmo Microsoft_Association_Rules está habilitado.  
  
 `Microsoft_Clustering\ Enabled`  
 Una propiedad booleana que indica si el algoritmo Microsoft_Clustering está habilitado.  
  
 `Microsoft_Decision_Trees\ Enabled`  
 Una propiedad booleana que indica si el algoritmo Microsoft_DecisionTrees está habilitado.  
  
 `Microsoft_Naive_Bayes\ Enabled`  
 Una propiedad booleana que indica si el algoritmo Microsoft_ Naive_Bayes está habilitado.  
  
 `Microsoft_Neural_Network\ Enabled`  
 Una propiedad booleana que indica si el algoritmo Microsoft_Neural_Network está habilitado.  
  
 `Microsoft_Sequence_Clustering\ Enabled`  
 Una propiedad booleana que indica si el algoritmo Microsoft_Sequence_Clustering está habilitado.  
  
 `Microsoft_Time_Series\ Enabled`  
 Una propiedad booleana que indica si el algoritmo Microsoft_Time_Series está habilitado.  
  
 `Microsoft_Linear_Regression\ Enabled`  
 Una propiedad booleana que indica si el algoritmo Microsoft_Linear_Regression está habilitado.  
  
 `Microsoft_Logistic_Regression\ Enabled`  
 Una propiedad booleana que indica si el algoritmo Microsoft_Logistic_Regression está habilitado.  
  
> [!NOTE]  
>  Además de las propiedades que definen los servicios de minería de datos disponibles en el servidor, existen propiedades de minería de datos que definen el comportamiento de algoritmos concretos. Estas propiedades se configuran al crear un modelo de minería de datos individual, no en el nivel de servidor. Para obtener más información, vea [Algoritmos de minería de datos &#40;Analysis Services: Minería de datos&#41;](../data-mining/data-mining-algorithms-analysis-services-data-mining.md).  
  
## <a name="see-also"></a>Consulte también  
 [Arquitectura física &#40;Analysis Services:&#41;de minería de datos](../data-mining/physical-architecture-analysis-services-data-mining.md)   
 [Configurar las propiedades del servidor en Analysis Services](server-properties-in-analysis-services.md)   
 [Determinar el modo de servidor de una instancia de Analysis Services](../instances/determine-the-server-mode-of-an-analysis-services-instance.md)  
  
  
