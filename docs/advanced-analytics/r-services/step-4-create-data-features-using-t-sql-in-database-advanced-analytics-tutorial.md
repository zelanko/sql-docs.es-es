---
title: "Step 4: Create Data Features using T-SQL (In-Database Advanced Analytics Tutorial) (Paso 4: Crear caracter&#237;sticas de datos mediante T-SQL (Tutorial de an&#225;lisis avanzado de bases de datos)) | Microsoft Docs"
ms.custom: ""
ms.date: "04/19/2016"
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
  - "TSQL"
ms.assetid: 5b2f4c44-6192-40df-abf1-fc983844f1d0
caps.latest.revision: 10
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 10
---
# Step 4: Create Data Features using T-SQL (In-Database Advanced Analytics Tutorial) (Paso 4: Crear caracter&#237;sticas de datos mediante T-SQL (Tutorial de an&#225;lisis avanzado de bases de datos))
Después de varias series de exploración de datos, ha recopilado conocimientos de los datos y está listo para pasar a la *ingeniería de funciones*. Este proceso de creación de características a partir de los datos sin procesar es un paso crítico en el modelado de análisis avanzado.  
  
En este paso, aprenderá a crear características desde datos sin procesar mediante una función de [!INCLUDE[tsql](../../includes/tsql-md.md)]. Después, llamaremos a esa función desde un procedimiento almacenado para crear una tabla que contiene los valores de las características.  
  
## Definir la función  
Los valores de distancia notificados en los datos originales se basan en la distancia notificada del taxímetro y no representan necesariamente la distancia geográfica o la distancia recorrida. Por tanto, debe calcular la distancia directa entre los puntos de origen y destino, usando las coordenadas disponibles en el conjunto de datos de origen NYC Taxi. Puede hacerlo mediante la [fórmula Haversine](https://en.wikipedia.org/wiki/Haversine_formula) en un función personalizada de [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
Usará una función personalizada de T-SQL, _fnCalculateDistance_, para calcular la distancia usando la fórmula Haversine, y una segunda función personalizada de T-SQL, _fnEngineerFeatures_, para crear una tabla que contiene todas las características.  
  
#### Para calcular la distancia de viaje mediante fnCalculateDistance  
  
1.  La función _fnCalculateDistance_ debe haberse descargado y registrado con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] como parte de la preparación para este tutorial. Tómese un minuto para revisar el código  
  
    En [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], expanda **Programación**, expanda **Funciones** y, después, **Funciones escalares**.   
    Haga clic con el botón derecho en _fnCalculateDistance_ y seleccione **Modificar** para abrir el script de [!INCLUDE[tsql](../../includes/tsql-md.md)] en una nueva ventana de consulta.  
  
    ```  
    CREATE FUNCTION [dbo].[fnCalculateDistance] (@Lat1 float, @Long1 float, @Lat2 float, @Long2 float)  
    -- User-defined function that calculates the direct distance between two geographical coordinates.  
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
    GO  
  
    ```  
  
    -   La función es una función escalar y devuelve un único valor de datos de un tipo predefinido.  
  
    -   Toma los valores de latitud y longitud como entradas, obtenidos de las ubicaciones de origen y destino de los viajes. La fórmula Haversine convierte ubicaciones en radianes y usa esos valores para calcular la distancia directa en millas entre las dos ubicaciones.  
  
Para agregar el valor calculado a una tabla y poder usarlo para entrenar el modelo, deberá usar otra función, _fnEngineerFeatures_.  
  
#### Para guardar las características mediante _fnEngineerFeatures_  
  
1.  Tómese un minuto para revisar el código de la función personalizada de T-SQL, _fnEngineerFeatures_, que debe haberse creado como parte de la preparación para este tutorial.  
  
    Esta función es una función con valores de tabla que toma varias columnas como entradas y genera una tabla con varias columnas de características.  El propósito de esta función es crear un conjunto de características para usar en la creación de un modelo. La función _fnEngineerFeatures_ llama a la función de T-SQL creada anteriormente, _fnCalculateDistance_, para obtener la distancia directa entre las ubicaciones de origen y destino.  
  
    ```  
    CREATE FUNCTION [dbo].[fnEngineerFeatures] (  
    @passenger_count int = 0,  
    @trip_distance float = 0,  
    @trip_time_in_secs int = 0,  
    @pickup_latitude float = 0,  
    @pickup_longitude float = 0,  
    @dropoff_latitude float = 0,  
    @dropoff_longitude float = 0)  
    RETURNS TABLE  
    AS  
      RETURN  
      (  
      -- Add the SELECT statement with parameter references here  
      SELECT  
        @passenger_count AS passenger_count,  
        @trip_distance AS trip_distance,  
        @trip_time_in_secs AS trip_time_in_secs,  
        [dbo].[fnCalculateDistance](@pickup_latitude, @pickup_longitude, @dropoff_latitude, @dropoff_longitude) AS direct_distance  
  
      )  
    GO  
  
    ```  
  
2.  Para comprobar que esta función funciona, puede usarla para calcular la distancia geográfica de los viajes en los que la distancia medida era 0 pero las ubicaciones de origen y destino eran diferentes.  
  
    ```  
        SELECT tipped, fare_amount, passenger_count,(trip_time_in_secs/60) as TripMinutes,  
        trip_distance, pickup_datetime, dropoff_datetime,   
        dbo.fnCalculateDistance(pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) AS direct_distance  
        FROM nyctaxi_sample  
        WHERE pickup_longitude != dropoff_longitude and pickup_latitude != dropoff_latitude and trip_distance = 0  
        ORDER BY trip_time_in_secs DESC  
    ```  
  
    Como puede ver, la distancia notificada por el taxímetro no siempre se corresponde con la distancia geográfica. Por eso es tan importante la ingeniería de características.  
  
En el paso siguiente, aprenderá cómo usar estas características de datos para entrenar un modelo de aprendizaje automático con R.  
  
## Paso siguiente  
[Paso 5: Entrenar y guardar un modelo con T-SQL](../../advanced-analytics/r-services/step-5-train-and-save-a-model-using-t-sql.md)  
  
## Paso anterior  
[Paso 3: Explorar y visualizar los datos](../../advanced-analytics/r-services/step-3-explore-and-visualize-the-data-in-database-advanced-analytics-tutorial.md)  
  
## Vea también  
[In-Database Advanced Analytics for SQL Developers &#40;Tutorial&#41; (Análisis avanzado en base de datos para desarrolladores de SQL &#40;Tutorial&#41;)](../../advanced-analytics/r-services/in-database-advanced-analytics-for-sql-developers-tutorial.md)  
[Tutoriales de SQL Server R Services](../../advanced-analytics/r-services/sql-server-r-services-tutorials.md)  
  
  
  
