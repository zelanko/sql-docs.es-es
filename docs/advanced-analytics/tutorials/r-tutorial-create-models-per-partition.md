---
title: Tutorial sobre cómo crear, entrenar y puntuar modelos en función de partición en R - SQL Server Machine Learning Services
description: Aprenda a modelar, entrenar y usar datos con particiones que se crean dinámicamente al usar las funcionalidades de modelado basado en la partición del aprendizaje automático de SQL Server.
ms.custom: sqlseattle
ms.prod: sql
ms.technology: machine-learning
ms.date: 03/27/2018
ms.topic: tutorial
ms.author: heidist
author: HeidiSteen
manager: cgronlun
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: abe7dbe193cc4e5f90095e7764f35aa1dc0cd9bf
ms.sourcegitcommit: 2db83830514d23691b914466a314dfeb49094b3c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/27/2019
ms.locfileid: "58493337"
---
# <a name="tutorial-create-partition-based-models-in-r-on-sql-server"></a>Tutorial: Crear modelos basados en la partición en R en SQL Server
[!INCLUDE[appliesto-ssvnex-xxxx-xxxx-xxx-md-winonly](../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

En SQL Server 2019, modelado basado en la partición es la capacidad para crear y entrenar modelos de datos con particiones. Para los datos estratificados que segmenta naturalmente en un esquema de clasificación determinada - como las regiones geográficas, fecha y hora, edad o género - puede ejecutar el script en todo el conjunto de datos, con la capacidad de modelar, entrenar y puntuar a través de particiones que permanecen intactas a través de todas estas operaciones. 

Modelado basado en la partición se habilita a través de dos parámetros nuevos en [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql):

+ **input_data_1_partition_by_columns**, que especifica una columna a partición por.
+ **input_data_1_order_by_columns** especifica qué columnas de order by. 

En este tutorial, aprenderá modelado basado en la partición con los datos de ejemplo de taxi de nueva clásicos y script de R. La columna de partición es el método de pago.

> [!div class="checklist"]
> * Las particiones se basan en tipos de pago (5).
> * Crear y entrenar modelos en cada partición y almacenar los objetos en la base de datos.
> * Predecir la probabilidad de que los resultados de la sugerencia a través de cada modelo de partición, con datos de ejemplo que se reserva para ese propósito.

## <a name="prerequisites"></a>Requisitos previos
 
Para completar este tutorial, debe tener lo siguiente:

+ Suficientes recursos del sistema. El conjunto de datos es grande y las operaciones de aprendizaje son que consumen muchos recursos. Si es posible, utilice un sistema que tenga al menos 8 GB de RAM. Como alternativa, puede usar conjuntos de datos más pequeños para evitar las restricciones de recursos. Instrucciones para reducir el conjunto de datos están en línea. 

+ Una herramienta para Transact-SQL, la ejecución de consulta como [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).

+ [NYCTaxi_Sample.bak](https://sqlmldoccontent.blob.core.windows.net/sqlml/NYCTaxi_Sample.bak), que puede [descargue y restaure](demo-data-nyctaxi-in-sql.md) a la instancia del motor de base de datos local. Tamaño del archivo es de aproximadamente 90 MB.

+ SQL Server 2019 preview base de datos instancia del motor, con la integración de Machine Learning Services y R.

Comprobar la versión ejecutando **`SELECT @@Version`** como una consulta de Transact-SQL en una herramienta de consulta. Salida debe ser "Microsoft SQL Server (CTP 2.4) - 2019 15.0".

Compruebe la disponibilidad de los paquetes de R al devolver una lista de todos los paquetes de R instalados actualmente con la instancia del motor de base de datos tiene el formato correcto:

```sql
EXECUTE sp_execute_external_script
  @language=N'R',
  @script = N'str(OutputDataSet);
  packagematrix <- installed.packages();
  Name <- packagematrix[,1];
  Version <- packagematrix[,3];
  OutputDataSet <- data.frame(Name, Version);',
  @input_data_1 = N''
WITH RESULT SETS ((PackageName nvarchar(250), PackageVersion nvarchar(max) ))
```

## <a name="connect-to-the-database"></a>Conectarse a la base de datos

Inicie Management Studio y conéctese a la instancia del motor de base de datos. En el Explorador de objetos, compruebe el [NYCTaxi_Sample database](demo-data-nyctaxi-in-sql.md) existe. 

## <a name="create-calculatedistance"></a>Crear CalculateDistance

La base de datos de demostración incluye una función escalar para el cálculo de distancia, pero nuestro mejor funciona el procedimiento almacenado con una función con valores de tabla. Ejecute el siguiente script para crear el **CalculateDistance** función utilizada en el [paso entrenamiento](#training-step) más adelante.

Para confirmar que se creó la función, compruebe las funciones \Programmability\Functions\Table-valued bajo el **NYCTaxi_Sample** base de datos en el Explorador de objetos.

```sql
USE NYCTaxi_sample
GO

SET ANSI_NULLS ON
GO

SET QUOTED_IDENTIFIER ON
GO

CREATE FUNCTION [dbo].[CalculateDistance] (
    @Lat1 FLOAT
    ,@Long1 FLOAT
    ,@Lat2 FLOAT
    ,@Long2 FLOAT
    )
    -- User-defined function calculates the direct distance between two geographical coordinates.
RETURNS TABLE
AS
RETURN

SELECT COALESCE(3958.75 * ATAN(SQRT(1 - POWER(t.distance, 2)) / nullif(t.distance, 0)), 0) AS direct_distance
FROM (
    VALUES (CAST((SIN(@Lat1 / 57.2958) * SIN(@Lat2 / 57.2958)) + (COS(@Lat1 / 57.2958) * COS(@Lat2 / 57.2958) * COS((@Long2 / 57.2958) - (@Long1 / 57.2958))) AS DECIMAL(28, 10)))
    ) AS t(distance)
GO
 ```

## <a name="define-a-procedure-for-creating-and-training-per-partition-models"></a>Defina un procedimiento para crear y entrenar modelos de por partición

Este tutorial incluye scripts de R en un procedimiento almacenado. En este paso, creará un procedimiento almacenado que usa R para crear un conjunto de datos de entrada, un modelo de clasificación para predecir los resultados de la sugerencia de compilación y, a continuación, almacena el modelo en la base de datos.

Entre las entradas de parámetro utilizadas por esta secuencia de comandos, verá **input_data_1_partition_by_columns** y **input_data_1_order_by_columns**. Recuerde que estos parámetros son el mecanismo por el cual particiones modelado se produce. Los parámetros se pasan como entradas para [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) para procesar las particiones con el script externo ejecuta una vez para cada partición. 

Para este procedimiento almacenado, [usar el paralelismo](#parallel) para reducir el tiempo hasta su finalización.

Después de ejecutar este script, debería ver **train_rxLogIt_per_partition** en procedimientos \Programmability\Stored bajo el **NYCTaxi_Sample** base de datos en el Explorador de objetos. También verá una nueva tabla usada para almacenar modelos: **dbo.nyctaxi_models**.

```sql
USE NYCTaxi_Sample
GO

CREATE
    OR

ALTER PROCEDURE [dbo].[train_rxLogIt_per_partition] (@input_query NVARCHAR(max))
AS
BEGIN
    DECLARE @start DATETIME2 = SYSDATETIME()
        ,@model_generation_duration FLOAT
        ,@model VARBINARY(max)
        ,@instance_name NVARCHAR(100) = @@SERVERNAME
        ,@database_name NVARCHAR(128) = db_name();

    EXEC sp_execute_external_script @language = N'R'
        ,@script = 
        N'
    
    # Make sure InputDataSet is not empty. In parallel mode, if one thread gets zero data, an error occurs
    if (nrow(InputDataSet) > 0) {
    # Define the connection string
    connStr <- paste("Driver=SQL Server;Server=", instance_name, ";Database=", database_name, ";Trusted_Connection=true;", sep="");
    
    # build classification model to predict a tip outcome
    duration <- system.time(logitObj <- rxLogit(tipped ~ passenger_count + trip_distance + trip_time_in_secs + direct_distance, data = InputDataSet))[3];

    # First, serialize a model to and put it into a database table
    modelbin <- as.raw(serialize(logitObj, NULL));

    # Create the data source. To reduce data size, add rowsPerRead=500000 to cut the dataset by half.
    ds <- RxOdbcData(table="ml_models", connectionString=connStr);

    # Store the model in the database
    model_name <- paste0("nyctaxi.", InputDataSet[1,]$payment_type);
    
    rxWriteObject(ds, model_name, modelbin, version = "v1",
    keyName = "model_name", valueName = "model_object", versionName = "model_version", overwrite = TRUE, serialize = FALSE);
    } 
    
    '
        ,@input_data_1 = @input_query
        ,@input_data_1_partition_by_columns = N'payment_type'
        ,@input_data_1_order_by_columns = N'passenger_count'
        ,@parallel = 1
        ,@params = N'@instance_name nvarchar(100), @database_name nvarchar(128)'
        ,@instance_name = @instance_name
        ,@database_name = @database_name
    WITH RESULT SETS NONE
END;
GO
```

<a name="parallel"></a>

### <a name="parallel-execution"></a>Ejecución en paralelo

Tenga en cuenta que el [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) entradas incluyen  **@parallel= 1**, que se usa para habilitar el procesamiento en paralelo. A diferencia de las versiones anteriores, en SQL Server de 2019, establecer  **@parallel= 1** ofrece una sugerencia más sólida para el optimizador de consultas, hacer un resultado mucho más probable que la ejecución en paralelo.

De forma predeterminada, el optimizador de consultas suele funcionar en  **@parallel= 1** en las tablas que tienen más de 256 filas, pero si puede controlarlo explícitamente estableciendo  **@parallel= 1** tal como se muestra en este secuencia de comandos.

> [!Tip]
> Para entrenamiento workoads, puede usar **@parallel** con los scripts de entrenamiento arbitrario, incluso aquellas que usan algoritmos de rx que no sean de Microsoft. Normalmente, solo los algoritmos RevoScaleR (con el prefijo rx) ofrecen paralelismo en escenarios de formación en SQL Server. Pero con el nuevo parámetro, puede paralelizar una secuencia de comandos que llama a funciones, incluidas las funciones de R de código abierto, no específicamente diseñadas con esa capacidad. Esto funciona porque las particiones tienen afinidad de subprocesos específicos, por lo que todas las operaciones que se llama en una secuencia de comandos se ejecutan en una base por partición, en el subproceso.

<a name="training-step"></a>

## <a name="run-the-procedure-and-train-the-model"></a>Ejecutar el procedimiento y entrenar el modelo

En esta sección, la secuencia de comandos entrena el modelo que ha creado y guardado en el paso anterior. Los ejemplos siguientes muestran dos enfoques para entrenar el modelo: mediante un conjunto de datos o un datos parciales. 

Esperar a que este paso para llevar cierto tiempo. El entrenamiento es computacionalmente intensivo, tomar varios minutos en completarse. Si los recursos del sistema, especialmente en memoria, no son suficientes para la carga, use un subconjunto de los datos. El segundo ejemplo proporciona la sintaxis.

```sql
--Example 1: train on entire dataset
EXEC train_rxLogIt_per_partition N'
SELECT payment_type, tipped, passenger_count, trip_time_in_secs, trip_distance, d.direct_distance
  FROM dbo.nyctaxi_sample CROSS APPLY [CalculateDistance](pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) as d
';
GO
```

```sql
--Example 2: Train on 20 percent of the dataset to expedite processing.
EXEC train_rxLogIt_per_partition N'
  SELECT tipped, payment_type, passenger_count, trip_time_in_secs, trip_distance, d.direct_distance
  FROM dbo.nyctaxi_sample TABLESAMPLE (20 PERCENT) REPEATABLE (98074)
  CROSS APPLY [CalculateDistance](pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) as d
';
GO
```

> [!NOTE]
> Si está ejecutando otras cargas de trabajo, puede anexar `OPTION(MAXDOP 2)` a la instrucción SELECT, si desea limitar el procesamiento de consulta a solo 2 núcleos.

## <a name="check-results"></a>Comprobar resultados

El resultado de la tabla de modelos debe ser cinco modelos diferentes, en función de cinco particiones segmentadas por los tipos de pago de cinco. Los modelos se encuentran en el **ml_models** origen de datos.

```sql
SELECT *
FROM ml_models
```
 
## <a name="define-a-procedure-for-predicting-outcomes"></a>Defina un procedimiento para predecir resultados

Puede usar los mismos parámetros para la puntuación. El siguiente ejemplo contiene un script de R que se puntuar usando el modelo correcto para la partición que se está procesando actualmente.

Como antes, cree un procedimiento almacenado para encapsular el código de R.

```sql
USE NYCTaxi_Sample
GO

-- Stored procedure that scores per partition. 
-- Depending on the partition being processed, a model specific to that partition will be used
CREATE
    OR

ALTER PROCEDURE [dbo].[predict_per_partition]
AS
BEGIN
    DECLARE @predict_duration FLOAT
        ,@instance_name NVARCHAR(100) = @@SERVERNAME
        ,@database_name NVARCHAR(128) = db_name()
        ,@input_query NVARCHAR(max);

    SET @input_query = 'SELECT tipped, passenger_count, trip_time_in_secs, trip_distance, d.direct_distance, payment_type
                          FROM dbo.nyctaxi_sample TABLESAMPLE (1 PERCENT) REPEATABLE (98074)
                          CROSS APPLY [CalculateDistance](pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) as d'

    EXEC sp_execute_external_script @language = N'R'
        ,@script = 
        N'
    
    if (nrow(InputDataSet) > 0) {

    #Get the partition that is currently being processed
    current_partition <- InputDataSet[1,]$payment_type;

    #Create the SQL query to select the right model
    query_getModel <- paste0("select model_object from ml_models where model_name = ", "''", "nyctaxi.",InputDataSet[1,]$payment_type,"''", ";")
    

    # Define the connection string
    connStr <- paste("Driver=SQL Server;Server=", instance_name, ";Database=", database_name, ";Trusted_Connection=true;", sep="");
        
    #Define data source to use for getting the model
    ds <- RxOdbcData(sqlQuery = query_getModel, connectionString = connStr)

    # Load the model
    modelbin <- rxReadObject(ds, deserialize = FALSE)
    # unserialize model
    logitObj <- unserialize(modelbin);

    # predict tipped or not based on model
    predictions <- rxPredict(logitObj, data = InputDataSet, overwrite = TRUE, type = "response", writeModelVars = TRUE
        , extraVarsToWrite = c("payment_type"));        
    OutputDataSet <- predictions
    
    } else {
        OutputDataSet <- data.frame(integer(), InputDataSet[,]);        
    }
    '
        ,@input_data_1 = @input_query
        ,@parallel = 1
        ,@input_data_1_partition_by_columns = N'payment_type'
        ,@params = N'@instance_name nvarchar(100), @database_name nvarchar(128)'
        ,@instance_name = @instance_name
        ,@database_name = @database_name
    WITH RESULT SETS((
                tipped_Pred INT
                ,payment_type VARCHAR(5)
                ,tipped INT
                ,passenger_count INT
                ,trip_distance FLOAT
                ,trip_time_in_secs INT
                ,direct_distance FLOAT
                ));
END;
GO
```

## <a name="create-a-table-to-store-predictions"></a>Crear una tabla para almacenar las predicciones

```sql
CREATE TABLE prediction_results (
    tipped_Pred INT
    ,payment_type VARCHAR(5)
    ,tipped INT
    ,passenger_count INT
    ,trip_distance FLOAT
    ,trip_time_in_secs INT
    ,direct_distance FLOAT
    );

TRUNCATE TABLE prediction_results
GO
```

## <a name="run-the-procedure-and-save-predictions"></a>Ejecutar el procedimiento y guardar las predicciones

```sql
INSERT INTO prediction_results (
    tipped_Pred
    ,payment_type
    ,tipped
    ,passenger_count
    ,trip_distance
    ,trip_time_in_secs
    ,direct_distance
    )
EXECUTE [predict_per_partition]
GO
```

## <a name="view-predictions"></a>Predicciones de vista

Dado que se almacenan las predicciones, puede ejecutar una consulta simple para devolver un conjunto de resultados.

```sql
SELECT *
FROM prediction_results;
```

## <a name="next-steps"></a>Pasos siguientes

En este tutorial, ha utilizado [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) para iterar en las operaciones de datos con particiones. Para con más examine una llamada a scripts externos en los procedimientos almacenados y utilizando las funciones de RevoScaleR, continúe con el siguiente tutorial.

> [!div class="nextstepaction"]
> [Tutorial de R y SQL Server](walkthrough-data-science-end-to-end-walkthrough.md)

<!--
## Old intro

**(Not for production workloads)**

One of the more common approaches for executing R or Python code on SQL data is providing script as an input parameter to the [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) stored procedure. In this CTP release, SQL Server 2019 adds new parameters to `sp_execute_external_script` to process partitions with the external script executing once for every partition:

| Parameter | Usage |
|-----------|-------|
| **input_data_1_partition_by_columns** | Specifies which columns to partition by. |
| **input_data_1_order_by_columns** | Specifies which columns to order by.  |

Partitions are an organizational mechanism for stratified data that naturally segments into a given classification scheme. Common examples include partitioning by geographic region, by date and time, by age or gender, and so forth. Given the existence of partitioned data, you might want to execute script over the entire data set, with the ability to model, train, and score partitions that remain intact over all these operations. Calling `sp_execute_external_script` with the new parameters allows you to do just that.

You can run this operation in parallel by combining `partition_by` with `@parallel`. If the input query can be parallelized, set `@parallel=1` as part of your arguments to `sp_execute_external_script`. By default, the query optimizer operates under `@parallel=1` on tables having more than 256 rows.

When the scenario is training, one advantage is that any arbitrary training script, even those using non-Microsoft-rx algorithms, can be parallelized by also using the @parallel parameter. Typically, you would have to use RevoScaleR algorithms (with the rx prefix) to obtain parallelism in training scenarios in SQL Server. But with the new parameter, you can parallelize a script that calls functions not specifically engineered with that capability.
-->
