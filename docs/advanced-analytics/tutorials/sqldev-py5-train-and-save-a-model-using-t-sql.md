---
title: 'Entrenar y guardar un modelo de Python con T-SQL: SQL Server Machine Learning'
description: Tutorial de Python que muestra cómo entrenar y guardar un modelo con Transact-SQL en SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/01/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 2e0505cf847a091a5650b392aab56f486cee16aa
ms.sourcegitcommit: 2827d19393c8060eafac18db3155a9bd230df423
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/27/2019
ms.locfileid: "58511252"
---
# <a name="train-and-save-a-python-model-using-t-sql"></a>Entrenar y guardar un modelo de Python mediante T-SQL
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Este artículo forma parte de un tutorial, [análisis de Python en bases de datos para desarrolladores de SQL](sqldev-in-database-python-for-sql-developers.md). 

En este paso, aprenderá a entrenar un modelo de aprendizaje automático con los paquetes de Python **scikit-aprender** y **revoscalepy**. Estas bibliotecas de Python ya están instaladas con SQL Server Machine Learning Services.

Cargar los módulos y llamar a las funciones necesarias para crear y entrenar el modelo con un procedimiento almacenado de SQL Server. El modelo requiere las características de datos que ha diseñado en las lecciones anteriores. Por último, guarda el modelo entrenado para un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tabla.
 

## <a name="split-the-sample-data-into-training-and-testing-sets"></a>Dividir los datos de ejemplo en entrenamiento y conjuntos de pruebas

1. Crear un procedimiento almacenado llamado **PyTrainTestSplit** para dividir los datos en la tabla nyctaxi_sample en dos partes: nyctaxi_sample_training y nyctaxi_sample_testing. 

    Este procedimiento almacenado debe ser creado por usted, pero puede ejecutar el siguiente código para crearla:

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

2. Para dividir los datos utilizando una división personalizada, ejecute el procedimiento almacenado y escriba un entero que representa el porcentaje de los datos asignados al conjunto de entrenamiento. Por ejemplo, la siguiente instrucción asignaría un 60% de los datos para el conjunto de entrenamiento.

    ```sql
    EXEC PyTrainTestSplit 60
    GO
    ```

## <a name="build-a-logistic-regression-model"></a>Crear un modelo de regresión logística

Una vez preparados los datos, puede usarlo para entrenar un modelo. Para ello, una llamada a un almacenado procedimiento que se ejecuta código Python, toma como entrada en la tabla de datos de entrenamiento. Para este tutorial, creará dos modelos, ambos modelos de clasificación binaria:

+ El procedimiento almacenado **PyTrainScikit** crea un modelo de predicción de tip mediante el **scikit-aprender** paquete.
+ El procedimiento almacenado **TrainTipPredictionModelRxPy** crea un modelo de predicción de tip mediante el **revoscalepy** paquete.

Cada procedimiento almacenado usa los datos de entrada que proporcione para crear y entrenar un modelo de regresión logística. Todo el código Python se ajusta en el procedimiento almacenado del sistema, [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md).

Para que sea más fácil volver a entrenar el modelo con nuevos datos, ajuste la llamada a sp_execute_exernal_script en otro procedimiento almacenado y pasar de los nuevos datos de entrenamiento como un parámetro. En esta sección le guiará a través de ese proceso.

### <a name="pytrainscikit"></a>PyTrainScikit

1.  En [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], abra una nueva **consulta** ventana y ejecute la instrucción siguiente para crear el procedimiento almacenado **PyTrainScikit**.  El procedimiento almacenado contiene una definición de los datos de entrada, por lo que no es necesario proporcionar una consulta de entrada.

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

2. Ejecute la siguiente tabla de instrucciones SQL para insertar el modelo entrenado en Nueva York\_taxi_models.

    ```sql
    DECLARE @model VARBINARY(MAX);
    EXEC PyTrainScikit @model OUTPUT;
    INSERT INTO nyc_taxi_models (name, model) VALUES('SciKit_model', @model);
    ```

    Procesamiento de los datos y ajuste del modelo pueden tardar un par de minutos. Los mensajes que se canalicen de Python **stdout** secuencia se muestran en el **mensajes** ventana de [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]. Por ejemplo:

    *Mensajes STDOUT del script externo:*
  *C:\Program Files\Microsoft SQL Server\MSSQL14. MSSQLSERVER\PYTHON_SERVICES\lib\site packages\revoscalepy*

3. Abra la tabla *nyc\_taxi_models*. Puede ver que se ha agregado una fila nueva, que contiene el modelo serializado en la columna _modelo_.

    *SciKit_model* *0x800363736B6C6561726E2E6C696E6561....*

### <a name="traintippredictionmodelrxpy"></a>TrainTipPredictionModelRxPy

Este procedimiento almacenado usa el nuevo **revoscalepy** paquete, que es un nuevo paquete de Python. Contiene objetos, transformación y algoritmos similares a los proporcionados para el lenguaje R **RevoScaleR** paquete. 

Mediante el uso de **revoscalepy**, puede crear contextos de cálculo remoto, el proceso de mover datos entre contextos, transformar datos y entrenar modelos predictivos con algoritmos populares, como la regresión logística y lineal, árboles de decisión, y más. Para obtener más información, consulte [módulo revoscalepy en SQL Server](../python/ref-py-revoscalepy.md) y [referencia de funciones de revoscalepy](https://docs.microsoft.com/r-server/python-reference/revoscalepy/revoscalepy-package).

1. En [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], abra una nueva **consulta** ventana y ejecute la instrucción siguiente para crear el procedimiento almacenado _TrainTipPredictionModelRxPy_.  Dado que el procedimiento almacenado ya incluye una definición de los datos de entrada, no es necesario proporcionar una consulta de entrada.

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

    Este procedimiento almacenado realiza los pasos siguientes como parte de entrenamiento del modelo:

    - La consulta SELECT que aplica la función escalar personalizada _fnCalculateDistance_ para calcular la distancia directa entre las ubicaciones de origen y destino. Los resultados de la consulta se almacenan en la variable de entrada de Python de forma predeterminada, `InputDataset`.
    - La variable binaria _tipped_ se utiliza como el *etiqueta* o columna del resultado y el modelo se ajusta mediante estas columnas de característica: _passenger_count_, _trip_ distancia_, _trip_time_in_secs_, y _direct_distance_.
    - El modelo entrenado se serializa y se almacena en la variable de Python `logitObj`. Agregando la palabra clave de Transact-SQL salida, puede agregar la variable como una salida del procedimiento almacenado. En el paso siguiente, se utiliza esa variable para insertar el código binario del modelo en una tabla de base de datos _nyc_taxi_models_. Este mecanismo hace que resulte fácil almacenar y volver a usar los modelos.

2. Ejecute el procedimiento almacenado como se indica a continuación para insertar el entrenado **revoscalepy** modelos en la tabla *nyc_taxi_models*.

    ```sql
    DECLARE @model VARBINARY(MAX);
    EXEC TrainTipPredictionModelRxPy @model OUTPUT;
    INSERT INTO nyc_taxi_models (name, model) VALUES('revoscalepy_model', @model);
    ```

    Procesamiento de los datos y ajuste del modelo pueden tardar un rato. Los mensajes que se canalicen de Python **stdout** secuencia se muestran en el **mensajes** ventana de [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]. Por ejemplo:

    *Mensajes STDOUT del script externo:*
  *C:\Program Files\Microsoft SQL Server\MSSQL14. MSSQLSERVER\PYTHON_SERVICES\lib\site packages\revoscalepy*

3. Abra la tabla *nyc_taxi_models*. Puede ver que se ha agregado una fila nueva, que contiene el modelo serializado en la columna _modelo_.

    *revoscalepy_model* *0x8003637265766F7363616c....*

En el paso siguiente, usará los modelos entrenados para crear predicciones.

## <a name="next-step"></a>Paso siguiente

[Ejecutar predicciones con Python incrustado en un procedimiento almacenado](sqldev-py6-operationalize-the-model.md)

## <a name="previous-step"></a>Paso anterior

[Crear características de datos mediante T-SQL](sqldev-py5-train-and-save-a-model-using-t-sql.md)
