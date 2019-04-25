---
title: Lag (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 0f984e50b2c6a800a66f689d88b21dfcb487e282
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62503552"
---
# <a name="lag-dmx"></a>Lag (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Devuelve el período de tiempo transcurrido entre la fecha del caso actual y la última fecha del conjunto de entrenamiento.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Lag()  
```  
  
## <a name="return-type"></a>Tipo devuelto  
 Un valor escalar del tipo integer.  
  
## <a name="remarks"></a>Comentarios  
 Si el **Lag** función se utiliza en un modelo donde la columna KEY TIME se encuentra dentro de una tabla anidada, la función debe encontrarse dentro de la subselección de la instrucción.  
  
## <a name="examples"></a>Ejemplos  
 El ejemplo siguiente devuelve los casos que tienen lugar dentro de los 12 últimos meses de los datos que se han utilizado para formar al modelo.  
  
```  
SELECT * FROM [Forecasting].CASES  
WHERE Lag() < 12  
```  
  
## <a name="see-also"></a>Vea también  
 [Extensiones de minería de datos &#40;DMX&#41; referencia de funciones](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Funciones &#40;DMX&#41;](../dmx/functions-dmx.md)   
 [Funciones de predicción generales &#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)  
  
  
