---
title: Realizar análisis fragmentación mediante rxDataStep (SQL y R profundización) | Documentos de Microsoft
ms.custom: ''
ms.date: 12/14/2017
ms.reviewer: ''
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: ''
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: tutorial
applies_to:
- SQL Server 2016
- SQL Server 2017
dev_langs:
- R
ms.author: heidist
author: HeidiSteen
manager: cgronlun
ms.workload: Inactive
ms.openlocfilehash: 7037ced2194a5076f12f81858e98cc7dc9b89aad
ms.sourcegitcommit: 059fc64ba858ea2adaad2db39f306a8bff9649c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/04/2018
---
# <a name="perform-chunking-analysis-using-rxdatastep-sql-and-r-deep-dive"></a>Realizar análisis fragmentación mediante rxDataStep (SQL y R profundización)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Este artículo forma parte del tutorial exhaustiva de ciencia de datos, acerca de cómo usar [RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) con SQL Server.

En esta lección, utilizará la **rxDataStep** función para procesar los datos en fragmentos, en lugar de requerir que todo el conjunto de datos se cargan en la memoria y procesar al mismo tiempo, como en tradicional R. El **rxDataStep** funciones lee los datos en fragmentos, se aplica a las funciones de R para cada fragmento de datos a su vez y, a continuación, guarda los resultados de resumen para cada fragmento en común [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] origen de datos. Cuando se han leído todos los datos, se combinan los resultados.

> [!TIP]
> En esta lección, calcular una tabla de contingencia utilizando el `table` función en R. Este ejemplo está pensado únicamente con fines informativos. 
> 
> Si necesita pasar conjuntos de datos del mundo real, se recomienda que realice la **rxCrossTabs** o **rxCube** las funciones de **RevoScaleR**, que se optimizan para este tipo de operación.

## <a name="partition-data-by-values"></a>Datos de la partición por valores

1. Crear una función de R personalizada que llama la R `table` funcionen en cada fragmento de datos y el nombre de la nueva función `ProcessChunk`.
  
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
    rxSetComputeContext( sqlCompute )
    ```
  
3. Definir un origen de datos de SQL Server para almacenar los datos que está procesando. Comience por asignar una consulta de SQL a una variable. A continuación, usar esa variable en el *sqlQuery* argumento de un nuevo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] origen de datos.
  
  
    ```R
    dayQuery <-  "SELECT DayOfWeek FROM AirDemoSmallTest"
    inDataSource <- RxSqlServerData(sqlQuery = dayQuery,
        connectionString = sqlConnString,
        rowsPerRead = 50000,
        colInfo = list(DayOfWeek = list(type = "factor",
            levels = as.character(1:7))))
    ```
4. Si lo desea, puede ejecutar **rxGetVarInfo** en este origen de datos. En este punto, contiene una sola columna: *Var 1: DayOfWeek, escriba: no factor, ningún nivel de factor disponibles*
     
5. Antes de aplicar esta variable de factor en los datos de origen, cree una tabla independiente para contener los resultados intermedios. Una vez más, simplemente utilizar la función RxSqlServerData para definir los datos, makign seguro que desea eliminar las tablas existentes del mismo nombre.
  
    ```R
    iroDataSource = RxSqlServerData(table = "iroResults",   connectionString = sqlConnString)
    # Check whether the table already exists.
    if (rxSqlServerTableExists(table = "iroResults",  connectionString = sqlConnString))  { rxSqlServerDropTable( table = "iroResults", connectionString = sqlConnString) }
    ```
  
7.  Llame a la función personalizada `ProcessChunk` para transformar los datos tal y como se leen, utilizando como el *transformFunc* argumento pasado a la **rxDataStep** (función).
  
    ```R
    rxDataStep( inData = inDataSource, outFile = iroDataSource, transformFunc = ProcessChunk, overwrite = TRUE)
    ```
  
8.  Para ver los resultados intermedios de `ProcessChunk`, asigne los resultados de **rxImport** a una variable y, a continuación, los resultados en la consola.
  
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

10. Para quitar la tabla de resultados intermedios, realizar una llamada a **rxSqlServerDropTable**.
  
    ```R
    rxSqlServerDropTable( table = "iroResults", connectionString = sqlConnString)
    ```

## <a name="next-step"></a>Paso siguiente

[Analizar datos en el contexto del proceso local](../../advanced-analytics/tutorials/deepdive-analyze-data-in-local-compute-context.md)

## <a name="previous-step"></a>Paso anterior

[Crear una nueva tabla de SQL Server mediante rxDataStep](../../advanced-analytics/tutorials/deepdive-create-new-sql-server-table-using-rxdatastep.md)
