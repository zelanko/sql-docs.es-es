---
title: 'Guía de inicio rápido para los modelos de Python para el entrenamiento y predicciones mediante procedimientos almacenados: SQL Server Machine Learning'
description: Insertar código de Python en procedimientos almacenados de SQL Server para crear, entrenar y usar un modelo de Python con el conjunto de datos de Iris clásico. Guardar un modelo entrenado en SQL Server y, a continuación, usarlo para generar resultados.
ms.prod: sql
ms.technology: machine-learning
ms.date: 01/04/2019
ms.topic: tutorial
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: e8bacc383eba1148c1b357c344bc483e824df99b
ms.sourcegitcommit: baca29731a1be4f8fa47567888278394966e2af7
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/04/2019
ms.locfileid: "54046975"
---
# <a name="quickstart-create-train-and-use-a-python-model-with-stored-procedures-in-sql-server"></a>Inicio rápido: Crear, entrenar y usar un modelo de Python con procedimientos almacenados en SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

En este tutorial con Python, creará y ejecutará dos procedimientos almacenados. El primero usa el conjunto de datos Iris clásico y genera un modelo de Naïve Bayes para predecir una especie de Iris en función de las características de flor. El segundo procedimiento es para la puntuación. Lo llama el modelo generado en el primer procedimiento para generar un conjunto de predicciones. Al colocar código en un procedimiento almacenado, las operaciones son independientes, reutilizables y que se puede llamar mediante otros procedimientos almacenados y las aplicaciones cliente. 

Al completar este tutorial rápido, aprenderá lo siguiente:

> [!div class="checklist"]
> * Procedimiento para insertar código de Python en un procedimiento almacenado
> * Cómo pasar entradas en el código a través de entradas en el procedimiento almacenado
> * Cómo se utilizan procedimientos almacenados para hacer operativos los modelos

## <a name="prerequisites"></a>Requisitos previos

Un tutorial anterior, [Python Compruebe que existe en SQL Server](quickstart-python-verify.md), proporciona información y vínculos para configurar el entorno de Python necesario para este inicio rápido.

Los datos de ejemplo utilizados en este ejercicio están la [ **irissql** ](demo-data-iris-in-sql.md) base de datos.

## <a name="create-a-stored-procedure-that-generates-models"></a>Crear un procedimiento almacenado que genera modelos

Es un patrón común en el desarrollo de SQL Server organizar las operaciones programables en distintos procedimientos almacenados. En este paso, creará un procedimiento almacenado que genera un modelo para predecir los resultados. 

1. Abra una nueva ventana de consulta en Management Studio, conectado a la **irissql** base de datos. 

    ```sql
    USE irissql
    GO
    ```

2. Copiar en el código siguiente para crear un nuevo procedimiento almacenado. 

   Cuando se ejecuta, este procedimiento llama [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) para iniciar una sesión de Python. 
   
   Las entradas que necesita el código Python se pasan como parámetros de entrada en este procedimiento almacenado. Salida será un modelo entrenado, basándose en la versión de Python **scikit-aprender** biblioteca para el algoritmo de aprendizaje automático. 

   Este código usa [ **pickle** ](https://docs.python.org/2/library/pickle.html) para serializar el modelo. Se va a entrenar el modelo utilizando los datos de las columnas 0 y 4 de la **iris_data** tabla. 
   
   Los parámetros que se ve en la segunda parte del procedimiento articulan entradas de datos y genera el modelo. Tanto como sea posible, se desea que el código de Python que se ejecuta en un procedimiento almacenado para que se ha definido claramente las entradas y salidas que se asignan al procedimiento almacenado entradas y salidas que se pasa en tiempo de ejecución. 

    ```sql
    CREATE PROCEDURE generate_iris_model (@trained_model varbinary(max) OUTPUT)
    AS
    BEGIN
    EXEC sp_execute_external_script @language = N'Python',
    @script = N'
    import pickle
    from sklearn.naive_bayes import GaussianNB
    GNB = GaussianNB()
    trained_model = pickle.dumps(GNB.fit(iris_data[[0,1,2,3]], iris_data[[4]].values.ravel()))
    '
    , @input_data_1 = N'select "Sepal.Length", "Sepal.Width", "Petal.Length", "Petal.Width", "SpeciesId" from iris_data'
    , @input_data_1_name = N'iris_data'
    , @params = N'@trained_model varbinary(max) OUTPUT'
    , @trained_model = @trained_model OUTPUT;
    END;
    GO
    ```

3. Compruebe si que existe el procedimiento almacenado. 

   Si el script de T-SQL en el paso anterior se ejecutó sin errores, un nuevo procedimiento almacenado llamado **generate_iris_model** se crea y agrega a la **irissql** base de datos. Puede encontrar los procedimientos almacenados en Management Studio **Explorador de objetos**, en **programación**.

## <a name="execute-the-procedure-to-create-and-train-models"></a>Ejecute el procedimiento para crear y entrenar modelos

En este paso, ejecute el procedimiento para ejecutar el código incrustado, creación de un modelo entrenado y serializarse como salida. Los modelos que se almacenan para su reutilización en SQL Server se serializa como una secuencia de bytes y se almacenan en una columna varbinary (max) en una tabla de base de datos. Una vez que el modelo se crea, entrenado, serializar y guardado en una base de datos, puede llamarse mediante otros procedimientos o a través del [T-SQL PREDECIR](https://docs.microsoft.com/sql/t-sql/queries/predict-transact-sql) función en las cargas de trabajo de puntuación.

1. Copie el código siguiente para ejecutar el procedimiento. La instrucción específica para ejecutar un procedimiento almacenado es `EXEC` en la quinta línea.

   Este script elimina un modelo existente del mismo nombre ("Bayes Naive") para dejar espacio para nuevos creados por volver a ejecutar el mismo procedimiento. Sin que se eliminen del modelo, produce un error que indica que el objeto ya existe. El modelo se almacena en una tabla denominada **iris_models**, aprovisionaron cuando creó la **irissql** base de datos.

    ```sql
    DECLARE @model varbinary(max);
    DECLARE @new_model_name varchar(50)
    SET @new_model_name = 'Naive Bayes'
    EXEC generate_iris_model @model OUTPUT;
    DELETE iris_models WHERE model_name = @new_model_name;
    INSERT INTO iris_models (model_name, model) values(@new_model_name, @model);
    GO
    ```

2. Compruebe que se insertó el modelo es otra manera de devolver una lista de modelos

    ```sql
    SELECT * FROM dbo.iris_models
    ```

    **Resultado**

    | MODEL_NAME  | model |
    |---|-----------------|
    | Bayes naive | 0x800363736B6C6561726E2E6E616976655F62617965730A... | 

## <a name="create-and-execute-a-stored-procedure-for-generating-predictions"></a>Crear y ejecutar un procedimiento almacenado para generar predicciones

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

En este ejercicio, ha aprendido a crear procedimientos almacenados dedicados para tareas diferentes, donde cada procedimiento almacenado usa el procedimiento almacenado del sistema [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) para iniciar un proceso de Python. Entradas para el proceso de Python se pasan al script sp_execute_external como parámetros. Tanto el propio script de Python y las variables de datos en una base de datos de SQL Server se pasan como entradas.

Por lo general, sólo debe planear sobre el uso de SSMS con código Python pulido o código de Python simple que devuelve un resultado basado en filas. Como una herramienta de SSMS admite los lenguajes de consulta similar a Transact-SQL y devuelve los conjuntos de filas planas. Si el código genera visual parecido a un gráfico de dispersión o de histograma, necesita una aplicación de la herramienta o del usuario final que puede presentar la imagen.

Para algunos desarrolladores de Python que sirven para escribir secuencias de comandos con todo incluido una variedad de operaciones de control, puede parecer innecesario organizar tareas en procedimientos independientes. Pero, de entrenamiento y puntuación tienen distintos casos de uso. Si los separa, puede colocar cada tarea en otra programación y los permisos de ámbito para la operación.

Del mismo modo, también puede aprovechar los recursos de características de SQL Server, como el procesamiento paralelo, la regulación de recursos, o al escribir la secuencia de comandos para usar algoritmos en [revoscalepy](../python/ref-py-revoscalepy.md) o [microsoftml](../python/ref-py-microsoftml.md) que compatibilidad con streaming y ejecución en paralelo. Mediante la separación de entrenamiento y puntuación, puede tener como destino las optimizaciones para cargas de trabajo específicas.

Una ventaja final es que los procesos pueden modificarse mediante parámetros. En este ejercicio, el código de Python que se creó el modelo (denominado "Bayes Naive" en este ejemplo) se pasó como entrada a un segundo procedimiento almacenado que llamar al modelo en un proceso de puntuación. Este ejercicio solo usa un modelo, pero se puede imaginar cómo parametrizar el modelo en una tarea de puntuación haría que esa secuencia de comandos más útiles.

## <a name="next-steps"></a>Pasos siguientes

Si es desarrollador SQL familiarizado con Python, revise los pasos y herramientas para trabajar con código de Python de forma local, con la capacidad de desplazar la ejecución de las sesiones de locales a una instancia remota de SQL Server.

> [!div class="nextstepaction"]
> [Configurar una estación de trabajo del cliente de Python](../python/setup-python-client-tools-sql.md).

