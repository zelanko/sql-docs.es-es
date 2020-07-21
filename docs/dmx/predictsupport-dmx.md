---
title: PredictSupport (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 7a6509980065c2293a0b2697beacae1ba2d4b0d1
ms.sourcegitcommit: 4cb53a8072dbd94a83ed8c7409de2fb5e2a1a0d9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/19/2020
ms.locfileid: "83667189"
---
# <a name="predictsupport-dmx"></a>PredictSupport (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Devuelve el valor de soporte de un estado especificado.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
PredictSupport(<scalar column reference>, [<predicted state>])  
```  
  
## <a name="applies-to"></a>Se aplica a  
 Una columna escalar.  
  
## <a name="return-type"></a>Tipo de valor devuelto  
 Valor escalar del tipo especificado por la referencia de *\<* columna escalar *>* .  
  
## <a name="remarks"></a>Observaciones  
 Si se omite el estado predicho, se usa el estado que tiene la mayor probabilidad de predicción, sin incluir el depósito de estados que falta. Para incluir el depósito de Estados que faltan, establezca el \<> de estado de predicción en **INCLUDE_NULL**.  
  
 Para devolver la compatibilidad de los Estados que faltan, establezca el \<> de estado de predicción en NULL.  
  
> [!NOTE]  
>  Los valores de compatibilidad se calculan de manera diferente o pueden tener una interpretación distinta en función del tipo de modelo que se está consultando. Para obtener más información sobre cómo se calcula la compatibilidad para un tipo de modelo concreto, vea el tipo de algoritmo individual en el [contenido del modelo de minería de datos &#40;Analysis Services-Data Mining&#41;](https://docs.microsoft.com/analysis-services/data-mining/mining-model-content-analysis-services-data-mining).  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se utiliza una consulta singleton para predecir si un individuo comprará una bicicleta, y también determina el soporte para la predicción en función del modelo de minería de datos TM Decision Tree.  
  
```  
SELECT  
  [Bike Buyer],  
  PredictSupport([Bike Buyer]) AS [Support],  
From  
  [TM Decision Tree]  
NATURAL PREDICTION JOIN  
(SELECT 28 AS [Age],  
  '2-5 Miles' AS [Commute Distance],  
  'Graduate Degree' AS [Education],  
  0 AS [Number Cars Owned],  
  0 AS [Number Children At Home]) AS t  
```  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de funciones de extensiones de minería de datos &#40;DMX&#41;](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Funciones &#40;DMX&#41;](../dmx/functions-dmx.md)   
 [Funciones de predicción generales &#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)  
  
  
