---
title: "Paso 5: Entrenar y guardar un modelo con T-SQL (Tutorial de an&#225;lisis avanzado de bases de datos) | Microsoft Docs"
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
ms.assetid: 3282e8ed-b515-4ed5-8543-fcef68629a92
caps.latest.revision: 10
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 10
---
# Paso 5: Entrenar y guardar un modelo con T-SQL (Tutorial de an&#225;lisis avanzado de bases de datos)
En este paso, aprenderá a entrenar un modelo de aprendizaje automático mediante el uso de R. Los paquetes de R ya están instalados con [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] de modo que puede llamar al desde un procedimiento almacenado. Puede entrenar el modelo mediante las características de datos que acaba de crear y, después, guardar el modelo entrenado en una tabla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## Generación de un modelo de R mediante procedimientos almacenados  
Todas las llamadas al tiempo de ejecución de R que se instala con [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] se realizan mediante el procedimiento almacenado del sistema [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md). Pero si necesita volver a entrenar un modelo, probablemente es más fácil encapsular la llamada a sp_execute_exernal_script en otro procedimiento almacenado.  
  
En esta sección, creará un procedimiento almacenado que se puede usar para generar un modelo usando los datos que acaba de preparar. Este procedimiento almacenado define los datos de entrada y usa un paquete de R para crear un modelo de regresión logística.  
  
#### Para crear el procedimiento almacenado  
  
1.  En [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], abra una nueva ventana de consulta y ejecute la instrucción siguiente para crear el procedimiento almacenado _TrainTipPredictionModel_.  
  
    Observe que, como el procedimiento almacenado ya incluye una definición de los datos de entrada, no es necesario proporcionar una consulta de entrada.  
  
    ```  
    CREATE PROCEDURE [dbo].[TrainTipPredictionModel]  
  
    AS  
    BEGIN  
      DECLARE @inquery nvarchar(max) = N'  
        select tipped, fare_amount, passenger_count,trip_time_in_secs,trip_distance,   
        pickup_datetime, dropoff_datetime,   
        dbo.fnCalculateDistance(pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) as direct_distance  
        from nyctaxi_sample  
        tablesample (70 percent) repeatable (98052)  
    '  
      -- Insert the trained model into a database table  
      INSERT INTO nyc_taxi_models  
      EXEC sp_execute_external_script @language = N'R',  
                                      @script = N'  
  
    ## Create model  
    logitObj <- rxLogit(tipped ~ passenger_count + trip_distance + trip_time_in_secs + direct_distance, data = InputDataSet)  
    summary(logitObj)  
  
    ## Serialize model and put it in data frame  
    trained_model <- data.frame(model=as.raw(serialize(logitObj, NULL)));  
    ',  
                                      @input_data_1 = @inquery,  
                                      @output_data_1_name = N'trained_model'  
      ;  
  
    END  
    GO  
  
    ```  
  
    Este procedimiento almacenado realiza estas actividades como parte del entrenamiento del modelo:  
  
    -   Para asegurarse de que se dejan algunos datos para probar el modelo, el 70% de los datos se seleccionan aleatoriamente de la tabla de datos de taxi.  
  
    -   La consulta SELECT usa la función escalar personalizada _fnCalculateDistance_ para calcular la distancia directa entre las ubicaciones de origen y destino.  Los resultados de la consulta se almacenan en la variable de entrada predeterminada de R `InputDataset`.  
  
    -   El script de R llama a la función `rxLogit`, que es una de las funciones mejoradas de R incluida con [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], para crear el modelo de regresión logística.  
  
        La variable binaria _tipped_ se usa como la *etiqueta* o columna del resultado y el modelo se ajusta mediante estas columnas específicas: _passenger_count_, _trip_distance_, _trip_time_in_secs_ y _direct_distance_.  
  
    -   El modelo entrenado, guardado en la variable de R `logitObj`, se serializa y se coloca en una trama de datos de salida a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Esa salida se inserta en la tabla de base de datos _nyc_taxi_models_, para que la puede usar para predicciones futuras.  
  
2.  Ejecute la instrucción para crear el procedimiento almacenado.  
  
#### Para crear el modelo de R usando el procedimiento almacenado  
  
1.  En [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], ejecute esta instrucción.  
  
    ```  
    EXEC TrainTipPredictionModel  
    ```  
  
    Es posible que el procesamiento de los datos y el ajuste del modelo tarden un rato. Los mensajes que se canalicen al flujo **stdout** de R se muestran en la ventana **Mensajes** de [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]. Por ejemplo:  
  
  
*Mensaje(s) STDOUT del script externo: Filas leídas: 1193025, Total de filas procesadas: 1193025, Tiempo total de los fragmentos: 0,093 segundos*       
  
Los fragmentos sucesivos de datos se leen y se procesan. Es posible que también vea mensajes específicos de la función individual, `rxLogit`, que indican la variable y métrica de pruebas.  
  
2.  Abra la tabla *nyc_taxi_models*. Puede ver que se ha agregado una fila nueva, que contiene el modelo serializado en la columna _modelo_.  
  
  
  
*modelo*  
*0x580A00000002000302020....*  
  
En el siguiente paso usará el modelo entrenado para crear predicciones.  
  
## Paso siguiente  
[Paso 6: Hacer operativo el modelo](../../advanced-analytics/r-services/step-6-operationalize-the-model-in-database-advanced-analytics-tutorial.md)  
  
## Paso anterior  
[Paso 4: Crear características de datos mediante T-SQL](../../advanced-analytics/r-services/step-4-create-data-features-using-t-sql-in-database-advanced-analytics-tutorial.md)  
  
## Vea también  
[In-Database Advanced Analytics for SQL Developers &#40;Tutorial&#41; (Análisis avanzado en base de datos para desarrolladores de SQL &#40;Tutorial&#41;)](../../advanced-analytics/r-services/in-database-advanced-analytics-for-sql-developers-tutorial.md)  
[Tutoriales de SQL Server R Services](../../advanced-analytics/r-services/sql-server-r-services-tutorials.md)  
  
  
  
