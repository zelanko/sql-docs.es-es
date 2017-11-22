---
title: Cargar datos en memoria mediante rxImport | Documentos de Microsoft
ms.custom: 
ms.date: 05/18/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to: SQL Server 2016
dev_langs: R
ms.assetid: 47a42e9a-05a0-4a50-871d-de73253cf070
caps.latest.revision: "14"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 85d6174686be113ff9a23985b1d5b5763783c986
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2017
---
# <a name="load-data-into-memory-using-rximport"></a>Cargar datos en memoria mediante rxImport

La función **rxImport** se puede usar para mover datos desde un origen de datos a una trama de datos en una memoria de sesión de R o en un archivo XDF en disco. Si no especifica un archivo como destino, los datos se colocan en memoria como una trama de datos.

En este paso, obtendrá información sobre cómo obtener datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]y, a continuación, use la función rxImport para poner los datos de interés en un archivo local. De este modo, puede analizarlos en el contexto de cálculo local varias veces, sin tener que volver a consultar la base de datos.

## <a name="extract-a-subset-of-data-from-sql-server-to-local-memory"></a>Extraer un subconjunto de datos de SQL Server a la memoria Local

Ha decidido que solo quiere examinar los individuos de alto riesgo con más detalle. La tabla de origen en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] es grande, por lo que solo obtendrá la información de los clientes de alto riesgo y la cargará en una trama de datos en la memoria de la estación de trabajo local.

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

3. Use la función **rxImport** para cargar realmente los datos en una trama de datos de la sesión de R local.

    ```R
    highRisk <- rxImport(sqlServerProbDS)
    ```

    Si la operación se ha realizado correctamente, debería ver un mensaje de estado: Filas leídas: 35, total de filas procesadas: 35, tiempo total de fragmentos: 0,036 segundos.

4. Ahora que tiene las observaciones de alto riesgo en una trama de datos en memoria, puede usar varias funciones de R para manipular la trama de datos. Para este ejemplo, puede ordenar los clientes por su puntuación de riesgo e imprimir los que supongan un riesgo más alto.

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

Puede usar rxImport no solo para mover los datos, pero para transformar los datos en el proceso que lo lean. Por ejemplo, puede especificar el número de caracteres para las columnas de ancho fijo, proporcionar una descripción de las variables, establecer niveles para las columnas de factor e incluso crear nuevos niveles para usar después de la importación.

La función rxImport asigna nombres de variables a las columnas durante el proceso de importación, pero puede indicar nombres de variable nueva mediante el uso de la *colInfo* parámetro y se pueden cambiar los tipos de datos mediante la *colClasses* parámetro.

Mediante la especificación de operaciones adicionales en el parámetro *transforms* , puede realizar un procesamiento elemental en cada fragmento de datos que se lee.

## <a name="next-step"></a>Paso siguiente

[Crear nueva tabla de SQL Server mediante rxDataStep](../../advanced-analytics/tutorials/deepdive-create-new-sql-server-table-using-rxdatastep.md)

## <a name="previous-step"></a>Paso anterior

[Transformar datos mediante R](../../advanced-analytics/tutorials/deepdive-transform-data-using-r.md)

## <a name="see-also"></a>Vea también

[Tutoriales de aprendizaje automático](../../advanced-analytics/tutorials/machine-learning-services-tutorials.md)

