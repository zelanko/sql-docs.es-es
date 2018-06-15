---
title: Consultar y modificar los datos de SQL Server (SQL y R profundización) | Documentos de Microsoft
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 90b836cd09fd0c6f130ff65c531f6077a28c2014
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
ms.locfileid: "31202227"
---
# <a name="query-and-modify-the-sql-server-data-sql-and-r-deep-dive"></a>Consultar y modificar los datos de SQL Server (SQL y R profundización)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Este artículo forma parte del tutorial exhaustiva de ciencia de datos, acerca de cómo usar [RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) con SQL Server.

Ahora que ha cargado los datos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], puede usar los orígenes de datos que ha creado como argumentos para funciones de R en [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]para obtener información básica sobre las variables y generar resúmenes e histogramas.

En este paso, volver a usar los orígenes de datos para realizar un análisis rápido y, a continuación, mejorar los datos.

## <a name="query-the-data"></a>Consultar los datos

En primer lugar, obtenga una lista de las columnas y sus tipos de datos.

1.  Use la función [rxGetVarInfo](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxgetvarinfoxdf) y especifique el origen de datos que desea analizar.

    Dependiendo de la versión de RevoScaleR, también puede usar [rxGetVarNames](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxgetvarnames). 
  
    ```R
    rxGetVarInfo(data = sqlFraudDS)
    ```

    **Resultado**
    
    *Var 1: custID, Type: integer*
    
    *Var 2: gender, Type: integer*
    
    *Var 3: state, Type: integer*
    
    *Var 4: cardholder, Type: integer*
    
    *Var 5: balance, Type: integer*
    
    *Var 6: numTrans, Type: integer*
    
    *Var 7: numIntlTrans, Type: integer*
    
    *Var 8: creditLine, Type: integer*
    
    *Var 9: fraudRisk, Type: integer*


## <a name="modify-metadata"></a>Modificar los metadatos

Todas las variables se almacenan como enteros, pero algunas de las variables representan datos categóricos denominados *variables de factor* en R. Por ejemplo, el *estado* de la columna contiene números que se usan como identificadores de los 50 estados, más el Distrito de Columbia.  Para facilitar la comprensión de los datos, reemplace los números con una lista de abreviaturas de estado.

En este paso, crear un vector de cadena que contiene las abreviaturas y, a continuación, asignar los valores de estas categorías para los identificadores de enteros original. A continuación, usar la nueva variable en la *colInfo* argumento, para especificar que esta columna se trate como un factor. Cada vez que analice los datos o moverlo, se utilizan las abreviaturas y la columna se trata como un factor.

Asignar la columna a las abreviaturas antes de usarla como un factor mejora realmente también el rendimiento. Para obtener más información, consulte [optimización R y datos](..\r\r-and-data-optimization-r-services.md).

1. Empiece por crear una variable de R, *stateAbb*, y defina el vector de cadenas que se agregará, como sigue:
  
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
  
3. Para crear el origen de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que usa los datos actualizados, llame a la función **RxSqlServerData** como antes pero agregue el argumento *colInfo* .
  
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
    
    *Var 1: custID, Type: integer*
    
    *Var 2: 2 niveles de factor de género: masculina femenino*
    
    *Var 3: 51 niveles de factor de estado: AK AL AR AZ CA... VT WA WI WV WY*
    
    *Var 4: niveles de factor información de los titulares 2: entidad de seguridad de base de datos secundaria*
    
    *Var 5: balance, Type: integer*
    
    *Var 6: numTrans, Type: integer*
    
    *Var 7: numIntlTrans, Type: integer*
    
    *Var 8: creditLine, Type: integer*
    
    *Var 9: fraudRisk, Type: integer*

Ahora las tres variables que ha especificado (_gender_, _state_y _cardholder_) se tratan como factores.

## <a name="next-step"></a>Paso siguiente

[Definir y usar contextos de cálculo](../../advanced-analytics/tutorials/deepdive-define-and-use-compute-contexts.md)

## <a name="previous-step"></a>Paso anterior

[Crear objetos de datos de SQL Server mediante RxSqlServerData](../../advanced-analytics/tutorials/deepdive-create-sql-server-data-objects-using-rxsqlserverdata.md)
