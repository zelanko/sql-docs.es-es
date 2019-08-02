---
title: Crear características de datos mediante funciones de R y SQL Server
description: Tutorial en el que se muestra cómo crear características de datos mediante funciones de SQL Server para el análisis en bases de datos.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/26/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: f12c20a54c0811e392eaa85684d7fac1a209c396
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/01/2019
ms.locfileid: "68714695"
---
# <a name="create-data-features-using-r-and-sql-server-walkthrough"></a>Crear características de datos mediante R y SQL Server (tutorial)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

La ingeniería de datos es un aspecto importante del aprendizaje automático. Los datos suelen requerir la transformación antes de poder usarlos para el modelado predictivo. Si los datos no tienen las características que necesita, puede diseñarlos a partir de valores existentes.

Para esta tarea de modelado, en lugar de usar los valores de latitud y longitud sin procesar de la ubicación de origen y destino, le gustaría tener la distancia en millas entre las dos ubicaciones. Para crear esta característica, debe calcular la distancia lineal directa entre dos puntos, mediante la [fórmula Haversine](https://en.wikipedia.org/wiki/Haversine_formula).

En este paso, aprenderá dos métodos diferentes para crear una característica a partir de los datos:

> [!div class="checklist"]
> * Usar una función personalizada de R
> * Usar una función de T-SQL personalizada en[!INCLUDE[tsql](../../includes/tsql-md.md)]

El objetivo es crear un nuevo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] conjunto de datos que incluya las columnas originales más la nueva característica numérica, *direct_distance*.

## <a name="prerequisites"></a>Requisitos previos

En este paso se supone que hay una sesión de R en curso basada en los pasos anteriores de este tutorial. Utiliza las cadenas de conexión y los objetos de origen de datos creados en esos pasos. Las siguientes herramientas y paquetes se utilizan para ejecutar el script.

+ Rgui. exe para ejecutar comandos de R
+ Management Studio para ejecutar T-SQL

## <a name="featurization-using-r"></a>Características con R

El lenguaje R es conocido por sus completas y variadas bibliotecas estadísticas, pero también podría necesitar crear transformaciones de datos personalizadas.

En primer lugar, vamos a hacerlo de la forma en que los usuarios de R están acostumbrados: obtener los datos en el portátil y, a continuación, ejecutar una función de R personalizada, *ComputeDist*, que calcula la distancia lineal entre dos puntos especificados por los valores de latitud y longitud.

1. Recuerde que el objeto de origen de datos que creó anteriormente obtiene solo las primeras 1000 filas. Vamos a definir una consulta que obtenga todos los datos.

    ```R
    bigQuery <- "SELECT tipped, fare_amount, passenger_count,trip_time_in_secs,trip_distance, pickup_datetime, dropoff_datetime,  pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude FROM nyctaxi_sample";
    ```

2. Cree un nuevo objeto de origen de datos mediante la consulta.

    ```R
    featureDataSource <- RxSqlServerData(sqlQuery = bigQuery,colClasses = c(pickup_longitude = "numeric", pickup_latitude = "numeric", dropoff_longitude = "numeric", dropoff_latitude = "numeric", passenger_count  = "numeric", trip_distance  = "numeric", trip_time_in_secs  = "numeric", direct_distance  = "numeric"), connectionString = connStr);
    ```

    - [RxSqlServerData](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxsqlserverdata) puede tomar una consulta que conste de una consulta Select válida, que se proporciona como argumento para el parámetro _sqlquery_ , o el nombre de un objeto de tabla, proporcionado como parámetro de _tabla_ .
    
    - Si desea hacer un muestreo de los datos de una tabla, debe usar el parámetro _sqlquery_ , definir parámetros de muestreo mediante la cláusula TABLESAMPLE de T-SQL y establecer el argumento _rowBuffering_ en false.

3. Ejecute el código siguiente para crear la función personalizada de R. ComputeDist toma dos pares de valores de latitud y longitud, y calcula la distancia lineal entre ellos, devolviendo la distancia en millas.

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

4. Una vez definida la función, se aplica a los datos para crear una nueva columna de característica, *direct_distance*. pero antes de ejecutar la transformación, cambie el contexto de cálculo a local.

    ```R
    rxSetComputeContext("local");
    ```

5. Llame a la función [rxDataStep](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdatastep) para obtener los datos de ingeniería de características y `env$ComputeDist` aplique la función a los datos de la memoria.

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

    + La función rxDataStep admite varios métodos para modificar los datos en su lugar. Para obtener más información, consulte este artículo:  [Cómo transformar y subconjuntos de datos en una R](https://docs.microsoft.com/r-server/r/how-to-revoscaler-data-transform)
    
    Sin embargo, hay un par de puntos que merece la pena tener en cuenta respecto a rxDataStep: 
    
    En otros orígenes de datos, puede usar los argumentos *varsToKeep* y *varsToDrop*, pero no se admiten para los orígenes de datos de SQL Server. Por lo tanto, en este ejemplo, se ha usado el argumento Transformations para especificar las columnas de paso a través y las columnas transformadas. Además, cuando se ejecuta en un contexto de cálculo de SQL Server , el argumento indata solo puede tomar un SQL Server origen de datos.

    El código anterior también puede generar un mensaje de advertencia cuando se ejecuta en conjuntos de datos de mayor tamaño. Cuando el número de filas multiplicadas por el número de columnas que se están creando supera un valor establecido (el valor predeterminado es 3 millones), rxDataStep devuelve una advertencia y se trunca el número de filas de la trama de datos devuelta. Para quitar la advertencia, puede modificar el argumento _maxRowsByCols_ en la función rxDataStep. Sin embargo, si _maxRowsByCols_ es demasiado grande, puede experimentar problemas al cargar la trama de datos en la memoria.

7. Opcionalmente, puede llamar a [rxGetVarInfo](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxgetvarinfo) para inspeccionar el esquema del origen de datos transformado.

    ```R
    rxGetVarInfo(data = changed_ds);
    ```

## <a name="featurization-using-transact-sql"></a>Características con Transact-SQL

En este ejercicio, aprenderá a realizar la misma tarea con las funciones de SQL en lugar de las funciones personalizadas de R. 

Cambie a [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) u otro editor de consultas para ejecutar el script T-SQL.

1. Use una función SQL, denominada *fnCalculateDistance*. La función ya debe existir en la base de datos NYCTaxi_Sample. En Explorador de objetos, Compruebe la función existente navegando por esta ruta de acceso: Las bases de datos > la programación de > de NYCTaxi_Sample > funciones > funciones escalares > DBO. fnCalculateDistance.

    Si la función no existe, use SQL Server Management Studio para generar la función en la base de datos NYCTaxi_Sample.

    ```sql
    CREATE FUNCTION [dbo].[fnCalculateDistance] (@Lat1 float, @Long1 float, @Lat2 float, @Long2 float)
    -- User-defined function calculates the direct distance between two geographical coordinates.
    RETURNS decimal(28, 10)
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

2. En Management Studio, en una nueva ventana de consulta, ejecute la [!INCLUDE[tsql](../../includes/tsql-md.md)] siguiente instrucción desde cualquier aplicación que [!INCLUDE[tsql](../../includes/tsql-md.md)] admita para ver cómo funciona la función.

    ```sql
    USE nyctaxi_sample
    GO

    SELECT tipped, fare_amount, passenger_count,trip_time_in_secs,trip_distance, pickup_datetime, dropoff_datetime,
    dbo.fnCalculateDistance(pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude) as direct_distance, pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude 
    FROM nyctaxi_sample
    ```
3. Para insertar valores directamente en una nueva tabla (debe crearlo primero), puede Agregar una cláusula **into** que especifique el nombre de la tabla.

    ```sql
    USE nyctaxi_sample
    GO

    SELECT tipped, fare_amount, passenger_count, trip_time_in_secs, trip_distance, pickup_datetime, dropoff_datetime,
    dbo.fnCalculateDistance(pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude) as direct_distance, pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude
    INTO NewFeatureTable
    FROM nyctaxi_sample
    ```

4. También puede llamar a la función SQL desde código R. Vuelva a Rgui y almacene la consulta SQL características en una variable de R.

    ```R
    featureEngineeringQuery = "SELECT tipped, fare_amount, passenger_count,
        trip_time_in_secs,trip_distance, pickup_datetime, dropoff_datetime,
        dbo.fnCalculateDistance(pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) as direct_distance,
        pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude
        FROM nyctaxi_sample
        tablesample (1 percent) repeatable (98052)"
    ```
  
    > [!TIP]
    > Esta consulta se ha modificado para obtener un ejemplo más pequeño de los datos, para que este tutorial sea más rápido. Puede quitar la cláusula TABLESAMPLE si desea obtener todos los datos; sin embargo, en función de su entorno, es posible que no sea posible cargar el conjuntos completo en R, lo que produce un error.
  
5. Use las siguientes líneas de código para llamar a la función de [!INCLUDE[tsql](../../includes/tsql-md.md)] desde su entorno de R y aplicarla a los datos definidos en *featureEngineeringQuery*.
  
    ```R
    featureDataSource = RxSqlServerData(sqlQuery = featureEngineeringQuery,
      colClasses = c(pickup_longitude = "numeric", pickup_latitude = "numeric",
        dropoff_longitude = "numeric", dropoff_latitude = "numeric",
        passenger_count  = "numeric", trip_distance  = "numeric",
        trip_time_in_secs  = "numeric", direct_distance  = "numeric"),
      connectionString = connStr)
    ```
  
6.  Ahora que se ha creado la nueva característica, llame a **rxGetVarsInfo** para crear un resumen de los datos en la tabla de características.
  
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
    > En algunos casos, podría recibir un error similar al siguiente: *Se denegó el permiso Execute en el objeto ' fnCalculateDistance '* Si es así, asegúrese de que el inicio de sesión que usa tiene permisos para ejecutar scripts y crear objetos en la base de datos, no solo en la instancia.
    > Compruebe el esquema del objeto, fnCalculateDistance. Si el objeto fue creado por el propietario de la base de datos y el inicio de sesión pertenece al rol db_datareader, debe conceder al inicio de sesión permisos explícitos para ejecutar el script.

## <a name="comparing-r-functions-and-sql-functions"></a>Comparación de funciones de R y funciones de SQL

¿Recuerda este fragmento de código que se usa para el código R?

```R
start.time <- proc.time()
<your code here>
used.time <- proc.time() - start.time
print(paste("It takes CPU Time=", round(used.time[1]+used.time[2],2)," seconds, Elapsed Time=", round(used.time[3],2), " seconds to generate features.", sep=""))
```

Puede intentar usarlo con el ejemplo de función personalizada de SQL para ver cuánto tiempo tarda la transformación de datos al llamar a una función de SQL. Además, intente cambiar los contextos de cálculo con rxSetComputeContext y compare los tiempos.

Los tiempos pueden variar significativamente, en función de la velocidad de la red y de la configuración del hardware. En las configuraciones probadas, el [!INCLUDE[tsql](../../includes/tsql-md.md)] enfoque de la función era más rápido que usar una función personalizada de R. Por lo tanto, se usa [!INCLUDE[tsql](../../includes/tsql-md.md)] la función para estos cálculos en pasos posteriores.

> [!TIP]
> Con mucha frecuencia, el diseño [!INCLUDE[tsql](../../includes/tsql-md.md)] de características con será más rápido que R. Por ejemplo, T-SQL incluye funciones de clasificación y ventanas rápidas que se pueden aplicar a cálculos de ciencia de datos comunes, como medias móviles graduales y *n*-mosaicos. Elija el método más eficaz en función de los datos y la tarea.

## <a name="next-steps"></a>Pasos siguientes

> [!div class="nextstepaction"]
> [Compilar un modelo de R y guardarlo en SQL](walkthrough-build-and-save-the-model.md)

