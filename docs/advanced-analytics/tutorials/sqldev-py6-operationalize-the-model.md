---
title: Poner en marcha el modelo de Python con SQL Server | Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: d95edb081edc0f18a3734025a5902d13f8e9a295
ms.sourcegitcommit: 70e47a008b713ea30182aa22b575b5484375b041
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/23/2018
ms.locfileid: "49806815"
---
# <a name="operationalize-the-python-model-using-sql-server"></a>Poner en marcha el modelo de Python con SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Este artículo forma parte de un tutorial, [análisis de Python en bases de datos para desarrolladores de SQL](sqldev-in-database-python-for-sql-developers.md). 

En este paso, aprenderá a *operacionalizar* los modelos entrenados y guardó en el paso anterior.

En este escenario, la puesta en marcha significa implementar el modelo en producción para la puntuación. La integración con SQL Server hace esto bastante fácil, ya que puede insertar código de Python en un procedimiento almacenado. Para obtener las predicciones del modelo en función de las entradas nuevas, llame al procedimiento almacenado desde una aplicación y pasar los datos nuevos.

Esta lección muestra dos métodos para crear predicciones basadas en un modelo de Python: procesar por lotes de puntuación y la puntuación de fila por fila.

- **Puntuación por lotes:** para proporcionar varias filas de datos de entrada, pasar una consulta SELECT como un argumento para el procedimiento almacenado. El resultado es una tabla de observaciones correspondientes a los casos de entrada.
- **Puntuación individuales:** pasar un conjunto de valores de parámetro individuales como entrada.  El procedimiento almacenado devuelve una sola fila o valor.

Todo el código de Python necesario para la puntuación se proporciona como parte de los procedimientos almacenados.

| Nombre del procedimiento almacenado | Proceso por lotes o único | Origen del modelo|
|----|----|----|
|PredictTipRxPy|lote| modelo de revoscalepy|
|PredictTipSciKitPy|lote |scikit-aprender modelo|
|PredictTipSingleModeRxPy|fila única| modelo de revoscalepy|
|PredictTipSingleModeSciKitPy|fila única| scikit-aprender modelo|

## <a name="batch-scoring"></a>Puntuación por lotes

Los primeros dos procedimientos almacenados muestran la sintaxis básica para el ajuste de una llamada de predicción de Python en un procedimiento almacenado. Ambos procedimientos almacenados requieren una tabla de datos como entradas.

- Se proporciona el nombre del modelo exacto para usar como parámetro de entrada al procedimiento almacenado. El procedimiento almacenado carga el modelo serializado de la tabla de base de datos `nyc_taxi_models`.table, mediante la instrucción SELECT del procedimiento almacenado.
- El modelo serializado se almacena en la variable de Python `mod` para su posterior procesamiento mediante Python.
- Los nuevos casos que deben puntuarse se obtienen de la [!INCLUDE[tsql](../../includes/tsql-md.md)] consulta especificada en `@input_data_1`. Cuando se leen los datos de la consulta, las filas se guardan en la trama de datos predeterminada, `InputDataSet`.
- Ambos procedimientos almacenados se usen funciones de `sklearn` para calcular una métrica de precisión, AUC (área bajo la curva). Métricas de precisión como AUC sólo pueden generarse si también proporciona la etiqueta de destino (el _tipped_ columna). Predicciones no necesitan la etiqueta de destino (variable `y`), pero lo hace el cálculo de métricas de precisión.

    Por lo tanto, si no tiene etiquetas de destino para los datos que se puntuarán para, puede modificar el procedimiento almacenado para quitar los cálculos de AUC y devolver solo las probabilidades de sugerencia de las características (variable `X` en el procedimiento almacenado).

### <a name="predicttipscikitpy"></a>PredictTipSciKitPy

El procedimiento almacenado debe ya creado para usted. Si no lo encuentra, ejecute las siguientes instrucciones de T-SQL para crear los procedimientos almacenados.

Este procedimiento almacenado requiere un modelo basado en el scikit-aprender el paquete, porque utiliza las funciones específicas de ese paquete:

+ La trama de datos que contiene las entradas que se pasa a la `predict_proba` función del modelo de regresión logística, `mod`. El `predict_proba` función (`probArray = mod.predict_proba(X)`) devuelve un **float** que representa la probabilidad de que se dará una propina (de cualquier importe).

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

### <a name="predicttiprxpy"></a>PredictTipRxPy

Este procedimiento almacenado usa las mismas entradas y crea el mismo tipo de puntuaciones que el procedimiento almacenado anterior, pero usa funciones desde la **revoscalepy** paquete proporcionado con el aprendizaje automático de SQL Server.

> [!NOTE] 
> El código para este procedimiento almacenado ha cambiado ligeramente entre las primeras versiones de lanzamiento y la versión RTM, para reflejar los cambios realizados en el paquete de revoscalepy. Consulte la [cambios](#changes) tabla para obtener más información.

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
      from sklearn import metrics
      from revoscalepy.functions.RxPredict import rx_predict;
      
      mod = pickle.loads(lmodel2)
      X = InputDataSet[["passenger_count", "trip_distance", "trip_time_in_secs", "direct_distance"]]
      y = numpy.ravel(InputDataSet[["tipped"]])
      
      probArray = rx_predict(mod, X)
      prob_list = prob_array["tipped_Pred"].values 
      
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

## <a name="run-batch-scoring-using-a-select-query"></a>Ejecute la puntuación por lotes mediante una consulta SELECT

Los procedimientos almacenados **PredictTipSciKitPy** y **PredictTipRxPy** requiere dos parámetros de entrada: 

- La consulta que recupera los datos de puntuación
- El nombre de un modelo entrenado

Al pasar esos argumentos al procedimiento almacenado, puede seleccionar un modelo determinado o cambiar los datos utilizados para la puntuación.

1. Para usar el **scikit-aprender** del modelo para puntuar, llame al procedimiento almacenado **PredictTipSciKitPy**, pasando el nombre del modelo y la cadena de consulta como entradas.

    ```SQL
    DECLARE @query_string nvarchar(max) -- Specify input query
      SET @query_string='
      select tipped, fare_amount, passenger_count, trip_time_in_secs, trip_distance,
      dbo.fnCalculateDistance(pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) as direct_distance
      from nyctaxi_sample_testing'
    EXEC [dbo].[PredictTipSciKitPy] 'SciKit_model', @query_string;
    ```

    El procedimiento almacenado devuelve las probabilidades de predicción para cada carrera que se pasó como parte de la consulta de entrada. 
    
    Si está utilizando SSMS (SQL Server Management Studio) para ejecutar consultas, las probabilidades aparecerá como una tabla en la **resultados** panel. El **mensajes** panel da como resultado la métrica de precisión (AUC o área bajo la curva) con un valor de aproximadamente 0.56.

2. Para usar el **revoscalepy** del modelo para puntuar, llame al procedimiento almacenado **PredictTipRxPy**, pasando el nombre del modelo y la cadena de consulta como entradas.

    ```SQL
    EXEC [dbo].[PredictTipRxPy] 'revoscalepy_model', @query_string;
    ```

## <a name="single-row-scoring"></a>Puntuación de fila única

A veces, en lugar de puntuación por lotes, es posible que van a pasar en una sola carcasa, obtener valores desde una aplicación y devolver un resultado único basado en esos valores. Por ejemplo, podría configurar una hoja de cálculo Excel, la aplicación web o el informe para llamar al procedimiento almacenado y pásele entradas escritos o seleccionados por los usuarios.

En esta sección, aprenderá a crear predicciones únicas mediante una llamada a dos procedimientos almacenados:

+ [PredictTipSingleModeSciKitPy](#PredictTipSingleModeSciKitPy) está diseñado para la puntuación de fila única mediante el scikit-aprender modelo.
+ [PredictTipSingleModeRxPy](#PredictTipSingleModeRxPy) está diseñado para la puntuación de fila única mediante el modelo de revoscalepy.
+ Si aún no lo ha entrenado un modelo todavía, volver a [paso 5](sqldev-py5-train-and-save-a-model-using-t-sql.md)!

Ambos modelos se toman como entrada una serie de valores únicos, como número de pasajeros, distancia de viaje y así sucesivamente. Una función con valores de tabla, `fnEngineerFeatures`, se utiliza para convertir los valores de latitud y longitud de las entradas a una nueva característica, la distancia directa. [Lección 4](sqldev-py4-create-data-features-using-t-sql.md) contiene una descripción de esta función con valores de tabla.

Ambos procedimientos almacenados crean una puntuación basada en el modelo de Python.

> [!NOTE]
> 
> Es importante que indique todas las características de entrada requeridas por el modelo de Python al llamar al procedimiento almacenado desde una aplicación externa. Para evitar errores, es posible que deba convertir los datos de entrada a un tipo de datos de Python, además de validar el tipo y longitud de los datos.

### <a name="predicttipsinglemodescikitpy"></a>PredictTipSingleModeSciKitPy

Tómese un minuto para revisar el código del procedimiento almacenado que realiza la puntuación mediante el **scikit-aprender** modelo.

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

El siguiente procedimiento almacenado realiza la puntuación mediante el **revoscalepy** modelo.

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
      from revoscalepy.functions.RxPredict import rx_predict;
      
      # Load model and unserialize
      mod = pickle.loads(model)
      
      # Get features for scoring from input data
      X = InputDataSet[["passenger_count", "trip_distance", "trip_time_in_secs", "direct_distance"]]
      
      # Score data to get tip prediction probability as a list (of float)
      
      probArray = rx_predict(mod, X)
      
      probList = []
      prob_list = prob_array["tipped_Pred"].values
      
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

### <a name="generate-scores-from-models"></a>Generar puntuaciones a partir de modelos

Una vez creados los procedimientos almacenados, es fácil generar una puntuación basada en cualquier modelo. Simplemente abra un nuevo **consulta** ventana y escriba o pegue los parámetros para cada una de las columnas de característica. Las siete necesarias son valores de estas columnas de característica, en orden:
    
+ *passenger_count*
+ *trip_distance* v*trip_time_in_secs*
+ *pickup_latitude*
+ *pickup_longitude*
+ *dropoff_latitude*
+ *dropoff_longitude*

1. Para generar una predicción mediante el **revoscalepy** modelo, ejecute esta instrucción:
  
    ```SQL
    EXEC [dbo].[PredictTipSingleModeRxPy] 'revoscalepy_model', 1, 2.5, 631, 40.763958,-73.973373, 40.782139,-73.977303
    ```

2. Para generar una puntuación mediante el **scikit-aprender** modelo, ejecute esta instrucción:

    ```SQL
    EXEC [dbo].[PredictTipSingleModeSciKitPy] 'linear_model', 1, 2.5, 631, 40.763958,-73.973373, 40.782139,-73.977303
    ```

La salida de ambos procedimientos es una probabilidad de una propina de la carrera de taxi con los parámetros especificados o características.

### <a name="changes"></a> Cambios

Esta sección enumeran los cambios realizados en el código usado en este tutorial. Estos cambios se realizaron para reflejar la versión más reciente **revoscalepy** versión. Para obtener ayuda de API, consulte [referencia de biblioteca de funciones de Python](https://docs.microsoft.com/machine-learning-server/python-reference/introducing-python-package-reference).

| Cambiar detalles | Notas|
| ----|----|
| eliminar `import pandas` en todas las muestras| Ahora se cargan de forma predeterminada de pandas|
| función `rx_predict_ex` ha cambiado a `rx_predict`| Las versiones preliminares y RTM requieren `rx_predict_ex`|
| función `rx_logit_ex` ha cambiado a `rx_logit`| Las versiones preliminares y RTM requieren `rx_logit_ex`|
| ` probList.append(probArray._results["tipped_Pred"])` ha cambiado a `prob_list = prob_array["tipped_Pred"].values`| actualizaciones de API|

Si ha instalado los servicios de Python con una versión preliminar de SQL Server 2017, se recomienda que actualice. También puede actualizar solo los componentes de Python y R mediante el uso de la versión más reciente de Machine Learning Server. Para obtener más información, consulte [mediante el enlace para actualizar una instancia de SQL Server](../r/use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md).

## <a name="conclusions"></a>Conclusiones

En este tutorial, ha aprendido cómo trabajar con código Python incrustado en procedimientos almacenados. La integración con [!INCLUDE[tsql](../../includes/tsql-md.md)] facilita en gran medida para implementar modelos de Python para la predicción e incorporar el reciclaje de los modelos como parte de un flujo de datos empresariales.

## <a name="previous-step"></a>Paso anterior

[Entrenar y guardar un modelo de Python](sqldev-py5-train-and-save-a-model-using-t-sql.md)

## <a name="see-also"></a>Vea también

[Extensión de Python en SQL Server](../concepts/extension-python.md)
