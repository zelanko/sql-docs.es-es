---
title: Conjunto de datos de demostración de iris para tutoriales de Python y R
Description: Cree una base de datos que contenga el conjunto de datos de iris y una tabla para almacenar los modelos. Este conjunto de DataSet se usa en ejercicios que muestran cómo ajustar el lenguaje R o el código Python en un SQL Server procedimiento almacenado.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/19/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 78acdd0ef2eed808d8f974c38899282dc823436d
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/01/2019
ms.locfileid: "68715499"
---
#  <a name="iris-demo-data-for-python-and-r-tutorials-in-sql-server"></a>Datos de demostración de iris para tutoriales de Python y R en SQL Server 
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

En este ejercicio, cree una base de datos de SQL Server para almacenar los datos del conjunto de datos y los modelos de [flores de iris](https://en.wikipedia.org/wiki/Iris_flower_data_set) basados en los mismos datos. Los datos de iris se incluyen en las distribuciones de R y Python instaladas por SQL Server y se usan en los tutoriales de aprendizaje automático de SQL Server. 

Para completar este ejercicio, debe tener [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms?view=sql-server-2017) u otra herramienta que pueda ejecutar consultas de T-SQL.

Entre los tutoriales y las guías de inicio rápido que usan este conjunto de datos se incluyen los siguientes:

+  [Inicio rápido: Crear, entrenar y usar un modelo de Python con procedimientos almacenados en SQL Server](quickstart-python-train-score-in-tsql.md)

## <a name="create-the-database"></a>Crear la base de datos

1. Inicie SQL Server Management Studio y abra una nueva ventana de **consulta** .  

2. Cree una nueva base de datos para este proyecto y cambie el contexto de la ventana de **consulta** para usar la nueva base de datos.

    ```sql
    CREATE DATABASE irissql
    GO
    USE irissql
    GO
    ```

    > [!TIP] 
    > Si no está familiarizado con SQL Server, o si está trabajando en un servidor de su propiedad, un error común es iniciar sesión y empezar a trabajar sin advertir de que está en la base de datos **maestra** . Para asegurarse de que está usando la base de datos correcta, especifique siempre el contexto mediante `USE <database name>` la instrucción (por ejemplo `use irissql`,).

3. Agregue algunas tablas vacías: una para almacenar los datos y otra para almacenar los modelos entrenados. La tabla **iris_models** se usa para almacenar modelos serializados generados en otros ejercicios.

    En el código siguiente se crea la tabla para los datos de entrenamiento.

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
    > Si no está familiarizado con T-SQL, se merece la pena memorizar la `DROP...IF` instrucción. Al intentar crear una tabla y ya existe una, SQL Server devuelve un error: "Ya hay un objeto denominado" iris_data "en la base de datos". Una manera de evitar estos errores es eliminar las tablas existentes u otros objetos como parte del código.

4. Ejecute el código siguiente para crear la tabla utilizada para almacenar el modelo entrenado. Para guardar los modelos de Python (o R) en SQL Server, se deben serializar y almacenar en una columna de tipo **varbinary (Max)** . 

    ```sql
    DROP TABLE IF EXISTS iris_models;
    GO
    
    CREATE TABLE iris_models (
      model_name VARCHAR(50) NOT NULL DEFAULT('default model') PRIMARY KEY,
      model VARBINARY(MAX) NOT NULL
    );
    GO
    ```

    Además del contenido del modelo, normalmente también se agregan columnas para otros metadatos útiles, como el nombre del modelo, la fecha en que se entrenó, el algoritmo y los parámetros de origen, los datos de origen, etc. Por ahora, lo haremos sencillo y usaremos solo el nombre del modelo.

## <a name="populate-the-table"></a>Rellenar la tabla

Puede obtener datos de iris integrados de R o Python. Puede usar Python o R para cargar los datos en una trama de datos y, a continuación, insertarlos en una tabla de la base de datos. Mover los datos de entrenamiento de una sesión externa a una tabla SQL Server es un proceso de varios pasos:

+ Diseñe un procedimiento almacenado que obtenga los datos deseados.
+ Ejecute el procedimiento almacenado para obtener realmente los datos.
+ Construya una instrucción INSERT para especificar dónde deben guardarse los datos recuperados.

1. En sistemas con integración de Python, cree el siguiente procedimiento almacenado que utiliza el código de Python para cargar los datos.

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

    Al ejecutar este código, debería obtener el mensaje "comandos completados correctamente". Todo esto significa que el procedimiento almacenado se ha creado según sus especificaciones.

2. Como alternativa, en los sistemas que tienen integración con R, cree un procedimiento que use R en su lugar.

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

3. Para rellenar realmente la tabla, ejecute el procedimiento almacenado y especifique la tabla en la que se deben escribir los datos. Cuando se ejecuta, el procedimiento almacenado ejecuta el código de Python o R, que carga el conjunto de datos de iris integrado y, a continuación, inserta los datos en la tabla **iris_data** .

    ```sql
    INSERT INTO iris_data ("Sepal.Length", "Sepal.Width", "Petal.Length", "Petal.Width", "Species", "SpeciesId")
    EXEC dbo.get_iris_dataset;
    ```

    Si no está familiarizado con T-SQL, tenga en cuenta que la instrucción INSERT solo agrega nuevos datos. no comprobará si hay datos existentes o eliminará y reconstruirá la tabla. Para evitar la obtención de varias copias de los mismos datos en una tabla, puede ejecutar esta instrucción primero `TRUNCATE TABLE iris_data`:. La instrucción [TRUNCATE TABLE](https://docs.microsoft.com/sql/t-sql/statements/truncate-table-transact-sql) de T-SQL elimina los datos existentes, pero mantiene intacta la estructura de la tabla.

    > [!TIP]
    > Para modificar el procedimiento almacenado más adelante, no es necesario quitarlo y volver a crearlo. Use la instrucción [ALTER PROCEDURE](https://docs.microsoft.com/sql/t-sql/statements/alter-procedure-transact-sql) . 


## <a name="query-the-data"></a>Consultar los datos

Como paso de validación, ejecute una consulta para confirmar que se cargaron los datos.

1. En Explorador de objetos, en bases de datos, haga clic con el botón secundario en la base de datos **irissql** e inicie una nueva consulta.

2. Ejecute algunas consultas sencillas:

    ```sql
    SELECT TOP(10) * FROM iris_data;
    SELECT COUNT(*) FROM iris_data;
    ```

## <a name="next-steps"></a>Pasos siguientes

En la guía de inicio rápido siguiente, creará un modelo de aprendizaje automático y lo guardará en una tabla y, a continuación, usará el modelo para generar los resultados previstos.

+ [Inicio rápido: Crear, entrenar y usar un modelo de Python con procedimientos almacenados en SQL Server](quickstart-python-train-score-in-tsql.md)
