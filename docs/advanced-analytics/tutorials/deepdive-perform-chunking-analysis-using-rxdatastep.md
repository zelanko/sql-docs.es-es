---
title: Realizar análisis de fragmentación mediante RevoScaleR rxDataStep
description: Tutorial tutorial sobre cómo fragmentar los datos para el análisis distribuido mediante el lenguaje R en SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: ed22020b162bfac9f35eb8328ea6409903191a4c
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/01/2019
ms.locfileid: "68714894"
---
# <a name="perform-chunking-analysis-using-rxdatastep-sql-server-and-revoscaler-tutorial"></a>Realización de análisis de fragmentación mediante rxDataStep (tutorial de SQL Server y RevoScaleR)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Esta lección forma parte del [tutorial de RevoScaleR](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md) sobre cómo usar [las funciones de RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) con SQL Server.

En esta lección, usará la función **rxDataStep** para procesar los datos en fragmentos, en lugar de requerir que el conjunto de datos completo se cargue en memoria y se procese de una vez, como en R tradicional. Las funciones **rxDataStep** leen los datos en fragmentos, aplica las funciones de R a cada fragmento de datos a su vez y, a continuación, guarda los resultados de Resumen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de cada fragmento en un origen de datos común. Cuando se han leído todos los datos, se combinan los resultados.

> [!TIP]
> En esta lección, se calcula una tabla de contingencia mediante la función **TABLE** de R. Este ejemplo está pensado únicamente para fines informativos. 
> 
> Si necesita tabular conjuntos de datos del mundo real, se recomienda usar las funciones **rxCrossTabs** o **rxCube** en **RevoScaleR**, que están optimizadas para este tipo de operación.

## <a name="partition-data-by-values"></a>Particionar datos por valores

1. Cree una función personalizada de R que llame a la función de **tabla** de r en cada fragmento de datos y asigne un nombre a la nueva función **ProcessChunk**.
  
    ```R
    ProcessChunk <- function( dataList) {
    # Convert the input list to a data frame and compute contingency table
    chunkTable <- table(as.data.frame(dataList))
  
    # Convert table output to a data frame with a single row
    varNames <- names(chunkTable)
    varValues <- as.vector(chunkTable)
    dim(varValues) <- c(1, length(varNames))
    chunkDF <- as.data.frame(varValues)
    names(chunkDF) <- varNames
  
    # Return the data frame, which has a single row
    return( chunkDF )
    }
    ```

2. Establezca el contexto de cálculo en el servidor.
  
    ```R
    rxSetComputeContext(sqlCompute)
    ```
  
3. Defina un origen de datos de SQL Server para que contenga los datos que está procesando. Comience por asignar una consulta de SQL a una variable. A continuación, use esa variable en el argumento *sqlquery* de un nuevo origen de datos de SQL Server.
  
    ```R
    dayQuery <-  "SELECT DayOfWeek FROM AirDemoSmallTest"
    inDataSource <- RxSqlServerData(sqlQuery = dayQuery,
        connectionString = sqlConnString,
        rowsPerRead = 50000,
        colInfo = list(DayOfWeek = list(type = "factor",
            levels = as.character(1:7))))
    ```

4. Opcionalmente, puede ejecutar **rxGetVarInfo** en este origen de datos. En este punto, contiene una sola columna: *Var 1: DayOfWeek, tipo: factor, no hay niveles de factor disponibles*
     
5. Antes de aplicar esta variable de factor en los datos de origen, cree una tabla independiente para contener los resultados intermedios. De nuevo, solo tiene que usar la función **RxSqlServerData** para definir los datos, asegurándose de eliminar las tablas existentes del mismo nombre.
  
    ```R
    iroDataSource = RxSqlServerData(table = "iroResults",   connectionString = sqlConnString)
    # Check whether the table already exists.
    if (rxSqlServerTableExists(table = "iroResults",  connectionString = sqlConnString))  { rxSqlServerDropTable( table = "iroResults", connectionString = sqlConnString) }
    ```
  
7.  Llame a la función personalizada **ProcessChunk** para transformar los datos a medida que se leen, mediante el uso del argumento *transformFunc* para la función **rxDataStep** .
  
    ```R
    rxDataStep( inData = inDataSource, outFile = iroDataSource, transformFunc = ProcessChunk, overwrite = TRUE)
    ```
  
8.  Para ver los resultados intermedios de **ProcessChunk**, asigne los resultados de **rxImport** a una variable y, a continuación, genere los resultados en la consola.
  
    ```R
    iroResults <- rxImport(iroDataSource)
    iroResults
    ```

    **Resultados parciales**

    |      |    1  |   2   |  3   |  4   |  5  |   6   |  7 |
    | --- | ---  | --- | ---  |  ---  | ---  | ---  | --- |
    | 1 | 8228 | 8924 | 6916 | 6932 | 6944 | 5602 | 6454 |
    | 2  | 8321  | 5351 | 7329 | 7411 | 7409 | 6487 | 7692 |

9. Para calcular los resultados finales en todos los fragmentos, puede sumar las columnas y mostrar los resultados en la consola.

    ```R
    finalResults <- colSums(iroResults)
    finalResults
    ```

    **Resultado**

    1  |   2  |   3  |   4  |   5  |   6  |   7
    ---  |   ---  |   ---  |   ---  |   ---  |   ---  |   ---
    97975 | 77725 | 78875 | 81304 | 82987 | 86159 | 94975 

10. Para quitar la tabla de resultados intermedios, realice una llamada a **rxSqlServerDropTable**.
  
    ```R
    rxSqlServerDropTable( table = "iroResults", connectionString = sqlConnString)
    ```

## <a name="next-steps"></a>Pasos siguientes

> [!div class="nextstepaction"]
> [Tutoriales de R para SQL Server](sql-server-r-tutorials.md)