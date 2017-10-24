---
title: "Lección 6: Poner el modelo R | Documentos de Microsoft"
ms.custom: 
ms.date: 08/23/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
dev_langs:
- R
- TSQL
ms.assetid: 52b05828-11f5-4ce3-9010-59c213a674d1
caps.latest.revision: 11
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: f0fbdebc582650b0bd524d583d936848ae42e5f6
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="lesson-6-operationalize-the-r-model"></a>Lección 6: Poner el modelo R

Este artículo forma parte de un tutorial para desarrolladores de SQL sobre cómo usar R en SQL Server.

En este paso, aprenderá a *poner* del modelo mediante un procedimiento almacenado. Este procedimiento almacenado se puede llamar directamente por otras aplicaciones, para realizar predicciones en nuevas observaciones. El tutorial muestran dos maneras de realizar puntuaciones con un modelo de R en un procedimiento almacenado:

- **Modo de puntuación de lotes**: utilizar una consulta de selección como una entrada para el procedimiento almacenado. El procedimiento almacenado devuelve una tabla de observaciones correspondientes a los casos de entrada.

- **Modo de puntuación individual**: pasar un conjunto de valores de parámetros individuales como entrada.  El procedimiento almacenado devuelve una sola fila o valor.

En primer lugar, veremos cómo funcionan las puntuaciones en general.

## <a name="basic-scoring"></a>La puntuación básica

El procedimiento almacenado _PredictTip_ muestra la sintaxis básica para ajustar una llamada de predicción en un procedimiento almacenado.

```SQL
CREATE PROCEDURE [dbo].[PredictTip] @inquery nvarchar(max)  
AS  
BEGIN  
  
  DECLARE @lmodel2 varbinary(max) = (SELECT TOP 1 model  
  FROM nyc_taxi_models);  
  EXEC sp_execute_external_script @language = N'R',  
                                  @script = N'  
mod <- unserialize(as.raw(model));  
print(summary(mod))  
OutputDataSet<-rxPredict(modelObject = mod, data = InputDataSet, outData = NULL,   
          predVarNames = "Score", type = "response", writeModelVars = FALSE, overwrite = TRUE);  
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

- La instrucción SELECT obtiene el modelo serializado de la base de datos y lo almacena en la variable de R `mod` para su posterior procesamiento con R.

- Se obtienen los nuevos casos de la puntuación de la [!INCLUDE[tsql](../../includes/tsql-md.md)] consulta especificada en `@inquery`, el primer parámetro del procedimiento almacenado. Cuando se leen los datos de la consulta, las filas se guardan en la trama de datos predeterminada, `InputDataSet`. Esta trama de datos se pasa a la función `rxPredict` de R, que genera las puntuaciones.
  
    `OutputDataSet<-rxPredict(modelObject = mod, data = InputDataSet, outData = NULL,            predVarNames = "Score", type = "response", writeModelVars = FALSE, overwrite = TRUE);`
  
    Como data.frame puede contener una sola fila, puede usar el mismo código para la puntuación individual o por lotes.
  
-   El valor devuelto por la `rxPredict` función es un **float** que representa la probabilidad de que el controlador Obtenga una sugerencia de cualquier cantidad.

## <a name="batch-scoring"></a>La puntuación del lote

Ahora veamos cómo funciona la puntuación por lotes.

1.  Para empezar se obtiene un conjunto más pequeño de los datos de entrada con el que trabajar. Esta consulta crea una lista de los "Diez mejores" viajes con número de pasajeros y otras características necesarias para realizar una predicción.
  
    ```SQL
    SELECT TOP 10 a.passenger_count AS passenger_count,
        a.trip_time_in_secs AS trip_time_in_secs, 
        a.trip_distance AS trip_distance, 
        a.dropoff_datetime AS dropoff_datetime, 
        dbo.fnCalculateDistance(pickup_latitude, pickup_longitude, dropoff_latitude,dropoff_longitude) AS direct_distance
    FROM
    (
        SELECT medallion, hack_license, pickup_datetime, passenger_count,trip_time_in_secs,trip_distance,
         dropoff_datetime, pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude FROM nyctaxi_sample)a
    LEFT OUTERJOIN
    (
    SELECT medallion, hack_license, pickup_datetime
    FROM nyctaxi_sample
    TABLESAMPLE (70 percent) REPEATABLE (98052)
    )b
    ON a.medallion=b.medallion AND a.hack_license=b.hack_license 
    AND a.pickup_datetime=b.pickup_datetime  
    WHERE b.medallion IS NULL
    ```

    **Resultados del ejemplo**
    
    ```
    passenger_count   trip_time_in_secs    trip_distance  dropoff_datetime   direct_distance
    1  283 0.7 2013-03-27 14:54:50.000   0.5427964547
    1  289 0.7 2013-02-24 12:55:29.000   0.3797099614
    1  214 0.7 2013-06-26 13:28:10.000   0.6970098661
    ```

    Esta consulta se puede usar como entrada para el procedimiento almacenado, _PredictTipBatchMode_, se proporciona como parte de la descarga.

2. Dedique un minuto a revisar el código del procedimiento almacenado _PredictTipBatchMode_ en [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)].

    ```SQL
    /****** Object:  StoredProcedure [dbo].[PredictTipBatchMode]  ******/
    CREATE PROCEDURE [dbo].[PredictTipBatchMode] @inquery nvarchar(max)
    AS
    BEGIN
      DECLARE @lmodel2 varbinary(max) = (SELECT TOP 1 model
      FROM nyc_taxi_models);
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
    ```

3.  Proporcione el texto de consulta en una variable y pasarla como un parámetro al procedimiento almacenado:

    ```SQL
    -- Define the input data
    DECLARE @query_string nvarchar(max)
    SET @query_string='
    select top 10 a.passenger_count as passenger_count,
        a.trip_time_in_secs as trip_time_in_secs,
        a.trip_distance as trip_distance,
        a.dropoff_datetime as dropoff_datetime,
        dbo.fnCalculateDistance(pickup_latitude, pickup_longitude, dropoff_latitude,dropoff_longitude) as direct_distance
    from
        select medallion, hack_license, pickup_datetime, passenger_count,trip_time_in_secs,trip_distance,
            dropoff_datetime, pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude
        from nyctaxi_sample
    )a  
    LEFT OUTER JOIN
    (
    SELECT medallion, hack_license, pickup_datetime
    FROM nyctaxi_sample  
    TABLESAMPLE (70 percent) REPEATABLE (98052)
    )b 
    ON a.medallion=b.medallion AND a.hack_license=b.hack_license AND a.pickup_datetime=b.pickup_datetime  
    WHERE b.medallion is null'

    -- Call the stored procedure for scoring and pass the input data
    EXEC [dbo].[PredictTip] @inquery = @query_string;
    ```
  
4. El procedimiento almacenado devuelve una serie de valores que representan la predicción para cada uno de los viajes de diez. Sin embargo, los viajes superiores también son viajes de pasajeros único con una distancia relativamente cortas de ida y vuelta, para que el controlador no es probable que obtener una sugerencia.
  

> [!TIP]
> 
> En lugar de devolver resultados de tipo propina sí/propina no, podría también devolver la puntuación de probabilidad de la predicción y, después, aplicar una cláusula WHERE a los valores de la columna _Score_ para clasificar el resultado como "propina probable" o "propina improbable", con un valor de umbral como 0,5 o 0,7. Este paso no se incluye en el procedimiento almacenado, pero es fácil de implementar.

## <a name="single-row-scoring"></a>Puntuación de varias filas

A veces querrá pasar valores individuales de una aplicación y obtener un resultado único basado en esos valores. Por ejemplo, podría configurar una hoja de cálculo de Excel, una aplicación web o un informe de Reporting Services para llamar al procedimiento almacenado y proporcionar entradas escritas o seleccionadas por los usuarios.

En esta sección, aprenderá a crear predicciones únicas mediante un procedimiento almacenado.

1. Tómese un minuto para revisar el código del procedimiento almacenado _PredictTipSingleMode_, que se incluye como parte de la descarga.
  
    ```SQL
    CREATE PROCEDURE [dbo].[PredictTipSingleMode] @passenger_count int = 0,
    @trip_distance float = 0,
    @trip_time_in_secs int = 0,
    @pickup_latitude float = 0,
    @pickup_longitude float = 0,
    @dropoff_latitude float = 0,
    @dropoff_longitude float = 0
    AS  
    BEGIN  
      DECLARE @inquery nvarchar(max) = N'  
      SELECT * FROM [dbo].[fnEngineerFeatures](@passenger_count,  
    @trip_distance,  
    @trip_time_in_secs,  
    @pickup_latitude,  
    @pickup_longitude,  
    @dropoff_latitude,  
    @dropoff_longitude)  
        '  
      DECLARE @lmodel2 varbinary(max) = (SELECT TOP 1 model  
      FROM nyc_taxi_models);  
      EXEC sp_execute_external_script @language = N'R',  
                                      @script = N'  
    mod <- unserialize(as.raw(model));  
    print(summary(mod))  
    OutputDataSet<-rxPredict(modelObject = mod, data = InputDataSet, outData = NULL,   
              predVarNames = "Score", type = "response", writeModelVars = FALSE, overwrite = TRUE);  
    str(OutputDataSet)  
    print(OutputDataSet)  
    ',  
    @input_data_1 = @inquery,  
    @params = N'@model varbinary(max),@passenger_count int,@trip_distance float,@trip_time_in_secs int ,  
    @pickup_latitude float ,@pickup_longitude float ,@dropoff_latitude float ,@dropoff_longitude float',  
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
    ```
  
    - Este procedimiento almacenado toma varios valores únicos como entrada, como el número de pasajeros, la distancia del viaje y así sucesivamente.
  
        Si llama al procedimiento almacenado desde una aplicación externa, asegúrese de que los datos coinciden con los requisitos del modelo de R. Esto puede incluir asegurarse de que los datos de entrada se pueden convertir a un tipo de datos R o validar el tipo y la longitud de los datos. Para obtener más información, consulte [Trabajar con tipos de datos de R](https://msdn.microsoft.com/library/mt590948.aspx).
  
    -   El procedimiento almacenado crea una puntuación basada en el modelo almacenado de R.
  
2. Pruébelo, proporcionando los valores manualmente.
  
    Abra una nueva **consulta** ventana y llame al procedimiento almacenado para proporcionar valores para cada uno de los parámetros. Los parámetros representan las columnas de característica usadas por el modelo y son necesarios.

    ```
    EXEC [dbo].[PredictTipSingleMode] @passenger_count = 0,
    @trip_distance float = 2.5,
    @trip_time_in_secs int = 631,
    @pickup_latitude float = 40.763958,
    @pickup_longitude float = -73.973373,
    @dropoff_latitude float =  40.782139,
    @dropoff_longitude float = 73.977303
    ```

    O bien, use este formato más corto compatible para [parámetros a un procedimiento almacenado](https://docs.microsoft.com/sql/relational-databases/stored-procedures/specify-parameters):
  
    ```SQL
    EXEC [dbo].[PredictTipSingleMode] 1, 2.5, 631, 40.763958,-73.973373, 40.782139,-73.977303
    ```

3. Los resultados indican que la probabilidad de obtener una sugerencia es muy baja en estas 10 viajes superiores, puesto que todos son viajes de pasajeros único en una distancia relativamente corta.

## <a name="conclusions"></a>Conclusiones

Esto concluye el tutorial. Ahora que ha aprendido a incrustar código R en los procedimientos almacenados, puede ampliar estas prácticas para generar modelos de su elección. La integración con [!INCLUDE[tsql](../../includes/tsql-md.md)] hace mucho más fácil la implementación de modelos de R para la predicción y la incorporación del reciclaje de modelos como parte de un flujo de trabajo de datos empresarial.

## <a name="previous-lesson"></a>Lección anterior

[Lección 5: Entrenar y guardar un modelo de R con T-SQL](../r/sqldev-train-and-save-a-model-using-t-sql.md)

