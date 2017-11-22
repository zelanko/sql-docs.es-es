---
title: "Propiedades de minería de datos | Documentos de Microsoft"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: server-properties
ms.reviewer: 
ms.suite: sql
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: reference
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
caps.latest.revision: "19"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: c53c6fffea0e6710a5fccb0b1f8272d57dd4a3ce
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="data-mining-properties"></a>Propiedades de minería de datos
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] admite las propiedades de servidor de minería de datos descritas en las siguientes tablas. Para obtener más información sobre las propiedades de servidor adicionales y cómo establecerlas, vea [Configurar las propiedades de servidor en Analysis Services](../../analysis-services/server-properties/server-properties-in-analysis-services.md).  
  
 **Se aplica a:** modo de servidor multidimensional únicamente  
  
## <a name="non-specific-category"></a>Categoría no específica  
 **AllowSessionMiningModels**  
 Una propiedad booleana que indica si se pueden crear modelos de minería de datos de sesión.  
  
 El valor predeterminado para esta propiedad es False, que indica que no se pueden crear modelos de minería de datos de sesión.  
  
 **AllowAdHocOpenRowsetQueries**  
 Una propiedad booleana que indica si se permiten consultas ad hoc de conjuntos de filas abiertos.  
  
 El valor predeterminado para esta propiedad es False, que indica que las consultas de conjuntos de filas abiertos no están permitidas durante una sesión.  
  
 **AllowedProvidersInOpenRowset**  
 Una propiedad de cadena que identifica los proveedores que están permitidos en un conjunto de filas abierto; se compone de una lista separada por comas/puntos y coma de ProgID de proveedor, o en caso contrario [All].  
  
 **MaxConcurrentPredictionQueries**  
 Una propiedad de entero de 32 bits con signo que define el máximo de consultas de predicción simultáneas.  
  
## <a name="algorithms-category"></a>Categoría Algoritmos  
 **Microsoft_Association_Rules\ Enabled**  
 Una propiedad booleana que indica si el algoritmo Microsoft_Association_Rules está habilitado.  
  
 **Microsoft_Clustering\ Enabled**  
 Una propiedad booleana que indica si el algoritmo Microsoft_Clustering está habilitado.  
  
 **Microsoft_Decision_Trees\ Enabled**  
 Una propiedad booleana que indica si el algoritmo Microsoft_DecisionTrees está habilitado.  
  
 **Microsoft_Naive_Bayes\ Enabled**  
 Una propiedad booleana que indica si el algoritmo Microsoft_ Naive_Bayes está habilitado.  
  
 **Microsoft_Neural_Network\ Enabled**  
 Una propiedad booleana que indica si el algoritmo Microsoft_Neural_Network está habilitado.  
  
 **Microsoft_Sequence_Clustering\ Enabled**  
 Una propiedad booleana que indica si el algoritmo Microsoft_Sequence_Clustering está habilitado.  
  
 **Microsoft_Time_Series\ Enabled**  
 Una propiedad booleana que indica si el algoritmo Microsoft_Time_Series está habilitado.  
  
 **Microsoft_Linear_Regression\ Enabled**  
 Una propiedad booleana que indica si el algoritmo Microsoft_Linear_Regression está habilitado.  
  
 **Microsoft_Logistic_Regression\ Enabled**  
 Una propiedad booleana que indica si el algoritmo Microsoft_Logistic_Regression está habilitado.  
  
> [!NOTE]  
>  Además de las propiedades que definen los servicios de minería de datos disponibles en el servidor, existen propiedades de minería de datos que definen el comportamiento de algoritmos concretos. Estas propiedades se configuran al crear un modelo de minería de datos individual, no en el nivel de servidor. Para obtener más información, vea [Algoritmos de minería de datos &#40;Analysis Services: Minería de datos&#41;](../../analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining.md).  
  
## <a name="see-also"></a>Vea también  
 [Arquitectura física &#40;Analysis Services - Minería de datos&#41;](../../analysis-services/data-mining/physical-architecture-analysis-services-data-mining.md)   
 [Configurar las propiedades de servidor en Analysis Services](../../analysis-services/server-properties/server-properties-in-analysis-services.md)   
 [Determinar el modo de servidor de una instancia de Analysis Services](../../analysis-services/instances/determine-the-server-mode-of-an-analysis-services-instance.md)  
  
  
