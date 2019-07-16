---
title: 'Mover datos entre SQL Server y el archivo XDF con RevoScaleR: SQL Server Machine Learning'
description: Tutorial del tutorial sobre cómo mover datos con XDF y el lenguaje R en SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.openlocfilehash: f5800f315ee09328908b612c18faf6c77a7ac13c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67962210"
---
# <a name="move-data-between-sql-server-and-xdf-file-sql-server-and-revoscaler-tutorial"></a>Mover datos entre SQL Server y el archivo XDF (tutorial de SQL Server y RevoScaleR)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

En esta lección forma parte de la [RevoScaleR tutorial](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md) sobre cómo usar [funciones de RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) con SQL Server.

En este paso, aprenderá a usar un archivo XDF para transferir datos entre contextos de cálculo remotos y locales. Almacenamiento de datos en un archivo XDF le permite realizar transformaciones en los datos.

Cuando haya terminado, use los datos en el archivo para crear un nuevo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tabla. La función [rxDataStep](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdatastep) puede aplicar transformaciones a los datos y realiza la conversión entre las tramas de datos y archivos xdf.
  
## <a name="create-a-sql-server-table-from-an-xdf-file"></a>Crear una tabla de SQL Server desde un archivo XDF

Para este ejercicio, use otra vez los datos de fraude de tarjeta de crédito. En este escenario, se le ha pedido realizar un análisis adicional de los usuarios en los estados de California, Oregon y Washington. Para que sea más eficaz, ha decidido almacenar datos para solo estos Estados en el equipo local, y trabajar con solo las variables sexo, los titulares de tarjetas, estado y saldo.

1. Volver a usar el `stateAbb` variable que creó anteriormente para identificar los niveles para incluir y escribirlos en una nueva variable, `statesToKeep`.
  
    ```R
    statesToKeep <- sapply(c("CA", "OR", "WA"), grep, stateAbb)
    statesToKeep
    ```
    **Resultado**
    
    CA|OR|WA
    ----|----|----
    5|38|48
    
2. Definir los datos que desea conectar a través de SQL Server, utilizando un [!INCLUDE[tsql](../../includes/tsql-md.md)] consulta.  Más adelante se utiliza esta variable como el *inData* argumento para **rxImport**.
  
    ```R
    importQuery <- paste("SELECT gender,cardholder,balance,state FROM",  sqlFraudTable,  "WHERE (state = 5 OR state = 38 OR state = 48)")
    ```
  
    Asegúrese de que no hay ningún carácter oculto como saltos de línea o tabulaciones en la consulta.
  
3. A continuación, defina las columnas que se va a usar al trabajar con los datos en R. Por ejemplo, en el conjunto de datos más pequeño, necesita solo tres niveles de factor, porque la consulta devuelve datos para sólo tres estados.  Aplicar el `statesToKeep` variable para identificar los niveles correctos que incluir.
  
    ```R
    importColInfo <- list(
        gender = list( type = "factor",  levels = c("1", "2"), newLevels = c("Male", "Female")),
        cardholder = list(  type = "factor",  levels = c("1", "2"), newLevels = c("Principal", "Secondary")),
        state = list(   type = "factor",  levels = as.character(statesToKeep), newLevels = names(statesToKeep))
            )
    ```
  
4. Establece el contexto de cálculo en **local**, porque desea que todos los datos disponibles en el equipo local.
  
    ```R
    rxSetComputeContext("local")
    ```
    
    El [rxImport](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqlserverdata) función puede importar datos desde cualquier origen de datos admitidos en un archivo XDF local. Con una copia local de los datos es útil cuando desea realizar muchos análisis distintos en los datos, pero quiere evitar ejecutar la misma consulta una y otra vez.

5. Cree el objeto de origen de datos pasando las variables definidas anteriormente como argumentos a **RxSqlServerData**.
  
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
  
    El `localDs` objeto devuelto por la **rxImport** función es un ligero **RxXdfData** objeto de origen de datos que representa el `ccFraud.xdf` archivo de datos almacenado localmente en el disco.
  
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

8. Ahora puede llamar a varias funciones de R para analizar el **localDs** de objeto, como haría con los datos de origen en SQL Server. Por ejemplo, podría Resumir por género:
  
    ```R
    rxSummary(~gender + cardholder + balance + state, data = localDS)
    ```

## <a name="next-steps"></a>Pasos siguientes

En esta lección se concluye la serie de tutoriales de varias partes en **RevoScaleR** y SQL Server. Presenta numerosos conceptos relacionados con los datos y cálculo, lo que le ofrece una base para avanzar con sus propios requisitos de datos y de proyecto.

Para profundizar sus conocimientos de **RevoScaleR**, puede volver a la lista de tutoriales de R paso a paso a través de los ejercicios que podría haber pasado por alto. Como alternativa, revise los artículos de procedimientos en la tabla de contenido para obtener información sobre las tareas generales.

> [!div class="nextstepaction"]
> [Tutoriales de R para SQL Server](sql-server-r-tutorials.md)