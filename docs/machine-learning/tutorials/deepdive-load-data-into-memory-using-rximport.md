---
title: Carga de datos mediante rxImport
description: Aprenda a obtener datos de SQL Server y, después, a usar la función rxImport para colocar los datos de interés en un archivo local.
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 7c31650525934b14bf31135264d9b86c52d85119
ms.sourcegitcommit: 9b41725d6db9957dd7928a3620fe4db41eb51c6e
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/13/2020
ms.locfileid: "88179954"
---
# <a name="load-data-into-memory-using-rximport-sql-server-and-revoscaler-tutorial"></a>Carga de datos en memoria mediante rxImport (tutorial de SQL Server y RevoScaleR)
[!INCLUDE [SQL Server 2016 and later](../../includes/applies-to-version/sqlserver2016.md)]

Este es el tutorial 10 de la [serie de tutoriales de RevoScaleR](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md) sobre el uso de las [funciones de RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) con SQL Server.

En este tutorial, aprenderá cómo obtener datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]y, después, usar la función **rxImport** para colocar los datos de interés en un archivo local. De este modo, puede analizarlos en el contexto de cálculo local varias veces, sin tener que volver a consultar la base de datos.

La función [rxImport](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rximport) se puede usar para mover datos desde un origen de datos a una trama de datos en una memoria de sesión o en un archivo XDF en disco. Si no especifica un archivo como destino, los datos se colocan en memoria como una trama de datos.

## <a name="extract-a-subset-of-data-from-sql-server-to-local-memory"></a>Extracción de un subconjunto de datos desde SQL Server a la memoria local

Ha decidido que solo quiere examinar los individuos de alto riesgo con más detalle. La tabla de origen de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] es grande, por lo que quiere obtener información única y exclusivamente sobre los clientes de alto riesgo. Luego, cargará los datos en una trama de datos en la memoria de la estación de trabajo local.

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

3. Llame a la función [rxImport](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rximport) para leer los datos en una trama de datos de la sesión de R local.

    ```R
    highRisk <- rxImport(sqlServerProbDS)
    ```

    Si la operación se realiza correctamente, debería aparecer un mensaje de estado similar al siguiente: "Filas leídas: 35, Total de filas procesadas: 35, Tiempo total de fragmentos: 0,036 segundos"

4. Ahora que las observaciones de alto riesgo están en una trama de datos en memoria, puede usar varias funciones de R para manipular esa trama de datos. En este ejemplo, puede ordenar los clientes por su puntuación de riesgo e imprimir una lista de aquellos que suponen un riesgo más alto.

    ```R
    orderedHighRisk <- highRisk[order(-highRisk$ccFraudProb),]
    row.names(orderedHighRisk) <- NULL
    head(orderedHighRisk)
    ```

**Resultados**

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

La función **rxImport** asigna nombres de variable a las columnas durante el proceso de importación, pero puede indicar nombres de variable nuevos con el parámetro *colInfo* o cambiar los tipos de datos con el parámetro *colClasses*.

Mediante la especificación de operaciones adicionales en el parámetro *transforms* , puede realizar un procesamiento elemental en cada fragmento de datos que se lee.

## <a name="next-steps"></a>Pasos siguientes

> [!div class="nextstepaction"]
> [Crear una nueva tabla de SQL Server mediante rxDataStep](../../machine-learning/tutorials/deepdive-move-data-between-sql-server-and-xdf-file.md)