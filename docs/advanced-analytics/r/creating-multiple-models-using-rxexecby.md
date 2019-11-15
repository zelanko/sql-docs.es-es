---
title: Creación de varios modelos con rxExecBy
description: Use la función rxExecBy de la biblioteca de RevoScaleR para compilar varios minimodelos en los datos de la máquina almacenados en SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: dbba63ae69997c9c5dbdccf49ec590b3f4eba652
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/07/2019
ms.locfileid: "73727486"
---
# <a name="creating-multiple-models-using-rxexecby"></a>Crear varios modelos mediante rxExecBy
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

La función **rxExecBy** de RevoScaleR admite el procesamiento en paralelo de varios modelos relacionados. En lugar de entrenar un modelo grande en función de los datos de varias entidades similares, un científico de datos puede crear rápidamente muchos modelos relacionados, cada uno con datos específicos de una sola entidad. 

Por ejemplo, supongamos que está supervisando los errores del dispositivo y captura los datos para muchos tipos diferentes de equipos. Mediante rxExecBy, puede proporcionar un único conjunto de datos grande como entrada, especificar una columna en la que quiera estratificar el conjunto de datos —por ejemplo, el tipo de dispositivo—, y, después, crear varios modelos para dispositivos individuales.

Este caso de uso se ha denominado ["pleasingly parallel"](https://en.wikipedia.org/wiki/Embarrassingly_parallel) (agradablemente paralelo) ya que divide un problema complejo grande en partes componentes para un procesamiento simultáneo.

Entre las aplicaciones típicas de este enfoque se incluye la previsión de los medidores inteligentes domésticos individuales, la creación de proyecciones de ingresos para líneas de productos independientes o la creación de modelos para aprobaciones de préstamos que se adaptan a sucursales bancarias individuales.

## <a name="how-rxexec-works"></a>Funcionamiento de rxExec

La función rxExecBy de RevoScaleR está diseñada para el procesamiento paralelo de gran volumen en un gran número de conjuntos de datos pequeños.

1. Llame a la función rxExecBy como parte del código de R y pase un conjunto de datos no ordenados.
2. Especifique la partición por la que se deben agrupar y ordenar los datos.
3. Defina una función de transformación o modelado que se deba aplicar a cada partición de datos.
4. Cuando se ejecuta la función, las consultas de datos se procesan en paralelo si su entorno lo admite. Además, las tareas de modelado o transformación se distribuyen entre núcleos individuales y se ejecutan en paralelo. RxSpark y RxInSQLServer son contextos de proceso admitidos.
5. Se devuelven varios resultados.

## <a name="rxexecby-syntax-and-examples"></a>Sintaxis y ejemplos de rxExecBy

**rxExecBy** toma cuatro entradas, una de las cuales es un conjunto de datos o un objeto de origen de datos que se puede particionar en una columna **key** especificada. La función devuelve una salida para cada partición. La forma de la salida depende de la función que se pasa como argumento. Por ejemplo, si se pasa una función de modelado como rxLinMod, podría devolver un modelo entrenado independiente para cada partición del conjunto de datos.

### <a name="supported-functions"></a>Funciones admitidas

Modelado: `rxLinMod`, `rxLogit`, `rxGlm`, `rxDtree`

Puntuación: `rxPredict`

Transformación o análisis: `rxCovCor`

## <a name="example"></a>Ejemplo

En el ejemplo siguiente se muestra cómo crear varios modelos mediante el conjunto de datos Airline, que está particionado en la columna [DayOfWeek]. La función definida por el usuario, `delayFunc`, se aplica a cada una de las particiones mediante una llamada a rxExecBy. La función crea modelos independientes para los lunes, los martes, etc.

```sql
EXEC sp_execute_external_script
@language = N'R'
, @script = N'
delayFunc <- function(key, data, params) { 
    df <- rxImport(inData = airlineData) 
    rxLinMod(ArrDelay ~ CRSDepTime, data = df) 
} 
OutputDataSet <- rxExecBy(airlineData, c("DayOfWeek"), delayFunc)
'
, @input_data_1 = N'select ArrDelay, DayOfWeek, CRSDepTime from AirlineDemoSmall]'
, @input_data_1_name = N'airlineData'

```

Si obtiene el error `varsToPartition is invalid`, compruebe si el nombre de la columna o columnas de clave está escrito correctamente. El lenguaje de R distingue mayúsculas de minúsculas.

Este ejemplo concreto no está optimizado para SQL Server y, en muchos casos, puede lograr un mejor rendimiento si usa SQL para agrupar los datos. Sin embargo, con rxExecBy, puede crear trabajos paralelos desde R.

En el ejemplo siguiente se muestra el proceso en R, usando SQL Server como contexto de proceso:

```R
sqlServerConnString <- "SERVER=hostname;DATABASE=TestDB;UID=DBUser;PWD=Password;"
inTable <- paste("airlinedemosmall")
sqlServerDataDS <- RxSqlServerData(table = inTable, connectionString = sqlServerConnString)

# user function
".Count" <- function(keys, data, params)
{
  myDF <- rxImport(inData = data)
  return (nrow(myDF))
}

# Set SQL Server compute context with level of parallelism = 2
sqlServerCC <- RxInSqlServer(connectionString = sqlServerConnString, numTasks = 4)
rxSetComputeContext(sqlServerCC)

# Execute rxExecBy in SQL Server compute context
sqlServerCCResults <- rxExecBy(inData = sqlServerDataDS, keys = c("DayOfWeek"), func = .Count)
```


