---
title: PredictAssociation (DMX) | Documentos de Microsoft
ms.custom: ''
ms.date: 09/14/2016
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
- PredictAssociation
dev_langs:
- DMX
helpviewer_keywords:
- PredictAssociation function
ms.assetid: 33eb66b5-84c6-449f-aaae-316345bc4ad5
caps.latest.revision: 33
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 09933a65f19ca025c8a681b068bf31c6fe0e9d7b
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/08/2018
---
# <a name="predictassociation-dmx"></a>PredictAssociation (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Predice los miembros de asociaciones.  
  
Por ejemplo, puede usar la función PredictAssociation para obtener el conjunto de recomendaciones dado el estado actual de la cesta de compra de un cliente. 
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
PredictAssociation(<table column reference>, option1, option2, n ...)  
```  
  
## <a name="applies-to"></a>Se aplica a  
 Algoritmos que contienen tablas anidadas predicción, incluidos algunos algoritmos de clasificación y asociación. Los algoritmos de clasificación que admiten tablas anidadas se incluyen la [!INCLUDE[msCoName](../includes/msconame-md.md)] árboles de decisión, [!INCLUDE[msCoName](../includes/msconame-md.md)] Bayes Naive, y [!INCLUDE[msCoName](../includes/msconame-md.md)] algoritmos de red neuronal.  
  
## <a name="return-type"></a>Tipo devuelto  
 \<expresión de tabla >  
  
## <a name="remarks"></a>Comentarios  
 Las opciones para la **PredictAssociation** función incluye EXCLUDE_NULL, INCLUDE_NULL, INCLUSIVE, EXCLUSIVE (predeterminada), INPUT_ONLY, INCLUDE_STATISTICS e INCLUDE_NODE_ID.  
  
> [!NOTE]  
>  INCLUSIVE, EXCLUSIVE, INPUT_ONLY e INCLUDE_STATISTICS solo se aplican a una referencia de columna de tabla, mientras que EXCLUDE_NULL e INCLUDE_NULL se aplican exclusivamente a una referencia de columna escalar.  
  
 INCLUDE_STATISTICS solo devuelve **$Probability** y **$AdjustedProbability**.  
  
 Si el parámetro numérico  *n*  se especifica, el **PredictAssociation** función devuelve los valores más probables n superiores en función de la probabilidad:  
  
```  
PredictAssociation(colref, [$AdjustedProbability], n)  
```  
  
 Si incluye **$AdjustedProbability**, la instrucción devuelve la parte superior  *n*  valores basados en la **$AdjustedProbability**.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se usa el **PredictAssociation** función para devolver los cuatro productos de Adventure Works de bases de datos que es más probable que pueden vender juntos.  
  
```  
SELECT  
  PredictAssociation([Association].[v Assoc Seq Line Items],4)  
From  
  [Association]  
```  
En el ejemplo siguiente se muestra cómo puede utilizar una tabla anidada como entrada para la función de predicción, mediante la cláusula SHAPE. La consulta SHAPE crea un conjunto de filas con customerId como una columna y una tabla anidada como una segunda columna, que contiene la lista de productos que ya ha traído un cliente. 

~~~~
SELECT T.[CustomerId], PredictAssociation(MyNestedTable, 5) // returns top 5 associated items
FROM My Model
PREDICTION JOIN
SHAPE {
    OPENQUERY([Adventure Works DW],'SELECT CustomerID, OrderNumber
    FROM vAssocSeqOrders ORDER BY OrderNumber')
} APPEND (
    {OPENQUERY([Adventure Works DW],'SELECT OrderNumber, model FROM 
    dbo.vAssocSeqLineItems ORDER BY OrderNumber, Model')}
  RELATE OrderNumber to OrderNumber) AS T
~~~~  

  
## <a name="see-also"></a>Vea también  
 [Extensiones de minería de datos &#40; DMX &#41; Referencia de funciones](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Funciones &#40; DMX &#41;](../dmx/functions-dmx.md)   
 [Funciones de predicción generales &#40; DMX &#41;](../dmx/general-prediction-functions-dmx.md)  
  
  
