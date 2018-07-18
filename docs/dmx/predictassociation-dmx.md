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
manager: kfile
ms.openlocfilehash: 7a23407b546bcde2dd1fde81654da4fe861e0719
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2018
ms.locfileid: "37989547"
---
# <a name="predictassociation-dmx"></a>PredictAssociation (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Predice los miembros de asociaciones.  
  
Por ejemplo, puede usar la función PredictAssociation para obtener el conjunto de recomendaciones, dado el estado actual de la cesta de compra de un cliente. 
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
PredictAssociation(<table column reference>, option1, option2, n ...)  
```  
  
## <a name="applies-to"></a>Se aplica a  
 Algoritmos que contienen tablas anidadas predecibles, incluida la asociación y algunos algoritmos de clasificación. Los algoritmos de clasificación que admiten tablas anidadas se incluyen la [!INCLUDE[msCoName](../includes/msconame-md.md)] árboles de decisión, [!INCLUDE[msCoName](../includes/msconame-md.md)] Bayes Naive, y [!INCLUDE[msCoName](../includes/msconame-md.md)] algoritmos de red neuronal.  
  
## <a name="return-type"></a>Tipo devuelto  
 \<expresión de tabla >  
  
## <a name="remarks"></a>Notas  
 Las opciones para la **PredictAssociation** función incluir EXCLUDE_NULL, INCLUDE_NULL, INCLUSIVE, EXCLUSIVE (predeterminada), INPUT_ONLY, INCLUDE_STATISTICS e INCLUDE_NODE_ID.  
  
> [!NOTE]  
>  INCLUSIVE, EXCLUSIVE, INPUT_ONLY e INCLUDE_STATISTICS solo se aplican a una referencia de columna de tabla, mientras que EXCLUDE_NULL e INCLUDE_NULL se aplican exclusivamente a una referencia de columna escalar.  
  
 INCLUDE_STATISTICS solo devuelve **$Probability** y **$AdjustedProbability**.  
  
 Si el parámetro numérico *n* se especifica, el **PredictAssociation** función devuelve los valores más probables n superiores en función de la probabilidad:  
  
```  
PredictAssociation(colref, [$AdjustedProbability], n)  
```  
  
 Si incluye **$AdjustedProbability**, la instrucción devuelve la parte superior *n* valores según el **$AdjustedProbability**.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se usa el **PredictAssociation** función para devolver los cuatro productos en el de Adventure Works de bases de datos que es más probable que pueden vender juntos.  
  
```  
SELECT  
  PredictAssociation([Association].[v Assoc Seq Line Items],4)  
From  
  [Association]  
```  
El ejemplo siguiente muestra cómo usar una tabla anidada como entrada para la función de predicción mediante la cláusula SHAPE. La consulta SHAPE crea un conjunto de filas con customerId como una columna y una tabla anidada como una segunda columna, que contiene la lista de productos que ya ha aportado un cliente. 

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
 [Extensiones de minería de datos &#40;DMX&#41; referencia de funciones](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Funciones &#40;DMX&#41;](../dmx/functions-dmx.md)   
 [Funciones de predicción generales &#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)  
  
  
