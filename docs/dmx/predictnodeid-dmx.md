---
description: PredictNodeId (DMX)
title: PredictNodeId (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 3fac7baa2f30d20c8e5043a405156a36f43a29a4
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88426137"
---
# <a name="predictnodeid-dmx"></a>PredictNodeId (DMX)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  Devuelve el Node_ID del nodo en que está clasificado el caso.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
PredictNodeId(<scalar column reference>)  
```  
  
## <a name="applies-to"></a>Se aplica a  
 Una columna escalar.  
  
## <a name="return-type"></a>Tipo de valor devuelto  
 \<scalar expression>  
  
## <a name="examples"></a>Ejemplos  
 El ejemplo siguiente indica si el individuo especificado es probable que compre una bicicleta y también indica el Id. del nodo del que es más probable que forme parte.  
  
```  
SELECT  
  [Bike Buyer],  
  PredictNodeId([Bike Buyer])  
From  
  [TM Decision Tree]  
NATURAL PREDICTION JOIN  
(SELECT 28 AS [Age],  
  '2-5 Miles' AS [Commute Distance],  
  'Graduate Degree' AS [Education],  
  0 AS [Number Cars Owned],  
  0 AS [Number Children At Home]) AS t  
```  
  
 Luego puede utilizar la siguiente instrucción para determinar el contenido del nodo:  
  
```  
SELECT   
  NODE_CAPTION   
FROM   
  [TM Decision Tree].CONTENT  
WHERE NODE_UNIQUE_NAME= '00000000100'   
```  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de funciones de extensiones de minería de datos &#40;DMX&#41;](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Funciones &#40;DMX&#41;](../dmx/functions-dmx.md)   
 [Funciones de predicción generales &#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)  
  
  
