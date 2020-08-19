---
description: ClusterProbability (DMX)
title: ClusterProbability (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: f27a901bbb45c48996c82bbedbbb3691c1a6cbc2
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88431117"
---
# <a name="clusterprobability-dmx"></a>ClusterProbability (DMX)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  Devuelve la probabilidad de que el caso de entrada pertenezca al clúster especificado.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
ClusterProbability([<Node_Caption>])  
```  
  
## <a name="applies-to"></a>Se aplica a  
 Esta función solo se puede utilizar si el modelo de minería de datos subyacente admite la agrupación en clústeres.  
  
## <a name="return-type"></a>Tipo de valor devuelto  
 Un valor escalar.  
  
## <a name="remarks"></a>Observaciones  
 La siguiente sintaxis usa el conjunto de filas de esquema CONTENT del modelo de minería de datos para devolver los títulos de nodo que existen en el modelo de minería de datos.  
  
```  
SELECT NODE_CAPTION FROM <model>.CONTENT  
```  
  
 Para obtener más información sobre el uso de esta sintaxis, vea [SELECT FROM &#60;model&#62;. CONTENT &#40;DMX&#41;](../dmx/select-from-model-content-dmx.md). Para obtener más información sobre el conjunto de filas de esquema de contenido del modelo de minería de datos, vea [DMSCHEMA_MINING_MODEL_CONTENT conjunto de filas](https://docs.microsoft.com/previous-versions/sql/sql-server-2012/ms126267(v=sql.110)).  
  
 Si \<node caption> no se especifica, la función devuelve la probabilidad de que los casos de entrada pertenezcan al clúster más probable. Use la función **cluster** para devolver el clúster más probable.  
  
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
  
## <a name="see-also"></a>Consulte también  
 [&#41;de &#40;DMX de clúster ](../dmx/cluster-dmx.md)   
 [Referencia de funciones de extensiones de minería de datos &#40;DMX&#41;](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Funciones &#40;DMX&#41;](../dmx/functions-dmx.md)   
 [Funciones de predicción generales &#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)  
  
  
