---
title: Movimiento de datos con el archivo XDF
description: 'Tutorial 13 de RevoScaleR: Traslado de datos usando XDF y el lenguaje R en SQL Server.'
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 9c7e5ce4cbe995fd677acd406187dfaf264a7461
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85680005"
---
# <a name="move-data-between-sql-server-and-xdf-file-sql-server-and-revoscaler-tutorial"></a>Movimiento de datos entre SQL Server y el archivo XDF (tutorial de SQL Server y RevoScaleR)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

Este es el tutorial 13 de la [serie de tutoriales de RevoScaleR](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md) sobre el uso de las [funciones de RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) con SQL Server.

En este tutorial, aprenderá a usar un archivo XDF para transferir datos entre contextos de cálculo remotos y locales. El almacenamiento de los datos en un archivo XDF permite realizar transformaciones en los datos.

Cuando termine, use los datos en el archivo para crear una nueva tabla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. La función [rxDataStep](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdatastep) puede aplicar transformaciones a los datos y realiza la conversión entre tramas de datos y archivos .xdf.
  
## <a name="create-a-sql-server-table-from-an-xdf-file"></a>Creación de una tabla de SQL Server desde un archivo XDF

Para este ejercicio, use de nuevo los datos de fraude de tarjetas de crédito. En este escenario, se le ha pedido realizar un análisis adicional de los usuarios en los estados de California, Oregon y Washington. Para que sea más eficaz, hemos decidido almacenar datos solo para estos estados en el equipo local, y trabajar únicamente con las variables sexo, titular de la tarjeta, estado y saldo.

1. Vuelva a usar la variable `stateAbb` que ha creado anteriormente para identificar los niveles que quiere incluir y escriba una nueva variable, `statesToKeep`.
  
    ```R
    statesToKeep <- sapply(c("CA", "OR", "WA"), grep, stateAbb)
    statesToKeep
    ```
    **Resultados**
    
    CA|O BIEN|WA
    ----|----|----
    5|38|48
    
2. Defina los datos que quiere traer de SQL Server mediante una consulta de [!INCLUDE[tsql](../../includes/tsql-md.md)].  Más adelante use esta variable como el argumento *inData* para **rxImport**.
  
    ```R
    importQuery <- paste("SELECT gender,cardholder,balance,state FROM",  sqlFraudTable,  "WHERE (state = 5 OR state = 38 OR state = 48)")
    ```
  
    Asegúrese de que no hay ningún carácter oculto como saltos de línea o tabulaciones en la consulta.
  
3. A continuación, defina las columnas que se van a usar al trabajar con los datos en R. Por ejemplo, en el conjunto de datos más pequeño, solo necesita tres niveles de factor, porque la consulta solo devuelve datos para tres estados.  Aplique la variable `statesToKeep` para identificar los niveles correctos que incluir.
  
    ```R
    importColInfo <- list(
        gender = list( type = "factor",  levels = c("1", "2"), newLevels = c("Male", "Female")),
        cardholder = list(  type = "factor",  levels = c("1", "2"), newLevels = c("Principal", "Secondary")),
        state = list(   type = "factor",  levels = as.character(statesToKeep), newLevels = names(statesToKeep))
            )
    ```
  
4. Establezca el contexto de cálculo en **local**, ya que quiere todos los datos disponibles en el equipo local.
  
    ```R
    rxSetComputeContext("local")
    ```
    
    La función [rxImport](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqlserverdata) puede importar datos desde cualquier origen de datos que se admita a un archivo XDF local. El uso de una copia local de los datos puede ser conveniente cuando quiera realizar muchos análisis distintos en los datos, pero quiere evitar ejecutar la misma consulta una y otra vez.

5. Cree el objeto de origen de datos pasando las variables previamente definidas como argumentos a **RxSqlServerData**.
  
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
  
    El objeto `localDs` devuelto desde la función **rxImport** es un objeto de origen de datos **RxXdfData** ligero que representa el archivo de datos `ccFraud.xdf` almacenado localmente en el disco.
  
7. Llame a [rxGetVarInfo](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxgetvarinfoxdf) en el archivo XDF para comprobar que el esquema de datos es el mismo.
  
    ```R
    rxGetVarInfo(data = localDS)
    ```

    **Resultados**
    
    ```R
    rxGetVarInfo(data = localDS)
    Var 1: gender, Type: factor, no factor levels available
    Var 2: cardholder, Type: factor, no factor levels available
    Var 3: balance, Type: integer, Low/High: (0, 22463)
    Var 4: state, Type: factor, no factor levels available
    ```

8. Ahora puede llamar a varias funciones de R para analizar el objeto **localDs**, como haría con los datos de origen en SQL Server. Por ejemplo, puede resumir por sexo:
  
    ```R
    rxSummary(~gender + cardholder + balance + state, data = localDS)
    ```

## <a name="next-steps"></a>Pasos siguientes

En esta tutorial se concluye la serie de tutoriales de varias partes en **RevoScaleR** y SQL Server. Presenta numerosos conceptos relacionados con los datos y de cálculo, lo que le proporciona una base para avanzar con sus propios datos y requisitos de proyecto.

Para profundizar en los conocimientos de **RevoScaleR**, puede volver a la lista de tutoriales de R para repasar todos y cada uno de los ejercicios que podría no haber realizado. Como alternativa, revise los artículos de procedimientos de la tabla de contenido para obtener información sobre las tareas generales.

> [!div class="nextstepaction"]
> [Tutoriales de R para SQL Server](sql-server-r-tutorials.md)