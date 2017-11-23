---
title: IsInNode (DMX) | Documentos de Microsoft
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: IsInNode
dev_langs: DMX
helpviewer_keywords: IsInNode function
ms.assetid: 47b2114f-9ad6-45cc-9498-193ad6fa5288
caps.latest.revision: "29"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 895fe529a2fc67528d37b19202575aa0b9c14116
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/20/2017
---
# <a name="isinnode-dmx"></a>IsInNode (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Indica si el nodo especificado contiene el caso actual.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
IsInNode(<NodeID>)  
```  
  
## <a name="return-type"></a>Tipo devuelto  
 Un tipo booleano.  
  
## <a name="remarks"></a>Comentarios  
 **IsInNode** solo se usa en [SELECT FROM &#60; modelo &#62;. CASOS &#40; DMX &#41; ](../dmx/select-from-model-cases-dmx.md) y [SELECT FROM &#60; modelo &#62;. SAMPLE_CASES &#40; DMX &#41; ](../dmx/select-from-model-sample-cases-dmx.md) consultas.  
  
## <a name="examples"></a>Ejemplos  
 El ejemplo siguiente devuelve todos los casos que se han utilizado para crear el modelo que está asociado al nodo especificado en la función IsInNode.  
  
```  
Select * from [TM Decision Tree].Cases  
WHERE IsInNode('0')  
```  
  
## <a name="see-also"></a>Vea también  
 [Extensiones de minería de datos &#40; DMX &#41; Referencia de funciones](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Funciones &#40; DMX &#41;](../dmx/functions-dmx.md)   
 [Funciones de predicción generales &#40; DMX &#41;](../dmx/general-prediction-functions-dmx.md)  
  
  
