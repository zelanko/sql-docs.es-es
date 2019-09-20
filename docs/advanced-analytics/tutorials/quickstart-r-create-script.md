---
title: Crear y ejecutar scripts de R simples
titleSuffix: SQL Server Machine Learning Services
description: Crear y ejecutar scripts de R simples en una instancia de SQL Server con SQL Server Machine Learning Services.
ms.prod: sql
ms.technology: machine-learning
ms.date: 09/17/2019
ms.topic: quickstart
author: garyericson
ms.author: garye
ms.reviewer: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: d723fa9b90659eb31e96626a3a85c1299c17fa2f
ms.sourcegitcommit: 1661c3e1bb38ed12f8485c3860fc2d2b97dd2c9d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/20/2019
ms.locfileid: "71150318"
---
# <a name="quickstart-create-and-run-simple-r-scripts-with-sql-server-machine-learning-services"></a>Inicio rápido: Crear y ejecutar scripts de R sencillos con SQL Server Machine Learning Services
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

En esta guía de inicio rápido, creará y ejecutará un conjunto de sencillos scripts de R mediante [SQL Server Machine Learning Services](../what-is-sql-server-machine-learning.md). Aprenderá a ajustar un script R correcto en el procedimiento almacenado [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) y a ejecutar el script en una instancia de SQL Server.

## <a name="prerequisites"></a>Requisitos previos

- Esta guía de inicio rápido requiere acceso a una instancia de SQL Server con [SQL Server Machine Learning Services](../install/sql-machine-learning-services-windows-install.md) con el lenguaje R instalado.

  La instancia de SQL Server puede estar en una máquina virtual de Azure o en un entorno local. Tenga en cuenta que la característica de scripting externo está deshabilitada de forma predeterminada, por lo que es posible que tenga que [Habilitar el scripting externo](../install/sql-machine-learning-services-windows-install.md#bkmk_enableFeature) y comprobar que **SQL Server Launchpad servicio** se está ejecutando antes de empezar.

- También necesita una herramienta para ejecutar consultas SQL que contienen scripts de R. Puede ejecutar estos scripts mediante cualquier herramienta de consulta o administración de bases de datos, siempre que pueda conectarse a una instancia de SQL Server y ejecutar una consulta T-SQL o un procedimiento almacenado. Esta guía de inicio rápido usa [SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/sql-server-management-studio-ssms).

## <a name="run-a-simple-script"></a>Ejecutar un script simple

Para ejecutar un script de R, lo pasará como argumento al procedimiento almacenado del sistema, [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md).
Este procedimiento almacenado del sistema inicia el tiempo de ejecución de R en el contexto de SQL Server, pasa datos a R, administra las sesiones de usuario de R de forma segura y devuelve los resultados al cliente.

En los pasos siguientes, ejecutará este script R de ejemplo en la instancia de SQL Server:

```r
a <- 1
b <- 2
c <- a/b
d <- a*b
print(c(c, d))
```

1. Abra **SQL Server Management Studio** y conéctese a su instancia de SQL Server.

1. Pase el script de R completo al `sp_execute_external_script` procedimiento almacenado.

   El script se pasa a través `@script` del argumento. Todo lo que `@script` se encuentra dentro del argumento debe ser un código de R válido.

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

1. Se calcula el resultado correcto y la función `print` de R devuelve el resultado a la ventana **mensajes** .

   Debe tener un aspecto similar al siguiente.

    **Resultado**

    ```text
    STDOUT message(s) from external script:
    0.5 2
    ```

## <a name="run-a-hello-world-script"></a>Ejecutar un script de Hola mundo

Un script de ejemplo típico es aquél que simplemente genera la cadena "Hola mundo". Ejecute el siguiente comando:

```sql
EXECUTE sp_execute_external_script @language = N'R'
    , @script = N'OutputDataSet<-InputDataSet'
    , @input_data_1 = N'SELECT 1 AS hello'
WITH RESULT SETS(([Hello World] INT));
GO
```

Entre las entradas `sp_execute_external_script` del procedimiento almacenado se incluyen:

| | |
|-|-|
| @language | define la extensión del lenguaje para llamar a, en este caso, R |
| @script | define los comandos que se pasan al tiempo de ejecución de R. El script de R debe estar todo incluido en este argumento en texto Unicode. También puede Agregar el texto a una variable de tipo **nvarchar** y, después, llamar a la variable. |
| @input_data_1 | datos devueltos por la consulta, pasados al Runtime de R, que devuelve los datos que se van a SQL Server como una trama de datos. |
|CON CONJUNTOS DE RESULTADOS | la cláusula define el esquema de la tabla de datos devuelta para SQL Server, agregando "Hola mundo" como nombre de columna, **int** para el tipo de datos |

El comando genera el siguiente texto:

| Hola mundo |
|-------------|
| 1 |

## <a name="use-inputs-and-outputs"></a>Usar entradas y salidas

De forma predeterminada `sp_execute_external_script` , acepta un único conjunto de datos como entrada, que normalmente se proporciona en forma de consulta SQL válida. A continuación, devuelve una sola trama de datos de R como salida.

Por ahora, vamos a usar las variables de entrada y salida predeterminadas de `sp_execute_external_script`: **InputDataSet** y **OutputDataSet**.

1. Cree una tabla pequeña de datos de prueba.

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

1. Use la `SELECT` instrucción para consultar la tabla.
  
    ```sql
    SELECT *
    FROM RTestData
    ```

    **Resultado**

    ![Contenido de la tabla RTestData](./media/select-rtestdata.png)

1. Ejecute el siguiente script de R. Recupera los datos de la tabla mediante la instrucción, `SELECT` los pasa a través del tiempo de ejecución de R y devuelve los datos como una trama de datos. La `WITH RESULT SETS` cláusula define el esquema de la tabla de datos devuelta para SQL, agregando el nombre de columna *NewColName*.

    ```sql
    EXECUTE sp_execute_external_script @language = N'R'
        , @script = N'OutputDataSet <- InputDataSet;'
        , @input_data_1 = N'SELECT * FROM RTestData;'
    WITH RESULT SETS(([NewColName] INT NOT NULL));
    ```

    **Resultado**

    ![Salida del script de R que devuelve datos de una tabla](./media/r-output-rtestdata.png)

1. Ahora vamos a cambiar los nombres de las variables de entrada y salida. Los nombres de variables de entrada y salida predeterminados son **InputDataSet** y **OutputDataSet**, este script cambia los nombres a **SQL_in** y **SQL_out**:

    ```sql
    EXECUTE sp_execute_external_script @language = N'R'
        , @script = N' SQL_out <- SQL_in;'
        , @input_data_1 = N' SELECT 12 as Col;'
        , @input_data_1_name = N'SQL_in'
        , @output_data_1_name = N'SQL_out'
    WITH RESULT SETS(([NewColName] INT NOT NULL));
    ```

    Tenga en cuenta que R distingue mayúsculas de minúsculas. Las variables de entrada y salida que se usan en el script de R (**SQL_out**, **SQL_in**) deben coincidir `@input_data_1_name` con `@output_data_1_name`los nombres definidos con y, incluido el uso de mayúsculas y minúsculas.

   > [!TIP]
   > Solo se puede pasar un conjunto de datos de entrada como parámetro y solo puede devolver un conjunto de datos. Pero puede llamar a otros conjuntos de datos desde dentro de su código de R y devolver resultados de otros tipos además del conjunto de datos. También puede agregar la palabra clave OUTPUT a cualquier parámetro para que se devuelva con los resultados.

1. También puede generar valores simplemente mediante el script de R sin datos de entrada (`@input_data_1` está establecido en en blanco).

   El script siguiente genera el texto "Hello" y "World".

    ```sql
    EXECUTE sp_execute_external_script @language = N'R'
        , @script = N'
    mytextvariable <- c("hello", " ", "world");
    OutputDataSet <- as.data.frame(mytextvariable);
    '
        , @input_data_1 = N''
    WITH RESULT SETS(([Col1] CHAR(20) NOT NULL));
    ```

    **Resultado**

    ![Resultados de la @script consulta mediante como entrada](./media/r-data-generated-output.png)

## <a name="check-r-version"></a>Comprobar versión de R

Si desea ver qué versión de R está instalada en la instancia de SQL Server, ejecute el siguiente script.

```sql
EXECUTE sp_execute_external_script @language = N'R'
    , @script = N'print(version)';
GO
```

La función `print` R devuelve la versión a la ventana **mensajes** . En el resultado del ejemplo siguiente, puede ver que, en este caso, la versión de R 3.4.4 está instalada.

**Resultado**

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

## <a name="list-r-packages"></a>Enumerar paquetes de R

Microsoft ofrece una serie de paquetes de R preinstalados con Machine Learning Services de SQL Server.

Para ver una lista de los paquetes de R instalados, incluidas la versión, las dependencias, la licencia y la información de la ruta de acceso de la biblioteca, ejecute el script siguiente.

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

El resultado es de `installed.packages()` en R y se devuelve como un conjunto de resultados.

**Resultado**

![Paquetes instalados en R](./media/rsql-installed-packages.png) 

## <a name="next-steps"></a>Pasos siguientes

Para crear un modelo de aprendizaje automático con R en SQL Server, siga esta guía de inicio rápido:

> [!div class="nextstepaction"]
> [Crear y puntuar un modelo predictivo en R con SQL Server Machine Learning Services](quickstart-r-train-score-model.md)

Para obtener más información sobre SQL Server Machine Learning Services, consulte los siguientes artículos.

- [Administrar tipos de datos y objetos mediante R en SQL Server Machine Learning Services](quickstart-r-data-types-and-objects.md)
- [Escritura de funciones avanzadas de R con SQL Server Machine Learning Services](quickstart-r-functions.md)
- [¿Qué es SQL Server Machine Learning Services (Python y R)?](../what-is-sql-server-machine-learning.md)
