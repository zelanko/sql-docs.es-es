---
title: BottomSum (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: cceeac44646b904a7d7e1b45bd3c92d4ad07a0d5
ms.sourcegitcommit: 205de8fa4845c491914902432791bddf11002945
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/23/2020
ms.locfileid: "86969943"
---
# <a name="bottomsum-dmx"></a>BottomSum (DMX)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  Devuelve, en orden creciente de rango, las filas inferiores de una tabla cuyo total acumulado sea al menos un valor especificado.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
BottomSum(<table expression>, <rank expression>, <sum>)  
```  
  
## <a name="applies-to"></a>Se aplica a  
 Expresión que devuelve una tabla, como \<table column reference> , o una función que devuelve una tabla.  
  
## <a name="return-type"></a>Tipo de valor devuelto  
 \<table expression>  
  
## <a name="remarks"></a>Observaciones  
 La función **BottomSum** devuelve las filas inferiores en orden creciente de rango. El rango se basa en el valor evaluado del \<rank expression> argumento de cada fila, de modo que la suma de los \<rank expression> valores sea al menos el total especificado por el \<sum> argumento. **BottomSum** devuelve el menor número posible de elementos mientras se cumple el valor de suma especificado.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se crea una consulta de predicción con el modelo de asociación que se genera mediante el [tutorial básico de minería de datos](https://msdn.microsoft.com/library/6602edb6-d160-43fb-83c8-9df5dddfeb9c).  
  
 Para entender cómo funciona BottomSum, puede ser útil ejecutar primero una consulta de predicción que devuelva solo la tabla anidada.  
  
```  
SELECT Predict ([Association].[v Assoc Seq Line Items], INCLUDE_STATISTICS, 10)  
FROM   
     [Association]  
NATURAL PREDICTION JOIN  
SELECT (SELECT 'Women''s Mountain Shorts' as [Model]) AS [v Assoc Seq Line Items]) AS t  
```  
  
> [!NOTE]  
>  En este ejemplo, el valor proporcionado como entrada contiene una comilla sencilla y, por consiguiente, se debe anteponer como carácter de escape otra comilla sencilla. Si duda de la sintaxis para insertar un carácter de escape, puede utilizar el generador de consultas de predicción para crear la consulta. Al seleccionar el valor en la lista desplegable, se inserta el carácter de escape necesario. Para obtener más información, vea [crear una consulta Singleton en el diseñador de minería de datos](https://docs.microsoft.com/analysis-services/data-mining/create-a-singleton-query-in-the-data-mining-designer).  
  
 Resultados de ejemplo:  
  
|Modelo|$SUPPORT|$PROBABILITY|$ADJUSTEDPROBABILITY|  
|-----------|--------------|------------------|--------------------------|  
|Sport-100|4334|0,291283016|0,252695851|  
|Water Bottle|2866|0,192620472|0,175205052|  
|Patch kit|2113|0,142012232|0,132389356|  
|Mountain Tire Tube|1992|0,133879965|0,125304948|  
|Mountain-200|1755|0,117951475|0,111260823|  
|Road Tire Tube|1588|0,106727603|0,101229538|  
|Cycling Cap|1473|0,098998589|0,094256014|  
|Fender Set - Mountain|1415|0,095100477|0,090718432|  
|Mountain Bottle Cage|1367|0,091874454|0,087780332|  
|Road Bottle Cage|1195|0,080314537|0,077173962|  
  
 La función BottomSum toma los resultados de esta consulta y devuelve las filas con los valores más bajos que suman al recuento especificado.  
  
```  
SELECT   
BottomSum  
    (  
    Predict([Association].[v Assoc Seq Line Items],INCLUDE_STATISTICS,10),  
    $PROBABILITY,  
    .1)  
FROM   
     [Association]  
NATURAL PREDICTION JOIN  
(SELECT (SELECT 'Women''s Mountain Shorts' as [Model]) AS [v Assoc Seq Line Items]) AS t  
```  
  
 El primer argumento de la función BottomSum es el nombre de una columna de la tabla. En este ejemplo, la tabla anidada se devuelve llamando a la función PREDICT y usando el argumento INCLUDE_STATISTICS.  
  
 El segundo argumento de la función BottomSum es la columna de la tabla anidada que se usa para ordenar los resultados. En este ejemplo, la opción INCLUDE_STATISTICS devuelve las columnas $SUPPORT, $PROBABILTY y $ADJUSTED PROBABILITY. En este ejemplo se utiliza $PROBABILITY para devolver las filas que suman al menos una probabilidad del 50 por ciento.  
  
 El tercer argumento de la función BottomSum especifica la suma de destino, como un valor de tipo Double. Para obtener las filas de los productos con el recuento más bajo que suman una probabilidad del 10 por ciento, escriba .1.  
  
 Resultados de ejemplo:  
  
|Modelo|$SUPPORT|$PROBABILITY|$ADJUSTEDPROBABILITY|  
|-----------|--------------|------------------|--------------------------|  
|Road Bottle Cage|1195|0,08...|0,07...|  
|Mountain Bottle Cage|1367|0,09...|0,08...|  
  
 **Nota:** Este ejemplo solo se proporciona para mostrar el uso de BottomSum. Dependiendo del tamaño del conjunto de datos, esta consulta podría tardar mucho tiempo en ejecutarse.  
  
## <a name="see-also"></a>Consulte también  
 [Funciones &#40;DMX&#41;](../dmx/functions-dmx.md)   
 [Funciones de predicción generales &#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)   
 [&#41;BottomPercent &#40;DMX](../dmx/bottompercent-dmx.md)  
  
  
