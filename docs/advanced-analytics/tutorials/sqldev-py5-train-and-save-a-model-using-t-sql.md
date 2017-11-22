---
title: 'Paso 5: Entrenar y guardar un modelo de Python mediante T-SQL | Documentos de Microsoft'
ms.custom: 
ms.date: 10/17/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology: python-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to: SQL Server 2017
dev_langs:
- Python
- TSQL
ms.assetid: 
caps.latest.revision: "2"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.openlocfilehash: 11fa031229d8bc08a9091c3fa6f85e81468d7379
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2017
---
# <a name="step-5-train-and-save-a-python-model-using-t-sql"></a>Paso 5: Entrenar y guardar un modelo de Python mediante T-SQL

Este artículo forma parte de un tutorial, [análisis de Python en bases de datos para desarrolladores de SQL](sqldev-in-database-python-for-sql-developers.md). 

En este paso, aprenderá a entrenar un modelo de aprendizaje automático con los paquetes de Python **scikit-Obtenga información acerca de** y **revoscalepy**. Estas bibliotecas de Python ya están instaladas con servicios de aprendizaje de máquina de SQL Server.

Cargar los módulos y llamar a las funciones necesarias para crear y entrenar el modelo con un procedimiento almacenado de SQL Server. El modelo requiere las características de datos diseñada en las lecciones anteriores. Por último, guarde el modelo entrenado para un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tabla.

> [!IMPORTANT]
> Ha habido varios cambios en el **revoscalepy** paquete, que requiere cambios pequeños en el código para este tutorial. Consulte la [la lista de cambios](sqldev-py6-operationalize-the-model.md#changes) al final de este tutorial. 
> 
> Si ha instalado servicios de Python con una versión preliminar de SQL Server 2017, se recomienda que actualice a la versión más reciente. 

## <a name="split-the-sample-data-into-training-and-testing-sets"></a>Dividir los datos de ejemplo de entrenamiento y conjuntos de pruebas

1. Puede usar el procedimiento almacenado **TrainTestSplit** para dividir los datos de la nyctaxi\_tabla de ejemplo en dos partes: nyctaxi\_ejemplo\_formación y nyctaxi\_ejemplo\_pruebas. 

    Este procedimiento almacenado ya se debe crear automáticamente, pero puede ejecutar el código siguiente para crearla:

    ```SQL
    CREATE PROCEDURE [dbo].[TrainTestSplit] (@pct int)
    AS
    
    DROP TABLE IF EXISTS dbo.nyctaxi_sample_training
    SELECT * into nyctaxi_sample_training FROM nyctaxi_sample WHERE (ABS(CAST(BINARY_CHECKSUM(medallion,hack_license)  as int)) % 100) < @pct
    
    DROP TABLE IF EXISTS dbo.nyctaxi_sample_testing
    SELECT * into nyctaxi_sample_testing FROM nyctaxi_sample
    WHERE (ABS(CAST(BINARY_CHECKSUM(medallion,hack_license)  as int)) % 100) > @pct
    GO
    ```

2. Para dividir los datos mediante una división personalizada, ejecute el procedimiento almacenado y escriba un entero que representa el porcentaje de datos asignados al conjunto de entrenamiento. Por ejemplo, la siguiente instrucción asignaría el 60% de los datos para el conjunto de entrenamiento.

    ```SQL
    EXEC TrainTestSplit 60
    GO
    ```

## <a name="build-a-logistic-regression-model"></a>Crear un modelo de regresión logística

Después de que se ha preparado los datos, puede usarlo para entrenar un modelo. Para ello, al llamar a un procedimiento procedimiento que se ejecuta el código Python, toma como entrada en la tabla de datos de entrenamiento. Para este tutorial, cree dos modelos, ambos modelos de clasificación binaria:

+ El procedimiento almacenado **TrainTipPredictionModelRxPy** crea un modelo de predicción de sugerencias con el **revoscalepy** paquete.
+ El procedimiento almacenado **TrainTipPredictionModelSciKitPy** crea un modelo de predicción de sugerencias con el **scikit-aprender** paquete.

Cada procedimiento almacenado utiliza los datos de entrada que proporcione para crear y entrenar un modelo de regresión logística. Todo el código Python se ajusta en el procedimiento almacenado del sistema, [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md).

Para que sea más fácil volver a entrenar el modelo con nuevos datos, incluya la llamada a sp_execute_exernal_script en otro procedimiento almacenado y pasar de los nuevos datos de entrenamiento como un parámetro. En esta sección le guiará a través de ese proceso.

### <a name="traintippredictionmodelscikitpy"></a>TrainTipPredictionModelSciKitPy

1.  En [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], abra una nueva **consulta** ventana y ejecute la instrucción siguiente para crear el procedimiento almacenado _TrainTipPredictionModelSciKitPy_.  El procedimiento almacenado contiene una definición de los datos de entrada, por lo que no es necesario proporcionar una consulta de entrada.

    ```SQL
    DROP PROCEDURE IF EXISTS TrainTipPredictionModelSciKitPy;
    GO

    CREATE PROCEDURE [dbo].[TrainTipPredictionModelSciKitPy] (@trained_model varbinary(max) OUTPUT)
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

    ```SQL
    DECLARE @model VARBINARY(MAX);
    EXEC TrainTipPredictionModelSciKitPy @model OUTPUT;
    INSERT INTO nyc_taxi_models (name, model) VALUES('SciKit_model', @model);
    ```

    Procesamiento de los datos y ajuste del modelo pueden tardar un par de minutos. Los mensajes que se canalizan a de Python **stdout** secuencia se muestran en la **mensajes** ventana de [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]. Por ejemplo:

    *Mensajes STDOUT de script externo:*
  *C:\Program Files\Microsoft SQL Server\MSSQL14. MSSQLSERVER\PYTHON_SERVICES\lib\site packages\revoscalepy*

3. Abra la tabla *nyc\_taxi_models*. Puede ver que se ha agregado una fila nueva, que contiene el modelo serializado en la columna _modelo_.

    *linear_model* *0x800363736B6C6561726E2E6C696E6561...*

### <a name="traintippredictionmodelrxpy"></a>TrainTipPredictionModelRxPy

Este procedimiento almacenado usa el nuevo **revoscalepy** paquete, que es un nuevo paquete de Python. Contiene los objetos, transformación y algoritmos similares a los proporcionados para el lenguaje R **RevoScaleR** paquete. 

Mediante el uso de **revoscalepy**, puede crear contextos de proceso remoto, el proceso de mover datos entre los contextos, transformar datos y entrenar modelos predictivos utilizando algoritmos populares, como la regresión logística y lineal, árboles de decisión, y más. Para obtener más información, vea [¿qué es revoscalepy?](../python/what-is-revoscalepy.md)

1. En [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], abra una nueva **consulta** ventana y ejecute la instrucción siguiente para crear el procedimiento almacenado _TrainTipPredictionModelRxPy_.  Dado que el procedimiento almacenado ya incluye una definición de los datos de entrada, no es necesario proporcionar una consulta de entrada.

    ```SQL
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

    - La consulta SELECT que aplica la función escalar personalizada _fnCalculateDistance_ para calcular la distancia directa entre las ubicaciones de recogida y entrega. Los resultados de la consulta se almacenan en la variable de entrada de Python de manera predeterminada, `InputDataset`.
    - La variable binaria _superpuesto_ se utiliza como el *etiqueta* o columna del resultado y el modelo es ajustar con estas columnas de característica: _passenger_count_, _trip_ distancia_, _trip_time_in_secs_, y _direct_distance_.
    - El modelo entrenado se serializa y se almacena en la variable de Python `logitObj`. Agregando la palabra clave de T-SQL salida, puede agregar la variable como una salida del procedimiento almacenado. En el paso siguiente, se utiliza esa variable para insertar código binario del modelo en una tabla de base de datos _nyc_taxi_models_. Este mecanismo hace más sencilla almacenar y volver a usar los modelos.

2. Ejecute el procedimiento almacenado como se indica a continuación para insertar el modelo **revoscalepy** modelo en la tabla _nyc\_taxi\_modelos.

    ```SQL
    DECLARE @model VARBINARY(MAX);
    EXEC TrainTipPredictionModelRxPy @model OUTPUT;
    
    INSERT INTO nyc_taxi_models (name, model) VALUES('revoscalepy_model', @model);
    ```

    Procesamiento de los datos y ajuste del modelo pueden tardar un poco. Los mensajes que se canalizan a de Python **stdout** secuencia se muestran en la **mensajes** ventana de [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]. Por ejemplo:

    *Mensajes STDOUT de script externo:*
  *C:\Program Files\Microsoft SQL Server\MSSQL14. MSSQLSERVER\PYTHON_SERVICES\lib\site packages\revoscalepy*

3. Abra la tabla *nyc_taxi_models*. Puede ver que se ha agregado una fila nueva, que contiene el modelo serializado en la columna _modelo_.

    *rx_model* *0x8003637265766F7363616c...*

En el paso siguiente, usa los modelos entrenados para crear predicciones.

## <a name="next-step"></a>Paso siguiente

[Paso 6: Poner el modelo de Python con SQL Server](sqldev-py6-operationalize-the-model.md)

## <a name="previous-step"></a>Paso anterior

[Paso 4: Crear características de datos mediante T-SQL](sqldev-py5-train-and-save-a-model-using-t-sql.md)
