---
title: Guía de inicio rápido para trabajar con entradas y salidas en R
description: En esta guía de inicio rápido para script R en SQL Server, obtenga información sobre cómo estructurar entradas y salidas en el procedimiento almacenado del sistema sp_execute_external_script.
ms.prod: sql
ms.technology: machine-learning
ms.date: 01/04/2019
ms.topic: quickstart
author: dphansen
ms.author: davidph
ms.openlocfilehash: 4e9e7efe6143d35e627abef4272281aad4b5b184
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/24/2019
ms.locfileid: "68469157"
---
# <a name="quickstart-handle-inputs-and-outputs-using-r-in-sql-server"></a>Inicio rápido: Control de entradas y salidas mediante R en SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

En esta guía de inicio rápido se muestra cómo controlar las entradas y salidas al usar R en SQL Server Machine Learning Services o R Services.

Si desea ejecutar código R en SQL Server, debe ajustar el script de R en un procedimiento almacenado. Puede escribir uno o pasar el script de R a [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md). Este procedimiento almacenado del sistema se utiliza para iniciar el tiempo de ejecución de R en el contexto de SQL Server, que pasa datos a R, administra las sesiones de usuario de R de forma segura y devuelve los resultados al cliente.

De forma predeterminada, [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) acepta un único conjunto de datos de entrada, que normalmente se proporciona en forma de consulta SQL válida. Otros tipos de entrada se pueden pasar como variables SQL.

El procedimiento almacenado devuelve una sola trama de datos de R como salida, pero también puede generar valores escalares y modelos como variables. Por ejemplo, puede generar un modelo entrenado como una variable binaria y pasarlo a una instrucción INSERT de T-SQL para escribir ese modelo en una tabla. También puede generar trazados (en formato binario) o escalares (valores individuales, como la fecha y la hora, el tiempo transcurrido para entrenar el modelo, etc.).

## <a name="prerequisites"></a>Requisitos previos

En una guía de inicio rápido anterior, [Verify r existe en SQL Server](quickstart-r-verify.md), se proporciona información y vínculos para configurar el entorno de r necesario para esta guía de inicio rápido.

## <a name="create-the-source-data"></a>Crear el origen de datos

Cree una tabla pequeña de datos de prueba mediante la ejecución de la siguiente instrucción T-SQL:

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

Echemos un vistazo a las variables de entrada y salida predeterminadas `OutputDataSet`de sp_execute_external_script: `InputDataSet` y.

1. Puede obtener los datos de la tabla como entrada para el script de R. Ejecute la instrucción siguiente. Obtiene los datos de la tabla, realiza un recorrido de ida y vuelta a través del tiempo de ejecución de R y devuelve los valores con el nombre de columna *NewColName*.

    Los datos devueltos por la consulta se pasan al tiempo de ejecución de R, que devuelve los datos que se van a SQL Database como una trama de datos. La cláusula WITH RESULT SETS define el esquema de la tabla de datos devuelta para SQL Database.

    ```sql
    EXECUTE sp_execute_external_script
        @language = N'R'
        , @script = N'OutputDataSet <- InputDataSet;'
        , @input_data_1 = N'SELECT * FROM RTestData;'
    WITH RESULT SETS (([NewColName] INT NOT NULL));
    ```

    **Resultado**

    ![Salida del script de R que devuelve datos de una tabla](./media/r-output-rtestdata.png)

2. Vamos a cambiar el nombre de las variables de entrada o salida. El script anterior usaba los nombres de variables de entrada y salida predeterminados, _InputDataSet_ y _OutputDataSet_. Para definir los datos de entrada asociados a _InputDatSet_, se usa *@input_data_1* la variable.

    En este script, los nombres de las variables de entrada y salida del procedimiento almacenado se han cambiado a *SQL_out* y *SQL_in*:

    ```sql
    EXECUTE sp_execute_external_script
      @language = N'R'
      , @script = N' SQL_out <- SQL_in;'
      , @input_data_1 = N'SELECT 12 as Col;'
      , @input_data_1_name  = N'SQL_in'
      , @output_data_1_name =  N'SQL_out'
      WITH RESULT SETS (([NewColName] INT NOT NULL));
    ```

    Tenga en cuenta que R distingue entre mayúsculas y minúsculas, por lo que el caso `@input_data_1_name` de `@output_data_1_name` las variables de entrada y salida de y debe coincidir con los del código R en `@script`. 

    Solo se puede pasar un conjunto de datos de entrada como parámetro y solo puede devolver un conjunto de datos. Pero puede llamar a otros conjuntos de datos desde dentro de su código de R y devolver resultados de otros tipos además del conjunto de datos. También puede agregar la palabra clave OUTPUT a cualquier parámetro para que se devuelva con los resultados. 

    La `WITH RESULT SETS` instrucción define el esquema de los datos que se usan en SQL Server. Debe proporcionar tipos de datos compatibles con SQL para cada columna que devuelva desde R. También puede usar la definición de esquema para proporcionar nuevos nombres de columna, ya que no es necesario usar los nombres de columna de la trama de datos de R.

3. También puede generar valores mediante el script de R y dejar la cadena de consulta de _@input_data_1_ entrada en blanco.

    ```sql
    EXECUTE sp_execute_external_script
        @language = N'R'
        , @script = N' mytextvariable <- c("hello", " ", "world");
            OutputDataSet <- as.data.frame(mytextvariable);'
        , @input_data_1 = N''
    WITH RESULT SETS (([Col1] CHAR(20) NOT NULL));
    ```

    **Resultado**

    ![Resultados de la @script consulta mediante como entrada](./media/r-data-generated-output.png)

## <a name="next-steps"></a>Pasos siguientes

Examine algunos de los problemas que pueden surgir al pasar datos entre R y SQL Server, como conversiones implícitas y diferencias en los datos tabulares entre R y SQL.

> [!div class="nextstepaction"]
> [Inicio rápido: Controlar tipos de datos y objetos](quickstart-r-data-types-and-objects.md)