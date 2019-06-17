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
manager: kfile
ms.openlocfilehash: f7e7129985eac09d741ea9d00c551a9507ee92c9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62659179"
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
 Los histogramas generan columnas de estadísticas. La estructura de columnas del histograma devuelto depende del tipo de referencia de columna que se usa con el **PredictHistogram** función.  
  
## <a name="scalar-columns"></a>Columnas escalares  
 Para un \<referencia de columna escalar >, el histograma que la **PredictHistogram** devueltos de función consta de las siguientes columnas:  
  
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
 El histograma que la **PredictHistogram** función devuelve para un \<referencia de columna de clúster > consta de las siguientes columnas:  
  
-   **$Cluster** (representa el nombre del clúster)  
  
-   **$Distance**  
  
-   **$Probability**  
  
## <a name="examples"></a>Ejemplos  
 El ejemplo siguiente devuelve el estado predicho de la columna Bike Buyer en una consulta singleton. La consulta también devuelve los Estados de dos primeras más probables del atributo Bike Buyer, según la probabilidad ajustada obtenida mediante el uso de la **PredictHistogram** función.  
  
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
 [Cluster &#40;DMX&#41;](../dmx/cluster-dmx.md)   
 [ClusterProbability &#40;DMX&#41;](../dmx/clusterprobability-dmx.md)   
 [PredictAdjustedProbability &#40;DMX&#41;](../dmx/predictadjustedprobability-dmx.md)   
 [PredictProbability &#40;DMX&#41;](../dmx/predictprobability-dmx.md)   
 [PredictStdev &#40;DMX&#41;](../dmx/predictstdev-dmx.md)   
 [PredictSupport &#40;DMX&#41;](../dmx/predictsupport-dmx.md)   
 [PredictVariance &#40;DMX&#41;](../dmx/predictvariance-dmx.md)   
 [Algoritmos de minería de datos &#40;Analysis Services: Minería de datos&#41;](../analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [Extensiones de minería de datos &#40;DMX&#41; referencia de funciones](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Funciones &#40;DMX&#41;](../dmx/functions-dmx.md)   
 [Funciones de predicción generales &#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)  
  
  
