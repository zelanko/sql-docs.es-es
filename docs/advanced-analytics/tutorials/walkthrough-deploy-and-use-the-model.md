---
title: Implementar el modelo de R y su uso en SQL (tutorial) | Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 74a5d8b7ac8bd36a6ce76b895b2dde4a07f5ea96
ms.sourcegitcommit: c8f7e9f05043ac10af8a742153e81ab81aa6a3c3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/17/2018
ms.locfileid: "39085357"
---
# <a name="deploy-the-r-model-and-use-it-in-sql"></a>Implementar el modelo de R y su uso en SQL
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

En esta lección, usará los modelos de R en un entorno de producción, mediante una llamada a un modelo entrenado de un procedimiento almacenado. A continuación, puede invocar el procedimiento almacenado de R o cualquier lenguaje de programación de aplicación que admita [!INCLUDE[tsql](../../includes/tsql-md.md)] (por ejemplo, C#, Java, Python, etc.), para usar el modelo para realizar predicciones en observaciones nuevas.

Este ejemplo muestra las dos formas más comunes para usar un modelo de puntuación:

- **Modo de puntuación por lotes** se utiliza cuando es necesario crear varias predicciones muy rápidas, pasando una instancia de SQL de consulta o la tabla como entrada. Se devuelve una tabla de resultados, que puede insertar directamente en una tabla o escribir en un archivo.

- **Modo de puntuación individual** se utiliza cuando se necesita crear predicciones a la vez. Pasar un conjunto de valores individuales para el procedimiento almacenado. Los valores se corresponden con las características en el modelo, que usa el modelo para crear una predicción, o generan otro resultado como un valor de probabilidad. A continuación, puede devolver ese valor a la aplicación o usuario.

## <a name="batch-scoring"></a>Puntuación por lotes

Un procedimiento almacenado para la puntuación de batch se creó cuando ejecutó el script de PowerShell por primera vez. Este procedimiento almacenado, *PredictTipBatchMode*, hace lo siguiente:

- Obtiene un conjunto de datos de entrada como una consulta SQL
- Llama al modelo de regresión logística entrenado que ha guardado en la lección anterior
- Predice la probabilidad de que el controlador Obtiene cualquier sugerencia distinto de cero

1. Tómese un minuto para revisar el script para el procedimiento almacenado, *PredictTipBatchMode*. Ilustra varios aspectos sobre cómo se puede hacer operativo un modelo mediante [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)].
  
    ```tsql
    CREATE PROCEDURE [dbo].[PredictTipBatchMode]
    @input nvarchar(max)
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

    + Utilice una instrucción SELECT para llamar el modelo almacenado desde una tabla SQL. El modelo se recupera de la tabla como **varbinary (max)** datos se almacenan en la variable SQL,  _\@lmodel2_y se pasa como parámetro *mod* al sistema procedimiento almacenado [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md).

    + Los datos que se usan como entradas para la puntuación se define como una consulta SQL y se almacena como una cadena en la variable SQL  _\@entrada_. Cuando se recuperan datos de la base de datos, se almacenan en una trama de datos denominada *InputDataSet*, que es simplemente el nombre predeterminado para los datos de entrada para el [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) procedimiento; se puede definir otro nombre de variable si es necesario mediante el parámetro   *_\@input_data_1_name_*.

    + Para generar las puntuaciones, el procedimiento almacenado llama a la función `rxPredict` de la biblioteca **RevoScaleR** .

    + El valor devuelto, *puntuación*, es la probabilidad, dado el modelo, que el controlador obtiene una sugerencia. Si lo desea, puede aplicar fácilmente algún tipo de filtro para los valores devueltos para clasificarlos en grupos de "sin propina" y "sugerencia".  Por ejemplo, una probabilidad menor que 0,5 significaría que una sugerencia es improbable.
  
2.  Para llamar al procedimiento almacenado en modo por lotes, defina la consulta que se necesita como entrada para el procedimiento almacenado. Esta es la consulta SQL; puede ejecutarlo en SSMS para comprobar que funciona.

    ```SQL
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

3. Use este código de R para crear la cadena de entrada de la consulta SQL:

    ```R
    input <- "N'SELECT TOP 10 a.passenger_count AS passenger_count, a.trip_time_in_secs AS trip_time_in_secs, a.trip_distance AS trip_distance, a.dropoff_datetime AS dropoff_datetime, dbo.fnCalculateDistance(pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude) AS direct_distance FROM (SELECT medallion, hack_license, pickup_datetime, passenger_count,trip_time_in_secs,trip_distance, dropoff_datetime, pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude FROM nyctaxi_sample)a LEFT OUTER JOIN ( SELECT medallion, hack_license, pickup_datetime FROM nyctaxi_sample  tablesample (1 percent) repeatable (98052)  )b ON a.medallion=b.medallion AND a.hack_license=b.hack_license AND  a.pickup_datetime=b.pickup_datetime WHERE b.medallion is null'";
    q <- paste("EXEC PredictTipBatchMode @inquery = ", input, sep="");
    ```

4. Para ejecutar el procedimiento almacenado de R, llame a la **sqlQuery** método de la **RODBC** empaquetar y utilizar la conexión SQL `conn` que definió anteriormente:

    ```R
    sqlQuery (conn, q);
    ```

    Si se produce un error ODBC, compruebe la sintaxis de consulta, y si tiene el número correcto de las comillas. 
    
    Si se produce un error de permisos, asegúrese de que el inicio de sesión tiene la capacidad de ejecutar el procedimiento almacenado.

## <a name="single-row-scoring"></a>Puntuación de fila única

Al llamar al modelo de predicción según una fila por fila, pasar un conjunto de valores que representan las características de cada caso individual. El procedimiento almacenado, a continuación, devuelve una sola predicción o la probabilidad. 

El procedimiento almacenado *PredictTipSingleMode* muestra este enfoque. Toma como entrada varios parámetros que representan valores de característica (por ejemplo, distancia de pasajeros viaje y el número), puntúa estas características mediante el modelo de R almacenado y da como resultado la probabilidad de sugerencia.

1. Si el procedimiento almacenado *PredictTipSingleMode* no se creó la secuencia de comandos de PowerShell inicial, puede ejecutar la siguiente instrucción de Transact-SQL para crearla ahora.

    ```tsql
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

2. En SQL Server Management Studio, puede usar el [!INCLUDE[tsql](../../includes/tsql-md.md)] **EXEC** procedimiento (o **EXECUTE**) para llamar al procedimiento almacenado y pásele las entradas necesarias. Por ejemplo, intente ejecutar esta instrucción en Management Studio:

    ```SQL
    EXEC [dbo].[PredictTipSingleMode] 1, 2.5, 631, 40.763958,-73.973373, 40.782139,-73.977303
    ```

    Los valores pasados aquí son, respectivamente, para las variables _pasajeros\_recuento_, _trip_distance_, _recorridos\_tiempo\_en\_segundos_, _pickup\_latitud_, _pickup\_longitud_, _recogida\_latitud_, y _recogida\_longitud_.

3. Para ejecutar esta misma llamada desde código de R, simplemente hay que definir una variable de R que contiene la llamada de procedimiento almacenado completo, como la siguiente:

    ```R
    q2 = "EXEC PredictTipSingleMode 1, 2.5, 631, 40.763958,-73.973373, 40.782139,-73.977303 ";
    ```

    Los valores pasados aquí son, respectivamente, para las variables _pasajeros\_recuento_, _recorridos\_distancia_, _recorridos\_tiempo\_en\_segundos_, _pickup\_latitud_, _pickup\_longitud_, _recogida\_ latitud_, y _recogida\_longitud_.

4. Llame a `sqlQuery` (desde el **RODBC** paquete) y pase la cadena de conexión, junto con la variable de cadena que contiene la llamada de procedimiento almacenado.

    ```R
    # predict with stored procedure in single mode
    sqlQuery (conn, q2);
    ```

    >[!TIP]
    > Herramientas de R para Visual Studio (RTVS) proporciona una integración excelente con SQL Server y R. Consulte este artículo para obtener más ejemplos del uso de RODBC con una conexión de SQL Server: [trabajar con SQL Server y R](https://docs.microsoft.com/visualstudio/rtvs/sql-server)

## <a name="summary"></a>Resumen

Ahora que ha aprendido cómo trabajar con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] datos y conservar modelos entrenados de R para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], debería ser relativamente fácil crear nuevos modelos basados en este conjunto de datos. Por ejemplo, puede intentar crear estos modelos adicionales:

- Un modelo de regresión que predice la cantidad de propina

- Un modelo de clasificación con múltiples clases que predice si la sugerencia es pequeña, mediana o grande

También se recomienda que revise algunos ejemplos y recursos adicionales:

+ [Escenarios de ciencia de datos y plantillas de soluciones](data-science-scenarios-and-solution-templates.md)

+ [Análisis avanzado en base de datos](sqldev-in-database-r-for-sql-developers.md)

+ [Microsoft R - Diving into Data Analysis](https://msdn.microsoft.com/microsoft-r/data-analysis-in-microsoft-r)

+ [Recursos adicionales](https://msdn.microsoft.com/microsoft-r/microsoft-r-more-resources)

## <a name="previous-lesson"></a>Lección anterior

[Generar un modelo de R y guardarlo en SQL Server](walkthrough-build-and-save-the-model.md)

## <a name="next-steps"></a>Pasos siguientes

[Tutoriales de SQL Server R](sql-server-r-tutorials.md)

[Cómo crear un procedimiento almacenado mediante sqlrutils](../r/how-to-create-a-stored-procedure-using-sqlrutils.md)
