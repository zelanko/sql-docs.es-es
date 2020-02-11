---
title: Clúster (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: fa7df2782b8102e386c70d5e874a25f7868dbb1c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68071078"
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
  
## <a name="return-type"></a>Tipo de valor devuelto  
 La función de **clúster** no requiere parámetros.  
  
 La función de **clúster** devuelve un valor escalar de un nombre de clúster. Sin embargo, si usa esta función como argumento de otra función, debe tener en cuenta como una \<referencia de columna de clúster>.  
  
## <a name="remarks"></a>Observaciones  
 El **clúster** también se puede usar como `<`referencia`>` de columna de clúster para una función **PredictHistogram** .  
  
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
  
  
