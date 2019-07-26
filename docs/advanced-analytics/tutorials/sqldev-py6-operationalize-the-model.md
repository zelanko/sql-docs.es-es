---
title: Predicción de posibles resultados con modelos de Python
description: Tutorial que muestra cómo poner en funcionamiento el script de PYthon incrustado en SQL Server procedimientos almacenados con funciones de T-SQL
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/02/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.openlocfilehash: b04e57c45c6113d4a0404a3a338e6beba4cda813
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/24/2019
ms.locfileid: "68468595"
---
# <a name="run-predictions-using-python-embedded-in-a-stored-procedure"></a>Ejecutar predicciones con Python incrustado en un procedimiento almacenado
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Este artículo forma parte de un tutorial, [análisis de Python en base de datos para desarrolladores de SQL](sqldev-in-database-python-for-sql-developers.md). 

En este paso, aprenderá a poner en *funcionamiento* los modelos que ha entrenado y guardado en el paso anterior.

En este escenario, la operativa significa implementar el modelo en producción para su puntuación. La integración con SQL Server hace que esto sea bastante sencillo, ya que se puede incrustar código de Python en un procedimiento almacenado. Para obtener las predicciones del modelo en función de nuevas entradas, basta con llamar al procedimiento almacenado desde una aplicación y pasar los nuevos datos.

En esta lección se muestran dos métodos para crear predicciones basadas en un modelo de Python: puntuación por lotes y puntuación fila por fila.

- **Puntuación por lotes:** Para proporcionar varias filas de datos de entrada, pase una consulta SELECT como argumento al procedimiento almacenado. El resultado es una tabla de observaciones correspondiente a los casos de entrada.
- **Puntuación individual:** Pase un conjunto de valores de parámetro individuales como entrada.  El procedimiento almacenado devuelve una sola fila o valor.

Todo el código de Python necesario para la puntuación se proporciona como parte de los procedimientos almacenados.

## <a name="batch-scoring"></a>Puntuación por lotes

Los dos primeros procedimientos almacenados muestran la sintaxis básica para encapsular una llamada de predicción de Python en un procedimiento almacenado. Ambos procedimientos almacenados requieren una tabla de datos como entradas.

- El nombre del modelo exacto que se va a utilizar se proporciona como parámetro de entrada para el procedimiento almacenado. El procedimiento almacenado carga el modelo serializado de la tabla `nyc_taxi_models`de base de datos. Table, utilizando la instrucción SELECT en el procedimiento almacenado.
- El modelo serializado se almacena en la variable `mod` de Python para su posterior procesamiento mediante python.
- Los nuevos casos que deben puntuarse se obtienen a partir de la [!INCLUDE[tsql](../../includes/tsql-md.md)] consulta especificada en `@input_data_1`. Cuando se leen los datos de la consulta, las filas se guardan en la trama de datos predeterminada, `InputDataSet`.
- Ambos procedimientos almacenados usan funciones de `sklearn` para calcular una métrica de precisión, AUC (área en curva). Solo se pueden generar métricas de precisión, como AUC, si también proporciona la etiqueta de destino ( _la columna marcada_ ). Las predicciones no necesitan la etiqueta de destino ( `y`variable), pero sí el cálculo de la métrica de precisión.

    Por lo tanto, si no tiene etiquetas de destino para los datos que se van a puntuar, puede modificar el procedimiento almacenado para quitar los cálculos de AUC y devolver solo las probabilidades de propinas `X` de las características (variable en el procedimiento almacenado).

### <a name="predicttipscikitpy"></a>PredictTipSciKitPy

Rrun las siguientes instrucciones T-SQL para crear los procedimientos almacenados. Este procedimiento almacenado requiere un modelo basado en el paquete scikit-Learn, porque usa funciones específicas para ese paquete:

+ La trama de datos que contiene entradas se pasa `predict_proba` a la función del modelo de regresión `mod`logística,. La `predict_proba` función (`probArray = mod.predict_proba(X)`) devuelve un valor **float** que representa la probabilidad de que se proporcione una propina (de cualquier cantidad).

```sql
DROP PROCEDURE IF EXISTS PredictTipSciKitPy;
GO

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

Este procedimiento almacenado utiliza las mismas entradas y crea el mismo tipo de puntuaciones que el procedimiento almacenado anterior, pero usa las funciones del paquete **revoscalepy** proporcionado con SQL Server machine learning.

```sql
DROP PROCEDURE IF EXISTS PredictTipRxPy;
GO

CREATE PROCEDURE [dbo].[PredictTipRxPy] (@model varchar(50), @inquery nvarchar(max))
AS
BEGIN
DECLARE @lmodel2 varbinary(max) = (select model from nyc_taxi_models where name = @model);
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
probList = probArray["tipped_Pred"].values 

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

## <a name="run-batch-scoring-using-a-select-query"></a>Ejecutar la puntuación por lotes mediante una consulta SELECT

Los procedimientos almacenados **PredictTipSciKitPy** y **PredictTipRxPy** requieren dos parámetros de entrada: 

- La consulta que recupera los datos para la puntuación
- El nombre de un modelo entrenado

Al pasar esos argumentos al procedimiento almacenado, puede seleccionar un modelo determinado o cambiar los datos que se usan para la puntuación.

1. Para usar el modelo **scikit-Learn** para la puntuación, llame al procedimiento almacenado **PredictTipSciKitPy**, pasando el nombre del modelo y la cadena de consulta como entradas.

    ```sql
    DECLARE @query_string nvarchar(max) -- Specify input query
      SET @query_string='
      select tipped, fare_amount, passenger_count, trip_time_in_secs, trip_distance,
      dbo.fnCalculateDistance(pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) as direct_distance
      from nyctaxi_sample_testing'
    EXEC [dbo].[PredictTipSciKitPy] 'SciKit_model', @query_string;
    ```

    El procedimiento almacenado devuelve las probabilidades previstas de cada recorrido que se pasó como parte de la consulta de entrada. 
    
    Si usa SSMS (SQL Server Management Studio) para ejecutar consultas, las probabilidades aparecerán como una tabla en el panel de **resultados** . El panel **mensajes** genera la métrica de precisión (AUC o área en curva) con un valor de alrededor de 0,56.

2. Para usar el modelo **revoscalepy** para la puntuación, llame al procedimiento almacenado **PredictTipRxPy**, pasando el nombre del modelo y la cadena de consulta como entradas.

    ```sql
    DECLARE @query_string nvarchar(max) -- Specify input query
      SET @query_string='
      select tipped, fare_amount, passenger_count, trip_time_in_secs, trip_distance,
      dbo.fnCalculateDistance(pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) as direct_distance
      from nyctaxi_sample_testing'
    EXEC [dbo].[PredictTipRxPy] 'revoscalepy_model', @query_string;
    ```

## <a name="single-row-scoring"></a>Puntuación de fila única

A veces, en lugar de la puntuación por lotes, puede que desee pasar un solo caso, obtener valores de una aplicación y devolver un único resultado basado en esos valores. Por ejemplo, podría configurar una hoja de cálculo de Excel, una aplicación web o un informe para llamar al procedimiento almacenado y pasarlo a entradas de ti escritas o seleccionadas por los usuarios.

En esta sección, aprenderá a crear predicciones únicas llamando a dos procedimientos almacenados:

+ [PredictTipSingleModeSciKitPy](#predicttipsinglemodescikitpy) está diseñado para la puntuación de fila única mediante el modelo scikit-Learn.
+ [PredictTipSingleModeRxPy](#predicttipsinglemoderxpy) está diseñado para la puntuación de fila única mediante el modelo revoscalepy.
+ Si aún no ha entrenado un modelo, vuelva al [paso 5](sqldev-py5-train-and-save-a-model-using-t-sql.md).

Ambos modelos toman como entrada una serie de valores únicos, como el número de pasajeros, la distancia del viaje, etc. Una función con valores de tabla `fnEngineerFeatures`,, se usa para convertir los valores de latitud y longitud de las entradas a una nueva característica, distancia directa. La [Lección 4](sqldev-py4-create-data-features-using-t-sql.md) contiene una descripción de esta función con valores de tabla.

Ambos procedimientos almacenados crean una puntuación basada en el modelo de Python.

> [!NOTE]
> 
> Es importante que proporcione todas las características de entrada que requiere el modelo de Python al llamar al procedimiento almacenado desde una aplicación externa. Para evitar errores, es posible que tenga que convertir los datos de entrada a un tipo de datos de Python, además de validar el tipo de datos y la longitud de los datos.

### <a name="predicttipsinglemodescikitpy"></a>PredictTipSingleModeSciKitPy

Tómese un minuto para revisar el código del procedimiento almacenado que realiza la puntuación mediante el modelo **scikit-Learn** .

```sql
DROP PROCEDURE IF EXISTS PredictTipSingleModeSciKitPy;
GO

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
DECLARE @lmodel2 varbinary(max) = (select model from nyc_taxi_models where name = @model);
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

El siguiente procedimiento almacenado realiza la puntuación mediante el modelo **revoscalepy** .

```sql
DROP PROCEDURE IF EXISTS PredictTipSingleModeRxPy;
GO

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
DECLARE @lmodel2 varbinary(max) = (select model from nyc_taxi_models where name = @model);
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
probList = probArray["tipped_Pred"].values

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

Una vez creados los procedimientos almacenados, es fácil generar una puntuación basada en cualquiera de los modelos. Simplemente abra una nueva ventana de **consulta** y escriba o pegue parámetros para cada una de las columnas de característica. Los siete valores necesarios son para estas columnas de características, en orden:
    
+ *passenger_count*
+ *trip_distance* v*trip_time_in_secs*
+ *pickup_latitude*
+ *pickup_longitude*
+ *dropoff_latitude*
+ *dropoff_longitude*

1. Para generar una predicción mediante el modelo **revoscalepy** , ejecute esta instrucción:
  
    ```sql
    EXEC [dbo].[PredictTipSingleModeRxPy] 'revoscalepy_model', 1, 2.5, 631, 40.763958,-73.973373, 40.782139,-73.977303
    ```

2. Para generar una puntuación mediante el modelo **scikit-Learn** , ejecute esta instrucción:

    ```sql
    EXEC [dbo].[PredictTipSingleModeSciKitPy] 'SciKit_model', 1, 2.5, 631, 40.763958,-73.973373, 40.782139,-73.977303
    ```

La salida de ambos procedimientos es una probabilidad de que se pague una propina por el viaje de taxi con los parámetros o características especificados.

## <a name="conclusions"></a>Conclusiones

En este tutorial, ha aprendido a trabajar con código de Python insertado en procedimientos almacenados. La integración con [!INCLUDE[tsql](../../includes/tsql-md.md)] hace que sea mucho más fácil implementar modelos de Python para la predicción y incorporar el reciclaje de modelos como parte de un flujo de trabajo de datos empresariales.

## <a name="previous-step"></a>Paso anterior

[Entrenar y guardar un modelo de Python](sqldev-py5-train-and-save-a-model-using-t-sql.md)

## <a name="see-also"></a>Vea también

[Extensión de Python en SQL Server](../concepts/extension-python.md)
