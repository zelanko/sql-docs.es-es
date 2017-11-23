---
title: PredictTimeSeries (DMX) | Documentos de Microsoft
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
f1_keywords: PredictTimeSeries
dev_langs: DMX
helpviewer_keywords:
- time series algorithms [Analysis Services]
- time series [Analysis Services]
- EXTEND_MODEL_CASES parameter
- REPLACE_MODEL_CASES parameter
- PredictTimeSeries function
ms.assetid: 85c596be-a7f4-499b-8d36-7e67c2647b6c
caps.latest.revision: "56"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: eba719cb9cc1463b83e6e8aeda8b489d05fba53a
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/20/2017
---
# <a name="predicttimeseries-dmx"></a>PredictTimeSeries (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Devuelve valores futuros de predicción para datos de series temporales. Los datos de series temporales son continuos y pueden almacenarse en una tabla anidada o en una tabla de casos. El **PredictTimeSeries** función siempre devuelve una tabla anidada.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
PredictTimeSeries(<table column reference>)  
PredictTimeSeries(<table column reference>, n)  
PredictTimeSeries(<table column reference>, n-start, n-end)  
PredictTimeSeries(<scalar column reference>)  
PredictTimeSeries(<scalar column reference>, n)  
PredictTimeSeries(<scalar column reference>, n-start, n-end)  
PredictTimeSeries(<table column reference>, n, REPLACE_MODEL_CASES | EXTEND_MODEL_CASES) PREDICTION JOIN <source query>  
PredictTimeSeries(<table column reference>, n-start, n-end, REPLACE_MODEL_CASES | EXTEND_MODEL_CASES) PREDICTION JOIN <source query>  
PredictTimeSeries(<scalar column reference>, n, REPLACE_MODEL_CASES | EXTEND_MODEL_CASES) PREDICTION JOIN <source query>  
PredictTimeSeries(<scalar column reference>, n-start, n-end, REPLACE_MODEL_CASES | EXTEND_MODEL_CASES) PREDICTION JOIN <source query>  
```  
  
## <a name="arguments"></a>Argumentos  
 *\<referencia de columna de la tabla >*,  *\<referencia de columna escalar >*  
 Especifica el nombre de la columna que se va a predecir. La columna puede contener datos escalares o tabulares.  
  
 *n*  
 Especifica el número de pasos siguientes que hay que predecir. Si no se especifica un valor para  *n* , el valor predeterminado es 1.  
  
 *n*no puede ser 0. La función devuelve un error si no realiza al menos una predicción.  
  
 *inicio de n, n-end*  
 Especifica un intervalo de pasos de serie temporal.  
  
 *n-start* debe ser un número entero y no puede ser 0.  
  
 *n-end* debe ser un entero mayor que *n-start*.  
  
 *\<consulta de origen >*  
 Define los datos externos que se utilizan para realizar las predicciones.  
  
 REPLACE_MODEL_CASES | EXTEND_MODEL_CASES  
 Indica cómo administrar los nuevos datos.  
  
 REPLACE_MODEL_CASES especifica que los datos del modelo se deberían reemplazar con datos nuevos. Sin embargo, las predicciones están basadas en los patrones del modelo de minería de datos existente.  
  
 EXTEND_MODEL_CASES especifica que los datos nuevos se deberían agregar al conjunto de datos de entrenamiento originales. Las predicciones futuras solo se realizan en el conjunto de datos compuesto una vez agotados los nuevos datos.  
  
 Estos argumentos solo se pueden utilizar cuando se agregan datos nuevos mediante una instrucción PREDICTION JOIN. Si usa una consulta PREDICTION JOIN y no especifica un argumento, el valor predeterminado es EXTEND_MODEL_CASES.  
  
## <a name="return-type"></a>Tipo devuelto  
 A \< *expresión de tabla*>.  
  
## <a name="remarks"></a>Comentarios  
 El algoritmo de serie temporal [!INCLUDE[msCoName](../includes/msconame-md.md)] no admite la predicción histórica cuando se utiliza la instrucción PREDICTION JOIN para agregar datos.  
  
 En una instrucción PREDICTION JOIN, el proceso de predicción siempre se inicia en el estadio temporal inmediatamente posterior a la finalización de la serie de entrenamiento original. Esto es cierto incluso si se agregan datos nuevos. Por lo tanto, la  *n*  parámetro y *n-start* valores de parámetro deben ser un entero mayor que 0.  
  
> [!NOTE]  
>  La longitud de los datos nuevos no afecta al punto inicial para la predicción. Por ello, si desea agregar datos nuevos y también realizar predicciones nuevas, asegúrese de que establece el punto de inicio de la predicción en un valor mayor que la longitud de los datos nuevos o que extiende el punto final de la predicción según la longitud de los datos nuevos.  
  
## <a name="examples"></a>Ejemplos  
 Los ejemplos siguientes muestran cómo realizar predicciones basadas en un modelo de serie temporal existente:  
  
-   El primer ejemplo muestra cómo realizar un número de predicciones especificado basándose en el modelo actual.  
  
-   En el segundo ejemplo se muestra cómo utilizar el parámetro REPLACE_MODEL_CASES para aplicar los patrones en el modelo especificado a un nuevo conjunto de datos.  
  
-   En el tercer ejemplo se muestra cómo utilizar el parámetro EXTEND_MODEL_CASES para actualizar un modelo de minería de datos con datos nuevos.  
  
 Para más información sobre cómo trabajar con modelos de serie temporal, vea el tutorial de minería de datos, [lección 2: creación de un escenario de previsión &#40; Tutorial intermedio de minería de datos &#41;](http://msdn.microsoft.com/library/9a988156-c900-4c22-97fa-f6b0c1aea9e2) y [Tutorial de DMX de predicción de Series temporales](http://msdn.microsoft.com/library/38ea7c03-4754-4e71-896a-f68cc2c98ce2).  
  
> [!NOTE]  
>  Podría obtener resultados diferentes en un modelo; los resultados de los ejemplos siguientes solo se proporcionan para mostrar el formato del resultado.  
  
### <a name="example-1-predicting-a-number-of-time-slices"></a>Ejemplo 1: predecir un número de intervalos de tiempo  
 En el ejemplo siguiente se usa el **PredictTimeSeries** función para devolver una predicción para los siguientes tres estadios temporales y restringe los resultados a la serie M200 de las regiones de Europa y Pacífico. En este modelo determinado, el atributo de predicción es Quantity, por lo que debe usar `[Quantity]` como el primer argumento a la función PredictTimeSeries.  
  
```  
SELECT FLATTENED  
    [Forecasting].[Model Region],  
    PredictTimeSeries([Forecasting].[Quantity],3)AS t   
FROM  
    [Forecasting]  
WHERE [Model Region] = 'M200 Europe'  
OR [Model Region] = 'M200 Pacific'  
```  
  
 Resultados esperados:  
  
|Model Region|t.$TIME|t.Quantity|  
|------------------|-------------|----------------|  
|M200 Europe|7/25/2008 12:00:00 AM|121|  
|M200 Europe|8/25/2008 12:00:00 AM|142|  
|M200 Europe|9/25/2008 12:00:00 AM|152|  
|M200 Pacific|7/25/2008 12:00:00 AM|46|  
|M200 Pacific|8/25/2008 12:00:00 AM|44|  
|M200 Pacific|9/25/2008 12:00:00 AM|42|  
  
 En este ejemplo, la palabra clave FLATTENED se ha utilizado para hacer que los resultados sean más legibles.  Si no utiliza la palabra clave FLATTENED y en su lugar devuelve un conjunto de filas jerárquico, esta consulta devuelve dos columnas. La primera columna contiene el valor para [ModelRegion] y la segunda contiene una tabla anidada con dos columnas: $TIME, que muestra los intervalos de tiempo que se predicen, y Quantity, que contiene los valores predichos.  
  
### <a name="example-2-adding-new-data-and-using-replacemodelcases"></a>Ejemplo 2: agregar datos nuevos y utilizar REPLACE_MODEL_CASES  
 Suponga que encuentra que los datos eran incorrectos para una región determinada y desea utilizar los patrones en el modelo, pero ajustar las predicciones para que coincidan con los datos nuevos. O bien, podría encontrar que otra región tiene tendencias más confiables y desea aplicar el modelo más confiable a los datos de una región diferente.  
  
 En tales escenarios, puede utilizar el parámetro REPLACE_MODEL_CASES y especificar un conjunto de datos nuevos para utilizar como datos históricos. De ese modo, las proyecciones se basarán en los patrones del modelo especificado, pero continuarán sin problemas desde el fin de los datos nuevos. Para obtener un tutorial completo de este escenario, vea [predicciones de serie temporal avanzadas &#40; Tutorial intermedio de minería de datos &#41;](http://msdn.microsoft.com/library/b614ebdb-07ca-44af-a0ff-893364bd4b71).  
  
 La consulta PREDICTION JOIN siguiente muestra la sintaxis para reemplazar los datos y realizar nuevas predicciones. Para los datos sustitutos, el ejemplo recupera el valor de las columnas Amount y Quantity, y multiplica cada uno por dos:  
  
```  
SELECT [Forecasting].[Model Region],  
    PredictTimeSeries([Forecasting].[Quantity], 3, REPLACE_MODEL_CASES)   
FROM  
    [Forecasting]  
PREDICTION JOIN  
  OPENQUERY([Adventure Works DW Multidimensional 2012],  
    'SELECT [ModelRegion],   
    ([Quantity] * 2) as Quantity,  
    ([Amount] * 2) as Amount,  
      [ReportingDate]  
    FROM [dbo].vTimeSeries  
    WHERE ModelRegion = N''M200 Pacific''  
    ') AS t  
ON  
  [Forecasting].[Model Region] = t.[ Model Region] AND  
[Forecasting].[Reporting Date] = t.[ReportingDate] AND  
[Forecasting].[Quantity] = t.[Quantity] AND  
[Forecasting].[Amount] = t.[Amount]  
```  
  
 Las tablas siguientes comparan los resultados de predicción.  
  
 Predicciones originales:  
  
||||  
|-|-|-|  
|M200 Pacific|7/25/2008 12:00:00 AM|46|  
|M200 Pacific|8/25/2008 12:00:00 AM|44|  
|M200 Pacific|9/25/2008 12:00:00 AM|42|  
  
 Predicciones actualizadas:  
  
||||  
|-|-|-|  
|M200 Pacific|7/25/2008 12:00:00 AM|91|  
|M200 Pacific|8/25/2008 12:00:00 AM|89|  
|M200 Pacific|9/25/2008 12:00:00 AM|84|  
  
### <a name="example-3-adding-new-data-and-using-extendmodelcases"></a>Ejemplo 3: agregar datos nuevos y utilizar EXTEND_MODEL_CASES  
 Ejemplo 3 muestra el uso de la *EXTEND_MODEL_CASES* opción para proporcionar nuevos datos, que se agregan al final de una serie de datos ya existente. En lugar de reemplazar los datos existentes, se agregan los datos nuevos al modelo.  
  
 En el ejemplo siguiente, los datos nuevos se proporcionan en la instrucción SELECT que sigue a NATURAL PREDICTION JOIN. Puede proporcionar varias filas de una nueva entrada con esta sintaxis, pero cada fila de entrada nueva debe tener una marca de tiempo única:  
  
```  
SELECT [Model Region],  
    PredictTimeSeries([Forecasting].[Quantity], 5, EXTEND_MODEL_CASES)   
FROM  
    [Forecasting]  
NATURAL PREDICTION JOIN  
    (SELECT  
        1 as [Reporting Date],  
        10 as [Quantity],  
        'M200 Europe' AS [Model Region]  
    UNION SELECT   
        2 as [Reporting Date],  
        15 as [Quantity],  
        'M200 Europe' AS [Model Region]  
) AS T  
WHERE ([Model Region] = 'M200 Europe'  
 OR [Model Region] = 'M200 Pacific')  
```  
  
 Dado que la consulta utiliza la *EXTEND_MODEL_CASES* opción [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] realiza las siguientes acciones para sus predicciones:  
  
-   Aumenta el tamaño total de los casos de entrenamiento agregando al modelo los dos meses de datos nuevos.  
  
-   Inicia las predicciones al final de los datos de casos anteriores. Por consiguiente, las primeras dos predicciones representan los datos nuevos de ventas reales recién agregados al modelo.  
  
-   Devuelve las predicciones nuevas para los tres intervalos de tiempo restantes basándose en el modelo recientemente ampliado.  
  
 En la tabla siguiente se muestran los resultados de la consulta del ejemplo 2. Observe que los primeros dos valores devueltos para M200 Europe son exactamente iguales que los nuevos valores que proporcionó. Este comportamiento es así por diseño; si desea iniciar las predicciones después del fin de los datos nuevos, debe especificar un paso de inicio y finalización. Para obtener un ejemplo de cómo hacerlo, consulte [lección 5: Extender el modelo de serie temporal](http://msdn.microsoft.com/library/7aad4946-c903-4e25-88b9-b087c20cb67d).  
  
 También, observe que no proporcionó los datos nuevos para la región del Pacífico. Por consiguiente, [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] devuelve las predicciones nuevas para los cinco intervalos de tiempo.  
  
 Cantidad: M200 Europe. EXTEND_MODEL_CASES:  
  
|$TIME|Cantidad|  
|-----------|--------------|  
|7/25/2008 0:00|10|  
|8/25/2008 0:00|15|  
|9/25/2008 0:00|72|  
|10/25/2008 0:00|69|  
|11/25/2008 0:00|68|  
  
 Cantidad: M200 Pacífico. EXTEND_MODEL_CASES:  
  
|$TIME|Cantidad|  
|-----------|--------------|  
|7/25/2008 0:00|46|  
|8/25/2008 0:00|44|  
|9/25/2008 0:00|42|  
|10/25/2008 0:00|42|  
|11/25/2008 0:00|38|  
  
## <a name="example-4-returning-statistics-in-a-time-series-prediction"></a>Ejemplo 4: devolver estadísticas en una predicción de serie temporal  
 El **PredictTimeSeries** función no admite *INCLUDE_STATISTICS* como un parámetro. Sin embargo, se puede utilizar la consulta siguiente para devolver las estadísticas de predicción para una consulta de serie temporal. Este enfoque también se puede utilizar con modelos que tienen columnas de tabla anidadas.  
  
 En este modelo determinado, el atributo de predicción es Quantity, por lo que debe usar `[Quantity]` como el primer argumento a la función PredictTimeSeries. Si el modelo usa un atributo de predicción diferente, puede sustituir un nombre de columna distinto.  
  
```  
SELECT FLATTENED [Model Region],  
(SELECT   
     $Time,  
     [Quantity] as [PREDICTION],   
     PredictVariance([Quantity]) AS [VARIANCE],  
     PredictStdev([Quantity]) AS [STDEV]  
FROM  
      PredictTimeSeries([Quantity], 3) AS t  
) AS t  
FROM Forecasting  
WHERE [Model Region] = 'M200 Europe'  
OR [Model Region] = 'M200 North America'  
```  
  
 Resultados del ejemplo:  
  
|Model Region|t.$TIME|t.PREDICTION|t.VARIANCE|t.STDEV|  
|------------------|-------------|------------------|----------------|-------------|  
|M200 Europe|7/25/2008 12:00:00 AM|121|11.6050581415597|3.40661975300439|  
|M200 Europe|8/25/2008 12:00:00 AM|142|10.678201866621|3.26775180615374|  
|M200 Europe|9/25/2008 12:00:00 AM|152|9.86897842568614|3.14149302493037|  
|M200 North America|7/25/2008 12:00:00 AM|163|1.20434529288162|1.20434529288162|  
|M200 North America|8/25/2008 12:00:00 AM|178|1.65031343900634|1.65031343900634|  
|M200 North America|9/25/2008 12:00:00 AM|156|1.68969399185442|1.68969399185442|  
  
> [!NOTE]  
>  La palabra clave FLATTENED se usó en este ejemplo para hacer que los resultados sean más fáciles de presentar en una tabla; sin embargo, si su proveedor admite conjuntos de filas jerárquicos, puede omitirla. Si omite la palabra clave FLATTENED, la consulta devuelve dos columnas: la primera contiene el valor que identifica la serie de datos `[Model Region]` y la segunda contiene la tabla anidada de estadísticas.  
  
## <a name="see-also"></a>Vea también  
 [Extensiones de minería de datos &#40; DMX &#41; Referencia de funciones](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Ejemplos de consultas de modelo de serie temporal](../analysis-services/data-mining/time-series-model-query-examples.md)   
 [Predecir &#40; DMX &#41;](../dmx/predict-dmx.md)  
  
  
