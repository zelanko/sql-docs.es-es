---
title: Guía de inicio rápido para trabajar con entradas y salidas en R - SQL Server Machine Learning
description: En este inicio rápido para script de R en SQL Server, obtenga información sobre cómo estructurar las entradas y salidas para el procedimiento almacenado del sistema de sp_execute_external_script.
ms.prod: sql
ms.technology: machine-learning
ms.date: 01/04/2019
ms.topic: quickstart
author: dphansen
ms.author: davidph
ms.openlocfilehash: 1672cdeb59dfe35e313c999549e46f3fd76b688e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67962007"
---
# <a name="quickstart-handle-inputs-and-outputs-using-r-in-sql-server"></a>Inicio rápido: Controlar las entradas y salidas con R en SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

En este tutorial rápido se muestra cómo controlar las entradas y salidas al usar R en SQL Server Machine Learning Services o R Services.

Cuando desea ejecutar código R en SQL Server, debe incluir el script de R en un procedimiento almacenado. Puede escribir uno, o pasar el script de R a [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md). Este sistema de procedimiento almacenado se utiliza para iniciar el runtime de R en el contexto de SQL Server, que pasa datos a R, administra las sesiones de usuario de R de forma segura y devuelve todos los resultados al cliente.

De forma predeterminada, [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) acepta un único conjunto de entrada, que normalmente proporciona en forma de una consulta SQL válida. Otros tipos de entrada pueden pasarse como variables de SQL.

El procedimiento almacenado devuelve una única trama de datos de R como resultado, pero también puede generar modelos como variables y valores escalares. Por ejemplo, puede de salida de un modelo entrenado como una variable binaria y pasarlo a una instrucción INSERT de T-SQL para escribir ese modelo en una tabla. También puede generar trazados (en formato binario) o valores escalares (valores individuales, como la fecha y hora, transcurrido el tiempo para entrenar el modelo y así sucesivamente).

## <a name="prerequisites"></a>Requisitos previos

Un tutorial anterior, [R Compruebe que existe en SQL Server](quickstart-r-verify.md), proporciona información y vínculos para configurar el entorno de R necesario para este inicio rápido.

## <a name="create-the-source-data"></a>Crear el origen de datos

Crear una tabla pequeña de datos de prueba mediante la ejecución de la siguiente instrucción T-SQL:

```sql
CREATE TABLE RTestData (col1 INT NOT NULL)
INSERT INTO RTestData VALUES (1);
INSERT INTO RTestData VALUES (10);
INSERT INTO RTestData VALUES (100);
GO
```

Después de crear la tabla, use la siguiente instrucción para consultar la tabla:
  
```sql
SELECT * FROM RTestData
```

**Resultado**

![Contenido de la tabla RTestData](./media/select-rtestdata.png)

## <a name="inputs-and-outputs"></a>Entradas y salidas

Echemos un vistazo a la forma predeterminada las variables de entrada y salidas de sp_execute_external_script: `InputDataSet` y `OutputDataSet`.

1. Puede obtener los datos de la tabla como entrada para el script de R. Ejecute la instrucción siguiente. Obtiene los datos de la tabla, realiza un recorrido por el runtime de R y devuelve los valores con el nombre de columna *NewColName*.

    Los datos devueltos por la consulta se pasan al runtime de R, que devuelve los datos a la base de datos de SQL como una trama de datos. La cláusula WITH RESULT SETS define el esquema de la tabla de datos devueltos para la base de datos SQL.

    ```sql
    EXECUTE sp_execute_external_script
        @language = N'R'
        , @script = N'OutputDataSet <- InputDataSet;'
        , @input_data_1 = N'SELECT * FROM RTestData;'
    WITH RESULT SETS (([NewColName] INT NOT NULL));
    ```

    **Resultado**

    ![Salida de script de R que devuelve datos de una tabla](./media/r-output-rtestdata.png)

2. Vamos a cambiar el nombre de las variables de entrada o salidas. El script anterior usa la entrada predeterminada y los nombres de variable de salida _InputDataSet_ y _OutputDataSet_. Para definir los datos de entrada asociados con _InputDatSet_, usa el *@input_data_1* variable.

    En esta secuencia de comandos, los nombres de las variables de entrada y salida para el procedimiento almacenado se cambió a *SQL_out* y *SQL_in*:

    ```sql
    EXECUTE sp_execute_external_script
      @language = N'R'
      , @script = N' SQL_out <- SQL_in;'
      , @input_data_1 = N'SELECT 12 as Col;'
      , @input_data_1_name  = N'SQL_in'
      , @output_data_1_name =  N'SQL_out'
      WITH RESULT SETS (([NewColName] INT NOT NULL));
    ```

    Tenga en cuenta que R distingue mayúsculas de minúsculas, por lo que el caso de las variables de entrada y salidas de `@input_data_1_name` y `@output_data_1_name` tiene que coincidir con los que en el código de R `@script`. 

    Solo se puede pasar un conjunto de datos de entrada como parámetro y solo puede devolver un conjunto de datos. Pero puede llamar a otros conjuntos de datos desde dentro de su código de R y devolver resultados de otros tipos además del conjunto de datos. También puede agregar la palabra clave OUTPUT a cualquier parámetro para que se devuelva con los resultados. 

    El `WITH RESULT SETS` instrucción define el esquema de los datos que se usan en SQL Server. Deberá proporcionar tipos de datos compatibles de SQL para cada columna que se obtenga de R. Puede usar la definición de esquema para proporcionar nuevos nombres de columna también, ya que no es necesario usar los nombres de columna de la trama de datos de R.

3. También puede generar valores mediante el script de R y dejando la cadena de consulta de entrada de _@input_data_1_ en blanco.

    ```sql
    EXECUTE sp_execute_external_script
        @language = N'R'
        , @script = N' mytextvariable <- c("hello", " ", "world");
            OutputDataSet <- as.data.frame(mytextvariable);'
        , @input_data_1 = N''
    WITH RESULT SETS (([Col1] CHAR(20) NOT NULL));
    ```

    **Resultado**

    ![Los resultados de consulta con @script como entrada](./media/r-data-generated-output.png)

## <a name="next-steps"></a>Pasos siguientes

Examine algunos de los problemas que pueden surgir cuando se pasan datos entre R y SQL Server, como las conversiones implícitas y las diferencias en los datos tabulares entre R y SQL.

> [!div class="nextstepaction"]
> [Inicio rápido: Administrar tipos de datos y objetos](quickstart-r-data-types-and-objects.md)