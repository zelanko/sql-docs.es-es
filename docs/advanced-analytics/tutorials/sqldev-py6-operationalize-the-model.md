---
title: 'Paso 6: Poner el modelo | Documentos de Microsoft'
ms.custom: 
ms.date: 05/25/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology:
- python-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2017
dev_langs:
- Python
- TSQL
ms.assetid: 
caps.latest.revision: 2
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: b33f3876f054d7e7150a18967d5cfa37dd2d82bf
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="step-6-operationalize-the-model"></a>Paso 6: Hacer operativo el modelo

En este paso, aprenderá a *poner* los modelos que entrena y guardó en el paso anterior. Poner en este caso significa "implementar el modelo a producción para puntuar". Es fácil hacer si el código Python se encuentra en un procedimiento almacenado. A continuación, puede llamar al procedimiento almacenado desde aplicaciones, para realizar predicciones en observaciones nuevo.

Aprenderá dos métodos para llamar a un modelo de Python desde un procedimiento almacenado:

- **Modo de puntuación por lotes**: usar una consulta SELECT para proporcionar varias filas de datos. El procedimiento almacenado devuelve una tabla de observaciones correspondientes a los casos de entrada.
- **Modo de puntuación individual**: pasar un conjunto de valores de parámetros individuales como entrada.  El procedimiento almacenado devuelve una sola fila o valor.

## <a name="scoring-using-the-scikit-learn-model"></a>Puntuar usando el scikit-Obtenga información acerca de modelo

El procedimiento almacenado _PredictTipSciKitPy_ usa el scikit-obtener información sobre el modelo. Este procedimiento almacenado muestra la sintaxis básica de ajuste de una llamada de predicción de Python en un procedimiento almacenado.

- Se proporcionó el nombre del modelo que se utilice como parámetro de entrada para el procedimiento almacenado. 
- El procedimiento almacenado, a continuación, cargará el modelo serializado de la tabla de base de datos `nyc_taxi_models`.table, mediante la instrucción SELECT en el procedimiento almacenado.
- El modelo serializado se almacena en la variable de Python `mod` para su posterior procesamiento con Python.
- Los nuevos casos que se deban puntuarse se obtienen de la [!INCLUDE[tsql](../../includes/tsql-md.md)] consulta especificada en `@input_data_1`. Cuando se leen los datos de la consulta, las filas se guardan en la trama de datos predeterminada, `InputDataSet`.
- Este marco de datos se pasa a la `predict_proba` función del modelo de regresión logística, `mod`, que se creó mediante scikit-obtener información sobre el modelo. 
- El `predict_proba` función (`probArray = mod.predict_proba(X)`) devuelve un **float** que representa la probabilidad de que se proporcionará una sugerencia (de cualquier cantidad).
- El procedimiento almacenado también calcula una métrica de precisión, AUC (área bajo la curva). Métricas de precisión como AUC sólo pueden generarse si también proporciona la etiqueta de destino (es decir, la columna superpuesta). Las predicciones no necesita que la etiqueta de destino (variable `y`), pero no el cálculo de métricas de precisión.

  Por lo tanto, si no tiene etiquetas de destino para los datos que se desea puntuar, puede modificar el procedimiento almacenado para quitar los cálculos de AUC y simplemente devuelven las probabilidades de sugerencia de las características (variable `X` en el procedimiento almacenado).

```SQL
CREATE PROCEDURE [dbo].[PredictTipSciKitPy] (@model varchar(50), @inquery nvarchar(max))
AS
BEGIN
  DECLARE @lmodel2 varbinary(max) = (select model from nyc_taxi_models where name = @model);
  EXEC sp_execute_external_script
    @language = N'Python',
    @script = N'
        import pickle;
        import numpy;
        import pandas;
        from sklearn import metrics
        
        mod = pickle.loads(lmodel2)
        
        X = InputDataSet[["passenger_count", "trip_distance", "trip_time_in_secs", "direct_distance"]]
        y = numpy.ravel(InputDataSet[["tipped"]])
        
        probArray = mod.predict_proba(X)
        probList = []
        for i in range(len(probArray)):
          probList.append((probArray[i])[1])
        
        probArray = numpy.asarray(probList)
        fpr, tpr, thresholds = metrics.roc_curve(y, probArray)
        aucResult = metrics.auc(fpr, tpr)
        print ("AUC on testing data is: " + str(aucResult))
        
        OutputDataSet = pandas.DataFrame(data = probList, columns = ["predictions"])
        ',  
    @input_data_1 = @inquery,
    @input_data_1_name = N'InputDataSet',
    @params = N'@lmodel2 varbinary(max)',
    @lmodel2 = @lmodel2
  WITH RESULT SETS ((Score float));
END
GO
```

## <a name="scoring-using-the-revoscalepy-model"></a>Puntuar usando el modelo de revoscalepy

El procedimiento almacenado _PredictTipRxPy_ utiliza un modelo que se creó mediante la **revoscalepy** biblioteca. Funciona de la misma manera como el _PredictTipSciKitPy_ procedimiento, pero algunos cambios para la **revoscalepy** funciones.

```SQL
CREATE PROCEDURE [dbo].[PredictTipRxPy] (@model varchar(50), @inquery nvarchar(max))
AS
BEGIN
  DECLARE @lmodel2 varbinary(max) = (select model from nyc_taxi_models2 where name = @model);
  
  EXEC sp_execute_external_script 
    @language = N'Python',
    @script = N'
      import pickle;
      import numpy;
      import pandas;
      from sklearn import metrics
      from revoscalepy.functions.RxPredict import rx_predict_ex;
      
      mod = pickle.loads(lmodel2)
      X = InputDataSet[["passenger_count", "trip_distance", "trip_time_in_secs", "direct_distance"]]
      y = numpy.ravel(InputDataSet[["tipped"]])
      
      probArray = rx_predict_ex(mod, X)
      probList = []
      for i in range(len(probArray._results["tipped_Pred"])):
        probList.append((probArray._results["tipped_Pred"][i]))
      
      probArray = numpy.asarray(probList)
      fpr, tpr, thresholds = metrics.roc_curve(y, probArray)
      aucResult = metrics.auc(fpr, tpr)
      print ("AUC on testing data is: " + str(aucResult))
      OutputDataSet = pandas.DataFrame(data = probList, columns = ["predictions"])
      ',    
    @input_data_1 = @inquery,
    @input_data_1_name = N'InputDataSet',
    @params = N'@lmodel2 varbinary(max)',
    @lmodel2 = @lmodel2
  WITH RESULT SETS ((Score float));
END
GO
```

## <a name="batch-scoring-using-a-select-query"></a>Puntuación por lotes con una consulta SELECT

Los procedimientos almacenados **PredictTipSciKitPy** y **PredictTipRxPy** requieren dos parámetros de entrada: 

- La consulta que recupera los datos para puntuar
- El nombre de un modelo entrenado

En esta sección aprenderá cómo pasar los argumentos para el procedimiento almacenado para cambiar fácilmente el modelo y los datos usados para puntuar.

1. Definir los datos de entrada y llamar a los procedimientos almacenados para puntuar como se indica a continuación. En este ejemplo se utiliza el procedimiento almacenado PredictTipSciKitPy para puntuar y pasa el nombre del modelo y la cadena de consulta

    ```SQL
    DECLARE @query_string nvarchar(max) -- Specify input query
      SET @query_string='
      select tipped, fare_amount, passenger_count, trip_time_in_secs, trip_distance,
      dbo.fnCalculateDistance(pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) as direct_distance
      from nyctaxi_sample_testing'
    EXEC [dbo].[PredictTipSciKitPy] 'SciKit_model', @query_string;
    ```

    El procedimiento almacenado devuelve las probabilidades de predicción para cada recorrido que se pasa como parte de la consulta de entrada. Si usas SSMS (SQL Server Management Studio) para ejecutar consultas, las probabilidades aparecerá como una tabla en la **resultados** panel. El **mensajes** panel genera la métrica de precisión (AUC o área en curva) con un valor de aproximadamente 0.56.

2. Para usar el **revoscalepy** del modelo para puntuar, llame al procedimiento almacenado **PredictTipRxPy**, pasando la cadena de consulta y al nombre del modelo.

    ```SQL
    EXEC [dbo].[PredictTipRxPy] 'revoscalepy_model', @query_string;
    ```

## <a name="score-individual-rows-using-scikit-learn-model"></a>Puntuación filas individuales mediante scikit-Obtenga información acerca de modelo

A veces, en lugar de la puntuación del lote, quizás desee pasar en una sola carcasa, obtener valores de una aplicación y obtener un resultado único basado en esos valores. Por ejemplo, podría configurar una hoja de cálculo de Excel, una aplicación web o un informe de Reporting Services para llamar al procedimiento almacenado y proporcionar entradas escritas o seleccionadas por los usuarios.

En esta sección, aprenderá a crear predicciones únicas mediante una llamada a un procedimiento almacenado.

1. Dedique un minuto a revisar el código de los procedimientos almacenados [PredictTipSingleModeSciKitPy](#PredictTipSingleModeSciKitPy) y [PredictTipSingleModeRxPy](#PredictTipSingleModeRxPy), que se incluye como parte de la descarga. Estos procedimientos almacenados utilizan el scikit-obtener información y revoscalepy modelos y realizar puntuaciones como se indica a continuación:

  - El nombre del modelo y varios valores solo se proporcionan como entrada. Estas entradas incluyen el recuento de pasajeros, la distancia de ida y vuelta y así sucesivamente.
  - Una función con valores de tabla, `fnEngineerFeatures`, toma los valores de entrada y convierte las latitudes y longitudes para indicar a distancia. [Lección 4](sqldev-py4-create-data-features-using-t-sql.md) contiene una descripción de esta función con valores de tabla.
  - Si se llama al procedimiento almacenado desde una aplicación externa, asegúrese de que los datos de entrada coincide con las características necesarias de entrada del modelo de Python. Esto podría incluir la conversión de tipo o convertir los datos de entrada a un tipo de datos de Python, o la validación de tipo de datos y la longitud de los datos.
  - El procedimiento almacenado crea una puntuación basada en el modelo de Python almacenado.

### <a name="predicttipsinglemodescikitpy"></a>PredictTipSingleModeSciKitPy

Aquí está la definición del procedimiento almacenado que realiza la puntuación mediante el **scikit-aprender** modelo.

```SQL
CREATE PROCEDURE [dbo].[PredictTipSingleModeSciKitPy] (@model varchar(50), @passenger_count int = 0,
  @trip_distance float = 0,
  @trip_time_in_secs int = 0,
  @pickup_latitude float = 0,
  @pickup_longitude float = 0,
  @dropoff_latitude float = 0,
  @dropoff_longitude float = 0)
AS
BEGIN
  DECLARE @inquery nvarchar(max) = N'
  SELECT * FROM [dbo].[fnEngineerFeatures]( 
    @passenger_count,
    @trip_distance,
    @trip_time_in_secs,
    @pickup_latitude,
    @pickup_longitude,
    @dropoff_latitude,
    @dropoff_longitude)
    '
  DECLARE @lmodel2 varbinary(max) = (select model from nyc_taxi_models2 where name = @model);
  EXEC sp_execute_external_script 
    @language = N'Python',
    @script = N'
      import pickle;
      import numpy;
      import pandas;
      
      # Load model and unserialize
      mod = pickle.loads(model)
      
      # Get features for scoring from input data
      X = InputDataSet[["passenger_count", "trip_distance", "trip_time_in_secs", "direct_distance"]]
      
      # Score data to get tip prediction probability as a list (of float)
      probList = []
      probList.append((mod.predict_proba(X)[0])[1])
      
      # Create output data frame
      OutputDataSet = pandas.DataFrame(data = probList, columns = ["predictions"])
    ',
    @input_data_1 = @inquery,
    @params = N'@model varbinary(max),@passenger_count int,@trip_distance float,
      @trip_time_in_secs int ,
      @pickup_latitude float ,
      @pickup_longitude float ,
      @dropoff_latitude float ,
      @dropoff_longitude float',
      @model = @lmodel2,
      @passenger_count =@passenger_count ,
      @trip_distance=@trip_distance,
      @trip_time_in_secs=@trip_time_in_secs,
      @pickup_latitude=@pickup_latitude,
      @pickup_longitude=@pickup_longitude,
      @dropoff_latitude=@dropoff_latitude,
      @dropoff_longitude=@dropoff_longitude
  WITH RESULT SETS ((Score float));
END
GO
```

### <a name="predicttipsinglemoderxpy"></a>PredictTipSingleModeRxPy

Aquí está la definición del procedimiento almacenado que realiza la puntuación mediante el **revoscalepy** modelo.

```SQL
CREATE PROCEDURE [dbo].[PredictTipSingleModeRxPy] (@model varchar(50), @passenger_count int = 0,
  @trip_distance float = 0,
  @trip_time_in_secs int = 0,
  @pickup_latitude float = 0,
  @pickup_longitude float = 0,
  @dropoff_latitude float = 0,
  @dropoff_longitude float = 0)
AS
BEGIN
  DECLARE @inquery nvarchar(max) = N'
    SELECT * FROM [dbo].[fnEngineerFeatures]( 
      @passenger_count,
      @trip_distance,
      @trip_time_in_secs,
      @pickup_latitude,
      @pickup_longitude,
      @dropoff_latitude,
      @dropoff_longitude)
    '
  DECLARE @lmodel2 varbinary(max) = (select model from nyc_taxi_models2 where name = @model);
  EXEC sp_execute_external_script 
    @language = N'Python',
    @script = N'
      import pickle;
      import numpy;
      import pandas;
      from revoscalepy.functions.RxPredict import rx_predict_ex;
      
      # Load model and unserialize
      mod = pickle.loads(model)
      
      # Get features for scoring from input data
      X = InputDataSet[["passenger_count", "trip_distance", "trip_time_in_secs", "direct_distance"]]
      
      # Score data to get tip prediction probability as a list (of float)
      
      probArray = rx_predict_ex(mod, X)
      
      probList = []
      probList.append(probArray._results["tipped_Pred"])
      
      # Create output data frame
      OutputDataSet = pandas.DataFrame(data = probList, columns = ["predictions"])
      ',
    @input_data_1 = @inquery,
    @params = N'@model varbinary(max),@passenger_count int,@trip_distance float,
      @trip_time_in_secs int ,
      @pickup_latitude float ,
      @pickup_longitude float ,
      @dropoff_latitude float ,
      @dropoff_longitude float',
      @model = @lmodel2,
      @passenger_count =@passenger_count ,
      @trip_distance=@trip_distance,
      @trip_time_in_secs=@trip_time_in_secs,
      @pickup_latitude=@pickup_latitude,
      @pickup_longitude=@pickup_longitude,
      @dropoff_latitude=@dropoff_latitude,
      @dropoff_longitude=@dropoff_longitude
  WITH RESULT SETS ((Score float));
END
GO
```

2.  Para probarlo, abra una nueva **consulta** ventana y llame al procedimiento almacenado escribir parámetros para cada una de las columnas de característica.

    ```SQL
    -- Call stored procedure PredictTipSingleModeSciKitPy to score using SciKit-Learn model
    EXEC [dbo].[PredictTipSingleModeSciKitPy] 'linear_model', 1, 2.5, 631, 40.763958,-73.973373, 40.782139,-73.977303
    -- Call stored procedure PredictTipSingleModeRxPy to score using revoscalepy model
    EXEC [dbo].[PredictTipSingleModeRxPy] 'revoscalepy_model', 1, 2.5, 631, 40.763958,-73.973373, 40.782139,-73.977303
    ```
    
    Son los siete valores para estas columnas de característica, en orden:
    
    -   *passenger_count*
    -   *trip_distance*
    -   *trip_time_in_secs*
    -   *pickup_latitude*
    -   *pickup_longitude*
    -   *dropoff_latitude*
    -   *dropoff_longitude*

3. Los resultados de ambos procedimientos es una probabilidad de una sugerencia para el recorrido taxi con los parámetros anteriores o las características de pago.

## <a name="conclusions"></a>Conclusiones

En este tutorial, ha aprendido cómo trabajar con código de Python incrustado en procedimientos almacenados. La integración con [!INCLUDE[tsql](../../includes/tsql-md.md)] , resulta más fácil implementar modelos de Python para la predicción e incorporar modelo reciclaje como parte de un flujo de trabajo de datos de empresa.

## <a name="previous-step"></a>Paso anterior
[Paso 6: Hacer operativo el modelo](sqldev-py6-operationalize-the-model.md)

## <a name="see-also"></a>Vea también

[Los servicios con Python de aprendizaje automático](../python/sql-server-python-services.md)

