---
title: PredictSupport (DMX) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: data-mining
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- PredictSupport
dev_langs:
- DMX
helpviewer_keywords:
- PredictSupport function
ms.assetid: 325437d6-7cb5-4ae0-8abe-edb58fe5e90d
caps.latest.revision: 35
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: bd626493ce217fed886e699519e207bbb7df66c1
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
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
  
## <a name="return-type"></a>Tipo devuelto  
 Un valor escalar del tipo especificado por *\<* referencia de columna escalar*>*.  
  
## <a name="remarks"></a>Comentarios  
 Si se omite el estado predicho, se usa el estado que tiene la mayor probabilidad de predicción, sin incluir el depósito de estados que falta. Para incluir el depósito de Estados que faltan, establezca el \<estado de predicción > a **INCLUDE_NULL**.  
  
 Para devolver la compatibilidad con los Estados que faltan, establezca el \<estado de predicción > en NULL.  
  
> [!NOTE]  
>  Los valores de compatibilidad se calculan de manera diferente o pueden tener una interpretación distinta en función del tipo de modelo que se está consultando. Para obtener más información sobre cómo se calcula el soporte técnico para cualquier tipo de modelo determinado, vea el algoritmo individual escriba [contenido del modelo de minería de datos &#40;Analysis Services: minería de datos&#41;](../analysis-services/data-mining/mining-model-content-analysis-services-data-mining.md).  
  
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
  
## <a name="see-also"></a>Vea también  
 [Extensiones de minería de datos &#40;DMX&#41; Referencia de funciones](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Funciones &#40;DMX&#41;](../dmx/functions-dmx.md)   
 [Funciones de predicción generales &#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)  
  
  
