---
title: 'Cargar datos en memoria mediante rxImport RevoScaleR: SQL Server Machine Learning'
description: Tutorial del tutorial sobre cómo cargar datos mediante el lenguaje R en SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 5fc29872795623bd0d9e72414a15add92591ec7d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62641392"
---
# <a name="load-data-into-memory-using-rximport-sql-server-and-revoscaler-tutorial"></a>Cargar datos en memoria mediante rxImport (tutorial de SQL Server y RevoScaleR)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

En esta lección forma parte de la [RevoScaleR tutorial](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md) sobre cómo usar [funciones de RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) con SQL Server.

El [rxImport](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rximport) función se puede usar para mover datos desde un origen de datos en una trama de datos en memoria para la sesión, o en un archivo XDF en disco. Si no especifica un archivo como destino, los datos se colocan en memoria como una trama de datos.

En este paso, obtendrá información sobre cómo obtener datos desde [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]y, a continuación, utilice el **rxImport** función para colocar los datos de interés en un archivo local. De este modo, puede analizarlos en el contexto de cálculo local varias veces, sin tener que volver a consultar la base de datos.

## <a name="extract-a-subset-of-data-from-sql-server-to-local-memory"></a>Extraer un subconjunto de datos de SQL Server a la memoria local

Ha decidido que desea examinar a solo los individuos de alto riesgo con más detalle. La tabla de origen en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] es grande, por lo que desee obtener la información sobre los clientes de alto riesgo. A continuación, cargar esos datos en una trama de datos en la memoria de la estación de trabajo local.

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

3. Llame a la función [rxImport](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rximport) para leer los datos en una trama de datos en la sesión de R local.

    ```R
    highRisk <- rxImport(sqlServerProbDS)
    ```

    Si la operación se realizó correctamente, debería ver un mensaje de estado como esta: "Filas leídas: 35, filas procesadas: 35, tiempo de fragmentos total: 0,036 segundos"

4. Ahora que las observaciones de alto riesgo se encuentran en una trama de datos en memoria, puede usar varias funciones de R para manipular la trama de datos. Por ejemplo, puede ordenar los clientes por su puntuación de riesgo y una lista de los clientes que supongan un riesgo más alto de impresión.

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

El **rxImport** función asigna los nombres de variables a las columnas durante el proceso de importación, pero puede indicar nombres de variable nuevos mediante el *colInfo* parámetros o tipos de datos de cambio mediante la *colClasses* parámetro.

Mediante la especificación de operaciones adicionales en el parámetro *transforms* , puede realizar un procesamiento elemental en cada fragmento de datos que se lee.

## <a name="next-steps"></a>Pasos siguientes

> [!div class="nextstepaction"]
> [Crear una nueva tabla de SQL Server mediante rxDataStep](../../advanced-analytics/tutorials/deepdive-move-data-between-sql-server-and-xdf-file.md)