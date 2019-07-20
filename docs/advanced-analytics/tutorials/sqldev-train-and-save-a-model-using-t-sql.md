---
title: Lección 3 entrenar y guardar un modelo mediante R y T-SQL
description: Tutorial que muestra cómo entrenar, serializar y guardar un modelo de R mediante SQL Server procedimientos almacenados y funciones de T-SQL.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/16/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.openlocfilehash: 0d26f549bcca4860f4febe01a868f360edfa4fa2
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/19/2019
ms.locfileid: "68345861"
---
# <a name="lesson-3-train-and-save-a-model-using-t-sql"></a>Lección 3: Entrenar y guardar un modelo mediante T-SQL
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Este artículo forma parte de un tutorial para desarrolladores de SQL sobre cómo usar R en SQL Server.

En esta lección, aprenderá a entrenar un modelo de aprendizaje automático mediante R. Deberá entrenar el modelo con las características de datos que creó en la lección anterior y, a continuación, guardar el modelo entrenado [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en una tabla. En este caso, los paquetes de R ya están instalados [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]con, por lo que todo puede realizarse desde SQL.

## <a name="create-the-stored-procedure"></a>Crear el procedimiento almacenado

Al llamar a R desde T-SQL, se usa el procedimiento almacenado del sistema [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md). Sin embargo, para los procesos que se repiten con frecuencia, como volver a entrenar un modelo, es más fácil encapsular la llamada a sp_execute_exernal_script en otro procedimiento almacenado.

1. En [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], abra una nueva ventana de **consulta** .

2. Ejecute la instrucción siguiente para crear el procedimiento almacenado **RxTrainLogitModel**. Este procedimiento almacenado define los datos de entrada y usa **rxLogit** de RevoScaleR para crear un modelo de regresión logística.

    ```sql
    CREATE PROCEDURE [dbo].[RxTrainLogitModel] (@trained_model varbinary(max) OUTPUT)
    
    AS
    BEGIN
      DECLARE @inquery nvarchar(max) = N'
        select tipped, fare_amount, passenger_count,trip_time_in_secs,trip_distance,
        pickup_datetime, dropoff_datetime,
        dbo.fnCalculateDistance(pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) as direct_distance
        from nyctaxi_sample
        tablesample (70 percent) repeatable (98052)
    '
    
      EXEC sp_execute_external_script @language = N'R',
                                      @script = N'
    ## Create model
    logitObj <- rxLogit(tipped ~ passenger_count + trip_distance + trip_time_in_secs + direct_distance, data = InputDataSet)
    summary(logitObj)
    
    ## Serialize model 
    trained_model <- as.raw(serialize(logitObj, NULL));
    ',
      @input_data_1 = @inquery,
      @params = N'@trained_model varbinary(max) OUTPUT',
      @trained_model = @trained_model OUTPUT; 
    END
    GO
    ```

    - Para asegurarse de que se dejan algunos datos para probar el modelo, el 70% de los datos se seleccionan aleatoriamente en la tabla de datos de taxi para fines de entrenamiento.

    - La consulta SELECT usa la función escalar personalizada *fnCalculateDistance* para calcular la distancia directa entre las ubicaciones de origen y destino. Los resultados de la consulta se almacenan en la variable de entrada de `InputDataset`R predeterminada,.
  
    - El script de r llama a la función **rxLogit** , que es una de las funciones mejoradas [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]de r que se incluyen con, para crear el modelo de regresión logística.
  
        La variable binaria _tipped_ se usa como la *etiqueta* o columna del resultado y el modelo se ajusta mediante estas columnas específicas:  _passenger_count_, _trip_distance_, _trip_time_in_secs_y _direct_distance_.
  
    - El modelo entrenado, guardado en la variable `logitObj`de R, se serializa y se devuelve como parámetro de salida.

## <a name="train-and-deploy-the-r-model-using-the-stored-procedure"></a>Entrenar e implementar el modelo de R mediante el procedimiento almacenado

Dado que el procedimiento almacenado ya incluye una definición de los datos de entrada, no es necesario proporcionar una consulta de entrada.

1. Para entrenar e implementar el modelo de R, llame al procedimiento almacenado e insértelo en la tabla de base de datos _nyc_taxi_models_, de modo que pueda usarlo para predicciones futuras:

    ```sql
    DECLARE @model VARBINARY(MAX);
    EXEC RxTrainLogitModel @model OUTPUT;
    INSERT INTO nyc_taxi_models (name, model) VALUES('RxTrainLogit_model', @model);
    ```

2. Vea la ventana **mensajes** de [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] para ver los mensajes que se canalizarán al flujo **stdout** de R, como este mensaje: 

    "Mensaje (s) STDOUT del script externo: Filas leídas: 1193025, total de filas procesadas: 1193025, tiempo total de fragmentos: 0,093 segundos "

    También puede ver mensajes específicos de la función individual, `rxLogit`y mostrar las variables y las métricas de prueba generadas como parte de la creación del modelo.

3.  Cuando la instrucción se haya completado, abra la tabla *nyc_taxi_models*. El procesamiento de los datos y la conexión del modelo puede tardar unos minutos.

    Puede ver que se ha agregado una nueva fila, que contiene el modelo serializado en el _modelo_ de columna y el nombre de modelo **RxTrainLogit_model** en el _nombre_de columna.

    ```sql
    model                        name
    ---------------------------- ------------------
    0x580A00000002000302020....  RxTrainLogit_model
    ```

En el paso siguiente, usará el modelo entrenado para generar predicciones.

## <a name="next-lesson"></a>Lección siguiente

[Lección 4: Predecir los resultados potenciales mediante un modelo de R en un procedimiento almacenado](../tutorials/sqldev-operationalize-the-model.md)

## <a name="previous-lesson"></a>Lección anterior

[Lección 2: Crear características de datos mediante las funciones de R y T-SQL](..//tutorials/sqldev-create-data-features-using-t-sql.md)

