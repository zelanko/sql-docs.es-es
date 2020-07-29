---
title: 'Python + T-SQL: Entrenamiento de un modelo'
description: Tutorial de Python que muestra cómo entrenar y guardar un modelo con Transact-SQL en SQL Server.
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 11/01/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 8d7bc2e2d46cb5b3f0c9619e59ab448e95bf4db2
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85775337"
---
# <a name="train-and-save-a-python-model-using-t-sql"></a>Entrenar y guardar un modelo de Python mediante T-SQL
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

Este artículo forma parte de un tutorial, [Análisis de datos de Python en base de datos para desarrolladores de SQL](sqldev-in-database-python-for-sql-developers.md). 

En este paso, aprenderá a entrenar un modelo de aprendizaje automático mediante los paquetes de Python **scikit-Learn** y **revoscalepy**. Estas bibliotecas de Python ya están instaladas con SQL Server Machine Learning Services.

Cargue los módulos y llame a las funciones necesarias para crear y entrenar el modelo mediante un procedimiento almacenado de SQL Server. El modelo necesita las características de datos que ha diseñado en lecciones anteriores. Por último, guarde el modelo entrenado en una tabla [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].
 

## <a name="split-the-sample-data-into-training-and-testing-sets"></a>Dividir los datos de muestra en conjuntos de entrenamiento y de prueba

1. Cree un procedimiento almacenado denominado **PyTrainTestSplit** para dividir los datos de la tabla nyctaxi_sample en dos partes: nyctaxi_sample_training y nyctaxi_sample_testing. 

    Aunque este procedimiento almacenado ya debería estar creado, puede ejecutar este código para crearlo:

    ```sql
    DROP PROCEDURE IF EXISTS PyTrainTestSplit;
    GO

    CREATE PROCEDURE [dbo].[PyTrainTestSplit] (@pct int)
    AS
    
    DROP TABLE IF EXISTS dbo.nyctaxi_sample_training
    SELECT * into nyctaxi_sample_training FROM nyctaxi_sample WHERE (ABS(CAST(BINARY_CHECKSUM(medallion,hack_license)  as int)) % 100) < @pct
    
    DROP TABLE IF EXISTS dbo.nyctaxi_sample_testing
    SELECT * into nyctaxi_sample_testing FROM nyctaxi_sample
    WHERE (ABS(CAST(BINARY_CHECKSUM(medallion,hack_license)  as int)) % 100) > @pct
    GO
    ```

2. Para dividir los datos mediante una división personalizada, ejecute el procedimiento almacenado y escriba un entero que represente el porcentaje de datos asignados al conjunto de entrenamiento. Por ejemplo, la siguiente instrucción asignaría el 60 % de los datos al conjunto de entrenamiento.

    ```sql
    EXEC PyTrainTestSplit 60
    GO
    ```

## <a name="build-a-logistic-regression-model"></a>Crear un modelo de regresión logística

Una vez preparados los datos, ya puede usarlos para entrenar un modelo. Para ello, llame a un procedimiento almacenado que ejecute código de Python, tomando como entrada la tabla de datos de entrenamiento. En este tutorial, creará dos modelos, ambos modelos de clasificación binaria:

+ El procedimiento almacenado **PyTrainScikit** crea un modelo de predicción de propinas mediante el paquete **scikit-learn**.
+ El procedimiento almacenado **TrainTipPredictionModelRxPy** crea un modelo de predicción de propinas mediante el paquete **revoscalepy**.

Cada procedimiento almacenado usa los datos de entrada proporcionados para crear y entrenar un modelo de regresión logística. Todo el código de Python se ajusta en el procedimiento almacenado del sistema, [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md).

Para que sea más fácil volver a entrenar el modelo según los nuevos datos, ajuste la llamada a sp_execute_external_script en otro procedimiento almacenado y pase los nuevos datos de entrenamiento como un parámetro. Esta sección le guiará a través de ese proceso.

### <a name="pytrainscikit"></a>PyTrainScikit

1.  En [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], abra una nueva ventana **Consulta** y ejecute esta instrucción siguiente para crear el procedimiento almacenado **PyTrainScikit**.  El procedimiento almacenado contiene una definición de los datos de entrada, por lo que no es necesario proporcionar una consulta de entrada.

    ```sql
    DROP PROCEDURE IF EXISTS PyTrainScikit;
    GO

    CREATE PROCEDURE [dbo].[PyTrainScikit] (@trained_model varbinary(max) OUTPUT)
    AS
    BEGIN
    EXEC sp_execute_external_script
      @language = N'Python',
      @script = N'
    import numpy
    import pickle
    from sklearn.linear_model import LogisticRegression
    
    ##Create SciKit-Learn logistic regression model
    X = InputDataSet[["passenger_count", "trip_distance", "trip_time_in_secs", "direct_distance"]]
    y = numpy.ravel(InputDataSet[["tipped"]])
    
    SKLalgo = LogisticRegression()
    logitObj = SKLalgo.fit(X, y)
    
    ##Serialize model
    trained_model = pickle.dumps(logitObj)
    ',
    @input_data_1 = N'
    select tipped, fare_amount, passenger_count, trip_time_in_secs, trip_distance, 
    dbo.fnCalculateDistance(pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) as direct_distance
    from nyctaxi_sample_training
    ',
    @input_data_1_name = N'InputDataSet',
    @params = N'@trained_model varbinary(max) OUTPUT',
    @trained_model = @trained_model OUTPUT;
    ;
    END;
    GO
    ```

2. Ejecute estas instrucciones SQL para insertar el modelo entrenado en la tabla nyc\_taxi_models.

    ```sql
    DECLARE @model VARBINARY(MAX);
    EXEC PyTrainScikit @model OUTPUT;
    INSERT INTO nyc_taxi_models (name, model) VALUES('SciKit_model', @model);
    ```

    Es posible que el procesamiento de los datos y el ajuste del modelo tarde unos minutos. Los mensajes que se canalicen al flujo **stdout** de Python se muestran en la ventana **Mensajes** de [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]. Por ejemplo:

    *Mensajes STDOUT del script externo:* 
  *C:\Archivos de programa\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\lib\site-packages\revoscalepy*

3. Abra la tabla *nyc\_taxi_models*. Puede ver que se ha agregado una fila nueva, que contiene el modelo serializado en la columna _modelo_.

    *SciKit_model* *0x800363736B6C6561726E2E6C696E6561....*

### <a name="traintippredictionmodelrxpy"></a>TrainTipPredictionModelRxPy

Este procedimiento almacenado usa el nuevo paquete **revoscalepy**, que es un nuevo paquete de Python. Contiene objetos, transformaciones y algoritmos similares a los proporcionados para el paquete **RevoScaleR** del lenguaje R. 

Al usar **revoscalepy**, puede crear contextos de proceso remotos, trasladar datos entre contextos de proceso, transformar datos y entrenar modelos predictivos mediante algoritmos populares, como regresión logística y lineal, árboles de decisión, etc. Para más información, vea [Módulo revoscalepy en SQL Server](../python/ref-py-revoscalepy.md) y [Referencia de funciones de revoscalepy](https://docs.microsoft.com/r-server/python-reference/revoscalepy/revoscalepy-package).

1. En [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], abra una nueva ventana **Consulta** y ejecute esta instrucción para crear el procedimiento almacenado _TrainTipPredictionModelRxPy_.  Como el procedimiento almacenado ya incluye una definición de los datos de entrada, no es necesario proporcionar una consulta de entrada.

    ```sql
    DROP PROCEDURE IF EXISTS TrainTipPredictionModelRxPy;
    GO

    CREATE PROCEDURE [dbo].[TrainTipPredictionModelRxPy] (@trained_model varbinary(max) OUTPUT)
    AS
    BEGIN
    EXEC sp_execute_external_script 
      @language = N'Python',
      @script = N'
    import numpy
    import pickle
    from revoscalepy.functions.RxLogit import rx_logit
    
    ## Create a logistic regression model using rx_logit function from revoscalepy package
    logitObj = rx_logit("tipped ~ passenger_count + trip_distance + trip_time_in_secs + direct_distance", data = InputDataSet);
    
    ## Serialize model
    trained_model = pickle.dumps(logitObj)
    ',
    @input_data_1 = N'
    select tipped, fare_amount, passenger_count, trip_time_in_secs, trip_distance, 
    dbo.fnCalculateDistance(pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) as direct_distance
    from nyctaxi_sample_training
    ',
    @input_data_1_name = N'InputDataSet',
    @params = N'@trained_model varbinary(max) OUTPUT',
    @trained_model = @trained_model OUTPUT;
    ;
    END;
    GO
    ```

    Este procedimiento almacenado realiza estos pasos como parte del entrenamiento del modelo:

    - La consulta SELECT aplica la función escalar personalizada _fnCalculateDistance_ para calcular la distancia directa entre las ubicaciones de origen y de destino. Los resultados de la consulta se almacenan en la variable de entrada predeterminada de Python, `InputDataset`.
    - La variable binaria _tipped_ se usa como la *etiqueta* o la columna de resultados y el modelo se ajusta mediante estas columnas específicas: _passenger_count_, _trip_distance_, _trip_time_in_secs_ y _direct_distance_.
    - El modelo entrenado se serializa y se almacena en la variable de Python `logitObj`. Al agregar la palabra clave OUTPUT de T-SQL, puede agregar la variable como un resultado del procedimiento almacenado. En el paso siguiente, esa variable se usa para insertar el código binario del modelo en una tabla de base de datos _nyc_taxi_models_. Este mecanismo facilita el almacenamiento y la reutilización de modelos.

2. Ejecute el procedimiento almacenado como se indica aquí para insertar el modelo entrenado **revoscalepy** en la tabla *nyc_taxi_models*.

    ```sql
    DECLARE @model VARBINARY(MAX);
    EXEC TrainTipPredictionModelRxPy @model OUTPUT;
    INSERT INTO nyc_taxi_models (name, model) VALUES('revoscalepy_model', @model);
    ```

    Es posible que el procesamiento de los datos y el ajuste del modelo tarden un rato. Los mensajes que se canalicen al flujo **stdout** de Python se muestran en la ventana **Mensajes** de [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]. Por ejemplo:

    *Mensajes STDOUT del script externo:* 
  *C:\Archivos de programa\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\lib\site-packages\revoscalepy*

3. Abra la tabla *nyc_taxi_models*. Puede ver que se ha agregado una fila nueva, que contiene el modelo serializado en la columna _modelo_.

    *revoscalepy_model* *0x8003637265766F7363616c....*

En el siguiente paso, se usará el modelo entrenado para crear predicciones.

## <a name="next-step"></a>Paso siguiente

[Ejecución de predicciones con Python insertado en un procedimiento almacenado](sqldev-py6-operationalize-the-model.md)

## <a name="previous-step"></a>Paso anterior

[Crear características de datos mediante T-SQL](sqldev-py5-train-and-save-a-model-using-t-sql.md)
