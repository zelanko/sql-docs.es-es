---
title: Ejemplos de consultas de modelos de serie temporal | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- time series algorithms [Analysis Services]
- MISSING_VALUE_SUBSTITUTION
- time series [Analysis Services]
- predictions [Analysis Services], time series
- EXTEND_MODEL_CASES parameter
- REPLACE_MODEL_CASES parameter
- prediction queries [DMX]
- PREDICTION_SMOOTHING
- content queries [DMX]
ms.assetid: 9a1c527e-2997-493b-ad6a-aaa71260b018
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 1d7451c82261e23c75b748d4b1cde473191b7749
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "66082749"
---
# <a name="time-series-model-query-examples"></a>Ejemplos de consultas de modelos de serie temporal
  Cuando se crea una consulta en un modelo de minería de datos, puede tratarse de una consulta de contenido, que proporciona detalles sobre las reglas y los conjuntos de elementos detectados durante el análisis, o una consulta de predicción, que usa las asociaciones detectadas en los datos para realizar predicciones. Por ejemplo, una consulta de contenido para un modelo de serie temporal podría proporcionar detalles adicionales sobre las estructuras periódicas que se detectaron, mientras que una consulta de predicción podría ofrecer predicciones para los intervalos de tiempo 5 a 10 siguientes. También se pueden recuperar metadatos sobre el modelo mediante una consulta.  
  
 En esta sección se explica cómo crear ambos tipos de consultas en modelos basados en el algoritmo de serie temporal de Microsoft.  
  
 **Consultas de contenido**  
  
 [Recuperar las sugerencias de periodicidad para el modelo](#bkmk_Query1)  
  
 [Recuperar la ecuación para un modelo ARIMA](#bkmk_Query2)  
  
 [Recuperar la ecuación para un modelo ARTxp](#bkmk_Query3)  
  
 **Consultas de predicción**  
  
 [Entender cuándo reemplazar y cuándo ampliar los datos de serie temporal](#bkmk_ReplaceExtend)  
  
 [Realización de predicciones con EXTEND_MODEL_CASES](#bkmk_EXTEND)  
  
 [Realizar predicciones con REPLACE_MODEL_CASES](#bkmk_REPLACE)  
  
 [Sustitución de valores ausentes en modelos de serie temporal](#bkmk_MissingValues)  
  
## <a name="getting-information-about-a-time-series-model"></a>Obtener información sobre un modelo de serie temporal  
 Una consulta de contenido del modelo puede proporcionar información básica sobre el modelo, como los parámetros que se utilizaron cuando se creó o el momento en que se procesó por última vez. En el ejemplo siguiente se muestra la sintaxis básica para consultar el contenido del modelo utilizando los conjuntos de filas de esquema de minería de datos.  
  
###  <a name="sample-query-1-retrieving-periodicity-hints-for-the-model"></a><a name="bkmk_Query1"></a> Ejemplo de consulta 1: Recuperar las sugerencias de periodicidad para el modelo  
 Puede recuperar las periodicidades que se encontraron dentro de la serie temporal consultando el árbol ARIMA o el árbol ARTXP. Sin embargo, las periodicidades en el modelo completado podrían no ser iguales que los segmentos de tiempo que especificó como sugerencias cuando creó el modelo. Para recuperar las sugerencias que se proporcionaron como parámetros cuando creó el modelo, puede consultar el conjunto de filas de esquema de contenido del modelo de minería de datos utilizando la instrucción DMX siguiente:  
  
```  
SELECT MINING_PARAMETERS   
FROM $system.DMSCHEMA_MINING_MODELS  
WHERE MODEL_NAME = '<model name>'  
```  
  
 Resultados parciales:  
  
|MINING_PARAMETERS|  
|------------------------|  
|COMPLEXITY_PENALTY = 0.1, MINIMUM_SUPPORT = 10, PERIODICITY_HINT ={1,3},....|  
  
 La sugerencia de periodicidad predeterminada es {1} y aparece en todos los modelos; este modelo de ejemplo se creó con una sugerencia adicional que podría no estar presente en el modelo final.  
  
> [!NOTE]  
>  Los resultados se han truncado aquí para facilitar la lectura.  
  
###  <a name="sample-query-2-retrieving-the-equation-for-an-arima-model"></a><a name="bkmk_Query2"></a> Ejemplo de consulta 2: Recuperar la ecuación para un modelo ARIMA  
 Puede recuperar la ecuación para un modelo ARIMA consultando cualquier nodo en un árbol individual. Recuerde que cada árbol dentro de un modelo ARIMA representa una periodicidad diferente y, si hay varias series de datos, cada una tendrá su propio conjunto de árboles de periodicidad. Por consiguiente, para recuperar la ecuación de una serie de datos concreta debe identificar primero el árbol.  
  
 Por ejemplo, el prefijo TA le indica que el nodo forma parte de un árbol ARIMA, mientras que el prefijo TS se utiliza para los árboles ARTXP. Puede buscar todos los árboles de raíz de ARIMA consultando los nodos en el contenido del modelo con el valor 27 en NODE_TYPE. También puede utilizar el valor de ATTRIBUTE_NAME para buscar el nodo raíz ARIMA para una serie de datos determinada. Este ejemplo de consulta busca los nodos ARIMA que representan las cantidades vendidas del modelo R250 en la región de Europa.  
  
```  
SELECT NODE_UNIQUE_NAME  
FROM Forecasting.CONTENT  
WHERE ATTRIBUTE_NAME = 'R250 Europe: Quantity"  
AND NODE_TYPE = 27  
```  
  
 Utilizando este identificador de nodo, puede recuperar los detalles de la ecuación ARIMA para este árbol. La instrucción DMX siguiente recupera la forma abreviada de la ecuación ARIMA para la serie de datos. También recupera el corte de la tabla anidada, NODE_DISTRIBUTION. En este ejemplo, la ecuación se obtiene haciendo referencia al identificador único de nodo TA00000007. Sin embargo, puede que tenga que utilizar un identificador de nodo diferente y puede obtener resultados ligeramente diferentes en su modelo.  
  
```  
SELECT FLATTENED NODE_CAPTION as [Short equation],   
(SELECT ATTRIBUTE_NAME, ATTRIBUTE_VALUE   
FROM NODE_DISTRIBUTION) as t  
FROM Forecasting.CONTENT  
WHERE NODE_NAME = 'TA00000007'  
```  
  
 Resultados de ejemplo:  
  
|Ecuación corta|T.ATTRIBUTE_NAME|t.ATTRIBUTE_VALUE|  
|--------------------|-----------------------|------------------------|  
|ARIMA (2,0,7)x(1,0,2)(12)|R250 Europa:Quantity(Intercept)|15,24....|  
|ARIMA (2,0,7)x(1,0,2)(12)|R250 Europa:Quantity(Periodicity)|1|  
|ARIMA (2,0,7)x(1,0,2)(12)|R250 Europa:Quantity(Periodicity)|12|  
  
 Para obtener más información sobre cómo interpretar estos datos, vea [Contenido del modelo de minería de datos para los modelos de serie temporal &#40;Analysis Services - Minería de datos&#41;](mining-model-content-for-time-series-models-analysis-services-data-mining.md).  
  
###  <a name="sample-query-3-retrieving-the-equation-for-an-artxp-model"></a><a name="bkmk_Query3"></a>Consulta de ejemplo 3: recuperar la ecuación para un modelo ARTXP  
 Para un modelo ARTXP, se almacena información diferente en cada nivel del árbol. Para obtener más información sobre la estructura de un modelo ARTXP y sobre cómo interpretar la información en la ecuación, vea [Contenido del modelo de minería de datos para los modelos de serie temporal &#40;Analysis Services - Minería de datos&#41;](mining-model-content-for-time-series-models-analysis-services-data-mining.md).  
  
 La instrucción DMX siguiente recupera información de una parte del árbol ARTXP que representa la cantidad de ventas del modelo R250 en Europa.  
  
> [!NOTE]  
>  El nombre de la columna de tabla anidada, VARIANCE, debe ir entre corchetes para distinguirla de una palabra clave reservada que tiene la misma denominación. Las columnas de tabla anidada, PROBABILITY y SUPPORT, no se incluyen porque están en blanco en la mayoría de los casos.  
  
```  
SELECT NODE_CAPTION as [Split information],   
(SELECT ATTRIBUTE_NAME, ATTRIBUTE_VALUE,  
   [VARIANCE]  
   FROM NODE_DISTRIBUTION) AS t  
FROM Forecasting.CONTENT  
WHERE NODE_ATTRIBUTE_NAME = 'R250 Europe:Quantity'  
AND NODE_TYPE = 15  
```  
  
 Para obtener más información sobre cómo interpretar estos datos, vea [Contenido del modelo de minería de datos para los modelos de serie temporal &#40;Analysis Services - Minería de datos&#41;](mining-model-content-for-time-series-models-analysis-services-data-mining.md).  
  
## <a name="creating-predictions-on-a-time-series-model"></a>Crear las predicciones en un modelo de serie temporal  
 A partir de [!INCLUDE[ssEnterpriseEd10](../../includes/ssenterpriseed10-md.md)], es posible agregar nuevos datos a un modelo de serie temporal e incorporar automáticamente los nuevos datos en el modelo. Los nuevos datos se agregan a un modelo de minería de datos de serie temporal de una de estas dos maneras:  
  
-   Utilice una instrucción `PREDICTION JOIN` para unir los datos de un origen externo a los datos de aprendizaje.  
  
-   Usando una consulta de predicción singleton para proporcionar los datos segmento a segmento. Para obtener información sobre cómo crear una consulta de predicción singleton, vea [interfaces de consulta de minería de datos](data-mining-query-tools.md).  
  
###  <a name="understanding-the-behavior-of-replace-and-extend-operations"></a><a name="bkmk_ReplaceExtend"></a> Descripción del comportamiento de las operaciones Reemplazar y Ampliar  
 Al agregar nuevos datos a un modelo de serie temporal, puede especificar si deben ampliar o reemplazar a los datos de aprendizaje:  
  
-   **Ampliar:** cuando se amplía una serie de datos, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] agrega los nuevos datos al final de los datos de aprendizaje. El número de casos de aprendizaje también aumenta.  
  
     La ampliación de los casos del modelo resulta útil para actualizar continuamente el modelo con nuevos datos. Por ejemplo, si desea que el conjunto de aprendizaje crezca con el paso del tiempo, lo único que debe hacer es ampliar el modelo.  
  
     Para ampliar los datos, se crea una instrucción `PREDICTION JOIN` en un modelo de serie temporal, se especifica el origen de los nuevos datos y se usa el argumento `EXTEND_MODEL_CASES`.  
  
-   **Reemplazar:** cuando se reemplazan los datos de una serie de datos, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] mantiene el modelo de aprendizaje, pero usa los nuevos valores de datos para reemplazar algunos o todos los casos de aprendizaje existentes. De esta forma, el tamaño de los datos de aprendizaje nunca cambia, pero los propios casos se reemplazan continuamente con nuevos datos. Si proporciona suficientes datos nuevos, puede reemplazar los datos de aprendizaje con una serie completamente nueva.  
  
     La sustitución de los casos del modelo resulta útil si desear entrenar un modelo en un conjunto de casos y, a continuación, aplicar ese modelo a una serie de datos diferente.  
  
     Para reemplazar los datos, se crea una instrucción `PREDICTION JOIN` en un modelo de serie temporal, se especifica el origen de los nuevos datos y se usa el argumento `REPLACE_MODEL_CASES`.  
  
> [!NOTE]  
>  Si agrega nuevos datos, no puede realizar predicciones históricas.  
  
 Independientemente de si amplía o reemplaza los datos de entrenamiento, las predicciones comienzan siempre en la marca de tiempo que finaliza el conjunto de entrenamiento original. En otras palabras, si los datos nuevos contienen n intervalos de tiempo y se solicitan predicciones para los pasos temporales 1 a n, las predicciones coincidirán con el mismo período que los datos nuevos y no se obtendrán nuevas predicciones.  
  
 Para obtener nuevas predicciones en períodos de tiempo que no se solapen con los nuevos datos, debe iniciar las predicciones en el intervalo de tiempo n+1 o asegurarse de que solicita intervalos de tiempo adicionales.  
  
 Por ejemplo, suponga que el modelo existente incluye datos de seis meses. Desea ampliar este modelo agregando las cifras de ventas de los últimos tres meses. Al mismo tiempo, desea realizar una predicción acerca de los tres meses siguientes. Para obtener solo las nuevas predicciones al agregar los nuevos datos, especifique el punto inicial como el intervalo de tiempo 4 y el punto final como el intervalo de tiempo 7. También puede solicitar seis predicciones en total, pero los intervalos de tiempo para las tres primeras se superpondrían con los nuevos datos recién agregados.  
  
 Para obtener ejemplos de consultas y más información sobre la sintaxis `REPLACE_MODEL_CASES` para `EXTEND_MODEL_CASES`usar y, consulte [PredictTimeSeries &#40;DMX&#41;](/sql/dmx/predicttimeseries-dmx).  
  
###  <a name="making-predictions-with-extend_model_cases"></a><a name="bkmk_EXTEND"></a> Realizar predicciones con EXTEND_MODEL_CASES  
 El comportamiento de la predicción varía en función de si se amplían o se reemplazan los casos del modelo. Al ampliar un modelo, los nuevos datos se asocian al final de la serie y el tamaño del conjunto de aprendizaje aumenta. Sin embargo, los intervalos de tiempo usados en las consultas de predicción siempre se inician al final de la serie original. Por tanto, si agrega tres nuevos puntos de datos y solicita seis predicciones, las tres primeras predicciones devueltas se superponen a los nuevos datos. En este caso, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] devuelve los nuevos puntos de datos reales en lugar de realizar una predicción, hasta que se agoten los nuevos puntos de datos. A continuación, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] realiza predicciones basadas en la serie compuesta.  
  
 Este comportamiento permite agregar nuevos datos y, a continuación, mostrar las cifras de ventas reales en el gráfico de predicción, en lugar de ver proyecciones.  
  
 Por ejemplo, para agregar tres nuevos puntos de datos y realizar tres nuevas predicciones, haría lo siguiente:  
  
-   Cree una instrucción `PREDICTION JOIN` en un modelo de serie temporal y especifique el origen de los nuevos datos de tres meses.  
  
-   Solicite predicciones para seis intervalos de tiempo. Para ello, especifique 6 intervalos de tiempo, donde el punto inicial es el intervalo de tiempo 1 y el punto final es el intervalo de tiempo 7. Esto solo se cumple para EXTEND_MODEL_CASES.  
  
-   Para obtener solo las nuevas predicciones, especifique el punto inicial como el segmento de tiempo 4 y el punto final como el segmento de tiempo 7.  
  
-   Debe usar el argumento `EXTEND_MODEL_CASES`.  
  
     Se devuelven las cifras de ventas reales de los tres primeros intervalos de tiempo y las predicciones basadas en el modelo ampliado de los tres intervalos de tiempo siguientes.  
  
###  <a name="making-predictions-with-replace_model_cases"></a><a name="bkmk_REPLACE"></a>Realización de predicciones con REPLACE_MODEL_CASES  
 Al reemplazar los casos de un modelo, el tamaño del modelo no se modifica, sino que [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] reemplaza los casos individuales del modelo. Esto es útil para predicciones cruzadas y escenarios en los que resulta importante mantener el conjunto de datos de aprendizaje con un tamaño uniforme.  
  
 Por ejemplo, una de sus tiendas no dispone de suficientes datos de ventas. Podría crear un modelo general calculando el promedio de las ventas de todas las tiendas de una región determinada y, a continuación, entrenar un modelo. Posteriormente, para realizar predicciones sobre la tienda con datos de ventas insuficientes, crearía una instrucción `PREDICTION JOIN` para los nuevos datos de ventas únicamente de dicha tienda. Al hacer esto, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] mantiene los patrones derivados del modelo regional, pero reemplaza los casos de aprendizaje existentes con los datos de la tienda individual. Como resultado, los valores de predicción estarán más próximos a las líneas de tendencia de la tienda individual.  
  
 Al usar el argumento `REPLACE_MODEL_CASES`, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] agrega continuamente los nuevos casos al final del conjunto de casos y elimina un número correspondiente del principio del conjunto. Si agrega nuevos datos en un número mayor que el conjunto de aprendizaje original, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] descarta los primeros datos. Si proporciona suficientes valores nuevos, las predicciones se pueden basar en datos completamente nuevos.  
  
 Por ejemplo, supongamos que entrenó el modelo con un conjunto de datos de casos que contenía 1000 filas. A continuación agrega 100 filas de datos nuevos. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] quita las 100 primeras filas del conjunto de entrenamiento y agrega las 100 filas de datos nuevos al final del conjunto, para obtener un total de 1000 filas. Si agrega 1100 filas de nuevos datos, solo se usan las 1000 filas más recientes.  
  
 A continuación se muestra otro ejemplo. Para agregar datos acerca de tres nuevos meses y realizar tres nuevas predicciones, realizaría las siguientes acciones:  
  
-   Cree una instrucción `PREDICTION JOIN` en un modelo de serie temporal y use el argumento `REPLACE_MODEL_CASE`.  
  
-   Especifique el origen de los nuevos datos correspondientes a tres meses. Estos datos pueden proceder de un origen completamente diferente a los datos de aprendizaje originales.  
  
-   Solicite predicciones para seis intervalos de tiempo. Para ello, especifique 6 intervalos de tiempo o especifique el punto inicial como el intervalo de tiempo 1 y el punto final como el intervalo de tiempo 7.  
  
    > [!NOTE]  
    >  A diferencia de `EXTEND_MODEL_CASES`, no puede devolver los mismos valores que agregó como datos de entrada. Los seis valores devueltos son predicciones basadas en el modelo actualizado, que incluye tanto los datos anteriores como los nuevos.  
  
    > [!NOTE]  
    >  Con REPLACE_MODEL_CASES, al comenzar en la marca de tiempo 1, se obtienen predicciones nuevas basadas en los datos nuevos, que reemplazan los datos de entrenamiento antiguos.  
  
 Para obtener ejemplos de consultas y más información sobre la sintaxis `REPLACE_MODEL_CASES` para `EXTEND_MODEL_CASES`usar y, consulte [PredictTimeSeries &#40;DMX&#41;](/sql/dmx/predicttimeseries-dmx).  
  
###  <a name="missing-value-substitution-in-time-series-models"></a><a name="bkmk_MissingValues"></a>Sustitución de valores que faltan en los modelos de serie temporal  
 Al agregar nuevos datos a un modelo de serie temporal con una instrucción `PREDICTION JOIN`, en el nuevo conjunto de datos no puede faltar ningún valor. Si alguna serie está incompleta, el modelo debe proporcionar los valores ausentes mediante un valor NULL, una media numérica, una media numérica concreta o un valor de predicción. Si especifica `EXTEND_MODEL_CASES`, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] reemplaza los valores ausentes con predicciones basadas en el modelo original. Si usa `REPLACE_MODEL_CASES`, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] reemplaza los valores que faltan por el valor que especifique en el parámetro *MISSING_VALUE_SUBSTITUTION* .  
  
## <a name="list-of-prediction-functions"></a>Lista de funciones de predicción  
 Todos los algoritmos de [!INCLUDE[msCoName](../../includes/msconame-md.md)] son compatibles con un conjunto común de funciones. No obstante, el algoritmo de serie temporal de [!INCLUDE[msCoName](../../includes/msconame-md.md)] admite las funciones adicionales que figuran en la siguiente tabla.  
  
|||  
|-|-|  
|función de predicción|Uso|  
|[Lag &#40;DMX&#41;](/sql/dmx/lag-dmx)|Devuelve un número de intervalos de tiempo entre la fecha del caso actual y la última fecha del conjunto de entrenamiento.<br /><br /> Un uso típico de esta función consiste en identificar los recientes escenarios de aprendizaje con el fin de poder recuperar datos detallados sobre los escenarios.|  
|[PredictNodeId &#40;DMX&#41;](/sql/dmx/predictnodeid-dmx)|Devuelve el ID del nodo para la columna predecible especificada.<br /><br /> Un uso típico de esta función consiste en identificar el nodo que generó un determinado valor predicho de forma que se puedan revisar los escenarios asociados al nodo o recuperar la ecuación y otros detalles.|  
|[PredictStdev &#40;DMX&#41;](/sql/dmx/predictstdev-dmx)|Devuelve la desviación estándar de las predicciones de la columna predecible especificada.<br /><br /> Esta función reemplaza el argumento INCLUDE_STATISTICS, que no se admite para los modelos de serie temporal.|  
|[PredictVariance &#40;DMX&#41;](/sql/dmx/predictvariance-dmx)|Devuelve la varianza de las predicciones para la columna predecible especificada.<br /><br /> Esta función reemplaza el argumento INCLUDE_STATISTICS, que no se admite para los modelos de serie temporal.|  
|[PredictTimeSeries &#40;DMX&#41;](/sql/dmx/predicttimeseries-dmx)|Devuelve valores históricos o futuros predichos en una serie temporal.<br /><br /> También puede consultar los modelos de serie temporal usando la función de predicción general, [Predict &#40;DMX&#41;](/sql/dmx/predict-dmx).|  
  
 Para consultar una lista de las funciones comunes a todos los algoritmos de [!INCLUDE[msCoName](../../includes/msconame-md.md)], vea [Funciones de predicción generales &#40;DMX&#41;](/sql/dmx/general-prediction-functions-dmx). Para más información sobre la sintaxis de funciones específicas, vea [Referencia de funciones de Extensiones de minería de datos &#40;DMX&#41;](/sql/dmx/data-mining-extensions-dmx-function-reference).  
  
## <a name="see-also"></a>Consulte también  
 [Consultas de minería de datos](data-mining-queries.md)   
 [Algoritmo de serie temporal de Microsoft](microsoft-time-series-algorithm.md)   
 [Referencia técnica del algoritmo de serie temporal de Microsoft](microsoft-time-series-algorithm-technical-reference.md)   
 [Contenido del modelo de minería de datos para los modelos de serie temporal &#40;Analysis Services - Minería de datos&#41;](mining-model-content-for-time-series-models-analysis-services-data-mining.md)  
  
  
