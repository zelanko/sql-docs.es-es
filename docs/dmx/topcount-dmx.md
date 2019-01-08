---
title: TopCount (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 0ec801da96735f15b6320c3f0372855c1ff3c2c8
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/28/2018
ms.locfileid: "52502831"
---
# <a name="topcount-dmx"></a>TopCount (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Devuelve el número especificado de filas superiores en orden decreciente de rango, como lo especifica una expresión.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
TopCount(<table expression>, <rank expression>, <count>)  
```  
  
## <a name="applies-to"></a>Se aplica a  
 Una expresión que devuelve una tabla, como un \<referencia de columna de tabla >, o una función que devuelve una tabla.  
  
## <a name="return-type"></a>Tipo devuelto  
 \<expresión de tabla >  
  
## <a name="remarks"></a>Comentarios  
 El valor proporcionado por el \<rank expression > argumento determina el orden decreciente de rango para las filas que se proporcionan en el \<expresión de tabla > argumento y el número de filas de nivel superior que se especifica en el \<recuento > se devuelve el argumento.  
  
 La función TopCount se presentó originalmente para habilitar las predicciones asociativas y en general, genera los mismos resultados que una instrucción que incluye **SELECT TOP** y **ORDER BY** cláusulas. Obtendrá un mejor rendimiento para las predicciones asociativas si usa el **predecir (DMX)** función, que admite la especificación de un número de predicciones que devolver.  
  
 Sin embargo, existen situaciones donde es posible que todavía deberá usar TopCount. Por ejemplo, DMX no admite la **superior** calificador en una instrucción Sub-select. El [PredictHistogram &#40;DMX&#41; ](../dmx/predicthistogram-dmx.md) función también no admite la adición de **superior**.  
  
## <a name="examples"></a>Ejemplos  
 Los siguientes ejemplos son consultas de predicción en el modelo de asociación que se crea mediante el uso de la [Basic Data Mining Tutorial](https://msdn.microsoft.com/library/6602edb6-d160-43fb-83c8-9df5dddfeb9c). Las consultas devuelven los mismos resultados, pero el primer ejemplo utiliza TopCount y el segundo ejemplo usa la función Predict.  
  
 Para entender cómo funciona TopCount, puede ser útil ejecutar primero una consulta de predicción que devuelve solo la tabla anidada.  
  
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
  
 La función TopCount toma los resultados de esta consulta y devuelve el número especificado de las filas con los valores menores.  
  
```  
SELECT   
TopCount  
    (  
    Predict ([Association].[v Assoc Seq Line Items],INCLUDE_STATISTICS,10),  
    $SUPPORT,  
    3)  
FROM   
     [Association]  
NATURAL PREDICTION JOIN  
(SELECT (SELECT 'Women''s Mountain Shorts' as [Model]) AS [v Assoc Seq Line Items]) AS t  
```  
  
 El primer argumento a la función TopCount es el nombre de una columna de tabla. En este ejemplo, la tabla anidada se devuelve al llamar a la función Predict y con el argumento INCLUDE_STATISTICS.  
  
 El segundo argumento a la función TopCount es la columna en la tabla anidada que se utiliza para ordenar los resultados. En este ejemplo, la opción INCLUDE_STATISTICS devuelve las columnas $SUPPORT, $PROBABILTY y $ADJUSTED PROBABILITY. En este ejemplo se utiliza $SUPPORT para clasificar los resultados.  
  
 El tercer argumento a la función TopCount especifica el número de filas que se devolverán como un entero. Para obtener los tres productos de la parte superior, ordenados por $SUPPORT, se escribe 3.  
  
 Resultados del ejemplo:  
  
|Modelo|$SUPPORT|$PROBABILITY|$ADJUSTEDPROBABILITY|  
|-----------|--------------|------------------|--------------------------|  
|Sport-100|4334|0.29...|0,25...|  
|Water Bottle|2866|0.19...|0,17...|  
|Patch kit|2113|0,14...|0.13...|  
  
 Sin embargo, este tipo de consulta podría afectar al rendimiento en una configuración de producción. Esto se debe a que la consulta devuelve un conjunto de todas las predicciones del algoritmo, ordena estas predicciones y devuelve las tres primeras.  
  
 En el ejemplo siguiente se proporciona una instrucción alternativa que devuelve los mismos resultados pero se ejecuta significativamente más rápido. Este ejemplo reemplaza TopCount con la función de predicción, que acepta un número de predicciones como argumento. En este ejemplo también usa el **$SUPPORT** palabra clave para recuperar directamente la columna de tabla anidada.  
  
```  
SELECT Predict ([Association].[v Assoc Seq Line Items], INCLUDE_STATISTICS, 3, $SUPPORT)  
```  
  
 Los resultados contienen las tres primeras predicciones ordenadas por el valor de compatibilidad. Puede reemplazar $SUPPORT con $PROBABILITY o $ADJUSTED_PROBABILITY para devolver predicciones clasificadas por probabilidad o ajustar la probabilidad. Para obtener más información, consulte **predecir (DMX)**.  
  
## <a name="see-also"></a>Vea también  
 [Funciones &#40;DMX&#41;](../dmx/functions-dmx.md)   
 [Funciones de predicción generales &#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)   
 [BottomCount &#40;DMX&#41;](../dmx/bottomcount-dmx.md)   
 [TopPercent &#40;DMX&#41;](../dmx/toppercent-dmx.md)   
 [TopSum &#40;DMX&#41;](../dmx/topsum-dmx.md)  
  
  
