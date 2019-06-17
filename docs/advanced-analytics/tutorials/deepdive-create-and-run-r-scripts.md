---
title: 'Calcular las estadísticas de resumen RevoScaleR tutorial: SQL Server Machine Learning'
description: Tutorial del tutorial sobre cómo calcular las estadísticas de resumen Estadísticas usando el lenguaje R en SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 883a4afa68571c18e6dcaffe96d12644f611f99a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62641335"
---
# <a name="compute-summary-statistics-in-r-sql-server-and-revoscaler-tutorial"></a>Calcular las estadísticas de resumen en R (tutorial de SQL Server y RevoScaleR)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

En esta lección forma parte de la [RevoScaleR tutorial](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md) sobre cómo usar [funciones de RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) con SQL Server.

Los orígenes de datos establecidas y contextos de proceso que creó en lecciones anteriores usa para ejecutar scripts de R de alta potencia en este caso. En esta lección, usará los contextos de proceso de servidor local y remoto para las siguientes tareas:

> [!div class="checklist"]
> * Cambiar el contexto de cálculo a SQL Server
> * Obtener estadísticas de resumen sobre los objetos de datos remotos
> * Calcular un resumen local

Si ha completado las lecciones anteriores, debe tener los siguientes contextos de cálculo remoto: sqlCompute y sqlComputeTrace. Más adelante, que usa sqlCompute y local calculará contexto en lecciones posteriores.

Usar un IDE de R o **Rgui** para ejecutar el script de R en esta lección.

## <a name="compute-summary-statistics-on-remote-data"></a>Calcular las estadísticas de resumen de datos remotos

Antes de que puede ejecutar cualquier código R de forma remota, deberá especificar el contexto de proceso remoto. Todos los cálculos posteriores tienen lugar el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] equipo especificado en el *sqlCompute* parámetro.

Un contexto de proceso permanece activo hasta que la cambie. Sin embargo, los scripts de R que *no* ejecución en un contexto de servidor remoto se ejecutará automáticamente localmente.

Para ver cómo funciona un contexto de cálculo, generar estadísticas de resumen sobre el origen de datos sqlFraudDS en el servidor SQL remoto. Se creó este objeto de origen de datos en [lección dos](deepdive-create-sql-server-data-objects-using-rxsqlserverdata.md) y representa la tabla ccFraudSmall en la base de datos RevoDeepDive. 

1. Cambiar el contexto de cálculo a sqlCompute que creó en la lección anterior:
  
    ```R
    rxSetComputeContext(sqlCompute)
    ```

2. Llame a la [rxSummary](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsummary) funcionando y pase los argumentos necesarios, como la fórmula y el origen de datos y asigne los resultados a la variable `sumOut`.
  
    ```R
    sumOut <- rxSummary(formula = ~gender + balance + numTrans + numIntlTrans + creditLine, data = sqlFraudDS)
    ```
  
    El lenguaje R proporciona muchas funciones de resumen, pero **rxSummary** en **RevoScaleR** admite la ejecución en varios contextos de cálculo remoto, incluidos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obtener información sobre funciones similares, vea [resúmenes de los datos con RevoScaleR](https://docs.microsoft.com/machine-learning-server/r/how-to-revoscaler-data-summaries).
  
3. Imprimir el contenido de sumOut en la consola.
  
    ```R
    sumOut
    ```
    > [!NOTE]
    > Si se produce un error, espere unos minutos para que finalice antes de reintentar el comando de la ejecución.

**Resultado**

```R
Summary Statistics Results for: ~gender + balance + numTrans + numIntlTrans + creditLine
Data: sqlFraudDS (RxSqlServerData Data Source)
Number of valid observations: 10000

 Name  Mean    StdDev  Min Max ValidObs    MissingObs
 balance       4075.0318 3926.558714            0   25626 100000
 numTrans        29.1061   26.619923 0     100 10000    0           100000
 numIntlTrans     4.0868    8.726757 0      60 10000    0           100000
 creditLine       9.1856    9.870364 1      75 10000    0          100000
 
 Category Counts for gender
 Number of categories: 2
 Number of valid observations: 10000
 Number of missing observations: 0

 gender Counts
  Male   6154
  Female 3846
```

## <a name="create-a-local-summary"></a>Crear un resumen local

1. Cambie el contexto de proceso para hacer todo el trabajo localmente.
  
    ```R
    rxSetComputeContext ("local")
    ```
  
2. Al extraer datos de SQL Server, a menudo encontrará un mejor rendimiento si aumenta el número de filas que se extraen para cada lectura, suponiendo que se puede incluir el tamaño del mayor bloque de memoria. Ejecute el siguiente comando para aumentar el valor para el *rowsPerRead* parámetro en el origen de datos. Antes, el valor de *rowsPerRead* estaba establecido en 5000.
  
    ```R
    sqlServerDS1 <- RxSqlServerData(
       connectionString = sqlConnString,
       table = sqlFraudTable,
       colInfo = ccColInfo,
       rowsPerRead = 10000)
    ```

3. Llame a **rxSummary** en el nuevo origen de datos.
  
    ```R
    rxSummary(formula = ~gender + balance + numTrans + numIntlTrans + creditLine, data = sqlServerDS1)
    ```
  
   Los resultados actuales deben ser los mismos que cuando ejecuta **rxSummary** en el contexto del equipo de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . En cambio, la operación puede ser más rápida o más lenta. Depende en gran medida de la conexión a la base de datos, ya que los datos se transfieren al equipo local para el análisis.

4. Vuelva a remoto el contexto de proceso para el siguientes varias lecciones.

    ```R
    rxSetComputeContext(sqlCompute)
    ```

## <a name="next-steps"></a>Pasos siguientes

> [!div class="nextstepaction"]
> [Visualizar datos de SQL Server con R](../../advanced-analytics/tutorials/deepdive-visualize-sql-server-data-using-r.md)