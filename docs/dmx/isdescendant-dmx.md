---
description: IsDescendant (DMX)
title: IsDescendant (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 9fe1c150f243e78c379823427e9940bba3680cb1
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88352651"
---
# <a name="isdescendant-dmx"></a>IsDescendant (DMX)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  Indica si el nodo actual desciende del nodo especificado.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
IsDescendant(<NodeID>)  
```  
  
## <a name="return-type"></a>Tipo de valor devuelto  
 Tipo Boolean.  
  
## <a name="remarks"></a>Observaciones  
 **IsDescendant** solo se usa en [SELECT desde &#60;&#62; de modelo. CONTENT &#40;DMX&#41;](../dmx/select-from-model-content-dmx.md) y [seleccione de &#60;Modelo&#62;. DIMENSION_CONTENT las consultas &#40;DMX&#41;](../dmx/select-from-model-dimension-content-dmx.md) .  
  
## <a name="examples"></a>Ejemplos  
 El ejemplo siguiente devuelve todos los casos que son descendientes del nodo especificado en la función IsDescendant.  
  
```  
SELECT * FROM [TM Decision Tree].CONTENT  
WHERE IsDescendant('00000000100')  
```  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de funciones de extensiones de minería de datos &#40;DMX&#41;](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Funciones &#40;DMX&#41;](../dmx/functions-dmx.md)   
 [Funciones de predicción generales &#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)  
  
  
