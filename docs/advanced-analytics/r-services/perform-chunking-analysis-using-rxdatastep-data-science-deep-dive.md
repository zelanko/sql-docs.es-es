---
title: "Perform Chunking Analysis using rxDataStep (Data Science Deep Dive) (Realizar an&#225;lisis de fragmentaci&#243;n mediante rxDataStep (An&#225;lisis detallado de ciencia de datos)) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to: 
  - "SQL Server 2016"
dev_langs: 
  - "R"
ms.assetid: 4290ee5f-be90-446a-91e8-3095d694bd82
caps.latest.revision: 17
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
---
# Perform Chunking Analysis using rxDataStep (Data Science Deep Dive) (Realizar an&#225;lisis de fragmentaci&#243;n mediante rxDataStep (An&#225;lisis detallado de ciencia de datos))
La función *rxDataStep* puede usarse para procesar datos en fragmentos en lugar de requerir que el conjunto de datos completo se cargue en memoria y se procese de una vez, como en R tradicional. Funciona de manera que lee los datos en fragmentos y usa funciones de R para procesar cada fragmento de datos a su vez y, después, escribe los resultados de resumen de cada fragmento en un origen de datos común de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
En esta lección, pondrá en práctica esta técnica usando la función *table* de R para calcular una tabla de contingencia.  
  
> [!TIP]  
> Este ejemplo está pensado únicamente con fines informativos. Si necesita tabular conjuntos de datos reales, le recomendamos que use las funciones *rxCrossTabs* o *rxCube* creadas en **RevoScaleR**, que se han optimizado para este tipo de operación.  
  
## Datos de partición por valores  
  
1.  Primero, cree una función de R personalizada denominada *ProcessChunk* que llame a la función *table* en cada fragmento de datos.  
  
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
 
  
2.  Establezca el contexto de cálculo en el servidor.  
  
    ```R  
    rxSetComputeContext( sqlCompute )   
    ```  
  
3.  Definirá un origen de datos de SQL Server para almacenar los datos que está procesando. Comience por asignar una consulta de SQL a una variable.   
  
    ```R  
    dayQuery <-  "SELECT DayOfWeek FROM AirDemoSmallTest"   
    ```  

4.  Conecte esa variable al argumento *sqlQuery* de un nuevo origen de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
    ```R  
    inDataSource <- RxSqlServerData(sqlQuery = dayQuery,  
        connectionString = sqlConnString,    
        rowsPerRead = 50000,      
        colInfo = list(DayOfWeek = list(type = "factor",   
            levels = as.character(1:7))))    
    ```  
     Si ha ejecutado *rxGetVarInfo* en este origen de datos, habrá visto que contiene solo la columna única: *Var 1: DayOfWeek, Tipo: factor, no hay niveles de factor disponibles*
     
5.  Antes de aplicar esta variable de factor en los datos de origen, cree una tabla independiente para contener los resultados intermedios. De nuevo, simplemente use la función *RxSqlServerData* para definir los datos y elimine cualquier tabla existente con el mismo nombre.   
  
    ```R  
    iroDataSource = RxSqlServerData(table = "iroResults",   connectionString = sqlConnString)   
    # Check whether the table already exists.  
    if (rxSqlServerTableExists(table = "iroResults",  connectionString = sqlConnString))  { rxSqlServerDropTable( table = "iroResults", connectionString = sqlConnString) }   
    ```  
  
7.  Ahora, llamará a la función personalizada *ProcessChunk* para transformar los datos a medida que se leen usándolos como el argumento *transformFunc* en la función *rxDataStep*.  
  
    ```R  
    rxDataStep( inData = inDataSource, outFile = iroDataSource, transformFunc = ProcessChunk, overwrite = TRUE)   
    ```  
  
8.  Para ver los resultados intermedios de *ProcessChunk*, asigne los resultados de *rxImport* a una variable y, después, imprima los resultados en la consola.  
  
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
  
10. Para quitar la tabla de resultados intermedios, realice otra llamada a *rxSqlServerDropTable*.  
  
    ```R  
    rxSqlServerDropTable( table = "iroResults",     connectionString = sqlConnString)    
    ```  
  
## Paso siguiente  
[Lesson 4: Analyze Data in Local Compute Context &#40;Data Science Deep Dive&#41; (Lección 4: Analizar datos en el contexto de cálculo local &#40;Análisis detallado de ciencia de datos&#41;)](../../advanced-analytics/r-services/lesson-4-analyze-data-in-local-compute-context-data-science-deep-dive.md)  
  
## Paso anterior  
[Create New SQL Server Table using rxDataStep &#40;Data Science Deep Dive&#41; (Crear una nueva tabla de SQL Server mediante rxDataStep &#40;Análisis detallado de ciencia de datos&#41;)](../../advanced-analytics/r-services/create-new-sql-server-table-using-rxdatastep-data-science-deep-dive.md)  
  
## Vea también  
[Análisis detallado de ciencia de datos: Usar los paquetes de RevoScaleR](../../advanced-analytics/r-services/data-science-deep-dive-using-the-revoscaler-packages.md)  
  
  
  
