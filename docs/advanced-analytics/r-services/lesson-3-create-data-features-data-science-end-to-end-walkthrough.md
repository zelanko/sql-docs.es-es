---
title: "Lesson 3: Create Data Features (Data Science End-to-End Walkthrough) [Lecci&#243;n 3: Crear caracter&#237;sticas de datos (Tutorial integral de ciencia de datos)] | Microsoft Docs"
ms.custom: ""
ms.date: "11/22/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to: 
  - "SQL Server 2016"
dev_langs: 
  - "R"
ms.assetid: 4981d4eb-0874-4fe9-82e1-edf99890e27a
caps.latest.revision: 21
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 17
---
# Lesson 3: Create Data Features (Data Science End-to-End Walkthrough) [Lecci&#243;n 3: Crear caracter&#237;sticas de datos (Tutorial integral de ciencia de datos)]
La ingeniería de datos es otro aspecto importante del aprendizaje automático. A menudo los datos deben transformarse antes de poder usarlos para el modelado de predicción. Si los datos no tienen las características que necesita, puede diseñarlos a partir de valores existentes.  
  
Para esta tarea de modelado, en lugar de usar los valores de latitud y longitud sin procesar de la ubicación de origen y destino, le gustaría tener la distancia en millas entre las dos ubicaciones. Para crear esta característica, calculará la distancia directa en línea entre dos puntos, usando la [fórmula haversine](https://en.wikipedia.org/wiki/Haversine_formula).  
Comparará dos métodos diferentes para crear una característica a partir de los datos:  
  
-   Usar R y la función `rxDataStep`    
-   Usar una función personalizada en [!INCLUDE[tsql](../../includes/tsql-md.md)]  
  
Para ambos métodos, el resultado del código es un objeto de origen de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , `featureDataSource`, que incluye la nueva característica numérica, `direct_distance`.  
  
## <a name="creating-features-using-r"></a>Creación de características mediante R  

El lenguaje R es conocido por sus completas y variadas bibliotecas estadísticas, pero también podría necesitar crear transformaciones de datos personalizadas. 

+ Creará una nueva función de R, `ComputeDist`, para calcular la distancia lineal entre dos puntos especificados mediante valores de latitud y longitud.  
+ Llamará a la función para transformar los datos del objetos de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que creó anteriormente y los guardará en nuevo origen de datos, `featureDataSource`.  

### <a name="create-the-transformation-function"></a>Crear la función de transformación  
1.  Cree una función personalizada de R, `ComputeDist`. Toma dos pares de valores de latitud y longitud, y calcula la distancia lineal entre ellos.  Esta función devuelve una distancia en millas.
  
    ```R  
    env <- new.env()  
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
  
    + La primera línea define un nuevo entorno. En R, se puede usar un entorno para encapsular los espacios de nombres en paquetes y similares.
    + Puede usar la función `search()` para ver los entornos en el área de trabajo. Para ver los objetos en un entorno específico, escriba `ls(<envname>)`. 
    + Las líneas que comienzan con `$env.ComputeDistance` contienen el código que define la fórmula haversine, que calcula la *distancia del círculo máximo* entre dos puntos en una esfera.  
 
  
### <a name="apply-the-transformation-function-to-data"></a>Aplicar la función de transformación a los datos

Después de definir la función, se aplicará a los datos para crear una nueva columna de característica, *direct_distance*.

1. Cree un origen de datos con el cual trabajar mediante el constructor `RxSqlServerData`.  
  
    ```R  
    featureDataSource = RxSqlServerData(table = "features",   
       colClasses = c(pickup_longitude = "numeric", 
       pickup_latitude = "numeric",   
       dropoff_longitude = "numeric", 
       dropoff_latitude = "numeric",  
       passenger_count  = "numeric", 
       trip_distance  = "numeric",  
       trip_time_in_secs  = "numeric", 
       direct_distance  = "numeric"),  
      connectionString = connStr)  
    ```  
  
3.  Llame a la función `rxDataStep` para aplicar la función `env$ComputeDist` a los datos especificados.  
    
    ```R  
    start.time <- proc.time()  
  
    rxDataStep(inData = inDataSource, outFile = featureDataSource,  
         overwrite = TRUE,  
         varsToKeep=c("tipped", "fare_amount", passenger_count", "trip_time_in_secs", 
            "trip_distance", "pickup_datetime", "dropoff_datetime", "pickup_longitude",
            "pickup_latitude", "dropoff_longitude", "dropoff_latitude")
         , transforms = list(direct_distance=ComputeDist(pickup_longitude, 
            pickup_latitude, dropoff_longitude, dropoff_latitude)),
            transformEnvir = env, rowsPerRead=500, reportProgress = 3)  
  
    used.time <- proc.time() - start.time  
    print(paste("It takes CPU Time=", round(used.time[1]+used.time[2],2)," seconds, Elapsed Time=", round(used.time[3],2), " seconds to generate features.", sep=""))    
    ```  
  
    + La función `rxDataStep` puede modificar los datos de forma local. Los argumentos incluyen un vector de caracteres de columnas que se pasa (*varsToKeep*) y una lista que define las transformaciones.
    + Las columnas que se transforman se generan automáticamente como resultados y, por tanto, no es necesario incluirlas en el argumento *varsToKeep* .
    + Como alternativa, puede especificar que se incluyan todas las columnas en el origen, excepto las variables especificadas, usando el argumento *varsToDrop* .  
  
4.  Por último, llame a `rxGetVarInfo` para inspeccionar el esquema del nuevo origen de datos:  
  
    ```R  
    rxGetVarInfo(data = featureDataSource)  
    ```  
  
    *Resultados*
    
    *"Se necesita Tiempo de CPU=0,74 segundos, Tiempo transcurrido=35,75 segundos para generar características."*  
    *Var 1: tipped, Type: integer*   
    *Var 2: fare_amount, Type: numeric*   
    *Var 3: passenger_count, Type: numeric*   
    *Var 4: trip_time_in_secs, Type: numeric*   
    *Var 5: trip_distance, Type: numeric*   
    *Var 6: pickup_datetime, Type: character*   
    *Var 7: dropoff_datetime, Type: character*   
    *Var 8: pickup_longitude, Type: numeric*   
    *Var 9: pickup_latitude, Type: numeric*   
    *Var 10: dropoff_longitude, Type: numeric*   
    *Var 11: dropoff_latitude, Type: numeric*   
    *Var 12: direct_distance, Type: numeric*   
  
## <a name="creating-features-using-transact-sql"></a>Creación de características mediante Transact-SQL  
Ahora que ha visto cómo crear una característica mediante una función de R, usará una función personalizada de SQL, `ComputeDist`, para hacer lo mismo. La función `ComputeDist` de SQL opera en un objeto de datos `RxSqlServerData` existente para crear las nuevas características de distancia a partir de los valores de longitud y latitud existentes.  
  
Deberá guardar los resultados de la transformación en un objeto de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , `featureDataSource`, tal como hizo con R.  
  
Con frecuencia, la ingeniería de características con [!INCLUDE[tsql](../../includes/tsql-md.md)] será más rápida que con R. Elija el método más eficaz en función de los datos y la tarea.  

### <a name="define-the-t-sql-custom-function"></a>Definir la función T-SQL personalizada
  
1.  Defina una nueva función SQL, `fnCalculateDistance`  
  
    ```tsql  
    CREATE FUNCTION [dbo].[fnCalculateDistance] (@Lat1 float, @Long1 float, @Lat2 float, @Long2 float)  
    -- User-defined function calculates the direct distance between two geographical coordinates.  
    RETURNS float  
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

    + El código para esta *función definida por el usuario* de SQL se proporcionó como parte del script de PowerShell que ejecutó para crear y configurar la base de datos.  La función ya debe existir en la base de datos.  Si no existe, use SQL Server Management Studio para generar la función en la misma base de datos donde están almacenados los datos de taxis.

2.  Para ver cómo trabaja la función, la siguiente instrucción [!INCLUDE[tsql](../../includes/tsql-md.md)] desde cualquier aplicación que admite [!INCLUDE[tsql](../../includes/tsql-md.md)].   
  
    ```tsql  
    SELECT tipped, fare_amount, passenger_count,trip_time_in_secs,trip_distance, pickup_datetime, dropoff_datetime,       
    dbo.fnCalculateDistance(pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) as direct_distance,  
    pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude   
    FROM nyctaxi_sample  
  
    ```  
### <a name="call-the-sql-function-from-r"></a>Llamar a la función SQL desde R

1. Guarde la instrucción SQL que llama a la función personalizada en una variable de R.  
  
    ```R  
    featureEngineeringQuery = "SELECT tipped, fare_amount, passenger_count,  
        trip_time_in_secs,trip_distance, pickup_datetime, dropoff_datetime,   
        dbo.fnCalculateDistance(pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) as direct_distance,  
        pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude  
        FROM nyctaxi_joined_1_percent  
        tablesample (1 percent) repeatable (98052)"    
    ```  
  
    > [!TIP] Esta consulta es ligeramente diferente de la consulta [!INCLUDE[tsql](../../includes/tsql-md.md)] que usó anteriormente. Se modificó para obtener una muestra más pequeña de los datos, para realizar este tutorial con mayor rapidez.  
  
4.  Ahora, use las siguientes líneas de código para llamar a la función de [!INCLUDE[tsql](../../includes/tsql-md.md)] desde su entorno de R y aplicarla a los datos definidos en `featureEngineeringQuery`.  
  
    ```R  
    featureDataSource = RxSqlServerData(sqlQuery = featureEngineeringQuery,  
      colClasses = c(pickup_longitude = "numeric", pickup_latitude = "numeric",           
             dropoff_longitude = "numeric", dropoff_latitude = "numeric",  
             passenger_count  = "numeric", trip_distance  = "numeric",  
              trip_time_in_secs  = "numeric", direct_distance  = "numeric"),  
      connectionString = connStr)  
    ```  
  
5.  Ahora que se creó la característica nueva, llame a `rxGetVarsInfo` para crear un resumen de la tabla de características.  
  
    ```R  
    rxGetVarInfo(data = featureDataSource)  
    ```  
  
## <a name="comparing-r-functions-and-sql-functions"></a>Comparar funciones de R y funciones de SQL

Según parece, para esta tarea concreta, el enfoque de la función de [!INCLUDE[tsql](../../includes/tsql-md.md)] es más rápido que la función personalizada de R. Por lo tanto, en los pasos siguientes usará la función de [!INCLUDE[tsql](../../includes/tsql-md.md)] para estos cálculos.  

Continúe con la lección siguiente para obtener información sobre cómo crear un modelo de predicción con estos datos y guardar el modelo a una tabla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="next-lesson"></a>Lección siguiente  
[Lección 4: Generar y guardar el modelo &#40;Tutorial integral de ciencia de datos&#41;](../../advanced-analytics/r-services/lesson-4-build-and-save-the-model-data-science-end-to-end-walkthrough.md)  
  
## <a name="previous-lesson"></a>Lección anterior  
[Lección 2: Ver y explorar los datos &#40;Tutorial integral de ciencia de datos&#41;](../../advanced-analytics/r-services/lesson-2-view-and-explore-the-data-data-science-end-to-end-walkthrough.md)  
  
  
  
