---
title: Guía de inicio rápido para trabajar con entradas y salidas en Python - SQL Server Machine Learning
description: En este inicio rápido para script de Python en SQL Server, obtenga información sobre cómo estructurar las entradas y salidas para el procedimiento almacenado del sistema de sp_execute_external_script.
ms.prod: sql
ms.technology: machine-learning
ms.date: 01/04/2019
ms.topic: quickstart
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: fe60197671e40317f56a62ad98ea364a238df174
ms.sourcegitcommit: c3de32efeee3095fcea0d3faebb8f2ff1b56d229
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/12/2019
ms.locfileid: "67033395"
---
# <a name="quickstart-handle-inputs-and-outputs-using-python-in-sql-server"></a>Inicio rápido: Controlar las entradas y salidas con Python en SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

En este tutorial rápido se muestra cómo controlar las entradas y salidas al uso de Python en SQL Server Machine Learning Services.

De forma predeterminada, [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) acepta un único conjunto de entrada, que normalmente proporciona en forma de una consulta SQL válida.

Otros tipos de entrada pueden pasarse como variables de SQL: por ejemplo, puede pasar un modelo entrenado como una variable, con una función de serialización como [pickle](https://docs.python.org/3.0/library/pickle.html) o [rx_serialize_model](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-serialize-model) para escribir el modelo un formato binario.

El procedimiento almacenado devuelve un único Python [pandas](https://pandas.pydata.org/pandas-docs/stable/index.html) una trama de datos como salida, pero también puede generar modelos como variables y valores escalares. Por ejemplo, puede de salida de un modelo entrenado como una variable binaria y pasarlo a una instrucción INSERT de T-SQL para escribir ese modelo en una tabla. También puede generar trazados (en formato binario) o valores escalares (valores individuales, como la fecha y hora, transcurrido el tiempo para entrenar el modelo y así sucesivamente).

## <a name="prerequisites"></a>Requisitos previos

Un tutorial anterior, [Python Compruebe que existe en SQL Server](quickstart-python-verify.md), proporciona información y vínculos para configurar el entorno de Python necesario para este inicio rápido.

## <a name="create-the-source-data"></a>Crear el origen de datos

Crear una tabla pequeña de datos de prueba mediante la ejecución de la siguiente instrucción T-SQL:

```sql
CREATE TABLE PythonTestData (col1 INT NOT NULL)
INSERT INTO PythonTestData VALUES (1);
INSERT INTO PythonTestData VALUES (10);
INSERT INTO PythonTestData VALUES (100);
GO
```

Después de crear la tabla, use la siguiente instrucción para consultar la tabla:
  
```sql
SELECT * FROM PythonTestData
```

**Resultado**

![Contenido de la tabla PythonTestData](./media/select-pythontestdata.png)

## <a name="inputs-and-outputs"></a>Entradas y salidas

Echemos un vistazo a la forma predeterminada las variables de entrada y salidas de sp_execute_external_script: `InputDataSet` y `OutputDataSet`.

1. Puede obtener los datos de la tabla como entrada para el script de Python. Ejecute la instrucción siguiente. Obtiene los datos de la tabla, realiza un recorrido por el runtime de Python y devuelve los valores con el nombre de columna *NewColName*.

    Los datos devueltos por la consulta se pasan al runtime de Python, que devuelve los datos a la base de datos SQL como un DataFrame de pandas. La cláusula WITH RESULT SETS define el esquema de la tabla de datos devueltos para la base de datos SQL.

    ```sql
    EXECUTE sp_execute_external_script
        @language = N'Python'
        , @script = N'OutputDataSet = InputDataSet;'
        , @input_data_1 = N'SELECT * FROM PythonTestData;'
    WITH RESULT SETS (([NewColName] INT NOT NULL));
    ```

    **Resultado**

    ![Salida de script de Python que devuelve datos de una tabla](./media/python-output-pythontestdata.png)

2. Vamos a cambiar el nombre de las variables de entrada o salidas. El script anterior usa la entrada predeterminada y los nombres de variable de salida _InputDataSet_ y _OutputDataSet_. Para definir los datos de entrada asociados con _InputDataSet_, usa el *@input_data_1* variable.

    En esta secuencia de comandos, los nombres de las variables de entrada y salida para el procedimiento almacenado se cambió a *SQL_out* y *SQL_in*:

    ```sql
    EXECUTE sp_execute_external_script
      @language = N'Python'
      , @script = N'SQL_out = SQL_in'
      , @input_data_1 = N' SELECT 12 as Col;'
      , @input_data_1_name  = N'SQL_in'
      , @output_data_1_name =  N'SQL_out'
      WITH RESULT SETS (([NewColName] INT NOT NULL));
    ```

    El caso de las variables de entrada y salidas de `@input_data_1_name` y `@output_data_1_name` tiene que coincidir con el caso de los que en el código de Python `@script`, como Python distingue mayúsculas de minúsculas.

    Solo se puede pasar un conjunto de datos de entrada como parámetro y solo puede devolver un conjunto de datos. Sin embargo, puede llamar a otros conjuntos de datos desde dentro de su código de Python y puede devolver resultados de otros tipos además del conjunto de datos. También puede agregar la palabra clave OUTPUT a cualquier parámetro para que se devuelva con los resultados. 

    El `WITH RESULT SETS` instrucción define el esquema de los datos que se usan en SQL Server. Deberá proporcionar tipos de datos compatibles de SQL para cada columna que devuelven desde Python. Puede usar la definición de esquema para proporcionar nuevos nombres de columna también, ya que no es necesario usar los nombres de columna de la trama de datos de Python.

3. También puede generar valores mediante el script de Python y dejando la cadena de consulta de entrada de _@input_data_1_ en blanco.

    ```sql
    EXECUTE sp_execute_external_script
    @language = N'Python'
    , @script = N'
    import pandas as pd
    mytextvariable = pandas.Series(["hello", " ", "world"]);
    OutputDataSet = pd.DataFrame(mytextvariable);'
    , @input_data_1 = N''
    WITH RESULT SETS (([Col1] CHAR(20) NOT NULL));
    ```

    **Resultado**

    ![Los resultados de consulta con @script como entrada](./media/python-data-generated-output.png)

## <a name="next-steps"></a>Pasos siguientes

Examine algunos de los problemas que pueden surgir cuando se pasan datos tabulares entre Python y SQL Server.

> [!div class="nextstepaction"]
> [Inicio rápido: Estructuras de datos de Python en SQL Server](quickstart-python-data-structures.md)
