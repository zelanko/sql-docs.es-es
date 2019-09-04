---
title: 'Tutorial de Python: Implementación del modelo (regresión lineal)'
description: En este tutorial usará Python y la regresión lineal en SQL Server Machine Learning Services para predecir el número de alquileres de esquí. Implementará un modelo de regresión lineal desarrollado en Python en una base de datos de SQL Server con Machine Learning Services.
ms.prod: sql
ms.technology: machine-learning
ms.date: 09/03/2019
ms.topic: tutorial
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 08f5d19af93ab180c660a264d5aaabc538d527a5
ms.sourcegitcommit: ecb19d0be87c38a283014dbc330adc2f1819a697
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/04/2019
ms.locfileid: "70242523"
---
# <a name="python-tutorial-deploy-a-linear-regression-model-to-sql-server-machine-learning-services"></a>Tutorial de Python: Implementar un modelo de regresión lineal en SQL Server Machine Learning Services
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

En la cuarta parte de esta serie de tutoriales de cuatro partes, implementará un modelo de regresión lineal desarrollado en Python en una base de datos de SQL Server con Machine Learning Services.

En este artículo, aprenderá a:

> [!div class="checklist"]
> * Crear un procedimiento almacenado que genera el modelo de aprendizaje automático
> * Almacenar el modelo en una tabla de base de datos
> * Crear un procedimiento almacenado que realice predicciones utilizando el modelo
> * Ejecutar el modelo con nuevos datos

En la [primera parte](python-ski-rental-linear-regression.md), aprendió a restaurar la base de datos de ejemplo.

En la [segunda parte](python-ski-rental-linear-regression-prepare-data.md), ha aprendido a cargar los datos de SQL Server en una trama de datos de Python y a preparar los datos en Python.

En la tercera [parte](python-ski-rental-linear-regression-train-model.md), aprendió a entrenar un modelo de aprendizaje automático de regresión lineal en Python.

## <a name="prerequisites"></a>Requisitos previos

* En la cuarta parte de este tutorial se supone que ha completado la [parte uno](python-ski-rental-linear-regression.md) y sus requisitos previos.

## <a name="create-a-stored-procedure-that-generates-the-model"></a>Crear un procedimiento almacenado que genere el modelo

Ahora, con los scripts de Python desarrollados, cree un procedimiento almacenado **generate_rental_rx_model** que entrena y genere el modelo de regresión lineal mediante LinearRegression desde scikit-Learn.

Ejecute la siguiente instrucción T-SQL en Azure Data Studio para crear el procedimiento almacenado para entrenar el modelo.

```sql
-- Stored procedure that trains and generates a Python model using the rental_data and a decision tree algorithm
DROP PROCEDURE IF EXISTS generate_rental_py_model;
go
CREATE PROCEDURE generate_rental_py_model (@trained_model varbinary(max) OUTPUT)
AS
BEGIN
    EXECUTE sp_execute_external_script
      @language = N'Python'
    , @script = N'
from sklearn.linear_model import LinearRegression
import pickle

df = rental_train_data

# Get all the columns from the dataframe.
columns = df.columns.tolist()

# Store the variable well be predicting on.
target = "RentalCount"

# Initialize the model class.
lin_model = LinearRegression()

# Fit the model to the training data.
lin_model.fit(df[columns], df[target])

# Before saving the model to the DB table, convert it to a binary object
trained_model = pickle.dumps(lin_model)'

, @input_data_1 = N'select "RentalCount", "Year", "Month", "Day", "WeekDay", "Snow", "Holiday" from dbo.rental_data where Year < 2015'
, @input_data_1_name = N'rental_train_data'
, @params = N'@trained_model varbinary(max) OUTPUT'
, @trained_model = @trained_model OUTPUT;
END;
GO
```

## <a name="store-the-model-in-a-database-table"></a>Almacenar el modelo en una tabla de base de datos

Cree una tabla en la base de datos TutorialDB y, a continuación, guarde el modelo en la tabla.

1. Ejecute la siguiente instrucción T-SQL en Azure Data Studio para crear una tabla denominada **dbo. rental_py_models** , que se usa para almacenar el modelo.

    ```sql
    USE TutorialDB;
    DROP TABLE IF EXISTS dbo.rental_py_models;
    GO
    CREATE TABLE dbo.rental_py_models (
        model_name VARCHAR(30) NOT NULL DEFAULT('default model') PRIMARY KEY,
        model VARBINARY(MAX) NOT NULL
    );
    GO
    ```

1. Guarde el modelo en la tabla como un objeto binario, con el nombre de modelo **linear_model**.

    ```sql
    DECLARE @model VARBINARY(MAX);
    EXEC generate_rental_py_model @model OUTPUT;
    
    INSERT INTO rental_py_models (model_name, model) VALUES('linear_model', @model);
    ```

## <a name="create-a-stored-procedure-that-makes-predictions"></a>Crear un procedimiento almacenado que realice predicciones

1. Cree un procedimiento almacenado **py_predict_rentalcount** que realice predicciones utilizando el modelo entrenado y un conjunto de datos nuevos. Ejecute el T-SQL siguiente en Azure Data Studio.

    ```sql
    DROP PROCEDURE IF EXISTS py_predict_rentalcount;
    GO
    CREATE PROCEDURE py_predict_rentalcount (@model varchar(100))
    AS
    BEGIN
        DECLARE @py_model varbinary(max) = (select model from rental_py_models where model_name = @model);
    
        EXEC sp_execute_external_script
                    @language = N'Python',
                    @script = N'
    
    # Import the scikit-learn function to compute error.
    from sklearn.metrics import mean_squared_error
    import pickle
    import pandas as pd
    
    rental_model = pickle.loads(py_model)
    
    df = rental_score_data
    
    # Get all the columns from the dataframe.
    columns = df.columns.tolist()
    
    # Variable you will be predicting on.
    target = "RentalCount"
    
    # Generate the predictions for the test set.
    lin_predictions = rental_model.predict(df[columns])
    print(lin_predictions)
    
    # Compute error between the test predictions and the actual values.
    lin_mse = mean_squared_error(lin_predictions, df[target])
    #print(lin_mse)
    
    predictions_df = pd.DataFrame(lin_predictions)
    
    OutputDataSet = pd.concat([predictions_df, df["RentalCount"], df["Month"], df["Day"], df["WeekDay"], df["Snow"], df["Holiday"], df["Year"]], axis=1)
    '
    , @input_data_1 = N'Select "RentalCount", "Year" ,"Month", "Day", "WeekDay", "Snow", "Holiday"  from rental_data where Year = 2015'
    , @input_data_1_name = N'rental_score_data'
    , @params = N'@py_model varbinary(max)'
    , @py_model = @py_model
    with result sets (("RentalCount_Predicted" float, "RentalCount" float, "Month" float,"Day" float,"WeekDay" float,"Snow" float,"Holiday" float, "Year" float));
    
    END;
    GO
    ```

1. Cree una tabla para almacenar las predicciones.

    ```sql
    DROP TABLE IF EXISTS [dbo].[py_rental_predictions];
    GO

    CREATE TABLE [dbo].[py_rental_predictions](
     [RentalCount_Predicted] [int] NULL,
     [RentalCount_Actual] [int] NULL,
     [Month] [int] NULL,
     [Day] [int] NULL,
     [WeekDay] [int] NULL,
     [Snow] [int] NULL,
     [Holiday] [int] NULL,
     [Year] [int] NULL
    ) ON [PRIMARY]
    GO
    ```

1. Ejecutar el procedimiento almacenado para predecir los recuentos de alquiler

    ```sql
    --Insert the results of the predictions for test set into a table
    INSERT INTO py_rental_predictions
    EXEC py_predict_rentalcount 'linear_model';

    -- Select contents of the table
    SELECT * FROM py_rental_predictions;
    ```

Ha creado, entrenado e implementado correctamente un modelo en una SQL Server Machine Learning Services. A continuación, se usa ese modelo en un procedimiento almacenado para predecir valores basados en datos nuevos.

## <a name="next-steps"></a>Pasos siguientes

En la cuarta parte de esta serie de tutoriales, ha completado estos pasos:

* Crear un procedimiento almacenado que genera el modelo de aprendizaje automático
* Almacenar el modelo en una tabla de base de datos
* Crear un procedimiento almacenado que realice predicciones utilizando el modelo
* Ejecutar el modelo con nuevos datos

Para obtener más información sobre el uso de Python en SQL Server Machine Learning Services, consulte:

+ [Tutoriales de Python para SQL Server Machine Learning Services](sql-server-python-tutorials.md)