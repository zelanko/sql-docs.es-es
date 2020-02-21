---
title: Modificar datos de SQL mediante RevoScaleR
description: 'Tutorial 3 de RevoScaleR: Consulta y modificación de datos mediante el lenguaje R en SQL Server.'
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 48802f815515948c957c718e4bf666b0d7133670
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/31/2020
ms.locfileid: "74947085"
---
# <a name="query-and-modify-the-sql-server-data-sql-server-and-revoscaler-tutorial"></a>Consulta y modificación de datos de SQL Server (tutorial de SQL Server y RevoScaleR)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Este es el tutorial 3 de la [serie de tutoriales de RevoScaleR](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md) sobre el uso de las [funciones de RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) con SQL Server.

En el tutorial anterior, cargó los datos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. En este tutorial, puede explorar y modificar los datos mediante **RevoScaleR**:

> [!div class="checklist"]
> * Devolver información básica sobre las variables
> * Crear datos categóricos a partir de datos sin procesar

Los datos categóricos, o *variables de factor*, son útiles para las visualizaciones de datos exploratorias. Puede usarlos como entradas para los histogramas para hacerse una idea de qué aspecto tienen los datos de variables.

## <a name="query-for-columns-and-types"></a>Consultar columnas y tipos

Use un IDE de R o RGui.exe para ejecutar el script de R. 

En primer lugar, obtenga una lista de las columnas y sus tipos de datos. Use la función [rxGetVarInfo](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxgetvarinfoxdf) y especifique el origen de datos que quiera analizar. Según la versión de **RevoScaleR**, también puede usar [rxGetVarNames](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxgetvarnames). 
  
```R
rxGetVarInfo(data = sqlFraudDS)
```

**Resultados**

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

## <a name="create-categorical-data"></a>Crear datos categóricos

Todas las variables se almacenan como enteros, pero algunas de las variables representan datos categóricos denominados *variables de factor* en R. Por ejemplo, la columna *state* contiene números que se usan como identificadores de los 50 estados, más el Distrito de Columbia. Para facilitar la comprensión de los datos, reemplace los números con una lista de abreviaturas de estado.

En este paso, creará un vector de cadena que contenga las abreviaturas y, después, asignará estos valores categóricos a los identificadores enteros originales. Después usará la nueva variable en el argumento *colInfo* para especificar que esta columna se trate como un factor. Cada vez que analice o mueva los datos, se usan las abreviaturas y la columna se trata como un factor.

Asignar la columna a las abreviaturas antes de usarla como un factor mejora realmente también el rendimiento. Para más información, vea [R y optimización de datos](../r/r-and-data-optimization-r-services.md).

1. Para empezar, cree una variable de R, *stateAbb*, y defina el vector de cadenas que se agregará, como sigue:
  
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
  
3. Para crear el origen de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que usa los datos actualizados, llame a la función **RxSqlServerData** como antes, pero agregue el argumento *colInfo*.
  
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

    **Resultados**
    
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