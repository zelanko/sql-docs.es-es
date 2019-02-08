---
title: 'Crear características de datos mediante funciones de R y SQL Server: SQL Server Machine Learning'
description: Tutorial que muestra cómo crear características de datos mediante las funciones de SQL Server para realizar análisis en bases de datos.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/26/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 527f88ed14adc0140cbca179177e85670f72cafd
ms.sourcegitcommit: afc0c3e46a5fec6759fe3616e2d4ba10196c06d1
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2019
ms.locfileid: "55890016"
---
# <a name="create-data-features-using-r-and-sql-server-walkthrough"></a>Crear características de datos mediante R y SQL Server (tutorial)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

La ingeniería de datos es un aspecto importante del aprendizaje automático. Datos a menudo requieren la transformación antes de usarlo para el modelado predictivo. Si los datos no tienen las características que necesita, puede diseñarlos a partir de valores existentes.

Para esta tarea de modelado, en lugar de usar los valores de latitud y longitud sin procesar de la ubicación de origen y destino, le gustaría tener la distancia en millas entre las dos ubicaciones. Para crear esta característica, calcula la distancia lineal directa entre dos puntos, usando la [fórmula haversine](https://en.wikipedia.org/wiki/Haversine_formula).

En este paso, obtenga información sobre dos métodos diferentes para crear una característica de datos:

> [!div class="checklist"]
> * Usar una función personalizada de R
> * Usar una función personalizada de T-SQL en [!INCLUDE[tsql](../../includes/tsql-md.md)]

El objetivo es crear un nuevo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] conjunto de datos que incluyen la nueva característica numérica, además de las columnas originales *direct_distance*.

## <a name="prerequisites"></a>Requisitos previos

Este paso presupone una sesión de R en curso según los pasos anteriores en este tutorial. Usa cadenas y datos de origen creados objetos de conexión en esos pasos. Las siguientes herramientas y los paquetes se utilizan para ejecutar el script.

+ Rgui.exe para ejecutar comandos de R
+ Management Studio para ejecutar T-SQL

## <a name="featurization-using-r"></a>Características con R

El lenguaje R es conocido por sus completas y variadas bibliotecas estadísticas, pero también podría necesitar crear transformaciones de datos personalizadas.

Primero, vamos a hacer que la forma de R, los usuarios está acostumbrado a: obtener los datos en su equipo portátil y, a continuación, ejecute una función de R personalizada, *ComputeDist*, que calcula la distancia lineal entre dos puntos especificados mediante valores de latitud y longitud.

1. Recuerde que el objeto de origen de datos que creó anteriormente obtiene solo las primeras 1000 filas. Así que vamos a definir una consulta que obtiene todos los datos.

    ```R
    bigQuery <- "SELECT tipped, fare_amount, passenger_count,trip_time_in_secs,trip_distance, pickup_datetime, dropoff_datetime,  pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude FROM nyctaxi_sample";
    ```

2. Cree un nuevo objeto de origen de datos mediante la consulta.

    ```R
    featureDataSource <- RxSqlServerData(sqlQuery = bigQuery,colClasses = c(pickup_longitude = "numeric", pickup_latitude = "numeric", dropoff_longitude = "numeric", dropoff_latitude = "numeric", passenger_count  = "numeric", trip_distance  = "numeric", trip_time_in_secs  = "numeric", direct_distance  = "numeric"), connectionString = connStr);
    ```

    - [RxSqlServerData](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxsqlserverdata) puede tardar tratarse de una consulta que consta de una consulta SELECT válida, proporcionada como argumento a la _sqlQuery_ parámetro o el nombre de un objeto table, proporcionado como el _tabla_ parámetro.
    
    - Si desea datos de ejemplo de una tabla, debe usar el _sqlQuery_ parámetro, definir parámetros de muestreo mediante la cláusula TABLESAMPLE T-SQL y establecer el _rowBuffering_ argumento en FALSE.

3. Ejecute el siguiente código para crear la función personalizada de R. ComputeDist toma dos pares de valores de latitud y longitud y calcula la distancia lineal entre ellas y devuelve la distancia en millas.

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
  
    + La primera línea define un nuevo entorno. En R, se puede usar un entorno para encapsular los espacios de nombres en paquetes y similares. Puede usar la función `search()` para ver los entornos en el área de trabajo. Para ver los objetos en un entorno específico, escriba `ls(<envname>)`.
    + Las líneas que comienzan con `$env.ComputeDist` contienen el código que define la fórmula haversine, que calcula la *distancia del círculo máximo* entre dos puntos en una esfera.

4. Después de definir la función, se aplica a los datos para crear una nueva columna de característica, *direct_distance*. pero antes de ejecutar la transformación, cambiar el contexto de cálculo a local.

    ```R
    rxSetComputeContext("local");
    ```

5. Llame a la [rxDataStep](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdatastep) función para obtener los datos de ingeniería de características y aplicar el `env$ComputeDist` función a los datos en memoria.

    ```R
    start.time <- proc.time();
  
    changed_ds <- rxDataStep(inData = featureDataSource,
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

    + La función rxDataStep admite varios métodos para modificar datos en su lugar. Para obtener más información, consulte este artículo:  [Datos de transformación y el subconjunto de Microsft R](https://docs.microsoft.com/r-server/r/how-to-revoscaler-data-transform)
    
    Sin embargo, un par de puntos que vale la pena mencionar sobre rxDataStep: 
    
    En otros orígenes de datos, puede usar los argumentos *varsToKeep* y *varsToDrop*, pero no se admiten para los orígenes de datos de SQL Server. Por lo tanto, en este ejemplo, hemos usado el _transforma_ argumento para especificar las columnas de paso a través y las columnas transformadas. Además, al que se ejecute en un servidor SQL Server contexto de proceso, el _inData_ argumento solo puede tomar un origen de datos de SQL Server.

    El código anterior también puede generar un mensaje de advertencia cuando se ejecutan en grandes conjuntos de datos. Cuando el número de filas, multiplicado por el número de columnas que se está creando supera un valor establecido (el valor predeterminado es 3,000,000), rxDataStep devuelve una advertencia y se truncará el número de filas en la trama de datos devuelto. Para quitar la advertencia, puede modificar el _maxRowsByCols_ argumento en la función rxDataStep. Sin embargo, si _maxRowsByCols_ es demasiado grande, podría experimentar problemas al cargar la trama de datos en memoria.

7. Si lo desea, puede llamar a [rxGetVarInfo](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxgetvarinfo) para inspeccionar el esquema del origen de datos transformados.

    ```R
    rxGetVarInfo(data = changed_ds);
    ```

## <a name="featurization-using-transact-sql"></a>Características con Transact-SQL

En este ejercicio, aprenderá a realizar la misma tarea utilizando las funciones de SQL en lugar de funciones de R personalizadas. 

Cambie a [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) u otro editor de consultas para ejecutar el script de T-SQL.

1. Usar una función SQL, denominada *fnCalculateDistance*. La función ya debe existir en la base de datos NYCTaxi_Sample. En el Explorador de objetos, compruebe que la función existe, vaya a esta ruta de acceso: Las bases de datos > NYCTaxi_Sample > programación > funciones > funciones escalares > dbo.fnCalculateDistance.

    Si no existe la función, utilice SQL Server Management Studio para generar la función en la base de datos NYCTaxi_Sample.

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

2. En Management Studio, en una nueva ventana de consulta, ejecute el siguiente [!INCLUDE[tsql](../../includes/tsql-md.md)] instrucción desde cualquier aplicación que admita [!INCLUDE[tsql](../../includes/tsql-md.md)] para ver cómo funciona la función.

    ```sql
    USE nyctaxi_sample
    GO

    SELECT tipped, fare_amount, passenger_count,trip_time_in_secs,trip_distance, pickup_datetime, dropoff_datetime,
    dbo.fnCalculateDistance(pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude) as direct_distance, pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude 
    FROM nyctaxi_sample
    ```
3. Para insertar valores directamente en una tabla nueva (tendrá que crearlo primero), puede agregar un **INTO** cláusula que especifica el nombre de tabla.

    ```sql
    USE nyctaxi_sample
    GO

    SELECT tipped, fare_amount, passenger_count, trip_time_in_secs, trip_distance, pickup_datetime, dropoff_datetime,
    dbo.fnCalculateDistance(pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude) as direct_distance, pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude
    INTO NewFeatureTable
    FROM nyctaxi_sample
    ```

4. También puede llamar a la función SQL desde el código de R. Volver al Rgui y almacene la consulta de características SQL en una variable de R.

    ```R
    featureEngineeringQuery = "SELECT tipped, fare_amount, passenger_count,
        trip_time_in_secs,trip_distance, pickup_datetime, dropoff_datetime,
        dbo.fnCalculateDistance(pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) as direct_distance,
        pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude
        FROM nyctaxi_sample
        tablesample (1 percent) repeatable (98052)"
    ```
  
    > [!TIP]
    > Esta consulta se ha modificado para obtener una muestra más pequeña de datos, para realizar este tutorial con mayor rapidez. Puede quitar la cláusula TABLESAMPLE si desea obtener todos los datos; Sin embargo, dependiendo de su entorno, no sería posible cargar el conjunto de datos completa en R, lo que produce un error.
  
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

    **Resultado**

    ```R
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
    > En algunos casos, podría obtener un error como este: *Se denegó el permiso EXECUTE en el objeto 'fnCalculateDistance'* si es así, asegúrese de que el inicio de sesión que usa tiene permisos para ejecutar scripts y crear objetos en la base de datos, no solo en la instancia.
    > Compruebe el esquema para el objeto, fnCalculateDistance. Si el objeto fue creado por el propietario de la base de datos y el inicio de sesión que pertenece el db_datareader de rol, deberá dar permisos explícitos para ejecutar el script de inicio de sesión.

## <a name="comparing-r-functions-and-sql-functions"></a>Comparar funciones de R y funciones SQL

¿Recuerde que este fragmento de código que se usa para el tiempo en el código de R?

```R
start.time <- proc.time()
<your code here>
used.time <- proc.time() - start.time
print(paste("It takes CPU Time=", round(used.time[1]+used.time[2],2)," seconds, Elapsed Time=", round(used.time[3],2), " seconds to generate features.", sep=""))
```

Puede probar a usar esto con el ejemplo de la función personalizada de SQL para ver cuánto tiempo la transformación de datos toma al llamar a una función SQL. Además, intente cambiar los contextos de cálculo con rxSetComputeContext y compare el rendimiento.

Las horas pueden variar considerablemente, dependiendo de la velocidad de red y la configuración del hardware. En las configuraciones, probamos la [!INCLUDE[tsql](../../includes/tsql-md.md)] función supuso más rápido que utilizar una función personalizada de R. Por lo tanto, hemos usado el [!INCLUDE[tsql](../../includes/tsql-md.md)] función para estos cálculos en pasos posteriores.

> [!TIP]
> Muy a menudo, ingeniería de características con [!INCLUDE[tsql](../../includes/tsql-md.md)] será más rápida que R. Por ejemplo, T-SQL incluye ventanas rápida y funciones de categoría que se pueden aplicar a los cálculos de ciencia de datos comunes, como aplicar medias y *n*-iconos. Elija el método más eficaz en función de los datos y la tarea.

## <a name="next-steps"></a>Pasos siguientes

> [!div class="nextstepaction"]
> [Crear un modelo de R y guarde a SQL](walkthrough-build-and-save-the-model.md)

