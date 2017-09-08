---
title: PredictProbability (DMX) | Documentos de Microsoft
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- PredictProbability
dev_langs:
- DMX
helpviewer_keywords:
- PredictProbability function
ms.assetid: 7bb7e74f-e33b-4f7b-ade8-be21ace0dbd0
caps.latest.revision: 36
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 8e0cdcf4b193cf1b05967fdbc5b266ebd0ca9700
ms.contentlocale: es-es
ms.lasthandoff: 08/02/2017

---
# <a name="predictprobability-dmx"></a>PredictProbability (DMX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve la probabilidad de un estado especificado.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
PredictProbability(<scalar column reference>, [<predicted state>])  
```  
  
## <a name="applies-to"></a>Se aplica a  
 Una columna escalar.  
  
## <a name="return-type"></a>Tipo devuelto  
 Un valor escalar.  
  
## <a name="remarks"></a>Comentarios  
 Si se omite el estado predicho, se usa el estado que tenga la mayor probabilidad de predicción, sin incluir el depósito de estados que faltan. Para incluir el depósito de Estados que faltan, establezca el \<estado de predicción > a **INCLUDE_NULL**. Para devolver la probabilidad de los Estados que faltan, establezca el \<estado de predicción > en NULL.  
  
> [!NOTE]  
>  Algunos modelos de minería de datos no proporcionan los valores de probabilidad y, por consiguiente, no pueden utilizar esta función. Además, los valores de probabilidad de cualquier valor del objetivo determinado se calcula de manera diferente o podría tener una interpretación distinta que dependa del tipo de modelo que esté consultando. Para obtener más información sobre cómo se calcula la probabilidad para un tipo de modelo determinado, vea el tema de algoritmo individual en [contenido del modelo de minería de datos &#40; Analysis Services: minería de datos &#41; ](../analysis-services/data-mining/mining-model-content-analysis-services-data-mining.md).  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se utiliza una cláusula NATURAL PREDICTION JOIN para determinar si es probable que un individuo compre una bicicleta en función del modelo de minería de datos TM Decision Tree; también se determina la probabilidad de la predicción. En este ejemplo hay dos funciones PredictProbability, una para cada valor posible. Si omite este argumento, la función devuelve la probabilidad para el valor más probable.  
  
```  
SELECT  
  [Bike Buyer],  
  PredictProbability([Bike Buyer], 1) AS [Bike Buyer = Yes],  
  PredictProbability([Bike Buyer], 0) AS [Bike Buyer = No]  
FROM [TM Decision Tree]  
NATURAL PREDICTION JOIN  
(SELECT 28 AS [Age],  
  '2-5 Miles' AS [Commute Distance],  
  'Graduate Degree' AS [Education],  
  0 AS [Number Cars Owned],  
  0 AS [Number Children At Home]) AS t  
```  
  
 Resultados del ejemplo:  
  
|Bike Buyer|Bike Buyer = Sí|Bike Buyer = No|  
|----------------|-----------------------|----------------------|  
|1|0.867074195848097|0.132755556974282|  
  
## <a name="see-also"></a>Vea también  
 [Extensiones de minería de datos &#40; DMX &#41; Referencia de funciones](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Funciones &#40; DMX &#41;](../dmx/functions-dmx.md)   
 [Funciones de predicción generales &#40; DMX &#41;](../dmx/general-prediction-functions-dmx.md)  
  
  

