---
title: Carga de datos en memoria mediante RevoScaleR rxImport
description: Tutorial tutorial sobre cómo cargar datos mediante el lenguaje R en SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 0e498e2aff0f6c21d11e4c34439301f36119257f
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/01/2019
ms.locfileid: "68714923"
---
# <a name="load-data-into-memory-using-rximport-sql-server-and-revoscaler-tutorial"></a>Carga de datos en memoria mediante rxImport (tutorial de SQL Server y RevoScaleR)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Esta lección forma parte del [tutorial de RevoScaleR](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md) sobre cómo usar [las funciones de RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) con SQL Server.

La función [rxImport](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rximport) se puede usar para trasladar datos de un origen de datos a una trama de datos en la memoria de la sesión o a un archivo XDF en el disco. Si no especifica un archivo como destino, los datos se colocan en memoria como una trama de datos.

En este paso, aprenderá a obtener datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]y, a continuación, usará la función **rxImport** para colocar los datos de interés en un archivo local. De este modo, puede analizarlos en el contexto de cálculo local varias veces, sin tener que volver a consultar la base de datos.

## <a name="extract-a-subset-of-data-from-sql-server-to-local-memory"></a>Extraer un subconjunto de datos de SQL Server a la memoria local

Ha decidido que solo desea examinar los usuarios de alto riesgo con más detalle. La tabla de origen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de es grande, por lo que desea obtener la información sobre los clientes de alto riesgo. A continuación, cargue los datos en una trama de datos en la memoria de la estación de trabajo local.

1. Restablezca el contexto de cálculo a su estación de trabajo local.

    ```R
    rxSetComputeContext("local")
    ```

2. Cree un nuevo objeto de origen de datos de SQL Server proporcionando una instrucción de SQL válida en el parámetro *rxImport* . En este ejemplo se obtiene un subconjunto de las observaciones con las puntuaciones de riesgo más altas. De este modo, solo los datos que necesita realmente se colocan en la memoria local.

    ```R
    sqlServerProbDS \<- RxSqlServerData(
        sqlQuery = paste("SELECT * FROM ccScoreOutput2",
        "WHERE (ccFraudProb > .99)"),
        connectionString = sqlConnString)
    ```

3. Llame a la función [rxImport](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rximport) para leer los datos en una trama de datos en la sesión local de R.

    ```R
    highRisk <- rxImport(sqlServerProbDS)
    ```

    Si la operación se realizó correctamente, debería ver un mensaje de estado similar al siguiente: "Filas leídas: 35, total de filas procesadas: 35, tiempo total de fragmentos: 0,036 segundos "

4. Ahora que las observaciones de alto riesgo se encuentran en una trama de datos en memoria, puede usar varias funciones de R para manipular la trama de datos. Por ejemplo, puede ordenar a los clientes por su puntuación de riesgo e imprimir una lista de los clientes que suponen un riesgo más alto.

    ```R
    orderedHighRisk <- highRisk[order(-highRisk$ccFraudProb),]
    row.names(orderedHighRisk) <- NULL
    head(orderedHighRisk)
    ```

**Resultado**

```R
ccFraudLogitScore   state gender cardholder balance numTrans numIntlTrans creditLine ccFraudProb1
9.786345    SD   Male  Principal   23456       25            5 75   0.99994382
9.433040    FL Female  Principal   20629       24           28 75   0.99992003
8.556785    NY Female  Principal   19064       82           53 43   0.99980784
8.188668    AZ Female  Principal   19948       29            0 75   0.99972235
7.551699    NY Female  Principal   11051       95            0 75   0.99947516
7.335080    NV   Male  Principal   21566        4            6  75   0.9993482
```

## <a name="more-about-rximport"></a>Más información sobre rxImport

Puede usar **rxImport** no solo para mover los datos, sino también para transformar los datos mientras se leen. Por ejemplo, puede especificar el número de caracteres para las columnas de ancho fijo, proporcionar una descripción de las variables, establecer niveles para las columnas de factor e incluso crear nuevos niveles para usar después de la importación.

La función **rxImport** asigna nombres de variable a las columnas durante el proceso de importación, pero puede indicar nombres de variable nuevos mediante el parámetro *colInfo* o cambiar los tipos de datos mediante el parámetro *colClasses* .

Mediante la especificación de operaciones adicionales en el parámetro *transforms* , puede realizar un procesamiento elemental en cada fragmento de datos que se lee.

## <a name="next-steps"></a>Pasos siguientes

> [!div class="nextstepaction"]
> [Crear una nueva tabla de SQL Server mediante rxDataStep](../../advanced-analytics/tutorials/deepdive-move-data-between-sql-server-and-xdf-file.md)