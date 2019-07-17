---
title: Ejemplos de consultas de modelo de árboles de decisión | Microsoft Docs
ms.date: 05/01/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: b2045dfa9923fb745f0f9d3936579a4e73a50564
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "68210062"
---
# <a name="decision-trees-model-query-examples"></a>Ejemplos de consultas de modelos de árboles de decisión
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Cuando se crea una consulta en un modelo de minería de datos, puede tratarse de una consulta de contenido, que proporciona detalles de los patrones detectados durante el análisis, o de una consulta de predicción, que utiliza los patrones del modelo para realizar predicciones de los nuevos datos. Por ejemplo, una consulta de contenido para un modelo de árboles de decisión puede proporcionar estadísticas sobre el número de casos en cada nivel del árbol, o de las reglas que diferencian los casos. O bien, una consulta de predicción asigna el modelo a los datos nuevos para generar recomendaciones, clasificaciones, etc. También se pueden recuperar metadatos sobre el modelo mediante una consulta.  
  
 En esta sección se explica cómo crear consultas para modelos basados en el algoritmo de árboles de decisión de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **Consultas de contenido**  
  
 [Recuperar parámetros del modelo a partir del conjunto de filas de esquema de minería de datos](#bkmk_Query1)  
  
 [Obtener detalles sobre los árboles del modelo mediante DMX](#bkmk_Query2)  
  
 [Recuperar subárboles a partir del modelo](#bkmk_Query3)  
  
 **Consultas de predicción**  
  
 [Devolver predicciones con probabilidades](#bkmk_Query4)  
  
 [Predecir asociaciones a partir de un modelo de árbol de decisión](#bkmk_Query5)  
  
 [Recuperar una fórmula de regresión a partir de un modelo de árbol de decisión](#bkmk_Query6)  
  
##  <a name="bkmk_top2"></a> Buscar información sobre un modelo de árbol de decisión  
 Para crear consultas significativas en el contenido de un modelo de árboles de decisión, se debe entender la estructura del contenido del modelo, así como qué tipos de nodo almacenan información y de qué tipo es esta. Para obtener más información, vea [Contenido del modelo de minería de datos para los modelos de árboles de decisión &#40;Analysis Services - Minería de datos&#41;](../../analysis-services/data-mining/mining-model-content-for-decision-tree-models-analysis-services-data-mining.md).  
  
###  <a name="bkmk_Query1"></a> Consulta de ejemplo 1: Recuperar parámetros del modelo a partir del conjunto de filas de esquema de minería de datos  
 Al consultar el conjunto de filas de esquema de minería de datos, se pueden encontrar metadatos sobre el modelo, como cuándo se creó, cuándo se procesó por última vez, el nombre de la estructura de minería de datos en que se basa el modelo, y el nombre de la columna que se usa como atributo de predicción. También se pueden devolver los parámetros que se utilizaron cuando se creó el modelo por primera vez.  
  
```  
select MINING_PARAMETERS   
from $system.DMSCHEMA_MINING_MODELS  
WHERE MODEL_NAME = 'TM_Decision Tree'  
```  
  
 Resultados del ejemplo:  
  
 MINING_PARAMETERS  
  
 COMPLEXITY_PENALTY=0.5, MAXIMUM_INPUT_ATTRIBUTES=255,MAXIMUM_OUTPUT_ATTRIBUTES=255,MINIMUM_SUPPORT=10,SCORE_METHOD=4,SPLIT_METHOD=3,FORCE_REGRESSOR=  
  
###  <a name="bkmk_Query2"></a> Consulta de ejemplo 2: Devolver detalles sobre el contenido del modelo utilizando DMX  
 La consulta siguiente devuelve información básica sobre los árboles de decisión creados cuando compiló el modelo en el [Basic Data Mining Tutorial](http://msdn.microsoft.com/library/6602edb6-d160-43fb-83c8-9df5dddfeb9c). Todas las estructuras de árboles se almacenan en su propio nodo. Dado que este modelo contiene un único atributo de predicción, solamente hay un nodo de árbol. Sin embargo, si se crea un modelo de asociación mediante el algoritmo de árboles de decisión, puede que haya centenares de árboles, uno para cada producto.  
  
 Esta consulta devuelve todos los nodos de tipo 2, que son los nodos de nivel superior de un árbol que representa un atributo de predicción determinado.  
  
> [!NOTE]  
>  La columna CHILDREN_CARDINALITY debe ir entre corchetes para distinguirla de la palabra clave reservada de MDX con la misma denominación.  
  
```  
SELECT MODEL_NAME, NODE_NAME, NODE_CAPTION,   
NODE_SUPPORT, [CHILDREN_CARDINALITY]  
FROM TM_DecisionTrees.CONTENT  
WHERE NODE_TYPE = 2  
```  
  
 Resultados del ejemplo:  
  
|MODEL_NAME|NODE_NAME|NODE_CAPTION|NODE_SUPPORT|CHILDREN_CARDINALITY|  
|-----------------|----------------|-------------------|-------------------|---------------------------|  
|TM_DecisionTree|000000001|Todo|12939|5|  
  
 ¿Qué indican estos resultados? En un modelo de árboles de decisión, la cardinalidad de un nodo determinado indica cuántos elementos secundarios inmediatos tiene el nodo. La cardinalidad de este nodo es 5. Es decir, el modelo dividió la población de destino de posibles compradores de bicicletas en 5 subgrupos.  
  
 La consulta relacionada siguiente devuelve los elementos secundarios para estos cinco subgrupos, junto con la distribución de atributos y valores de los nodos secundarios. Dado que elementos estadísticos como compatibilidad, probabilidad y varianza se almacenan en la tabla anidada NODE_DISTRIBUTION, este ejemplo usa la palabra clave `FLATTENED` para generar las columnas de la tabla anidada.  
  
> [!NOTE]  
>  La columna de tabla anidada SUPPORT debe ir entre corchetes para distinguirla de la palabra clave reservada con la misma denominación.  
  
```  
SELECT FLATTENED NODE_NAME, NODE_CAPTION,  
(SELECT ATTRIBUTE_NAME, ATTRIBUTE_VALUE, [SUPPORT]  
FROM NODE_DISTRIBUTION) AS t  
FROM TM_DecisionTree.CONTENT  
WHERE [PARENT_UNIQUE_NAME] = '000000001'  
```  
  
 Resultados del ejemplo:  
  
|NODE_NAME|NODE_CAPTION|T.ATTRIBUTE_NAME|T.ATTRIBUTE_VALUE|Support|  
|----------------|-------------------|-----------------------|------------------------|-------------|  
|00000000100|Number Cars Owned = 0|Bike Buyer|Missing|0|  
|00000000100|Number Cars Owned = 0|Bike Buyer|0|1067|  
|00000000100|Number Cars Owned = 0|Bike Buyer|1|1875|  
|00000000101|Number Cars Owned = 3|Bike Buyer|Missing|0|  
|00000000101|Number Cars Owned = 3|Bike Buyer|0|678|  
|00000000101|Number Cars Owned = 3|Bike Buyer|1|473|  
  
 A partir de estos resultados, se puede decir que, de los clientes que compraron una bicicleta ([Bike Buyer] = 1), 1067 clientes tenían 0 automóviles y 473 clientes tenían 3 automóviles.  
  
###  <a name="bkmk_Query3"></a> Consulta de ejemplo 3: Recuperar subárboles a partir del modelo  
 Suponga que desea averiguar más sobre los clientes que compraron una bicicleta. Puede ver detalles adicionales de cualquiera de los subárboles usando la función [IsDescendant &#40;DMX&#41;](../../dmx/isdescendant-dmx.md) en la consulta, como se muestra en el ejemplo siguiente. La consulta devuelve el recuento de compradores de bicicletas recuperando los nodos hoja (NODE_TYPE = 4) del árbol que contiene clientes con más de 42 años de edad. La consulta restringe las filas de la tabla anidada a aquellos en los que Bike Buyer = 1.  
  
```  
SELECT FLATTENED NODE_NAME, NODE_CAPTION,NODE_TYPE,  
(  
SELECT [SUPPORT] FROM NODE_DISTRIBUTION WHERE ATTRIBUTE_NAME = 'Bike Buyer' AND ATTRIBUTE_VALUE = '1'  
) AS t  
FROM TM_DecisionTree.CONTENT  
WHERE ISDESCENDANT('0000000010001')  
AND NODE_TYPE = 4  
```  
  
 Resultados del ejemplo:  
  
|NODE_NAME|NODE_CAPTION|t.SUPPORT|  
|----------------|-------------------|---------------|  
|000000001000100|Yearly Income >= 26000 and < 42000|266|  
|00000000100010100|Total Children = 3|75|  
|0000000010001010100|Number Children At Home = 1|75|  
  
## <a name="making-predictions-using-a-decision-trees-model"></a>Realizar predicciones mediante un modelo de árbol de decisión  
 Dado que los árboles de decisión se pueden utilizar para diversas tareas, como son la clasificación, la regresión e incluso la asociación, al crear una consulta de predicción en un modelo de árbol de decisión se tienen muchas opciones disponibles. Se debe conocer el propósito para el que se creó el modelo si desea entender los resultados de la predicción. Los ejemplos de consulta siguientes ilustran tres escenarios diferentes:  
  
-   Devolver una predicción para un modelo de clasificación, junto con la probabilidad de que la predicción sea correcta, y después filtrar los resultados por probabilidad;  
  
-   Crear una consulta singleton para predecir asociaciones;  
  
-   Recuperar la fórmula de regresión para una parte de un árbol de decisión en el que la relación entre la entrada y la salida es lineal.  
  
###  <a name="bkmk_Query4"></a> Consulta de ejemplo 4: Devolver predicciones con probabilidades  
 La consulta de ejemplo siguiente utiliza el modelo de árbol de decisión que se creó en [Basic Data Mining Tutorial](http://msdn.microsoft.com/library/6602edb6-d160-43fb-83c8-9df5dddfeb9c). La consulta pasa un nuevo conjunto de datos de ejemplo, a partir de la tabla dbo.ProspectiveBuyers de [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] DW, para predecir cuál de los clientes del nuevo conjunto de datos comprará una bicicleta.  
  
 La consulta usa la función de predicción [PredictHistogram &#40;DMX&#41;](../../dmx/predicthistogram-dmx.md), que devuelve una tabla anidada que contiene información útil sobre las probabilidades detectadas por el modelo. La cláusula WHERE final de la consulta filtra los resultados para devolver solo los clientes de los que se ha predicho que son posibles compradores de bicicletas con una probabilidad mayor del 0%.  
  
```  
SELECT  
  [TM_DecisionTree].[Bike Buyer],  
  PredictHistogram([Bike Buyer]) as Results  
From  
  [TM_DecisionTree]  
PREDICTION JOIN  
  OPENQUERY([Adventure Works DW Multidimensional 2012],  
    'SELECT  
      [FirstName],  
      [LastName],  
      [MaritalStatus],  
      [Gender],  
      [YearlyIncome],  
      [TotalChildren],  
      [NumberChildrenAtHome],  
      [HouseOwnerFlag],  
      [NumberCarsOwned]  
    FROM  
      [dbo].[ProspectiveBuyer]  
    ') AS t  
ON  
  [TM_DecisionTree].[First Name] = t.[FirstName] AND  
  [TM_DecisionTree].[Last Name] = t.[LastName] AND  
  [TM_DecisionTree].[Marital Status] = t.[MaritalStatus] AND  
  [TM_DecisionTree].[Gender] = t.[Gender] AND  
  [TM_DecisionTree].[Yearly Income] = t.[YearlyIncome] AND  
  [TM_DecisionTree].[Total Children] = t.[TotalChildren] AND  
  [TM_DecisionTree].[Number Children At Home] = t.[NumberChildrenAtHome] AND  
  [TM_DecisionTree].[House Owner Flag] = t.[HouseOwnerFlag] AND  
  [TM_DecisionTree].[Number Cars Owned] = t.[NumberCarsOwned]  
WHERE [Bike Buyer] = 1  
AND PredictProbability([Bike Buyer]) >'.05'  
```  
  
 De forma predeterminada, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] devuelve tablas anidadas con la etiqueta de columna, **Expression**. Se puede cambiar esta etiqueta creando un alias de la columna que se devuelve. Si hace esto, el alias (en este caso, **Results**) se usa como encabezado de columna y como valor en la tabla anidada. Se debe expandir la tabla anidada para ver los resultados.  
  
 Ejemplo de resultados con **Bike Buyer** = 1:  
  
|Bike Buyer|$SUPPORT|$PROBABILITY|$ADJUSTEDPROBABILITY|$VARIANCE|$STDEV|  
|----------------|--------------|------------------|--------------------------|---------------|------------|  
|1|2540|0.634849242045644|0.013562168281562|0|0|  
|0|1460|0.364984174579377|0.00661336932550915|0|0|  
||0|0.000166583374979177|0.000166583374979177|0|0|  
  
 Si el proveedor no admite conjuntos de filas jerárquicos, como los mostrados aquí, puede usar la palabra clave FLATTENED en la consulta para devolver los resultados como una tabla que contenga valores NULL en lugar de valores de columna repetidos. Para obtener más información, vea [Tablas anidadas &#40;Analysis Services - Minería de datos&#41;](../../analysis-services/data-mining/nested-tables-analysis-services-data-mining.md) y [Descripción de la instrucción Select de DMX](../../dmx/understanding-the-dmx-select-statement.md).  
  
###  <a name="bkmk_Query5"></a> Consulta de ejemplo 5: Predecir asociaciones a partir de un modelo de árbol de decisión  
 La siguiente consulta de ejemplo se basa en la estructura de minería de datos Association. Para proseguir con este ejemplo, puede agregar un nuevo modelo a esta estructura de minería de datos y seleccionar árboles de decisión de Microsoft como algoritmo. Para obtener más información sobre cómo crear la estructura de minería de datos de asociación, vea [lección 3: Generar un escenario de cesta &#40;intermedio de Tutorial de minería de datos&#41;](http://msdn.microsoft.com/library/651eef38-772e-4d97-af51-075b1b27fc5a).  
  
 La consulta de ejemplo siguiente es una consulta singleton, que se puede crear con facilidad en [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] eligiendo los campos y seleccionando a continuación los valores para esos campos en una lista desplegable.  
  
```  
SELECT PredictAssociation([DT_Association].[v Assoc Seq Line Items],3)  
FROM  
  [DT_Association]  
NATURAL PREDICTION JOIN  
(SELECT (SELECT 'Patch kit' AS [Model]) AS [v Assoc Seq Line Items]) AS t  
```  
  
 Resultados esperados:  
  
|Modelo|  
|-----------|  
|Mountain-200|  
|Mountain Tire Tube|  
|Touring Tire Tube|  
  
 Los resultados indican los tres productos mejores que se pueden recomendar a los clientes que han comprado el producto Patch Kit. También se pueden proporcionar varios productos como entrada cuando se realizan recomendaciones, ya sea escribiendo valores o usando el cuadro de diálogo **Entrada de consulta singleton** y agregando o quitando valores. La consulta de ejemplo siguiente muestra cómo se proporcionan los múltiples valores con los que se puede realizar una predicción. Los valores se conectan mediante una cláusula UNION en la instrucción SELECT que define los valores de entrada.  
  
```  
SELECT PredictAssociation([DT_Association].[v Assoc Seq Line Items],3)  
From  
  [DT_Association]  
NATURAL PREDICTION JOIN  
(SELECT (SELECT 'Racing Socks' AS [Model]  
  UNION SELECT 'Women''s Mountain Shorts' AS [Model]) AS [v Assoc Seq Line Items]) AS t  
```  
  
 Resultados esperados:  
  
|Modelo|  
|-----------|  
|Long-Sleeve Logo Jersey|  
|Mountain-400-W|  
|Classic Vest|  
  
###  <a name="bkmk_Query6"></a> Consulta de ejemplo 6: Recuperar una fórmula de regresión a partir de un modelo de árbol de decisión  
 Cuando se crea un modelo de árbol de decisión que contiene una regresión en un atributo continuo, se puede utilizar la fórmula de regresión para hacer predicciones, o se puede extraer información sobre la fórmula de regresión. Para obtener más información sobre consultas en modelos de regresión, vea [Ejemplos de consultas de modelos de regresión lineal](../../analysis-services/data-mining/linear-regression-model-query-examples.md).  
  
 Si un modelo de árbol de decisión contiene una combinación de nodos de regresión y nodos que se dividen en intervalos o atributos discretos, se puede crear una consulta que devuelva solo el nodo de regresión. La tabla NODE_DISTRIBUTION contiene los detalles de la fórmula de regresión. En este ejemplo, se quita información de estructura jerárquica de las columnas y la tabla NODE_DISTRIBUTION usa un alias para facilitar la presentación. Pero, en este modelo, no se encontró ningún regresor para relacionar Income con otros atributos continuos. En casos como éste, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] devuelve el valor medio del atributo y la varianza total en el modelo para ese atributo.  
  
```  
SELECT FLATTENED NODE_DISTRIBUTION AS t  
FROM DT_Predict. CONTENT  
WHERE NODE_TYPE = 25  
```  
  
 Resultados del ejemplo:  
  
|T.ATTRIBUTE_NAME|t.ATTRIBUTE_VALUE|t.SUPPORT|t.PROBABILITY|t.VARIANCE|t.VALUETYPE|  
|-----------------------|------------------------|---------------|-------------------|----------------|-----------------|  
|Yearly Income|Missing|0|0.000457142857142857|0|1|  
|Yearly Income|57220.8876687257|17484|0.999542857142857|1041275619.52776|3|  
||57220.8876687257|0|0|1041216662.54387|11|  
  
 Para obtener más información sobre los tipos de valor y las estadísticas usadas en modelos de regresión, vea [Contenido del modelo de minería de datos para los modelos de regresión lineal &#40;Analysis Services - Minería de datos&#41;](../../analysis-services/data-mining/mining-model-content-for-linear-regression-models-analysis-services-data-mining.md).  
  
## <a name="list-of-prediction-functions"></a>Lista de funciones de predicción  
 Todos los algoritmos de [!INCLUDE[msCoName](../../includes/msconame-md.md)] son compatibles con un conjunto común de funciones. Sin embargo, el algoritmo de árboles de decisión de [!INCLUDE[msCoName](../../includes/msconame-md.md)] admite las funciones adicionales que se enumeran en la tabla siguiente.  
  
|||  
|-|-|  
|Función de predicción|Uso|  
|[IsDescendant &#40;DMX&#41;](../../dmx/isdescendant-dmx.md)|Determina si un nodo es un elemento secundario de otro nodo del modelo.|  
|[IsInNode &#40;DMX&#41;](../../dmx/isinnode-dmx.md)|Indica si el nodo especificado contiene el caso actual.|  
|[PredictAdjustedProbability &#40;DMX&#41;](../../dmx/predictadjustedprobability-dmx.md)|Devuelve la probabilidad ponderada.|  
|[PredictAssociation &#40;DMX&#41;](../../dmx/predictassociation-dmx.md)|Predice los miembros de un conjunto de datos asociativo.|  
|[PredictHistogram &#40;DMX&#41;](../../dmx/predicthistogram-dmx.md)|Devuelve una tabla de valores relacionados con el valor de predicción actual.|  
|[PredictNodeId &#40;DMX&#41;](../../dmx/predictnodeid-dmx.md)|Devuelve el Node_ID de cada caso.|  
|[PredictProbability &#40;DMX&#41;](../../dmx/predictprobability-dmx.md)|Devuelve la probabilidad del valor de predicción.|  
|[PredictStdev &#40;DMX&#41;](../../dmx/predictstdev-dmx.md)|Devuelve la desviación estándar predicha para la columna especificada.|  
|[PredictSupport &#40;DMX&#41;](../../dmx/predictsupport-dmx.md)|Devuelve el valor de soporte de un estado especificado.|  
|[PredictVariance &#40;DMX&#41;](../../dmx/predictvariance-dmx.md)|Devuelve la varianza de una columna especificada.|  
  
 Para consultar una lista de las funciones comunes a todos los algoritmos de [!INCLUDE[msCoName](../../includes/msconame-md.md)], vea [Funciones de predicción generales &#40;DMX&#41;](../../dmx/general-prediction-functions-dmx.md). Para más información sobre la sintaxis de funciones específicas, vea [Referencia de funciones de Extensiones de minería de datos &#40;DMX&#41;](../../dmx/data-mining-extensions-dmx-function-reference.md).  
  
## <a name="see-also"></a>Vea también  
 [Consultas de minería de datos](../../analysis-services/data-mining/data-mining-queries.md)   
 [Algoritmo de árboles de decisión de Microsoft](../../analysis-services/data-mining/microsoft-decision-trees-algorithm.md)   
 [Referencia técnica del algoritmo de árboles de decisión de Microsoft](../../analysis-services/data-mining/microsoft-decision-trees-algorithm-technical-reference.md)   
 [Contenido del modelo de minería de datos para los modelos de árboles de decisión &#40;Analysis Services - Minería de datos&#41;](../../analysis-services/data-mining/mining-model-content-for-decision-tree-models-analysis-services-data-mining.md)  
  
  
