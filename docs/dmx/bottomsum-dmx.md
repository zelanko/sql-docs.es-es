---
title: BottomSum (DMX) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.component: data-mining
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- BOTTOMSUM
dev_langs:
- DMX
helpviewer_keywords:
- BottomSum function
ms.assetid: fd4b0418-f814-4d83-b2fe-850117e1beb7
caps.latest.revision: 36
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: b7bb5ede61f9ddb95c5f9d76ea09ef2667811bc7
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="bottomsum-dmx"></a>BottomSum (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Devuelve, en orden creciente de rango, las filas inferiores de una tabla cuyo total acumulado sea al menos un valor especificado.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
BottomSum(<table expression>, <rank expression>, <sum>)  
```  
  
## <a name="applies-to"></a>Se aplica a  
 Una expresión que devuelve una tabla, como un \<referencia de columna de la tabla >, o una función que devuelve una tabla.  
  
## <a name="return-type"></a>Tipo devuelto  
 \<expresión de tabla >  
  
## <a name="remarks"></a>Comentarios  
 El **BottomSum** función devuelve las filas inferiores en orden creciente de rango. El rango se basa en el valor evaluado de la \<rank expression > argumento para cada fila, tal que la suma de la \<clasificar expresión > valores sea al menos el total especificado por el \<suma > argumento. **BottomSum** devuelve el número de elementos más pequeño posible que siga cumpliendo el valor de suma especificada.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se crea una consulta de predicción con el modelo de asociación que se compila mediante la [Tutorial básico de minería de datos](http://msdn.microsoft.com/library/6602edb6-d160-43fb-83c8-9df5dddfeb9c).  
  
 Para entender cómo funciona BottomSum, puede resultar útil ejecutar primero una consulta de predicción que devuelve solo la tabla anidada.  
  
```  
SELECT Predict ([Association].[v Assoc Seq Line Items], INCLUDE_STATISTICS, 10)  
FROM   
     [Association]  
NATURAL PREDICTION JOIN  
SELECT (SELECT 'Women''s Mountain Shorts' as [Model]) AS [v Assoc Seq Line Items]) AS t  
```  
  
> [!NOTE]  
>  En este ejemplo, el valor proporcionado como entrada contiene una comilla sencilla y, por consiguiente, se debe anteponer como carácter de escape otra comilla sencilla. Si duda de la sintaxis para insertar un carácter de escape, puede utilizar el generador de consultas de predicción para crear la consulta. Al seleccionar el valor en la lista desplegable, se inserta el carácter de escape necesario. Para obtener más información, consulte [crear una consulta Singleton en el Diseñador de minería de datos](../analysis-services/data-mining/create-a-singleton-query-in-the-data-mining-designer.md).  
  
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
  
 La función BottomSum toma los resultados de esta consulta y devuelve las filas con los valores menores que suman el número especificado.  
  
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
  
 El primer argumento a la función BottomSum es el nombre de una columna de tabla. En este ejemplo, la tabla anidada se devuelve al llamar a la función de predicción y con el argumento INCLUDE_STATISTICS.  
  
 El segundo argumento a la función BottomSum es la columna de la tabla anidada que se utiliza para ordenar los resultados. En este ejemplo, la opción INCLUDE_STATISTICS devuelve las columnas $SUPPORT, $PROBABILTY y $ADJUSTED PROBABILITY. En este ejemplo se utiliza $PROBABILITY para devolver las filas que suman al menos una probabilidad del 50 por ciento.  
  
 El tercer argumento de la función BottomSum especifica la suma de destino, como un tipo double. Para obtener las filas de los productos con el recuento más bajo que suman una probabilidad del 10 por ciento, escriba .1.  
  
 Resultados del ejemplo:  
  
|Modelo|$SUPPORT|$PROBABILITY|$ADJUSTEDPROBABILITY|  
|-----------|--------------|------------------|--------------------------|  
|Road Bottle Cage|1195|0.08…|0.07…|  
|Mountain Bottle Cage|1367|0.09…|0.08…|  
  
 **Tenga en cuenta** en este ejemplo se proporciona únicamente para ilustrar el uso de BottomSum. Dependiendo del tamaño del conjunto de datos, esta consulta podría tardar mucho tiempo en ejecutarse.  
  
## <a name="see-also"></a>Vea también  
 [Funciones &#40;DMX&#41;](../dmx/functions-dmx.md)   
 [Funciones de predicción generales &#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)   
 [BottomPercent &#40;DMX&#41;](../dmx/bottompercent-dmx.md)  
  
  
