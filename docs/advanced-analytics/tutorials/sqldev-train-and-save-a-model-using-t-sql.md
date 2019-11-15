---
title: 'Tutorial de R y T-SQL: Entrenamiento del modelo'
description: En este tutorial se explica cómo entrenar, serializar y guardar un modelo de R mediante funciones de T-SQL y procedimientos almacenados en SQL.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/16/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 406f8e1c60c5820f9edaaf7760b7aeed321d2611
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/07/2019
ms.locfileid: "73724457"
---
# <a name="lesson-3-train-and-save-a-model-using-t-sql"></a>Lección 3: Entrenar y guardar un modelo con T-SQL
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Este artículo forma parte de un tutorial para desarrolladores de SQL sobre cómo usar R en SQL Server.

En esta lección, aprenderá a entrenar un modelo de aprendizaje automático mediante R. Deberá entrenar el modelo con las características de datos que creó en la lección anterior y después guardar el modelo entrenado en una tabla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. En este caso, los paquetes de R ya se han instalado con [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], por lo que todo se puede hacer desde SQL.

## <a name="create-the-stored-procedure"></a>Creación del procedimiento almacenado

Al llamar a R desde T-SQL, utilice el procedimiento almacenado del sistema [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md). Sin embargo, para procesos que repite a menudo, como volver a entrenar un modelo, es más fácil encapsular la llamada a sp_execute_exernal_script en otro procedimiento almacenado.

1. En [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], abra una nueva ventana de **consulta**.

2. Ejecute la siguiente instrucción para crear el procedimiento almacenado **RxTrainLogitModel**. Este procedimiento almacenado define los datos de entrada y usa **rxLogit** de RevoScaleR para crear un modelo de regresión logística.

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

    - Para asegurarse de que se dejan algunos datos para probar el modelo, el 70 % de los datos se seleccionan aleatoriamente de la tabla de datos de taxi con fines de entrenamiento.

    - La consulta SELECT usa la función escalar personalizada *fnCalculateDistance* para calcular la distancia directa entre las ubicaciones de origen y destino. Los resultados de la consulta se almacenan en la variable de entrada predeterminada de R `InputDataset`.
  
    - El script de R llama a la función **rxLogit**, que es una de las funciones mejoradas de R incluida con [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], para crear el modelo de regresión logística.
  
        La variable binaria _tipped_ se usa como la *etiqueta* o columna del resultado y el modelo se ajusta mediante estas columnas específicas:  _passenger_count_, _trip_distance_, _trip_time_in_secs_y _direct_distance_.
  
    - El modelo entrenado, guardado en la variable de R `logitObj`, se serializa y se devuelve como un parámetro de salida.

## <a name="train-and-deploy-the-r-model-using-the-stored-procedure"></a>Entreno e implementación del modelo de R usando el procedimiento almacenado

Como el procedimiento almacenado ya incluye una definición de los datos de entrada, no es necesario proporcionar una consulta de entrada.

1. Para entrenar e implementar el modelo de R, llame al procedimiento almacenado e insértelo en la tabla de base de datos _nyc_taxi_models_ para poder usarlo en predicciones futuras:

    ```sql
    DECLARE @model VARBINARY(MAX);
    EXEC RxTrainLogitModel @model OUTPUT;
    INSERT INTO nyc_taxi_models (name, model) VALUES('RxTrainLogit_model', @model);
    ```

2. Vea en la ventana **Mensajes** de [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] los mensajes que se canalizan al flujo **stdout** de R: 

    Mensaje(s) STDOUT del script externo: Filas leídas: 1193025, Total de filas procesadas: 1193025, Tiempo total de fragmentos: 0,093 segundos

    Es posible que también vea mensajes específicos de la función individual, `rxLogit`, que muestran las variables y métricas de pruebas generadas como parte de la creación del modelo.

3.  Una vez completada la instrucción, abra la tabla *nyc_taxi_models*. Es posible que el procesamiento de los datos y el ajuste del modelo tarden un rato.

    Puede ver que se ha agregado una fila nueva, que contiene el modelo serializado en la columna _model_ y el nombre del modelo **RxTrainLogit_model** en la columna _name_.

    ```sql
    model                        name
    ---------------------------- ------------------
    0x580A00000002000302020....  RxTrainLogit_model
    ```

En el siguiente paso usará el modelo entrenado para generar predicciones.

## <a name="next-lesson"></a>Lección siguiente

[Lección 4: Predecir posibles resultados mediante un modelo de R en un procedimiento almacenado](../tutorials/sqldev-operationalize-the-model.md)

## <a name="previous-lesson"></a>Lección anterior

[Lección 2: Crear características de datos con R y funciones de T-SQL](..//tutorials/sqldev-create-data-features-using-t-sql.md)

