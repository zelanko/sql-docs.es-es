---
title: Entrenar y guardar un modelo de Python mediante T-SQL
description: Tutorial de Python que muestra cómo entrenar y guardar un modelo con Transact-SQL en SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/01/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 470d7be0e1777d029f406e183aad644359c82f13
ms.sourcegitcommit: 454270de64347db917ebe41c081128bd17194d73
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/07/2019
ms.locfileid: "72005996"
---
# <a name="train-and-save-a-python-model-using-t-sql"></a>Entrenar y guardar un modelo de Python mediante T-SQL
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Este artículo forma parte de un tutorial, [análisis de Python en base de datos para desarrolladores de SQL](sqldev-in-database-python-for-sql-developers.md). 

En este paso, aprenderá a entrenar un modelo de aprendizaje automático mediante los paquetes **de Python scikit-Learn** y **revoscalepy**. Estas bibliotecas de Python ya están instaladas con SQL Server Machine Learning Services.

Los módulos se cargan y se llama a las funciones necesarias para crear y entrenar el modelo mediante un SQL Server procedimiento almacenado. El modelo requiere las características de datos que ha diseñado en lecciones anteriores. Por último, guarde el modelo entrenado en una tabla [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].
 

## <a name="split-the-sample-data-into-training-and-testing-sets"></a>Divida los datos de ejemplo en conjuntos de entrenamiento y de prueba

1. Cree un procedimiento almacenado denominado **PyTrainTestSplit** para dividir los datos de la tabla nyctaxi_sample en dos partes: nyctaxi_sample_training y nyctaxi_sample_testing. 

    Este procedimiento almacenado ya debe estar creado, pero puede ejecutar el código siguiente para crearlo:

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

2. Para dividir los datos mediante una división personalizada, ejecute el procedimiento almacenado y escriba un entero que represente el porcentaje de datos asignados al conjunto de entrenamiento. Por ejemplo, la siguiente instrucción asignaría el 60% de los datos al conjunto de entrenamiento.

    ```sql
    EXEC PyTrainTestSplit 60
    GO
    ```

## <a name="build-a-logistic-regression-model"></a>Crear un modelo de regresión logística

Una vez preparados los datos, puede usarlos para entrenar un modelo. Para ello, se llama a un procedimiento almacenado que ejecuta código de Python y se toma como entrada la tabla de datos de entrenamiento. En este tutorial, creará dos modelos, ambos modelos de clasificación binaria:

+ El procedimiento almacenado **PyTrainScikit** crea un modelo de predicción de propina mediante el paquete **scikit-Learn** .
+ El procedimiento almacenado **TrainTipPredictionModelRxPy** crea un modelo de predicción de propinas mediante el paquete **revoscalepy** .

Cada procedimiento almacenado utiliza los datos de entrada proporcionados para crear y entrenar un modelo de regresión logística. Todo el código de Python se ajusta en el procedimiento almacenado del sistema, [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md).

Para que sea más fácil volver a entrenar el modelo en los nuevos datos, se ajusta la llamada a sp_execute_external_script en otro procedimiento almacenado y se pasan los nuevos datos de entrenamiento como un parámetro. Esta sección le guiará a través de ese proceso.

### <a name="pytrainscikit"></a>PyTrainScikit

1.  En [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], abra una nueva ventana de **consulta** y ejecute la instrucción siguiente para crear el procedimiento almacenado **PyTrainScikit**.  El procedimiento almacenado contiene una definición de los datos de entrada, por lo que no es necesario proporcionar una consulta de entrada.

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

2. Ejecute las siguientes instrucciones SQL para insertar el modelo entrenado en la tabla Nueva York @ no__t-0taxi_models.

    ```sql
    DECLARE @model VARBINARY(MAX);
    EXEC PyTrainScikit @model OUTPUT;
    INSERT INTO nyc_taxi_models (name, model) VALUES('SciKit_model', @model);
    ```

    El procesamiento de los datos y la conexión del modelo puede tardar un par de minutos. Los mensajes que se canalizarán al flujo **stdout** de Python se muestran en la ventana **mensajes** de [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]. Por ejemplo:

    *Mensaje (s) stdout del script externo:* 
  *C:\Archivos de programa\Microsoft SQL Server\MSSQL14. MSSQLSERVER\PYTHON_SERVICES\lib\site-packages\revoscalepy*

3. Abra la tabla *Nueva York @ no__t-1taxi_models*. Puede ver que se ha agregado una fila nueva, que contiene el modelo serializado en la columna _modelo_.

    *SciKit_model* *0x800363736B6C6561726E2E6C696E6561....*

### <a name="traintippredictionmodelrxpy"></a>TrainTipPredictionModelRxPy

Este procedimiento almacenado usa el nuevo paquete **revoscalepy** , que es un nuevo paquete de Python. Contiene objetos, transformaciones y algoritmos similares a los proporcionados para el paquete **RevoScaleR** del lenguaje R. 

Mediante el uso de **revoscalepy**, puede crear contextos de cálculo remotos, trasladar datos entre contextos de cálculo, transformar datos y entrenar modelos predictivos con algoritmos populares, como regresión logística y lineal, árboles de decisión, etc. Para obtener más información, vea [módulo revoscalepy en](../python/ref-py-revoscalepy.md) la [referencia de funciones](https://docs.microsoft.com/r-server/python-reference/revoscalepy/revoscalepy-package)de SQL Server y revoscalepy.

1. En [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], abra una nueva ventana de **consulta** y ejecute la instrucción siguiente para crear el procedimiento almacenado _TrainTipPredictionModelRxPy_.  Dado que el procedimiento almacenado ya incluye una definición de los datos de entrada, no es necesario proporcionar una consulta de entrada.

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

    Este procedimiento almacenado realiza los pasos siguientes como parte del entrenamiento del modelo:

    - La consulta SELECT aplica la función escalar personalizada _fnCalculateDistance_ para calcular la distancia directa entre las ubicaciones de recogida y desactivación. Los resultados de la consulta se almacenan en la variable de entrada predeterminada de Python, `InputDataset`.
    - La _variable_ binaria *enmarcada* se usa como la etiqueta o la columna de resultados, y el modelo se ajusta mediante estas columnas de características: _passenger_count_, _trip_distance_, _trip_time_in_secs_y _direct_distance_.
    - El modelo entrenado se serializa y se almacena en la variable de Python `logitObj`. Al agregar la salida de la palabra clave de T-SQL, puede Agregar la variable como salida del procedimiento almacenado. En el paso siguiente, esa variable se utiliza para insertar el código binario del modelo en una tabla de base de datos _nyc_taxi_models_. Este mecanismo facilita el almacenamiento y la reutilización de modelos.

2. Ejecute el procedimiento almacenado como se indica a continuación para insertar el modelo de **revoscalepy** entrenado en la tabla *nyc_taxi_models*.

    ```sql
    DECLARE @model VARBINARY(MAX);
    EXEC TrainTipPredictionModelRxPy @model OUTPUT;
    INSERT INTO nyc_taxi_models (name, model) VALUES('revoscalepy_model', @model);
    ```

    El procesamiento de los datos y la conexión del modelo puede tardar unos minutos. Los mensajes que se canalizarán al flujo **stdout** de Python se muestran en la ventana **mensajes** de [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]. Por ejemplo:

    *Mensaje (s) stdout del script externo:* 
  *C:\Archivos de programa\Microsoft SQL Server\MSSQL14. MSSQLSERVER\PYTHON_SERVICES\lib\site-packages\revoscalepy*

3. Abra la tabla *nyc_taxi_models*. Puede ver que se ha agregado una fila nueva, que contiene el modelo serializado en la columna _modelo_.

    *revoscalepy_model* *0x8003637265766F7363616c....*

En el paso siguiente, se usan los modelos entrenados para crear predicciones.

## <a name="next-step"></a>Paso siguiente

[Ejecutar predicciones con Python incrustado en un procedimiento almacenado](sqldev-py6-operationalize-the-model.md)

## <a name="previous-step"></a>Paso anterior

[Crear características de datos mediante T-SQL](sqldev-py5-train-and-save-a-model-using-t-sql.md)
