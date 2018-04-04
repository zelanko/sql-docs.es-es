---
title: Incluir código Python en un procedimiento almacenado | Documentos de Microsoft
titleSuffix: SQL Server
ms.custom: ''
ms.date: 02/28/2018
ms.reviewer: ''
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: ''
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: tutorial
applies_to:
- SQL Server 2017
dev_langs:
- Python
ms.author: heidist
author: HeidiSteen
manager: cgronlun
ms.openlocfilehash: fa802c2ae213168d7b6d16cecbfad2eb540dce66
ms.sourcegitcommit: 059fc64ba858ea2adaad2db39f306a8bff9649c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/04/2018
---
# <a name="wrap-python-code-in-a-stored-procedure"></a>Incluir código Python en un procedimiento almacenado
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

En un [lección anterior](run-python-using-t-sql.md), ha aprendido cómo hacer Python hablar con SQL Server. En esta lección, aprenderá cómo incrustar código Python en un procedimiento almacenado para obtener datos de los conjuntos de datos de ejemplo de Python y escribir datos en una tabla de SQL Server.

Procedimiento almacenado del sistema [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) proporciona el contenedor que entren Python en variables de SQL y conjuntos de datos SQL. También controla la salida de resultados por Python y pasa a SQL Server en un formato compatible con los tipos de datos SQL.

Veamos cómo funciona.

## <a name="prepare-the-database-and-tables"></a>Preparar la base de datos y tablas

Aunque es posible configurar un cliente remoto y ejecutar código de Python mediante código de Visual Studio, Visual Studio, PyCharm u otras herramientas, para simplificar el escenario, todo el código en esta lección se debe ejecutar como parte de un procedimiento almacenado.

1. Inicie SQL Server Management Studio y abra una nueva **consulta** ventana.  

2. Crear una nueva base de datos para este proyecto y cambiar el contexto de su **consulta** ventana para usar la nueva base de datos.

    ```sql
    CREATE DATABASE sqlpy;
    GO;
    USE sqlpy;
    GO;
    ```

    > [!TIP] 
    > Si está familiarizado con SQL Server, o si está trabajando en un servidor que usted es el propietario, un error común es iniciar sesión y empezar a trabajar sin advertir que están en el **maestro** base de datos. Para asegurarse de que está usando la base de datos, especifique siempre el contexto mediante la `USE <database name>` instrucción.

3. Agregar algunas tablas vacías: uno para almacenar los datos y otro para almacenar los modelos de entrenamiento. Más adelante rellena las tablas con Python.

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

    Si está familiarizado con T-SQL, vale la pena memorizar los `DROP...IF` instrucción. Cuando se intenta crear una tabla y ya existe una, SQL Server devuelve un error: "Ya hay un objeto denominado 'iris_data' en la base de datos." Una manera de evitar tales errores consiste en eliminar las tablas existentes u otros objetos como parte del código.

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

    Además del contenido del modelo, por lo general, también podría agregar columnas para otros metadatos útil, por ejemplo, el nombre del modelo, la fecha en que se ha entrenado, el algoritmo de origen y los parámetros, datos de origen y así sucesivamente. Por ahora comenzaremos por simplificar y usar simplemente el nombre del modelo.

## <a name="populate-the-table"></a>Rellene la tabla

Para mover los datos de entrenamiento de Python en un servidor SQL Server tabla es un proceso de varios pasos:

+ Diseñar un procedimiento almacenado que obtenga los datos que desea.
+ Ejecute el procedimiento almacenado para obtener los datos realmente.
+ Utilice una instrucción INSERT para especificar dónde se deben guardar los datos recuperados.

1. Cree el siguiente procedimiento almacenado que incluye código de Python. 

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

    Cuando se ejecuta este código, debe obtener el mensaje "Comandos completados correctamente." Todo esto significa que es que el procedimiento almacenado se ha creado según sus especificaciones.

2. Para rellenar realmente en la tabla, ejecute el procedimiento almacenado y especificar la tabla donde se deben escribir los datos. Cuando se ejecuta, el procedimiento almacenado ejecuta el código Python, que carga el conjunto de datos de Iris desde los datos de ejemplo de Python integrados.

    ```sql
    INSERT INTO iris_data ("Sepal.Length", "Sepal.Width", "Petal.Length", "Petal.Width", "Species", "SpeciesId")
    EXEC dbo.get_iris_dataset;
    ```

    Si está familiarizado con T-SQL, tenga en cuenta que la instrucción INSERT solo agrega nuevos datos; No comprobar datos existentes, o eliminar y volver a generar la tabla. Para evitar obtener varias copias de los mismos datos en una tabla, puede ejecutar esta instrucción en primer lugar: `TRUNCATE TABLE iris_data`. El código T-SQL [TRUNCATE TABLE](https://docs.microsoft.com/sql/t-sql/statements/truncate-table-transact-sql) instrucción elimina los datos existentes, pero mantiene intacta la estructura de la tabla.

    > [!TIP]
    > Para modificar el procedimiento almacenado más adelante, no debe quitar y volver a crearlo. Use la [ALTER PROCEDURE](https://docs.microsoft.com/sql/t-sql/statements/alter-procedure-transact-sql) instrucción. 

3. Para comprobar que los datos se ha cargado correctamente, puede ejecutar algunas consultas sencillas:

    ```sql
    SELECT TOP(10) * FROM iris_data;
    SELECT COUNT(*) FROM iris_data;
    ```

En el [siguiente lección](../tutorials/train-score-using-python-in-tsql.md), crear un modelo de aprendizaje automático y guardarlo en una tabla.

### <a name="further-reading-about-stored-procedures"></a>Obtener más información sobre los procedimientos almacenados

Si está familiarizado con SQL Server, puede ser complicados al principio los procedimientos almacenados. Pero un procedimiento almacenado es una interfaz eficaz y flexible para pasar datos entre aplicaciones y el servidor. Mediante el uso de un procedimiento almacenado, se pueden definir de forma dinámica entradas, que resulta muy sencillo pasar en nuevos nombres de modelo, los nuevos parámetros y los nuevos datos, sin modificar el código Python.

Para obtener información general de almacenado cómo funcionan los procedimientos, consulte [procedimientos almacenados (motor de base de datos)](https://docs.microsoft.com/sql/relational-databases/stored-procedures/stored-procedures-database-engine), o este tutorial: [escribir instrucciones de Transact-SQL](https://docs.microsoft.com/sql/t-sql/tutorial-writing-transact-sql-statements).

También hay algunos buenos tutoriales en sitios de comunidades como [Central de SQL Server](http://www.sqlservercentral.com/) o [equipo SQL](http://www.sqlteam.com/).

Como pensar en cómo se puede encapsular mejor código Python en T-SQL, considere también el uso de estas características:

+ Definir valores predeterminados para el procedimiento almacenado
+ Uso de la palabra clave OUTPUT para pasar a través de las variables de entrada
+ Crear definiciones de esquema mediante con resultados para asegurarse de que los datos usados por aplicaciones tiene los tipos de datos correctos y los nombres de columna
+ Proporciona sugerencias para mejorar el procesamiento por lotes
+ Suplantación de un usuario diferente para probar el código, usar EXECUTE AS cláusula

## <a name="next-lesson"></a>Lección siguiente

[Entrenar un modelo de Python y generar puntuaciones en SQL Server](../tutorials/train-score-using-python-in-tsql.md)