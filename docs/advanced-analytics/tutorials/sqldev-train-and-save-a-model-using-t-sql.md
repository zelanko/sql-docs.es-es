---
title: Lección 3 entrenar y guardar un modelo mediante R y T-SQL (SQL Server Machine Learning) | Microsoft Docs
description: Tutorial que muestra cómo insertar código de R en SQL Server los procedimientos almacenados y funciones de Transact-SQL
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/07/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 73e1b2ef70821af2247de000eba45a495075e614
ms.sourcegitcommit: 3cd6068f3baf434a4a8074ba67223899e77a690b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/19/2018
ms.locfileid: "49463050"
---
# <a name="lesson-3-train-and-save-a-model-using-t-sql"></a>Lección 3: Entrenar y guardar un modelo con T-SQL
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

En este artículo forma parte de un tutorial para desarrolladores de SQL sobre cómo usar R en SQL Server.

En esta lección, obtendrá información sobre cómo entrenar un modelo de aprendizaje automático mediante el uso de R. Que entrenar el modelo con las características de datos que creó en la lección anterior y, a continuación, guardar el modelo entrenado en un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tabla. En este caso, los paquetes de R ya están instalados con [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], por lo que todo lo que se puede realizar desde SQL.

## <a name="create-the-stored-procedure"></a>Crear el procedimiento almacenado

Al llamar a R desde T-SQL, utilice el procedimiento almacenado del sistema, [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md). Sin embargo, para los procesos que repita con frecuencia, como el reciclaje de un modelo, es más fácil encapsular la llamada a `sp_execute_exernal_script` en otro procedimiento almacenado.

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

    - Sin embargo, para asegurarse de que se dejan algunos datos para probar el modelo, un 70% de los datos se seleccionan aleatoriamente de la tabla de datos de taxi.
    
    - La consulta SELECT usa la función escalar personalizada _fnCalculateDistance_ para calcular la distancia directa entre las ubicaciones de origen y destino.  Los resultados de la consulta se almacenan en la variable de entrada predeterminada de R `InputDataset`.
  
    - El script de R llama el `rxLogit` función, que es una de las funciones mejoradas de R incluida con [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], para crear el modelo de regresión logística.
  
        La variable binaria _tipped_ se usa como la *etiqueta* o columna del resultado y el modelo se ajusta mediante estas columnas específicas:  _passenger_count_, _trip_distance_, _trip_time_in_secs_y _direct_distance_.
  
    -   El modelo entrenado, guardado en la variable de R `logitObj`, se serializa y se coloca en una trama de datos de salida a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Esa salida se inserta en la tabla de base de datos _nyc_taxi_models_, para que la puede usar para predicciones futuras.
  
2.  Ejecute la instrucción para crear el procedimiento almacenado, si aún no existe.

## <a name="generate-the-r-model-using-the-stored-procedure"></a>Generar el modelo de R mediante el procedimiento almacenado

Dado que el procedimiento almacenado ya incluye una definición de los datos de entrada, no es necesario proporcionar una consulta de entrada.

1. Para generar el modelo de R, llame al procedimiento almacenado sin ningún otro parámetro:

    ```SQL
    EXEC TrainTipPredictionModel
    ```

2. Inspección del **mensajes** ventana de [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] para los mensajes que se canalicen al R **stdout** secuencia, como este mensaje: 

    "Los mensajes STDOUT del script externo: filas leídas: 1193025, Total de filas procesadas: 1193025, tiempo Total de fragmentos: 0,093 segundos"

    También es posible que vea mensajes específicos de la función individual, `rxLogit`, mostrar las variables y probar las métricas que se generan como parte de la creación del modelo.

3.  Cuando haya finalizado la instrucción, abra la tabla *nyc_taxi_models*. Procesamiento de los datos y ajuste del modelo pueden tardar un rato.

    Puede ver que se ha agregado una fila nueva, que contiene el modelo serializado en la columna _modelo_.

    ```
    model
    ------
    0x580A00000002000302020....
    ```

En el siguiente paso usará el modelo entrenado para crear predicciones.

## <a name="next-lesson"></a>Lección siguiente

[Lección 4: Hacer operativo el modelo](../tutorials/sqldev-operationalize-the-model.md)

## <a name="previous-lesson"></a>Lección anterior

[Lección 2: Crear características de datos mediante las funciones de R y T-SQL](..//tutorials/sqldev-create-data-features-using-t-sql.md)

