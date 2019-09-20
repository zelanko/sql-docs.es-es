---
title: Escritura de funciones avanzadas de R
titleSuffix: SQL Server Machine Learning Services
description: En esta guía de inicio rápido, aprenderá a escribir una función de R para el cálculo estadístico avanzado con SQL Server Machine Learning Services.
ms.prod: sql
ms.technology: machine-learning
ms.date: 09/17/2019
ms.topic: quickstart
author: garyericson
ms.author: garye
ms.reviewer: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: cebd4ea6a356af6802a0e26f778667b2acc4b80c
ms.sourcegitcommit: 1661c3e1bb38ed12f8485c3860fc2d2b97dd2c9d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/20/2019
ms.locfileid: "71149908"
---
# <a name="quickstart-write-advanced-r-functions-with-sql-server-machine-learning-services"></a>Inicio rápido: Escritura de funciones avanzadas de R con SQL Server Machine Learning Services
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

En esta guía de inicio rápido se describe cómo insertar funciones matemáticas y de utilidad de R en un procedimiento almacenado de SQL con SQL Server Machine Learning Services. Las funciones estadísticas avanzadas que son complicadas de implementar en T-SQL se pueden realizar en R con una sola línea de código.

## <a name="prerequisites"></a>Requisitos previos

- Esta guía de inicio rápido requiere acceso a una instancia de SQL Server con [SQL Server Machine Learning Services](../install/sql-machine-learning-services-windows-install.md) con el lenguaje R instalado.

  La instancia de SQL Server puede estar en una máquina virtual de Azure o en un entorno local. Tenga en cuenta que la característica de scripting externo está deshabilitada de forma predeterminada, por lo que es posible que tenga que [Habilitar el scripting externo](../install/sql-machine-learning-services-windows-install.md#bkmk_enableFeature) y comprobar que **SQL Server Launchpad servicio** se está ejecutando antes de empezar.

- También necesita una herramienta para ejecutar consultas SQL que contienen scripts de R. Puede ejecutar estos scripts mediante cualquier herramienta de consulta o administración de bases de datos, siempre que pueda conectarse a una instancia de SQL Server y ejecutar una consulta T-SQL o un procedimiento almacenado. Esta guía de inicio rápido usa [SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/sql-server-management-studio-ssms).

## <a name="create-a-stored-procedure-to-generate-random-numbers"></a>Crear un procedimiento almacenado para generar números aleatorios

Para simplificar, vamos a usar el `stats` paquete de R, que se instala y carga de forma predeterminada en SQL Server Machine Learning Services con R instalado. El paquete contiene cientos de funciones para tareas estadísticas comunes, entre otras, la función `rnorm`, que genera una cantidad determinada de números aleatorios que usan la distribución normal, dadas una desviación estándar y la media.

Por ejemplo, el siguiente código R devuelve 100 números en una media de 50, dada una desviación estándar de 3.

```R
as.data.frame(rnorm(100, mean = 50, sd = 3));
```

Para llamar a esta línea de r desde T-SQL, agregue la función de r en el parámetro script `sp_execute_external_script`de r de, como se indica a continuación:

```sql
EXEC sp_execute_external_script
      @language = N'R'
    , @script = N'
         OutputDataSet <- as.data.frame(rnorm(100, mean = 50, sd =3));'
    , @input_data_1 = N'   ;'
      WITH RESULT SETS (([Density] float NOT NULL));
```

¿Y si quiere que sea más fácil generar otro conjunto de números aleatorios?

Es fácil cuando se combina con SQL Server. Defina un procedimiento almacenado que obtenga los argumentos del usuario y, a continuación, pase los argumentos al script de R como variables.

```sql
CREATE PROCEDURE MyRNorm (
    @param1 INT
    , @param2 INT
    , @param3 INT
    )
AS
EXEC sp_execute_external_script @language = N'R'
    , @script = N'
         OutputDataSet <- as.data.frame(rnorm(mynumbers, mymean, mysd));'
    , @input_data_1 = N'   ;'
    , @params = N' @mynumbers int, @mymean int, @mysd int'
    , @mynumbers = @param1
    , @mymean = @param2
    , @mysd = @param3
WITH RESULT SETS(([Density] FLOAT NOT NULL));
```

- La primera línea define cada uno de los parámetros de entrada de SQL que se requieren al ejecutar el procedimiento almacenado.

- La línea que empieza con `@params` define todas las variables que usa el código de R y los correspondientes tipos de datos SQL.

- Las líneas que siguen inmediatamente asignan los nombres de parámetro SQL a los valores de variables de R correspondientes.

Ahora que ha ajustado la función de R en un procedimiento almacenado, puede llamar a la función y pasar distintos valores fácilmente, de la manera siguiente:

```sql
EXEC MyRNorm @param1 = 100,@param2 = 50, @param3 = 3
```

## <a name="use-r-utility-functions-for-troubleshooting"></a>Usar funciones de utilidad de R para solucionar problemas

El paquete de **utils** , que se instala de forma predeterminada, proporciona una variedad de funciones de utilidad para investigar el entorno de R actual. Estas funciones pueden ser útiles si encuentra discrepancias en la forma en que el código de R realiza en SQL Server y en entornos externos.

Por ejemplo, puede usar la función `memory.limit()` de R para obtener memoria para el entorno actual de R. Dado que el paquete `utils` se instala pero no se carga de manera predeterminada, debe usar primero la función `library()` para cargarlo.

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
> Muchos usuarios desean usar las funciones de control de tiempo del sistema de r `system.time` , `proc.time`como y, para capturar el tiempo utilizado por los procesos de r y analizar los problemas de rendimiento.

Para obtener un ejemplo, consulte este tutorial: [Crear características de datos](../tutorials/walkthrough-create-data-features.md). En este tutorial, las funciones de control de tiempo de R se incrustan en la solución para comparar el rendimiento de las funciones de R y Funciones de T-SQL para crear características a partir de datos.

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información acerca de SQL Server Machine Learning Services, consulte:

- [¿Qué es SQL Server Machine Learning Services (Python y R)?](../what-is-sql-server-machine-learning.md)
