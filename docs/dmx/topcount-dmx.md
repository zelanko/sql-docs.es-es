---
title: TopCount (DMX) | Documentos de Microsoft
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: TOPCOUNT
dev_langs: DMX
helpviewer_keywords: TopCount function
ms.assetid: cbe031c9-4ff0-45df-9810-ebaebacf161d
caps.latest.revision: "40"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: b5d0020ea38edda21d5aec96b0b5a469d2f5f963
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/20/2017
---
# <a name="topcount-dmx"></a>TopCount (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Devuelve el número especificado de filas superiores en orden decreciente de rango, como lo especifica una expresión.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
TopCount(<table expression>, <rank expression>, <count>)  
```  
  
## <a name="applies-to"></a>Se aplica a  
 Una expresión que devuelve una tabla, como un \<referencia de columna de la tabla >, o una función que devuelve una tabla.  
  
## <a name="return-type"></a>Tipo devuelto  
 \<expresión de tabla >  
  
## <a name="remarks"></a>Comentarios  
 El valor proporcionado por el \<rank expression > argumento determina el orden decreciente de rango para las filas que se proporcionan en el \<expresión de tabla > argumento y el número de filas de nivel superior que se especifica en el \<recuento > se devuelve el argumento.  
  
 La función TopCount se presentó originalmente para habilitar las predicciones asociativas y por lo general, genera los mismos resultados que una instrucción que incluya **SELECT TOP** y **ORDER BY** cláusulas. Obtendrá un mejor rendimiento para las predicciones asociativas si usa el **predecir (DMX)** función, que admite la especificación de un número de predicciones que devolver.  
  
 Sin embargo, hay situaciones donde todavía tendrá que usar TopCount. Por ejemplo, DMX no admite la **arriba** calificador en una instrucción Sub-select. El [PredictHistogram &#40; DMX &#41;](../dmx/predicthistogram-dmx.md) función tampoco admite la adición de **arriba**.  
  
## <a name="examples"></a>Ejemplos  
 Los siguientes ejemplos son consultas de predicción en el modelo de asociación que se compila mediante la [Tutorial básico de minería de datos](http://msdn.microsoft.com/library/6602edb6-d160-43fb-83c8-9df5dddfeb9c). Las consultas devuelven los mismos resultados, pero el primer ejemplo utiliza TopCount y el segundo ejemplo utiliza la función de predicción.  
  
 Para entender cómo funciona TopCount, puede resultar útil ejecutar primero una consulta de predicción que devuelve solo la tabla anidada.  
  
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
  
 El primer argumento a la función TopCount es el nombre de una columna de tabla. En este ejemplo, la tabla anidada se devuelve al llamar a la función de predicción y con el argumento INCLUDE_STATISTICS.  
  
 El segundo argumento a la función TopCount es la columna de la tabla anidada que se utiliza para ordenar los resultados. En este ejemplo, la opción INCLUDE_STATISTICS devuelve las columnas $SUPPORT, $PROBABILTY y $ADJUSTED PROBABILITY. En este ejemplo se utiliza $SUPPORT para clasificar los resultados.  
  
 El tercer argumento a la función TopCount especifica el número de filas que se va a devolver, como un número entero. Para obtener los tres productos de la parte superior, ordenados por $SUPPORT, se escribe 3.  
  
 Resultados del ejemplo:  
  
|Modelo|$SUPPORT|$PROBABILITY|$ADJUSTEDPROBABILITY|  
|-----------|--------------|------------------|--------------------------|  
|Sport-100|4334|0.29…|0.25…|  
|Water Bottle|2866|0.19…|0.17…|  
|Patch kit|2113|0.14…|0.13…|  
  
 Sin embargo, este tipo de consulta podría afectar al rendimiento en una configuración de producción. Esto se debe a que la consulta devuelve un conjunto de todas las predicciones del algoritmo, ordena estas predicciones y devuelve las tres primeras.  
  
 En el ejemplo siguiente se proporciona una instrucción alternativa que devuelve los mismos resultados pero se ejecuta significativamente más rápido. Este ejemplo reemplaza TopCount con la función de predicción, que acepta un número de predicciones como argumento. Este ejemplo también utiliza el **$SUPPORT** palabra clave que se va a recuperar directamente la columna de tabla anidada.  
  
```  
SELECT Predict ([Association].[v Assoc Seq Line Items], INCLUDE_STATISTICS, 3, $SUPPORT)  
```  
  
 Los resultados contienen las tres primeras predicciones ordenadas por el valor de compatibilidad. Puede reemplazar $SUPPORT con $PROBABILITY o $ADJUSTED_PROBABILITY para devolver predicciones clasificadas por probabilidad o ajustar la probabilidad. Para obtener más información, consulte **predecir (DMX)**.  
  
## <a name="see-also"></a>Vea también  
 [Funciones &#40; DMX &#41;](../dmx/functions-dmx.md)   
 [Funciones de predicción generales &#40; DMX &#41;](../dmx/general-prediction-functions-dmx.md)   
 [BottomCount &#40; DMX &#41;](../dmx/bottomcount-dmx.md)   
 [TopPercent &#40; DMX &#41;](../dmx/toppercent-dmx.md)   
 [TopSum &#40; DMX &#41;](../dmx/topsum-dmx.md)  
  
  
