---
title: Clúster (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 0cd7b2e0a78f2d47349de2701572b2f9dc4b0095
ms.sourcegitcommit: 205de8fa4845c491914902432791bddf11002945
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/23/2020
ms.locfileid: "86969931"
---
# <a name="cluster-dmx"></a>Cluster (DMX)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  Devuelve el clúster que tiene la mayor probabilidad de contener el caso de entrada.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Cluster()  
```  
  
## <a name="applies-to"></a>Se aplica a  
 Esta función solo se puede utilizar si el modelo de minería de datos subyacente admite la agrupación en clústeres.  
  
## <a name="return-type"></a>Tipo de valor devuelto  
 La función de **clúster** no requiere parámetros.  
  
 La función de **clúster** devuelve un valor escalar de un nombre de clúster. Sin embargo, si usa esta función como argumento de otra función, debe tener en cuenta como \<cluster column reference> .  
  
## <a name="remarks"></a>Observaciones  
 El **clúster** también se puede usar como `<` referencia de columna `>` de clúster para una función **PredictHistogram** .  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se usa una consulta singleton con las funciones de clúster y [&#41;DMX &#40;DMX](../dmx/predicthistogram-dmx.md) para devolver la distancia del caso individual de cada clúster del modelo de minería de datos de clústeres de TM y la probabilidad de que el caso individual exista en cada clúster.  
  
```  
SELECT  
  PredictHistogram(Cluster())  
FROM  
  [TM Clustering]  
  NATURAL PREDICTION JOIN  
(SELECT 28 AS [Age],  
  '2-5 Miles' AS [Commute Distance],  
  'Graduate Degree' AS [Education],  
  0 AS [Number Cars Owned],  
  0 AS [Number Children At Home]) AS t  
```  
  
## <a name="see-also"></a>Consulte también  
 [&#41;ClusterProbability &#40;DMX](../dmx/clusterprobability-dmx.md)   
 [Referencia de funciones de extensiones de minería de datos &#40;DMX&#41;](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Funciones &#40;DMX&#41;](../dmx/functions-dmx.md)   
 [Funciones de predicción generales &#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)  
  
  
