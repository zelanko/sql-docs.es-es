---
title: Cargar datos en memoria mediante rxImport (SQL y R profundización) | Documentos de Microsoft
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: ea5a977f1504a245e270a93a876ac617d8aa6852
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="load-data-into-memory-using-rximport-sql-and-r-deep-dive"></a>Cargar datos en la memoria usando rxImport (SQL y R profundización)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Este artículo forma parte del tutorial exhaustiva de ciencia de datos, acerca de cómo usar [RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) con SQL Server.

El [rxImport](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rximport) función puede utilizarse para mover datos desde un origen de datos en una trama de datos en memoria para la sesión, o en un archivo xdf. en el disco. Si no especifica un archivo como destino, los datos se colocan en memoria como una trama de datos.

En este paso, aprenderá cómo obtener datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]y, a continuación, use la **rxImport** función poner los datos de interés en un archivo local. De este modo, puede analizarlos en el contexto de cálculo local varias veces, sin tener que volver a consultar la base de datos.

## <a name="extract-a-subset-of-data-from-sql-server-to-local-memory"></a>Extraer un subconjunto de datos de SQL Server en la memoria local

Ha decidido que desea examinar a sólo las personas de alto riesgo con más detalle. La tabla de origen en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] es grande, por lo que desea obtener la información sobre los clientes de alto riesgo. A continuación, cargar datos en una trama de datos en la memoria de la estación de trabajo local.

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

    Si la operación se realizó correctamente, debería ver un mensaje de estado como esta: "filas leídas: 35, procesados Total de filas: 35, tiempo Total de fragmentos: 0.036 segundos"

4. Ahora que las observaciones de alto riesgo se encuentran en un marco de datos en memoria, puede usar varias funciones de R para manipular la trama de datos. Por ejemplo, puede ordenar los clientes por su puntuación de riesgo e imprimir una lista de los clientes que suponen un riesgo más alto.

    ```R
    orderedHighRisk <- highRisk[order(-highRisk$ccFraudProb),]
    row.names(orderedHighRisk) <- NULL
    head(orderedHighRisk)
    ```

**Resultado**

*ccFraudLogitScore   state gender cardholder balance numTrans numIntlTrans creditLine ccFraudProb1*

*9.786345    SD   Male  Principal   23456       25            5 75   0.99994382*

*9.433040    FL Female  Principal   20629       24           28 75   0.99992003*

*8.556785    NY Female  Principal   19064       82           53 43   0.99980784*

*8.188668    AZ Female  Principal   19948       29            0 75   0.99972235*

*7.551699    NY Female  Principal   11051       95            0 75   0.99947516*

*7.335080    NV   Male  Principal   21566        4            6  75   0.9993482*

## <a name="more-about-rximport"></a>Más información sobre rxImport

Puede usar **rxImport** no solo para mover los datos, sino también para transformar los datos mientras se leen. Por ejemplo, puede especificar el número de caracteres para las columnas de ancho fijo, proporcionar una descripción de las variables, establecer niveles para las columnas de factor e incluso crear nuevos niveles para usar después de la importación.

El **rxImport** función asigna nombres de variables a las columnas durante el proceso de importación, pero puede indicar nombres de variable nueva mediante el uso de la *colInfo* parámetros o tipos de datos de cambio mediante la *colClasses* parámetro.

Mediante la especificación de operaciones adicionales en el parámetro *transforms* , puede realizar un procesamiento elemental en cada fragmento de datos que se lee.

## <a name="next-step"></a>Paso siguiente

[Crear una nueva tabla de SQL Server mediante rxDataStep](../../advanced-analytics/tutorials/deepdive-create-new-sql-server-table-using-rxdatastep.md)

## <a name="previous-step"></a>Paso anterior

[Transformar datos mediante R](../../advanced-analytics/tutorials/deepdive-transform-data-using-r.md)

