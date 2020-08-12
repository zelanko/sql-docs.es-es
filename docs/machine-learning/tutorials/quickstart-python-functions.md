---
title: 'Inicio rápido: funciones de Python'
titleSuffix: SQL machine learning
description: En este inicio rápido, obtendrá información sobre cómo usar las funciones matemáticas y de utilidad de Python con el aprendizaje automático de SQL.
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/21/2020
ms.topic: quickstart
author: cawrites
ms.author: chadam
ms.reviewer: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=azuresqldb-mi-current||=sqlallproducts-allversions'
ms.openlocfilehash: 5aef8010c48e08931998f1bd7e49c3797ef4e81a
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85784091"
---
# <a name="quickstart-python-functions-with-sql-machine-learning"></a>Inicio rápido: Funciones de Python con aprendizaje automático de SQL
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
En este inicio rápido, aprenderá a usar las funciones matemáticas y de utilidad de Python con [SQL Server Machine Learning Services](../sql-server-machine-learning-services.md) o en [clústeres de macrodatos](../../big-data-cluster/machine-learning-services.md). Las funciones estadísticas suelen ser complicadas de implementar en T-SQL, pero esto se puede hacer en Python con solo unas pocas líneas de código.
::: moniker-end
::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
En este inicio rápido, aprenderá a usar las funciones matemáticas y de utilidad de Python con [SQL Server Machine Learning Services](../sql-server-machine-learning-services.md). Las funciones estadísticas suelen ser complicadas de implementar en T-SQL, pero esto se puede hacer en Python con solo unas pocas líneas de código.
::: moniker-end
::: moniker range="=azuresqldb-mi-current||=sqlallproducts-allversions"
En este inicio rápido, descubrirá cómo usar las funciones matemáticas y de utilidad de Python con [Machine Learning Services en Azure SQL Managed Instance](/azure/azure-sql/managed-instance/machine-learning-services-overview). Las funciones estadísticas suelen ser complicadas de implementar en T-SQL, pero esto se puede hacer en Python con solo unas pocas líneas de código.
::: moniker-end

## <a name="prerequisites"></a>Prerrequisitos

Para ejecutar este inicio rápido, debe cumplir los siguientes requisitos previos.

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
- SQL Server Machine Learning Services. Para obtener información sobre cómo instalar Machine Learning Services, vea la [Guía de instalación para Windows](../install/sql-machine-learning-services-windows-install.md) o la [Guía de instalación para Linux](../../linux/sql-server-linux-setup-machine-learning.md?toc=%2Fsql%2Fmachine-learning%2Ftoc.json). También puede [habilitar Machine Learning Services en clústeres de macrodatos de SQL Server](../../big-data-cluster/machine-learning-services.md).
::: moniker-end
::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
- SQL Server Machine Learning Services. SQL Server Machine Learning Services: para obtener información sobre cómo instalar Machine Learning Services, vea la [Guía de instalación para Windows](../install/sql-machine-learning-services-windows-install.md). 
::: moniker-end
::: moniker range="=azuresqldb-mi-current||=sqlallproducts-allversions"
- Machine Learning Services en Azure SQL Managed Instance. Para obtener información sobre cómo registrarse, vea la [información general de Machine Learning Services en Azure SQL Managed Instance](/azure/azure-sql/managed-instance/machine-learning-services-overview).
::: moniker-end

- Una herramienta para ejecutar consultas SQL que contengan scripts de Python. En este inicio rápido se utiliza [Azure Data Studio](../../azure-data-studio/what-is.md).

## <a name="create-a-stored-procedure-to-generate-random-numbers"></a>Creación de un procedimiento almacenado para generar números aleatorios

Para simplificar, vamos a usar el paquete `numpy` de Python, que se instala y carga de forma predeterminada. El paquete contiene cientos de funciones para tareas estadísticas comunes, entre otras, la función `random.normal`, que genera una cantidad determinada de números aleatorios que usan la distribución normal, dadas una desviación estándar y la media.

Por ejemplo, el siguiente código de Python devuelve 100 números en una media de 50, lo cual da una desviación estándar de 3.

```Python
numpy.random.normal(size=100, loc=50, scale=3)
```

Para llamar a esta línea de Python desde T-SQL, agregue la función de Python en el parámetro de script de Python de `sp_execute_external_script`. La salida espera una trama de datos, por lo que debe usar `pandas` para convertirla.

```sql
EXECUTE sp_execute_external_script @language = N'Python'
    , @script = N'
import numpy
import pandas
OutputDataSet = pandas.DataFrame(numpy.random.normal(size=100, loc=50, scale=3));
'
    , @input_data_1 = N'   ;'
WITH RESULT SETS(([Density] FLOAT NOT NULL));
```

¿Qué ocurriría si quisiera facilitar la generación de un conjunto diferente de números aleatorios? Defina un procedimiento almacenado que obtenga los argumentos del usuario y, a continuación, pase los argumentos al script de Python como variables.

```sql
CREATE PROCEDURE MyPyNorm (
      @param1 INT
    , @param2 INT
    , @param3 INT
    )
AS
EXECUTE sp_execute_external_script @language = N'Python'
    , @script = N'
import numpy
import pandas
OutputDataSet = pandas.DataFrame(numpy.random.normal(size=mynumbers, loc=mymean, scale=mysd));
'
    , @input_data_1 = N'   ;'
    , @params = N' @mynumbers int, @mymean int, @mysd int'
    , @mynumbers = @param1
    , @mymean = @param2
    , @mysd = @param3
WITH RESULT SETS(([Density] FLOAT NOT NULL));
```

- La primera línea define cada uno de los parámetros de entrada de SQL que son necesarios cuando se ejecuta el procedimiento almacenado.

- La línea que empieza con `@params` define todas las variables que usa el código de Python y los correspondientes tipos de datos SQL.

- Las líneas que siguen inmediatamente asignan los nombres de parámetro SQL a los valores de variables de Python correspondientes.

Ahora que ha ajustado la función de Python en un procedimiento almacenado, puede llamar a la función y pasar distintos valores fácilmente de la manera siguiente:

```sql
EXECUTE MyPyNorm @param1 = 100,@param2 = 50, @param3 = 3
```

## <a name="use-python-utility-functions-for-troubleshooting"></a>Usar funciones de utilidad de Python para solucionar problemas

Los paquetes de Python proporcionan una variedad de funciones de utilidad para investigar el entorno de Python actual. Estas funciones pueden ser útiles si encuentra discrepancias en la forma en que el código de Python se ejecuta en SQL Server y en entornos externos.

Por ejemplo, puede usar las funciones de temporización del sistema en el paquete `time` para medir la cantidad de tiempo que usan los procesos de Python y analizar los problemas de rendimiento.

```sql
EXECUTE sp_execute_external_script
      @language = N'Python'
    , @script = N'
import time
start_time = time.time()

# Run Python processes

elapsed_time = time.time() - start_time
'
    , @input_data_1 = N' ;';
```

## <a name="next-steps"></a>Pasos siguientes

Para crear un modelo de aprendizaje automático usando Python con aprendizaje automático de SQL, siga este inicio rápido:

> [!div class="nextstepaction"]
> [Inicio rápido: Creación y puntuación de un modelo predictivo en Python](quickstart-python-train-score-model.md)
