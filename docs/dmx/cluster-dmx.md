---
title: Clúster (DMX) | Documentos de Microsoft
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
- Cluster
dev_langs:
- DMX
helpviewer_keywords:
- Cluster function
ms.assetid: 14b2942a-6dec-4dfa-98a6-697a3c89036a
caps.latest.revision: 34
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: cec73e5b3c182073cfad14c3605183fe72732d72
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/08/2018
---
# <a name="cluster-dmx"></a>Cluster (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Devuelve el clúster que tiene la mayor probabilidad de contener el caso de entrada.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Cluster()  
```  
  
## <a name="applies-to"></a>Se aplica a  
 Esta función solo se puede utilizar si el modelo de minería de datos subyacente admite la agrupación en clústeres.  
  
## <a name="return-type"></a>Tipo devuelto  
 El **clúster** función no requiere parámetros.  
  
 El **clúster** función devuelve un valor escalar de un nombre de clúster. Sin embargo, si usa esta función como un argumento de otra función, se debe considerar como un \<referencia a una columna de clúster >.  
  
## <a name="remarks"></a>Comentarios  
 **Clúster** también puede usarse como un `<`referencia a una columna de clúster`>` para un **PredictHistogram** función.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se utiliza una consulta singleton con el [PredictHistogram &#40; DMX &#41;](../dmx/predicthistogram-dmx.md) y funciones para devolver la distancia del caso individual de cada clúster del modelo de minería de datos TM Clustering y la probabilidad de que dicho caso exista en cada clúster del clúster.  
  
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
  
## <a name="see-also"></a>Vea también  
 [ClusterProbability &#40; DMX &#41;](../dmx/clusterprobability-dmx.md)   
 [Extensiones de minería de datos &#40; DMX &#41; Referencia de funciones](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Funciones &#40; DMX &#41;](../dmx/functions-dmx.md)   
 [Funciones de predicción generales &#40; DMX &#41;](../dmx/general-prediction-functions-dmx.md)  
  
  
