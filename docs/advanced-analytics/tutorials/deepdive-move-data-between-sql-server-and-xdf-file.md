---
title: "Mover datos entre SQL Server y el archivo xdf. (SQL y R profundización) | Documentos de Microsoft"
ms.custom: 
ms.date: 12/14/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: 
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: tutorial
applies_to:
- SQL Server 2016
- SQL Server 2017
dev_langs: R
ms.assetid: 40887cb3-ffbb-4769-9f54-c006d7f4798c
caps.latest.revision: "17"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: 10be63f32a197134e4979dc976dd84919fde9e1f
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/08/2018
---
# <a name="move-data-between-sql-server-and-xdf-file-sql-and-r-deep-dive"></a>Mover datos entre SQL Server y el archivo xdf. (SQL y R profundización)

Este artículo forma parte del tutorial exhaustiva de ciencia de datos, acerca de cómo usar [RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) con SQL Server.

En este paso, aprenderá a usar un archivo xdf. para transferir datos entre los contextos de proceso remotos y locales. Almacenar los datos en un archivo xdf. le permite realizar transformaciones en los datos.

Cuando haya terminado, use los datos en el archivo para crear un nuevo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tabla. La función [rxDataStep](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdatastep) puede aplicar transformaciones a los datos y realiza la conversión entre tramas de datos y archivos xdf.
  
## <a name="create-a-sql-server-table-from-an-xdf-file"></a>Crear una tabla de SQL Server desde un archivo xdf.

Para este ejercicio, puede usar los datos de fraude de tarjeta de crédito nuevo. En este escenario, se le ha pedido realizar un análisis adicional de los usuarios en los estados de California, Oregon y Washington. Para que sea más eficaz, ha decidido para almacenar los datos de solo estos Estados en el equipo local y trabajar con solo el sexo de variables, información de los titulares, estado y equilibrio.

1. Volver a usar el `stateAbb` variable que creó anteriormente para identificar los niveles para incluir y escribirlos en una nueva variable, `statesToKeep`.
  
    ```R
    statesToKeep <- sapply(c("CA", "OR", "WA"), grep, stateAbb)
    statesToKeep
    ```
    **Resultado**
    
    CA|O BIEN|WA
    ----|----|----
    5|38|48
    
2. Definir los datos que desea conectar a través de SQL Server, mediante un [!INCLUDE[tsql](../../includes/tsql-md.md)] consulta.  Más adelante se utiliza esta variable como el *inData* argumento para **rxImport**.
  
    ```R
    importQuery <- paste("SELECT gender,cardholder,balance,state FROM",  sqlFraudTable,  "WHERE (state = 5 OR state = 38 OR state = 48)")
    ```
  
    Asegúrese de que no hay ningún carácter oculto como saltos de línea o tabulaciones en la consulta.
  
3. A continuación, defina las columnas que se va a usar al trabajar con los datos en R. Por ejemplo, en el conjunto de datos más pequeño, necesita solo tres niveles de factor, porque la consulta devuelve datos para sólo tres estados.  Aplicar el `statesToKeep` variable para identificar los niveles correcta para incluir.
  
    ```R
    importColInfo <- list(
        gender = list( type = "factor",  levels = c("1", "2"), newLevels = c("Male", "Female")),
        cardholder = list(  type = "factor",  levels = c("1", "2"), newLevels = c("Principal", "Secondary")),
        state = list(   type = "factor",  levels = as.character(statesToKeep), newLevels = names(statesToKeep))
            )
    ```
  
4. Establece el contexto de proceso en **local**, ya que desea que todos los datos disponibles en el equipo local.
  
    ```R
    rxSetComputeContext("local")
    ```
    
    El [rxImport](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqlserverdata) función puede importar datos desde cualquier origen de datos admitidos en un archivo xdf. local. Con una copia local de los datos resulta útil si desea llevar a cabo muchas análisis diferentes en los datos, pero desea evitar ejecutar la misma consulta una y otra vez.

5. Cree el objeto de origen de datos pasando las variables definidas previamente como argumentos a **RxSqlServerData**.
  
    ```R
    sqlServerImportDS <- RxSqlServerData(
        connectionString = sqlConnString,
        sqlQuery = importQuery,
        colInfo = importColInfo)
    ```
  
6. Llame a **rxImport** para escribir los datos en un archivo denominado `ccFraudSub.xdf`, en el directorio de trabajo actual.
  
    ```R
    localDS <- rxImport(inData = sqlServerImportDS,
        outFile = "ccFraudSub.xdf",
        overwrite = TRUE)
    ```
  
    El `localDs` objeto devuelto por la **rxImport** función es una ligera **RxXdfData** objeto de origen de datos que representa el `ccFraud.xdf` archivo de datos almacenado localmente en el disco.
  
7. Llame a [rxGetVarInfo](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxgetvarinfoxdf) en el archivo XDF para comprobar que el esquema de datos es el mismo.
  
    ```R
    rxGetVarInfo(data = localDS)
    ```

    **Resultado**
    
    *rxGetVarInfo(data = localDS)*

    *Var 1: gender, Tipo: factor, no hay niveles de factor disponibles*

    *Var 2: cardholder, Tipo: factor, no hay niveles de factor disponibles*

    *Var 3: balance, Tipo: integer, Low/High: (0, 22463)*

    *Var 4: state, Tipo: factor, no hay niveles de factor disponibles*
  
8. Ahora puede llamar a varias funciones de R para analizar el objeto `localDs`, como haría con los datos de origen en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Por ejemplo, podría Resumir por género:
  
    ```R
    rxSummary(~gender + cardholder + balance + state, data = localDS)
    ```

Ahora que ha aprendido a usar contextos de cálculo y trabajar con varios orígenes de datos, ha llegado el momento de probar algo divertido. En la lección siguiente y última, cree una simulación simple que se ejecuta una función de R personalizada en el servidor remoto.

## <a name="next-step"></a>Paso siguiente

[Crear una simulación sencilla](../../advanced-analytics/tutorials/deepdive-create-a-simple-simulation.md)

## <a name="previous-step"></a>Paso anterior

[Analizar datos en el contexto del proceso local](../../advanced-analytics/tutorials/deepdive-analyze-data-in-local-compute-context.md)



