---
title: RangeMid (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 8450107e9d591b8d789037303edbcaeea1ec08e5
ms.sourcegitcommit: 4cb53a8072dbd94a83ed8c7409de2fb5e2a1a0d9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/19/2020
ms.locfileid: "83669636"
---
# <a name="rangemid-dmx"></a>RangeMid (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Devuelve el punto medio del depósito predicho que se descubre para una columna de datos discretos.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
RangeMid(<scalar column reference>)  
```  
  
## <a name="applies-to"></a>Se aplica a  
 Columnas escalares de datos discretos.  
  
## <a name="return-type"></a>Tipo de valor devuelto  
 Un valor escalar.  
  
## <a name="remarks"></a>Observaciones  
 Cuando se usa con [Select desde &#60;modelo&#62; combinación de predicción &#40;DMX&#41;](../dmx/select-from-model-prediction-join-dmx.md), las funciones **RangeMin**, **RangeMid**y **RangeMax** devuelven los valores de límite reales del depósito especificado. Por ejemplo, si realiza una predicción en una columna de datos discretos, la consulta devuelve el número de depósito predicho de la columna de datos discretos. Las funciones **RangeMin**, **RangeMid**y **RangeMax** describen el depósito que especifica la predicción. Cuando la función **RangeMid** se utiliza con una instrucción de combinación de predicción, la referencia de columna escalar solo puede contener columnas discretas y de predicción.  
  
## <a name="examples"></a>Ejemplos  
 El ejemplo siguiente devuelve los valores mínimo, máximo y promedio para la columna continua Yearly Income en un modelo de minería de datos TM Decision Tree.  
  
```  
SELECT DISTINCT   
    RangeMin([Yearly Income]) AS [Bucket Minimum],  
    RangeMid([Yearly Income]) AS [Bucket Average],   
    RangeMax([Yearly Income]) AS [Bucket Maximum]  
FROM [TM Decision Tree]  
```  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de funciones de extensiones de minería de datos &#40;DMX&#41;](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Funciones &#40;DMX&#41;](../dmx/functions-dmx.md)   
 [Funciones de predicción generales &#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)   
 [&#41;de RangeMax &#40;DMX](../dmx/rangemax-dmx.md)   
 [&#41;RangeMin &#40;DMX](../dmx/rangemin-dmx.md)  
  
  
