---
title: PredictAdjustedProbability (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 735df047307f78c238fbf29669f0e0b1e0933e37
ms.sourcegitcommit: 205de8fa4845c491914902432791bddf11002945
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/23/2020
ms.locfileid: "86971571"
---
# <a name="predictadjustedprobability-dmx"></a>PredictAdjustedProbability (DMX)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  Devuelve la probabilidad ajustada de un estado especificado.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
PredictAdjustedProbability(<scalar column reference>, [<predicted state>])  
```  
  
## <a name="applies-to"></a>Se aplica a  
 Una columna escalar.  
  
## <a name="return-type"></a>Tipo de valor devuelto  
 Un valor escalar.  
  
## <a name="remarks"></a>Observaciones  
 Si se omite el estado predicho, se usa el estado que tiene la mayor probabilidad de predicción, sin incluir el depósito de estados que falta. Para incluir el depósito de Estados que faltan, establezca \<predicted state> en **INCLUDE_NULL**.  
  
 Para devolver la probabilidad ajustada para los Estados que faltan, establezca \<predicted state> en NULL.  
  
 La función **PredictAdjustedProbability** es una [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] extensión del [!INCLUDE[msCoName](../includes/msconame-md.md)] OLE DB para la especificación de minería de datos.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se utiliza una cláusula NATURAL PREDICTION JOIN para determinar si es probable que un individuo compre una bicicleta en función del modelo de minería de datos TM Decision Tree; también se determina la probabilidad ajustada para la predicción.  
  
```  
SELECT  
  [Bike Buyer],  
  PredictAdjustedProbability([Bike Buyer]) AS [Adjusted Probability]  
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
  
  
