---
title: PredictAssociation (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: ea0a9915e062d7b6f15b63e18976e88cc339202d
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "76939506"
---
# <a name="predictassociation-dmx"></a>PredictAssociation (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Predice los miembros de asociaciones.  
  
Por ejemplo, puede usar la función PredictAssociation para obtener el conjunto de recomendaciones dado el estado actual de la cesta de la compra de un cliente. 
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
PredictAssociation(<table column reference>, option1, option2, n ...)  
```  
  
## <a name="applies-to"></a>Se aplica a  
 Algoritmos que contienen tablas anidadas de predicción, incluidos algoritmos de asociación y de clasificación. Los algoritmos de clasificación que admiten tablas anidadas incluyen los algoritmos de [!INCLUDE[msCoName](../includes/msconame-md.md)] árboles de decisión, [!INCLUDE[msCoName](../includes/msconame-md.md)] Bayes Naive y [!INCLUDE[msCoName](../includes/msconame-md.md)] de red neuronal.  
  
## <a name="return-type"></a>Tipo de valor devuelto  
 \<> de expresión de tabla  
  
## <a name="remarks"></a>Observaciones  
 Entre las opciones de la función **PredictAssociation** se incluyen EXCLUDE_NULL, INCLUDE_NULL, inclusive, Exclusive (valor predeterminado), INPUT_ONLY, INCLUDE_STATISTICS y INCLUDE_NODE_ID.  
  
> [!NOTE]  
>  INCLUSIVE, EXCLUSIVE, INPUT_ONLY e INCLUDE_STATISTICS solo se aplican a una referencia de columna de tabla, mientras que EXCLUDE_NULL e INCLUDE_NULL se aplican exclusivamente a una referencia de columna escalar.  
  
 INCLUDE_STATISTICS solo devuelve **$probability** y **$AdjustedProbability**.  
  
 Si se especifica el parámetro numérico *n* , la función **PredictAssociation** devuelve los n valores más probables en función de la probabilidad:  
  
```  
PredictAssociation(colref, [$AdjustedProbability], n)  
```  
  
 Si incluye **$AdjustedProbability**, la instrucción devuelve los *n* valores principales basados en el **$AdjustedProbability**.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se usa la función **PredictAssociation** para devolver los cuatro productos de la base de datos de Adventure Works que es más probable que se vendan juntos.  
  
```  
SELECT  
  PredictAssociation([Association].[v Assoc Seq Line Items],4)  
From  
  [Association]  
```  
En el ejemplo siguiente se muestra cómo se puede usar una tabla anidada como entrada para la función de predicción mediante la cláusula SHAPE. La consulta de forma crea un conjunto de filas con customerId como una columna y una tabla anidada como una segunda columna, que contiene la lista de productos que un cliente ya ha puesto. 

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

  
## <a name="see-also"></a>Consulte también  
 [Referencia de funciones de extensiones de minería de datos &#40;DMX&#41;](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Funciones &#40;DMX&#41;](../dmx/functions-dmx.md)   
 [Funciones de predicción generales &#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)  
  
  
