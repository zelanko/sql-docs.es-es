---
title: Tutorial sobre la creación, el entrenamiento y la puntuación de modelos basados en particiones en R
description: Aprenda a modelar, entrenar y usar datos con particiones creados de forma dinámica al usar las funcionalidades de modelado basado en particiones de SQL Server Machine Learning.
ms.custom: sqlseattle
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/04/2019
ms.topic: tutorial
ms.author: davidph
author: dphansen
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 1f73f45d2ac9830fed810746a5895554cded0691
ms.sourcegitcommit: 830149bdd6419b2299aec3f60d59e80ce4f3eb80
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/04/2019
ms.locfileid: "73532575"
---
# <a name="tutorial-create-partition-based-models-in-r-on-sql-server"></a>Tutorial: Creación de modelos basados en particiones en R en SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

En SQL Server 2019, el modelado basado en particiones es la capacidad de crear y entrenar modelos con los datos con particiones. En el caso de los datos estratificados que se segmentan de forma natural en un esquema de clasificación determinado, como regiones geográficas, fecha y hora, edad o sexo, puede ejecutar un script en todo el conjunto de datos, con la capacidad de modelar, entrenar y puntuar las particiones que permanecen intactas a lo largo de todas estas operaciones. 

El modelado basado en particiones se habilita mediante dos nuevos parámetros en [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql):

+ **input_data_1_partition_by_columns** especifica una columna por la que crear la partición.
+ **input_data_1_order_by_columns** especifica las columnas por las que ordenar. 

En este tutorial vamos a aprender sobre el modelado basado en particiones con los datos de ejemplo clásicos del taxi de Nueva York y el script de R. La columna de partición es el método de pago.

> [!div class="checklist"]
> * Las particiones se basan en los tipos de pago (5).
> * Cree y entrene modelos en cada partición y almacene los objetos en la base de datos.
> * Prediga la probabilidad de propina en cada modelo de partición con los datos de ejemplo reservados para ese propósito.

## <a name="prerequisites"></a>Prerequisites
 
Para realizar este tutorial, debe disponer de lo siguiente:

+ Suficientes recursos del sistema. El conjunto de datos es grande y las operaciones de entrenamiento usan muchos recursos. Si es posible, use un sistema con, al menos, 8 GB de RAM. También puede usar conjuntos de datos más pequeños para solucionar las restricciones de recursos. Las instrucciones para reducir el conjunto de datos están en línea. 

+ Una herramienta para la ejecución de consultas de T-SQL, como [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).

+ [NYCTaxi_Sample.bak](https://sqlmldoccontent.blob.core.windows.net/sqlml/NYCTaxi_Sample.bak), que puede [descargar y restaurar](demo-data-nyctaxi-in-sql.md) en la instancia local del motor de base de datos. El tamaño del archivo es de aproximadamente 90 MB.

+ Instancia del motor de base de datos de SQL Server 2019 versión preliminar, con Machine Learning Services e integración de R.

Compruebe la versión mediante la ejecución de **`SELECT @@Version`** como una consulta de T-SQL en una herramienta de consulta.

Compruebe la disponibilidad de paquetes de R; para ello, devuelva una lista con el formato correcto de todos los paquetes de R instalados actualmente en la instancia del motor de base de datos:

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

Inicie Management Studio y conéctese a la instancia del motor de base de datos. En el Explorador de objetos, compruebe que existe la [base de datos NYCTaxi_Sample](demo-data-nyctaxi-in-sql.md). 

## <a name="create-calculatedistance"></a>Crear CalculateDistance

La base de datos de demostración incluye una función escalar para calcular la distancia, pero el procedimiento almacenado funciona mejor con una función con valores de tabla. Ejecute el siguiente script para crear la función **CalculateDistance** que se usa en el [paso de entrenamiento](#training-step) más adelante.

Para confirmar que se ha creado la función, compruebe las funciones con valores de tabla de \Programmability\Functions\ en la base de datos **NYCTaxi_Sample** en el Explorador de objetos.

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

## <a name="define-a-procedure-for-creating-and-training-per-partition-models"></a>Definir un procedimiento para crear y entrenar modelos por partición

En este tutorial se encapsula el script de R en un procedimiento almacenado. En este paso se crea un procedimiento almacenado que usa R para crear un conjunto de datos de entrada, se crea un modelo de clasificación para predecir propinas y luego se almacena el modelo en la base de datos.

Entre las entradas de parámetros usadas por este script aparecen **input_data_1_partition_by_columns** e **input_data_1_order_by_columns**. Recuerde que estos parámetros son el mecanismo por el que se produce el modelado con particiones. Los parámetros se pasan como entradas a [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) para procesar las particiones con el script externo que se ejecuta una vez para cada partición. 

En este procedimiento almacenado [use paralelismo](#parallel) para terminar más rápido.

Después de ejecutar este script, debe ver **train_rxLogIt_per_partition** en los procedimientos almacenados de \Programmability\ en la base de datos **NYCTaxi_Sample** del Explorador de objetos. También debe ver una nueva tabla que se usa para almacenar modelos: **dbo.nyctaxi_models**.

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

Observe que las entradas de [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) incluyen `@parallel=1`, que se usa para habilitar el procesamiento paralelo. A diferencia de las versiones anteriores, en SQL Server 2019, el establecimiento de `@parallel=1` proporciona una indicación más fuerte al optimizador de consultas, lo que convierte a la ejecución en paralelo en un resultado mucho más probable.

De forma predeterminada, el optimizador de consultas tiende a funcionar con `@parallel=1` en tablas con más de 256 filas, pero puede controlar esto de forma explícita si establece `@parallel=1` como se muestra en este script.

> [!Tip]
> En las cargas de trabajo de entrenamiento, puede usar `@parallel` con cualquier script de entrenamiento arbitrario, incluso aquellos que usan algoritmos rx que no son de Microsoft. Normalmente, solo los algoritmos de RevoScaleR (con el prefijo rx) ofrecen paralelismo en escenarios de entrenamiento de SQL Server. Pero con el nuevo parámetro, puede paralelizar un script que llame a funciones, incluidas funciones de R de código abierto, no diseñado específicamente con esa capacidad. Esto funciona porque las particiones tienen afinidad con subprocesos concretos, así que todas las operaciones llamadas en un script se ejecutan por partición en el `thread.`<a name="training-step"></a> determinado.

## <a name="run-the-procedure-and-train-the-model"></a>Ejecutar el procedimiento y entrenar el modelo

En esta sección, el script entrena al modelo creado y guardado en el paso anterior. Los ejemplos siguientes muestran dos enfoques para entrenar el modelo: con un conjunto de datos completo o con datos parciales. 

Tenga en cuenta que este paso va a llevar bastante tiempo. El entrenamiento usa muchos recursos y tarda muchos minutos en completarse. Si los recursos del sistema, especialmente la memoria, son insuficientes para la carga, use un subconjunto de los datos. En el segundo ejemplo se proporciona la sintaxis.

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
> Si está ejecutando otras cargas de trabajo, puede anexar `OPTION(MAXDOP 2)` a la instrucción SELECT si quiere limitar el procesamiento de consultas a solo dos núcleos.

## <a name="check-results"></a>Comprobar los resultados

El resultado de la tabla de modelos debe ser de cinco modelos diferentes, según las cinco particiones segmentadas por los cinco tipos de pago. Los modelos se encuentran en el origen de datos **ml_models**.

```sql
SELECT *
FROM ml_models
```
 
## <a name="define-a-procedure-for-predicting-outcomes"></a>Definir un procedimiento para predecir resultados

Puede usar los mismos parámetros para puntuar. El ejemplo siguiente contiene un script de R que puntúa mediante el modelo correcto para la partición que se está procesando actualmente.

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

## <a name="view-predictions"></a>Ver las predicciones

Dado que las predicciones se almacenan, puede ejecutar una consulta simple para devolver un conjunto de resultados.

```sql
SELECT *
FROM prediction_results;
```

## <a name="next-steps"></a>Pasos siguientes

En este tutorial ha usado [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) para iterar operaciones en datos con particiones. Para obtener una visión más detallada de la llamada a scripts externos en procedimientos almacenados y del uso de funciones de RevoScaleR, continúe con el tutorial siguiente.

> [!div class="nextstepaction"]
> [Tutorial de R y SQL Server](walkthrough-data-science-end-to-end-walkthrough.md)

