---
title: Guía de inicio rápido para trabajar con estructuras de datos en Python
description: En esta guía de inicio rápido para el script de Python en SQL Server, obtenga información sobre cómo usar estructuras de datos con el procedimiento almacenado del sistema sp_execute_external_script.
ms.prod: sql
ms.technology: machine-learning
ms.date: 01/04/2019
ms.topic: quickstart
author: dphansen
ms.author: davidph
ms.openlocfilehash: 17b2c150368b32960907d6fdd2e31b109f51d771
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/24/2019
ms.locfileid: "68469636"
---
# <a name="quickstart-python-data-structures-in-sql-server"></a>Inicio rápido: Estructuras de datos de Python en SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

En esta guía de inicio rápido se muestra cómo usar las estructuras de datos al usar Python en SQL Server Machine Learning Services.

SQL Server se basa en el paquete **pandas** de Python, que es ideal para trabajar con datos tabulares. Sin embargo, no puede pasar un valor escalar desde Python a SQL Server y esperar que funcione. En esta guía de inicio rápido, revisaremos algunas definiciones de tipos de datos básicas para prepararle problemas adicionales que podrían ocurrir al pasar datos tabulares entre Python y SQL Server.

+ Una trama de datos es una tabla con _varias_ columnas.
+ Una sola columna de una trama de bits es un objeto de tipo lista denominado serie.
+ Un valor único es una celda de una trama de datos y debe llamarse por índice.

¿Cómo se expondría el resultado único de un cálculo como una trama de datos, si un Data. Frame requiere una estructura tabular? Una respuesta es representar el valor escalar único como una serie, que se convierte fácilmente en una trama de datos. 

## <a name="prerequisites"></a>Requisitos previos

En una guía de inicio rápido anterior, [Compruebe que Python existe en SQL Server](quickstart-python-verify.md), proporciona información y vínculos para configurar el entorno de Python necesario para esta guía de inicio rápido.

## <a name="scalar-value-as-a-series"></a>Valor escalar como una serie

Este ejemplo realiza algunas operaciones matemáticas simples y convierte un valor escalar en una serie.

1. Una serie requiere un índice, que puede asignar manualmente, como se muestra aquí, o mediante programación.

    ```sql
    execute sp_execute_external_script 
    @language = N'Python', 
    @script = N'
    a = 1
    b = 2
    c = a/b
    print(c)
    s = pandas.Series(c, index =["simple math example 1"])
    print(s)
    '
    ```

2. Dado que la serie no se ha convertido a Data. Frame, los valores se devuelven en la ventana mensajes, pero puede ver que los resultados se encuentran en un formato más tabular.

    **Resultado**

    ```text
    STDOUT message(s) from external script: 
    0.5
    simple math example 1    0.5
    dtype: float64
    ```

3. Para aumentar la longitud de la serie, puede agregar nuevos valores mediante una matriz. 

    ```sql
    execute sp_execute_external_script 
    @language = N'Python', 
    @script = N'
    a = 1
    b = 2
    c = a/b
    d = a*b
    s = pandas.Series([c,d])
    print(s)
    '
    ```

    Si no especifica un índice, se genera un índice con valores que empiezan por 0 y terminan con la longitud de la matriz.

    **Resultado**

    ```text
    STDOUT message(s) from external script: 
    0    0.5
    1    2.0
    dtype: float64
    ```

4. Si aumenta el número de valores de **Índice** , pero no agrega nuevos valores de **datos** , los valores de datos se repiten para rellenar la serie.

    ```sql
    execute sp_execute_external_script 
    @language = N'Python', 
    @script = N'
    a = 1
    b = 2
    c = a/b
    s = pandas.Series(c, index =["simple math example 1", "simple math example 2"])
    print(s)
    '
    ```

    **Resultado**

    ```text
    STDOUT message(s) from external script: 
    0.5
    simple math example 1    0.5
    simple math example 2    0.5
    dtype: float64
    ```

## <a name="convert-series-to-data-frame"></a>Convertir series en tramas de datos

Después de convertir nuestros resultados matemáticos escalares en una estructura tabular, todavía necesitamos convertirlos a un formato que SQL Server pueda controlar. 

1. Para convertir una serie en Data. Frame, llame al método pandas de [trama](https://pandas.pydata.org/pandas-docs/stable/dsintro.html#dataframe) de datos.

    ```sql
    execute sp_execute_external_script 
    @language = N'Python', 
    @script = N'
    import pandas as pd
    a = 1
    b = 2
    c = a/b
    d = a*b
    s = pandas.Series([c,d])
    print(s)
    df = pd.DataFrame(s)
    OutputDataSet = df
    '
    WITH RESULT SETS (( ResultValue float ))
    ```

2. El resultado se muestra a continuación. Incluso si usa el índice para obtener valores específicos de Data. Frame, los valores de índice no forman parte de la salida.

    **Resultado**

    |ResultValue|
    |------|
    |0.5|
    |2|

## <a name="output-values-into-dataframe"></a>Los valores de salida en Data. Frame

Veamos cómo la conversión a Data. Frame funciona con nuestras dos series que contienen los resultados de operaciones matemáticas simples. El primero tiene un índice de valores secuenciales generados por Python. El segundo usa un índice arbitrario de valores de cadena.

1. En este ejemplo se obtiene un valor de la serie que utiliza un índice de entero.

    ```sql
    EXECUTE sp_execute_external_script 
    @language = N'Python', 
    @script = N'
    import pandas as pd
    a = 1
    b = 2
    c = a/b
    d = a*b
    s = pandas.Series([c,d])
    print(s)
    df = pd.DataFrame(s, index=[1])
    OutputDataSet = df
    '
    WITH RESULT SETS (( ResultValue float ))
    ```

    Recuerde que el índice generado automáticamente comienza en 0. Pruebe a usar un valor de índice fuera de intervalo y vea lo que sucede.

2. Ahora, vamos a obtener un valor único de la otra trama de datos que tiene un índice de cadena. 

    ```sql
    EXECUTE sp_execute_external_script 
    @language = N'Python', 
    @script = N'
    import pandas as pd
    a = 1
    b = 2
    c = a/b
    s = pandas.Series(c, index =["simple math example 1", "simple math example 2"])
    print(s)
    df = pd.DataFrame(s, index=["simple math example 1"])
    OutputDataSet = df
    '
    WITH RESULT SETS (( ResultValue float ))
    ```

    **Resultado**

    |ResultValue|
    |------|
    |0.5|

    Si intenta usar un índice numérico para obtener un valor de esta serie, obtendrá un error.

## <a name="next-steps"></a>Pasos siguientes

A continuación, creará un modelo predictivo con Python en SQL Server.

> [!div class="nextstepaction"]
> [Crear, entrenar y usar un modelo de Python con procedimientos almacenados en SQL Server](quickstart-python-train-score-in-tsql.md)