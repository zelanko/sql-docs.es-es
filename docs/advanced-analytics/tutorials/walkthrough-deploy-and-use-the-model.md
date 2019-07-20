---
title: Implementar un modelo de R para las predicciones en SQL Server
description: Tutorial que muestra cómo implementar un modelo de R en SQL Server para el análisis en bases de datos.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/26/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.openlocfilehash: 2cb6bf28fa849e2015d111c564bb0af84f103d19
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/19/2019
ms.locfileid: "68345859"
---
# <a name="deploy-the-r-model-and-use-it-in-sql-server-walkthrough"></a>Implementar el modelo de R y usarlo en SQL Server (tutorial)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

En esta lección, aprenderá a implementar modelos de R en un entorno de producción mediante una llamada a un modelo entrenado desde un procedimiento almacenado. Puede invocar el procedimiento almacenado desde R o cualquier lenguaje de programación de aplicaciones [!INCLUDE[tsql](../../includes/tsql-md.md)] que admita ( C#como Java, Python, etc.) y usar el modelo para realizar predicciones en nuevas observaciones.

En este artículo se muestran las dos formas más comunes de usar un modelo en la puntuación:

> [!div class="checklist"]
> * El **modo de puntuación por lotes** genera varias predicciones
> * El **modo de puntuación individual** genera predicciones de una en una

## <a name="batch-scoring"></a>Puntuación por lotes

Cree un procedimiento almacenado, *PredictTipBatchMode*, que genere varias predicciones, pasando una consulta o tabla SQL como entrada. Se devuelve una tabla de resultados, que puede insertar directamente en una tabla o escribir en un archivo.

- Obtiene un conjunto de datos de entrada como una consulta SQL
- Llama al modelo de regresión logística entrenado que ha guardado en la lección anterior
- Predice la probabilidad de que el controlador obtenga cualquier sugerencia distinta de cero

1. En Management Studio, abra una nueva ventana de consulta y ejecute el siguiente script de T-SQL para crear el procedimiento almacenado PredictTipBatchMode.
  
    ```sql
    USE [NYCTaxi_Sample]
    GO

    SET ANSI_NULLS ON
    GO
    SET QUOTED_IDENTIFIER ON
    GO

    IF EXISTS (SELECT * FROM sys.objects WHERE type = 'P' AND name = 'PredictTipBatchMode')
    DROP PROCEDURE v
    GO

    CREATE PROCEDURE [dbo].[PredictTipBatchMode] @input nvarchar(max)
    AS
    BEGIN
      DECLARE @lmodel2 varbinary(max) = (SELECT TOP 1 model  FROM nyc_taxi_models);
      EXEC sp_execute_external_script @language = N'R',
         @script = N'
           mod <- unserialize(as.raw(model));
           print(summary(mod))
           OutputDataSet<-rxPredict(modelObject = mod,
             data = InputDataSet,
             outData = NULL,
             predVarNames = "Score", type = "response",
             writeModelVars = FALSE, overwrite = TRUE);
           str(OutputDataSet)
           print(OutputDataSet)',
      @input_data_1 = @input,
      @params = N'@model varbinary(max)',
      @model = @lmodel2
      WITH RESULT SETS ((Score float));
    END
    ```

    + Use una instrucción SELECT para llamar al modelo almacenado desde una tabla SQL. El modelo se recupera de la tabla como datos **varbinary (Max)** , se almacena en la variable  _\@SQL lmodel2_, y se pasa como el parámetro *mod* al procedimiento almacenado del sistema [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md).

    + Los datos que se usan como entradas para la puntuación se definen como una consulta SQL y se almacenan como una cadena en la  _\@entrada_de variable de SQL. A medida que se recuperan datos de la base de datos, se almacenan en una trama de datos denominada *InputDataSet*, que es solo el nombre predeterminado para los datos de entrada en el procedimiento [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) . puede definir otro nombre de variable si es necesario mediante el parámetro  *_\@input_data_1_name_* .

    + Para generar las puntuaciones, el procedimiento almacenado llama a la función rxPredict de la biblioteca **RevoScaleR** .

    + El valor devuelto, *score*, es la probabilidad, dado el modelo, que el controlador obtiene una sugerencia. Opcionalmente, puede aplicar fácilmente algún tipo de filtro a los valores devueltos para clasificar los valores devueltos en los grupos "TIP" y "sin propina".  Por ejemplo, una probabilidad de menos de 0,5 significaría que una sugerencia es improbable.
  
2.  Para llamar al procedimiento almacenado en el modo por lotes, defina la consulta requerida como entrada para el procedimiento almacenado. A continuación se muestra la consulta SQL, que puede ejecutar en SSMS para comprobar que funciona.

    ```sql
    SELECT TOP 10
      a.passenger_count AS passenger_count,
      a.trip_time_in_secs AS trip_time_in_secs,
      a.trip_distance AS trip_distance,
      a.dropoff_datetime AS dropoff_datetime,
      dbo.fnCalculateDistance( pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude) AS direct_distance
      FROM 
        (SELECT medallion, hack_license, pickup_datetime, passenger_count,trip_time_in_secs,trip_distance, dropoff_datetime, pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude 
        FROM nyctaxi_sample)a 
      LEFT OUTER JOIN
      ( SELECT medallion, hack_license, pickup_datetime
      FROM nyctaxi_sample  tablesample (1 percent) repeatable (98052)  )b
      ON a.medallion=b.medallion
      AND a.hack_license=b.hack_license
      AND a.pickup_datetime=b.pickup_datetime
      WHERE b.medallion is null
    ```

3. Use este código R para crear la cadena de entrada a partir de la consulta SQL:

    ```R
    input <- "N'SELECT TOP 10 a.passenger_count AS passenger_count, a.trip_time_in_secs AS trip_time_in_secs, a.trip_distance AS trip_distance, a.dropoff_datetime AS dropoff_datetime, dbo.fnCalculateDistance(pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude) AS direct_distance FROM (SELECT medallion, hack_license, pickup_datetime, passenger_count,trip_time_in_secs,trip_distance, dropoff_datetime, pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude FROM nyctaxi_sample)a LEFT OUTER JOIN ( SELECT medallion, hack_license, pickup_datetime FROM nyctaxi_sample  tablesample (1 percent) repeatable (98052)  )b ON a.medallion=b.medallion AND a.hack_license=b.hack_license AND  a.pickup_datetime=b.pickup_datetime WHERE b.medallion is null'";
    q <- paste("EXEC PredictTipBatchMode @inquery = ", input, sep="");
    ```

4. Para ejecutar el procedimiento almacenado desde R, llame al método **sqlquery** del paquete **RODBC** y use la conexión `conn` SQL que definió anteriormente:

    ```R
    sqlQuery (conn, q);
    ```

    Si obtiene un error ODBC, compruebe si hay errores de sintaxis y si tiene el número correcto de Comillas. 
    
    Si obtiene un error de permisos, asegúrese de que el inicio de sesión tiene la capacidad de ejecutar el procedimiento almacenado.

## <a name="single-row-scoring"></a>Puntuación de fila única

El modo de puntuación individual genera predicciones de una en una, pasando un conjunto de valores individuales al procedimiento almacenado como entrada. Los valores corresponden a las características del modelo, que el modelo usa para crear una predicción, o generar otro resultado, como un valor de probabilidad. A continuación, puede devolver ese valor a la aplicación o usuario.

Cuando se llama al modelo para la predicción fila a fila, se pasa un conjunto de valores que representan características para cada caso individual. Después, el procedimiento almacenado devuelve una sola predicción o probabilidad. 

El procedimiento almacenado *PredictTipSingleMode* muestra este enfoque. Toma como entrada varios parámetros que representan valores de características (por ejemplo, recuento de pasajeros y distancia de viaje), Puntua estas características con el modelo de R almacenado y genera la probabilidad de la sugerencia.

1. Ejecute la siguiente instrucción Transact-SQL para crear el procedimiento almacenado.

    ```sql
    USE [NYCTaxi_Sample]
    GO

    SET ANSI_NULLS ON
    GO
    SET QUOTED_IDENTIFIER ON
    GO

    IF EXISTS (SELECT * FROM sys.objects WHERE type = 'P' AND name = 'PredictTipSingleMode')
    DROP PROCEDURE v
    GO

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
        SELECT * FROM [dbo].[fnEngineerFeatures](@passenger_count, @trip_distance, @trip_time_in_secs, @pickup_latitude, @pickup_longitude, @dropoff_latitude, @dropoff_longitude)'
      DECLARE @lmodel2 varbinary(max) = (SELECT TOP 1 model FROM nyc_taxi_models);

      EXEC sp_execute_external_script @language = N'R',  @script = N'
            mod <- unserialize(as.raw(model));
            print(summary(mod))
            OutputDataSet<-rxPredict(
              modelObject = mod,
              data = InputDataSet,
              outData = NULL,
              predVarNames = "Score",
              type = "response",
              writeModelVars = FALSE,
              overwrite = TRUE);
            str(OutputDataSet)
            print(OutputDataSet)
            ',
      @input_data_1 = @inquery,
      @params = N'
      -- passthrough columns
      @model varbinary(max) ,
      @passenger_count int ,
      @trip_distance float ,
      @trip_time_in_secs int ,
      @pickup_latitude float ,
      @pickup_longitude float ,
      @dropoff_latitude float ,
      @dropoff_longitude float',
      -- mapped variables
      @model = @lmodel2 ,
      @passenger_count =@passenger_count ,
      @trip_distance=@trip_distance ,
      @trip_time_in_secs=@trip_time_in_secs ,
      @pickup_latitude=@pickup_latitude ,
      @pickup_longitude=@pickup_longitude ,
      @dropoff_latitude=@dropoff_latitude ,
      @dropoff_longitude=@dropoff_longitude
      WITH RESULT SETS ((Score float));
    END
    ```

2. En SQL Server Management Studio, puede usar el [!INCLUDE[tsql](../../includes/tsql-md.md)] procedimiento **exec** (o **Ejecutar**) para llamar al procedimiento almacenado y pasarle las entradas necesarias. Por ejemplo, intente ejecutar esta instrucción en Management Studio:

    ```sql
    EXEC [dbo].[PredictTipSingleMode] 1, 2.5, 631, 40.763958,-73.973373, 40.782139,-73.977303
    ```

    Los valores pasados aquí son, respectivamente, para las variables _recuento\_de pasajeros_, _trip_distance_, _tiempo\_de\_ida y vuelta\_en segundos_, _recogida\_de latitud_, _longitud\_de recogida_, _recogida\_de latitud_y _longitud\_de recogida_.

3. Para ejecutar esta misma llamada desde código R, solo tiene que definir una variable de R que contenga toda la llamada a procedimiento almacenado, como esta:

    ```R
    q2 = "EXEC PredictTipSingleMode 1, 2.5, 631, 40.763958,-73.973373, 40.782139,-73.977303 ";
    ```

    Los valores pasados aquí son, respectivamente, para las variables _recuento\_de pasajeros_, _distancia de viaje\__ , _tiempo\_\_de ida y vuelta\_en segundos_, _recogida\_ latitud_, _longitud\_de recogida_, _recogida\_de latitud_y _longitud\_de recogida_.

4. Llame `sqlQuery` a (desde el paquete **RODBC** ) y pase la cadena de conexión, junto con la variable de cadena que contiene la llamada al procedimiento almacenado.

    ```R
    # predict with stored procedure in single mode
    sqlQuery (conn, q2);
    ```

    >[!TIP]
    > Herramientas de R para Visual Studio (RTVS) proporciona una excelente integración con SQL Server y R. Consulte este artículo para obtener más ejemplos del uso de RODBC con una conexión SQL Server: [Trabajar con SQL Server y R](https://docs.microsoft.com/visualstudio/rtvs/sql-server)

## <a name="next-steps"></a>Pasos siguientes

Ahora que ha aprendido a trabajar con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] datos y a conservar modelos entrenados de R en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], debe ser relativamente fácil crear nuevos modelos basados en este conjunto de datos. Por ejemplo, puede intentar crear estos modelos adicionales:

+ Un modelo de regresión que predice la cantidad de propina
+ Un modelo de clasificación multiclase que predice si la propina es grande, mediana o pequeña

Es posible que también desee explorar estos ejemplos y recursos adicionales:

+ [Escenarios de ciencia de datos y plantillas de soluciones](data-science-scenarios-and-solution-templates.md)
+ [Análisis avanzado en base de datos](sqldev-in-database-r-for-sql-developers.md)
+ [Guías de procedimientos Machine Learning Server](https://docs.microsoft.com/machine-learning-server/r/how-to-introduction)
+ [Machine Learning Server recursos adicionales](https://docs.microsoft.com//machine-learning-server/resources-more)
