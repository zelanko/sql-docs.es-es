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
ms.openlocfilehash: 04b06d1cbe14ee83915bd5626337720acf9bd2a9
ms.sourcegitcommit: 4cb53a8072dbd94a83ed8c7409de2fb5e2a1a0d9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/19/2020
ms.locfileid: "83670346"
---
# <a name="lag-dmx"></a>Lag (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

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
  
  
