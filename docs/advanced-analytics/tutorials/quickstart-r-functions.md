---
title: 'Inicio rápido que muestra las funciones de R: SQL Server Machine Learning'
description: En esta guía de inicio rápido, aprenderá a escribir una función de R para el cálculo estadístico avanzado.
ms.prod: sql
ms.technology: machine-learning
ms.date: 01/04/2019
ms.topic: quickstart
author: dphansen
ms.author: davidph
ms.openlocfilehash: f43709f563d1dc5838cdd6636bcac4dc5664a6da
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/24/2019
ms.locfileid: "68469279"
---
# <a name="quickstart-using-r-functions"></a>Inicio rápido: Uso de funciones de R
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Si ha completado las guías de inicio rápido anteriores, está familiarizado con las operaciones básicas y está listo para algo más complejo, como las funciones estadísticas. Las funciones estadísticas avanzadas que son complicadas de implementar en T-SQL se pueden realizar en R con una sola línea de código.

En esta guía de inicio rápido, insertará funciones matemáticas y de utilidad de R en un SQL Server procedimiento almacenado.

## <a name="prerequisites"></a>Requisitos previos

En una guía de inicio rápido anterior, [Verify r existe en SQL Server](quickstart-r-verify.md), se proporciona información y vínculos para configurar el entorno de r necesario para esta guía de inicio rápido.

## <a name="create-a-stored-procedure-to-generate-random-numbers"></a>Crear un procedimiento almacenado para generar números aleatorios

Para simplificar, vamos a usar el `stats` paquete de r, que se instala y carga de forma predeterminada al instalar la compatibilidad con las características de r en SQL Server. El paquete contiene cientos de funciones para tareas estadísticas comunes, entre otras, la función `rnorm`, que genera una cantidad determinada de números aleatorios que usan la distribución normal, dadas una desviación estándar y la media.

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

Es fácil cuando se combina con SQL Server: defina un procedimiento almacenado que obtenga los argumentos del usuario. Luego, pase esos argumentos al script de R como variables.

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

De forma predeterminada, la instalación de R incluye `utils` el paquete, que proporciona una variedad de funciones de utilidad para investigar el entorno de R actual. Esto puede resultar útil si encuentra discrepancias en la forma en que el código de R se ejecuta en SQL Server y en entornos exteriores.

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

Muchos usuarios desean usar las funciones de control de tiempo del sistema de r `system.time` , `proc.time`como y, para capturar el tiempo utilizado por los procesos de r y analizar los problemas de rendimiento.

Para obtener un ejemplo, consulte este tutorial: [Crear características de datos](../tutorials/walkthrough-create-data-features.md). En este tutorial, las funciones de control de tiempo de R se incrustan en la solución para comparar el rendimiento de dos métodos para crear características a partir de los datos: Funciones de R frente a a funciones de T-SQL.

## <a name="next-steps"></a>Pasos siguientes

Después, compilará un modelo predictivo con R en SQL Server.

> [!div class="nextstepaction"]
> [Inicio rápido: Crear un modelo predictivo](quickstart-r-create-predictive-model.md)
