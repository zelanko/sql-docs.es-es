---
title: Uso de funciones de R con datos de SQL Server (R en Inicio rápido de SQL) | Documentos de Microsoft
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 52b03b16c55b4ae8a772c2c12861fcc4b184d1f4
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/04/2018
ms.locfileid: "34585747"
---
# <a name="using-r-functions-with-sql-server-data-r-in-sql-quickstart"></a>Uso de funciones de R con datos de SQL Server (R en Inicio rápido de SQL)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Ahora que está familiarizado con las operaciones básicas, ha llegado el momento de divertirse un poco con R. Por ejemplo, es posible que sea complicado implementar muchas funciones estadísticas avanzadas con T-SQL, pero únicamente se necesita una sola línea de código de R.  Con R Services, resulta fácil insertar scripts de utilidad de R en un procedimiento almacenado.

En estos ejemplos, insertará funciones matemáticas y de utilidad de R en un procedimiento almacenado de SQL Server.

## <a name="create-a-stored-procedure-to-generate-random-numbers"></a>Crear un procedimiento almacenado para generar números aleatorios

Para simplificar, vamos a usar el objeto R `stats` paquete, que se instala y se cargan de forma predeterminada con R Services. El paquete contiene cientos de funciones para tareas estadísticas comunes, entre otras, la función `rnorm`, que genera una cantidad determinada de números aleatorios que usan la distribución normal, dadas una desviación estándar y la media.

Por ejemplo, esté código de R devuelve 100 números en una media de 50, dada una desviación estándar de 3.

```R
as.data.frame(rnorm(100, mean = 50, sd = 3));
```

Para llamar a esta línea de R desde T-SQL, ejecute sp_execute_external_script y agregue la función de R del parámetro de script de R, de la manera siguiente:

```sql
EXEC sp_execute_external_script
      @language = N'R'
    , @script = N'
         OutputDataSet <- as.data.frame(rnorm(100, mean = 50, sd =3));'
    , @input_data_1 = N'   ;'
      WITH RESULT SETS (([Density] float NOT NULL));
```

¿Y si quiere que sea más fácil generar otro conjunto de números aleatorios?

Que es fácil cuando se combina con SQL Server: defina un procedimiento almacenado que obtiene los argumentos del usuario. Luego, pase esos argumentos al script de R como variables.

```sql
CREATE PROCEDURE MyRNorm (@param1 int, @param2 int, @param3 int)
AS
    EXEC sp_execute_external_script
      @language = N'R'
    , @script = N'
         OutputDataSet <- as.data.frame(rnorm(mynumbers, mymean, mysd));'
    , @input_data_1 = N'   ;'
    , @params = N' @mynumbers int, @mymean int, @mysd int'
    , @mynumbers = @param1
    , @mymean = @param2
    , @mysd = @param3
    WITH RESULT SETS (([Density] float NOT NULL));
```

+ La primera línea define cada uno de los parámetros de entrada de SQL que se requieren al ejecutar el procedimiento almacenado.

+ La línea que empieza con `@params` define todas las variables que usa el código de R y los correspondientes tipos de datos SQL.

+ Las líneas que siguen inmediatamente asignan los nombres de parámetro SQL a los valores de variables de R correspondientes.

Ahora que ha ajustado la función de R en un procedimiento almacenado, puede llamar a la función y pasar distintos valores fácilmente, de la manera siguiente:

```sql
EXEC MyRNorm @param1 = 100,@param2 = 50, @param3 = 3
```

## <a name="use-r-utility-functions-for-troubleshooting"></a>Usar funciones de utilidad de R para solucionar problemas

De forma predeterminada, una instalación de R incluye el `utils` paquete, que proporciona una variedad de funciones de utilidad para investigar el actual entorno de R. Esto puede resultar útil si encuentra discrepancias en la forma en que el código de R se ejecuta en SQL Server y en entornos exteriores.

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

Al igual que muchos usuarios usar las funciones de control de tiempo de sistema de R, como `system.time` y `proc.time`, para capturar el tiempo utilizado por los procesos de R y analizar problemas de rendimiento.

Para obtener un ejemplo, vea este tutorial: [Crear características de datos](../tutorials/walkthrough-create-data-features.md). En este tutorial, se insertan funciones de control de tiempo de R en la solución para comparar el rendimiento de dos métodos para crear características de datos: funciones de R frente a funciones de T-SQL.

## <a name="next-lesson"></a>Lección siguiente

Después, compilará un modelo predictivo con R en SQL Server.

[Crear un modelo predictivo](../tutorials/rtsql-create-a-predictive-model-r.md)
