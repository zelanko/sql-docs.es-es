---
title: 'Inicio rápido: Ejecutar scripts de R'
description: Ejecute un conjunto de scripts de R sencillos con SQL Server Machine Learning Services. Obtenga información sobre cómo usar el procedimiento almacenado sp_execute_external_script para ejecutar el script en una instancia de SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 01/27/2020
ms.topic: quickstart
author: garyericson
ms.author: garye
ms.reviewer: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 33baeba807711c1eb65b3a9c972066bb384e2542
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2020
ms.locfileid: "81487304"
---
# <a name="quickstart-run-simple-r-scripts-with-sql-server-machine-learning-services"></a>Inicio rápido: ejecución de scripts de R sencillos con SQL Server Machine Learning Services
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

En este inicio rápido, ejecutará un conjunto de scripts de R sencillos mediante [SQL Server Machine Learning Services](../sql-server-machine-learning-services.md). Aprenderá a usar el procedimiento almacenado [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) para ejecutar el script en una instancia de SQL Server.

## <a name="prerequisites"></a>Prerrequisitos

- Para este inicio rápido, es necesario tener acceso a una instancia de SQL Server con [SQL Server Machine Learning Services](../install/sql-machine-learning-services-windows-install.md) que tenga instalado el lenguaje de R.

  Su instancia de SQL Server puede estar en una máquina virtual de Azure o en un entorno local. Tenga en cuenta que la característica de scripts externos está deshabilitada de forma predeterminada, por lo que puede que tenga que [habilitar scripts externos](../install/sql-machine-learning-services-windows-install.md#bkmk_enableFeature) y asegurarse de que el **servicio SQL Server Launchpad** esté ejecutándose antes de empezar.

- También necesita una herramienta para ejecutar consultas SQL que contengan scripts de R. Puede ejecutar estos scripts con cualquier herramienta de consultas o administración de bases de datos, siempre que pueda conectarse a una instancia de SQL Server y ejecutar una consulta T-SQL o un procedimiento almacenado. En este inicio rápido, se usa [SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/sql-server-management-studio-ssms).

## <a name="run-a-simple-script"></a>Ejecución de un script sencillo

Para ejecutar un script de R, necesita pasarlo como un argumento al procedimiento almacenado del sistema, [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md).
Este procedimiento almacenado del sistema inicia el entorno de ejecución de R en el contexto de SQL Server, pasa datos a R, administra de forma segura las sesiones de usuario de R y devuelve los resultados al cliente.

En los pasos siguientes, ejecutará este script de R de ejemplo en su instancia de SQL Server:

```r
a <- 1
b <- 2
c <- a/b
d <- a*b
print(c(c, d))
```

1. Abra **SQL Server Management Studio** y conéctese a su instancia de SQL Server.

1. Pase todo el script de R al procedimiento almacenado `sp_execute_external_script`.

   El script se pasa mediante el argumento `@script`. Todo lo que contenga el argumento `@script` tiene que ser código de R válido.

    ```sql
    EXECUTE sp_execute_external_script @language = N'R'
        , @script = N'
    a <- 1
    b <- 2
    c <- a/b
    d <- a*b
    print(c(c, d))
    '
    ```

1. Se calcula el resultado correcto y la función de R `print` devuelve el resultado a la ventana **Mensajes**.

   Necesita tener el siguiente aspecto.

    **Resultados**

    ```text
    STDOUT message(s) from external script:
    0.5 2
    ```

## <a name="run-a-hello-world-script"></a>Ejecución de un script Hola mundo

Un script de ejemplo típico es uno que simplemente muestra la cadena "Hola mundo". Ejecute el siguiente comando:

```sql
EXECUTE sp_execute_external_script @language = N'R'
    , @script = N'OutputDataSet<-InputDataSet'
    , @input_data_1 = N'SELECT 1 AS hello'
WITH RESULT SETS(([Hello World] INT));
GO
```

Entre las entradas para el procedimiento almacenado `sp_execute_external_script`, se incluyen las siguientes:

| | |
|-|-|
| @language | define la extensión del lenguaje a la que se llamará (en este caso, R). |
| @script | define los comandos que se pasarán al entorno de ejecución de R. Su script de R completo debe estar incluido en este argumento, como texto Unicode. También puede agregar texto a una variable del tipo **nvarchar** y, después, llamar a la variable. |
| @input_data_1 | los datos devueltos por la consulta se pasan al entorno de ejecución de R, que los devuelve a su vez a SQL Server como una trama de datos. |
|WITH RESULT SETS | cláusula que define el esquema de la tabla de datos devuelta a SQL Server (se agrega "Hola mundo" como el nombre de columna e **int** para el tipo de datos). |

El comando muestra el texto siguiente:

| Hola mundo |
|-------------|
| 1 |

## <a name="use-inputs-and-outputs"></a>Uso de entradas y salidas

De forma predeterminada, `sp_execute_external_script` acepta un único conjunto de datos como entrada, que se suele proporcionar como una consulta SQL válida. Después, devuelve una única trama de datos de R como salida.

Por ahora, usaremos las variables de entrada y salida predeterminadas de `sp_execute_external_script`: **InputDataSet** y **OutputDataSet**.

1. Cree una tabla pequeña con datos de prueba.

    ```sql
    CREATE TABLE RTestData (col1 INT NOT NULL)
    
    INSERT INTO RTestData
    VALUES (1);
    
    INSERT INTO RTestData
    VALUES (10);
    
    INSERT INTO RTestData
    VALUES (100);
    GO
    ```

1. Use la instrucción `SELECT` para consultar la tabla.
  
    ```sql
    SELECT *
    FROM RTestData
    ```

    **Resultados**

    ![Contenido de la tabla RTestData](./media/select-rtestdata.png)

1. Ejecute el siguiente script de R. Recupera los datos de la tabla mediante la instrucción `SELECT`, los pasa mediante el entorno de ejecución de R y devuelve los datos como una trama de datos. La cláusula `WITH RESULT SETS` define el esquema de la tabla de datos devuelta para SQL y agrega el nombre de columna *NewColName*.

    ```sql
    EXECUTE sp_execute_external_script @language = N'R'
        , @script = N'OutputDataSet <- InputDataSet;'
        , @input_data_1 = N'SELECT * FROM RTestData;'
    WITH RESULT SETS(([NewColName] INT NOT NULL));
    ```

    **Resultados**

    ![Salida del script de R que devuelve datos de una tabla](./media/r-output-rtestdata.png)

1. Ahora, cambie los nombres de las variables de entrada y salida. Los nombres predeterminados de las variables de entrada y salida son **InputDataSet** y **OutputDataSet**; este script cambia los nombres a **SQL_in** y **SQL_out**:

    ```sql
    EXECUTE sp_execute_external_script @language = N'R'
        , @script = N' SQL_out <- SQL_in;'
        , @input_data_1 = N' SELECT 12 as Col;'
        , @input_data_1_name = N'SQL_in'
        , @output_data_1_name = N'SQL_out'
    WITH RESULT SETS(([NewColName] INT NOT NULL));
    ```

    Tenga en cuenta que R distingue mayúsculas de minúsculas. Las variables de entrada y salida usadas en el script de R (**SQL_out** y **SQL_in**) tienen que coincidir con los nombres definidos con `@input_data_1_name` y `@output_data_1_name`, incluido el uso de mayúsculas.

   > [!TIP]
   > Solo se puede pasar un conjunto de datos de entrada como parámetro, y solo se puede devolver un conjunto de datos. Sin embargo, puede llamar a otros conjuntos de datos desde el interior del código R y puede devolver salidas de otros tipos además del conjunto de datos. También puede agregar la palabra clave OUTPUT a cualquier parámetro para que se devuelva con los resultados.

1. También puede generar valores con el script de R sin datos de entrada (`@input_data_1` se establece en blanco).

   El script siguiente genera el texto "hola" y "mundo".

    ```sql
    EXECUTE sp_execute_external_script @language = N'R'
        , @script = N'
    mytextvariable <- c("hello", " ", "world");
    OutputDataSet <- as.data.frame(mytextvariable);
    '
        , @input_data_1 = N''
    WITH RESULT SETS(([Col1] CHAR(20) NOT NULL));
    ```

    **Resultados**

    ![Resultados de consultas con @script como entrada](./media/r-data-generated-output.png)

## <a name="check-r-version"></a>Comprobación de la versión de R

Si quiere ver qué versión de R está instalada en su instancia de SQL Server, ejecute el script siguiente.

```sql
EXECUTE sp_execute_external_script @language = N'R'
    , @script = N'print(version)';
GO
```

La función `print` de R devuelve la versión en la ventana **Mensajes**. En la salida de ejemplo siguiente, puede ver que, en este caso, la versión de R instalada es 3.4.4.

**Resultados**

```text
STDOUT message(s) from external script:
                   _
platform       x86_64-w64-mingw32
arch           x86_64
os             mingw32
system         x86_64, mingw32
status
major          3
minor          4.4
year           2018
month          03
day            15
svn rev        74408
language       R
version.string R version 3.4.4 (2018-03-15)
nickname       Someone to Lean On
```

## <a name="list-r-packages"></a>Lista de paquetes de R

Microsoft proporciona varios paquetes de R preinstalados con SQL Server Machine Learning Services.

Para ver una lista de los paquetes de R instalados (además de la versión, las dependencias, la licencia y la información de la ruta de la biblioteca), ejecute el script siguiente.

```SQL
EXEC sp_execute_external_script @language = N'R'
    , @script = N'
OutputDataSet <- data.frame(installed.packages()[,c("Package", "Version", "Depends", "License", "LibPath")]);'
WITH result sets((
            Package NVARCHAR(255)
            , Version NVARCHAR(100)
            , Depends NVARCHAR(4000)
            , License NVARCHAR(1000)
            , LibPath NVARCHAR(2000)
            ));
```

El resultado es `installed.packages()` de R y se devuelve como un conjunto de resultados.

**Resultados**

![Paquetes instalados en R](./media/rsql-installed-packages.png) 

## <a name="next-steps"></a>Pasos siguientes

Para obtener información sobre cómo usar estructuras de datos al usar R en SQL Server Machine Learning Services, siga este inicio rápido:

> [!div class="nextstepaction"]
> [Procesamiento de tipos de datos y objetos mediante R en SQL Server Machine Learning Services](quickstart-r-data-types-and-objects.md)

Para más información sobre cómo usar R en SQL Server Machine Learning Services, vea los artículos siguientes:

- [Creación de funciones avanzadas de R con SQL Server Machine Learning Services](quickstart-r-functions.md)
- [Creación y puntuación de un modelo predictivo en R con SQL Server Machine Learning Services](quickstart-r-train-score-model.md)
- [¿Qué es SQL Server Machine Learning Services (Python y R)?](../sql-server-machine-learning-services.md)
