---
title: Resultados posibles para la lección 4 predicción mediante modelos de R, SQL Server Machine Learning
description: Tutorial que muestra cómo poner los scripts de R incrustados en SQL Server en procedimientos almacenados con funciones de Transact-SQL
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/16/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.openlocfilehash: ca5d09b052d80083589189f53a8dc9c059e5cf99
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67961861"
---
# <a name="lesson-4-run-predictions-using-r-embedded-in-a-stored-procedure"></a>Lección 4: Ejecutar predicciones con R incrustado en un procedimiento almacenado
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

En este artículo forma parte de un tutorial para desarrolladores de SQL sobre cómo usar R en SQL Server.

En este paso, aprenderá a usar el modelo con las nuevas observaciones para predecir resultados posibles. El modelo se ajusta en un procedimiento almacenado que se puede llamar directamente por otras aplicaciones. El tutorial muestran varias maneras de realizar la puntuación:

- **Modo de puntuación por lotes**: Utilice una consulta de selección como entrada al procedimiento almacenado. El procedimiento almacenado devuelve una tabla de observaciones correspondientes a los casos de entrada.

- **Modo de puntuación individual**: Pasar un conjunto de valores de parámetro individuales como entrada.  El procedimiento almacenado devuelve una sola fila o valor.

En primer lugar, veremos cómo funcionan las puntuaciones en general.

## <a name="basic-scoring"></a>Puntuaciones básicas

El procedimiento almacenado **RxPredict** muestra la sintaxis básica para el ajuste de una llamada de RevoScaleR rxPredict en un procedimiento almacenado.

```sql
CREATE PROCEDURE [dbo].[RxPredict] (@model varchar(250), @inquery nvarchar(max))
AS 
BEGIN 

DECLARE @lmodel2 varbinary(max) = (SELECT model FROM nyc_taxi_models WHERE name = @model);  
EXEC sp_execute_external_script @language = N'R',
  @script = N' 
    mod <- unserialize(as.raw(model)); 
    print(summary(mod)) 
    OutputDataSet<-rxPredict(modelObject = mod, data = InputDataSet, outData = NULL, predVarNames = "Score", type = "response", writeModelVars = FALSE, overwrite = TRUE); 
    str(OutputDataSet) 
    print(OutputDataSet) 
    ', 
  @input_data_1 = @inquery, 
  @params = N'@model varbinary(max)',
  @model = @lmodel2 
  WITH RESULT SETS ((Score float));
END
GO
```

+ La instrucción SELECT Obtiene el modelo serializado de la base de datos y almacena el modelo en la variable de R `mod` para su posterior procesamiento con R.

+ Los nuevos casos para puntuar se obtienen de la [!INCLUDE[tsql](../../includes/tsql-md.md)] consulta especificada en `@inquery`, el primer parámetro del procedimiento almacenado. Cuando se leen los datos de la consulta, las filas se guardan en la trama de datos predeterminada, `InputDataSet`. Esta trama de datos se pasa a la [rxPredict](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxpredict) funcionando en [RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler), lo que genera las puntuaciones.
  
    `OutputDataSet<-rxPredict(modelObject = mod, data = InputDataSet, outData = NULL, predVarNames = "Score", type = "response", writeModelVars = FALSE, overwrite = TRUE);`
  
    Como data.frame puede contener una sola fila, puede usar el mismo código para la puntuación individual o por lotes.
  
+ El valor devuelto por la `rxPredict` función es un **float** que representa la probabilidad de que el controlador obtiene una sugerencia de cualquier cantidad.

## <a name="batch-scoring-a-list-of-predictions"></a>(Una lista de predicciones) de puntuación por lotes

Un escenario más común es generar predicciones para diversas observaciones en modo por lotes. En este paso, vamos a ver cómo funciona la puntuación por lotes.

1.  Comience por obtener un conjunto de datos de entrada para que funcione con menor. Esta consulta crea una lista de los "Diez mejores" viajes con número de pasajeros y otras características necesarias para realizar una predicción.
  
    ```sql
    SELECT TOP 10 a.passenger_count AS passenger_count, a.trip_time_in_secs AS trip_time_in_secs, a.trip_distance AS trip_distance, a.dropoff_datetime AS dropoff_datetime, dbo.fnCalculateDistance(pickup_latitude, pickup_longitude, dropoff_latitude,dropoff_longitude) AS direct_distance
    
    FROM (SELECT medallion, hack_license, pickup_datetime, passenger_count,trip_time_in_secs,trip_distance, dropoff_datetime, pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude FROM nyctaxi_sample)a

    LEFT OUTER JOIN

    (SELECT medallion, hack_license, pickup_datetime FROM nyctaxi_sample TABLESAMPLE (70 percent) REPEATABLE (98052)    )b

    ON a.medallion=b.medallion AND a.hack_license=b.hack_license 
    AND a.pickup_datetime=b.pickup_datetime
    WHERE b.medallion IS NULL
    ```

    **Resultados de ejemplo**
    
    ```sql
    passenger_count   trip_time_in_secs    trip_distance  dropoff_datetime   direct_distance
    1  283 0.7 2013-03-27 14:54:50.000   0.5427964547
    1  289 0.7 2013-02-24 12:55:29.000   0.3797099614
    1  214 0.7 2013-06-26 13:28:10.000   0.6970098661
    ```

2. Crear un procedimiento almacenado llamado **RxPredictBatchOutput** en [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)].

    ```sql
    CREATE PROCEDURE [dbo].[RxPredictBatchOutput] (@model varchar(250), @inquery nvarchar(max))
    AS
    BEGIN
    DECLARE @lmodel2 varbinary(max) = (SELECT model FROM nyc_taxi_models WHERE name = @model);
    EXEC sp_execute_external_script 
      @language = N'R',
      @script = N'
        mod <- unserialize(as.raw(model));
        print(summary(mod))
        OutputDataSet<-rxPredict(modelObject = mod, data = InputDataSet, outData = NULL, predVarNames = "Score", type = "response", writeModelVars = FALSE, overwrite = TRUE);
        str(OutputDataSet)
        print(OutputDataSet)
      ',
      @input_data_1 = @inquery,
      @params = N'@model varbinary(max)',
      @model = @lmodel2
      WITH RESULT SETS ((Score float));
    END
    ```

3.  Proporcione el texto de consulta en una variable y pasarla como parámetro al procedimiento almacenado:

    ```sql
    -- Define the input data
    DECLARE @query_string nvarchar(max)
    SET @query_string='SELECT TOP 10 a.passenger_count as passenger_count, a.trip_time_in_secs AS trip_time_in_secs, a.trip_distance AS trip_distance, a.dropoff_datetime AS dropoff_datetime, dbo.fnCalculateDistance(pickup_latitude, pickup_longitude, dropoff_latitude,dropoff_longitude) AS direct_distance FROM  (SELECT medallion, hack_license, pickup_datetime, passenger_count,trip_time_in_secs,trip_distance, dropoff_datetime, pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude FROM nyctaxi_sample  )a   LEFT OUTER JOIN (SELECT medallion, hack_license, pickup_datetime FROM nyctaxi_sample TABLESAMPLE (70 percent) REPEATABLE (98052))b ON a.medallion=b.medallion AND a.hack_license=b.hack_license AND a.pickup_datetime=b.pickup_datetime WHERE b.medallion is null'
    
    -- Call the stored procedure for scoring and pass the input data
    EXEC [dbo].[RxPredictBatchOutput] @model = 'RxTrainLogit_model', @inquery = @query_string;
    ```
  
El procedimiento almacenado devuelve una serie de valores que representan la predicción para cada uno de los viajes en los 10 principales. Sin embargo, los viajes superiores también son único pasajero viajes con una distancia de viaje relativamente corta, para que el controlador no es probable que reciba una propina.
  

> [!TIP]
> 
> En lugar de devolver únicamente el "Sí: propina" y "no-sugerencia" resultados, podría también devolver la puntuación de probabilidad de predicción y, a continuación, aplicar una cláusula WHERE a la _puntuación_ valores de columna para clasificar el resultado como "propina probable" o " propina improbable", con un valor de umbral como 0,5 o 0,7. Este paso no se incluye en el procedimiento almacenado, pero es fácil de implementar.

## <a name="single-row-scoring-of-multiple-inputs"></a>Fila única de puntuación de varias entradas

A veces desea pasar varios valores de entrada y obtener una sola predicción según esos valores. Por ejemplo, podría configurar una hoja de cálculo de Excel, una aplicación web o un informe de Reporting Services para llamar al procedimiento almacenado y proporcionar entradas escritas o seleccionadas por los usuarios de esas aplicaciones.

En esta sección, aprenderá a crear predicciones únicas mediante un procedimiento almacenado que toma varias entradas, como número de pasajeros, distancia de viaje y así sucesivamente. El procedimiento almacenado crea una puntuación basada en el modelo de R almacenado previamente.
  
Si se llama al procedimiento almacenado desde una aplicación externa, debe asegurarse de que los datos coinciden con los requisitos del modelo de R. Esto puede incluir asegurarse de que los datos de entrada se pueden convertir a un tipo de datos R o validar el tipo y la longitud de los datos. 

1. Crear un procedimiento almacenado **RxPredictSingleRow**.
  
    ```sql
    CREATE PROCEDURE [dbo].[RxPredictSingleRow] @model varchar(50), @passenger_count int = 0, @trip_distance float = 0, @trip_time_in_secs int = 0, @pickup_latitude float = 0, @pickup_longitude float = 0, @dropoff_latitude float = 0, @dropoff_longitude float = 0
    AS
    BEGIN
    DECLARE @inquery nvarchar(max) = N'SELECT * FROM [dbo].[fnEngineerFeatures](@passenger_count, @trip_distance, @trip_time_in_secs,  @pickup_latitude, @pickup_longitude, @dropoff_latitude, @dropoff_longitude)';
    DECLARE @lmodel2 varbinary(max) = (SELECT model FROM nyc_taxi_models WHERE name = @model);
    EXEC sp_execute_external_script  
      @language = N'R',
      @script = N'  
        mod <- unserialize(as.raw(model));  
        print(summary(mod));  
        OutputDataSet<-rxPredict(modelObject = mod, data = InputDataSet, outData = NULL, predVarNames = "Score", type = "response", writeModelVars = FALSE, overwrite = TRUE);  
        str(OutputDataSet);
        print(OutputDataSet); 
        ',  
      @input_data_1 = @inquery,  
      @params = N'@model varbinary(max),@passenger_count int,@trip_distance float,@trip_time_in_secs int ,  @pickup_latitude float ,@pickup_longitude float ,@dropoff_latitude float ,@dropoff_longitude float', @model = @lmodel2, @passenger_count =@passenger_count, @trip_distance=@trip_distance, @trip_time_in_secs=@trip_time_in_secs, @pickup_latitude=@pickup_latitude, @pickup_longitude=@pickup_longitude, @dropoff_latitude=@dropoff_latitude, @dropoff_longitude=@dropoff_longitude  
      WITH RESULT SETS ((Score float));  
    END
    ```

2. Pruébelo, proporcionando los valores manualmente.
  
    Abra una nueva **consulta** ventana y llame al procedimiento almacenado, que proporciona valores para cada uno de los parámetros. Los parámetros representan las columnas de característica que se usa el modelo y son necesarios.

    ```sql
    EXEC [dbo].[RxPredictSingleRow] @model = 'RxTrainLogit_model',
    @passenger_count = 1,
    @trip_distance = 2.5,
    @trip_time_in_secs = 631,
    @pickup_latitude = 40.763958,
    @pickup_longitude = -73.973373,
    @dropoff_latitude =  40.782139,
    @dropoff_longitude = -73.977303
    ```

    O bien, use este formulario más corto compatibles con [parámetros a un procedimiento almacenado](https://docs.microsoft.com/sql/relational-databases/stored-procedures/specify-parameters):
  
    ```sql
    EXEC [dbo].[RxPredictSingleRow] 'RxTrainLogit_model', 1, 2.5, 631, 40.763958,-73.973373, 40.782139,-73.977303
    ```

3. Los resultados indican que la probabilidad de obtener una sugerencia es baja (cero) en los viajes 10 principales, ya que todos son viajes único pasajero en una distancia relativamente corta.

## <a name="conclusions"></a>Conclusiones

Esto concluye el tutorial. Ahora que ha aprendido a incrustar código R en procedimientos almacenados, puede ampliar estas prácticas para crear modelos de su elección. La integración con [!INCLUDE[tsql](../../includes/tsql-md.md)] hace mucho más fácil la implementación de modelos de R para la predicción y la incorporación del reciclaje de modelos como parte de un flujo de trabajo de datos empresarial.

## <a name="previous-lesson"></a>Lección anterior

[Lección 3: Entrenar y guardar un modelo de R mediante T-SQL](sqldev-train-and-save-a-model-using-t-sql.md)
