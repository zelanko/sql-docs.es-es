---
title: 'Realizar análisis de fragmentación mediante rxDataStep RevoScaleR: SQL Server Machine Learning'
description: Tutorial del tutorial sobre cómo fragmentar los datos para el análisis distribuido mediante el lenguaje R en SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.openlocfilehash: 6ccc64c98f0519b33b6ba9da180c01e4478492f6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67962208"
---
# <a name="perform-chunking-analysis-using-rxdatastep-sql-server-and-revoscaler-tutorial"></a>Realizar análisis de fragmentación mediante rxDataStep (tutorial de SQL Server y RevoScaleR)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

En esta lección forma parte de la [RevoScaleR tutorial](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md) sobre cómo usar [funciones de RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) con SQL Server.

En esta lección, usará el **rxDataStep** función para procesar los datos en fragmentos, en lugar de requerir que todo el conjunto de datos se cargan en memoria y procesar al mismo tiempo, como en r tradicional El **rxDataStep** funciones lee los datos en fragmentos, se aplica a las funciones de R para cada fragmento de datos a su vez y, a continuación, guarda los resultados de resumen para cada fragmento en una común [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] origen de datos. Cuando se ha leído todos los datos, se combinan los resultados.

> [!TIP]
> En esta lección, calcule una tabla de contingencia con los **tabla** función en R. Este ejemplo está pensado únicamente con fines informativos. 
> 
> Si necesita tabular conjuntos de datos del mundo real, se recomienda usar la **rxCrossTabs** o **rxCube** las funciones de **RevoScaleR**, que están optimizados para este tipo de operación.

## <a name="partition-data-by-values"></a>Crear particiones de datos por valores

1. Cree una función de R personalizada que llama el R **tabla** funcionan en cada fragmento de datos y el nombre de la nueva función **ProcessChunk**.
  
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
  
3. Definir un origen de datos de SQL Server para almacenar los datos que está procesando. Comience por asignar una consulta de SQL a una variable. A continuación, usar esa variable en el *sqlQuery* argumento de un nuevo origen de datos de SQL Server.
  
    ```R
    dayQuery <-  "SELECT DayOfWeek FROM AirDemoSmallTest"
    inDataSource <- RxSqlServerData(sqlQuery = dayQuery,
        connectionString = sqlConnString,
        rowsPerRead = 50000,
        colInfo = list(DayOfWeek = list(type = "factor",
            levels = as.character(1:7))))
    ```

4. Si lo desea, puede ejecutar **rxGetVarInfo** en este origen de datos. En este momento, contiene una sola columna: *Var 1: DayOfWeek, tipo: factor, no hay niveles de factor disponibles*
     
5. Antes de aplicar esta variable de factor en los datos de origen, cree una tabla independiente para contener los resultados intermedios. De nuevo, use simplemente el **RxSqlServerData** función para definir los datos, asegúrese de eliminar las tablas existentes del mismo nombre.
  
    ```R
    iroDataSource = RxSqlServerData(table = "iroResults",   connectionString = sqlConnString)
    # Check whether the table already exists.
    if (rxSqlServerTableExists(table = "iroResults",  connectionString = sqlConnString))  { rxSqlServerDropTable( table = "iroResults", connectionString = sqlConnString) }
    ```
  
7.  Llame a la función personalizada **ProcessChunk** para transformar los datos a medida que se lee usándolos como el *transformFunc* argumento para el **rxDataStep** función.
  
    ```R
    rxDataStep( inData = inDataSource, outFile = iroDataSource, transformFunc = ProcessChunk, overwrite = TRUE)
    ```
  
8.  Para ver los resultados intermedios de **ProcessChunk**, asigne los resultados de **rxImport** a una variable y, a continuación, los resultados en la consola.
  
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