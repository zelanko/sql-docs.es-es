---
title: Fragmentación de análisis en RevoScaleR
description: 'Tutorial 12 de RevoScaleR: Fragmentación de datos para realizar análisis distribuidos mediante el lenguaje R en SQL Server.'
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 0ad082c3a21292b782d5888b48b698c986c0b5b2
ms.sourcegitcommit: 68583d986ff5539fed73eacb7b2586a71c37b1fa
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/04/2020
ms.locfileid: "81116808"
---
# <a name="perform-chunking-analysis-using-rxdatastep-sql-server-and-revoscaler-tutorial"></a>Fragmentación de análisis con rxDataStep (tutorial de SQL Server y RevoScaleR)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Este es el tutorial 12 de la [serie de tutoriales de RevoScaleR](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md) sobre el uso de las [funciones de RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) con SQL Server.

En este tutorial, usará la función **rxDataStep** para procesar datos en fragmentos, en lugar de requerir que el conjunto de datos completo se cargue en memoria y se procese de una vez, como ocurre en el lenguaje R tradicional. La función **rxDataStep** lee los datos en fragmentos, aplica funciones de R a cada fragmento de datos y, después, guarda los resultados de resumen de cada fragmento en un origen de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] común. Cuando se lean todos los datos, se combinan los resultados.

> [!TIP]
> En este tutorial, calculará una tabla de contingencia usando la función **table** de R. Este ejemplo se incluye únicamente con fines instructivos. 
> 
> Si necesita tabular conjuntos de datos reales, le recomendamos que use las funciones **rxCrossTabs** o **rxCube** de **RevoScaleR**, que se han optimizado para este tipo de operación.

## <a name="partition-data-by-values"></a>Partición de datos por valores

1. Cree una función de R personalizada que llame a la función **table** de R en cada fragmento de datos, y denomine la nueva función **ProcessChunk**.
  
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
  
3. Defina un origen de datos de SQL Server para almacenar los datos que está procesando. Comience por asignar una consulta de SQL a una variable. Luego, use esa variable en el argumento *sqlQuery* de un nuevo origen de datos de SQL Server.
  
    ```R
    dayQuery <-  "SELECT DayOfWeek FROM AirDemoSmallTest"
    inDataSource <- RxSqlServerData(sqlQuery = dayQuery,
        connectionString = sqlConnString,
        rowsPerRead = 50000,
        colInfo = list(DayOfWeek = list(type = "factor",
            levels = as.character(1:7))))
    ```

4. Opcionalmente, puede ejecutar **rxGetVarInfo** en este origen de datos. Llegado este punto, contiene una sola columna: *Var 1: DayOfWeek, Tipo: factor, no hay niveles de factor disponibles*
     
5. Antes de aplicar esta variable de factor en los datos de origen, cree una tabla independiente para contener los resultados intermedios. De nuevo, simplemente use la función **RxSqlServerData** para definir los datos, procurando eliminar cualquier tabla existente con el mismo nombre.
  
    ```R
    iroDataSource = RxSqlServerData(table = "iroResults",   connectionString = sqlConnString)
    # Check whether the table already exists.
    if (rxSqlServerTableExists(table = "iroResults",  connectionString = sqlConnString))  { rxSqlServerDropTable( table = "iroResults", connectionString = sqlConnString) }
    ```
  
7.  Llame a la función personalizada **ProcessChunk** para transformar los datos a medida que se leen, usándolos como el argumento *transformFunc* en la función **rxDataStep**.
  
    ```R
    rxDataStep( inData = inDataSource, outFile = iroDataSource, transformFunc = ProcessChunk, overwrite = TRUE)
    ```
  
8.  Para ver los resultados intermedios de **ProcessChunk**, asigne los resultados de **rxImport** a una variable y, después, imprima los resultados en la consola.
  
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

    **Resultados**

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