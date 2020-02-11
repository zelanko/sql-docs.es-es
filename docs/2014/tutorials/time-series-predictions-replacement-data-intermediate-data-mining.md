---
title: Predicciones de serie temporal que usan datos de reemplazo (tutorial intermedio de minería de datos) | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: a23a6e1d-1d49-41ea-8314-925dc8e4df5e
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: c96b70775105ea9446810ac3b064ae7cb07d4337
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "63312879"
---
# <a name="time-series-predictions-using-replacement-data-intermediate-data-mining-tutorial"></a>Predicciones de serie temporal que usan datos de reemplazo (Tutorial intermedio de minería de datos)
  En esta tarea, se creará un nuevo modelo basado en datos de ventas mundiales. A continuación, se creará una consulta de predicción que aplica el modelo de ventas mundial a una de las regiones individuales.  
  
## <a name="building-a-general-model"></a>Crear un modelo general  
 Recuerde que el análisis de los resultados del modelo de minería de datos original reveló grandes diferencias entre ciertas regiones y entre las líneas de productos. Por ejemplo, las ventas de Norteamérica fueron buenas para el modelo M200, mientras que las ventas del modelo T1000 no fueron tan bien. Sin embargo, el análisis es complicado por el hecho de que algunas series no tenían muchos datos o se iniciaron en un momento diferente. También faltaban algunos datos.  
  
 ![Serie que predice la cantidad de M200 y T1000](../../2014/tutorials/media/6series-defaultforecasting.gif "Serie que predice la cantidad de M200 y T1000")  
  
 Para resolver algunos de los problemas de calidad de los datos, decide combinar los datos de ventas de todo el mundo y usar ese conjunto de tendencias de ventas generales para crear un modelo que se pueda aplicar para predecir las ventas futuras en cualquier región.  
  
 Al crear predicciones, usará el modelo que se genera mediante la formación en los datos de ventas mundiales, pero reemplazará los puntos de datos históricos con los datos de ventas de cada región individual. De este modo, se mantiene la forma de la tendencia, pero los valores previstos están alineados con las cifras de ventas históricas para cada región y modelo.  
  
## <a name="performing-cross-prediction-with-a-time-series-model"></a>Realizar una predicción cruzada con un modelo de serie temporal  
 El proceso de usar datos de una serie para predecir tendencias en otras series se denomina predicción cruzada. Puede usar la predicción cruzada en muchas situaciones: por ejemplo, podría decidir que las ventas de televisiones son adecuadas para predecir la actividad económica general, y aplicar un modelo formado en ventas de televisiones a los datos económicos generales.  
  
 En SQL Server minería de datos, se realiza una predicción cruzada mediante el parámetro REPLACE_MODEL_CASES dentro de los argumentos de la función, [PredictTimeSeries &#40;DMX&#41;](/sql/dmx/predicttimeseries-dmx).  
  
 En la tarea siguiente, aprenderá a usar REPLACE_MODEL_CASES. Usará los datos combinados de las ventas mundiales para crear un modelo y, a continuación, creará una consulta de predicción que asigna el modelo general a los datos de reemplazo.  
  
 Se supone que ya está familiarizado con la manera de generar modelos de minería de datos y, por consiguiente, se han simplificado las instrucciones para generar el modelo.  
  
#### <a name="to-build-a-mining-structure-and-mining-model-using-the-aggregated-data"></a>Para generar una estructura de minería de datos y un modelo de minería de datos utilizando los datos agregados  
  
1.  En **Explorador de soluciones**, haga clic con el botón secundario en **estructuras de minería**de datos y seleccione **nueva estructura de minería** de datos para iniciar el Asistente para minería de datos.  
  
2.  En el Asistente para minería de datos, realice las selecciones siguientes:  
  
    -   Algoritmo: serie temporal de Microsoft  
  
    -   Use el origen de datos que creó anteriormente en esta lección avanzada como origen para el modelo. Vea [predicciones de serie temporal avanzadas &#40;tutorial intermedio de minería de datos&#41;](../../2014/tutorials/advanced-time-series-predictions-intermediate-data-mining-tutorial.md).  
  
         Vista del origen de datos:`AllRegions`  
  
    -   Elija las columnas siguientes para la clave de serie y la clave temporal:  
  
         Hora clave: ReportingDate  
  
         Clave: región  
  
    -   Elija las columnas siguientes para `Input` y `Predict`:  
  
         SumQty  
  
         SumAmt  
  
         AvgAmt  
  
         AvgQty  
  
    -   En **nombre**de la estructura de minería de datos, escriba:`All Regions`  
  
    -   En **nombre del modelo de minería de datos**, escriba:`All Regions`  
  
3.  Procese la nueva estructura y el nuevo modelo.  
  
#### <a name="to-build-the-prediction-query-and-map-the-replacement-data"></a>Para generar la consulta de predicción y asignar los datos de reemplazo  
  
1.  Si el modelo aún no está abierto, haga doble clic en la estructura AllRegions y, en el diseñador de minería de datos, haga clic en la pestaña **predicción de modelo de minería** de datos.  
  
2.  En el panel **modelo de minería de datos** , el modelo AllRegions ya debe estar seleccionado. Si no está seleccionada, haga clic en **Seleccionar modelo**y, a continuación, seleccione el modelo AllRegions.  
  
3.  En el panel **seleccionar tabla (s) de entrada** , haga clic en **seleccionar tabla de casos**.  
  
4.  En el cuadro de diálogo **seleccionar tabla** , cambie el origen de datos a T1000 Pacific region y, a continuación, haga clic en **Aceptar**.  
  
5.  Haga clic con el botón secundario en la línea de combinación entre el modelo de minería de datos y los datos de entrada y seleccione **modificar conexiones**. Asigne los datos de la vista del origen de datos al modelo de la manera siguiente:  
  
    1.  Compruebe que la columna ReportingDate del modelo de minería de datos está asignada a la columna ReportingDate de los datos de entrada.  
  
    2.  En el cuadro de diálogo **modificar asignación** , en la fila de la columna del modelo AvgQty, haga clic en columna de la **tabla** y, a continuación, seleccione T1000 Pacific. quantity. Haga clic en **OK**.  
  
         Este paso asigna la columna que creó en el modelo para la cantidad promedio que predecía los datos reales de la serie T1000 de la cantidad de ventas.  
  
    3.  No asigne la región de columna del modelo a ninguna columna de entrada.  
  
         Puesto que el modelo agregaba los datos de todas las series, no hay ninguna coincidencia de los valores de series como T1000 Pacific y se generará un error cuando se ejecute la consulta de predicción.  
  
6.  Ahora creará la consulta de predicción.  
  
     Primero, agregue una columna a los resultados que genera la etiqueta AllRegions a partir del modelo y las predicciones. De esta manera, sabe que los resultados están basados en el modelo general.  
  
    1.  En la cuadrícula, haga clic en la primera fila vacía, en **origen**y, a continuación, seleccione modelo de minería de datos AllRegions.  
  
    2.  En **campo**, seleccione región.  
  
    3.  En **alias**, escriba **modelo utilizado**.  
  
7.  A continuación, agregue otra etiqueta a los resultados, de modo que pueda ver para qué serie son las predicciones.  
  
    1.  Haga clic en una fila vacía y, en **origen**, seleccione **expresión personalizada**.  
  
    2.  En la columna **alias** , escriba **ModelRegion**.  
  
    3.  En la columna **criterios o argumento** , escriba `'T1000 Pacific'`.  
  
8.  Ahora va a configurar la función de predicción cruzada.  
  
    1.  Haga clic en una fila vacía y, en **origen**, seleccione **función de predicción**.  
  
    2.  En la columna **campo** , seleccione **PredictTimeSeries**.  
  
    3.  En **alias**, escriba **valores predichos**.  
  
    4.  Arrastre el campo AvgQty del panel **modelo de minería de datos** a la columna **criterios o argumento** mediante la operación de arrastrar y colocar.  
  
    5.  En la columna **criterios o argumento** , después del nombre del campo, escriba el texto siguiente:`,5, REPLACE_MODEL_CASES`  
  
         El texto completo del cuadro de texto **criterios/argumento** debe ser el siguiente:`[AllRegions].[AvgQty],5,REPLACE_MODEL_CASES`  
  
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
 [Comparar las predicciones de modelos de previsión &#40;tutorial intermedio de minería de datos&#41;](../../2014/tutorials/comparing-predictions-for-forecasting-models-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>Consulte también  
 [Ejemplos de consultas de modelos de serie temporal](../../2014/analysis-services/data-mining/time-series-model-query-examples.md)   
 [&#41;PredictTimeSeries &#40;DMX](/sql/dmx/predicttimeseries-dmx)  
  
  
