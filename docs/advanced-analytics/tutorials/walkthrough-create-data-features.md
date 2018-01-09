---
title: "Crear características de datos mediante R y SQL (tutorial) | Documentos de Microsoft"
ms.custom: 
ms.date: 08/23/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: 
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: tutorial
applies_to: SQL Server 2016
dev_langs: R
ms.assetid: 4981d4eb-0874-4fe9-82e1-edf99890e27a
caps.latest.revision: "21"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: d9d0ddcbd20299a9e249b3fd1b81874c17234864
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/08/2018
---
# <a name="create-data-features-using-r-and-sql-walkthrough"></a>Crear características de datos mediante R y SQL (tutorial)

La ingeniería de datos es un aspecto importante del aprendizaje automático. Datos requieren a menudo la transformación antes de que se puede usar para el modelado de predicción. Si los datos no tienen las características que necesita, puede diseñarlos a partir de valores existentes.

Para esta tarea de modelado, en lugar de usar los valores de latitud y longitud sin procesar de la ubicación de origen y destino, le gustaría tener la distancia en millas entre las dos ubicaciones. Para crear esta característica, calcular la distancia lineal directa entre dos puntos, mediante el uso de la [fórmula haversine](https://en.wikipedia.org/wiki/Haversine_formula).

En este paso, se comparan dos métodos diferentes para la creación de una característica de datos:

- Uso de una función de R personalizada
- Usar una función personalizada de T-SQL en[!INCLUDE[tsql](../../includes/tsql-md.md)]

El objetivo es crear un nuevo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] conjunto de datos que incluyen la nueva característica numérica, además de las columnas originales *direct_distance*.

## <a name="featurization-using-r"></a>Características de uso de R

El lenguaje R es conocido por sus completas y variadas bibliotecas estadísticas, pero también podría necesitar crear transformaciones de datos personalizadas.

Primero, vamos a hacer que la forma R, los usuarios acostumbrados a: obtener los datos en su equipo portátil y, a continuación, ejecutar una función de R personalizada, *ComputeDist*, que calcula la distancia lineal entre dos puntos especificados por los valores de latitud y longitud.

1. Recuerde que el objeto de origen de datos que creó anteriormente obtiene solo las primeras 1000 filas. Así que vamos a definir una consulta que obtiene todos los datos.

    ```R
    bigQuery <- "SELECT tipped, fare_amount, passenger_count,trip_time_in_secs,trip_distance, pickup_datetime, dropoff_datetime,  pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude FROM nyctaxi_sample";
    ```

2. Crear un nuevo origen de datos de SQL Server mediante la consulta.

    ```R
    featureDataSource <- RxSqlServerData(sqlQuery = bigQuery,colClasses = c(pickup_longitude = "numeric", pickup_latitude = "numeric", dropoff_longitude = "numeric", dropoff_latitude = "numeric", passenger_count  = "numeric", trip_distance  = "numeric", trip_time_in_secs  = "numeric", direct_distance  = "numeric"), connectionString = connStr);
    ```

    - [RxSqlServerData](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxsqlserverdata) puede tardar tratarse de una consulta que consta de una consulta SELECT válida, proporcionada como argumento para la _sqlQuery_ parámetro o el nombre de un objeto table, que se proporciona como el _tabla_ parámetro.
    
    - Si desea datos de ejemplo de una tabla, debe utilizar el _sqlQuery_ parámetro, definir parámetros de muestreo mediante la cláusula TABLESAMPLE de T-SQL y establecer el _rowBuffering_ argumento en FALSE.

3. Ejecute el código siguiente para crear la función de R personalizada. ComputeDist toma dos pares de valores de latitud y longitud y calcula la distancia lineal entre ellas y devuelve la distancia en millas.

    ```R
    env <- new.env();
    env$ComputeDist <- function(pickup_long, pickup_lat, dropoff_long, dropoff_lat){
      R <- 6371/1.609344 #radius in mile
      delta_lat <- dropoff_lat - pickup_lat
      delta_long <- dropoff_long - pickup_long
      degrees_to_radians = pi/180.0
      a1 <- sin(delta_lat/2*degrees_to_radians)
      a2 <- as.numeric(a1)^2
      a3 <- cos(pickup_lat*degrees_to_radians)
      a4 <- cos(dropoff_lat*degrees_to_radians)
      a5 <- sin(delta_long/2*degrees_to_radians)
      a6 <- as.numeric(a5)^2
      a <- a2+a3*a4*a6
      c <- 2*atan2(sqrt(a),sqrt(1-a))
      d <- R*c
      return (d)
    }
    ```
  
    + La primera línea define un nuevo entorno. En R, se puede usar un entorno para encapsular los espacios de nombres en paquetes y similares.  Puede usar la función `search()` para ver los entornos en el área de trabajo. Para ver los objetos en un entorno específico, escriba `ls(<envname>)`.
    + Las líneas que comienzan con `$env.ComputeDistance` contienen el código que define la fórmula haversine, que calcula la *distancia del círculo máximo* entre dos puntos en una esfera.

4. Habiendo definido la función, se aplica a los datos que se va a crear una nueva columna de característica, *direct_distance*. pero antes de ejecutar la transformación, cambiar el contexto de proceso a local.

    ```R
    rxSetComputeContext("local");
    ```

5. Llame a la [rxDataStep](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdatastep) función para habilitar la característica datos de ingeniería y aplicar el `env$ComputeDist` función a los datos en memoria.

    ```R
    start.time <- proc.time();
  
    changed_ds <- rxDataStep(inData = featureEngineeringQuery,
    transforms = list(direct_distance=ComputeDist(pickup_longitude,pickup_latitude, dropoff_longitude, dropoff_latitude),
    tipped = "tipped", fare_amount = "fare_amount", passenger_count = "passenger_count",
    trip_time_in_secs = "trip_time_in_secs",  trip_distance="trip_distance",
    pickup_datetime = "pickup_datetime",  dropoff_datetime = "dropoff_datetime"),
    transformEnvir = env,
    rowsPerRead=500,
    reportProgress = 3);
  
    used.time <- proc.time() - start.time;
    print(paste("It takes CPU Time=", round(used.time[1]+used.time[2],2)," seconds, Elapsed Time=", round(used.time[3],2), " seconds to generate features.", sep=""));
    ```

    + La función rxDataStep admite varios métodos para modificar los datos en su lugar. Para obtener más información, consulte este artículo: [cómo transformar y el subconjunto de los datos de Microsft R](https://docs.microsoft.com/r-server/r/how-to-revoscaler-data-transform)
    
    Sin embargo, un par de puntos que tener en cuenta con respecto a rxDataStep: 
    
    En otros orígenes de datos, puede usar los argumentos *varsToKeep* y *varsToDrop*, pero no se admiten para los orígenes de datos de SQL Server. Por lo tanto, en este ejemplo, hemos usado el _transforma_ argumento para especificar las columnas de paso a través y las columnas transformadas. Además, cuando ejecuta en un servidor SQL Server cálculo, el _inData_ argumento solo puede tomar un origen de datos de SQL Server.

    El código anterior también puede generar un mensaje de advertencia cuando se ejecuta en los conjuntos de datos más grandes. Cuando el número de filas veces el número de columnas que se está creando supera un valor especificado (el valor predeterminado es 3,000,000), rxDataStep devuelve una advertencia y se truncará el número de filas de la trama de datos devuelto. Para quitar la advertencia, puede modificar el _maxRowsByCols_ argumento de la función rxDataStep. Sin embargo, si _maxRowsByCols_ es demasiado grande, podría experimentar problemas al cargar la trama de datos en memoria.

7. Si lo desea, puede llamar a [rxGetVarInfo](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxgetvarinfo) para inspeccionar el esquema del origen de datos transformado.

    ```R
    rxGetVarInfo(data = changed_ds);
    ```

## <a name="featurization-using-transact-sql"></a>Características con Transact-SQL

Ahora, cree una función SQL personalizada, *ComputeDist*, para realizar la misma tarea que la función de R personalizada.

1. Defina una nueva función personalizada de SQL denominada *fnCalculateDistance*. El código para esta función de SQL definida por el usuario se proporciona como parte del script de PowerShell que ejecutó para crear y configurar la base de datos.  La función ya debe existir en la base de datos.

    Si no existe, use SQL Server Management Studio para generar la función en la misma base de datos donde están almacenados los datos de taxis.

    ```sql
    CREATE FUNCTION [dbo].[fnCalculateDistance] (@Lat1 float, @Long1 float, @Lat2 float, @Long2 float)
    -- User-defined function calculates the direct distance between two geographical coordinates.
    RETURNS
    AS
    BEGIN
      DECLARE @distance decimal(28, 10)
      -- Convert to radians
      SET @Lat1 = @Lat1 / 57.2958
      SET @Long1 = @Long1 / 57.2958
      SET @Lat2 = @Lat2 / 57.2958
      SET @Long2 = @Long2 / 57.2958
      -- Calculate distance
      SET @distance = (SIN(@Lat1) * SIN(@Lat2)) + (COS(@Lat1) * COS(@Lat2) * COS(@Long2 - @Long1))
      --Convert to miles
      IF @distance <> 0
      BEGIN
        SET @distance = 3958.75 * ATAN(SQRT(1 - POWER(@distance, 2)) / @distance);
      END
      RETURN @distance
    END
    ```

2. Para ver cómo actúa la función, ejecute la siguiente instrucción [!INCLUDE[tsql](../../includes/tsql-md.md)] desde cualquier aplicación que admita [!INCLUDE[tsql](../../includes/tsql-md.md)].

    ```sql
    SELECT tipped, fare_amount, passenger_count,trip_time_in_secs,trip_distance, pickup_datetime, dropoff_datetime,
    dbo.fnCalculateDistance(pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) as direct_distance,
    pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude
    FROM nyctaxi_sample
    ```
3. Habiendo definido esta función, que resultaría muy fácil crear las características que desea mediante SQL y, a continuación, insertar los valores directamente en una tabla nueva:

    ```
    SELECT tipped, fare_amount, passenger_count,trip_time_in_secs,trip_distance, pickup_datetime, dropoff_datetime,
    dbo.fnCalculateDistance(pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) as direct_distance,
    pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude
    INTO NewFeatureTable
    FROM nyctaxi_sample
    ```

4. Sin embargo, vamos a ver cómo llamar a la función SQL personalizada desde el código de R. En primer lugar, almacena la consulta de características SQL en una variable de R.

    ```R
    featureEngineeringQuery = "SELECT tipped, fare_amount, passenger_count,
        trip_time_in_secs,trip_distance, pickup_datetime, dropoff_datetime,
        dbo.fnCalculateDistance(pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) as direct_distance,
        pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude
        FROM nyctaxi_sample
        tablesample (1 percent) repeatable (98052)"
    ```
  
    > [!TIP]
    > Esta consulta se ha modificado para obtener un ejemplo más pequeño de datos, para realizar este tutorial con mayor rapidez. Puede quitar la cláusula TABLESAMPLE si desea obtener todos los datos; Sin embargo, dependiendo de su entorno, no sería posible cargar el conjunto de datos completa en R, genera un error.
  
5. Use las siguientes líneas de código para llamar a la función de [!INCLUDE[tsql](../../includes/tsql-md.md)] desde su entorno de R y aplicarla a los datos definidos en *featureEngineeringQuery*.
  
    ```R
    featureDataSource = RxSqlServerData(sqlQuery = featureEngineeringQuery,
      colClasses = c(pickup_longitude = "numeric", pickup_latitude = "numeric",
             dropoff_longitude = "numeric", dropoff_latitude = "numeric",
             passenger_count  = "numeric", trip_distance  = "numeric",
              trip_time_in_secs  = "numeric", direct_distance  = "numeric"),
      connectionString = connStr)
    ```
  
6.  Ahora que se crea la nueva característica, llame a **rxGetVarsInfo** para crear un resumen de los datos en la tabla de características.
  
    ```R
    rxGetVarInfo(data = featureDataSource)
    ```

    *Resultados*

    ```
    Var 1: tipped, Type: integer
    Var 2: fare_amount, Type: numeric
    Var 3: passenger_count, Type: numeric
    Var 4: trip_time_in_secs, Type: numeric
    Var 5: trip_distance, Type: numeric
    Var 6: pickup_datetime, Type: character
    Var 7: dropoff_datetime, Type: character
    Var 8: direct_distance, Type: numeric
    Var 9: pickup_latitude, Type: numeric
    Var 10: pickup_longitude, Type: numeric
    Var 11: dropoff_latitude, Type: numeric
    Var 12: dropoff_longitude, Type: numeric
    ```

    > [!NOTE]
    > En algunos casos, podría obtener un error como éste: *se denegó el permiso de ejecutar el en el objeto 'fnCalculateDistance'* si es así, asegúrese de que el inicio de sesión que utilizas tiene permisos para ejecutar secuencias de comandos y crear objetos en la base de datos no solo en la instancia.
    > Compruebe el esquema para el objeto, fnCalculateDistance. Si el objeto fue creado por el propietario de la base de datos y el inicio de sesión que pertenece el rol db_datareader, debe otorgar permisos explícitos para ejecutar el script de inicio de sesión.

## <a name="comparing-r-functions-and-sql-functions"></a>Comparación de funciones de R y funciones SQL

¿Recuerde que este fragmento de código que se usa para el código de R de tiempo?

```R
start.time <- proc.time()
<your code here>
used.time <- proc.time() - start.time
print(paste("It takes CPU Time=", round(used.time[1]+used.time[2],2)," seconds, Elapsed Time=", round(used.time[3],2), " seconds to generate features.", sep=""))
```

También puede intentar usar esto con el ejemplo de función personalizada de SQL para ver cuánto tiempo la transformación de datos toma al llamar a una función SQL. Además, intente cambiar contextos de proceso con rxSetComputeContext y compare el rendimiento.

Las horas pueden variar considerablemente, según la velocidad de la red y la configuración del hardware. En las configuraciones que hemos probado, el [!INCLUDE[tsql](../../includes/tsql-md.md)] enfoque de función era más rápido que utilizar una función de R personalizada. Por lo tanto, hemos uso el [!INCLUDE[tsql](../../includes/tsql-md.md)] función para estos cálculos en los siguientes pasos.

> [!TIP]
> Uso de ingeniería de características muy a menudo, [!INCLUDE[tsql](../../includes/tsql-md.md)] será más rápido que R. Por ejemplo, T-SQL incluye rápida basada en ventanas y las funciones de clasificación que se pueden aplicar a los cálculos de ciencia de datos comunes como gradual medias móviles y  *n* -iconos. Elija el método más eficaz en función de los datos y la tarea.

## <a name="next-lesson"></a>Lección siguiente

[Generar un modelo de R y guardar en SQL](walkthrough-build-and-save-the-model.md)

## <a name="previous-lesson"></a>Lección anterior

[Ver y resumir datos mediante R](walkthrough-view-and-summarize-data-using-r.md)

