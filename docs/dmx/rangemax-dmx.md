---
title: RangeMax (DMX) | Documentos de Microsoft
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
f1_keywords:
- RangeMax
dev_langs:
- DMX
helpviewer_keywords:
- RangeMax function
ms.assetid: 6798d9d7-c3dc-40fb-bd8e-56cb1a6d0e5f
caps.latest.revision: 31
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 8b8cb363e9d5db767ed172206f497ff300bb29a6
ms.contentlocale: es-es
ms.lasthandoff: 08/02/2017

---
# <a name="rangemax-dmx"></a>RangeMax (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Devuelve el extremo superior del depósito predicho que se descubre para una columna de datos discretos.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
RangeMax(<scalar column reference>)  
```  
  
## <a name="applies-to"></a>Se aplica a  
 Columnas escalares.  
  
## <a name="return-type"></a>Tipo devuelto  
 Un valor escalar.  
  
## <a name="remarks"></a>Comentarios  
 El **RangeMax** función puede utilizarse en [SELECT DISTINCT FROM &#60; modelo de &#62; &#40; DMX &#41;](../dmx/select-distinct-from-model-dmx.md) consultas. Cuando se usa con este tipo de consulta, la referencia de columna escalar puede contener columnas continuas o discretas que son de predicción o de entrada.  
  
 Cuando se usa con [SELECT FROM &#60; modelo &#62; COMBINACIÓN de PREDICCIÓN &#40; DMX &#41; ](../dmx/select-from-model-prediction-join-dmx.md), **RangeMin**, **RangeMid**, y **RangeMax** funciones devuelven los valores de límite reales del depósito especificado. Por ejemplo, si realiza una predicción en una columna de datos discretos, la consulta devuelve el número de depósito predicho de la columna de datos discretos. El **RangeMin**, **RangeMid**, y **RangeMax** funciones describen el depósito que especifica la predicción. Cuando el **RangeMax** función se utiliza con una instrucción PREDICTION JOIN, la referencia de columna escalar solo puede contener columnas discretas y predecibles.  
  
## <a name="examples"></a>Ejemplos  
 El ejemplo siguiente devuelve los valores mínimo, máximo y promedio para la columna continua Yearly Income en el modelo de minería de datos Decision Tree.  
  
```  
SELECT DISTINCT   
    RangeMin([Yearly Income]) AS [Bucket Minimum],  
    RangeMid([Yearly Income]) AS [Bucket Average],   
    RangeMax([Yearly Income]) AS [Bucket Maximum]  
FROM [TM Decision Tree]  
```  
  
## <a name="see-also"></a>Vea también  
 [Extensiones de minería de datos &#40; DMX &#41; Referencia de funciones](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Funciones &#40; DMX &#41;](../dmx/functions-dmx.md)   
 [Funciones de predicción generales &#40; DMX &#41;](../dmx/general-prediction-functions-dmx.md)   
 [RangeMid &#40; DMX &#41;](../dmx/rangemid-dmx.md)   
 [RangeMin &#40; DMX &#41;](../dmx/rangemin-dmx.md)  
  
  

