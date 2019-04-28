---
title: 'Lección 5: Ampliación de la serie temporal de modelo | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 7aad4946-c903-4e25-88b9-b087c20cb67d
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 2716e985897f8115d189d9410b7cdb13fb1af291
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62822107"
---
# <a name="lesson-5-extending-the-time-series-model"></a>Lección 5: Extensión del modelo de serie temporal
  En [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] Enterprise, es posible agregar datos nuevos a un modelo de serie temporal e incorporarlos automáticamente al mismo. Los nuevos datos se agregan a un modelo de minería de datos de serie temporal de una de estas dos maneras:  
  
-   Usando una instrucción PREDICTION JOIN  para unir los datos de un origen externo a los datos de entrenamiento.  
  
-   Usando una consulta de predicción singleton para proporcionar los datos segmento a segmento.  
  
 Por ejemplo, suponga que entrenó el modelo de minería de datos con los datos de ventas existentes hace algunos meses. Al conseguir ventas nuevas, podría desear actualizar las predicciones de ventas para incorporar los datos nuevos. Puede hacer esto en un paso, proporcionando las nuevas cifras de ventas como datos de entrada y generando predicciones nuevas basadas en el conjunto de datos compuesto.  
  
## <a name="making-predictions-with-extendmodelcases"></a>Realizar predicciones con EXTEND_MODEL_CASES  
 A continuación se muestran ejemplos genéricos de una predicción de serie temporal que usa EXTEND_MODEL_CASES. El primer ejemplo permite especificar el número de predicciones a partir del último estadio temporal del modelo original:  
  
```  
SELECT [<model columns>,] PredictTimeSeries(<table column reference>, n, EXTEND_MODEL_CASES)   
FROM <mining model>  
PREDICTION JOIN <source query>  
[WHERE <criteria>]  
```  
  
 El segundo ejemplo permite especificar el estadio temporal donde las predicciones deberían iniciarse y donde deberían finalizar. Esta opción es importante al extender los casos del modelo porque, de forma predeterminada, los estadios temporales que se usan para las consultas de predicción siempre se inician al final de la serie original.  
  
```  
SELECT [<model columns>,] PredictTimeSeries(<table column reference>, n-start, n-end, EXTEND_MODEL_CASES)   
FROM <mining model>  
PREDICTION JOIN <source query>  
[WHERE <criteria>}  
```  
  
 En este tutorial, creará ambos tipos de consultas.  
  
#### <a name="to-create-a-singleton-prediction-query-on-a-time-series-model"></a>Para crear una consulta de predicción singleton en un modelo de serie temporal  
  
1.  En **Explorador de objetos**, haga clic en la instancia de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], apunte a **nueva consulta**y, a continuación, haga clic en **DMX**.  
  
     Se abre el Editor de consultas, que contiene una consulta nueva en blanco.  
  
2.  Copie el ejemplo genérico de la instrucción singleton en la consulta en blanco.  
  
3.  Reemplace lo siguiente:  
  
    ```  
    SELECT [<model columns>,] PredictTimeSeries(<table column reference>, n, EXTEND_MODEL_CASES)   
    ```  
  
     por:  
  
    ```  
    SELECT [Model Region],  
    PredictTimeSeries([Quantity],6, EXTEND_MODEL_CASES) AS PredictQty  
    ```  
  
     La primera línea recupera un valor del modelo que identifica la serie.  
  
     La segunda línea contiene la función de predicción, que obtiene seis predicciones para Quantity. Se asigna un alias, `PredictQty`, a la columna del resultado de la predicción para que los resultados se entiendan más fácilmente.  
  
4.  Reemplace lo siguiente:  
  
    ```  
    FROM <mining model>  
    ```  
  
     por:  
  
    ```  
    FROM [Forecasting_MIXED]  
    ```  
  
5.  Reemplace lo siguiente:  
  
    ```  
    PREDICTION JOIN <source query>  
    ```  
  
     por:  
  
    ```  
    NATURAL PREDICTION JOIN   
    (  
       SELECT 1 AS [Reporting Date],  
       '10' AS [Quantity],  
       'M200 Europe' AS [Model Region]  
       UNION SELECT  
       2 AS [Reporting Date],  
       15 AS [Quantity]),  
       'M200 Europe' AS [Model Region]  
    ) AS t  
    ```  
  
6.  Reemplace lo siguiente:  
  
    ```  
    [WHERE <criteria>]  
    ```  
  
     por:  
  
    ```  
    WHERE [ModelRegion] = 'M200 Europe' OR  
    [ModelRegion] = 'M200 Pacific'  
    ```  
  
     Ahora la apariencia de la instrucción completa debe ser como la siguiente:  
  
    ```  
    SELECT [Model Region],  
    PredictTimeSeries([Quantity],6, EXTEND_MODEL_CASES) AS PredictQty  
    FROM  
       [Forecasting_MIXED]  
    NATURAL PREDICTION JOIN   
       SELECT 1 AS [ReportingDate],  
      '10' AS [Quantity],  
      'M200 Europe' AS [ModelRegion]  
    UNION SELECT  
      2 AS [ReportingDate],  
      15 AS [Quantity]),  
      'M200 Europe' AS [ModelRegion]  
    ) AS t  
    WHERE [ModelRegion] = 'M200 Europe' OR  
    [ModelRegion] = 'M200 Pacific'  
    ```  
  
7.  En el **archivo** menú, haga clic en **guardar DMXQuery1.dmx como**.  
  
8.  En el **Guardar como** cuadro de diálogo, desplácese a la carpeta correspondiente y asigne el nombre `Singleton_TimeSeries_Query.dmx`.  
  
9. En la barra de herramientas, haga clic en el **Execute** botón.  
  
     La consulta devuelve predicciones de la cantidad de ventas de la bicicleta M200 en las regiones de Europa y Pacífico.  
  
## <a name="understanding-prediction-start-with-extendmodelcases"></a>Descripción del inicio de la predicción con EXTEND_MODEL_CASES  
 Ahora que ha creado predicciones basadas en el modelo original, puede comparar con datos nuevos los resultados para ver cómo afecta a las predicciones la actualización de los datos de ventas. Antes, revise el código recién creado y observe lo siguiente:  
  
-   Proporcionó datos nuevos solo para la región de Europa.  
  
-   Proporcionó solo datos nuevos para dos meses.  
  
 La tabla siguiente muestra cómo los valores nuevos proporcionados para M200 en Europa afectan a las predicciones. No proporcionó ningún dato nuevo para el producto M200 en la región de Pacífico, pero esta serie se presenta para poder comparar:  
  
 **Producto y región: M200 Europe**  
  
|||||  
|-|-|-|-|  
|||Modelo existente (`PredictTimeSeries`)|Modelo con datos de ventas actualizados (`PredictTimeSeries` con `EXTEND_MODEL_CASES`)|  
|M200 Europe|7/25/2008 12:00:00 AM|77|10|  
|M200 Europe|8/25/2008 12:00:00 AM|64|15|  
|M200 Europe|9/25/2008 12:00:00 AM|59|72|  
|M200 Europe|10/25/2008 12:00:00 AM|56|69|  
|M200 Europe|11/25/2008 12:00:00 AM|56|68|  
|M200 Europe|12/25/2008 12:00:00 AM|74|89|  
  
 **Producto y región: M200 Pacífico**  
  
|||||  
|-|-|-|-|  
|||Modelo existente (`PredictTimeSeries`)|Modelo con datos de ventas actualizados (`PredictTimeSeries` con `EXTEND_MODEL_CASES`)|  
|M200 Pacific|7/25/2008 12:00:00 AM|41|41|  
|M200 Pacific|8/25/2008 12:00:00 AM|44|44|  
|M200 Pacific|9/25/2008 12:00:00 AM|38|38|  
|M200 Pacific|10/25/2008 12:00:00 AM|41|41|  
|M200 Pacific|11/25/2008 12:00:00 AM|36|36|  
|M200 Pacific|12/25/2008 12:00:00 AM|39|39|  
  
 A raíz de estos resultados, puede observar dos cuestiones:  
  
-   Las primeras dos predicciones para la serie M200 Europe son exactamente iguales que los nuevos datos que proporcionó. Por diseño, Analysis Services devuelve los nuevos datos reales en lugar de realizar una predicción. Eso se debe a que al extender los casos del modelo, los pasos temporales utilizados para las consultas de predicción siempre se inician al final de la serie original. Por tanto, si agrega dos datos nuevos, las dos primeras predicciones devueltas se superponen a los datos nuevos.  
  
-   Una vez agotados todos los nuevos datos, [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] realiza predicciones basadas en el modelo actualizado. Por consiguiente, a partir de septiembre de 2005, puede ver la diferencia entre las predicciones para M200 Europe del modelo original, en la columna de la izquierda, y el modelo que utiliza EXTEND_MODEL_CASES, en la columna de la derecha. Las predicciones son diferentes porque el modelo se ha actualizado con datos nuevos.  
  
## <a name="using-start-and-end-time-steps-to-control-predictions"></a>Usar pasos temporales de inicio y de fin para controlar las predicciones  
 Al extender un modelo, los datos nuevos siempre se asocian al final de la serie. Sin embargo, para la predicción, los intervalos de tiempo usados en las consultas de predicción se inician al final de la serie original. Si únicamente desea obtener las predicciones nuevas al agregar datos nuevos, debe especificar el punto inicial como un número de intervalos de tiempo. Por ejemplo, si va a agregar dos datos nuevos y desea realizar cuatro predicciones nuevas, haría lo siguiente:  
  
-   Cree una instrucción PREDICTION JOIN en un modelo de serie temporal y especifique los datos nuevos correspondientes a dos meses.  
  
-   Solicite predicciones para cuatro intervalos de tiempo, donde el punto inicial es el intervalo de tiempo 3 y el punto final es el intervalo de tiempo 6.  
  
 En otras palabras, si los datos nuevos contienen n intervalos de tiempo y solicita predicciones para los pasos de tiempo 1 a n, las predicciones coincidirán con el mismo período que los nuevos datos. Para obtener nuevas predicciones de un período de tiempo que no cubren los datos, debe iniciar las predicciones en el intervalo de tiempo n+1 tras la nueva serie de datos o asegurarse de que solicita intervalos de tiempo adicionales.  
  
> [!NOTE]  
>  Si agrega nuevos datos, no puede realizar predicciones históricas.  
  
 En el ejemplo siguiente se muestra la instrucción DMX que permite obtener solo las predicciones nuevas para las dos series del ejemplo anterior.  
  
```  
SELECT [Model Region],  
PredictTimeSeries([Quantity],3,6, EXTEND_MODEL_CASES) AS PredictQty  
FROM  
   [Forecasting_MIXED]  
NATURAL PREDICTION JOIN   
   SELECT 1 AS [ReportingDate],  
  '10' AS [Quantity],  
  'M200 Europe' AS [ModelRegion]  
UNION SELECT  
  2 AS [ReportingDate],  
  15 AS [Quantity]),  
  'M200 Europe' AS [ModelRegion]  
) AS t  
WHERE [ModelRegion] = 'M200 Europe'  
```  
  
 Los resultados de la predicción se inician en el intervalo de tiempo 3, que está después de los datos nuevos para 2 meses que proporcionó.  
  
 **Producto y región: M200 Europe**  
  
 Modelo con datos actualizados (PredictTimeSeries con EXTEND_MODEL_CASES)  
  
||||  
|-|-|-|  
|M200 Europe|9/25/2008 12:00:00 AM|72|  
|M200 Europe|10/25/2008 12:00:00 AM|69|  
|M200 Europe|11/25/2008 12:00:00 AM|68|  
|M200 Europe|12/25/2008 12:00:00 AM|89|  
  
## <a name="making-predictions-with-replacemodelcases"></a>Realizar predicciones con REPLACE_MODEL_CASES  
 La sustitución de los casos del modelo resulta útil si desear entrenar un modelo en un conjunto de casos y, a continuación, aplicar ese modelo a una serie de datos diferente. Un tutorial detallado sobre este escenario se presenta en [lección 2: Generar un escenario de pronóstico &#40;intermedio de Tutorial de minería de datos&#41;](../../2014/tutorials/lesson-2-building-a-forecasting-scenario-intermediate-data-mining-tutorial.md).  
  
## <a name="see-also"></a>Vea también  
 [Ejemplos de consultas de modelos de serie temporal](../../2014/analysis-services/data-mining/time-series-model-query-examples.md)   
 [PredictTimeSeries &#40;DMX&#41;](/sql/dmx/predicttimeseries-dmx)  
  
  
