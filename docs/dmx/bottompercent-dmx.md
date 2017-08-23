---
title: BottomPercent (DMX) | Documentos de Microsoft
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
- BOTTOMPERCENT
dev_langs:
- DMX
helpviewer_keywords:
- BottomPercent function
ms.assetid: 984eb18a-c55c-49f3-81fa-918dfc983174
caps.latest.revision: 41
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: cdc60cbc61d0c84953f2e80a5896dbd8465bdb8a
ms.contentlocale: es-es
ms.lasthandoff: 08/02/2017

---
# <a name="bottompercent-dmx"></a>BottomPercent (DMX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve, en orden creciente de rango, las filas inferiores de una tabla cuyo total acumulado sea al menos un porcentaje especificado.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
BottomPercent(<table expression>, <rank expression>, <percent>)  
```  
  
## <a name="arguments"></a>Argumentos  
 *\<Expresión de tabla >*  
 Nombre de una columna de tabla anidada o expresión de valores de tabla.  
  
 *\<Rank expression >*  
 Columna de la tabla anidada o expresión que se evalúa como una columna.  
  
 *\<% >*  
 Valor doble que indica el porcentaje de destino total.  
  
## <a name="result-type"></a>Tipo de resultado  
 Tabla.  
  
## <a name="remarks"></a>Comentarios  
 El **BottomPercent** función devuelve las filas inferiores en orden creciente de rango. El rango se basa en el valor evaluado de la \<rank expression > argumento para cada fila, tal que la suma de la \<clasificar expresión > valores sea al menos el porcentaje especificado por el \<por ciento > argumento. **BottomPercent** devuelve el número de elementos más pequeño posible que siga cumpliendo el valor de porcentaje especificado.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se crea una consulta de predicción en el modelo de asociación que creó en el [Tutorial básico de minería de datos](http://msdn.microsoft.com/library/6602edb6-d160-43fb-83c8-9df5dddfeb9c).  
  
 Para entender cómo funciona BottomPercent, puede resultar útil ejecutar primero una consulta de predicción que devuelve solo la tabla anidada.  
  
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
  
 La función BottomPercent toma los resultados de esta consulta y devuelve las filas con los valores menores que suman el porcentaje especificado.  
  
```  
SELECT   
BottomPercent  
    (  
    Predict ([Association].[v Assoc Seq Line Items],INCLUDE_STATISTICS,10),  
    $SUPPORT,  
    50)  
FROM   
     [Association]  
NATURAL PREDICTION JOIN  
(SELECT (SELECT 'Women''s Mountain Shorts' as [Model]) AS [v Assoc Seq Line Items]) AS t  
```  
  
 El primer argumento a la función BottomPercent es el nombre de una columna de tabla. En este ejemplo, la tabla anidada se devuelve al llamar a la función de predicción y con el argumento INCLUDE_STATISTICS.  
  
 El segundo argumento a la función BottomPercent es la columna de la tabla anidada que se utiliza para ordenar los resultados. En este ejemplo, la opción INCLUDE_STATISTICS devuelve las columnas $SUPPORT, $PROBABILTY y $ADJUSTED PROBABILITY. En este ejemplo se utiliza $SUPPORT porque sus valores no son fraccionarios y, por consiguiente, son más fáciles de comprobar.  
  
 El tercer argumento a la función BottomPercent especifica el porcentaje, como un tipo double. Para obtener las filas que representan la mitad inferior del porcentaje de compatibilidad, escriba 50.  
  
 Resultados del ejemplo:  
  
|Modelo|$SUPPORT|$PROBABILITY|$ADJUSTEDPROBABILITY|  
|-----------|--------------|------------------|--------------------------|  
|Road Bottle Cage|1195|0.080314537|0.077173962|  
|Mountain Bottle Cage|1367|0.091874454|0.087780332|  
|Fender Set - Mountain|1415|0.095100477|0.090718432|  
|Cycling Cap|1473|0.098998589|0.094256014|  
|Road Tire Tube|1588|0.106727603|0.101229538|  
|Mountain-200|1755|0.117951475|0.111260823|  
|Mountain Tire Tube|1992|0.133879965|0.125304948|  
  
 **Tenga en cuenta** en este ejemplo se proporciona únicamente para ilustrar el uso de BottomPercent. Dependiendo del tamaño del conjunto de datos, esta consulta podría tardar mucho tiempo en ejecutarse.  
  
> [!WARNING]  
>  Las funciones MDX de TOPPERCENT y BOTTOMPERCENT pueden generar resultados inesperados cuando los valores utilizados para calcular el porcentaje contienen números negativos. Este comportamiento no afecta a las funciones DMX. Para obtener más información, vea [BottomPercent &#40; MDX &#41; ](../mdx/bottompercent-mdx.md).  
  
## <a name="see-also"></a>Vea también  
 [Extensiones de minería de datos &#40; DMX &#41; Referencia de funciones](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Funciones &#40; DMX &#41;](../dmx/functions-dmx.md)  
  
  

