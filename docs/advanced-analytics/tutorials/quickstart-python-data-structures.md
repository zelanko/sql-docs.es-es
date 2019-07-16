---
title: 'Guía de inicio rápido para trabajar con estructuras de datos en Python: SQL Server Machine Learning'
description: En este inicio rápido para script de Python en SQL Server, obtenga información sobre cómo usar las estructuras de datos con el procedimiento almacenado del sistema de sp_execute_external_script.
ms.prod: sql
ms.technology: machine-learning
ms.date: 01/04/2019
ms.topic: quickstart
author: dphansen
ms.author: davidph
ms.openlocfilehash: ffbbd39c08221db4afa6427626ca618e04617166
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67962088"
---
# <a name="quickstart-python-data-structures-in-sql-server"></a>Inicio rápido: Estructuras de datos de Python en SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Este inicio rápido muestra cómo usar las estructuras de datos cuando se usa Python en SQL Server Machine Learning Services.

SQL Server se basa en la versión de Python **pandas** paquete, que resulta ideal para trabajar con datos tabulares. Sin embargo, no se puede pasar un valor escalar de Python para SQL Server y espera que "simplemente funcione". En este tutorial, revisaremos algunas definiciones de tipo de datos básicos para prepararse para problemas adicionales que podrían surgir cuando se pasan datos tabulares entre Python y SQL Server.

+ Una trama de datos es una tabla con _varios_ columnas.
+ Una sola columna de una trama de datos es un objeto de lista como llama a una serie.
+ Un valor único es una celda de una trama de datos y tiene que llamarse por índice.

¿Cómo podría exponer el resultado de un cálculo como una trama de datos único si data.frame requiere una estructura tabular? Una respuesta que se va a representar el único valor escalar como una serie, que fácilmente se convierte en una trama de datos. 

## <a name="prerequisites"></a>Requisitos previos

Un tutorial anterior, [Python Compruebe que existe en SQL Server](quickstart-python-verify.md), proporciona información y vínculos para configurar el entorno de Python necesario para este inicio rápido.

## <a name="scalar-value-as-a-series"></a>Valor escalar como una serie

En este ejemplo se hace un simple cálculo matemático y se convierte un valor escalar en una serie.

1. Una serie requiere un índice, que puede asignar manualmente, tal como se muestra a continuación, o mediante programación.

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

2. Dado que la serie no se ha convertido en un data.frame, se devuelven los valores en la ventana de mensajes, pero puede ver que los resultados están en formato tabular más.

    **Resultado**

    ```text
    STDOUT message(s) from external script: 
    0.5
    simple math example 1    0.5
    dtype: float64
    ```

3. Para aumentar la longitud de la serie, puede agregar nuevos valores utilizando una matriz. 

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

    Si no especifica un índice, se genera un índice que tiene valores empezando por 0 y finalizando con la longitud de la matriz.

    **Resultado**

    ```text
    STDOUT message(s) from external script: 
    0    0.5
    1    2.0
    dtype: float64
    ```

4. Si aumenta el número de **índice** valores, pero no agregue nuevos **datos** valores, los valores de datos se repiten para rellenar la serie.

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

## <a name="convert-series-to-data-frame"></a>Convertir serie en la trama de datos

Tener convertido nuestros resultados escalares matemáticas a una estructura tabular, necesitamos convertirlos a un formato que puede administrar SQL Server. 

1. Para convertir una serie en un data.frame, llame a la pandas [DataFrame](https://pandas.pydata.org/pandas-docs/stable/dsintro.html#dataframe) método.

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

2. El resultado se muestra a continuación. Incluso si utiliza el índice para obtener los valores específicos de la trama de datos, los valores de índice no forman parte de la salida.

    **Resultado**

    |ResultValue|
    |------|
    |0.5|
    |2|

## <a name="output-values-into-dataframe"></a>Valores de salida en data.frame

Veamos cómo funciona la conversión a un data.frame con nuestros dos series que contiene los resultados de operaciones matemáticas sencillas. La primera tiene un índice de valores secuenciales generados por Python. El segundo usa un índice de valores de cadena arbitrario.

1. En este ejemplo se obtiene un valor de la serie que utiliza un índice entero.

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

    Recuerde que el índice generado automáticamente comienza en 0. Pruebe a usar un valor fuera del intervalo índice y vea Qué sucede.

2. Ahora vamos a obtener un único valor desde el marco de datos que tiene un índice de cadena. 

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

A continuación, compilará un modelo predictivo con Python en SQL Server.

> [!div class="nextstepaction"]
> [Crear, entrenar y usar un modelo de Python con procedimientos almacenados en SQL Server](quickstart-python-train-score-in-tsql.md)