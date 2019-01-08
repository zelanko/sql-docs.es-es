---
title: Conjunto de datos de iris demostración de tutoriales de Python y R, SQL Server Machine Learning
Description: Create a database containing the Iris dataset and a table for storing models. This dataset is used in exercises showing how to wrap R language or Python code in a SQL Server stored procedure.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/19/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: ce0469b5625af3f38047233737f3afbd209e11b9
ms.sourcegitcommit: baca29731a1be4f8fa47567888278394966e2af7
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/04/2019
ms.locfileid: "54046575"
---
#  <a name="iris-demo-data-for-python-and-r-tutorials-in-sql-server"></a>Datos de iris la demostración de tutoriales de Python y R en SQL Server 
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

En este ejercicio, creará una base de datos de SQL Server para almacenar los datos de la [conjunto de datos Iris](https://en.wikipedia.org/wiki/Iris_flower_data_set) y modelos basados en los mismos datos. Datos de iris se incluyen en las distribuciones de R y Python instaladas con SQL Server y se usan en los tutoriales sobre aprendizaje automático de SQL Server. 

Para completar este ejercicio, debe tener [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms?view=sql-server-2017) u otra herramienta que puede ejecutar consultas de T-SQL.

Tutoriales y guías de inicio rápido con este conjunto de datos incluyen lo siguiente:

+  [Inicio rápido: Crear, entrenar y usar un modelo de Python con procedimientos almacenados en SQL Server](quickstart-python-train-score-in-tsql.md)

## <a name="create-the-database"></a>Crear la base de datos

1. Inicie SQL Server Management Studio y abra una nueva **consulta** ventana.  

2. Crear una nueva base de datos para este proyecto y cambiar el contexto de su **consulta** ventana para utilizar la nueva base de datos.

    ```sql
    CREATE DATABASE irissql
    GO
    USE irissql
    GO
    ```

    > [!TIP] 
    > Si está familiarizado con SQL Server, o si está trabajando en un servidor que posee, un error común es iniciar sesión y empezar a trabajar sin advertir que se encuentra el **maestro** base de datos. Para asegurarse de que está usando la base de datos, especifique siempre el contexto mediante la `USE <database name>` instrucción (por ejemplo, `use irissql`).

3. Agregue algunas tablas vacías: uno para almacenar los datos y otro para almacenar los modelos entrenados. El **iris_models** tabla se utiliza para almacenar los modelos serializados generados en otros ejercicios.

    El código siguiente crea la tabla para los datos de entrenamiento.

    ```sql
    DROP TABLE IF EXISTS iris_data;
    GO
    CREATE TABLE iris_data (
      id INT NOT NULL IDENTITY PRIMARY KEY
      , "Sepal.Length" FLOAT NOT NULL, "Sepal.Width" FLOAT NOT NULL
      , "Petal.Length" FLOAT NOT NULL, "Petal.Width" FLOAT NOT NULL
      , "Species" VARCHAR(100) NOT NULL, "SpeciesId" INT NOT NULL
    );
    ```

    > [!TIP] 
    > Si está familiarizado con Transact-SQL, vale la pena memorizar los `DROP...IF` instrucción. Al intentar crear una tabla y ya existe uno, SQL Server devuelve un error: "Ya hay un objeto denominado 'iris_data' en la base de datos." Una manera de evitar estos errores es eliminar las tablas existentes u otros objetos como parte del código.

4. Ejecute el código siguiente para crear la tabla utilizada para almacenar el modelo entrenado. Para guardar los modelos de Python (o R) en SQL Server, debe ser serializados y almacenados en una columna de tipo **varbinary (max)**. 

    ```sql
    DROP TABLE IF EXISTS iris_models;
    GO
    
    CREATE TABLE iris_models (
      model_name VARCHAR(50) NOT NULL DEFAULT('default model') PRIMARY KEY,
      model VARBINARY(MAX) NOT NULL
    );
    GO
    ```

    Además del contenido del modelo, por lo general, podría también agregar columnas para otros metadatos útiles, como el nombre del modelo, la fecha en que se ha entrenado, el algoritmo de código fuente y los parámetros, los datos de origen y así sucesivamente. Por ahora se mantendrán simple y usar el nombre del modelo.

## <a name="populate-the-table"></a>Rellene la tabla

Puede obtener datos de Iris integrados de R o Python. Puede usar Python o R para cargar los datos en una trama de datos y, a continuación, insertarlo en una tabla en la base de datos. Mover datos de entrenamiento desde una sesión externa a una tabla de SQL Server es un proceso de varios pasos:

+ Diseñe un procedimiento almacenado que obtiene los datos que desee.
+ Ejecute el procedimiento almacenado para obtener los datos realmente.
+ Construir una instrucción INSERT para especificar dónde se deben guardar los datos recuperados.

1. En los sistemas con la integración de Python, cree el siguiente procedimiento almacenado que utiliza el código de Python para cargar los datos.

    ```sql
    CREATE PROCEDURE get_iris_dataset
    AS
    BEGIN
    EXEC sp_execute_external_script @language = N'Python', 
    @script = N'
    from sklearn import datasets
    iris = datasets.load_iris()
    iris_data = pandas.DataFrame(iris.data)
    iris_data["Species"] = pandas.Categorical.from_codes(iris.target, iris.target_names)
    iris_data["SpeciesId"] = iris.target
    ', 
    @input_data_1 = N'', 
    @output_data_1_name = N'iris_data'
    WITH RESULT SETS (("Sepal.Length" float not null, "Sepal.Width" float not null, "Petal.Length" float not null, "Petal.Width" float not null, "Species" varchar(100) not null, "SpeciesId" int not null));
    END;
    GO
    ```

    Al ejecutar este código, debe obtener el mensaje "Comandos completados correctamente." Todo esto significa es que el procedimiento almacenado se ha creado según sus especificaciones.

2. Como alternativa, en los sistemas que tienen integración de R, cree un procedimiento que usa R en su lugar.

    ```sql
    CREATE PROCEDURE get_iris_dataset
    AS
    BEGIN
    EXEC sp_execute_external_script @language = N'R', 
    @script = N'
    library(RevoScaleR)
    data(iris)
    iris$SpeciesID <- c(unclass(iris$Species))
    iris_data <- iris
    ', 
    @input_data_1 = N'', 
    @output_data_1_name = N'iris_data'
    WITH RESULT SETS (("Sepal.Length" float not null, "Sepal.Width" float not null, "Petal.Length" float not null, "Petal.Width" float not null, "Species" varchar(100) not null, "SpeciesId" int not null));
    END;
    GO
    ```

3. Para rellenar realmente en la tabla, ejecute el procedimiento almacenado y especifique la tabla donde se deben escribir los datos. Cuando se ejecuta, el procedimiento almacenado ejecuta el código Python o R, que carga el conjunto de datos de Iris integrado y, a continuación, inserta los datos en el **iris_data** tabla.

    ```sql
    INSERT INTO iris_data ("Sepal.Length", "Sepal.Width", "Petal.Length", "Petal.Width", "Species", "SpeciesId")
    EXEC dbo.get_iris_dataset;
    ```

    Si está familiarizado con T-SQL, tenga en cuenta que la instrucción INSERT solo agrega nuevos datos; No comprobar datos existentes, o eliminar y volver a generar la tabla. Para evitar varias copias de los mismos datos en una tabla, puede ejecutar esta instrucción primero: `TRUNCATE TABLE iris_data`. El código T_SQL [TRUNCATE TABLE](https://docs.microsoft.com/sql/t-sql/statements/truncate-table-transact-sql) instrucción elimina los datos existentes, pero mantiene intacta la estructura de la tabla.

    > [!TIP]
    > Más adelante, para modificar el procedimiento almacenado no debe quitar y volver a crearla. Use la [ALTER PROCEDURE](https://docs.microsoft.com/sql/t-sql/statements/alter-procedure-transact-sql) instrucción. 


## <a name="query-the-data"></a>Consultar los datos

Como paso de validación, ejecute una consulta para confirmar que se han cargado los datos.

1. En el Explorador de objetos, en las bases de datos, haga clic en el **irissql** , inicie una nueva consulta y base de datos.

2. Ejecute algunas consultas sencillas:

    ```sql
    SELECT TOP(10) * FROM iris_data;
    SELECT COUNT(*) FROM iris_data;
    ```

## <a name="next-steps"></a>Pasos siguientes

En el siguiente inicio rápido, creará un modelo de aprendizaje automático y guardarlo en una tabla y, a continuación, usar el modelo para generar resultados.

+ [Inicio rápido: Crear, entrenar y usar un modelo de Python con procedimientos almacenados en SQL Server](quickstart-python-train-score-in-tsql.md)
