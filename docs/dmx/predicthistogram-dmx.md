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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
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
  
## <a name="return-type"></a>Tipo de valor devuelto  
 Tabla.  
  
## <a name="remarks"></a>Observaciones  
 Los histogramas generan columnas de estadísticas. La estructura de columnas del histograma devuelto depende del tipo de referencia de columna que se usa con la función **PredictHistogram** .  
  
## <a name="scalar-columns"></a>Columnas escalares  
 En el \<caso de una referencia de columna escalar>, el histograma que devuelve la función **PredictHistogram** consta de las siguientes columnas:  
  
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
 El histograma que devuelve la función **PredictHistogram** para una \<referencia de columna de clúster> consta de las siguientes columnas:  
  
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
  
## <a name="see-also"></a>Consulte también  
 [&#41;de &#40;DMX de clúster](../dmx/cluster-dmx.md)   
 [&#41;ClusterProbability &#40;DMX](../dmx/clusterprobability-dmx.md)   
 [&#41;PredictAdjustedProbability &#40;DMX](../dmx/predictadjustedprobability-dmx.md)   
 [&#41;PredictProbability &#40;DMX](../dmx/predictprobability-dmx.md)   
 [&#41;PredictStdev &#40;DMX](../dmx/predictstdev-dmx.md)   
 [&#41;PredictSupport &#40;DMX](../dmx/predictsupport-dmx.md)   
 [&#41;PredictVariance &#40;DMX](../dmx/predictvariance-dmx.md)   
 [Algoritmos de minería de datos &#40;Analysis Services:&#41;de minería de datos](https://docs.microsoft.com/analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining)   
 [Referencia de funciones de extensiones de minería de datos &#40;DMX&#41;](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Funciones &#40;DMX&#41;](../dmx/functions-dmx.md)   
 [Funciones de predicción generales &#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)  
  
  
