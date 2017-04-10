---
title: "Step 6: Operationalize the Model (In-Database Advanced Analytics Tutorial) [Paso 6: Hacer operativo el modelo (Tutorial de base de datos de an&#225;lisis avanzado)] | Microsoft Docs"
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
ms.assetid: 52b05828-11f5-4ce3-9010-59c213a674d1
caps.latest.revision: 11
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 11
---
# Step 6: Operationalize the Model (In-Database Advanced Analytics Tutorial) [Paso 6: Hacer operativo el modelo (Tutorial de base de datos de an&#225;lisis avanzado)]
En este paso, aprenderá a *hacer operativo* el modelo mediante un procedimiento almacenado. Este procedimiento almacenado se puede llamar directamente por otras aplicaciones, para realizar predicciones en nuevas observaciones.  
  
En este paso, aprenderá dos métodos para llamar a un modelo de R desde un procedimiento almacenado:  
  
-   **Modo de puntuación por lotes**: usar una consulta SELECT para proporcionar varias filas de datos. El procedimiento almacenado devuelve una tabla de observaciones correspondientes a los casos de entrada.  
  
-   **Modo de puntuación individual**: pasar un conjunto de valores de parámetros individuales como entrada.  El procedimiento almacenado devuelve una sola fila o valor.  
  
En primer lugar, veremos cómo funcionan las puntuaciones en general.  
  
## Puntuaciones básicas  
El procedimiento almacenado _PredictTip_ muestra la sintaxis básica para ajustar una llamada de predicción en un procedimiento almacenado.  
  
```  
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
  
-   La instrucción SELECT obtiene el modelo serializado de la base de datos y lo almacena en la variable de R `mod` para su posterior procesamiento con R.  
  
-   Los nuevos casos que se van a puntuar se obtienen de la consulta de [!INCLUDE[tsql](../../includes/tsql-md.md)] especificada en `@inquery`, el primer parámetro del procedimiento almacenado. Cuando se leen los datos de la consulta, las filas se guardan en la trama de datos predeterminada, `InputDataSet`. Esta trama de datos se pasa a la función `rxPredict` de R, que genera las puntuaciones.  
  
    `OutputDataSet<-rxPredict(modelObject = mod, data = InputDataSet, outData = NULL,            predVarNames = "Score", type = "response", writeModelVars = FALSE, overwrite = TRUE);`  
  
    Como data.frame puede contener una sola fila, puede usar el mismo código para la puntuación individual o por lotes.  
  
-   El valor devuelto por la función `rxPredict` es un **float** que representa la probabilidad de que se dé una propina (de cualquier importe).  
  
## Puntuación por lotes con una consulta SELECT  
Ahora veamos cómo funciona la puntuación por lotes.  
  
1.  Para empezar se obtiene un conjunto más pequeño de los datos de entrada con el que trabajar.  
  
    ```  
    select top 10 a.passenger_count as passenger_count,   
        a.trip_time_in_secs as trip_time_in_secs,  
        a.trip_distance as trip_distance,  
        a.dropoff_datetime as dropoff_datetime,    
        dbo.fnCalculateDistance(pickup_latitude, pickup_longitude, dropoff_latitude,dropoff_longitude) as direct_distance   
    from  
    (  
        select medallion, hack_license, pickup_datetime, passenger_count,trip_time_in_secs,trip_distance,    
            dropoff_datetime, pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude  
        from nyctaxi_sample  
    )a  
    left outer join  
    (  
    select medallion, hack_license, pickup_datetime  
    from nyctaxi_sample  
    tablesample (70 percent) repeatable (98052)  
    )b  
    on a.medallion=b.medallion and a.hack_license=b.hack_license and a.pickup_datetime=b.pickup_datetime  
    where b.medallion is null  
    ```  
  
    Esta consulta crea una lista de los "Diez mejores" viajes con número de pasajeros y otras características necesarias para realizar una predicción.  
  
 **Resultado**  
  
*passenger_count   trip_time_in_secs    trip_distance  dropoff_datetime   direct_distance*  
*1  283 0.7 2013-03-27 14:54:50.000   0.5427964547*  
*1  289 0.7 2013-02-24 12:55:29.000   0.3797099614*  
*1  214 0.7 2013-06-26 13:28:10.000   0.6970098661*  
*1  276 0.7 2013-06-27 06:53:04.000   0.4478814362*  
*1  282 0.7 2013-02-21 07:59:54.000   0.5340645749*  
*1  260 0.7 2013-03-27 15:40:49.000   0.5513900727*  
*1  230 0.7 2013-02-05 09:47:59.000   0.5161578519*  
*1  250 0.7 2013-05-08 14:35:51.000   0.5626440915*  
*1  280 0.7 2013-05-11 12:22:01.000   0.5598517959*  
*1  308 0.7 2013-04-10 08:06:00.000   0.4478814362*  
  
Usará esta consulta como entrada para el procedimiento almacenado, _PredictTipBatchMode_, que se proporcionó como parte de la descarga.  
  
2.  En primer lugar, tómese un minuto para revisar el código del procedimiento almacenado _PredictTipBatchMode_ en [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)].  
  
    ```  
    /****** Object:  StoredProcedure [dbo].[PredictTipBatchMode]  ******/  
    SET ANSI_NULLS ON  
    GO  
    SET QUOTED_IDENTIFIER ON  
    GO  
  
    CREATE PROCEDURE [dbo].[PredictTipBatchMode] @inquery nvarchar(max)  
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
    ```  
  
3.  Para crear predicciones, deberá proporcionar el texto de consulta en una variable y pasarla como parámetro al procedimiento almacenado, mediante una instrucción de [!INCLUDE[tsql](../../includes/tsql-md.md)] como esta.  
  
    ```  
    -- Specify input query  
  
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
    left outer join  
    (  
    select medallion, hack_license, pickup_datetime  
    from nyctaxi_sample  
    tablesample (70 percent) repeatable (98052)  
    )b  
    on a.medallion=b.medallion and a.hack_license=b.hack_license and a.pickup_datetime=b.pickup_datetime  
    where b.medallion is null'  
  
    -- Call stored procedure for scoring  
    EXEC [dbo].[PredictTip] @inquery = @query_string;  
  
    ```  
  
4.  El procedimiento almacenado devuelve una serie de valores que representan la predicción para cada uno de los "Diez mejores viajes". Si volvemos a los valores de entrada, todos los "Diez mejores viajes" son viajes con un único pasajero y una distancia de viaje relativamente corta. En función de los datos, es muy poco probable que el conductor consiga una propina en este tipo de viajes.  
  
    En lugar de devolver resultados de tipo propina sí/propina no, podría también devolver la puntuación de probabilidad de la predicción y, después, aplicar una cláusula WHERE a los valores de la columna _Score_ para clasificar el resultado como "propina probable" o "propina improbable", con un valor de umbral como 0,5 o 0,7. Este paso no se incluye en el procedimiento almacenado, pero es fácil de implementar.  
  
## Puntuar filas individuales  
A veces querrá pasar valores individuales de una aplicación y obtener un resultado único basado en esos valores. Por ejemplo, podría configurar una hoja de cálculo de Excel, una aplicación web o un informe de Reporting Services para llamar al procedimiento almacenado y proporcionar entradas escritas o seleccionadas por los usuarios.  
  
En esta sección, aprenderá a crear predicciones únicas mediante un procedimiento almacenado.  
  
1.  Tómese un minuto para revisar el código del procedimiento almacenado _PredictTipSingleMode_, que se incluye como parte de la descarga.  
  
    ```  
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
  
    -   Este procedimiento almacenado toma varios valores únicos como entrada, como el número de pasajeros, la distancia del viaje y así sucesivamente.  
  
        Si llama al procedimiento almacenado desde una aplicación externa, asegúrese de que los datos coinciden con los requisitos del modelo de R. Esto puede incluir asegurarse de que los datos de entrada se pueden convertir a un tipo de datos R o validar el tipo y la longitud de los datos. Para obtener más información, consulte [Trabajar con tipos de datos de R](https://msdn.microsoft.com/library/mt590948.aspx).  
  
    -   El procedimiento almacenado crea una puntuación basada en el modelo almacenado de R.  
  
2.  Pruébelo, proporcionando los valores manualmente.  
  
    Abra una nueva ventana **Consulta** y llame al procedimiento almacenado, escribiendo parámetros para cada una de las columnas de característica.  
  
    ```  
  
    EXEC [dbo].[PredictTipSingleMode] 1, 2.5, 631, 40.763958,-73.973373, 40.782139,-73.977303  
  
    ```  
  
    Para estas columnas de característica, los valores son, en orden:  
  
    -   *trip_time_in_secs*  
    -   *pickup_latitude*  
    -   *pickup_longitude*  
    -   *dropoff_latitude*  
    -   *dropoff_longitude*  
  
3.  Los resultados indican que la probabilidad de obtener una propina es muy escasa en estos diez mejores viajes, que son todos viajes con un único pasajero en una distancia relativamente corta.  
  
## Conclusiones  
En este tutorial, ha aprendido a trabajar con código de R incrustado en procedimientos almacenados. La integración con [!INCLUDE[tsql](../../includes/tsql-md.md)] hace mucho más fácil la implementación de modelos de R para la predicción y la incorporación del reciclaje de modelos como parte de un flujo de trabajo de datos empresarial.  
  
  
## Paso anterior  
[Paso 4: Crear características de datos mediante T-SQL](../../advanced-analytics/r-services/step-4-create-data-features-using-t-sql-in-database-advanced-analytics-tutorial.md)  
  
## Vea también  
[In-Database Advanced Analytics for SQL Developers &#40;Tutorial&#41; (Análisis avanzado en base de datos para desarrolladores de SQL &#40;Tutorial&#41;)](../../advanced-analytics/r-services/in-database-advanced-analytics-for-sql-developers-tutorial.md)  
[Tutoriales de SQL Server R Services](../../advanced-analytics/r-services/sql-server-r-services-tutorials.md)  
  
  
  
