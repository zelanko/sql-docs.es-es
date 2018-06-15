---
title: Usar el modelo de Python en SQL para el entrenamiento y puntuación | Documentos de Microsoft
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: b7f5883356ff6878f869ee10f915bcb93a2dba17
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
ms.locfileid: "31202297"
---
# <a name="use-python-model-in-sql-for-training-and-scoring"></a>Utilizar el modelo de Python en SQL para el entrenamiento y de puntuación
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

En el [lección anterior](wrap-python-in-tsql-stored-procedure.md), ha aprendido el modelo común para el uso de Python junto con SQL. Ha aprendido que su Python código debe data.frame claramente definido uno de salida y, opcionalmente, puede devolver varias variables escalares o binarias. Ahora sabe que el procedimiento almacenado de SQL se debe diseñar para pasar el tipo de datos correcto en Python y controlar los resultados.

En esta sección, puedes usan este mismo patrón para entrenar un modelo en los datos que ha agregado a SQL Server y guarden el modelo en una tabla de SQL Server:

+ Diseñar un procedimiento almacenado que llama a un función de aprendizaje automático de Python.
+ El procedimiento almacenado necesita que los datos de SQL Server para utilizarla en el entrenamiento del modelo.
+ El procedimiento almacenado genera un modelo entrenado como una variable binaria. 
+ Guarde el modelo entrenado insertando el modelo de variable en una tabla. 

## <a name="create-the-stored-procedure-and-train-a-python-model"></a>Crear el procedimiento almacenado y entrenar un modelo de Python

1. Ejecute el siguiente código en SQL Server Management Studio para crear el procedimiento almacenado que genera un modelo.

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

2. Si este comando se ejecuta sin errores, se crea un nuevo procedimiento almacenado y se agrega a la base de datos. Puede encontrar los procedimientos almacenados en Management Studio **Explorador de objetos**, en **programación**.

3. Ahora ejecute el procedimiento almacenado.

    ```sql
    EXEC generate_iris_model
    ```

    Debería obtener un error, ya que aún no proporcionó que los datos proporcionados por el procedimiento almacenado requiere.

    "Procedimiento o función 'generate_iris_model' espera un parámetro '@trained_model', que no se proporcionó."

4. Para generar el modelo con las entradas necesarias y guardarla en una tabla requiere algunas instrucciones adicionales:

    ```sql
    DECLARE @model varbinary(max);
    EXEC generate_iris_model @model OUTPUT;
    INSERT INTO iris_models (model_name, model) values('Naive Bayes', @model);
    ```

5. Ahora, vuelva a ejecutar el código de generación de modelo una vez más. 

    Obtendrá el error: "infracción de restricción PRIMARY KEY no puede insertar una clave duplicada en el objeto 'dbo.iris_models'. El valor de clave duplicada es (Bayes Naive) ".

    Eso es porque no se proporcionó el nombre del modelo, escriba manualmente en "Bayes Naive" como parte de la instrucción INSERT. Suponiendo que va a crear una gran cantidad de modelos, con parámetros diferentes o algoritmos diferentes en cada ejecución, debe considerar cómo configurar un esquema de metadatos para que se pueden asignar nombre automáticamente a los modelos y más identifican fácilmente.

6. Para solucionar este error, puede realizar algunas modificaciones menores en el contenedor SQL. En este ejemplo genera el nombre de un modelo único anexando la fecha y hora actuales:

    ```sql
    DECLARE @model varbinary(max);
    DECLARE @new_model_name varchar(50)
    SET @new_model_name = 'Naive Bayes ' + CAST(GETDATE()as varchar)
    SELECT @new_model_name 
    EXEC generate_iris_model @model OUTPUT;
    INSERT INTO iris_models (model_name, model) values(@new_model_name, @model);
    ```

7. Para ver los modelos, ejecute una instrucción SELECT simple.

    ```sql
    SELECT * FROM iris_models;
    GO
    ```

    **Resultado**

    |MODEL_NAME | model |
    |------|------|
    | Bayes naive | 0x800363736B6C656172... |
    | Bayes naive de 2018 01 de enero 9:39 AM | 0x800363736B6C656172... |
    | Bayes naive 01 de Feb de 2018 10:51 A.M. | 0x800363736B6C656172... |

## <a name="generate-scores-from-the-model"></a>Generar puntuaciones a partir del modelo

Por último, vamos a cargar este modelo de la tabla en una variable y devuélvalo al Python para generar puntuaciones.

1. Ejecute el siguiente código para crear el procedimiento almacenado que realiza la puntuación. 

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
    OutputDataSet = iris_data.query( ''PredictedSpecies != SpeciesId'' )[[0, 5, 6]]
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

    El procedimiento almacenado Obtiene el modelo de Naïve Bayes de la tabla y las funciones asociadas con el modelo utiliza para generar puntuaciones. En este ejemplo, el procedimiento almacenado Obtiene el modelo de la tabla utilizando el nombre del modelo. Sin embargo, dependiendo de qué tipo de metadatos va a guardar con el modelo, también puede obtener el modelo más reciente, o el modelo con la mayor precisión.

2. Ejecute las siguientes líneas para pasar el nombre del modelo "Bayes Naive de" para el procedimiento almacenado que se ejecuta el código de puntuación. 

    ```sql
    EXEC predict_species 'Naive Bayes';
    GO
    ```

    Al ejecutar el procedimiento almacenado, devuelve un data.frame de Python. Esta línea de código T-SQL especifica el esquema para los resultados devueltos: `WITH RESULT SETS ( ("id" int, "SpeciesId" int, "SpeciesId.Predicted" int));`

    Puede insertar los resultados en una tabla nueva o devolverlos a una aplicación.

    En este ejemplo se ha realizado simple mediante el uso de los datos del conjunto de datos de iris de Python para puntuar. (Vea la línea `iris_data[[1,2,3,4]])`.) Sin embargo, por lo general se podría ejecutar una consulta SQL para obtener los nuevos datos y pasar ese en Python como `InputDataSet`. 

### <a name="remarks"></a>Comentarios

Si está acostumbrado a trabajar en Python, es posible que acostumbrado a cargar los datos, crear algunos resúmenes y gráficos, a continuación, entrenar un modelo y generar algunas puntuaciones en las mismas 250 líneas de código.

Sin embargo, si su objetivo es poner el proceso (creación de modelos, la puntuación, etc.) en SQL Server, es importante tener en cuenta las formas que puede separar el proceso en pasos repetibles que pueden modificarse mediante parámetros. Tanto como sea posible, desea que el código de Python que se ejecutan en un procedimiento almacenado para tener claramente definidos entradas y salidas que se asignan a un procedimiento almacenado entradas y salidas.

Además, por lo general puede mejorar el rendimiento al separar el proceso de exploración de datos de los procesos de entrenar un modelo o generar puntuaciones. 

Procesos de entrenamiento y puntuación a menudo se pueden optimizar mediante el aprovechamiento de características de SQL Server, como el procesamiento paralelo, o mediante el uso de algoritmos en [revoscalepy](../python/what-is-revoscalepy.md) o [MicrosoftML](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package) esa compatibilidad con transmisión por secuencias y la ejecución en paralelo, en lugar de utilizar bibliotecas estándares de Python. 

## <a name="next-lesson"></a>Lección siguiente

En la última lección, se ejecuta el código Python desde un cliente remoto, con SQL Server como el contexto de proceso. Este paso es opcional, si no dispone de un cliente de Python, o no va a ejecutar Python fuera de un procedimiento almacenado.

+ [Crear un modelo de revoscalepy desde un cliente de Python](use-python-revoscalepy-to-create-model.md)
