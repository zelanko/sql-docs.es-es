---
title: Trabajar con objetos y tipos de datos de Python y SQL
titleSuffix: SQL Server Machine Learning Services
description: En esta guía de inicio rápido, aprenderá a trabajar con tipos de datos y objetos de datos en Python y SQL Server con SQL Server Machine Learning Services.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/04/2019
ms.topic: quickstart
author: garyericson
ms.author: garye
ms.reviewer: davidph
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: c09c9ad4625520054f2d3f103ec055c37764aed2
ms.sourcegitcommit: 84e6922a57845a629391067ca4803e8d03e0ab90
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/07/2019
ms.locfileid: "72008432"
---
# <a name="quickstart-handle-data-types-and-objects-using-python-in-sql-server-machine-learning-services"></a>Inicio rápido: Control de tipos de datos y objetos mediante Python en SQL Server Machine Learning Services
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

En esta guía de inicio rápido se muestra cómo usar las estructuras de datos al usar Python en SQL Server Machine Learning Services.

SQL Server se basa en el paquete **pandas** de Python, que es ideal para trabajar con datos tabulares. Sin embargo, no puede pasar un valor escalar desde Python a SQL Server y esperar que funcione. En esta guía de inicio rápido, revisará algunas definiciones de tipos de datos básicas para prepararle problemas adicionales que podrían ocurrir al pasar datos tabulares entre Python y SQL Server.

Entre los conceptos que debe conocer por adelantado se incluyen:

- Una trama de datos es una tabla con _varias_ columnas.
- Una sola columna de una trama de datos es un objeto de tipo lista denominado serie.
- Un valor único de una trama de datos se denomina celda y se obtiene acceso a ella por índice.

¿Cómo se expondría el resultado único de un cálculo como una trama de datos, si un Data. Frame requiere una estructura tabular? Una respuesta es representar el valor escalar único como una serie, que se convierte fácilmente en una trama de datos. 

> [!NOTE]
> Cuando se devuelven fechas, Python en SQL usa DATETIME, que tiene un intervalo de fechas restringido de 1753-01-01 (-53690) a 9999-12-31 (2958463). 

## <a name="prerequisites"></a>Requisitos previos

- Esta guía de inicio rápido requiere acceso a una instancia de SQL Server con [SQL Server Machine Learning Services](../install/sql-machine-learning-services-windows-install.md) con el idioma de Python instalado.

- También necesita una herramienta para ejecutar consultas SQL que contienen scripts de Python. Puede ejecutar estos scripts mediante cualquier herramienta de consulta o administración de bases de datos, siempre que pueda conectarse a una instancia de SQL Server y ejecutar una consulta T-SQL o un procedimiento almacenado. Esta guía de inicio rápido usa [SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/sql-server-management-studio-ssms).

## <a name="scalar-value-as-a-series"></a>Valor escalar como una serie

Este ejemplo realiza algunas operaciones matemáticas simples y convierte un valor escalar en una serie.

1. Una serie requiere un índice, que puede asignar manualmente, como se muestra aquí, o mediante programación.

   ```sql
   EXECUTE sp_execute_external_script @language = N'Python'
       , @script = N'
   a = 1
   b = 2
   c = a/b
   print(c)
   s = pandas.Series(c, index =["simple math example 1"])
   print(s)
   '
   ```

   Dado que la serie no se ha convertido a Data. Frame, los valores se devuelven en la ventana mensajes, pero puede ver que los resultados se encuentran en un formato más tabular.

   **Resultado**

   ```text
   STDOUT message(s) from external script: 
   0.5
   simple math example 1    0.5
   dtype: float64
   ```

1. Para aumentar la longitud de la serie, puede agregar nuevos valores mediante una matriz. 

   ```sql
   EXECUTE sp_execute_external_script @language = N'Python'
       , @script = N'
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

1. Si aumenta el número de valores de **Índice** , pero no agrega nuevos valores de **datos** , los valores de datos se repiten para rellenar la serie.

   ```sql
   EXECUTE sp_execute_external_script @language = N'Python'
       , @script = N'
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

Después de convertir los resultados matemáticos escalares en una estructura tabular, debe convertirlos a un formato que SQL Server pueda controlar.

1. Para convertir una serie en Data. Frame, llame al método pandas de [trama](https://pandas.pydata.org/pandas-docs/stable/dsintro.html#dataframe) de datos.

   ```sql
   EXECUTE sp_execute_external_script @language = N'Python'
       , @script = N'
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
   WITH RESULT SETS((ResultValue FLOAT))
   ```

   El resultado se muestra a continuación. Incluso si usa el índice para obtener valores específicos de Data. Frame, los valores de índice no forman parte de la salida.

   **Resultado**

   |ResultValue|
   |------|
   |0.5|
   |2|

## <a name="output-values-into-dataframe"></a>Los valores de salida en Data. Frame

Ahora se mostrarán los valores específicos de dos series de resultados matemáticos en Data. Frame. El primero tiene un índice de valores secuenciales generados por Python. El segundo usa un índice arbitrario de valores de cadena.

1. En el ejemplo siguiente se obtiene un valor de la serie utilizando un índice de entero.

   ```sql
   EXECUTE sp_execute_external_script @language = N'Python'
       , @script = N'
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
   WITH RESULT SETS((ResultValue FLOAT))
   ```

   **Resultado**

   |ResultValue|
   |------|
   |2.0|

   Recuerde que el índice generado automáticamente comienza en 0. Pruebe a usar un valor de índice fuera de intervalo y vea lo que sucede.

1. Ahora obtenga un valor único de la otra trama de datos mediante un índice de cadena.

   ```sql
   EXECUTE sp_execute_external_script @language = N'Python'
       , @script = N'
   import pandas as pd
   a = 1
   b = 2
   c = a/b
   s = pandas.Series(c, index =["simple math example 1", "simple math example 2"])
   print(s)
   df = pd.DataFrame(s, index=["simple math example 1"])
   OutputDataSet = df
   '
   WITH RESULT SETS((ResultValue FLOAT))
   ```

   **Resultado**

   |ResultValue|
   |------|
   |0.5|

   Si intenta usar un índice numérico para obtener un valor de esta serie, obtendrá un error.

## <a name="next-steps"></a>Pasos siguientes

Para obtener información sobre cómo escribir funciones avanzadas de Python en SQL Server, siga esta guía de inicio rápido:

> [!div class="nextstepaction"]
> [Escritura de funciones avanzadas de Python con SQL Server Machine Learning Services](quickstart-python-functions.md)

Para obtener más información sobre el uso de Python en SQL Server Machine Learning Services, consulte los siguientes artículos:

- [Crear y puntuar un modelo predictivo en Python](quickstart-python-train-score-model.md)
- [¿Qué es SQL Server Machine Learning Services (Python y R)?](../what-is-sql-server-machine-learning.md)
