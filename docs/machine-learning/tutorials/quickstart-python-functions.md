---
title: 'Inicio rápido: funciones de Python'
description: En este inicio rápido, aprenderá a usar las funciones matemáticas y de utilidad de Python con SQL Server Machine Learning Services.
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/28/2020
ms.topic: quickstart
author: cawrites
ms.author: chadam
ms.reviewer: garye
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 6afe1685956c43e30ace59f3e5cc794a2abbd88f
ms.sourcegitcommit: dc965772bd4dbf8dd8372a846c67028e277ce57e
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/19/2020
ms.locfileid: "83606711"
---
# <a name="quickstart-python-functions-with-sql-server-machine-learning-services"></a>Inicio rápido: funciones de Python con SQL Server Machine Learning Services
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
En este inicio rápido, aprenderá a usar las funciones matemáticas y de utilidad de Python con [SQL Server Machine Learning Services](../sql-server-machine-learning-services.md) o en [clústeres de macrodatos](../../big-data-cluster/machine-learning-services.md). Las funciones estadísticas suelen ser complicadas de implementar en T-SQL, pero esto se puede hacer en Python con solo unas pocas líneas de código.
::: moniker-end
::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
En este inicio rápido, aprenderá a usar las funciones matemáticas y de utilidad de Python con [SQL Server Machine Learning Services](../sql-server-machine-learning-services.md). Las funciones estadísticas suelen ser complicadas de implementar en T-SQL, pero esto se puede hacer en Python con solo unas pocas líneas de código.
::: moniker-end

## <a name="prerequisites"></a>Prerrequisitos

- Para este inicio rápido, es necesario tener acceso a una instancia de SQL Server con [SQL Server Machine Learning Services](../install/sql-machine-learning-services-windows-install.md) que tenga instalado el lenguaje de Python.

  Su instancia de SQL Server puede estar en una máquina virtual de Azure o en un entorno local. Tenga en cuenta que la característica de scripts externos está deshabilitada de forma predeterminada, por lo que puede que tenga que [habilitar scripts externos](../install/sql-machine-learning-services-windows-install.md#bkmk_enableFeature) y asegurarse de que el **servicio SQL Server Launchpad** esté ejecutándose antes de empezar.

- También necesita una herramienta para ejecutar consultas SQL que contengan scripts de Python. Puede ejecutar estos scripts con cualquier herramienta de consultas o administración de bases de datos, siempre que pueda conectarse a una instancia de SQL Server y ejecutar una consulta T-SQL o un procedimiento almacenado. En este inicio rápido se utiliza [Azure Data Studio](https://docs.microsoft.com/sql/azure-data-studio/download-azure-data-studio).

## <a name="create-a-stored-procedure-to-generate-random-numbers"></a>Creación de un procedimiento almacenado para generar números aleatorios

Para simplificar, vamos a usar el paquete `numpy` de Python, que se instala y se carga de forma predeterminada en SQL Server Machine Learning Services con Python instalado. El paquete contiene cientos de funciones para tareas estadísticas comunes, entre otras, la función `random.normal`, que genera una cantidad determinada de números aleatorios que usan la distribución normal, dadas una desviación estándar y la media.

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

¿Qué ocurriría si quisiera facilitar la generación de un conjunto diferente de números aleatorios?

Es fácil cuando se combina con SQL Server. Defina un procedimiento almacenado que obtenga los argumentos del usuario y, a continuación, pase los argumentos al script de Python como variables.

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

Para crear un modelo de aprendizaje automático con Python en SQL Server, siga esta guía de inicio rápido:

> [!div class="nextstepaction"]
> [Inicio rápido: Crear y puntuar un modelo predictivo en Python con SQL Server Machine Learning Services](quickstart-python-train-score-model.md)

Para más información sobre SQL Server Machine Learning Services, vea:

- [¿Qué es SQL Server Machine Learning Services (Python y R)?](../sql-server-machine-learning-services.md)
