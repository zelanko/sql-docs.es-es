---
title: 'Inicio rápido: Ejecución de scripts de Python'
description: Ejecute un conjunto de scripts de Python sencillos con SQL Server Machine Learning Services. Obtenga información sobre cómo usar el procedimiento almacenado sp_execute_external_script para ejecutar el script en una instancia de SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 01/27/2020
ms.topic: quickstart
author: garyericson
ms.author: garye
ms.reviewer: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 1ae25eeb4890057074f78ec6a62c251cd097e22e
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2020
ms.locfileid: "81487404"
---
# <a name="quickstart-run-simple-python-scripts-with-sql-server-machine-learning-services"></a>Inicio rápido: Ejecución de scripts de Python sencillos con SQL Server Machine Learning Services
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

En este inicio rápido, ejecutará un conjunto de scripts de Python sencillos mediante [SQL Server Machine Learning Services](../sql-server-machine-learning-services.md). Aprenderá a usar el procedimiento almacenado [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) para ejecutar el script en una instancia de SQL Server.

## <a name="prerequisites"></a>Prerrequisitos

- Para este inicio rápido, es necesario tener acceso a una instancia de SQL Server con [SQL Server Machine Learning Services](../install/sql-machine-learning-services-windows-install.md) que tenga instalado el lenguaje de Python.

- También necesita una herramienta para ejecutar consultas SQL que contengan scripts de Python. Puede ejecutar estos scripts con cualquier herramienta de consultas o administración de bases de datos, siempre que pueda conectarse a una instancia de SQL Server y ejecutar una consulta T-SQL o un procedimiento almacenado. En este inicio rápido, se usa [SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/sql-server-management-studio-ssms).

## <a name="run-a-simple-script"></a>Ejecución de un script sencillo

Para ejecutar un script de Python, necesita pasarlo como argumento al procedimiento almacenado del sistema, [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md).
Este procedimiento almacenado del sistema inicia el entorno de ejecución de Python en el contexto de SQL Server, pasa datos a Python, administra de forma segura las sesiones de usuario de Python y devuelve los resultados al cliente.

En los pasos siguientes, ejecutará este script de Python de ejemplo en su instancia de SQL Server:

```python
a = 1
b = 2
c = a/b
d = a*b
print(c, d)
```

1. Abra una nueva ventana de consulta en **SQL Server Management Studio** conectada a su instancia de SQL Server.

1. Pase todo el script de Python al procedimiento almacenado `sp_execute_external_script`.

   El script se pasa mediante el argumento `@script`. Todo lo que contenga el argumento `@script` tiene que ser código de Python válido.

    ```sql
    EXECUTE sp_execute_external_script @language = N'Python'
        , @script = N'
    a = 1
    b = 2
    c = a/b
    d = a*b
    print(c, d)
    '
    ```

1. Se calcula el resultado correcto y la función `print` de Python devuelve el resultado a la ventana **Mensajes**.

   Necesita tener el siguiente aspecto.

    **Resultados**

    ```text
    STDOUT message(s) from external script:
    0.5 2
    ```

## <a name="run-a-hello-world-script"></a>Ejecución de un script Hola mundo

Un script de ejemplo típico es uno que simplemente muestra la cadena "Hola mundo". Ejecute el siguiente comando:

```sql
EXECUTE sp_execute_external_script @language = N'Python'
    , @script = N'OutputDataSet = InputDataSet'
    , @input_data_1 = N'SELECT 1 AS hello'
WITH RESULT SETS(([Hello World] INT));
GO
```

Entre las entradas para el procedimiento almacenado `sp_execute_external_script`, se incluyen las siguientes:

| | |
|-|-|
| @language | define la extensión del lenguaje de la llamada (en este caso, Python). |
| @script | define los comandos que se pasarán al entorno de ejecución de Python.<br>Es necesario incluir todo el script de Python en este argumento como texto Unicode. También puede agregar texto a una variable del tipo **nvarchar** y, después, llamar a la variable. |
| @input_data_1 | datos devueltos por la consulta, pasados al entorno de ejecución de Python, que devuelven los datos a SQL Server como una trama de datos. |
|WITH RESULT SETS | cláusula que define el esquema de la tabla de datos devuelta de SQL Server (en este caso, se agrega "Hola mundo" como el nombre de columna e **int** para el tipo de datos). |

El comando muestra el texto siguiente:

| Hola mundo |
|-------------|
| 1 |

## <a name="use-inputs-and-outputs"></a>Uso de entradas y salidas

De forma predeterminada, `sp_execute_external_script` acepta un único conjunto de datos como entrada, que se suele proporcionar como una consulta SQL válida. Después, devuelve una única trama de datos de Python como salida.

Por ahora, usaremos las variables de entrada y salida predeterminadas de `sp_execute_external_script`: **InputDataSet** y **OutputDataSet**.

1. Cree una tabla pequeña con datos de prueba.

    ```sql
    CREATE TABLE PythonTestData (col1 INT NOT NULL)
    
    INSERT INTO PythonTestData
    VALUES (1);
    
    INSERT INTO PythonTestData
    VALUES (10);
    
    INSERT INTO PythonTestData
    VALUES (100);
    GO
    ```

1. Use la instrucción `SELECT` para consultar la tabla.
  
    ```sql
    SELECT *
    FROM PythonTestData
    ```

    **Resultados**

    ![Contenido de la tabla PythonTestData](./media/select-pythontestdata.png)

1. Ejecute el siguiente script de Python. Recupera los datos de la tabla mediante la instrucción `SELECT`, los pasa mediante el entorno de ejecución de Python y devuelve los datos como una trama de datos. La cláusula `WITH RESULT SETS` define el esquema de la tabla de datos devuelta para SQL y agrega el nombre de columna *NewColName*.

    ```sql
    EXECUTE sp_execute_external_script @language = N'Python'
        , @script = N'OutputDataSet = InputDataSet;'
        , @input_data_1 = N'SELECT * FROM PythonTestData;'
    WITH RESULT SETS(([NewColName] INT NOT NULL));
    ```

    **Resultados**

    ![Salida del script de Python que devuelve datos de una tabla](./media/python-output-pythontestdata.png)

1. Ahora, cambie los nombres de las variables de entrada y salida. Los nombres predeterminados de las variables de entrada y salida son **InputDataSet** y **OutputDataSet**; el script siguiente cambia los nombres a **SQL_in** y **SQL_out**:

    ```sql
    EXECUTE sp_execute_external_script @language = N'Python'
        , @script = N'SQL_out = SQL_in;'
        , @input_data_1 = N'SELECT 12 as Col;'
        , @input_data_1_name  = N'SQL_in'
        , @output_data_1_name = N'SQL_out'
    WITH RESULT SETS(([NewColName] INT NOT NULL));
    ```

    Tenga en cuenta que Python distingue mayúsculas de minúsculas. Las variables de entrada y salida usadas en el script de Python (**SQL_out** y **SQL_in**) tienen que coincidir con los nombres definidos con `@input_data_1_name` y `@output_data_1_name`, incluido el uso de mayúsculas.

   > [!TIP]
   > Solo se puede pasar un conjunto de datos de entrada como parámetro, y solo se puede devolver un conjunto de datos. Pero puede llamar a otros conjuntos de datos desde dentro del código de Python y devolver salidas de otros tipos, además del conjunto de datos. También puede agregar la palabra clave OUTPUT a cualquier parámetro para que se devuelva con los resultados.

1. También puede generar valores con el script de Python sin datos de entrada (`@input_data_1` se establece en blanco).

   El script siguiente genera el texto "hola" y "mundo".

   ```sql
   EXECUTE sp_execute_external_script @language = N'Python'
       , @script = N'
   import pandas as pd
   mytextvariable = pandas.Series(["hello", " ", "world"]);
   OutputDataSet = pd.DataFrame(mytextvariable);
   '
       , @input_data_1 = N''
   WITH RESULT SETS(([Col1] CHAR(20) NOT NULL));
   ```

   **Resultados**

   ![Resultados de consultas con @script como entrada](./media/python-data-generated-output.png)

> [!NOTE]
> Python usa espacios iniciales para agrupar instrucciones. Por lo tanto, cuando el script de Python insertado abarca varias líneas, como en el script anterior, no intente agregar sangría a los comandos de Python para que estén alineados con los comandos de SQL. Por ejemplo, este script produciría un error:

  ```text
  EXECUTE sp_execute_external_script @language = N'Python'
      , @script = N'
      import pandas as pd
      mytextvariable = pandas.Series(["hello", " ", "world"]);
      OutputDataSet = pd.DataFrame(mytextvariable);
      '
      , @input_data_1 = N''
  WITH RESULT SETS(([Col1] CHAR(20) NOT NULL));
  ```

## <a name="check-python-version"></a>Comprobación de la versión de Python

Si quiere ver qué versión de Python está instalada en su instancia de SQL Server, ejecute el script siguiente.

```sql
EXECUTE sp_execute_external_script @language = N'Python'
    , @script = N'
import sys
print(sys.version)
'
GO
```

La función `print` de Python devuelve la versión en la ventana **Mensajes**. En la salida de ejemplo siguiente, puede ver que, en este caso, la versión de Python instalada es 3.5.2.

**Resultados**

```text
STDOUT message(s) from external script: 
3.5.2 |Continuum Analytics, Inc.| (default, Jul  5 2016, 11:41:13) [MSC v.1900 64 bit (AMD64)]
```

## <a name="list-python-packages"></a>Lista de paquetes de Python

Microsoft proporciona varios paquetes de Python preinstalados con SQL Server Machine Learning Services en su instancia de SQL Server.

Para ver una lista de los paquetes de Python instalados, incluida la versión, ejecute el script siguiente.

```SQL
EXECUTE sp_execute_external_script @language = N'Python'
    , @script = N'
import pkg_resources
import pandas
dists = [str(d) for d in pkg_resources.working_set]
OutputDataSet = pandas.DataFrame(dists)
'
WITH RESULT SETS(([Package] NVARCHAR(max)))
GO
```

La lista es de `pkg_resources.working_set` en Python y se devuelve a SQL como una trama de datos.

**Resultados**

:::image type="content" source="media/python-package-list.png" alt-text="Visualización de los paquetes de Python instalados":::

## <a name="next-steps"></a>Pasos siguientes

Para obtener información sobre cómo usar estructuras de datos al usar Python en SQL Server Machine Learning Services, siga este inicio rápido:

> [!div class="nextstepaction"]
> [Inicio rápido: estructuras de datos y objetos mediante Python en SQL Server Machine Learning Services](quickstart-python-data-structures.md)

Para más información sobre cómo usar Python en SQL Server Machine Learning Services, vea los artículos siguientes:

- [Creación de funciones avanzadas de Python con SQL Server Machine Learning Services](quickstart-python-functions.md)
- [Creación y puntuación de un modelo predictivo en Python con SQL Server Machine Learning Services](quickstart-python-train-score-model.md)
- [¿Qué es SQL Server Machine Learning Services (Python y R)?](../sql-server-machine-learning-services.md)
