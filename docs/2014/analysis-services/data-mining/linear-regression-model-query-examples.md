---
title: Ejemplos de consultas de modelos de regresión lineal | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- linear regression algorithms [Analysis Services]
- linear regression [Analysis Services]
- content queries [DMX]
ms.assetid: fd3cf312-57a1-44b6-b772-fce6fc1c26d7
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 917e41f6053aa499c7d3d7ca51a32b033591bdc1
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "66084296"
---
# <a name="linear-regression-model-query-examples"></a>Ejemplos de consultas de modelos de regresión lineal
  Cuando se crea una consulta en un modelo de minería de datos, puede tratarse de una consulta de contenido, que proporciona detalles de los patrones detectados durante el análisis, o de una consulta de predicción, que utiliza los patrones del modelo para realizar predicciones de los nuevos datos. Por ejemplo, una consulta de contenido podría proporcionar detalles adicionales sobre la fórmula de regresión, mientras que una consulta de predicción podría indicar si un nuevo punto de datos se ajusta al modelo. También se pueden recuperar metadatos sobre el modelo mediante una consulta.  
  
 En esta sección se explica cómo crear consultas para los modelos que se basan en el algoritmo de regresión lineal de Microsoft.  
  
> [!NOTE]  
>  Dado que la regresión lineal está basada en un caso especial del algoritmo de árboles de decisión de Microsoft, hay muchas similitudes y algunos modelos de árbol de decisión que utilizan atributos de predicción continuos pueden contener fórmulas de regresión. Para más información, vea [Referencia técnica del algoritmo de árboles de decisión de Microsoft](microsoft-decision-trees-algorithm-technical-reference.md).  
  
 **Consultas de contenido**  
  
 [Usar el conjunto de filas de esquema de minería de datos para determinar los parámetros que se usan para un modelo](#bkmk_Query1)  
  
 [Usar DMX para devolver la fórmula de regresión del modelo](#bkmk_Query2)  
  
 [Devolver solo el coeficiente para el modelo](#bkmk_Query3)  
  
 **Consultas de predicción**  
  
 [Predecir los ingresos utilizando una consulta singleton](#bkmk_Query4)  
  
 [Usar funciones de predicción con un modelo de regresión](#bkmk_Query5)  
  
##  <a name="finding-information-about-the-linear-regression-model"></a><a name="bkmk_top"></a>Buscar información sobre el modelo de regresión lineal  
 La estructura de un modelo de regresión lineal es sumamente simple: el modelo de minería de datos representa los datos como un nodo único, que define la fórmula de regresión. Para obtener más información, vea [Contenido del modelo de minería de datos para los modelos de regresión logística &#40;Analysis Services - Minería de datos&#41;](mining-model-content-for-logistic-regression-models.md).  
  
 [Volver al principio](#bkmk_top)  
  
###  <a name="sample-query-1-using-the-data-mining-schema-rowset-to-determine-parameters-used-for-a-model"></a><a name="bkmk_Query1"></a>Consulta de ejemplo 1: usar el conjunto de filas de esquema de minería de datos para determinar los parámetros usados para un modelo  
 Al consultar el conjunto de filas de esquema de minería de datos, puede buscar los metadatos acerca del modelo. Podría incluirse cuándo se creó el modelo, cuándo se procesó en último lugar, el nombre de la estructura de minería de datos en la que se basa y el nombre de la columna que se usa como atributo de predicción. También se pueden devolver los parámetros que se utilizaron cuando se creó el modelo por primera vez.  
  
```  
SELECT MINING_PARAMETERS   
FROM $system.DMSCHEMA_MINING_MODELS  
WHERE MODEL_NAME = 'TM_PredictIncome'  
```  
  
 Resultados del ejemplo:  
  
|MINING_PARAMETERS|  
|------------------------|  
|COMPLEXITY_PENALTY=0.9,<br /><br /> MAXIMUM_INPUT_ATTRIBUTES=255,<br /><br /> MAXIMUM_OUTPUT_ATTRIBUTES=255,<br /><br /> MINIMUM_SUPPORT=10,<br /><br /> SCORE_METHOD=4,<br /><br /> SPLIT_METHOD=3,<br /><br /> FORCE_REGRESSOR=|  
  
> [!NOTE]  
>  La configuración del parámetro, "`FORCE_REGRESSOR =` ", indica que el valor actual del parámetro FORCE_REGRESSOR es NULL.  
  
 [Volver al principio](#bkmk_top)  
  
###  <a name="sample-query-2-retrieving-the-regression-formula-for-the-model"></a><a name="bkmk_Query2"></a>Consulta de ejemplo 2: recuperar la fórmula de regresión del modelo  
 La consulta siguiente devuelve el contenido del modelo de minería de datos de un modelo de regresión lineal que se generó utilizando el mismo origen de datos que Targeted Mailing, que se utilizó en el [Basic Data Mining Tutorial](../../tutorials/basic-data-mining-tutorial.md). Este modelo predice los ingresos de los clientes en función de la edad.  
  
 La consulta devuelve el contenido del nodo que contiene la fórmula de regresión. Cada variable y coeficiente están almacenados en una fila independiente de la tabla NODE_DISTRIBUTION anidada. Si desea ver la fórmula de regresión completa, utilice el [visor de árboles de Microsoft](browse-a-model-using-the-microsoft-tree-viewer.md), haga clic en el nodo **(todos)** y abra la **leyenda de minería de datos**.  
  
```  
SELECT FLATTENED NODE_DISTRIBUTION as t  
FROM LR_PredictIncome.CONTENT  
```  
  
> [!NOTE]  
>  Si hace referencia a columnas individuales de la tabla anidada con una consulta como `SELECT <column name> from NODE_DISTRIBUTION`, algunas columnas (como **SUPPORT** o **PROBABILITY**) tienen que escribirse entre corchetes para distinguirlas de las palabras clave reservadas del mismo nombre.  
  
 Resultados esperados:  
  
|T.ATTRIBUTE_NAME|t.ATTRIBUTE_VALUE|t.SUPPORT|t.PROBABILITY|t.VARIANCE|t.VALUETYPE|  
|-----------------------|------------------------|---------------|-------------------|----------------|-----------------|  
|Yearly Income|Missing|0|0.000457142857142857|0|1|  
|Yearly Income|57220.8876687257|17484|0.999542857142857|1041275619.52776|3|  
|Age|471.687717702463|0|0|126.969442359327|7|  
|Age|234.680904692439|0|0|0|8|  
|Age|45.4269617936399|0|0|126.969442359327|9|  
||35793.5477381267|0|0|1012968919.28372|11|  
  
 En la comparación, en la **Leyenda de minería de datos**, la fórmula de regresión aparece como sigue:  
  
 Yearly Income = 57,220.919 + 471.688 * (Age - 45.427)  
  
 Puede ver que, en la **Leyenda de minería de datos**, algunos números se redondean, pero la tabla NODE_DISTRIBUTION y la **Leyenda de minería de datos** contienen básicamente los mismos valores.  
  
 Los valores de la columna VALUETYPE indican qué tipo de información contiene cada fila, lo que resulta útil si los resultados se procesan mediante programación. En la tabla siguiente se muestran los tipos de valores que se generan para una fórmula de regresión lineal.  
  
|VALUETYPE|  
|---------------|  
|1 (ausente)|  
|3 (continuo)|  
|7 (coeficiente)|  
|8 (ganancia de puntuación)|  
|9 (estadísticas)|  
|7 (coeficiente)|  
|8 (ganancia de puntuación)|  
|9 (estadísticas)|  
|11 (intersección)|  
  
 Para más información sobre los tipos de valor y las estadísticas usadas en modelos de regresión, vea [Contenido del modelo de minería de datos para los modelos de regresión lineal &#40;Analysis Services - Minería de datos&#41;](mining-model-content-for-linear-regression-models-analysis-services-data-mining.md).  
  
 [Volver al principio](#bkmk_top)  
  
###  <a name="sample-query-3-returning-only-the-coefficient-for-the-model"></a><a name="bkmk_Query3"></a>Consulta de ejemplo 3: devolver solo el coeficiente para el modelo  
 Utilizando la enumeración VALUETYPE, puede devolver solo el coeficiente para la ecuación de regresión, como se muestra en la consulta siguiente:  
  
```  
SELECT FLATTENED MODEL_NAME,  
    (SELECT ATTRIBUTE_VALUE, VALUETYPE  
     FROM NODE_DISTRIBUTION  
     WHERE VALUETYPE = 11)   
AS t  
FROM LR_PredictIncome.CONTENT  
```  
  
 Esta consulta devuelve dos filas, una del contenido del modelo de minería de datos y la fila de la tabla anidada que contiene el coeficiente. La columna ATTRIBUTE_NAME no está incluida aquí porque siempre está en blanco para el coeficiente.  
  
|MODEL_NAME|t.ATTRIBUTE_VALUE|t.VALUETYPE|  
|-----------------|------------------------|-----------------|  
|LR_PredictIncome|||  
|LR_PredictIncome|35793.5477381267|11|  
  
 [Volver al principio](#bkmk_top)  
  
## <a name="making-predictions-from-a-linear-regression-model"></a>Realizar predicciones a partir de un modelo de regresión lineal  
 Puede generar consultas de predicción en modelos de regresión lineal utilizando la pestaña Predicción de modelo de minería de datos del Diseñador de minería de datos. El generador de consultas de predicción está disponible en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] y [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
> [!NOTE]  
>  También puede crear consultas en modelos de regresión con los Complementos de minería de datos de [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] para Excel o los Complementos de minería de datos de [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] para Excel. Aunque los Complementos de minería de datos para Excel no crean modelos de regresión, puede examinar y consultar cualquier modelo de minería de datos que esté almacenado en una instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
 [Volver al principio](#bkmk_top)  
  
###  <a name="sample-query-4-predicting-income-using-a-singleton-query"></a><a name="bkmk_Query4"></a>Consulta de ejemplo 4: predecir los ingresos utilizando una consulta singleton  
 La manera más fácil de crear una sola consulta en un modelo de regresión es usar el cuadro de diálogo **Entrada de consulta singleton** . Por ejemplo, puede generar la consulta DMX siguiente seleccionando el modelo de regresión adecuado, eligiendo **consulta singleton**y escribiendo `20` como el valor de **Age**.  
  
```  
SELECT [LR_PredictIncome].[Yearly Income]  
From   [LR_PredictIncome]  
NATURAL PREDICTION JOIN  
(SELECT 20 AS [Age]) AS t  
```  
  
 Resultados del ejemplo:  
  
|Yearly Income|  
|-------------------|  
|45227.302092176|  
  
 [Volver al principio](#bkmk_top)  
  
###  <a name="sample-query-5-using-prediction-functions-with-a-regression-model"></a><a name="bkmk_Query5"></a>Consulta de ejemplo 5: usar funciones de predicción con un modelo de regresión  
 Puede utilizar muchas de las funciones de predicción estándar con modelos de regresión lineal. En el ejemplo siguiente se muestra cómo agregar algunas estadísticas descriptivas a los resultados de las consultas de predicción. A partir de estos resultados, puede que hay una desviación considerable de la media para este modelo.  
  
```  
SELECT  
  ([LR_PredictIncome].[Yearly Income]) as [PredIncome],  
  (PredictStdev([LR_PredictIncome].[Yearly Income])) as [StDev1]  
From  
  [LR_PredictIncome]  
NATURAL PREDICTION JOIN  
(SELECT 20 AS [Age]) AS t  
```  
  
 Resultados del ejemplo:  
  
|Yearly Income|StDev1|  
|-------------------|------------|  
|45227.302092176|31827.1726561396|  
  
 [Volver al principio](#bkmk_top)  
  
## <a name="list-of-prediction-functions"></a>Lista de funciones de predicción  
 Todos los algoritmos de [!INCLUDE[msCoName](../../includes/msconame-md.md)] son compatibles con un conjunto común de funciones. No obstante, el algoritmo de regresión lineal de [!INCLUDE[msCoName](../../includes/msconame-md.md)] admite las funciones adicionales que se enumeran en la siguiente tabla.  
  
|||  
|-|-|  
|función de predicción|Uso|  
|[IsDescendant &#40;DMX&#41;](/sql/dmx/isdescendant-dmx)|Determina si un nodo es un elemento secundario de otro nodo del modelo.|  
|[IsInNode &#40;DMX&#41;](/sql/dmx/isinnode-dmx)|Indica si el nodo especificado contiene el caso actual.|  
|[PredictHistogram &#40;DMX&#41;](/sql/dmx/predicthistogram-dmx)|Devuelve un valor o un conjunto de valores predichos para una columna especificada.|  
|[PredictNodeId &#40;DMX&#41;](/sql/dmx/predictnodeid-dmx)|Devuelve el Node_ID de cada caso.|  
|[PredictStdev &#40;DMX&#41;](/sql/dmx/predictstdev-dmx)|Devuelve la desviación estándar del valor predicho.|  
|[PredictSupport &#40;DMX&#41;](/sql/dmx/predictsupport-dmx)|Devuelve el valor de soporte de un estado especificado.|  
|[PredictVariance &#40;DMX&#41;](/sql/dmx/predictvariance-dmx)|Devuelve la varianza de una columna especificada.|  
  
 Para obtener una lista de las funciones que son comunes a todos los algoritmos de [!INCLUDE[msCoName](../../includes/msconame-md.md)], vea [Algoritmos de minería de datos &#40;Analysis Services: Minería de datos&#41;](data-mining-algorithms-analysis-services-data-mining.md). Para más información sobre cómo usar estas funciones, vea [Referencia de funciones de Extensiones de minería de datos &#40;DMX&#41;](/sql/dmx/data-mining-extensions-dmx-function-reference).  
  
## <a name="see-also"></a>Consulte también  
 [Algoritmo de regresión lineal de Microsoft](microsoft-linear-regression-algorithm.md)   
 [Consultas de minería de datos](data-mining-queries.md)   
 [Referencia técnica del algoritmo de regresión lineal de Microsoft](microsoft-linear-regression-algorithm-technical-reference.md)   
 [Contenido del modelo de minería de datos para los modelos de regresión lineal &#40;Analysis Services - Minería de datos&#41;](mining-model-content-for-linear-regression-models-analysis-services-data-mining.md)  
  
  
