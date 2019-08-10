---
title: Porcentaje (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: acd35dc68c4f42231aa6f71d6cc2a150ff027811
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/09/2019
ms.locfileid: "68893063"
---
# <a name="toppercent-dmx"></a>TopPercent (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  La función de **porcentaje** devuelve, en orden decreciente de rango, las filas superiores de una tabla cuyo total acumulado sea al menos un porcentaje especificado.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
TopPercent(<table expression>, <rank expression>, <percent>)  
```  
  
## <a name="applies-to"></a>Se aplica a  
 Expresión que devuelve una tabla, como una referencia de \<columna de tabla >, o una función que devuelve una tabla.  
  
## <a name="return-type"></a>Tipo devuelto  
 \<> de expresión de tabla  
  
## <a name="remarks"></a>Comentarios  
 La función de **porcentaje** devuelve las filas de nivel superior en orden decreciente de rango basándose en el valor evaluado \<de la expresión de rango > argumento de cada fila, de modo que \<la suma de la expresión de rango > valores sea al menos el porcentaje especificado por el \<argumento Percent >. El valor de **porcentaje** devuelve el menor número posible de elementos mientras se cumple el valor de porcentaje especificado.  
  
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
  
 Resultados del ejemplo:  
  
|Modelo|$SUPPORT|$PROBABILITY|$ADJUSTEDPROBABILITY|  
|-----------|--------------|------------------|--------------------------|  
|Sport-100|4334|0.291283016|0.252695851|  
|Water Bottle|2866|0.192620472|0.175205052|  
|Patch kit|2113|0.142012232|0.132389356|  
|Mountain Tire Tube|1992|0.133879965|0.125304948|  
|Mountain-200|1755|0.117951475|0.111260823|  
|Road Tire Tube|1588|0.106727603|0.101229538|  
|Cycling Cap|1473|0.098998589|0.094256014|  
|Fender Set - Mountain|1415|0.095100477|0.090718432|  
|Mountain Bottle Cage|1367|0.091874454|0.087780332|  
|Road Bottle Cage|1195|0.080314537|0.077173962|  
  
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
  
 El primer argumento de la función de porcentaje es el nombre de una columna de tabla. En este ejemplo, la tabla anidada se devuelve mediante una llamada a la función PREDICT y el uso del argumento INCLUDE_STATISTICS.  
  
 El segundo argumento de la función de porcentaje es la columna de la tabla anidada que se usa para ordenar los resultados. En este ejemplo, la opción INCLUDE_STATISTICS devuelve las columnas $SUPPORT, $PROBABILTY y $ADJUSTED PROBABILITY. En este ejemplo se utiliza $SUPPORT porque sus valores no son fraccionarios y, por consiguiente, son más fáciles de comprobar.  
  
 El tercer argumento de la función de porcentaje especifica el porcentaje, como un valor de tipo Double. Para obtener las filas de los primeros productos que suman el 50 por ciento de la compatibilidad total, escriba 50.  
  
 Resultados del ejemplo:  
  
|Modelo|$SUPPORT|$PROBABILITY|$ADJUSTEDPROBABILITY|  
|-----------|--------------|------------------|--------------------------|  
|Sport-100|4334|0,29...|0,25...|  
|Water Bottle|2866|0,19...|0,17...|  
|Patch kit|2113|0,14...|0,13...|  
|Mountain Tire Tube|1992|0,133...|0,12...|  
  
 **Nota:** Este ejemplo solo se proporciona para mostrar el uso del porcentaje. Dependiendo del tamaño del conjunto de datos, esta consulta podría tardar mucho tiempo en ejecutarse.  
  
> [!WARNING]  
>  Las funciones MDX de TOPPERCENT y BOTTOMPERCENT pueden generar resultados inesperados cuando los valores utilizados para calcular el porcentaje contienen números negativos. Este comportamiento no afecta a las funciones DMX. Para obtener más información, [consulte &#40;BottomPercent&#41;MDX](../mdx/bottompercent-mdx.md).  
  
## <a name="see-also"></a>Vea también  
 [Referencia de funciones &#40;DMX&#41; de extensiones de minería de datos](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [DMX &#40;de funciones&#41;](../dmx/functions-dmx.md)   
 [Funciones &#40;de predicción generales DMX&#41;](../dmx/general-prediction-functions-dmx.md)  
  
  
