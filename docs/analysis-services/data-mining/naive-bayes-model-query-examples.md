---
title: Ejemplos de consultas de modelo Bayes naive | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- naive bayes model [Analysis Services]
- naive bayes algorithms [Analysis Services]
- content queries [DMX]
ms.assetid: e642bd7d-5afa-4dfb-8cca-4f84aadf61b0
caps.latest.revision: 13
author: Minewiskan
ms.author: owend
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 6935ffd8851a9454a1a2e53655be814a4eda3af1
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="naive-bayes-model-query-examples"></a>Ejemplos de consultas del modelo Bayes naive
  Cuando se crea una consulta en un modelo de minería de datos, puede tratarse de una consulta de contenido, que proporciona detalles sobre las reglas y los conjuntos de elementos detectados durante el análisis, o una consulta de predicción, que usa las asociaciones detectadas en los datos para realizar predicciones. También puede recuperar los metadatos sobre el modelo utilizando una consulta del conjunto de filas de esquema de minería de datos. En esta sección se explica cómo crear estas consultas para los modelos que se basan en el algoritmo Bayes naive de Microsoft.  
  
 **Consultas de contenido**  
  
 [Obtener metadatos del modelo usando DMX](#bkmk_Query1)  
  
 [Recuperar un resumen de los datos de entrenamiento](#bkmk_Query2)  
  
 [Buscar más información sobre atributos](#bkmk_Query3)  
  
 [Usar procedimientos almacenados del sistema](#bkmk_Query4)  
  
 **Consultas de predicción**  
  
 [Predecir los resultados utilizando una consulta singleton](#bkmk_Query5)  
  
 [Obtener predicciones con valores de probabilidad y compatibilidad](#bkmk_Query6)  
  
 [Predecir asociaciones](#bkmk_Query7)  
  
## <a name="finding-information-about-a-naive-bayes-model"></a>Buscar información sobre un modelo Bayes naive  
 El contenido de un modelo Bayes naive proporciona información agregada sobre la distribución de los valores en los datos de entrenamiento. También puede recuperar la información sobre los metadatos del modelo creando consultas con los conjuntos de filas de esquema de minería de datos.  
  
###  <a name="bkmk_Query1"></a> Consulta de ejemplo 1: obtener metadatos del modelo usando DMX  
 Al consultar el conjunto de filas de esquema de minería de datos, puede buscar los metadatos del modelo. Esto podría incluir cuándo se creó, cuándo se procesó en último lugar, el nombre de la estructura de minería de datos en la que se basa el modelo y el nombre de las columnas que se usan como atributos de predicción. También se pueden devolver los parámetros que se utilizaron cuando se creó el modelo.  
  
```  
SELECT MODEL_CATALOG, MODEL_NAME, DATE_CREATED, LAST_PROCESSED,  
SERVICE_NAME, PREDICTION_ENTITY, FILTER  
FROM $system.DMSCHEMA_MINING_MODELS  
WHERE MODEL_NAME = 'TM_NaiveBayes_Filtered'  
```  
  
 Resultados del ejemplo:  
  
|||  
|-|-|  
|MODEL_CATALOG|AdventureWorks|  
|MODEL_NAME|TM_NaiveBayes_Filtered|  
|DATE_CREATED|3/1/2008 19:15|  
|LAST_PROCESSED|3/2/2008 20:00|  
|SERVICE_NAME|Microsoft_Naive_Bayes|  
|PREDICTION_ENTITY|Bike Buyer,Yearly Income|  
|FILTER|[Region] = 'Europe' OR [Region] = 'North America'|  
  
 El modelo que se usa para este ejemplo está basado en el modelo Bayes naive que se crea en [Basic Data Mining Tutorial](http://msdn.microsoft.com/library/6602edb6-d160-43fb-83c8-9df5dddfeb9c), pero se modificó agregando un segundo atributo de predicción y aplicando un filtro a los datos de entrenamiento.  
  
###  <a name="bkmk_Query2"></a> Consulta de ejemplo 2: recuperar un resumen de los datos de entrenamiento  
 En un modelo Bayes naive, el nodo de estadísticas marginal almacena información agregada sobre la distribución de los valores de los datos de entrenamiento. Este resumen es cómodo y le evita tener que crear consultas SQL con los datos de entrenamiento para encontrar la misma información.  
  
 En el ejemplo siguiente se utiliza una consulta de contenido DMX para recuperar los datos del nodo (NODE_TYPE = 24). Dado que las estadísticas están almacenadas en una tabla anidada, la palabra clave FLATTENED se utiliza para facilitar la visualización de los resultados.  
  
```  
SELECT FLATTENED MODEL_NAME,  
(SELECT ATTRIBUTE_NAME, ATTRIBUTE_VALUE, [SUPPORT], [PROBABILITY], VALUETYPE FROM NODE_DISTRIBUTION) AS t  
FROM TM_NaiveBayes.CONTENT  
WHERE NODE_TYPE = 26  
```  
  
> [!NOTE]  
>  El nombre de las columnas, SUPPORT y PROBABILITY, debe ir entre corchetes para distinguirlo de las palabras clave reservadas de Expresiones multidimensionales (MDX) con los mismos nombres.  
  
 Resultados parciales:  
  
|MODEL_NAME|t.ATTRIBUTE_NAME|t.ATTRIBUTE_VALUE|t.SUPPORT|t.PROBABILITY|t.VALUETYPE|  
|-----------------|-----------------------|------------------------|---------------|-------------------|-----------------|  
|TM_NaiveBayes|Bike Buyer|Missing|0|0|1|  
|TM_NaiveBayes|Bike Buyer|0|8869|0.507263784|4|  
|TM_NaiveBayes|Bike Buyer|1|8615|0.492736216|4|  
|TM_NaiveBayes|Gender|Missing|0|0|1|  
|TM_NaiveBayes|Gender|F|8656|0.495081217|4|  
|TM_NaiveBayes|Gender|M|8828|0.504918783|4|  
  
 Por ejemplo, estos resultados le indican el número de casos de entrenamiento para cada valor discreto (VALUETYPE = 4), junto con la probabilidad calculada, ajustados para los valores que faltan (VALUETYPE = 1).  
  
 Para obtener una definición de los valores proporcionados en la tabla NODE_DISTRIBUTION en un modelo Bayes naive, vea [Contenido del modelo de minería de datos para los modelos Bayes naive &#40;Analysis Services - Minería de datos&#41;](../../analysis-services/data-mining/mining-model-content-for-naive-bayes-models-analysis-services-data-mining.md). Para más información sobre cómo afectan los valores que faltan a los cálculos de probabilidad y compatibilidad, vea [Valores ausentes &#40;Analysis Services - Minería de datos&#41;](../../analysis-services/data-mining/missing-values-analysis-services-data-mining.md).  
  
###  <a name="bkmk_Query3"></a> Consulta de ejemplo 3: buscar más información sobre atributos  
 Dado que un modelo Bayes naive a menudo contiene información compleja sobre las relaciones entre atributos diferentes, la manera más fácil de ver estas relaciones es utilizar el [Visor Bayes naive de Microsoft](../../analysis-services/data-mining/browse-a-model-using-the-microsoft-naive-bayes-viewer.md). Sin embargo, puede crear consultas DMX para devolver los datos.  
  
 En el ejemplo siguiente se muestra cómo devolver información del modelo sobre un atributo determinado, `Region`.  
  
```  
SELECT NODE_TYPE, NODE_CAPTION,   
NODE_PROBABILITY, NODE_SUPPORT, MSOLAP_NODE_SCORE  
FROM TM_NaiveBayes.CONTENT  
WHERE ATTRIBUTE_NAME = 'Region'  
```  
  
 Esta consulta devuelve dos tipos de nodos: el nodo que representa el atributo de entrada (NODE_TYPE = 10) y nodos para cada valor del atributo (NODE_TYPE = 11). El título del nodo se utiliza para identificarlo, en lugar del nombre, porque el título muestra tanto el nombre como el valor del atributo.  
  
|NODE_TYPE|NODE_CAPTION|NODE_PROBABILITY|NODE_SUPPORT|MSOLAP_NODE_SCORE|NODE_TYPE|  
|----------------|-------------------|-----------------------|-------------------|-------------------------|----------------|  
|10|Bike Buyer -> Region|1|17484|84.51555875|10|  
|11|Bike Buyer -> Region = Missing|0|0|0|11|  
|11|Bike Buyer -> Region = North America|0.508236102|8886|0|11|  
|11|Bike Buyer -> Region = Pacific|0.193891558|3390|0|11|  
|11|Bike Buyer -> Region = Europe|0.29787234|5208|0|11|  
  
 Algunas de las columnas almacenadas en los nodos son las mismas que se pueden obtener de los nodos de estadísticas marginales, como los valores de compatibilidad de los nodos y de puntuación de la probabilidad de los nodos. Sin embargo, MSOLAP_NODE_SCORE es un valor especial que solo se proporciona para los nodos de atributos de entrada e indica la importancia relativa de este atributo en el modelo. Puede ver casi toda esa misma información en el panel Red de dependencia del visor; sin embargo, el visor no proporciona puntuaciones.  
  
 La consulta siguiente devuelve las puntuaciones de importancia de todos los atributos del modelo:  
  
```  
SELECT NODE_CAPTION, MSOLAP_NODE_SCORE  
FROM TM_NaiveBayes.CONTENT  
WHERE NODE_TYPE = 10  
ORDER BY MSOLAP_NODE_SCORE DESC  
```  
  
 Resultados del ejemplo:  
  
|NODE_CAPTION|MSOLAP_NODE_SCORE|  
|-------------------|-------------------------|  
|Bike Buyer -> Total Children|181.3654836|  
|Bike Buyer -> Commute Distance|179.8419482|  
|Bike Buyer -> English Education|156.9841928|  
|Bike Buyer -> Number Children At Home|111.8122599|  
|Bike Buyer -> Region|84.51555875|  
|Bike Buyer -> Marital Status|23.13297354|  
|Bike Buyer -> English Occupation|2.832069191|  
  
 Al examinar el contenido del modelo en el [Visor de árbol de contenido genérico de Microsoft](../../analysis-services/data-mining/browse-a-model-using-the-microsoft-generic-content-tree-viewer.md), se hará una mejor idea de qué estadísticas podrían ser interesantes. Aquí se demostraron algunos ejemplos sencillos; más a menudo puede que tenga que ejecutar varias consultas o almacenar los resultados y procesarlos en el cliente.  
  
###  <a name="bkmk_Query4"></a> Consulta de ejemplo 4: usar procedimientos almacenados del sistema  
 Para explorar los resultados, puede utilizar algunos procedimientos almacenados de sistema de Analysis Services además de escribir sus propias consultas de contenido. Para utilizar un procedimiento almacenado de sistema, anteponga al nombre del procedimiento almacenado la palabra clave CALL:  
  
```  
CALL GetPredictableAttributes ('TM_NaiveBayes')  
```  
  
 Resultados parciales:  
  
|ATTRIBUTE_NAME|NODE_UNIQUE_NAME|  
|---------------------|------------------------|  
|Bike Buyer|100000001|  
  
> [!NOTE]  
>  Estos procedimientos almacenados de sistema son para la comunicación interna entre el servidor de Analysis Services y el cliente, y solamente se utilizan por comodidad al desarrollar y probar los modelos de minería de datos. Al crear consultas para un sistema de producción, siempre debería escribir sus consultas utilizando DMX.  
  
 Para más información sobre los procedimientos almacenados del sistema de Analysis Services, vea [Procedimientos almacenados de minería de datos &#40;Analysis Services - Minería de datos&#41;](../../analysis-services/data-mining/data-mining-stored-procedures-analysis-services-data-mining.md).  
  
## <a name="using-a-naive-bayes-model-to-make-predictions"></a>Usar un modelo Bayes naive para realizar predicciones  
 El algoritmo Bayes naive de Microsoft se suele utilizar menos para la predicción que para la exploración de relaciones entre los atributos de predicción y la entrada. Sin embargo, el modelo admite el uso de funciones de predicción tanto para predicción como para asociación.  
  
###  <a name="bkmk_Query5"></a> Consulta de ejemplo 5: predecir los resultados utilizando una consulta singleton  
 La consulta siguiente utiliza una consulta singleton para proporcionar un nuevo valor y predecir, según el modelo, si es probable que un cliente con estas características compre una bicicleta. La manera más fácil de crear una consulta singleton en un modelo de regresión es usar el cuadro de diálogo **Entrada de consulta singleton** . Por ejemplo, puede generar la consulta DMX siguiente seleccionando el modelo `TM_NaiveBayes` , eligiendo **Consulta singleton**y seleccionando los valores en las listas desplegables para `[Commute Distance]` y `Gender`.  
  
```  
SELECT  
  Predict([TM_NaiveBayes].[Bike Buyer])  
FROM  
  [TM_NaiveBayes]  
NATURAL PREDICTION JOIN  
(SELECT '5-10 Miles' AS [Commute Distance],  
  'F' AS [Gender]) AS t  
```  
  
 Resultados del ejemplo:  
  
|Expresión|  
|----------------|  
|0|  
  
 La función de predicción devuelve el valor más probable, en este caso 0, que significa que es improbable que este tipo de cliente compre una bicicleta.  
  
###  <a name="bkmk_Query6"></a> Consulta de ejemplo 6: obtener predicciones con valores de probabilidad y compatibilidad  
 Además de predecir un resultado, a menudo desea conocer la precisión de la predicción. La consulta siguiente usa la misma consulta singleton que el ejemplo anterior, pero agrega la función de predicción [PredictHistogram &#40;DMX&#41;](../../dmx/predicthistogram-dmx.md) para devolver una tabla anidada que contiene las estadísticas de la compatibilidad de la predicción.  
  
```  
SELECT  
  Predict([TM_NaiveBayes].[Bike Buyer]),  
  PredictHistogram([TM_NaiveBayes].[Bike Buyer])  
FROM  
  [TM_NaiveBayes]  
NATURAL PREDICTION JOIN  
(SELECT '5-10 Miles' AS [Commute Distance],  
  'F' AS [Gender]) AS t  
```  
  
 Resultados del ejemplo:  
  
|Bike Buyer|$SUPPORT|$PROBABILITY|$ADJUSTEDPROBABILITY|$VARIANCE|$STDEV|  
|----------------|--------------|------------------|--------------------------|---------------|------------|  
|0|10161.5714|0.581192599|0.010530981|0|0|  
|1|7321.428768|0.418750215|0.008945684|0|0|  
||0.999828444|5.72E-05|5.72E-05|0|0|  
  
 La fila final en la tabla muestra los ajustes para la compatibilidad y la probabilidad del valor que falta. Los valores de la desviación estándar y la varianza siempre son 0, porque los modelos Bayes naive no pueden modelar los valores continuos.  
  
###  <a name="bkmk_Query7"></a> Consulta de ejemplo 7: predecir las asociaciones  
 El algoritmo Bayes naive de Microsoft se puede utilizar para el análisis de la asociación, si la estructura de minería de datos contiene una tabla anidada con el atributo de predicción como clave. Por ejemplo, podría crear un modelo Bayes naive al usar la estructura de minería de datos creada en [Lección 3: Generar un escenario de cesta de la compra &#40;Tutorial intermedio de minería de datos&#41;](http://msdn.microsoft.com/library/651eef38-772e-4d97-af51-075b1b27fc5a) del tutorial de minería de datos. El modelo utilizado en este ejemplo se modificó para agregar información sobre los ingresos y la región del cliente en la tabla de casos.  
  
 En el ejemplo de consulta siguiente se muestra una consulta singleton que predice los productos que están relacionados con las compras del producto, `'Road Tire Tube'`. Podría utilizar esta información para recomendar productos a un tipo específico de cliente.  
  
```  
SELECT   PredictAssociation([Association].[v Assoc Seq Line Items])  
FROM [Association_NB]  
NATURAL PREDICTION JOIN  
(SELECT 'High' AS [Income Group],  
  'Europe' AS [Region],  
  (SELECT 'Road Tire Tube' AS [Model])   
AS [v Assoc Seq Line Items])   
AS t  
```  
  
 Resultados parciales:  
  
|Modelo|  
|-----------|  
|Women's Mountain Shorts|  
|Water Bottle|  
|Touring-3000|  
|Touring-2000|  
|Touring-1000|  
  
## <a name="function-list"></a>Lista de funciones  
 Todos los algoritmos de [!INCLUDE[msCoName](../../includes/msconame-md.md)] son compatibles con un conjunto común de funciones. No obstante, el algoritmo Bayes naive de [!INCLUDE[msCoName](../../includes/msconame-md.md)] admite las funciones adicionales que se enumeran en la siguiente tabla.  
  
|||  
|-|-|  
|función de predicción|Uso|  
|[IsDescendant &#40;DMX&#41;](../../dmx/isdescendant-dmx.md)|Determina si un nodo es un elemento secundario de otro nodo del modelo.|  
|[Predict &#40;DMX&#41;](../../dmx/predict-dmx.md)|Devuelve un valor o un conjunto de valores predichos para una columna especificada.|  
|[PredictAdjustedProbability &#40;DMX&#41;](../../dmx/predictadjustedprobability-dmx.md)|Devuelve la probabilidad ponderada.|  
|[PredictAssociation &#40;DMX&#41;](../../dmx/predictassociation-dmx.md)|Predice los miembros de un conjunto de datos asociativo.|  
|[PredictNodeId &#40;DMX&#41;](../../dmx/predictnodeid-dmx.md)|Devuelve el Node_ID de cada caso.|  
|[PredictProbability &#40;DMX&#41;](../../dmx/predictprobability-dmx.md)|Devuelve la probabilidad del valor de predicción.|  
|[PredictSupport &#40;DMX&#41;](../../dmx/predictsupport-dmx.md)|Devuelve el valor de soporte de un estado especificado.|  
  
 Para ver la sintaxis de funciones específicas, vea [Referencia de funciones de Extensiones de minería de datos &#40;DMX&#41;](../../dmx/data-mining-extensions-dmx-function-reference.md).  
  
## <a name="see-also"></a>Vea también  
 [Referencia técnica del algoritmo Bayes naive de Microsoft](../../analysis-services/data-mining/microsoft-naive-bayes-algorithm-technical-reference.md)   
 [Microsoft Naive Bayes Algorithm](../../analysis-services/data-mining/microsoft-naive-bayes-algorithm.md)   
 [Contenido del modelo de minería de datos para los modelos Bayes naive &#40;Analysis Services - Minería de datos&#41;](../../analysis-services/data-mining/mining-model-content-for-naive-bayes-models-analysis-services-data-mining.md)  
  
  

