---
title: Ejemplos de consultas de modelo de asociación | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- itemsets [Analysis Services]
- association algorithms [Analysis Services]
- rules [Data Mining]
- association rules
- content queries [DMX]
ms.assetid: 68b39f5c-c439-44ac-8046-6f2d36649059
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ad20cca3b87a3d3b94bef48dcdf94c55cf30a282
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48117387"
---
# <a name="association-model-query-examples"></a>Ejemplos de consultas del modelo de asociación
  Cuando se crea una consulta en un modelo de minería de datos, puede tratarse de una consulta de contenido, que proporciona detalles sobre las reglas y los conjuntos de elementos detectados durante el análisis, o una consulta de predicción, que utiliza las asociaciones detectadas en los datos para realizar predicciones. En un modelo de asociación, las predicciones se basan normalmente en reglas y se pueden utilizar para realizar recomendaciones, mientras que las consultas de contenido normalmente exploran la relación entre los conjuntos de elementos. También se puede recuperar metadatos sobre el modelo.  
  
 En esta sección se explica cómo crear estos tipos de consultas en modelos basados en el algoritmo de reglas de asociación de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **Consultas de contenido**  
  
 [Obtener datos de metadatos del modelo utilizando DMX](#bkmk_Query1)  
  
 [Obtener metadatos del conjunto de filas de esquema](#bkmk_Query2)  
  
 [Recuperar los parámetros originales del modelo](#bkmk_Query3)  
  
 [Recuperar una lista de conjuntos de elementos y de productos](#bkmk_Query4)  
  
 [Devolver los 10 primeros conjuntos de elementos](#bkmk_Query5)  
  
 **Consultas de predicción**  
  
 [Predecir elementos asociados](#bkmk_Query6)  
  
 [Determinar la confianza por los conjuntos de elementos relacionados](#bkmk_Query7)  
  
##  <a name="bkmk_top2"></a> Buscar información sobre el modelo  
 Todos los modelos de minería de datos exponen el contenido aprendido por el algoritmo de acuerdo con un esquema normalizado, denominado conjunto de filas de esquema del modelo de minería de datos. Puede crear consultas en el conjunto de filas de esquema del modelo de minería de datos utilizando instrucciones de Extensiones de minería de datos (DMX) o los procedimientos almacenados de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . En [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], también se pueden consultar directamente los conjuntos de filas de esquema como tablas del sistema, utilizando una sintaxis parecida a SQL.  
  
###  <a name="bkmk_Query1"></a> Consulta de ejemplo 1: obtener metadatos del modelo usando DMX  
 La consulta siguiente devuelve metadatos básicos sobre el modelo de asociación, `Association`, como el nombre del modelo, la base de datos en la que se encuentra almacenado y el número de nodos secundarios existentes en él. Esta consulta usa una consulta de contenido DMX para recuperar los metadatos del nodo primario del modelo:  
  
```  
SELECT MODEL_CATALOG, MODEL_NAME, NODE_CAPTION,   
NODE_SUPPORT, [CHILDREN_CARDINALITY], NODE_DESCRIPTION  
FROM Association.CONTENT  
WHERE NODE_TYPE = 1  
```  
  
> [!NOTE]  
>  El nombre de la columna CHILDREN_CARDINALITY debe ir entre corchetes para distinguirlo de la palabra clave reservada de MDX del mismo nombre.  
  
 Resultados del ejemplo:  
  
|||  
|-|-|  
|MODEL_CATALOG|Association Test|  
|MODEL_NAME|Asociación|  
|NODE_CAPTION|Association Rules Model|  
|NODE_SUPPORT|14879|  
|CHILDREN_CARDINALITY|942|  
|NODE_DESCRIPTION|Association Rules Model; ITEMSET_COUNT=679; RULE_COUNT=263; MIN_SUPPORT=14; MAX_SUPPORT=4334; MIN_ITEMSET_SIZE=0; MAX_ITEMSET_SIZE=3; MIN_PROBABILITY=0.400390625; MAX_PROBABILITY=1; MIN_LIFT=0.14309369632511; MAX_LIFT=1.95758227647523|  
  
 Para consultar una definición de lo que significan estas columnas en un modelo de asociación, vea [Mining Model Content for Association Models &#40;Analysis Services - Data Mining&#41;](mining-model-content-for-association-models-analysis-services-data-mining.md).  
  
 [Volver al principio](#bkmk_top2)  
  
###  <a name="bkmk_Query2"></a> Consulta de ejemplo 2: obtener metadatos adicionales del conjunto de filas de esquema  
 Mediante una consulta al conjunto de filas de esquema de minería de datos, puede obtener la misma información que a través de una consulta de contenido DMX. Sin embargo, el conjunto de filas de esquema proporciona algunas columnas adicionales, como la fecha en que se procesó el modelo por última vez, la estructura de minería de datos y el nombre de la columna usada como atributo de predicción.  
  
```  
SELECT MODEL_CATALOG, MODEL_NAME, SERVICE_NAME, PREDICTION_ENTITY,   
MINING_STRUCTURE, LAST_PROCESSED  
FROM $system.DMSCHEMA_MINING_MODELS  
WHERE MODEL_NAME = 'Association'  
```  
  
 Resultados del ejemplo:  
  
|||  
|-|-|  
|MODEL_CATALOG|Adventure Works DW Multidimensional 2012|  
|MODEL_NAME|Asociación|  
|SERVICE_NAME|Association Rules Model|  
|PREDICTION_ENTITY|v Assoc Seq Line Items|  
|MINING_STRUCTURE|Asociación|  
|LAST_PROCESSED|29/9/2007 10:21:24 PM|  
  
 [Volver al principio](#bkmk_top2)  
  
###  <a name="bkmk_Query3"></a> Consulta de ejemplo 3: recuperar los parámetros originales para el modelo  
 La consulta siguiente devuelve una única columna con detalles sobre la configuración de parámetros utilizada cuando se creó el modelo.  
  
```  
SELECT MINING_PARAMETERS   
from $system.DMSCHEMA_MINING_MODELS  
WHERE MODEL_NAME = 'Association'  
```  
  
 Resultados del ejemplo:  
  
 MAXIMUM_ITEMSET_COUNT=200000,MAXIMUM_ITEMSET_SIZE=3,MAXIMUM_SUPPORT=1,MINIMUM_SUPPORT=9.40923449156529E-04,MINIMUM_IMPORTANCE=-999999999,MINIMUM_ITEMSET_SIZE=0,MINIMUM_PROBABILITY=0.4  
  
 [Volver al principio](#bkmk_top2)  
  
## <a name="finding-information-about-rules-and-itemsets"></a>Buscar información sobre las reglas y los conjuntos de elementos  
 Los usos más comunes de un modelo de asociación son dos: detectar información sobre conjuntos de elementos frecuentes y extraer detalles sobre reglas y conjuntos de elementos concretos. Por ejemplo, puede que desee extraer una lista de reglas puntuadas como especialmente interesantes, o crear una lista de los conjuntos de elementos más comunes. Esta información se recupera utilizando una consulta de contenido DMX. También se puede examinar esta información utilizando el **Visor de asociación de Microsoft**.  
  
###  <a name="bkmk_Query4"></a> Consulta de ejemplo 4: recuperar una lista de conjuntos de elementos y productos  
 La consulta siguiente recupera todos los conjuntos de elementos junto con una tabla anidada que contiene la lista de productos incluidos en cada conjunto de elementos. La columna NODE_NAME contiene el identificador único del conjunto de elementos existente en el modelo, mientras que NODE_CAPTION proporciona una descripción de los elementos. En este ejemplo, se ha quitado la información de estructura jerárquica de la tabla anidada para que el conjunto de elementos que contenga dos productos genere dos filas en los resultados. Se puede omitir la palabra clave FLATTENED si el cliente admite datos jerárquicos.  
  
```  
SELECT FLATTENED NODE_NAME, NODE_CAPTION,  
NODE_PROBABILITY, NODE_SUPPORT,  
(SELECT ATTRIBUTE_NAME FROM NODE_DISTRIBUTION) as PurchasedProducts  
FROM Association.CONTENT  
WHERE NODE_TYPE = 7  
```  
  
 Resultados del ejemplo:  
  
|||  
|-|-|  
|NODE_NAME|37|  
|NODE_CAPTION|Sport-100 = Existing|  
|NODE_PROBABILITY|0.291283016331743|  
|NODE_SUPPORT|4334|  
|PURCHASEDPRODUCTS.ATTRIBUTE_NAME|v Assoc Seq Line Items(Sport-100)|  
  
 [Volver al principio](#bkmk_top2)  
  
###  <a name="bkmk_Query5"></a> Consulta de ejemplo 5: devolver los 10 primeros conjuntos de elementos  
 En este ejemplo se muestra cómo utilizar algunas de las funciones de agrupación y ordenación que DMX proporciona de forma predeterminada. La consulta devuelve los 10 mejores conjuntos de elementos ordenados según el soporte para cada nodo. Observe que no necesita agrupar explícitamente los resultados, tal como haría en Transact-SQL; sin embargo, puede utilizar solo una función de agregado en cada consulta.  
  
```  
SELECT TOP 10 (NODE_SUPPORT),NODE_NAME, NODE_CAPTION  
FROM Association.CONTENT  
WHERE NODE_TYPE = 7  
```  
  
 Resultados del ejemplo:  
  
|||  
|-|-|  
|NODE_SUPPORT|4334|  
|NODE_NAME|37|  
|NODE_CAPTION|Sport-100 = Existing|  
  
 [Volver al principio](#bkmk_top2)  
  
## <a name="making-predictions-using-the-model"></a>Realizar predicciones utilizando el modelo  
 Un modelo de reglas de asociación se suele utilizar para generar recomendaciones, que se basan en las correlaciones detectadas en los conjuntos de elementos. Por tanto, cuando se crea una consulta de predicción basada en un modelo de reglas de asociación, normalmente se usan las reglas del modelo para realizar estimaciones basadas en nuevos datos.  [PredictAssociation &#40;DMX&#41;](/sql/dmx/predictassociation-dmx) es la función que devuelve las recomendaciones y tiene varios argumentos que se pueden usar para personalizar los resultados de la consulta.  
  
 Otro ejemplo de dónde podrían resultar útiles las consultas en un modelo de asociación consiste en devolver la confianza para diversas reglas y conjuntos de elementos con objeto de poder comparar la efectividad de distintas estrategias de ventas cruzadas. En los ejemplos siguientes se muestra cómo crear tales consultas.  
  
###  <a name="bkmk_Query6"></a> Consulta de ejemplo 6: predecir elementos asociados  
 En este ejemplo se usa el modelo de asociación creado en el [Tutorial intermedio de minería de datos &#40;Analysis Services - Minería de datos&#41;](../../tutorials/intermediate-data-mining-tutorial-analysis-services-data-mining.md). Muestra cómo crear una consulta de predicción que indica qué productos se deben recomendar a un cliente que ha comprado un producto determinado. Este tipo de consulta, donde se deben proporcionar valores para el modelo en una instrucción `SELECT…UNION`, se denomina consulta singleton. Dado que la columna del modelo de predicción correspondiente a los nuevos valores es una tabla anidada, se debe utilizar una cláusula `SELECT` para asignar el nuevo valor a la columna de tabla anidada, `[Model]`, y otra cláusula `SELECT` para asignar la columna de tabla anidada a la columna de nivel de caso, `[v Assoc Seq Line Items]`. Si agrega la palabra clave INCLUDE-STATISTICS a la consulta, podrá ver la probabilidad y el soporte para las recomendaciones.  
  
```  
SELECT PredictAssociation([Association].[vAssocSeqLineItems],INCLUDE_STATISTICS, 3)  
FROM [Association]  
NATURAL PREDICTION JOIN   
(SELECT  
(SELECT 'Classic Vest' as [Model])  
AS [v Assoc Seq Line Items])  
AS t  
```  
  
 Resultados del ejemplo:  
  
|Modelo|$SUPPORT|$PROBABILITY|$ADJUSTEDPROBABILITY|  
|-----------|--------------|------------------|--------------------------|  
|Sport-100|4334|0.291283|0.252696|  
|Water Bottle|2866|0.19262|0.175205|  
|Patch kit|2113|0.142012|0.132389|  
  
 [Volver al principio](#bkmk_top2)  
  
###  <a name="bkmk_Query7"></a> Consulta de ejemplo 7: determinar la confianza para los conjuntos de elementos relacionados  
 Mientras que las reglas son útiles para generar recomendaciones, los conjuntos de elementos resultan más interesantes para realizar análisis más profundos de los patrones existentes en el conjunto de datos. Por ejemplo, si no quedó satisfecho con las recomendaciones devueltas por la consulta de ejemplo anterior, podría examinar otros conjuntos de elementos que contuviesen el Producto A para tener una idea más clara de si dicho producto es un accesorio que se compra con todo tipo de productos, o si se trata de un producto estrechamente relacionado con las compras de determinados productos. La manera más fácil de explorar estas relaciones es filtrando los conjuntos de elementos en el Visor de asociación de [!INCLUDE[msCoName](../../includes/msconame-md.md)] ; sin embargo, se puede recuperar la misma información con una consulta.  
  
 La consulta de ejemplo siguiente devuelve todos los conjuntos de elementos que incluyen el elemento Water Bottle, incluido el elemento Water Bottle por sí solo.  
  
```  
SELECT TOP 100 FROM   
(  
SELECT FLATTENED NODE_CAPTION, NODE_SUPPORT,   
(SELECT ATTRIBUTE_NAME from NODE_DISTRIBUTION  
WHERE ATTRIBUTE_NAME = 'v Assoc Seq Line Items(Water Bottle)') as D  
FROM Association.CONTENT  
WHERE NODE_TYPE = 7  
) AS Items  
WHERE [D.ATTRIBUTE_NAME] <> NULL  
ORDER BY NODE_SUPPORT DESC  
```  
  
 Resultados del ejemplo:  
  
|NODE_CAPTION|NODE_SUPPORT|D.ATTRIBUTE_NAME|  
|-------------------|-------------------|-----------------------|  
|Water Bottle = Existing|2866|v Assoc Seq Line Items(Water Bottle)|  
|Mountain Bottle Cage = Existing, Water Bottle = Existing|1136|v Assoc Seq Line Items(Water Bottle)|  
|Road Bottle Cage = Existing, Water Bottle = Existing|1068|v Assoc Seq Line Items(Water Bottle)|  
|Water Bottle = Existing, Sport-100 = Existing|734|v Assoc Seq Line Items(Water Bottle)|  
  
 Esta consulta devuelve tanto las filas de la tabla anidada que cumplen los criterios, como todas las filas externas o de la tabla de casos. Por consiguiente, se debe agregar una condición que elimine las filas de la tabla de casos que tengan un valor NULL para el nombre del atributo de destino.  
  
 [Volver al principio](#bkmk_top2)  
  
## <a name="function-list"></a>Lista de funciones  
 Todos los algoritmos de [!INCLUDE[msCoName](../../includes/msconame-md.md)] son compatibles con un conjunto común de funciones. Sin embargo, el algoritmo de asociación de [!INCLUDE[msCoName](../../includes/msconame-md.md)] admite las funciones adicionales que se incluyen en la tabla siguiente.  
  
|||  
|-|-|  
|función de predicción|Uso|  
|[IsDescendant &#40;DMX&#41;](/sql/dmx/isdescendant-dmx)|Determina si un nodo es un elemento secundario de otro nodo en el gráfico de red neuronal.|  
|[IsInNode &#40;DMX&#41;](/sql/dmx/isinnode-dmx)|Indica si el nodo especificado contiene el caso actual.|  
|[PredictAdjustedProbability &#40;DMX&#41;](/sql/dmx/predictadjustedprobability-dmx)|Devuelve la probabilidad ponderada.|  
|[PredictAssociation &#40;DMX&#41;](/sql/dmx/predictassociation-dmx)|Predice los miembros de un conjunto de datos asociativo.|  
|[PredictHistogram &#40;DMX&#41;](/sql/dmx/predicthistogram-dmx)|Devuelve una tabla de valores relacionados con el valor de predicción actual.|  
|[PredictNodeId &#40;DMX&#41;](/sql/dmx/predictnodeid-dmx)|Devuelve el Node_ID de cada caso.|  
|[PredictProbability &#40;DMX&#41;](/sql/dmx/predictprobability-dmx)|Devuelve la probabilidad del valor de predicción.|  
|[PredictSupport &#40;DMX&#41;](/sql/dmx/predictsupport-dmx)|Devuelve el valor de soporte de un estado especificado.|  
|[PredictVariance &#40;DMX&#41;](/sql/dmx/predictvariance-dmx)|Devuelve la varianza del valor de predicción.|  
  
## <a name="see-also"></a>Vea también  
 [Algoritmo de asociación de Microsoft](microsoft-association-algorithm.md)   
 [Referencia técnica del algoritmo de asociación de Microsoft](microsoft-association-algorithm-technical-reference.md)   
 [Contenido para los modelos de asociación del modelo de minería de datos &#40;Analysis Services - minería de datos&#41;](mining-model-content-for-association-models-analysis-services-data-mining.md)  
  
  
