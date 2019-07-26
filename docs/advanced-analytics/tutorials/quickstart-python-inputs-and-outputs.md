---
title: Guía de inicio rápido para trabajar con entradas y salidas en Python
description: En esta guía de inicio rápido para el script de Python en SQL Server, obtenga información sobre cómo estructurar entradas y salidas en el procedimiento almacenado del sistema sp_execute_external_script.
ms.prod: sql
ms.technology: machine-learning
ms.date: 01/04/2019
ms.topic: quickstart
author: dphansen
ms.author: davidph
ms.openlocfilehash: 0259a4695ab1ee6f42b92e12b47f81e9aa851469
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/24/2019
ms.locfileid: "68469605"
---
# <a name="quickstart-handle-inputs-and-outputs-using-python-in-sql-server"></a>Inicio rápido: Control de entradas y salidas mediante Python en SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

En esta guía de inicio rápido se muestra cómo controlar las entradas y salidas al usar Python en SQL Server Machine Learning Services.

De forma predeterminada, [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) acepta un único conjunto de datos de entrada, que normalmente se proporciona en forma de consulta SQL válida.

Se pueden pasar otros tipos de entrada como variables SQL: por ejemplo, puede pasar un modelo entrenado como una variable, mediante una función de serialización como [Pickle](https://docs.python.org/3.0/library/pickle.html) o [rx_serialize_model](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-serialize-model) para escribir el modelo en un formato binario.

El procedimiento almacenado devuelve una sola trama de datos de Python [pandas](https://pandas.pydata.org/pandas-docs/stable/index.html) como salida, pero también puede generar valores escalares y modelos como variables. Por ejemplo, puede generar un modelo entrenado como una variable binaria y pasarlo a una instrucción INSERT de T-SQL para escribir ese modelo en una tabla. También puede generar trazados (en formato binario) o escalares (valores individuales, como la fecha y la hora, el tiempo transcurrido para entrenar el modelo, etc.).

## <a name="prerequisites"></a>Requisitos previos

En una guía de inicio rápido anterior, [Compruebe que Python existe en SQL Server](quickstart-python-verify.md), proporciona información y vínculos para configurar el entorno de Python necesario para esta guía de inicio rápido.

## <a name="create-the-source-data"></a>Crear el origen de datos

Cree una tabla pequeña de datos de prueba mediante la ejecución de la siguiente instrucción T-SQL:

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

Echemos un vistazo a las variables de entrada y salida predeterminadas `OutputDataSet`de sp_execute_external_script: `InputDataSet` y.

1. Puede obtener los datos de la tabla como entrada para el script de Python. Ejecute la instrucción siguiente. Obtiene los datos de la tabla, realiza un recorrido de ida y vuelta a través del tiempo de ejecución de Python y devuelve los valores con el nombre de columna *NewColName*.

    Los datos devueltos por la consulta se pasan al tiempo de ejecución de Python, que devuelve los datos que se van a SQL Database como trama de datos pandas. La cláusula WITH RESULT SETS define el esquema de la tabla de datos devuelta para SQL Database.

    ```sql
    EXECUTE sp_execute_external_script
        @language = N'Python'
        , @script = N'OutputDataSet = InputDataSet;'
        , @input_data_1 = N'SELECT * FROM PythonTestData;'
    WITH RESULT SETS (([NewColName] INT NOT NULL));
    ```

    **Resultado**

    ![Salida del script de Python que devuelve datos de una tabla](./media/python-output-pythontestdata.png)

2. Vamos a cambiar el nombre de las variables de entrada o salida. El script anterior usaba los nombres de variables de entrada y salida predeterminados, _InputDataSet_ y _OutputDataSet_. Para definir los datos de entrada asociados a _InputDataSet_, se usa *@input_data_1* la variable.

    En este script, los nombres de las variables de entrada y salida del procedimiento almacenado se han cambiado a *SQL_out* y *SQL_in*:

    ```sql
    EXECUTE sp_execute_external_script
      @language = N'Python'
      , @script = N'SQL_out = SQL_in'
      , @input_data_1 = N' SELECT 12 as Col;'
      , @input_data_1_name  = N'SQL_in'
      , @output_data_1_name =  N'SQL_out'
      WITH RESULT SETS (([NewColName] INT NOT NULL));
    ```

    El caso de las variables de entrada y salida `@input_data_1_name` en `@output_data_1_name` y tienen que coincidir con el caso de los del código de `@script`Python en, ya que Python distingue entre mayúsculas y minúsculas.

    Solo se puede pasar un conjunto de datos de entrada como parámetro y solo puede devolver un conjunto de datos. Sin embargo, puede llamar a otros conjuntos de valores desde el código de Python y puede devolver resultados de otros tipos además del conjunto de elementos. También puede agregar la palabra clave OUTPUT a cualquier parámetro para que se devuelva con los resultados. 

    La `WITH RESULT SETS` instrucción define el esquema de los datos que se usan en SQL Server. Debe proporcionar tipos de datos compatibles con SQL para cada columna que devuelva desde Python. También puede usar la definición de esquema para proporcionar nuevos nombres de columna, ya que no es necesario usar los nombres de columna de Python Data. Frame.

3. También puede generar valores mediante el script de Python y dejar la cadena de consulta de _@input_data_1_ entrada en blanco.

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

    ![Resultados de la @script consulta mediante como entrada](./media/python-data-generated-output.png)

## <a name="next-steps"></a>Pasos siguientes

Examine algunos de los problemas que pueden surgir al pasar datos tabulares entre Python y SQL Server.

> [!div class="nextstepaction"]
> [Inicio rápido: Estructuras de datos de Python en SQL Server](quickstart-python-data-structures.md)
