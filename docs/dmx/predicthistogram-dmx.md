---
title: PredictHistogram (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: fdc63d1c93d1290c701233cb94f71f157c771182
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/09/2019
ms.locfileid: "68893848"
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
 Los histogramas generan columnas de estadísticas. La estructura de columnas del histograma devuelto depende del tipo de referencia de columna que se usa con la función **PredictHistogram** .  
  
## <a name="scalar-columns"></a>Columnas escalares  
 En el \<caso de una referencia de columna escalar >, el histograma que devuelve la función **PredictHistogram** consta de las siguientes columnas:  
  
-   El valor que se predice.  
  
-   **$Support**  
  
-   **$Probability**  
  
-   **$ProbabilityVariance**  
  
     [!INCLUDE[msCoName](../includes/msconame-md.md)]los algoritmos de minería de datos no admiten **$ProbabilityVariance**. Esta columna siempre contiene 0 para los algoritmos de [!INCLUDE[msCoName](../includes/msconame-md.md)].  
  
-   **$ProbabilityStdev**  
  
     [!INCLUDE[msCoName](../includes/msconame-md.md)]los algoritmos de minería de datos no admiten **$ProbabilityStdev**. Esta columna siempre contiene 0 para los algoritmos de [!INCLUDE[msCoName](../includes/msconame-md.md)].  
  
-   **$AdjustedProbability**  
  
     La columna **$AdjustedProbability** es una [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] extensión del OLE DB [!INCLUDE[msCoName](../includes/msconame-md.md)] para la especificación de minería de datos.  
  
## <a name="cluster-columns"></a>Columnas de clúster  
 El histograma que devuelve la función **PredictHistogram** para una \<referencia de columna de clúster > consta de las siguientes columnas:  
  
-   **$Cluster** (representa el nombre del clúster)  
  
-   **$Distance**  
  
-   **$Probability**  
  
## <a name="examples"></a>Ejemplos  
 El ejemplo siguiente devuelve el estado predicho de la columna Bike Buyer en una consulta singleton. La consulta también devuelve los dos Estados más probables del atributo Bike Buyer, en función de la probabilidad ajustada obtenida mediante la función **PredictHistogram** .  
  
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
 [DMX &#40;de clúster&#41;](../dmx/cluster-dmx.md)   
 [DMX &#40;ClusterProbability&#41;](../dmx/clusterprobability-dmx.md)   
 [PredictAdjustedProbability &#40;DMX&#41;](../dmx/predictadjustedprobability-dmx.md)   
 [PredictProbability &#40;DMX&#41;](../dmx/predictprobability-dmx.md)   
 [PredictStdev &#40;DMX&#41;](../dmx/predictstdev-dmx.md)   
 [PredictSupport &#40;DMX&#41;](../dmx/predictsupport-dmx.md)   
 [PredictVariance &#40;DMX&#41;](../dmx/predictvariance-dmx.md)   
 [Algoritmos de minería de datos &#40;Analysis Services: Minería de datos&#41;](https://docs.microsoft.com/analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining)   
 [Referencia de funciones &#40;DMX&#41; de extensiones de minería de datos](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [DMX &#40;de funciones&#41;](../dmx/functions-dmx.md)   
 [Funciones &#40;de predicción generales DMX&#41;](../dmx/general-prediction-functions-dmx.md)  
  
  
