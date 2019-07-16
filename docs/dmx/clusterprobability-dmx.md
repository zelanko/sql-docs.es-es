---
title: ClusterProbability (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 9beac713ec9a8b5a549602809d3612e4e29e67c6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68071952"
---
# <a name="clusterprobability-dmx"></a>ClusterProbability (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Devuelve la probabilidad de que el caso de entrada pertenezca al clúster especificado.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
ClusterProbability([<Node_Caption>])  
```  
  
## <a name="applies-to"></a>Se aplica a  
 Esta función solo se puede utilizar si el modelo de minería de datos subyacente admite la agrupación en clústeres.  
  
## <a name="return-type"></a>Tipo devuelto  
 Un valor escalar.  
  
## <a name="remarks"></a>Comentarios  
 La siguiente sintaxis usa el conjunto de filas de esquema CONTENT del modelo de minería de datos para devolver los títulos de nodo que existen en el modelo de minería de datos.  
  
```  
SELECT NODE_CAPTION FROM <model>.CONTENT  
```  
  
 Para obtener más información sobre el uso de esta sintaxis, vea [SELECT FROM &#60;modelo&#62;. CONTENIDO &#40;DMX&#41;](../dmx/select-from-model-content-dmx.md). Para obtener más información sobre el conjunto de filas de esquema de contenido de modelo de minería de datos, vea [de filas DMSCHEMA_MINING_MODEL_CONTENT](https://docs.microsoft.com/bi-reference/schema-rowsets/data-mining/dmschema-mining-model-content-rowset).  
  
 Si un \<título del nodo > no se especifica, la función devuelve la probabilidad de que los casos de entrada pertenecen al clúster más probable. Use la **clúster** función para devolver el clúster más probable.  
  
## <a name="examples"></a>Ejemplos  
 El ejemplo siguiente devuelve la probabilidad de que el caso especificado exista en el clúster que presenta la etiqueta Cluster 2.  
  
```  
SELECT  
  ClusterProbability('Cluster 2')  
From  
  [TM Clustering]  
NATURAL PREDICTION JOIN  
(SELECT 28 AS [Age],  
  '2-5 Miles' AS [Commute Distance],  
  'Graduate Degree' AS [Education],  
  0 AS [Number Cars Owned],  
  0 AS [Number Children At Home]) AS t  
```  
  
## <a name="see-also"></a>Vea también  
 [Clúster &#40;DMX&#41;](../dmx/cluster-dmx.md)   
 [Extensiones de minería de datos &#40;DMX&#41; referencia de funciones](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Funciones &#40;DMX&#41;](../dmx/functions-dmx.md)   
 [Funciones de predicción generales &#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)  
  
  
