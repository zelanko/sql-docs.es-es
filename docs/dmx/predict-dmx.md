---
title: Predecir (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: eb939c45d298117fa81b05d6188aa3a4c5cd7c4b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68008161"
---
# <a name="predict-dmx"></a>Predict (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  El **Predict** función devuelve un valor de predicción, o un conjunto de valores para una columna especificada.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Predict(<scalar column reference>, [option1], [option2], [option n], [INCLUDE_NODE_ID], n)  
Predict(<table column reference>, [option1], [option2], [option n], [INCLUDE_NODE_ID], n)  
```  
  
## <a name="applies-to"></a>Se aplica a  
 Una referencia de columna escalar o una referencia de columna de tabla.  
  
## <a name="return-type"></a>Tipo devuelto  
 \<referencia de columna escalar >  
  
 o Administrador de configuración de  
  
 \<referencia de columna de tabla >  
  
 El tipo devuelvo depende del tipo de columna a la que se aplica la función.  
  
> [!NOTE]  
>  INCLUSIVE, EXCLUSIVE, INPUT_ONLY e INCLUDE_STATISTICS solo se aplican a una referencia de columna de tabla, mientras que EXCLUDE_NULL e INCLUDE_NULL se aplican exclusivamente a una referencia de columna escalar.  
  
## <a name="remarks"></a>Comentarios  
 Entre las opciones de la función, figuran EXCLUDE_NULL (predeterminada), INCLUDE_NULL, INCLUSIVE, EXCLUSIVE (predeterminada), INPUT_ONLY e INCLUDE_STATISTICS.  
  
> [!NOTE]  
>  Para los modelos de serie temporal, la función Predict no admite INCLUDE_STATISTICS.  
  
 El parámetro INCLUDE_NODE_ID devuelve la columna $NODEID en el resultado. NODE_ID es el nodo de contenido en el que se ejecuta la predicción para un caso concreto. Este parámetro es opcional cuando el uso de Predict en columnas de tabla.  
  
 El *n* parámetro se aplica a columnas de la tabla. Define el número de filas que se devuelve en función del tipo de predicción. Si la columna subyacente es la secuencia, llama a la **PredictSequence** función. Si la columna subyacente es una serie temporal, llama a la **PredictTimeSeries** función. Caso de tipos de predicción, llama a la **PredictAssociation** función.  
  
 El **Predict** función admite el polimorfismo.  
  
 Las siguientes formas abreviadas alternativas son de uso frecuente:  
  
-   [Gender] es una alternativa para **Predict**([Gender], EXCLUDE_NULL).  
  
-   [Products Purchases] es una alternativa para **Predict**([Products Purchases], EXCLUDE_NULL, EXCLUSIVE).  
  
    > [!NOTE]  
    >  El propio tipo devuelto de esta función se considera como una referencia de columna. Esto significa que el **Predict** función se puede usar como argumento en otras funciones que toman una referencia de columna como un argumento (excepto para el **Predict** función en Sí).  
  
 Si se pasa INCLUDE_STATISTICS a una predicción en una columna con valores de tabla agrega las columnas **$Probability** y **$Support** a la tabla resultante. Estas columnas describen la probabilidad de que exista el registro de tabla anidada asociado.  
  
## <a name="examples"></a>Ejemplos  
 El ejemplo siguiente usa la función Predict para devolver los cuatro productos en la base de datos de Adventure Works que es más probable que se pueden vender juntos. Dado que la función predice frente a un modelo de minería de datos de reglas de asociación, usa automáticamente el **PredictAssociation** funcione como se describió anteriormente.  
  
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
  
## <a name="see-also"></a>Vea también  
 [Extensiones de minería de datos &#40;DMX&#41; referencia de funciones](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Funciones &#40;DMX&#41;](../dmx/functions-dmx.md)   
 [Funciones de predicción generales &#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)  
  
  
