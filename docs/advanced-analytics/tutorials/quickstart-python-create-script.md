---
title: Creación y ejecución de scripts de Python simples
titleSuffix: SQL Server Machine Learning Services
description: Cree y ejecute scripts de Python simples en una instancia de SQL Server con SQL Server Machine Learning Services.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/04/2019
ms.topic: quickstart
author: garyericson
ms.author: garye
ms.reviewer: davidph
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: ecf99f1ae70cf44b32955ae164dbe3017bdf5f24
ms.sourcegitcommit: 454270de64347db917ebe41c081128bd17194d73
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/07/2019
ms.locfileid: "72006119"
---
# <a name="quickstart-create-and-run-simple-python-scripts-with-sql-server-machine-learning-services"></a>Inicio rápido: Crear y ejecutar scripts de Python simples con SQL Server Machine Learning Services
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

En esta guía de inicio rápido, creará y ejecutará un conjunto de scripts de Python sencillos mediante [SQL Server Machine Learning Services](../what-is-sql-server-machine-learning.md). Aprenderá a ajustar un script de Python con el formato correcto en el procedimiento almacenado [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) y a ejecutar el script en una instancia de SQL Server.

## <a name="prerequisites"></a>Requisitos previos

- Esta guía de inicio rápido requiere acceso a una instancia de SQL Server con [SQL Server Machine Learning Services](../install/sql-machine-learning-services-windows-install.md) con el idioma de Python instalado.

- También necesita una herramienta para ejecutar consultas SQL que contienen scripts de Python. Puede ejecutar estos scripts mediante cualquier herramienta de consulta o administración de bases de datos, siempre que pueda conectarse a una instancia de SQL Server y ejecutar una consulta T-SQL o un procedimiento almacenado. Esta guía de inicio rápido usa [SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/sql-server-management-studio-ssms).

## <a name="run-a-simple-script"></a>Ejecutar un script simple

Para ejecutar un script de Python, lo pasará como argumento al procedimiento almacenado del sistema, [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md).
Este procedimiento almacenado del sistema inicia el tiempo de ejecución de Python en el contexto de SQL Server, pasa datos a Python, administra las sesiones de usuario de Python de forma segura y devuelve los resultados al cliente.

En los pasos siguientes, ejecutará este script de Python de ejemplo en la instancia de SQL Server:

```python
a = 1
b = 2
c = a/b
d = a*b
print(c, d)
```

1. Abra una nueva ventana de consulta en **SQL Server Management Studio** conectado a la instancia de SQL Server.

1. Pase el script de Python completo al procedimiento almacenado `sp_execute_external_script`.

   El script se pasa a través del argumento `@script`. Todo lo que se encuentra dentro del argumento `@script` debe ser código Python válido.

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

1. Se calcula el resultado correcto y la función `print` de Python devuelve el resultado a la ventana **mensajes** .

   Debe tener un aspecto similar al siguiente.

    **Resultado**

    ```text
    STDOUT message(s) from external script:
    0.5 2
    ```

## <a name="run-a-hello-world-script"></a>Ejecutar un script de Hola mundo

Un script de ejemplo típico es aquél que simplemente genera la cadena "Hola mundo". Ejecute el siguiente comando:

```sql
EXECUTE sp_execute_external_script @language = N'Python'
    , @script = N'OutputDataSet = InputDataSet'
    , @input_data_1 = N'SELECT 1 AS hello'
WITH RESULT SETS(([Hello World] INT));
GO
```

Las entradas del procedimiento almacenado `sp_execute_external_script` incluyen:

| | |
|-|-|
| @language | define la extensión del lenguaje para llamar, en este caso, Python |
| @script | define los comandos que se pasan al tiempo de ejecución de Python<br>Todo el script de Python debe incluirse en este argumento, como texto Unicode. También puede Agregar el texto a una variable de tipo **nvarchar** y, después, llamar a la variable. |
| @input_data_1 | datos devueltos por la consulta, pasados al tiempo de ejecución de Python, que devuelve los datos que se van a SQL Server como una trama de datos. |
|WITH RESULT SETS | la cláusula define el esquema de la tabla de datos devuelta para SQL Server, en este caso, se agrega "Hola mundo" como nombre de columna e **int** para el tipo de datos. |

El comando genera el siguiente texto:

| Hola mundo |
|-------------|
| 1 |

## <a name="use-inputs-and-outputs"></a>Usar entradas y salidas

De forma predeterminada, `sp_execute_external_script` acepta un único conjunto de datos como entrada, que normalmente se proporciona en forma de consulta SQL válida. A continuación, devuelve una sola trama de datos de Python como salida.

Por ahora, vamos a usar las variables de entrada y salida predeterminadas de `sp_execute_external_script`: **InputDataSet** y **OutputDataSet**.

1. Cree una tabla pequeña de datos de prueba.

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

    **Resultado**

    ![Contenido de la tabla PythonTestData](./media/select-pythontestdata.png)

1. Ejecute el siguiente script de Python. Recupera los datos de la tabla mediante la instrucción `SELECT`, los pasa a través del tiempo de ejecución de Python y devuelve los datos como una trama de datos. La cláusula `WITH RESULT SETS` define el esquema de la tabla de datos devuelta para SQL, agregando el nombre de columna *NewColName*.

    ```sql
    EXECUTE sp_execute_external_script @language = N'Python'
        , @script = N'OutputDataSet = InputDataSet;'
        , @input_data_1 = N'SELECT * FROM PythonTestData;'
    WITH RESULT SETS(([NewColName] INT NOT NULL));
    ```

    **Resultado**

    ![Salida del script de Python que devuelve datos de una tabla](./media/python-output-pythontestdata.png)

1. Ahora, cambie los nombres de las variables de entrada y salida. Los nombres de variables de entrada y de salida predeterminados son **InputDataSet** y **OutputDataSet**, el siguiente script cambia los nombres a **SQL_in** y **SQL_out**:

    ```sql
    EXECUTE sp_execute_external_script @language = N'Python'
        , @script = N'SQL_out = SQL_in;'
        , @input_data_1 = N'SELECT 12 as Col;'
        , @input_data_1_name  = N'SQL_in'
        , @output_data_1_name = N'SQL_out'
    WITH RESULT SETS(([NewColName] INT NOT NULL));
    ```

    Tenga en cuenta que Python distingue entre mayúsculas y minúsculas. Las variables de entrada y salida que se usan en el script de Python (**SQL_out**, **SQL_in**) deben coincidir con los nombres definidos con `@input_data_1_name` y `@output_data_1_name`, incluido el uso de mayúsculas y minúsculas.

   > [!TIP]
   > Solo se puede pasar un conjunto de datos de entrada como parámetro y solo puede devolver un conjunto de datos. Sin embargo, puede llamar a otros conjuntos de valores desde el código de Python y puede devolver resultados de otros tipos además del conjunto de elementos. También puede agregar la palabra clave OUTPUT a cualquier parámetro para que se devuelva con los resultados.

1. También puede generar valores simplemente mediante el script de Python sin datos de entrada (`@input_data_1` está establecido en Blank).

   El script siguiente genera el texto "Hello" y "World".

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

   **Resultado**

   ![Resultados de la consulta mediante @script como entrada](./media/python-data-generated-output.png)

> [!NOTE]
> Python usa espacios iniciales para agrupar instrucciones. Por tanto, cuando el script de Python desincrustado abarca varias líneas, como en el script anterior, no intente aplicar sangría a los comandos de Python para que estén en línea con los comandos SQL. Por ejemplo, este script producirá un error:

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

## <a name="check-python-version"></a>Comprobar la versión de Python

Si desea ver qué versión de Python está instalada en la instancia de SQL Server, ejecute el siguiente script.

```sql
EXECUTE sp_execute_external_script @language = N'Python'
    , @script = N'
import sys
print(sys.version)
'
GO
```

La función `print` de Python devuelve la versión a la ventana **mensajes** . En el resultado del ejemplo siguiente, puede ver que, en este caso, se instala Python versión 3.5.2.

**Resultado**

```text
STDOUT message(s) from external script: 
3.5.2 |Continuum Analytics, Inc.| (default, Jul  5 2016, 11:41:13) [MSC v.1900 64 bit (AMD64)]
```

## <a name="list-python-packages"></a>Enumeración de paquetes de Python

Microsoft ofrece una serie de paquetes de Python preinstalados con SQL Server Machine Learning Services en la instancia de SQL Server.

Para ver una lista de los paquetes de Python instalados, incluida la versión, ejecute el script siguiente.

```SQL
EXECUTE sp_execute_external_script @language = N'Python'
    , @script = N'
import pip
for i in pip.get_installed_distributions():
    print(i)
'
GO
```

La salida procede de `pip.get_installed_distributions()` en Python y se devuelve como mensajes `STDOUT`.

**Resultado**

```text
STDOUT message(s) from external script:
xlwt 1.2.0
XlsxWriter 0.9.6
xlrd 1.0.0
win-unicode-console 0.5
widgetsnbextension 2.0.0
wheel 0.29.0
Werkzeug 0.12.1
wcwidth 0.1.7
unicodecsv 0.14.1
traitlets 4.3.2
tornado 4.4.2
toolz 0.8.2
. . .
```

## <a name="next-steps"></a>Pasos siguientes

Para obtener información sobre cómo usar las estructuras de datos al usar Python en SQL Server Machine Learning Services, siga esta guía de inicio rápido:

> [!div class="nextstepaction"]
> [Control de tipos de datos y objetos mediante Python en SQL Server Machine Learning Services](quickstart-python-data-structures.md)

Para obtener más información sobre el uso de Python en SQL Server Machine Learning Services, consulte los siguientes artículos:

- [Escritura de funciones avanzadas de Python con SQL Server Machine Learning Services](quickstart-python-functions.md)
- [Crear y puntuar un modelo predictivo en Python con SQL Server Machine Learning Services](quickstart-python-train-score-model.md)
- [¿Qué es SQL Server Machine Learning Services (Python y R)?](../what-is-sql-server-machine-learning.md)
