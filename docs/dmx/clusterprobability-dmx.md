---
title: ClusterProbability (DMX) | Documentos de Microsoft
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
- ClusterProbability
dev_langs:
- DMX
helpviewer_keywords:
- ClusterProbability function
ms.assetid: a6447b3c-94ce-4122-a3eb-6f3827598d8f
caps.latest.revision: 35
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: dd1e979a3613dc95566875a57fc422c59dbc5074
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
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
  
 Para obtener más información sobre el uso de esta sintaxis, vea [SELECT FROM &#60;modelo&#62;. CONTENIDO &#40;DMX&#41;](../dmx/select-from-model-content-dmx.md). Para obtener más información sobre el conjunto de filas de esquema de contenido de modelo de minería de datos, vea [de filas DMSCHEMA_MINING_MODEL_CONTENT](../analysis-services/schema-rowsets/data-mining/dmschema-mining-model-content-rowset.md).  
  
 Si un \<título del nodo > no se especifica, la función devuelve la probabilidad de que los casos de entrada pertenezcan al clúster más probable. Use la **clúster** función para devolver el clúster más probable.  
  
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
 [Extensiones de minería de datos &#40;DMX&#41; Referencia de funciones](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Funciones &#40;DMX&#41;](../dmx/functions-dmx.md)   
 [Funciones de predicción generales &#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)  
  
  
