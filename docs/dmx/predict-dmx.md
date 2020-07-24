---
title: Predicción (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: d323794af598cb621b7fb8f9939cd2ae1c0f2746
ms.sourcegitcommit: 205de8fa4845c491914902432791bddf11002945
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/23/2020
ms.locfileid: "86968455"
---
# <a name="predict-dmx"></a>Predict (DMX)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  La función **PREDICT** devuelve un valor o un conjunto de valores predichos para una columna especificada.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Predict(<scalar column reference>, [option1], [option2], [option n], [INCLUDE_NODE_ID], n)  
Predict(<table column reference>, [option1], [option2], [option n], [INCLUDE_NODE_ID], n)  
```  
  
## <a name="applies-to"></a>Se aplica a  
 Una referencia de columna escalar o una referencia de columna de tabla.  
  
## <a name="return-type"></a>Tipo de valor devuelto  
 \<scalar column reference>  
  
 o  
  
 \<table column reference>  
  
 El tipo devuelvo depende del tipo de columna a la que se aplica la función.  
  
> [!NOTE]  
>  INCLUSIVE, EXCLUSIVE, INPUT_ONLY e INCLUDE_STATISTICS solo se aplican a una referencia de columna de tabla, mientras que EXCLUDE_NULL e INCLUDE_NULL se aplican exclusivamente a una referencia de columna escalar.  
  
## <a name="remarks"></a>Observaciones  
 Entre las opciones de la función, figuran EXCLUDE_NULL (predeterminada), INCLUDE_NULL, INCLUSIVE, EXCLUSIVE (predeterminada), INPUT_ONLY e INCLUDE_STATISTICS.  
  
> [!NOTE]  
>  En los modelos de serie temporal, la función PREDICT no admite INCLUDE_STATISTICS.  
  
 El parámetro INCLUDE_NODE_ID devuelve la columna $NODEID en el resultado. NODE_ID es el nodo de contenido en el que se ejecuta la predicción para un caso concreto. Este parámetro es opcional cuando se usa predecir en columnas de tabla.  
  
 El parámetro *n* se aplica a las columnas de la tabla. Define el número de filas que se devuelve en función del tipo de predicción. Si la columna subyacente es Sequence, llama a la función **PredictSequence** . Si la columna subyacente es serie temporal, llama a la función **PredictTimeSeries** . En el caso de tipos asociativos de predicción, llama a la función **PredictAssociation** .  
  
 La función **PREDICT** admite el polimorfismo.  
  
 Las siguientes formas abreviadas alternativas son de uso frecuente:  
  
-   [Gender] es una alternativa para **predicción**([sexo], EXCLUDE_NULL).  
  
-   [Products Purchases] es una alternativa para **predicción**([Products Purchases], EXCLUDE_NULL, Exclusive).  
  
    > [!NOTE]  
    >  El propio tipo devuelto de esta función se considera como una referencia de columna. Esto significa que la función de **predicción** se puede usar como argumento en otras funciones que toman una referencia de columna como argumento (excepto para la propia función de **predicción** ).  
  
 Al pasar INCLUDE_STATISTICS a una predicción en una columna con valores de tabla, se agregan las columnas **$probability** y **$support** a la tabla resultante. Estas columnas describen la probabilidad de que exista el registro de tabla anidada asociado.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se usa la función PREDICT para devolver los cuatro productos de la base de datos de Adventure Works que es más probable que se vendan juntos. Dado que la función está prediciendo en un modelo de minería de datos de reglas de asociación, utiliza automáticamente la función **PredictAssociation** como se describió anteriormente.  
  
```  
SELECT  
    Predict([Association].[v Assoc Seq Line Items],INCLUDE_STATISTICS,4)  
FROM     [Association]  
```  
  
 Resultados del ejemplo:  
  
 Esta consulta devuelve una sola fila de datos con una columna, `Expression`, pero esa columna contiene la siguiente tabla anidada.  
  
|Modelo|$SUPPORT|$PROBABILITY|$ADJUSTEDPROBABILITY|  
|-----------|--------------|------------------|--------------------------|  
|Sport-100|4334|0.291283016331743|0.252695851192499|  
|Water Bottle|2866|0.192620471805901|0.175205052318795|  
|Patch Kit|2113|0.142012232004839|0.132389356196586|  
|Mountain Tire Tube|1992|0.133879965051415|0.125304947722259|  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de funciones de extensiones de minería de datos &#40;DMX&#41;](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Funciones &#40;DMX&#41;](../dmx/functions-dmx.md)   
 [Funciones de predicción generales &#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)  
  
  
