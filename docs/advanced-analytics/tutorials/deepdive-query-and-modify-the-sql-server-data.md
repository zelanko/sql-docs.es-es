---
title: Consultar y modificar los datos de SQL Server mediante RevoScaleR
description: Tutorial tutorial sobre cómo consultar y modificar datos mediante el lenguaje R en SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.openlocfilehash: 0784f10bfc4405ce17e365b6afcb596fa534202d
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/19/2019
ms.locfileid: "68344658"
---
# <a name="query-and-modify-the-sql-server-data-sql-server-and-revoscaler-tutorial"></a>Consultar y modificar los datos de SQL Server (tutorial de SQL Server y RevoScaleR)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Esta lección forma parte del [tutorial de RevoScaleR](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md) sobre cómo usar [las funciones de RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) con SQL Server.

En la lección anterior, cargó los datos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. En este paso, puede explorar y modificar los datos mediante **RevoScaleR**:

> [!div class="checklist"]
> * Devolver información básica sobre las variables
> * Crear datos de categorías a partir de datos sin procesar

Los datos de categorías, o *las variables de factor*, son útiles para las visualizaciones de datos exploratorias. Puede usarlos como entradas para los histogramas para hacerse una idea de qué aspecto tienen los datos variables.

## <a name="query-for-columns-and-types"></a>Consultar columnas y tipos

Use un IDE de R o RGui. exe para ejecutar el script de R. 

En primer lugar, obtenga una lista de las columnas y sus tipos de datos. Puede usar la función [rxGetVarInfo](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxgetvarinfoxdf) y especificar el origen de datos que desea analizar. En función de la versión de **RevoScaleR**, también puede usar [rxGetVarNames](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxgetvarnames). 
  
```R
rxGetVarInfo(data = sqlFraudDS)
```

**Resultado**

```R
Var 1: custID, Type: integer
Var 2: gender, Type: integer
Var 3: state, Type: integer
Var 4: cardholder, Type: integer
Var 5: balance, Type: integer
Var 6: numTrans, Type: integer
Var 7: numIntlTrans, Type: integer
Var 8: creditLine, Type: integer
Var 9: fraudRisk, Type: integer
```

## <a name="create-categorical-data"></a>Crear datos de categorías

Todas las variables se almacenan como enteros, pero algunas variables representan datos de categorías, denominadas *variables de factor* en R. Por ejemplo, el *Estado* de la columna contiene números que se usan como identificadores para los Estados 50 más el distrito de Columbia. Para facilitar la comprensión de los datos, reemplace los números con una lista de abreviaturas de estado.

En este paso, creará un vector de cadena que contiene las abreviaturas y, a continuación, asignará estos valores de categorías a los identificadores enteros originales. A continuación, use la nueva variable en el argumento *colInfo* para especificar que esta columna se trate como un factor. Cada vez que analiza los datos o los mueve, se usan las abreviaturas y la columna se trata como un factor.

Asignar la columna a las abreviaturas antes de usarla como un factor mejora realmente también el rendimiento. Para obtener más información, vea [R y optimización de datos](../r/r-and-data-optimization-r-services.md).

1. Empiece por crear una variable de R, *stateAbb*, y definir el vector de cadenas que se va a agregar, como se indica a continuación.
  
    ```R
    stateAbb <- c("AK", "AL", "AR", "AZ", "CA", "CO", "CT", "DC",
        "DE", "FL", "GA", "HI","IA", "ID", "IL", "IN", "KS", "KY", "LA",
        "MA", "MD", "ME", "MI", "MN", "MO", "MS", "MT", "NB", "NC", "ND",
        "NH", "NJ", "NM", "NV", "NY", "OH", "OK", "OR", "PA", "RI","SC",
        "SD", "TN", "TX", "UT", "VA", "VT", "WA", "WI", "WV", "WY")
    ```

2. Después, cree un objeto de información de columna, denominado *ccColInfo*, que especifique la asignación de los valores enteros existentes con los niveles de categorías (las abreviaturas de los estados).
  
    Esta instrucción también crea variables de factor para el género y el titular de tarjeta.
  
    ```R
    ccColInfo <- list(
    gender = list(
              type = "factor",
              levels = c("1", "2"),
              newLevels = c("Male", "Female")
              ),
    cardholder = list(
                  type = "factor",
                  levels = c("1", "2"),
                  newLevels = c("Principal", "Secondary")
                   ),
    state = list(
             type = "factor",
             levels = as.character(1:51),
             newLevels = stateAbb
             ),
    balance = list(type = "numeric")
    )
    ```
  
3. Para crear el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] origen de datos que usa los datos actualizados, llame a la función **RxSqlServerData** como antes, pero agregue el argumento *colInfo* .
  
    ```R
    sqlFraudDS <- RxSqlServerData(connectionString = sqlConnString,
    table = sqlFraudTable, colInfo = ccColInfo,
    rowsPerRead = sqlRowsPerRead)
    ```
  
    - Para el parámetro *table* , pase la variable *sqlFraudTable*, que contiene el origen de datos que ha creado anteriormente.
    - Para el parámetro *colInfo* , pase la variable *ccColInfo* , que contiene los tipos de datos de columna y los niveles de factor.

4.  Ahora puede usar la función **rxGetVarInfo** para ver las variables en el nuevo origen de datos.
  
    ```R
    rxGetVarInfo(data = sqlFraudDS)
    ```

    **Resultado**
    
    ```R
    Var 1: custID, Type: integer
    Var 2: gender  2 factor levels: Male Female
    Var 3: state   51 factor levels: AK AL AR AZ CA ... VT WA WI WV WY
    Var 4: cardholder  2 factor levels: Principal Secondary
    Var 5: balance, Type: integer
    Var 6: numTrans, Type: integer
    Var 7: numIntlTrans, Type: integer
    Var 8: creditLine, Type: integer
    Var 9: fraudRisk, Type: integer
    ```

Ahora las tres variables que ha especificado (*gender*, *state*y *cardholder*) se tratan como factores.

## <a name="next-steps"></a>Pasos siguientes

> [!div class="nextstepaction"]
> [Definir y usar contextos de cálculo](../../advanced-analytics/tutorials/deepdive-define-and-use-compute-contexts.md)