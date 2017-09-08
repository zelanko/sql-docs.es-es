---
title: 'Paso 5: Entrenar y guardar un modelo con T-SQL | Microsoft Docs'
ms.custom: 
ms.date: 07/26/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology:
- python-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2017
dev_langs:
- Python
- TSQL
ms.assetid: 
caps.latest.revision: 2
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 80a47819dfbb2e96162a49730e0dcf0b1b340f07
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="step-5-train-and-save-a-model-using-t-sql"></a>Paso 5: Entrenar y guardar un modelo mediante T-SQL

En este paso, aprenderá a entrenar un modelo de aprendizaje automático con los paquetes de Python **scikit-Obtenga información acerca de** y **revoscalepy**. Estas bibliotecas de Python ya están instaladas con servicios de aprendizaje de máquina de SQL Server, por lo que puede cargar los módulos y llamar a las funciones necesarias desde dentro de un procedimiento almacenado. Puede entrenar el modelo mediante las características de datos que acaba de crear y, después, guardar el modelo entrenado en una tabla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .

## <a name="split-the-sample-data-into-training-and-testing-sets"></a>Dividir los datos de ejemplo de entrenamiento y conjuntos de pruebas

1. Ejecute los siguientes comandos de T-SQL para crear un procedimiento almacenado que divide los datos en el nyctaxi\_tabla de ejemplo en dos partes: nyctaxi\_ejemplo\_formación y nyctaxi\_ejemplo\_pruebas.

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

2. Ejecute el procedimiento almacenado y escriba un entero que representa el porcentaje de datos asignados al conjunto de entrenamiento. Por ejemplo, la siguiente instrucción asignaría el 60% de los datos para el conjunto de entrenamiento. Datos de pruebas y entrenamiento se almacenan en dos tablas independientes.

    ```SQL
    EXEC TrainTestSplit 60
    GO
    ```

## <a name="build-a-logistic-regression-model-using-scikit-learn"></a>Crear un modelo de regresión logística mediante scikit-Obtenga información acerca de

En esta sección, creará un procedimiento almacenado que se puede utilizar para entrenar un modelo con los datos de entrenamiento que acaba de preparar. Este procedimiento almacenado define los datos de entrada y usa un **scikit-aprender** función para entrenar un modelo de regresión logística. Se llama al tiempo de ejecución de Python que se instala con SQL Server mediante el procedimiento almacenado del sistema, [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md).

Para que sea más fácil volver a entrenar el modelo, puede ajustar la llamada a sp_execute_exernal_script en otro procedimiento almacenado y pase los nuevos datos de entrenamiento como un parámetro. En esta sección le guiará a través de ese proceso.

1.  En [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], abra una nueva **consulta** ventana y ejecute la instrucción siguiente para crear el procedimiento almacenado _TrainTipPredictionModelSciKitPy_.  Tenga en cuenta que el procedimiento almacenado contiene una definición de los datos de entrada, por lo que no es necesario proporcionar una consulta de entrada.

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
      import pandas
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

## <a name="build-a-logistic-model-using-the-revoscalepy-package"></a>Generar un modelo logística utilizando la _revoscalepy_ paquete

Ahora, cree otro procedimiento almacenado que utiliza el nuevo **revoscalepy** paquete para entrenar un modelo de regresión logística. El **revoscalepy** del paquete de Python contiene algoritmos similares a los proporcionados para el lenguaje R, transformación y objetos **RevoScaleR** paquete. Con esta biblioteca, puede crear un contexto de proceso, mover datos entre los contextos de proceso, transforman datos y entrenar modelos de predicción utilizando algoritmos populares, como la regresión logística y lineal, árboles de decisión y mucho más. Para obtener más información, vea [¿qué es revoscalepy?](../python/what-is-revoscalepy.md)

1. En [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], abra una nueva **consulta** ventana y ejecute la instrucción siguiente para crear el procedimiento almacenado _TrainTipPredictionModelRxPy_.  Este modelo también utiliza los datos de entrenamiento que acaba de preparar. Dado que el procedimiento almacenado ya incluye una definición de los datos de entrada, no es necesario proporcionar una consulta de entrada.

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
    import pandas
    from revoscalepy.functions.RxLogit import rx_logit_ex
    
    ## Create a logistic regression model using rx_logit_ex function from revoscalepy package
    logitObj = rx_logit_ex("tipped ~ passenger_count + trip_distance + trip_time_in_secs + direct_distance", data = InputDataSet);
    
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

    - Entrenar un modelo de regresión logística con el paquete de revoscalepy en nyctaxi\_ejemplo\_datos de entrenamiento.
    - La consulta SELECT usa la función escalar personalizada _fnCalculateDistance_ para calcular la distancia directa entre las ubicaciones de origen y destino. Los resultados de la consulta se almacenan en la variable de entrada de Python de manera predeterminada, `InputDataset`.
    - El script de Python llama la función de LogisticRegression del revoscalepy, que se incluye con [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], para crear el modelo de regresión logística.
    - La variable binaria _tipped_ se usa como la *etiqueta* o columna del resultado y el modelo se ajusta mediante estas columnas específicas:  _passenger_count_, _trip_distance_, _trip_time_in_secs_y _direct_distance_.
    - El modelo entrenado, contenido en la variable de Python `logitObj`, se serializa y se colocan como un parámetro de salida [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Que los resultados se insertan en la tabla de base de datos _nyc_taxi_models_, junto con su nombre, como una nueva fila, para que pueda recuperar y usar para las predicciones futuras.

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

[Paso 6: Poner el modelo](sqldev-py6-operationalize-the-model.md)

## <a name="previous-step"></a>Paso anterior

[Paso 4: Crear características de datos mediante T-SQL](sqldev-py5-train-and-save-a-model-using-t-sql.md)

