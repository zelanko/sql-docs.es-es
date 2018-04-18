---
title: Paso 6 poner el modelo de Python mediante SQL Server | Documentos de Microsoft
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: aedd6beeb720c24a6960950abc6a29c1bf89a5fa
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="step-6-operationalize-the-python-model-using-sql-server"></a>Paso 6: Poner el modelo de Python con SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Este artículo forma parte de un tutorial, [análisis de Python en bases de datos para desarrolladores de SQL](sqldev-in-database-python-for-sql-developers.md). 

En este paso, aprenderá a *poner* los modelos que entrena y guardó en el paso anterior.

En este escenario, puesta en marcha implica que la implementación del modelo a producción para puntuar. La integración con SQL Server facilita bastante, porque se puede incrustar código Python en un procedimiento almacenado. Para obtener las predicciones del modelo en función de las nuevas entradas, llame al procedimiento almacenado desde una aplicación y pasar los nuevos datos.

Esta lección muestra dos métodos para crear predicciones basadas en un modelo de Python: procesar por lotes de puntuación y puntuación fila por fila.

- **La puntuación del lote:** para proporcionar varias filas de datos de entrada, pase una consulta SELECT como argumento para el procedimiento almacenado. El resultado es una tabla de observaciones correspondiente a los casos de entrada.
- **Puntuación individuales:** pase un conjunto de valores de parámetro individual como entrada.  El procedimiento almacenado devuelve una sola fila o valor.

Todo el código de Python necesario para la puntuación se proporciona como parte de los procedimientos almacenados.

| Nombre del procedimiento almacenado | Proceso por lotes o único | Origen del modelo|
|----|----|----|
|PredictTipRxPy|lote| modelo de revoscalepy|
|PredictTipSciKitPy|lote |scikit-Obtenga información acerca de modelo|
|PredictTipSingleModeRxPy|fila única| modelo de revoscalepy|
|PredictTipSingleModeSciKitPy|fila única| scikit-Obtenga información acerca de modelo|

## <a name="batch-scoring"></a>La puntuación del lote

Los primeros dos procedimientos almacenados muestran la sintaxis básica para una llamada de predicción de Python de ajuste en un procedimiento almacenado. Ambos procedimientos almacenados requieren una tabla de datos como entradas.

- Se proporcionó el nombre del modelo exacto que se utilice como parámetro de entrada para el procedimiento almacenado. El procedimiento almacenado carga el modelo serializado de la tabla de base de datos `nyc_taxi_models`.table, mediante la instrucción SELECT en el procedimiento almacenado.
- El modelo serializado se almacena en la variable de Python `mod` para su posterior procesamiento con Python.
- Los nuevos casos que se deban puntuarse se obtienen de la [!INCLUDE[tsql](../../includes/tsql-md.md)] consulta especificada en `@input_data_1`. Cuando se leen los datos de la consulta, las filas se guardan en la trama de datos predeterminada, `InputDataSet`.
- Ambos procedimiento almacenado usar funciones de `sklearn` para calcular una métrica de precisión, AUC (área bajo la curva). Métricas de precisión como AUC sólo pueden generarse si también proporciona la etiqueta de destino (el _superpuesto_ columna). Las predicciones no necesita que la etiqueta de destino (variable `y`), pero no el cálculo de métricas de precisión.

    Por lo tanto, si no tiene etiquetas de destino para los datos que se desea puntuar, puede modificar el procedimiento almacenado para quitar los cálculos de AUC y devolver solo las probabilidades de sugerencia de las características (variable `X` en el procedimiento almacenado).

### <a name="predicttipscikitpy"></a>PredictTipSciKitPy

El procedimiento almacenado debe haber ya creado por usted. Si no lo encuentra, ejecute las siguientes instrucciones de T-SQL para crear los procedimientos almacenados.

Este procedimiento almacenado requiere un modelo basado en el scikit-Obtenga información acerca de paquete, ya que usa las funciones concretas de ese paquete:

+ La trama de datos que contiene entradas que se pasa a la `predict_proba` función del modelo de regresión logística, `mod`. El `predict_proba` función (`probArray = mod.predict_proba(X)`) devuelve un **float** que representa la probabilidad de que se proporcionará una sugerencia (de cualquier cantidad).

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

Este procedimiento almacenado utiliza las mismas entradas y crea el mismo tipo de puntuaciones que el anterior procedimiento almacenado, pero se utilizan funciones de la **revoscalepy** paquete suministrado con aprendizaje automático de SQL Server.

> [!NOTE] 
> El código de este procedimiento almacenado ha cambiado ligeramente entre las primeras versiones de lanzamiento y la versión RTM, para reflejar los cambios efectuados en el paquete revoscalepy. Consulte la [cambios](#changes) tabla para obtener más información.

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

## <a name="run-batch-scoring-using-a-select-query"></a>Ejecutar la puntuación del lote utilizando una consulta SELECT

Los procedimientos almacenados **PredictTipSciKitPy** y **PredictTipRxPy** requieren dos parámetros de entrada: 

- La consulta que recupera los datos para puntuar
- El nombre de un modelo entrenado

Al pasar los argumentos para el procedimiento almacenado, puede seleccionar un modelo determinado o cambiar los datos usados para puntuar.

1. Para usar el **scikit-Obtenga información acerca de** del modelo para puntuar, llame al procedimiento almacenado **PredictTipSciKitPy**, pasando el nombre del modelo y la cadena de consulta como entradas.

    ```SQL
    DECLARE @query_string nvarchar(max) -- Specify input query
      SET @query_string='
      select tipped, fare_amount, passenger_count, trip_time_in_secs, trip_distance,
      dbo.fnCalculateDistance(pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) as direct_distance
      from nyctaxi_sample_testing'
    EXEC [dbo].[PredictTipSciKitPy] 'SciKit_model', @query_string;
    ```

    El procedimiento almacenado devuelve las probabilidades de predicción para cada recorrido que se pasa como parte de la consulta de entrada. 
    
    Si usas SSMS (SQL Server Management Studio) para ejecutar consultas, las probabilidades aparecerá como una tabla en la **resultados** panel. El **mensajes** panel genera la métrica de precisión (AUC o área en curva) con un valor de aproximadamente 0.56.

2. Para usar el **revoscalepy** del modelo para puntuar, llame al procedimiento almacenado **PredictTipRxPy**, pasando el nombre del modelo y la cadena de consulta como entradas.

    ```SQL
    EXEC [dbo].[PredictTipRxPy] 'revoscalepy_model', @query_string;
    ```

## <a name="single-row-scoring"></a>Puntuación de varias filas

A veces, en lugar de puntuación de lote, puede pasar en un único caso, obtener valores de una aplicación y devolver un resultado único basado en esos valores. Por ejemplo, podría configurar una hoja de cálculo Excel, la aplicación web o el informe para llamar al procedimiento almacenado y pase a la se introduce escritos o seleccionados por los usuarios.

En esta sección, aprenderá a crear predicciones únicas mediante una llamada a dos procedimientos almacenados:

+ [PredictTipSingleModeSciKitPy](#PredictTipSingleModeSciKitPy) está diseñado para puntuar la fila única mediante el scikit-obtener información sobre el modelo.
+ [PredictTipSingleModeRxPy](#PredictTipSingleModeRxPy) está diseñado para su puntuación de varias filas utilizando el modelo de revoscalepy.
+ Si aún no lo ha entrenado un modelo todavía, volver a [paso 5](sqldev-py5-train-and-save-a-model-using-t-sql.md)!

Ambos modelos se toman como entrada una serie de valores únicos, como el recuento de pasajeros, distancia de viaje y así sucesivamente. Una función con valores de tabla, `fnEngineerFeatures`, se utiliza para convertir los valores de latitud y longitud de las entradas a una nueva característica, dirigir la distancia. [Lección 4](sqldev-py4-create-data-features-using-t-sql.md) contiene una descripción de esta función con valores de tabla.

Ambos procedimientos almacenados crear una puntuación basada en el modelo de Python.

> [!NOTE]
> 
> Es importante que proporcione todas las características de entrada requeridas por el modelo de Python cuando se llama al procedimiento almacenado desde una aplicación externa. Para evitar errores, deberá convertir los datos de entrada a un tipo de datos de Python, además de validación de datos de tipo y longitud de los datos.

### <a name="predicttipsinglemodescikitpy"></a>PredictTipSingleModeSciKitPy

Dedique un minuto a revisar el código del procedimiento almacenado que realiza la puntuación mediante el **scikit-aprender** modelo.

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

El siguiente procedimiento almacenado realiza puntuación mediante el **revoscalepy** modelo.

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

Una vez creados los procedimientos almacenados, es fácil generar una puntuación basada en cualquier modelo. Abra un nuevo **consulta** ventana y escriba o pegue parámetros para cada una de las columnas de característica. Las siete necesarias son valores de estas columnas de característica, en orden:
    
+ *passenger_count*
+ *trip_distance* v*trip_time_in_secs*
+ *pickup_latitude*
+ *pickup_longitude*
+ *dropoff_latitude*
+ *dropoff_longitude*

1. Para generar una predicción usando el **revoscalepy** modelo, ejecute esta instrucción:
  
    ```SQL
    EXEC [dbo].[PredictTipSingleModeRxPy] 'revoscalepy_model', 1, 2.5, 631, 40.763958,-73.973373, 40.782139,-73.977303
    ```

2. Para generar una puntuación mediante el uso de la **scikit-aprender** modelo, ejecute esta instrucción:

    ```SQL
    EXEC [dbo].[PredictTipSingleModeSciKitPy] 'linear_model', 1, 2.5, 631, 40.763958,-73.973373, 40.782139,-73.977303
    ```

Los resultados de ambos procedimientos es una probabilidad de una sugerencia para el recorrido taxi con los parámetros especificados o las características de pago.

### <a name="changes"></a> Cambios

Esta sección enumeran los cambios en el código utilizado en este tutorial. Estos cambios se realizaron para reflejar la versión más reciente **revoscalepy** versión. Para obtener ayuda acerca de la API, vea [referencia de la biblioteca de función de Python](https://docs.microsoft.com/machine-learning-server/python-reference/introducing-python-package-reference).

| Cambie los detalles | Notas|
| ----|----|
| eliminar `import pandas` en todos los ejemplos| pandas cargados ahora de forma predeterminada|
| función `rx_predict_ex` cambiado a `rx_predict`| Las versiones RTM y preliminares requieren `rx_predict_ex`|
| función `rx_logit_ex` cambiado a `rx_logit`| Las versiones RTM y preliminares requieren `rx_logit_ex`|
| ` probList.append(probArray._results["tipped_Pred"])` cambia a `prob_list = prob_array["tipped_Pred"].values`| actualizaciones de API|

Si ha instalado servicios de Python con una versión preliminar de SQL Server 2017, se recomienda que actualice. También puede actualizar solo los componentes de Python y R mediante la última versión del servidor de aprendizaje de máquina. Para obtener más información, consulte [utiliza el enlace para actualizar una instancia de SQL Server](../r/use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md).

## <a name="conclusions"></a>Conclusiones

En este tutorial, ha aprendido cómo trabajar con código de Python incrustado en procedimientos almacenados. La integración con [!INCLUDE[tsql](../../includes/tsql-md.md)] , resulta más fácil implementar modelos de Python para la predicción e incorporar modelo reciclaje como parte de un flujo de trabajo de datos de empresa.

## <a name="previous-step"></a>Paso anterior

[Paso 5: Entrenar y guardar un modelo de Python](sqldev-py5-train-and-save-a-model-using-t-sql.md)

## <a name="see-also"></a>Vea también

[Los servicios con Python de aprendizaje automático](../python/sql-server-python-services.md)
