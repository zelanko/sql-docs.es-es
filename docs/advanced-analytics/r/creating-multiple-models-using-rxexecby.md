---
title: Crear varios modelos utilizando rxExecBy | Documentos de Microsoft
ms.custom: 
ms.date: 04/18/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: 55d194bf888defeebba64eeb4bb87ac04363cefb
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/25/2018
---
# <a name="creating-multiple-models-using-rxexecby"></a>Crear varios modelos utilizando rxExecBy

SQL Server de 2017 CTP 2.0 incluye una nueva función, **rxExecBy**, que admite el procesamiento en paralelo de varios modelos relacionados. En lugar de entrenar un modelo muy grande se basa en datos procedentes de varias entidades similar, los científicos de datos pueden crear rápidamente varios modelos relacionados, cada uno con los datos específicos de una sola entidad.

Por ejemplo, supongamos que está supervisando los errores de dispositivo y la captura de datos para muchos tipos distintos de los equipos. Mediante el uso de rxExecBy, puede proporcionar un único conjunto de datos grande como entrada, especificar una columna en el que se estratificar el conjunto de datos, como el tipo de dispositivo y, a continuación, crear varios modelos de modelos para los dispositivos individuales.

Este proceso se se denomina procesamiento "pleasingly paralelo", porque toma una tarea que era un poco costoso para los científicos de datos o en el mejor tedioso y realiza una operación rápida y sencilla.

Las aplicaciones típicas de este enfoque incluyen previsión para individuales metros inteligentes domésticos, crear pronósticos de los ingresos para las líneas de producto independiente o creación de modelos para aprobaciones de préstamo que se adapten a sucursales bancarias individuales.

## <a name="how-rxexec-works"></a>Cómo funciona rxExec

La función rxExecBy en RevoScaleR está diseñada para el procesamiento a través de un gran número de conjuntos de datos pequeños de paralelo de gran volumen.

1. Llame a la función rxExecBy como parte del código R y pasar un conjunto de datos de datos no ordenados.
2. Especificar la partición mediante el cual los datos deben agruparse y ordenarse.
3. Definir una transformación o función que se debe aplicar a cada partición de datos de modelado
4. Cuando se ejecuta la función, las consultas de datos se procesan en paralelo si su entorno lo admite. Además, las tareas de modelado o transformación se distribuye entre núcleos individuales y ejecutar en paralelo. Contexto de proceso admitidas para las tres operaciones incluyen RxSpark y RxInSQLServer.
5. Se devuelven varios resultados.

## <a name="rxexecby-syntax-and-examples"></a>rxExecBy sintaxis y ejemplos

**rxExecBy** toma cuatro entradas, una de las entradas que se va a un objeto de origen de datos o conjunto de datos que se puede crear particiones en un determinado **clave** columna. La función devuelve un resultado para cada partición. El formato del resultado depende de la función que se pasa como argumento, por ejemplo, si se pasa una función de modelado como rxLinMod, podría devolver un modelo entrenado independiente para cada partición del conjunto de datos.

### <a name="supported-functions"></a>Funciones admitidas

Modelado: `rxLinMod`, `rxLogit`, `rxGlm`,`rxDtree`

Puntuación: `rxPredict`,

Transformación o el análisis:`rxCovCor`

## <a name="example"></a>Ejemplo

En el ejemplo siguiente se muestra cómo crear varios modelos utilizando el conjunto de datos Airline, que se crean particiones en la columna [DayOfWeek]. La función definida por el usuario, `delayFunc`, se aplica a cada una de las particiones por rxExecBy que realiza la llamada. La función crea modelos independientes para el lunes, el martes, y así sucesivamente.

```SQL
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

Si se produce un error, `varsToPartition is invalid`, compruebe si el nombre de la columna de clave o columnas se ha escrito correctamente. El lenguaje R distingue mayúsculas de minúsculas.

Tenga en cuenta que este ejemplo no se optimiza para SQL Server y se puede realizar en muchos casos lograr un mejor rendimiento con SQL para agrupar los datos. Sin embargo, con rxExecBy, se pueden crear trabajos paralelos de R.

En el ejemplo siguiente se ilustra el proceso de R, utilizando SQL Server como el contexto de proceso:

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


