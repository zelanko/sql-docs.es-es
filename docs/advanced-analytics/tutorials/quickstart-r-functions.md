---
title: 'Inicio rápido: funciones de R'
description: En este inicio rápido, aprenderá a usar las funciones matemáticas y de utilidad de R con SQL Server Machine Learning Services.
ms.prod: sql
ms.technology: machine-learning
ms.date: 01/27/2020
ms.topic: quickstart
author: garyericson
ms.author: garye
ms.reviewer: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: e67dcbc35bf5af88d2a7fab37f795cd5cc1d55d9
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/29/2020
ms.locfileid: "76831773"
---
# <a name="quickstart-r-functions-with-sql-server-machine-learning-services"></a>Inicio rápido: funciones de R con SQL Server Machine Learning Services
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

En este inicio rápido, aprenderá a usar las funciones matemáticas y de utilidad de R con SQL Server Machine Learning Services. Las funciones estadísticas suelen ser complicadas de implementar en T-SQL, pero esto se puede hacer en R con solo unas pocas líneas de código.

## <a name="prerequisites"></a>Prerrequisitos

- Para este inicio rápido, es necesario tener acceso a una instancia de SQL Server con [SQL Server Machine Learning Services](../install/sql-machine-learning-services-windows-install.md) que tenga instalado el lenguaje de R.

  Su instancia de SQL Server puede estar en una máquina virtual de Azure o en un entorno local. Tenga en cuenta que la característica de scripts externos está deshabilitada de forma predeterminada, por lo que puede que tenga que [habilitar scripts externos](../install/sql-machine-learning-services-windows-install.md#bkmk_enableFeature) y asegurarse de que el **servicio SQL Server Launchpad** esté ejecutándose antes de empezar.

- También necesita una herramienta para ejecutar consultas SQL que contengan scripts de R. Puede ejecutar estos scripts con cualquier herramienta de consultas o administración de bases de datos, siempre que pueda conectarse a una instancia de SQL Server y ejecutar una consulta T-SQL o un procedimiento almacenado. En este inicio rápido, se usa [SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/sql-server-management-studio-ssms).

## <a name="create-a-stored-procedure-to-generate-random-numbers"></a>Creación de un procedimiento almacenado para generar números aleatorios

Para simplificar, vamos a usar el paquete `stats` de R, que se instala y se carga de forma predeterminada en SQL Server Machine Learning Services con R instalado. El paquete contiene cientos de funciones para tareas estadísticas comunes, entre otras, la función `rnorm`, que genera una cantidad determinada de números aleatorios que usan la distribución normal, dadas una desviación estándar y la media.

Por ejemplo, el siguiente código de R devuelve 100 números en una media de 50, lo cual da una desviación estándar de 3.

```R
as.data.frame(rnorm(100, mean = 50, sd = 3));
```

Para llamar a esta línea de R desde T-SQL, agregue la función de R del parámetro de script de `sp_execute_external_script`, de la manera siguiente:

```sql
EXECUTE sp_execute_external_script
      @language = N'R'
    , @script = N'
         OutputDataSet <- as.data.frame(rnorm(100, mean = 50, sd =3));'
    , @input_data_1 = N'   ;'
      WITH RESULT SETS (([Density] float NOT NULL));
```

¿Qué ocurriría si quisiera facilitar la generación de un conjunto diferente de números aleatorios?

Es fácil cuando se combina con SQL Server. Defina un procedimiento almacenado que obtenga los argumentos del usuario y, a continuación, pase los argumentos al script de R como variables.

```sql
CREATE PROCEDURE MyRNorm (
    @param1 INT
    , @param2 INT
    , @param3 INT
    )
AS
EXECUTE sp_execute_external_script @language = N'R'
    , @script = N'
         OutputDataSet <- as.data.frame(rnorm(mynumbers, mymean, mysd));'
    , @input_data_1 = N'   ;'
    , @params = N' @mynumbers int, @mymean int, @mysd int'
    , @mynumbers = @param1
    , @mymean = @param2
    , @mysd = @param3
WITH RESULT SETS(([Density] FLOAT NOT NULL));
```

- La primera línea define cada uno de los parámetros de entrada de SQL que son necesarios cuando se ejecuta el procedimiento almacenado.

- La línea que comienza con `@params` define todas las variables usadas por el código de R y los correspondientes tipos de datos de SQL.

- Las líneas inmediatamente a continuación asignan los nombres de parámetro de SQL a los nombres de variable de R correspondientes.

Ahora que ha ajustado la función de R en un procedimiento almacenado, puede llamar a la función fácilmente y pasar distintos valores, como a continuación:

```sql
EXECUTE MyRNorm @param1 = 100,@param2 = 50, @param3 = 3
```

## <a name="use-r-utility-functions-for-troubleshooting"></a>Uso de funciones de utilidad de R para solucionar problemas

El paquete **utils**, instalado de forma predeterminada, ofrece diversas funciones de utilidad para investigar el entorno actual de R. Estas funciones pueden ser útiles si encuentra discrepancias en la forma en que el código de R se ejecuta en SQL Server y en entornos externos.

Por ejemplo, podría usar la función `memory.limit()` de R para obtener memoria para el entorno actual de R. Dado que el paquete `utils` está instalado pero no se carga de forma predeterminada, debe usar la función `library()` para cargarlo primero.

```sql
EXECUTE sp_execute_external_script
      @language = N'R'
    , @script = N'
        library(utils);
        mymemory <- memory.limit();
        OutputDataSet <- as.data.frame(mymemory);'
    , @input_data_1 = N' ;'
WITH RESULT SETS (([Col1] int not null));
```

> [!TIP]
> Muchos usuarios quieren usar las funciones de control de tiempo del sistema de R, como `system.time` y `proc.time`, para capturar el tiempo que tardan los procesos de R y analizar problemas de rendimiento. Para obtener un ejemplo, vea el tutorial [Creación de características de datos](../tutorials/walkthrough-create-data-features.md) donde las funciones de control de tiempo de R se incrustan en la solución.

## <a name="next-steps"></a>Pasos siguientes

Para crear un modelo de aprendizaje automático con R en SQL Server, siga esta guía de inicio rápido:

> [!div class="nextstepaction"]
> [Creación y puntuación de un modelo predictivo en R con SQL Server Machine Learning Services](quickstart-r-train-score-model.md)

Para más información sobre SQL Server Machine Learning Services, vea:

- [¿Qué es SQL Server Machine Learning Services (Python y R)?](../what-is-sql-server-machine-learning.md)
