---
title: "Lecci&#243;n 5: Implementar y usar el modelo (Tutorial integral de ciencia de datos) | Microsoft Docs"
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
ms.assetid: f28a7aac-6d08-4781-ad28-b48d18cc16a0
caps.latest.revision: 17
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 17
---
# Lecci&#243;n 5: Implementar y usar el modelo (Tutorial integral de ciencia de datos)
En esta lección, usará los modelos de R en un entorno de producción; para ello, ajustará el modelo guardado en un procedimiento almacenado. Después puede invocar el procedimiento almacenado de R o cualquier lenguaje de programación de aplicación compatible con [!INCLUDE[tsql](../../includes/tsql-md.md)] (como C#, Java, Python, etc.) para usar el modelo para realizar predicciones en observaciones nuevas.  
  
Hay dos formas de llamar a un modelo para obtener la puntuación:  
  
-   El**modo de puntuación por lotes** le permite crear varias predicciones según la entrada de una consulta SELECT.  
  
-   El**modo de puntuación individual** le permite crear predicciones de una en una; para ello, pase un conjunto de valores de características para un caso individual al procedimiento almacenado, que devuelve una sola predicción u otro valor como resultado.  
  
Aprenderá a crear predicciones mediante los métodos de puntuación por lotes e individual.  
  
## <a name="batch-scoring"></a>Puntuación por lotes  
Para mayor comodidad, puede usar un procedimiento almacenado creado al ejecutar al principio el script de PowerShell en la lección 1. Este procedimiento almacenado hace lo siguiente:  
  
-   Obtiene un conjunto de datos de entrada como una consulta SQL    
-   Llama al modelo de regresión logística entrenado que ha guardado en la lección anterior    
-   Predice la probabilidad de que el conductor reciba una propina  
  
### <a name="use-the-stored-procedure-predicttipbatchmode"></a>Usar el procedimiento almacenado PredictTipBatchMode

1. Le llevará un minuto revisar el script que define el procedimiento almacenado, *PredictTipBatchMode*. Ilustra varios aspectos sobre cómo se puede hacer operativo un modelo mediante [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)].  
  
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

    + Tenga en cuenta que la instrucción SELECT llama al modelo almacenado. Puede almacenar cualquier modelo entrenado en una tabla SQL mediante una columna de tipo **varbinary(max)**. En este código, el modelo se recupera de la tabla, almacenada en la variable SQL _@lmodel2_, y se pasa como el parámetro *mod* al procedimiento almacenado del sistema [sp_execute_external_script &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md).
    + Los datos de entrada usados para la puntuación se pasan como una cadena al procedimiento almacenado.  
  
        Para definir los datos de entrada para este modelo determinado, cree una consulta que devuelva datos válidos. Cuando se recuperan datos de la base de datos, se almacenan en una trama de datos denominada *InputDataSet*. Todas las filas de esta trama de datos se usan para la puntuación por lotes.
        + *InputDataSet* es el nombre predeterminado para los datos de entrada al procedimiento [sp_execute_external_script &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md); puede definir otro nombre de variable si es necesario.
        + Para generar las puntuaciones, el procedimiento almacenado llama a la función *rxPredict* de la biblioteca **RevoScaleR**.
    + El valor devuelto por el procedimiento almacenado, *Puntuación*, es una probabilidad de predicción de que el conductor recibirá una propina.  
  
2.  De manera opcional, podría aplicar fácilmente algún tipo de filtro a los valores devueltos para clasificarlos en grupos de "Sí: propina" o "Sin propina".  Por ejemplo, una probabilidad menor que 0,5 significaría que no es probable que reciba una propina.  
  
3.  Llame al procedimiento almacenado en el modo por lotes:  
  
    ```R  
    input = "N' 
      SELECT TOP 10 
          a.passenger_count AS passenger_count,   
          a.trip_time_in_secs AS trip_time_in_secs,  
          a.trip_distance AS trip_distance,  
          a.dropoff_datetime AS dropoff_datetime,    
          dbo.fnCalculateDistance(
            pickup_latitude, 
            pickup_longitude, 
            dropoff_latitude,
            dropoff_longitude) AS direct_distance   
      FROM  
      
      (SELECT medallion, hack_license, pickup_datetime,   
      passenger_count,trip_time_in_secs,trip_distance,    
      dropoff_datetime, pickup_latitude, pickup_longitude,   
      dropoff_latitude, dropoff_longitude from nyctaxi_sample)a  
      
      LEFT OUTER JOIN  
 
      ( SELECT medallion, hack_license, pickup_datetime 
        FROM nyctaxi_sample  tablesample (1 percent) repeatable (98052)  )b  

      ON a.medallion=b.medallion 
        AND a.hack_license=b.hack_license 
        AND a.pickup_datetime=b.pickup_datetime  

      WHERE b.medallion is null  
    '"  
    q<-paste("EXEC PredictTipBatchMode @inquery = ", input, sep="")  
    sqlQuery (conn, q)  
  
    ```  
  
## <a name="single-row-scoring"></a>Puntuación de fila única  

En lugar de usar una consulta para pasar los valores de entrada al modelo de R guardado, puede proporcionar las características como argumentos al procedimiento almacenado.  

### <a name="use-the-stored-procedure-predicttipsinglemode"></a>Usar el procedimiento almacenado PredictTipSingleMode
1.  Tómese un minuto para revisar si el código siguiente corresponde al procedimiento almacenado, *PredictTipSingleMode*, que ya debería estar creado en la base de datos.  
  
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
        SELECT * FROM [dbo].[fnEngineerFeatures](@passenger_count, 
            @trip_distance,  
            @trip_time_in_secs,  
            @pickup_latitude,  
            @pickup_longitude,  
            @dropoff_latitude,  
            @dropoff_longitude)  
        '  
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
      @params = N'@model varbinary(max),
                @passenger_count int,
                @trip_distance float,
                @trip_time_in_secs int ,  
                @pickup_latitude float ,
                @pickup_longitude float ,
                @dropoff_latitude float ,
                @dropoff_longitude float',  
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
  
    Esta procedimiento almacenado toma valores de característica como entrada, como la distancia del viaje y el número de pasajeros, puntúa estas características mediante el modelo de R almacenado y genera una puntuación.  
  
### <a name="call-the-stored-procedure-and-pass-parameters"></a>Llamar al procedimiento almacenado y pasar parámetros

1. En SQL Server Management Studio, pude usar [!INCLUDE[tsql](../../includes/tsql-md.md)] **EXEC** para llamar al procedimiento almacenado y pasar las entradas requeridas. .  
    ```tsql  
    EXEC [dbo].[PredictTipSingleMode] 1, 2.5, 631, 40.763958,-73.973373, 40.782139,-73.977303   
    ```  
  
    Los valores pasados aquí son, respectivamente, para las variables _passenger_count_, _trip_distance_, _trip_time_in_secs_, _pickup_latitude_, _pickup_longitude_, _dropoff_latitude_y _dropoff_longitude_.  
  
2.  Para ejecutar esta misma llamada desde el código R, simplemente defina una variable de R que contenga toda la llamada al procedimiento almacenado. 
  
    ```R  
    q = "EXEC PredictTipSingleMode 1, 2.5, 631, 40.763958,-73.973373, 40.782139,-73.977303 "  
    ```  
  
    Los valores pasados aquí son, respectivamente, para las variables _passenger_count_, _trip_distance_, _trip_time_in_secs_, _pickup_latitude_, _pickup_longitude_, _dropoff_latitude_y _dropoff_longitude_.  
  
### <a name="generate-scores"></a>Generar puntuaciones

1. Llame a la función *sqlQuery* del paquete **RODBC** y pase la cadena de conexión y la variable de cadena que contenga la llamada al procedimiento almacenado.  
  
    ```R  
    # predict with stored procedure in single mode  
    sqlQuery (conn, q)   
    ```  
  
    Para más información sobre **RODBC**, consulte [http://www.inside-r.org/packages/cran/RODBC/docs/sqlQuery](http://www.inside-r.org/packages/cran/RODBC/docs/sqlQuery).  
  
## <a name="conclusion"></a>Conclusión  
Ahora que ha aprendido a trabajar con datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y conservar modelos entrenados de R para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], debería serle relativamente fácil crear algunos modelos adicionales basados en este conjunto de datos. Por ejemplo, puede intentar crear modelos como estos:  
  
-   Un modelo de regresión que predice la cantidad de propina    
-   Un modelo de clasificación de varias clases que predice si la propina será pequeña, mediana o grande.  

También se recomienda que revise algunos ejemplos y recursos adicionales: 
+ [Escenarios de ciencia de datos y plantillas de soluciones](../../advanced-analytics/r-services/data-science-scenarios-and-solution-templates.md)
+ [Análisis avanzado en base de datos](../../advanced-analytics/r-services/in-database-advanced-analytics-for-sql-developers-tutorial.md)
+ [Microsoft R - Diving into Data Analysis](https://msdn.microsoft.com/microsoft-r/data-analysis-in-microsoft-r) (Microsoft R: profundizar en Análisis de datos)
+ [Recursos adicionales](https://msdn.microsoft.com/microsoft-r/microsoft-r-more-resources)
## <a name="previous-lesson"></a>Lección anterior  
[Lección 4: Generar y guardar el modelo &#40;Tutorial integral de ciencia de datos&#41;](../../advanced-analytics/r-services/lesson-4-build-and-save-the-model-data-science-end-to-end-walkthrough.md)  
  
## <a name="see-also"></a>Vea también  
[Tutoriales de SQL Server R Services](../../advanced-analytics/r-services/sql-server-r-services-tutorials.md)  
  
  
  
