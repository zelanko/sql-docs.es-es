---
title: Escritura de funciones avanzadas de Python
titleSuffix: SQL Server Machine Learning Services
description: En esta guía de inicio rápido, aprenderá a escribir una función de Python para el cálculo estadístico avanzado con SQL Server Machine Learning Services.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/04/2019
ms.topic: quickstart
author: garyericson
ms.author: garye
ms.reviewer: davidph
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: e369e83c99543cc31287932a25949c2ddec98e89
ms.sourcegitcommit: 454270de64347db917ebe41c081128bd17194d73
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/07/2019
ms.locfileid: "72007725"
---
# <a name="quickstart-write-advanced-python-functions-with-sql-server-machine-learning-services"></a>Inicio rápido: Escritura de funciones avanzadas de Python con SQL Server Machine Learning Services
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

En esta guía de inicio rápido se describe cómo insertar funciones matemáticas y de utilidad de Python en un procedimiento almacenado de SQL con SQL Server Machine Learning Services. Las funciones estadísticas avanzadas que son complicadas de implementar en T-SQL se pueden realizar en Python con una sola línea de código.

## <a name="prerequisites"></a>Requisitos previos

- Esta guía de inicio rápido requiere acceso a una instancia de SQL Server con [SQL Server Machine Learning Services](../install/sql-machine-learning-services-windows-install.md) con el idioma de Python instalado.

  La instancia de SQL Server puede estar en una máquina virtual de Azure o en un entorno local. Tenga en cuenta que la característica de scripting externo está deshabilitada de forma predeterminada, por lo que es posible que tenga que [Habilitar el scripting externo](../install/sql-machine-learning-services-windows-install.md#bkmk_enableFeature) y comprobar que **SQL Server Launchpad servicio** se está ejecutando antes de empezar.

- También necesita una herramienta para ejecutar consultas SQL que contienen scripts de Python. Puede ejecutar estos scripts mediante cualquier herramienta de consulta o administración de bases de datos, siempre que pueda conectarse a una instancia de SQL Server y ejecutar una consulta T-SQL o un procedimiento almacenado. Esta guía de inicio rápido usa [SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/sql-server-management-studio-ssms).

## <a name="create-a-stored-procedure-to-generate-random-numbers"></a>Crear un procedimiento almacenado para generar números aleatorios

Para simplificar, vamos a usar el paquete python `numpy`, que se instala y carga de forma predeterminada en SQL Server Machine Learning Services con Python instalado. El paquete contiene cientos de funciones para tareas estadísticas comunes, entre otras, la función `random.normal`, que genera una cantidad determinada de números aleatorios que usan la distribución normal, dadas una desviación estándar y la media.

Por ejemplo, el siguiente código de Python devuelve 100 números en una media de 50, dada una desviación estándar de 3.

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

¿Y si quiere que sea más fácil generar otro conjunto de números aleatorios?

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

- La primera línea define cada uno de los parámetros de entrada de SQL que se requieren al ejecutar el procedimiento almacenado.

- La línea que comienza por `@params` define todas las variables que usa el código de Python y los tipos de datos de SQL correspondientes.

- Las líneas que siguen inmediatamente asignan los nombres de los parámetros SQL a los nombres de variables de Python correspondientes.

Ahora que ha ajustado la función de Python en un procedimiento almacenado, puede llamar fácilmente a la función y pasar valores diferentes, de la siguiente manera:

```sql
EXECUTE MyPyNorm @param1 = 100,@param2 = 50, @param3 = 3
```

## <a name="use-python-utility-functions-for-troubleshooting"></a>Usar funciones de utilidad de Python para solucionar problemas

Los paquetes de Python proporcionan una variedad de funciones de utilidad para investigar el entorno de Python actual. Estas funciones pueden ser útiles si encuentra discrepancias en la forma en que el código de Python realiza en SQL Server y en entornos externos.

Por ejemplo, puede usar las funciones de control de tiempo del sistema en el paquete `time` para medir la cantidad de tiempo que usan los procesos de Python y analizar los problemas de rendimiento.

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
> [Inicio rápido: Crear y puntuar un modelo predictivo en Python con SQL Server Machine Learning Services @ no__t-0

Para obtener más información acerca de SQL Server Machine Learning Services, consulte:

- [¿Qué es SQL Server Machine Learning Services (Python y R)?](../what-is-sql-server-machine-learning.md)
