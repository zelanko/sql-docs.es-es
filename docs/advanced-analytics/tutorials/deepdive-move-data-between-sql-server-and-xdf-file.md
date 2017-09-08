---
title: Mover datos entre SQL Server y el archivo xdf. | Documentos de Microsoft
ms.custom: 
ms.date: 05/18/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
dev_langs:
- R
ms.assetid: 40887cb3-ffbb-4769-9f54-c006d7f4798c
caps.latest.revision: 17
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 1db44423f71f1808d99a9611062bdc8291640ece
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="move-data-between-sql-server-and-xdf-file"></a>Mover datos entre SQL Server y el archivo XDF

Cuando está trabajando en un contexto de proceso local, tener acceso a los archivos de datos locales y la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (definido como un origen de datos RxSqlServerData) de la base de datos.

En esta sección, aprenderá cómo obtener datos y almacenarlos en un archivo en el equipo local para que pueda realizar transformaciones en los datos. Cuando haya terminado, podrá utilizar los datos en el archivo para crear un nuevo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tabla, mediante el uso de rxDataStep.
  
## <a name="create-a-sql-server-table-from-an-xdf-file"></a>Crear una tabla de SQL Server desde un archivo XDF

La función rxImport le permite importar datos desde cualquier origen de datos admitidos en un archivo xdf. local. El uso de un archivo local puede ser conveniente si quiere realizar muchos análisis distintos en los datos almacenados en una base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y quiere evitar ejecutar la misma consulta una y otra vez.

Para este ejercicio, usará de nuevo los datos de fraude de tarjetas de crédito. En este escenario, se le ha pedido realizar un análisis adicional de los usuarios en los estados de California, Oregon y Washington. Para que sea más eficaz, hemos decidido almacenar datos solo para estos estados en el equipo local y trabajar con las variables sexo, titular de la tarjeta, estado y saldo.

1. Vuelva a usar el vector *stateAbb* que ha creado anteriormente para identificar los niveles que quiere incluir y, después, imprima en la consola la nueva variable, *statesToKeep*.
  
    ```R
    statesToKeep <- sapply(c("CA", "OR", "WA"), grep, stateAbb)
    statesToKeep
    ```
    **Resultado**
    
    CA|O BIEN|WA
    ----|----|----
    5|38|48
    
2. Ahora, definirá los datos que quiere traer de SQL Server mediante una consulta de [!INCLUDE[tsql](../../includes/tsql-md.md)] .  Más adelante usará esta variable como el argumento *inData* para *rxImport*.
  
    ```R
    importQuery <- paste("SELECT gender,cardholder,balance,state FROM",  sqlFraudTable,  "WHERE (state = 5 OR state = 38 OR state = 48)")
    ```
  
    Asegúrese de que no hay ningún carácter oculto como saltos de línea o tabulaciones en la consulta.
  
3. A continuación, definirá las columnas que se va a usar al trabajar con los datos en R. Por ejemplo, en el conjunto de datos más pequeño, necesita solo tres niveles de factor, ya que la consulta devolverá datos para sólo tres estados.  Puede volver a usar la variable *statesToKeep* para identificar los niveles correctos que incluir.
  
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
  
5. Cree el objeto de origen de datos pasando todas las variables que acaba de definir como argumentos a RxSqlServerData.
  
    ```R
    sqlServerImportDS <- RxSqlServerData(
        connectionString = sqlConnString,
        sqlQuery = importQuery,
        colInfo = importColInfo)
    ```
  
6. A continuación, llame a **rxImport** para escribir los datos en un archivo denominado `ccFraudSub.xdf`, en el directorio de trabajo actual.
  
    ```R
    localDS <- rxImport(inData = sqlServerImportDS,
        outFile = "ccFraudSub.xdf",
        overwrite = TRUE)
    ```
  
    El *localDs* objeto devuelto por la función rxImport es un objeto de origen de datos de RxXdfData ligero que representa el archivo de datos de ccFraud.xdf almacenado localmente en el disco.
  
7. Llamar a rxGetVarInfo en el archivo xdf. para comprobar que el esquema de datos es el mismo.
  
    ```R
    rxGetVarInfo(data = localDS)
    ```

    **Resultado**
    
    *rxGetVarInfo(data = localDS)*

    *Var 1: gender, Tipo: factor, no hay niveles de factor disponibles*

    *Var 2: cardholder, Tipo: factor, no hay niveles de factor disponibles*

    *Var 3: balance, Tipo: integer, Low/High: (0, 22463)*

    *Var 4: state, Tipo: factor, no hay niveles de factor disponibles*
  
8. Ahora puede llamar a varias funciones de R para analizar el objeto *localDs* , como haría con los datos de origen en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Por ejemplo:
  
    ```R
    rxSummary(~gender + cardholder + balance + state, data = localDS)
    ```

Ahora que ha aprendido a usar contextos de cálculo y trabajar con varios orígenes de datos, ha llegado el momento de probar algo divertido. En la siguiente y última lección, creará una simulación sencilla mediante una función personalizada de R y la ejecutará en el servidor remoto.

## <a name="next-step"></a>Paso siguiente

[Cree una simulación Simple](../../advanced-analytics/tutorials/deepdive-create-a-simple-simulation.md)

## <a name="previous-step"></a>Paso anterior

[Analizar los datos de contexto de proceso Local.](../../advanced-analytics/tutorials/deepdive-analyze-data-in-local-compute-context.md)




