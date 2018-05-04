---
title: PredictHistogram (DMX) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: data-mining
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- PredictHistogram
dev_langs:
- DMX
helpviewer_keywords:
- PredictHistogram function
ms.assetid: 85ffc542-96e7-4f58-aaa3-34d76befcedf
caps.latest.revision: 34
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: 2c06d117d2abd0fc988f5d5b497e588910bd744a
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="predicthistogram-dmx"></a>PredictHistogram (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Devuelve una tabla que representa un histograma para la predicción de una columna determinada.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
PredictHistogram(<scalar column reference> | <cluster column reference>)  
```  
  
## <a name="applies-to"></a>Se aplica a  
 Una referencia de columna escalar o una referencia de columna de clúster. Puede utilizarse con todos los tipos de algoritmo, excepto el algoritmo de asociación de [!INCLUDE[msCoName](../includes/msconame-md.md)].  
  
## <a name="return-type"></a>Tipo devuelto  
 Tabla.  
  
## <a name="remarks"></a>Comentarios  
 Los histogramas generan columnas de estadísticas. La estructura de columnas del histograma devuelto depende del tipo de referencia de columna que se usa con la **PredictHistogram** función.  
  
## <a name="scalar-columns"></a>Columnas escalares  
 Para una \<referencia de columna escalar >, el histograma que la **PredictHistogram** valores devueltos de función consta de las siguientes columnas:  
  
-   El valor que se predice.  
  
-   **$Support**  
  
-   **$Probability**  
  
-   **$ProbabilityVariance**  
  
     [!INCLUDE[msCoName](../includes/msconame-md.md)] algoritmos de minería de datos no admiten **$ProbabilityVariance**. Esta columna siempre contiene 0 para los algoritmos de [!INCLUDE[msCoName](../includes/msconame-md.md)].  
  
-   **$ProbabilityStdev**  
  
     [!INCLUDE[msCoName](../includes/msconame-md.md)] algoritmos de minería de datos no admiten **$ProbabilityStdev**. Esta columna siempre contiene 0 para los algoritmos de [!INCLUDE[msCoName](../includes/msconame-md.md)].  
  
-   **$AdjustedProbability**  
  
     El **$AdjustedProbability** columna es una [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] extensión a la [!INCLUDE[msCoName](../includes/msconame-md.md)] OLE DB para la especificación de minería de datos.  
  
## <a name="cluster-columns"></a>Columnas de clúster  
 El histograma que la **PredictHistogram** función devuelve para un \<referencia a una columna de clúster > consta de las siguientes columnas:  
  
-   **$Cluster** (representa el nombre del clúster)  
  
-   **$Distance**  
  
-   **$Probability**  
  
## <a name="examples"></a>Ejemplos  
 El ejemplo siguiente devuelve el estado predicho de la columna Bike Buyer en una consulta singleton. La consulta también devuelve los Estados de dos primeras más probables del atributo Bike Buyer, en función de la probabilidad ajustada obtenida mediante el uso de la **PredictHistogram** función.  
  
```  
SELECT  
  [TM Decision Tree].[Bike Buyer],  
  TopCount(PredictHistogram([Bike Buyer]),$AdjustedProbability,3)  
From  
  [TM Decision Tree]  
NATURAL PREDICTION JOIN  
(SELECT 28 AS [Age],  
  '2-5 Miles' AS [Commute Distance],  
  'Graduate Degree' AS [Education],  
  0 AS [Number Cars Owned],  
  0 AS [Number Children At Home]) AS t  
```  
  
## <a name="see-also"></a>Vea también  
 [Clúster &#40;DMX&#41;](../dmx/cluster-dmx.md)   
 [ClusterProbability &#40;DMX&#41;](../dmx/clusterprobability-dmx.md)   
 [PredictAdjustedProbability &#40;DMX&#41;](../dmx/predictadjustedprobability-dmx.md)   
 [PredictProbability &#40;DMX&#41;](../dmx/predictprobability-dmx.md)   
 [PredictStdev &#40;DMX&#41;](../dmx/predictstdev-dmx.md)   
 [PredictSupport &#40;DMX&#41;](../dmx/predictsupport-dmx.md)   
 [PredictVariance &#40;DMX&#41;](../dmx/predictvariance-dmx.md)   
 [Algoritmos de minería de datos & #40; Analysis Services: minería de datos & #41;](../analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [Extensiones de minería de datos &#40;DMX&#41; Referencia de funciones](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Funciones &#40;DMX&#41;](../dmx/functions-dmx.md)   
 [Funciones de predicción generales &#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)  
  
  
