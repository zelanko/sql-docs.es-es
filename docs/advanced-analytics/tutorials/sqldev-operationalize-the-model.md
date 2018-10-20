---
title: Lección 4 resultados posibles de predicción mediante modelos de R (SQL Server Machine Learning) | Microsoft Docs
description: Tutorial que muestra cómo insertar código de R en SQL Server los procedimientos almacenados y funciones de Transact-SQL
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/19/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 07c99279fdb511f1c6f59e15f83644a89642c176
ms.sourcegitcommit: 3cd6068f3baf434a4a8074ba67223899e77a690b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/19/2018
ms.locfileid: "49462131"
---
# <a name="lesson-4-predict-potential-outcomes-using-an-r-model-in-a-stored-procedure"></a>Lección 4: Predecir resultados posibles con un modelo de R en un procedimiento almacenado
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

En este artículo forma parte de un tutorial para desarrolladores de SQL sobre cómo usar R en SQL Server.

En este paso, aprenderá a usar el modelo con las nuevas observaciones para predecir resultados posibles. El modelo se ajusta en un procedimiento almacenado que se puede llamar directamente por otras aplicaciones. El tutorial muestran varias maneras de realizar la puntuación:

- **Modo de puntuación por lotes**: usar una consulta de selección como entrada al procedimiento almacenado. El procedimiento almacenado devuelve una tabla de observaciones correspondientes a los casos de entrada.

- **Modo de puntuación individual**: pasar un conjunto de valores de parámetros individuales como entrada.  El procedimiento almacenado devuelve una sola fila o valor.

En primer lugar, veremos cómo funcionan las puntuaciones en general.

## <a name="basic-scoring"></a>Puntuaciones básicas

El procedimiento almacenado **PredictTip** muestra la sintaxis básica para ajustar una llamada de predicción en un procedimiento almacenado.

```SQL
CREATE PROCEDURE [dbo].[PredictTip] @inquery nvarchar(max) 
AS 
BEGIN 
  
DECLARE @lmodel2 varbinary(max) = (SELECT TOP 1 model FROM nyc_taxi_models);  
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

## <a name="batch-scoring"></a>Puntuación por lotes

Ahora veamos cómo funciona la puntuación por lotes.

1.  Para empezar se obtiene un conjunto más pequeño de los datos de entrada con el que trabajar. Esta consulta crea una lista de los "Diez mejores" viajes con número de pasajeros y otras características necesarias para realizar una predicción.
  
    ```SQL
    SELECT TOP 10 a.passenger_count AS passenger_count, a.trip_time_in_secs AS trip_time_in_secs, a.trip_distance AS trip_distance, a.dropoff_datetime AS dropoff_datetime, dbo.fnCalculateDistance(pickup_latitude, pickup_longitude, dropoff_latitude,dropoff_longitude) AS direct_distance
    
    FROM (SELECT medallion, hack_license, pickup_datetime, passenger_count,trip_time_in_secs,trip_distance, dropoff_datetime, pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude FROM nyctaxi_sample)a

    LEFT OUTER JOIN

    (SELECT medallion, hack_license, pickup_datetime FROM nyctaxi_sample TABLESAMPLE (70 percent) REPEATABLE (98052)    )b

    ON a.medallion=b.medallion AND a.hack_license=b.hack_license 
    AND a.pickup_datetime=b.pickup_datetime
    WHERE b.medallion IS NULL
    ```

    **Resultados de ejemplo**
    
    ```
    passenger_count   trip_time_in_secs    trip_distance  dropoff_datetime   direct_distance
    1  283 0.7 2013-03-27 14:54:50.000   0.5427964547
    1  289 0.7 2013-02-24 12:55:29.000   0.3797099614
    1  214 0.7 2013-06-26 13:28:10.000   0.6970098661
    ```

    Esta consulta se puede usar como entrada para el procedimiento almacenado, **PredictTipMode**, que se suministra como parte de la descarga.

2. Tómese un minuto para revisar el código del procedimiento almacenado **PredictTipMode** en [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)].

    ```SQL
    /****** Object:  StoredProcedure [dbo].[PredictTipMode]  ******/
    CREATE PROCEDURE [dbo].[PredictTipMode] @inquery nvarchar(max)
    AS
    BEGIN
    DECLARE @lmodel2 varbinary(max) = (SELECT TOP 1 model FROM nyc_taxi_models);
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

    ```SQL
    -- Define the input data
    DECLARE @query_string nvarchar(max)
    SET @query_string='SELECT TOP 10 a.passenger_count as passenger_count, a.trip_time_in_secs AS trip_time_in_secs, a.trip_distance AS trip_distance, a.dropoff_datetime AS dropoff_datetime, dbo.fnCalculateDistance(pickup_latitude, pickup_longitude, dropoff_latitude,dropoff_longitude) AS direct_distance FROM  (SELECT medallion, hack_license, pickup_datetime, passenger_count,trip_time_in_secs,trip_distance, dropoff_datetime, pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude FROM nyctaxi_sample  )a   LEFT OUTER JOIN (SELECT medallion, hack_license, pickup_datetime FROM nyctaxi_sample TABLESAMPLE (70 percent) REPEATABLE (98052))b ON a.medallion=b.medallion AND a.hack_license=b.hack_license AND a.pickup_datetime=b.pickup_datetime WHERE b.medallion is null'

    -- Call the stored procedure for scoring and pass the input data
    EXEC [dbo].[PredictTip] @inquery = @query_string;
    ```
  
4. El procedimiento almacenado devuelve una serie de valores que representan la predicción para cada uno de los viajes en los 10 principales. Sin embargo, los viajes superiores también son único pasajero viajes con una distancia de viaje relativamente corta, para que el controlador no es probable que reciba una propina.
  

> [!TIP]
> 
> En lugar de devolver únicamente el "Sí: propina" y "no-sugerencia" resultados, podría también devolver la puntuación de probabilidad de predicción y, a continuación, aplicar una cláusula WHERE a la _puntuación_ valores de columna para clasificar el resultado como "propina probable" o " propina improbable", con un valor de umbral como 0,5 o 0,7. Este paso no se incluye en el procedimiento almacenado, pero es fácil de implementar.

## <a name="single-row-scoring"></a>Puntuación de fila única

A veces querrá pasar valores individuales de una aplicación y obtener un resultado único basado en esos valores. Por ejemplo, podría configurar una hoja de cálculo de Excel, una aplicación web o un informe de Reporting Services para llamar al procedimiento almacenado y proporcionar entradas escritas o seleccionadas por los usuarios.

En esta sección, aprenderá a crear predicciones únicas mediante un procedimiento almacenado.

1. Tómese un minuto para revisar el código del procedimiento almacenado **PredictTipSingleMode**, que se incluye como parte de la descarga.
  
    ```SQL
    CREATE PROCEDURE [dbo].[PredictTipSingleMode] @passenger_count int = 0, @trip_distance float = 0, @trip_time_in_secs int = 0, @pickup_latitude float = 0, @pickup_longitude float = 0, @dropoff_latitude float = 0, @dropoff_longitude float = 0
    AS
    BEGIN
    DECLARE @inquery nvarchar(max) = N'SELECT * FROM [dbo].[fnEngineerFeatures](@passenger_count, @trip_distance, @trip_time_in_secs,  @pickup_latitude, @pickup_longitude, @dropoff_latitude, @dropoff_longitude)';
    DECLARE @lmodel2 varbinary(max) = (SELECT TOP 1 model FROM nyc_taxi_models);
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
  
    - Este procedimiento almacenado toma varios valores únicos como entrada, como el número de pasajeros, la distancia del viaje y así sucesivamente.
  
        Si se llama al procedimiento almacenado desde una aplicación externa, debe asegurarse de que los datos coinciden con los requisitos del modelo de R. Esto puede incluir asegurarse de que los datos de entrada se pueden convertir a un tipo de datos R o validar el tipo y la longitud de los datos. 
  
    -   El procedimiento almacenado crea una puntuación basada en el modelo almacenado de R.
  
2. Pruébelo, proporcionando los valores manualmente.
  
    Abra una nueva **consulta** ventana y llame al procedimiento almacenado, que proporciona valores para cada uno de los parámetros. Los parámetros representan las columnas de característica que se usa el modelo y son necesarios.

    ```
    EXEC [dbo].[PredictTipSingleMode] @passenger_count = 0,
    @trip_distance = 2.5,
    @trip_time_in_secs = 631,
    @pickup_latitude = 40.763958,
    @pickup_longitude = -73.973373,
    @dropoff_latitude =  40.782139,
    @dropoff_longitude = 73.977303
    ```

    O bien, use este formulario más corto compatibles con [parámetros a un procedimiento almacenado](https://docs.microsoft.com/sql/relational-databases/stored-procedures/specify-parameters):
  
    ```SQL
    EXEC [dbo].[PredictTipSingleMode] 1, 2.5, 631, 40.763958,-73.973373, 40.782139,-73.977303
    ```

3. Los resultados indican que la probabilidad de obtener una sugerencia es baja (cero) en los viajes 10 principales, ya que todos son viajes único pasajero en una distancia relativamente corta.

## <a name="conclusions"></a>Conclusiones

Esto concluye el tutorial. Ahora que ha aprendido a incrustar código R en procedimientos almacenados, puede ampliar estas prácticas para crear modelos de su elección. La integración con [!INCLUDE[tsql](../../includes/tsql-md.md)] hace mucho más fácil la implementación de modelos de R para la predicción y la incorporación del reciclaje de modelos como parte de un flujo de trabajo de datos empresarial.

## <a name="previous-lesson"></a>Lección anterior

[Lección 3: Entrenar y guardar un modelo de R mediante T-SQL](sqldev-train-and-save-a-model-using-t-sql.md)
