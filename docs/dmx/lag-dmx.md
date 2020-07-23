---
title: Lag (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: e011fc48b63aa653cd63e11678b84d8356370bd0
ms.sourcegitcommit: 205de8fa4845c491914902432791bddf11002945
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/23/2020
ms.locfileid: "86969356"
---
# <a name="lag-dmx"></a>Lag (DMX)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  Devuelve el período de tiempo transcurrido entre la fecha del caso actual y la última fecha del conjunto de entrenamiento.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Lag()  
```  
  
## <a name="return-type"></a>Tipo de valor devuelto  
 Un valor escalar del tipo integer.  
  
## <a name="remarks"></a>Observaciones  
 Si se usa la función **lag** en un modelo en el que la columna Key Time está ubicada en una tabla anidada, la función debe estar ubicada dentro de la subselección de la instrucción.  
  
## <a name="examples"></a>Ejemplos  
 El ejemplo siguiente devuelve los casos que tienen lugar dentro de los 12 últimos meses de los datos que se han utilizado para formar al modelo.  
  
```  
SELECT * FROM [Forecasting].CASES  
WHERE Lag() < 12  
```  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de funciones de extensiones de minería de datos &#40;DMX&#41;](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Funciones &#40;DMX&#41;](../dmx/functions-dmx.md)   
 [Funciones de predicción generales &#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)  
  
  
