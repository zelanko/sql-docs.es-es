---
title: 'Consultar y modificar los datos de SQL Server con RevoScaleR: SQL Server Machine Learning'
description: Tutorial del tutorial sobre cómo consultar y modificar datos mediante el lenguaje R en SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 6d2768399ecd3d504e5bc51d4c7cbd151488782a
ms.sourcegitcommit: 2827d19393c8060eafac18db3155a9bd230df423
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/27/2019
ms.locfileid: "58513142"
---
# <a name="query-and-modify-the-sql-server-data-sql-server-and-revoscaler-tutorial"></a>Consultar y modificar los datos de SQL Server (tutorial de SQL Server y RevoScaleR)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

En esta lección forma parte de la [RevoScaleR tutorial](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md) sobre cómo usar [funciones de RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) con SQL Server.

En la lección anterior, se cargan los datos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. En este paso, puede explorar y modificar datos mediante **RevoScaleR**:

> [!div class="checklist"]
> * Devolver información básica acerca de las variables
> * Crear datos de categorías de datos sin procesar

Datos de categorías, o *variables de factor*, son útiles para las visualizaciones de exploración de datos. Puede utilizarlas como entradas de histogramas para hacerse una idea del aspecto de los datos de la variable.

## <a name="query-for-columns-and-types"></a>Consulta para las columnas y tipos

Usar un IDE de R o RGui.exe para ejecutar el script de R. 

En primer lugar, obtenga una lista de las columnas y sus tipos de datos. Puede usar la función [rxGetVarInfo](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxgetvarinfoxdf) y especifique el origen de datos que desea analizar. Según la versión de **RevoScaleR**, también puede usar [rxGetVarNames](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxgetvarnames). 
  
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

Todas las variables se almacenan como enteros, pero algunas de las variables representan datos categóricos denominados *variables de factor* en R. Por ejemplo, la columna *estado* contiene números que se usan como identificadores para los 50 estados, más el distrito de Columbia. Para facilitar la comprensión de los datos, reemplace los números con una lista de abreviaturas de estado.

En este paso, creará un vector de cadena que contiene las abreviaturas y, a continuación, asignará estos valores categóricos a los identificadores enteros originales. A continuación, usar la nueva variable en el *colInfo* argumento, para especificar que esta columna se tratará como un factor. Cada vez que se analizan los datos o moverlo, se usan las abreviaturas y la columna se tratará como un factor.

Asignar la columna a las abreviaturas antes de usarla como un factor mejora realmente también el rendimiento. Para obtener más información, consulte [R y los datos de optimización](../r/r-and-data-optimization-r-services.md).

1. Empiece por crear una variable de R, *stateAbb*y defina el vector de cadenas que se agregan a él, como se indica a continuación.
  
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
  
3. Para crear el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] origen de datos que usa los datos actualizados, llame a la **RxSqlServerData** funcionando como antes, pero agregue el *colInfo* argumento.
  
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