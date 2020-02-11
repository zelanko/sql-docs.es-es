---
title: Topcount (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: d4b91b06470c9cb22e98ac76ea52494728a7ca11
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68893105"
---
# <a name="topcount-dmx"></a>TopCount (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Devuelve el número especificado de filas superiores en orden decreciente de rango, como lo especifica una expresión.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
TopCount(<table expression>, <rank expression>, <count>)  
```  
  
## <a name="applies-to"></a>Se aplica a  
 Expresión que devuelve una tabla, como una referencia de \<columna de tabla>, o una función que devuelve una tabla.  
  
## <a name="return-type"></a>Tipo de valor devuelto  
 \<> de expresión de tabla  
  
## <a name="remarks"></a>Observaciones  
 El valor proporcionado por la expresión de \<rango> argumento determina el orden decreciente de rango para las filas que se proporcionan en la \<expresión de tabla> argumento, y se devuelve el número de filas de nivel superior que se especifica \<en el argumento Count>.  
  
 La función Topcount se introdujo originalmente para habilitar las predicciones asociativas y, en general, genera los mismos resultados que una instrucción que incluye las cláusulas **Select Top** y **order by** . Obtendrá un mejor rendimiento para las predicciones asociativas si usa la función **PREDICT (DMX)** , que admite la especificación de un número de predicciones para devolver.  
  
 Sin embargo, hay situaciones en las que es posible que siga necesitando usar el número de recuentos. Por ejemplo, DMX no admite el calificador **Top** en una instrucción Sub-SELECT. La función [PredictHistogram &#40;DMX&#41;](../dmx/predicthistogram-dmx.md) tampoco admite la adición de la **parte superior**.  
  
## <a name="examples"></a>Ejemplos  
 Los ejemplos siguientes son consultas de predicción en el modelo de asociación que se genera mediante el [tutorial básico de minería de datos](https://msdn.microsoft.com/library/6602edb6-d160-43fb-83c8-9df5dddfeb9c). Las consultas devuelven los mismos resultados, pero en el primer ejemplo se usa Topcount y en el segundo ejemplo se usa la función PREDICT.  
  
 Para entender cómo funciona el recuento, puede ser útil ejecutar primero una consulta de predicción que devuelva solo la tabla anidada.  
  
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
  
 La función Topcount toma los resultados de esta consulta y devuelve el número especificado de las filas con valores más pequeños.  
  
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
  
 El primer argumento de la función Topcount es el nombre de una columna de la tabla. En este ejemplo, la tabla anidada se devuelve llamando a la función PREDICT y usando el argumento INCLUDE_STATISTICS.  
  
 El segundo argumento de la función Topcount es la columna de la tabla anidada que se utiliza para ordenar los resultados. En este ejemplo, la opción INCLUDE_STATISTICS devuelve las columnas $SUPPORT, $PROBABILTY y $ADJUSTED PROBABILITY. En este ejemplo se utiliza $SUPPORT para clasificar los resultados.  
  
 El tercer argumento de la función Topcount especifica el número de filas que se van a devolver, como un entero. Para obtener los tres productos de la parte superior, ordenados por $SUPPORT, se escribe 3.  
  
 Resultados de ejemplo:  
  
|Modelo|$SUPPORT|$PROBABILITY|$ADJUSTEDPROBABILITY|  
|-----------|--------------|------------------|--------------------------|  
|Sport-100|4334|0,29...|0,25...|  
|Water Bottle|2866|0,19...|0,17...|  
|Patch kit|2113|0,14...|0,13...|  
  
 Sin embargo, este tipo de consulta podría afectar al rendimiento en una configuración de producción. Esto se debe a que la consulta devuelve un conjunto de todas las predicciones del algoritmo, ordena estas predicciones y devuelve las tres primeras.  
  
 En el ejemplo siguiente se proporciona una instrucción alternativa que devuelve los mismos resultados pero se ejecuta significativamente más rápido. En este ejemplo se reemplaza el valor de Topcount por la función PREDICT, que acepta un número de predicciones como argumento. En este ejemplo también se usa la palabra clave **$support** para recuperar directamente la columna de la tabla anidada.  
  
```  
SELECT Predict ([Association].[v Assoc Seq Line Items], INCLUDE_STATISTICS, 3, $SUPPORT)  
```  
  
 Los resultados contienen las tres primeras predicciones ordenadas por el valor de compatibilidad. Puede reemplazar $SUPPORT con $PROBABILITY o $ADJUSTED_PROBABILITY para devolver predicciones clasificadas por probabilidad o ajustar la probabilidad. Para obtener más información, vea **PREDICT (DMX)**.  
  
## <a name="see-also"></a>Consulte también  
 [Funciones &#40;DMX&#41;](../dmx/functions-dmx.md)   
 [Funciones de predicción generales &#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)   
 [&#41;BottomCount &#40;DMX](../dmx/bottomcount-dmx.md)   
 [&#40;DMX&#41;](../dmx/toppercent-dmx.md)   
 [&#40;DMX&#41;](../dmx/topsum-dmx.md)  
  
  
