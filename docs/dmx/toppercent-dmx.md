---
description: TopPercent (DMX)
title: Porcentaje (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 1a8cb8bc64f81f05196fd2856c6b9b5c1a583eb4
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88395181"
---
# <a name="toppercent-dmx"></a>TopPercent (DMX)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  La función de **porcentaje** devuelve, en orden decreciente de rango, las filas superiores de una tabla cuyo total acumulado sea al menos un porcentaje especificado.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
TopPercent(<table expression>, <rank expression>, <percent>)  
```  
  
## <a name="applies-to"></a>Se aplica a  
 Expresión que devuelve una tabla, como \<table column reference> , o una función que devuelve una tabla.  
  
## <a name="return-type"></a>Tipo de valor devuelto  
 \<table expression>  
  
## <a name="remarks"></a>Observaciones  
 La función de **porcentaje** devuelve las filas de nivel superior en orden decreciente de rango en función del valor evaluado del \<rank expression> argumento de cada fila, de modo que la suma de los \<rank expression> valores sea al menos el porcentaje especificado por el \<percent> argumento. El valor de **porcentaje** devuelve el menor número posible de elementos mientras se cumple el valor de porcentaje especificado.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se crea una consulta de predicción con el modelo de asociación que se genera mediante el [tutorial básico de minería de datos](https://msdn.microsoft.com/library/6602edb6-d160-43fb-83c8-9df5dddfeb9c).  
  
 Para entender cómo funciona el uso del porcentaje, puede ser útil ejecutar primero una consulta de predicción que solo devuelva la tabla anidada.  
  
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
  
 La función de porcentaje toma los resultados de esta consulta y devuelve las filas con los valores mayores que suman el porcentaje especificado.  
  
```  
SELECT   
TopPercent  
    (  
    Predict ([Association].[v Assoc Seq Line Items],INCLUDE_STATISTICS,10),  
    $SUPPORT,  
    50)  
FROM   
     [Association]  
NATURAL PREDICTION JOIN  
(SELECT (SELECT 'Women''s Mountain Shorts' as [Model]) AS [v Assoc Seq Line Items]) AS t  
```  
  
 El primer argumento de la función de porcentaje es el nombre de una columna de tabla. En este ejemplo, la tabla anidada se devuelve llamando a la función PREDICT y usando el argumento INCLUDE_STATISTICS.  
  
 El segundo argumento de la función de porcentaje es la columna de la tabla anidada que se usa para ordenar los resultados. En este ejemplo, la opción INCLUDE_STATISTICS devuelve las columnas $SUPPORT, $PROBABILTY y $ADJUSTED PROBABILITY. En este ejemplo se utiliza $SUPPORT porque sus valores no son fraccionarios y, por consiguiente, son más fáciles de comprobar.  
  
 El tercer argumento de la función de porcentaje especifica el porcentaje, como un valor de tipo Double. Para obtener las filas de los primeros productos que suman el 50 por ciento de la compatibilidad total, escriba 50.  
  
 Resultados de ejemplo:  
  
|Modelo|$SUPPORT|$PROBABILITY|$ADJUSTEDPROBABILITY|  
|-----------|--------------|------------------|--------------------------|  
|Sport-100|4334|0,29...|0,25...|  
|Water Bottle|2866|0,19...|0,17...|  
|Patch kit|2113|0,14...|0,13...|  
|Mountain Tire Tube|1992|0,133...|0,12...|  
  
 **Nota:** Este ejemplo solo se proporciona para mostrar el uso del porcentaje. Dependiendo del tamaño del conjunto de datos, esta consulta podría tardar mucho tiempo en ejecutarse.  
  
> [!WARNING]  
>  Las funciones MDX de TOPPERCENT y BOTTOMPERCENT pueden generar resultados inesperados cuando los valores utilizados para calcular el porcentaje contienen números negativos. Este comportamiento no afecta a las funciones DMX. Para obtener más información, consulte [BottomPercent &#40;MDX&#41;](../mdx/bottompercent-mdx.md).  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de funciones de extensiones de minería de datos &#40;DMX&#41;](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Funciones &#40;DMX&#41;](../dmx/functions-dmx.md)   
 [Funciones de predicción generales &#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)  
  
  
