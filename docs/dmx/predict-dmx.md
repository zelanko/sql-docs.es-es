---
title: Predecir (DMX) | Documentos de Microsoft
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
- PREDICT
dev_langs:
- DMX
helpviewer_keywords:
- Predict function
ms.assetid: f02ff4b3-9bd7-409d-ad14-ead67b3206c4
caps.latest.revision: 40
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: a976011c3b892d826d29038fb0501e57db4c5008
ms.contentlocale: es-es
ms.lasthandoff: 08/02/2017

---
# <a name="predict-dmx"></a>Predict (DMX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

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
  
 o bien  
  
 \<referencia de columna de la tabla >  
  
 El tipo devuelvo depende del tipo de columna a la que se aplica la función.  
  
> [!NOTE]  
>  INCLUSIVE, EXCLUSIVE, INPUT_ONLY e INCLUDE_STATISTICS solo se aplican a una referencia de columna de tabla, mientras que EXCLUDE_NULL e INCLUDE_NULL se aplican exclusivamente a una referencia de columna escalar.  
  
## <a name="remarks"></a>Comentarios  
 Entre las opciones de la función, figuran EXCLUDE_NULL (predeterminada), INCLUDE_NULL, INCLUSIVE, EXCLUSIVE (predeterminada), INPUT_ONLY e INCLUDE_STATISTICS.  
  
> [!NOTE]  
>  Para los modelos de serie temporal, la función de predicción no admite INCLUDE_STATISTICS.  
  
 El parámetro INCLUDE_NODE_ID devuelve la columna $NODEID en el resultado. NODE_ID es el nodo de contenido en el que se ejecuta la predicción para un caso concreto. Este parámetro es opcional cuando se usa Predict en columnas de la tabla.  
  
 El  *n*  parámetro se aplica a columnas de la tabla. Define el número de filas que se devuelve en función del tipo de predicción. Si la columna subyacente es secuencia, llama a la **PredictSequence** función. Si la columna subyacente es una serie temporal, llama a la **PredictTimeSeries** función. Para el caso de los tipos de predicción, llama a la **PredictAssociation** (función).  
  
 El **Predict** función admite el polimorfismo.  
  
 Las siguientes formas abreviadas alternativas son de uso frecuente:  
  
-   [Gender] es una alternativa a **Predict**([Gender], EXCLUDE_NULL).  
  
-   [Products Purchases] es una alternativa para **Predict**([Products Purchases], EXCLUDE_NULL, EXCLUSIVE).  
  
    > [!NOTE]  
    >  El propio tipo devuelto de esta función se considera como una referencia de columna. Esto significa que la **Predict** función puede utilizarse como un argumento en otras funciones que toman una referencia de columna como un argumento (excepto para la **Predict** propia función).  
  
 Si se pasa INCLUDE_STATISTICS a una predicción en una columna con valores de tabla agrega las columnas **$Probability** y **$Support** a la tabla resultante. Estas columnas describen la probabilidad de que exista el registro de tabla anidada asociado.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se utiliza la función de predicción para devolver los cuatro productos en la base de datos de Adventure Works que es más probable que se pueden vender juntos. Dado que la función predice frente a un modelo de minería de datos de reglas de asociación, utiliza automáticamente la **PredictAssociation** funcione como se describió anteriormente.  
  
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
 [Extensiones de minería de datos &#40; DMX &#41; Referencia de funciones](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Funciones &#40; DMX &#41;](../dmx/functions-dmx.md)   
 [Funciones de predicción generales &#40; DMX &#41;](../dmx/general-prediction-functions-dmx.md)  
  
  

