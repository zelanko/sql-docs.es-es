---
title: "Propiedades de miner&#237;a de datos | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
ms.tgt_pltfrm: ""
ms.topic: "reference"
helpviewer_keywords: 
  - "ClusterCount, propiedad"
  - "AllowedProvidersInOpenRowset, propiedad"
  - "MinimumSeriesValue, propiedad"
  - "ScoreMethod, propiedad"
  - "MinimumImportance, propiedad"
  - "ModellingCardinality, propiedad"
  - "BrentTolerance, propiedad"
  - "ComplexityPenalty, propiedad"
  - "MaximumItemsetCount, propiedad"
  - "MinimumSupport, propiedad"
  - "AllowSessionMiningModels, propiedad"
  - "HoldoutPercentage, propiedad"
  - "ClusterCountPrior, propiedad"
  - "MaximumSequenceStates, propiedad"
  - "OptimizedPredictionCount, propiedad"
  - "minería de datos [Analysis Services], propiedades"
  - "MaximumStates, propiedad"
  - "MaximumContinuousInputAttributes, propiedad"
  - "MaximumOutputAttributes, propiedad"
  - "AllowAdHocOpenRowsetQueries, propiedad"
  - "Enabled, propiedad"
  - "HistoricModelGap, propiedad"
  - "SampleSize, propiedad"
  - "MaximumInputAttributes, propiedad"
  - "PeriodicityHint, propiedad"
  - "MissingValueSubstitution, propiedad"
  - "SplitMethod, propiedad"
  - "ForceRegressor, propiedad"
  - "MaximumBucketsForContinuousSplit, propiedad"
  - "MaxConcurrentPredictionQueries, propiedad"
  - "MinimumItemsetSize, propiedad"
  - "AcyclicGraph, propiedad"
  - "HoldoutMethod, propiedad"
  - "StoppingTolerance, propiedad"
  - "propiedades [minería de datos]"
  - "AutoDetectPeriodicity, propiedad"
  - "HoldoutTolerance, propiedad"
  - "MinimumLeafCases, propiedad"
  - "HoldoutSeed, propiedad"
  - "MinimumClusterCases, propiedad"
  - "ClusterCountDeviation, propiedad"
  - "MinimumDependencyProbability, propiedad"
  - "ClusteringMethod, propiedad"
  - "MaximumItemsetSize, propiedad"
  - "HiddenNodeRatio, propiedad"
  - "MaximumSeriesValue, propiedad"
ms.assetid: 9bc9abed-180a-4bd8-b2eb-89c62fa88110
caps.latest.revision: 19
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 19
---
# Propiedades de miner&#237;a de datos
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] admite las propiedades de servidor de minería de datos descritas en las siguientes tablas. Para obtener más información sobre las propiedades de servidor adicionales y cómo establecerlas, vea [Configurar las propiedades de servidor en Analysis Services](../../analysis-services/server-properties/server-properties-in-analysis-services.md).  
  
 **Se aplica a:** modo de servidor multidimensional únicamente  
  
## Categoría no específica  
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
  
## Categoría Algoritmos  
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
  
## Vea también  
 [Arquitectura física &#40;Analysis Services - Minería de datos&#41;](../../analysis-services/data-mining/physical-architecture-analysis-services-data-mining.md)   
 [Configurar las propiedades de servidor en Analysis Services](../../analysis-services/server-properties/server-properties-in-analysis-services.md)   
 [Determinar el modo de servidor de una instancia de Analysis Services](../../analysis-services/instances/determine-the-server-mode-of-an-analysis-services-instance.md)  
  
  