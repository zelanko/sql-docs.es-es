---
title: "Lección 5: Entrenar y guardar un modelo mediante T-SQL | Documentos de Microsoft"
ms.custom: 
ms.date: 07/26/2016
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
applies_to: SQL Server 2016
dev_langs:
- R
- TSQL
ms.assetid: 3282e8ed-b515-4ed5-8543-fcef68629a92
caps.latest.revision: "10"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: 2ef4f1ee437a2999d8fa8c1aac27bb4fa64f5c76
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/25/2018
---
# <a name="lesson-5-train-and-save-a-model-using-t-sql"></a>Lección 5: Entrenar y guardar un modelo mediante T-SQL

Este artículo forma parte de un tutorial para desarrolladores de SQL sobre cómo usar R en SQL Server.

En esta lección, aprenderá a entrenar un modelo de aprendizaje automático mediante el uso de R. Podrá entrenar el modelo mediante las características de datos que acaba de crear y, a continuación, guarde el modelo entrenado en un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tabla. En este caso, los paquetes de R ya están instalados con [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], por lo que todo lo que puede realizarse desde SQL.

## <a name="create-the-stored-procedure"></a>Crear el procedimiento almacenado

Al llamar a R de T-SQL, utilice el procedimiento almacenado del sistema, [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md). Sin embargo, para los procesos que repiten con frecuencia, como el reciclaje de un modelo, resulta más fácil encapsular la llamada a `sp_execute_exernal_script` en otro procedimiento almacenado.

1.  En primer lugar, cree un procedimiento almacenado que contiene el código de R para generar el modelo de predicción de sugerencia. En [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], abra una nueva **consulta** ventana y ejecute la instrucción siguiente para crear el procedimiento almacenado _TrainTipPredictionModel_. Este procedimiento almacenado define los datos de entrada y usa un paquete de R para crear un modelo de regresión logística.

    ```SQL
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

    - Sin embargo, para asegurarse de que algunos datos se deja para probar el modelo, el 70% de los datos se seleccionan aleatoriamente de la tabla de datos taxi.
    
    - La consulta SELECT usa la función escalar personalizada _fnCalculateDistance_ para calcular la distancia directa entre las ubicaciones de origen y destino.  Los resultados de la consulta se almacenan en la variable de entrada predeterminada de R `InputDataset`.
  
    - Las llamadas de script de R el `rxLogit` función, que es una de las funciones de R mejoradas que se incluye con [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], para crear el modelo de regresión logística.
  
        La variable binaria _tipped_ se usa como la *etiqueta* o columna del resultado y el modelo se ajusta mediante estas columnas específicas:  _passenger_count_, _trip_distance_, _trip_time_in_secs_y _direct_distance_.
  
    -   El modelo entrenado, guardado en la variable de R `logitObj`, se serializa y se coloca en una trama de datos de salida a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Esa salida se inserta en la tabla de base de datos _nyc_taxi_models_, para que la puede usar para predicciones futuras.
  
2.  Ejecute la instrucción para crear el procedimiento almacenado, si aún no existe.

## <a name="generate-the-r-model-using-the-stored-procedure"></a>Generar el modelo de R mediante el procedimiento almacenado

Dado que el procedimiento almacenado ya incluye una definición de los datos de entrada, no es necesario proporcionar una consulta de entrada.

1. Para generar el modelo R, llame al procedimiento almacenado sin ningún otro parámetro:

    ```SQL
    EXEC TrainTipPredictionModel
    ```

2. Inspección del **mensajes** ventana de [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] para los mensajes que se canalizan a de R **stdout** flujo, al igual que este tiene: 

    "STDOUT mensajes desde un script externo: filas leídas: 1193025, de filas totales procesados: 1193025, tiempo Total de fragmentos: 0.093 segundos"

    También puede ver mensajes específicos de cada función, `rxLogit`, mostrar las variables y probar las métricas que se generan como parte de la creación del modelo.

3.  Cuando haya finalizado la instrucción, abra la tabla *nyc_taxi_models*. Procesamiento de los datos y ajuste del modelo pueden tardar un poco.

    Puede ver que se ha agregado una fila nueva, que contiene el modelo serializado en la columna _modelo_.

    ```
    model
    ------
    0x580A00000002000302020....
    ```

En el siguiente paso usará el modelo entrenado para crear predicciones.

## <a name="next-lesson"></a>Lección siguiente

[Lección 6: Poner el modelo](../tutorials/sqldev-operationalize-the-model.md)

## <a name="previous-lesson"></a>Lección anterior

[Lección 4: Crear características de datos mediante T-SQL](..//tutorials/sqldev-create-data-features-using-t-sql.md)

