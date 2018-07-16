---
title: Usar datos de reemplazo (Tutorial intermedio de datos de minería) de predicciones de serie temporal | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: a23a6e1d-1d49-41ea-8314-925dc8e4df5e
caps.latest.revision: 30
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: c170fab7f4f6711e81e07603302839430404aa3b
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37267761"
---
# <a name="time-series-predictions-using-replacement-data-intermediate-data-mining-tutorial"></a>Predicciones de serie temporal que usan datos de reemplazo (Tutorial intermedio de minería de datos)
  En esta tarea, se creará un nuevo modelo basado en datos de ventas mundiales. A continuación, se creará una consulta de predicción que aplica el modelo de ventas mundial a una de las regiones individuales.  
  
## <a name="building-a-general-model"></a>Crear un modelo general  
 Recuerde que el análisis de los resultados del modelo de minería de datos original reveló grandes diferencias entre ciertas regiones y entre las líneas de productos. Por ejemplo, las ventas de Norteamérica fueron buenas para el modelo M200, mientras que las ventas del modelo T1000 no fueron tan bien. Sin embargo, el análisis se complica por el hecho de que alguna serie no tenía muchos datos o que los datos empezaban en otro momento. También faltaban algunos datos.  
  
 ![Serie que predice la cantidad de M200 y T1000](../../2014/tutorials/media/6series-defaultforecasting.gif "serie que predice la cantidad de M200 y T1000")  
  
 Para resolver algunos de los problemas de calidad de los datos, decide combinar los datos de ventas de todo el mundo y usar ese conjunto de tendencias de ventas generales para crear un modelo que se pueda aplicar para predecir las ventas futuras en cualquier región.  
  
 Al crear predicciones, usará el modelo que se genera mediante la formación en los datos de ventas mundiales, pero reemplazará los puntos de datos históricos con los datos de ventas de cada región individual. De este modo, se mantiene la forma de la tendencia, pero los valores previstos están alineados con las cifras de ventas históricas para cada región y modelo.  
  
## <a name="performing-cross-prediction-with-a-time-series-model"></a>Realizar una predicción cruzada con un modelo de serie temporal  
 El proceso de usar datos de una serie para predecir tendencias en otras series se denomina predicción cruzada. Puede usar la predicción cruzada en muchas situaciones: por ejemplo, podría decidir que las ventas de televisiones son adecuadas para predecir la actividad económica general, y aplicar un modelo formado en ventas de televisiones a los datos económicos generales.  
  
 En SQL Server Data Mining, realizar una predicción cruzada utilizando el parámetro REPLACE_MODEL_CASES en los argumentos a la función, [PredictTimeSeries &#40;DMX&#41;](/sql/dmx/predicttimeseries-dmx).  
  
 En la tarea siguiente, aprenderá a usar REPLACE_MODEL_CASES. Usará los datos combinados de las ventas mundiales para crear un modelo y, a continuación, creará una consulta de predicción que asigna el modelo general a los datos de reemplazo.  
  
 Se supone que ya está familiarizado con la manera de generar modelos de minería de datos y, por consiguiente, se han simplificado las instrucciones para generar el modelo.  
  
#### <a name="to-build-a-mining-structure-and-mining-model-using-the-aggregated-data"></a>Para generar una estructura de minería de datos y un modelo de minería de datos utilizando los datos agregados  
  
1.  En **el Explorador de soluciones**, haga clic en **estructuras de minería de datos**y, a continuación, seleccione **nueva estructura de minería de datos** para iniciar el Asistente para minería de datos.  
  
2.  En el Asistente para minería de datos, realice las selecciones siguientes:  
  
    -   Algoritmo: serie temporal de Microsoft  
  
    -   Use el origen de datos que creó anteriormente en esta lección avanzada como origen para el modelo. Consulte [avanzada predicciones de serie temporal &#40;intermedio de Tutorial de minería de datos&#41;](../../2014/tutorials/advanced-time-series-predictions-intermediate-data-mining-tutorial.md).  
  
         Vista del origen de datos: `AllRegions`  
  
    -   Elija las columnas siguientes para la clave de serie y la clave temporal:  
  
         Hora clave: ReportingDate  
  
         Clave: región  
  
    -   Elija las columnas siguientes para `Input` y `Predict`:  
  
         SumQty  
  
         SumAmt  
  
         AvgAmt  
  
         AvgQty  
  
    -   Para **nombre de la estructura de minería de datos**, tipo: `All Regions`  
  
    -   Para **nombre del modelo de minería de datos**, tipo: `All Regions`  
  
3.  Procese la nueva estructura y el nuevo modelo.  
  
#### <a name="to-build-the-prediction-query-and-map-the-replacement-data"></a>Para generar la consulta de predicción y asignar los datos de reemplazo  
  
1.  Si el modelo no está abierto, haga doble clic en la estructura AllRegions y, en el Diseñador de minería de datos, haga clic en el **predicción de modelo de minería de datos** ficha.  
  
2.  En el **Mining Model** panel, el modelo AllRegions ya debería estar seleccionado. Si no está seleccionada, haga clic en **Seleccionar modelo**y, a continuación, seleccione el modelo AllRegions.  
  
3.  En el **Seleccionar tabla (s) de entrada** panel, haga clic en **Seleccionar tabla de casos**.  
  
4.  En el **Seleccionar tabla** cuadro de diálogo, cambie los datos de origen por T1000 Pacific Region y, a continuación, haga clic en **Aceptar**.  
  
5.  Haga clic en la línea de combinación entre el modelo de minería de datos y los datos de entrada y seleccione **modificar conexiones**. Asigne los datos de la vista del origen de datos al modelo de la manera siguiente:  
  
    1.  Compruebe que la columna ReportingDate del modelo de minería de datos se asigna a la columna ReportingDate en los datos de entrada.  
  
    2.  En el **modificar asignación** cuadro de diálogo, en la fila de la columna del modelo correspondiente a AvgQty, haga clic en **columna de tabla** y, a continuación, seleccione T1000 Pacific.Quantity. Haga clic en **Aceptar**.  
  
         Este paso asigna la columna que creó en el modelo para la cantidad promedio que predecía los datos reales de la serie T1000 de la cantidad de ventas.  
  
    3.  No asigne la columna de la región en el modelo a cualquier columna de entrada.  
  
         Puesto que el modelo agregaba los datos de todas las series, no hay ninguna coincidencia de los valores de series como T1000 Pacific y se generará un error cuando se ejecute la consulta de predicción.  
  
6.  Ahora creará la consulta de predicción.  
  
     Primero, agregue una columna a los resultados que genera la etiqueta AllRegions a partir del modelo y las predicciones. De esta manera, sabe que los resultados están basados en el modelo general.  
  
    1.  En la cuadrícula, haga clic en la primera fila vacía en **origen**y, a continuación, seleccione AllRegions modelo de minería de datos.  
  
    2.  Para **campo**, seleccione la región.  
  
    3.  Para **Alias**, tipo **modelo usa**.  
  
7.  A continuación, agregue otra etiqueta a los resultados, de modo que pueda ver para qué serie son las predicciones.  
  
    1.  Haga clic en una fila vacía y en **origen**, seleccione **expresión personalizada**.  
  
    2.  En el **Alias** columna, escriba **ModelRegion**.  
  
    3.  En el **criterios o argumento** columna, escriba `'T1000 Pacific'`.  
  
8.  Ahora va a configurar la función de predicción cruzada.  
  
    1.  Haga clic en una fila vacía y en **origen**, seleccione **función de predicción**.  
  
    2.  En el **campo** columna, seleccione **PredictTimeSeries**.  
  
    3.  Para **Alias**, tipo **valores predichos**.  
  
    4.  Arrastre el campo AvgQty desde el **Mining Model** panel en el **criterios o argumento** columna mediante el uso de la operación de arrastrar y colocar.  
  
    5.  En el **criterios o argumento** columna, después del nombre de campo, escriba el texto siguiente: `,5, REPLACE_MODEL_CASES`  
  
         El texto completo de la **criterios o argumento** cuadro de texto debería ser como sigue: `[AllRegions].[AvgQty],5,REPLACE_MODEL_CASES`  
  
9. Haga clic en **resultados**.  
  
## <a name="creating-the-cross-prediction-query-in-dmx"></a>Crear consultas de predicción cruzada en DMX  
 Quizá ha observado un problema con la predicción cruzada: a saber, que a aplicar el modelo general a una serie de datos diferente, como el modelo de producto T1000 en la región de Norteamérica, debe crear una consulta diferente para cada serie, con el fin de poder asignar cada conjunto de entradas al modelo.  
  
 Sin embargo, en lugar de crear la consulta en el diseñador, puede cambiar a la vista DMX y modificar la instrucción DMX que creó. Por ejemplo, la instrucción DMX siguiente representa la consulta recién creada:  
  
```  
SELECT  
      ([All Regions].[Region]) as [Model Used],  
      ('T-1000 Pacific') as [ModelRegion],  
      (PredictTimeSeries([All Regions].[Avg Qty],5, REPLACE_MODEL_CASES)) as [Predicted Quantity]  
     FROM [All Regions]  
PREDICTION JOIN  
    OPENQUERY([Adventure Works DW2003R2], 'SELECT [ReportingDate] FROM  
      (  
       SELECT  ReportingDate, ModelRegion, Quantity, Amount   
       FROM dbo.vTimeSeries   
       WHERE (ModelRegion = N''T1000 Pacific'')  
       ) as [T1000 Pacific]    ')   
    AS t  
ON   
[All Regions].[Reporting Date] = t.[ReportingDate]   
AND   
[All Regions].[Avg Qty] = t.[Quantity]  
```  
  
 Para aplicar esto a un modelo diferente, basta con modificar la instrucción de consulta para reemplazar la condición de filtro y actualizar las etiquetas asociadas a cada resultado.  
  
 Por ejemplo, si cambia las condiciones de filtro y las etiquetas de las columnas reemplazando 'Pacific' con 'North America', obtendrá las predicciones para el producto T1000 de Norteamérica, según los patrones del modelo general.  
  
## <a name="next-task-in-lesson"></a>Siguiente tarea de la lección  
 [Comparar las predicciones para los modelos de pronóstico &#40;intermedio de Tutorial de minería de datos&#41;](../../2014/tutorials/comparing-predictions-for-forecasting-models-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>Vea también  
 [Ejemplos de consultas de modelo de serie temporal](../../2014/analysis-services/data-mining/time-series-model-query-examples.md)   
 [PredictTimeSeries &#40;DMX&#41;](/sql/dmx/predicttimeseries-dmx)  
  
  
