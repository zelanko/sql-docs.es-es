---
title: Movimiento de datos entre SQL Server y el archivo XDF mediante RevoScaleR
description: Tutorial tutorial sobre cómo migrar datos mediante XDF y el lenguaje R en SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.openlocfilehash: 0e4c0fbdd9f625886a7d38fc80895e9f4407ce88
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/19/2019
ms.locfileid: "68344750"
---
# <a name="move-data-between-sql-server-and-xdf-file-sql-server-and-revoscaler-tutorial"></a>Movimiento de datos entre SQL Server y el archivo XDF (tutorial de SQL Server y RevoScaleR)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Esta lección forma parte del [tutorial de RevoScaleR](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md) sobre cómo usar [las funciones de RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) con SQL Server.

En este paso, aprenderá a usar un archivo XDF para transferir datos entre contextos de cálculo remotos y locales. El almacenamiento de los datos en un archivo XDF permite realizar transformaciones en los datos.

Cuando haya terminado, use los datos del archivo para crear una nueva [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tabla. La función [rxDataStep](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdatastep) puede aplicar transformaciones a los datos y realiza la conversión entre tramas de datos y archivos. xdf.
  
## <a name="create-a-sql-server-table-from-an-xdf-file"></a>Creación de una tabla de SQL Server a partir de un archivo XDF

Para este ejercicio, volverá a usar los datos de fraude de la tarjeta de crédito. En este escenario, se le ha pedido realizar un análisis adicional de los usuarios en los estados de California, Oregon y Washington. Para ser más eficaz, ha decidido almacenar datos solo para estos Estados en el equipo local y trabajar solo con las variables sexo, titular de la información, estado y saldo.

1. Vuelva a usar la `stateAbb` variable que creó anteriormente para identificar los niveles que se van a incluir y escríbalos en una nueva `statesToKeep`variable,.
  
    ```R
    statesToKeep <- sapply(c("CA", "OR", "WA"), grep, stateAbb)
    statesToKeep
    ```
    **Resultado**
    
    CA|OR|WA
    ----|----|----
    5|38|48
    
2. Defina los datos que desea traer de SQL Server, mediante una [!INCLUDE[tsql](../../includes/tsql-md.md)] consulta.  Más adelante usará esta variable como el  argumento indata para **rxImport**.
  
    ```R
    importQuery <- paste("SELECT gender,cardholder,balance,state FROM",  sqlFraudTable,  "WHERE (state = 5 OR state = 38 OR state = 48)")
    ```
  
    Asegúrese de que no hay ningún carácter oculto como saltos de línea o tabulaciones en la consulta.
  
3. A continuación, defina las columnas que se van a usar al trabajar con los datos de R. Por ejemplo, en el conjunto de datos más pequeño, solo necesita tres niveles de factor, porque la consulta solo devuelve datos para tres Estados.  Aplique la `statesToKeep` variable para identificar los niveles correctos que se van a incluir.
  
    ```R
    importColInfo <- list(
        gender = list( type = "factor",  levels = c("1", "2"), newLevels = c("Male", "Female")),
        cardholder = list(  type = "factor",  levels = c("1", "2"), newLevels = c("Principal", "Secondary")),
        state = list(   type = "factor",  levels = as.character(statesToKeep), newLevels = names(statesToKeep))
            )
    ```
  
4. Establezca el contexto de cálculo en **local**, ya que desea que todos los datos estén disponibles en el equipo local.
  
    ```R
    rxSetComputeContext("local")
    ```
    
    La función [rxImport](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqlserverdata) puede importar datos desde cualquier origen de datos compatible a un archivo XDF local. El uso de una copia local de los datos es práctico cuando desea realizar muchos análisis diferentes en los datos, pero desea evitar ejecutar la misma consulta una y otra vez.

5. Cree el objeto de origen de datos pasando las variables definidas previamente como argumentos a **RxSqlServerData**.
  
    ```R
    sqlServerImportDS <- RxSqlServerData(
        connectionString = sqlConnString,
        sqlQuery = importQuery,
        colInfo = importColInfo)
    ```
  
6. Llame a **rxImport** para escribir los datos en un archivo `ccFraudSub.xdf`denominado, en el directorio de trabajo actual.
  
    ```R
    localDS <- rxImport(inData = sqlServerImportDS,
        outFile = "ccFraudSub.xdf",
        overwrite = TRUE)
    ```
  
    El `localDs` objeto devuelto por la función **rxImport** es un objeto de origen de datos **RxXdfData** ligero que representa `ccFraud.xdf` el archivo de datos almacenado localmente en el disco.
  
7. Llame a [rxGetVarInfo](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxgetvarinfoxdf) en el archivo XDF para comprobar que el esquema de datos es el mismo.
  
    ```R
    rxGetVarInfo(data = localDS)
    ```

    **Resultado**
    
    ```R
    rxGetVarInfo(data = localDS)
    Var 1: gender, Type: factor, no factor levels available
    Var 2: cardholder, Type: factor, no factor levels available
    Var 3: balance, Type: integer, Low/High: (0, 22463)
    Var 4: state, Type: factor, no factor levels available
    ```

8. Ahora puede llamar a varias funciones de R para analizar el objeto **localDs** , tal como lo haría con los datos de origen en SQL Server. Por ejemplo, puede resumir por sexo:
  
    ```R
    rxSummary(~gender + cardholder + balance + state, data = localDS)
    ```

## <a name="next-steps"></a>Pasos siguientes

En esta lección se concluye la serie de tutoriales de varias partes en **RevoScaleR** y SQL Server. Le presentó numerosos conceptos relacionados con los datos y de cálculo, lo que le proporciona una base para avanzar con sus propios datos y requisitos de proyecto.

Para profundizar en sus conocimientos de **RevoScaleR**, puede volver a la lista de tutoriales de R para recorrer todos los ejercicios que podrían haber perdido. Como alternativa, revise los artículos de procedimientos de la tabla de contenido para obtener información sobre las tareas generales.

> [!div class="nextstepaction"]
> [Tutoriales de R para SQL Server](sql-server-r-tutorials.md)