---
title: Crear y puntuar un modelo predictivo en Python
titleSuffix: SQL Server Machine Learning Services
description: Cree un modelo predictivo simple en Python mediante SQL Server Machine Learning Services y, a continuación, predicte un resultado con nuevos datos.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/14/2019
ms.topic: quickstart
author: garyericson
ms.author: garye
ms.reviewer: davidph
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: cb564d7dc8564b31a90a09f53aedaba953519f76
ms.sourcegitcommit: c7a202af70fd16467a498688d59637d7d0b3d1f3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/15/2019
ms.locfileid: "72313672"
---
# <a name="quickstart-create-and-score-a-predictive-model-in-python-with-sql-server-machine-learning-services"></a>Inicio rápido: Crear y puntuar un modelo predictivo en Python con SQL Server Machine Learning Services
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

En esta guía de inicio rápido, creará y entrenará un modelo predictivo mediante Python, guardará el modelo en una tabla en la instancia de SQL Server y, a continuación, usará el modelo para predecir valores de datos nuevos con [SQL Server Machine Learning Services](../what-is-sql-server-machine-learning.md).

Creará y ejecutará dos procedimientos almacenados que se ejecutan en SQL. El primero usa el conjunto de datos de flores de iris clásico y genera un modelo Bayes Naive para predecir una especie de iris basada en las características de la flor. El segundo procedimiento es para puntuar: llama al modelo generado en el primer procedimiento para generar un conjunto de predicciones basadas en nuevos datos. Al colocar el código en un procedimiento almacenado, otros procedimientos almacenados y aplicaciones cliente pueden volver a usar las operaciones, volver a utilizarlas y llamarlas.

Al completar esta guía de inicio rápido, aprenderá lo siguiente:

> [!div class="checklist"]
> - Cómo insertar código Python en un procedimiento almacenado
> - Cómo pasar entradas al código mediante entradas en el procedimiento almacenado
> - Cómo se usan los procedimientos almacenados para poner en funcionamiento los modelos

## <a name="prerequisites"></a>Requisitos previos

- Esta guía de inicio rápido requiere acceso a una instancia de SQL Server con [SQL Server Machine Learning Services](../install/sql-machine-learning-services-windows-install.md) con el idioma de Python instalado.

- También necesita una herramienta para ejecutar consultas SQL que contienen scripts de Python. Puede ejecutar estos scripts mediante cualquier herramienta de consulta o administración de bases de datos, siempre que pueda conectarse a una instancia de SQL Server y ejecutar una consulta T-SQL o un procedimiento almacenado. Esta guía de inicio rápido usa [SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/sql-server-management-studio-ssms).

- Los datos de ejemplo que se usan en este ejercicio son los datos de ejemplo de iris. Siga las instrucciones de [datos de demostración de iris](demo-data-iris-in-sql.md) para crear la base de datos de ejemplo **irissql**.

## <a name="create-a-stored-procedure-that-generates-models"></a>Crear un procedimiento almacenado que genera modelos

En este paso, creará un procedimiento almacenado que genera un modelo para predecir los resultados.

1. Abra una nueva ventana de consulta en SSMS conectada a la base de datos **irissql** . 

    ```sql
    USE irissql
    GO
    ```

1. Copie en el código siguiente para crear un nuevo procedimiento almacenado.

   Cuando se ejecuta, este procedimiento llama a [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) para iniciar una sesión de Python. 
   
   Las entradas necesarias para el código de Python se pasan como parámetros de entrada en este procedimiento almacenado. La salida será un modelo entrenado, basado en la biblioteca Python **scikit-Learn** para el algoritmo de aprendizaje automático. 

   Este código usa [**Pickle**](https://docs.python.org/2/library/pickle.html) para serializar el modelo. El modelo se entrenará con datos de las columnas 0 a 4 de la tabla **iris_data** . 
   
   Los parámetros que se ven en la segunda parte del procedimiento articulan las entradas de datos y las salidas del modelo. En la medida de lo posible, desea que el código de Python que se ejecuta en un procedimiento almacenado tenga claramente definidas entradas y salidas que se asignan a las entradas y salidas de procedimientos almacenados que se pasan en tiempo de ejecución.

    ```sql
    CREATE PROCEDURE generate_iris_model (@trained_model VARBINARY(max) OUTPUT)
    AS
    BEGIN
        EXECUTE sp_execute_external_script @language = N'Python'
            , @script = N'
    import pickle
    from sklearn.naive_bayes import GaussianNB
    GNB = GaussianNB()
    trained_model = pickle.dumps(GNB.fit(iris_data[["Sepal.Length", "Sepal.Width", "Petal.Length", "Petal.Width"]], iris_data[["SpeciesId"]].values.ravel()))
    '
            , @input_data_1 = N'select "Sepal.Length", "Sepal.Width", "Petal.Length", "Petal.Width", "SpeciesId" from iris_data'
            , @input_data_1_name = N'iris_data'
            , @params = N'@trained_model varbinary(max) OUTPUT'
            , @trained_model = @trained_model OUTPUT;
    END;
    GO
    ```

1. Compruebe que el procedimiento almacenado existe. 

   Si el script T-SQL del paso anterior se ejecutó sin errores, se crea un nuevo procedimiento almacenado llamado **generate_iris_model** y se agrega a la base de datos **irissql** . Puede encontrar procedimientos almacenados en el **Explorador de objetos**SSMS, en **programación**.

## <a name="execute-the-procedure-to-create-and-train-models"></a>Ejecutar el procedimiento para crear y entrenar modelos

En este paso, ejecutará el procedimiento para ejecutar el código incrustado, creando un modelo entrenado y serializado como una salida. 

Los modelos que se almacenan para su reutilización en SQL Server se serializan como una secuencia de bytes y se almacenan en una columna VARBINARY (MAX) en una tabla de base de datos. Una vez que se crea, entrena, serializa y guarda el modelo en una base de datos, se puede llamar mediante otros procedimientos o mediante la función de [T-SQL de predicción](https://docs.microsoft.com/sql/t-sql/queries/predict-transact-sql) en las cargas de trabajo de puntuación.

1. Ejecute el siguiente script para ejecutar el procedimiento. La instrucción específica para ejecutar un procedimiento almacenado es `EXECUTE` en la cuarta línea.

   Este script concreto elimina un modelo existente con el mismo nombre ("Bayes naive") para dejar espacio para los nuevos creados al ejecutar de nuevo el mismo procedimiento. Sin la eliminación del modelo, se produce un error que indica que el objeto ya existe. El modelo se almacena en una tabla denominada **iris_models**, aprovisionada al crear la base de datos **irissql** .

    ```sql
    DECLARE @model varbinary(max);
    DECLARE @new_model_name varchar(50)
    SET @new_model_name = 'Naive Bayes'
    EXECUTE generate_iris_model @model OUTPUT;
    DELETE iris_models WHERE model_name = @new_model_name;
    INSERT INTO iris_models (model_name, model) values(@new_model_name, @model);
    GO
    ```

1. Compruebe que se ha insertado el modelo.

    ```sql
    SELECT * FROM dbo.iris_models
    ```

    **Resultado**

    | model_name  | model |
    |---|-----------------|
    | Bayes naive | 0x800363736B6C6561726E2E6E616976655F62617965730A... | 

## <a name="create-and-execute-a-stored-procedure-for-generating-predictions"></a>Crear y ejecutar un procedimiento almacenado para generar predicciones

Ahora que ha creado, entrenado y guardado un modelo, continúe con el paso siguiente: crear un procedimiento almacenado que genere predicciones. Para ello, debe llamar a `sp_execute_external_script` para ejecutar un script de Python que carga el modelo serializado y proporciona nuevas entradas de datos para puntuar.

1. Ejecute el código siguiente para crear el procedimiento almacenado que realiza la puntuación. En tiempo de ejecución, este procedimiento cargará un modelo binario, utilizará columnas `[1,2,3,4]` como entradas y especificará las columnas `[0,5,6]` como salida.

   ```sql
   CREATE PROCEDURE predict_species (@model VARCHAR(100))
   AS
   BEGIN
       DECLARE @nb_model VARBINARY(max) = (
               SELECT model
               FROM iris_models
               WHERE model_name = @model
               );
   
       EXECUTE sp_execute_external_script @language = N'Python'
           , @script = N'
   import pickle
   irismodel = pickle.loads(nb_model)
   species_pred = irismodel.predict(iris_data[["Sepal.Length", "Sepal.Width", "Petal.Length", "Petal.Width"]])
   iris_data["PredictedSpecies"] = species_pred
   OutputDataSet = iris_data[["id","SpeciesId","PredictedSpecies"]] 
   print(OutputDataSet)
   '
           , @input_data_1 = N'select id, "Sepal.Length", "Sepal.Width", "Petal.Length", "Petal.Width", "SpeciesId" from iris_data'
           , @input_data_1_name = N'iris_data'
           , @params = N'@nb_model varbinary(max)'
           , @nb_model = @nb_model
       WITH RESULT SETS((
                   "id" INT
                 , "SpeciesId" INT
                 , "SpeciesId.Predicted" INT
                   ));
   END;
   GO
   ```

2. Ejecute el procedimiento almacenado y proporcione el nombre del modelo "Naive Bayes" para que el procedimiento sepa qué modelo utilizar.

   ```sql
   EXECUTE predict_species 'Naive Bayes';
   GO
   ```

   Al ejecutar el procedimiento almacenado, devuelve un marco Data. Frame de Python. Esta línea de T-SQL especifica el esquema de los resultados devueltos: `WITH RESULT SETS ( ("id" int, "SpeciesId" int, "SpeciesId.Predicted" int));`. Puede insertar los resultados en una tabla nueva o devolverlos a una aplicación.

   ![Conjunto de resultados de ejecutar procedimiento almacenado](media/train-score-using-python-NB-model-results.png)

   Los resultados son las predicciones 150 sobre las especies que usan características floral como entradas. Para la mayoría de las observaciones, la especie de predicción coincide con la especie real.

   Este ejemplo se ha simplificado mediante el uso del conjunto de resultados de iris de Python para entrenamiento y puntuación. Un enfoque más típico implicaría la ejecución de una consulta SQL para obtener los datos nuevos y pasarlo a Python como `InputDataSet`.

## <a name="conclusion"></a>Conclusión

En este ejercicio, aprendió a crear procedimientos almacenados dedicados a diferentes tareas, donde cada procedimiento almacenado usaba el procedimiento almacenado del sistema `sp_execute_external_script` para iniciar un proceso de Python. Las entradas del proceso de Python se pasan a `sp_execute_external` como parámetros. El propio script de Python y las variables de datos en una base de datos de SQL Server se pasan como entradas.

Por lo general, solo debe planear el uso de SSMS con código Python pulido, o código de Python sencillo que devuelve la salida basada en filas. Como herramienta, SSMS admite lenguajes de consulta como T-SQL y devuelve conjuntos de filas planas. Si el código genera una salida visual como un dispersión o histograma, necesita una herramienta o una aplicación de usuario final que pueda representar la imagen.

En el caso de algunos desarrolladores de Python que se usan para escribir scripts inclusivos de un intervalo de operaciones, la organización de tareas en procedimientos independientes podría parecer innecesaria. Pero el entrenamiento y la puntuación tienen diferentes casos de uso. Al separarlos, puede colocar cada tarea en una programación diferente y permisos de ámbito para cada operación.

Del mismo modo, también puede aprovechar las características de reabastecimiento de SQL Server, como el procesamiento en paralelo, el gobierno de recursos o la escritura de un script para usar algoritmos en [microsoftml](../python/ref-py-microsoftml.md) que admita la transmisión por secuencias y la ejecución en paralelo. Al separar el entrenamiento y la puntuación, puede dirigirse a las optimizaciones para cargas de trabajo específicas.

Una ventaja final es que los procesos se pueden modificar mediante parámetros. En este ejercicio, el código de Python que creó el modelo (denominado "Bayes naive" en este ejemplo) se pasó como una entrada a un segundo procedimiento almacenado que llama al modelo en un proceso de puntuación. En este ejercicio solo se usa un modelo, pero puede imaginarse cómo la parametrización del modelo en una tarea de puntuación haría que ese script sea más útil.

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información acerca de SQL Server Machine Learning Services, consulte:

- [¿Qué es SQL Server Machine Learning Services (Python y R)?](../what-is-sql-server-machine-learning.md)
