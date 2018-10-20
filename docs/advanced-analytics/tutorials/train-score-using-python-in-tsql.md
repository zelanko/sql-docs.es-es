---
title: Usar un modelo de Python en SQL Server para el entrenamiento y las predicciones | Microsoft Docs
description: Crear y entrenar un modelo con Python y el conjunto de datos de Iris clásico. Guardar el modelo en SQL Server y, a continuación, usarlo para generar resultados.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/18/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 839bcecdeaf7b5e2a7ea1297fe941353bffed20e
ms.sourcegitcommit: 3cd6068f3baf434a4a8074ba67223899e77a690b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/19/2018
ms.locfileid: "49461841"
---
# <a name="use-a-python-model-in-sql-server-for-training-and-scoring"></a>Usar un modelo de Python en SQL Server para el entrenamiento y puntuación
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

En este ejercicio de Python, obtenga información sobre un patrón común para crear, entrenar y con un modelo en SQL Server. Este ejercicio crea dos procedimientos almacenados. La primera de ellas genera un modelo de Naïve Bayes para predecir una especie de Iris en función de las características de flor. El segundo procedimiento es para la puntuación. Lo llama el modelo generado en el primer procedimiento para generar un conjunto de predicciones. Mediante la ejecución paso a paso a través de este ejercicio, aprenderá técnicas básicas que son fundamentales para ejecutar código de Python en una instancia del motor de base de datos de SQL Server.

Datos de ejemplo utilizados en este ejercicio están la [conjunto de datos Iris](demo-data-iris-in-sql.md) en el **irissql** base de datos.

## <a name="create-a-model-using-a-sproc"></a>Crear un modelo con un procedimiento almacenado

1. Abra una nueva ventana de consulta en Management Studio, conectado a la **irissql** base de datos. 

    ```sql
    USE irissql
    GO
    ```

2. Ejecute el siguiente código en una nueva ventana de consulta para crear el procedimiento almacenado que crea y entrena un modelo. Los modelos que se almacenan para su reutilización en SQL Server se serializa como una secuencia de bytes y se almacenan en una columna varbinary (max) en una tabla de base de datos. Una vez creado, el modelo entrenado, serializar y guardado en una base de datos, se puede llamar otros procedimientos o por la función T-SQL PREDECIR en cargas de trabajo de puntuación.

   Este código usa pickle para serializar el modelo y scikit para proporcionar el algoritmo Naïve Bayes. Se va a entrenar el modelo utilizando los datos de las columnas 0 y 4 de la **iris_data** tabla. Los parámetros que se ve en la segunda parte del procedimiento articulan entradas de datos y genera el modelo. 

    ```sql
    CREATE PROCEDURE generate_iris_model (@trained_model varbinary(max) OUTPUT)
    AS
    BEGIN
    EXEC sp_execute_external_script @language = N'Python',
    @script = N'
    import pickle
    from sklearn.naive_bayes import GaussianNB
    GNB = GaussianNB()
    trained_model = pickle.dumps(GNB.fit(iris_data[[0,1,2,3]], iris_data[[4]]))
    '
    , @input_data_1 = N'select "Sepal.Length", "Sepal.Width", "Petal.Length", "Petal.Width", "SpeciesId" from iris_data'
    , @input_data_1_name = N'iris_data'
    , @params = N'@trained_model varbinary(max) OUTPUT'
    , @trained_model = @trained_model OUTPUT;
    END;
    GO
    ```

3. Compruebe si que existe el procedimiento almacenado. Si el script de T-SQL en el paso anterior se ejecutó sin errores, un nuevo procedimiento almacenado llamado **generate_iris_model** se crea y agrega a la **irissql** base de datos. Puede encontrar los procedimientos almacenados en Management Studio **Explorador de objetos**, en **programación**.

## <a name="execute-the-sproc-to-create-and-train-models"></a>Ejecute el procedimiento almacenado para crear y entrenar modelos

1. Después de crea el procedimiento almacenado, ejecute el siguiente código a continuación para ejecutarlo. La instrucción específica para ejecutar un procedimiento almacenado es `EXEC` en la quinta línea.

   Este script elimina un modelo existente del mismo nombre ("Bayes Naive") para dejar espacio para nuevos creados por volver a ejecutar el mismo procedimiento. Sin que se eliminen del modelo, produce un error que indica que el objeto ya existe. 

    ```sql
    DECLARE @model varbinary(max);
    DECLARE @new_model_name varchar(50)
    SET @new_model_name = 'Naive Bayes '
    SELECT @new_model_name 
    EXEC generate_iris_model @model OUTPUT;
    DELETE iris_models WHERE model_name = @new_model_name;
    INSERT INTO iris_models (model_name, model) values(@new_model_name, @model);
    GO
    ```

2. Ver los resultados en el área de salida. El script incluye una instrucción SELECT que muestra que existe el modelo. Otra manera de devolver una lista de modelos es `SELECT * FROM iris_models` en **irissql**.

    **Resultado**

    |   | (sin nombre de columna |
    |---|-----------------|
    | 1 | Bayes naive     | 


## <a name="create-and-execute-a-sproc-for-generating-predictions"></a>Crear y ejecutar un procedimiento almacenado para generar predicciones

Ahora que ha creado, entrenado y guardar un modelo, pasar al siguiente paso: crear un procedimiento almacenado que genera predicciones. Para ello, que realiza la llamada sp_execute_external_script iniciar Python, y, a continuación, pasar en el script de Python que carga un modelo serializado creado en el ejercicio anterior y, a continuación, le da las entradas de datos para puntuación.

1. Ejecute el siguiente código para crear el procedimiento almacenado que realiza la puntuación. En tiempo de ejecución, este procedimiento se carga un modelo binario, use columnas `[1,2,3,4]` como entradas y especificar las columnas `[0,5,6]` como salida.

    ```sql
    CREATE PROCEDURE predict_species (@model varchar(100))
    AS
    BEGIN
    DECLARE @nb_model varbinary(max) = (SELECT model FROM iris_models WHERE model_name = @model);
    EXEC sp_execute_external_script @language = N'Python', 
    @script = N'
    import pickle
    irismodel = pickle.loads(nb_model)
    species_pred = irismodel.predict(iris_data[[1,2,3,4]])
    iris_data["PredictedSpecies"] = species_pred
    OutputDataSet = iris_data[[0,5,6]] 
    print(OutputDataSet)
    '
    , @input_data_1 = N'select id, "Sepal.Length", "Sepal.Width", "Petal.Length", "Petal.Width", "SpeciesId" from iris_data'
    , @input_data_1_name = N'iris_data'
    , @params = N'@nb_model varbinary(max)'
    , @nb_model = @nb_model
    WITH RESULT SETS ( ("id" int, "SpeciesId" int, "SpeciesId.Predicted" int));
    END;
    GO
    ```

2. Ejecutar el procedimiento almacenado, lo que proporciona el nombre del modelo "Bayes Naive de" para que el procedimiento sepa qué modelo va a usar. 

    ```sql
    EXEC predict_species 'Naive Bayes';
    GO
    ```

    Al ejecutar el procedimiento almacenado, devuelve un data.frame de Python. Esta línea de Transact-SQL especifica el esquema para los resultados devueltos: `WITH RESULT SETS ( ("id" int, "SpeciesId" int, "SpeciesId.Predicted" int));`. Puede insertar los resultados en una tabla nueva o devolverlos a una aplicación.

    ![Conjunto de resultados de ejecución de procedimiento almacenado](media/train-score-using-python-NB-model-results.png)

    Los resultados son 150 predicciones sobre especie utilizando las características de motivos florales como entradas. Para la mayoría de las observaciones, la especie predicha coincide con la especie real.

    En este ejemplo se ha convertido simple utilizando el conjunto de datos de iris de Python para entrenamiento y puntuación. Un enfoque más habitual sería implican la ejecución de una consulta SQL para obtener los nuevos datos y que pase a Python como `InputDataSet`. 

## <a name="conclusion"></a>Conclusión

En este ejercicio, ha aprendido a crear procedimientos almacenados para tareas diferentes, donde cada procedimiento almacenado usa el procedimiento almacenado del sistema [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) para iniciar un proceso de Python. Entradas para el proceso de Python se pasan al script sp_execute_external como parámetros. Tanto el propio script de Python y las variables de datos en una base de datos de SQL Server se pasan como entradas.

Si está acostumbrado a trabajar en Python, es posible que acostumbrado a cargar los datos, crear algunos resúmenes y gráficos, a continuación, entrenar un modelo y generar algunas puntuaciones en la mismas 250 líneas de código. En este artículo difiere de enfoques habituales mediante la organización de las operaciones en procedimientos independientes. Esta práctica es útil en varios niveles.

Una ventaja es que puede separar los procesos repetibles pasos que se pueden modificar mediante parámetros. Tanto como sea posible, desea que el código de Python que se ejecuta en un procedimiento almacenado al que se ha definido claramente las entradas y salidas que se asignan a un procedimiento almacenado entradas y salidas que se pueden pasar en tiempo de ejecución. En este ejercicio, código de Python que crea un modelo (denominado "Bayes Naive" en este ejemplo) se pasa como entrada a un segundo procedimiento almacenado que llama al modelo en un proceso de puntuación.

Una segunda ventaja es la formación que necesita y se puede optimizar los procesos de puntuación mediante el aprovechamiento de las características de SQL Server, como el procesamiento paralelo, la regulación de recursos, o mediante el uso de algoritmos en [revoscalepy](../python/what-is-revoscalepy.md) o [MicrosoftML ](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package) que admiten el streaming y ejecución en paralelo. Mediante la separación de entrenamiento y puntuación, puede tener como destino las optimizaciones para cargas de trabajo específicas.

## <a name="next-steps"></a>Pasos siguientes

Tutoriales anteriores se centran en la ejecución local. Sin embargo, también puede ejecutar código de Python desde una estación de trabajo cliente, usar SQL Server como el contexto de cálculo remoto. Para obtener más información acerca de cómo configurar una estación de trabajo cliente que se conecta a SQL Server, vea [configurar herramientas de cliente de Python](../python/setup-python-client-tools-sql.md).

+ [Crear un modelo de revoscalepy desde un cliente de Python](use-python-revoscalepy-to-create-model.md)
