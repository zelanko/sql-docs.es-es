---
title: Estadísticas de resumen en RevoScaleR
description: Tutorial sobre cómo calcular estadísticas de resumen de proceso con el lenguaje R en SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 4ece8cdac4f39cfd5d4b93484f18b0d415cc2291
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/07/2019
ms.locfileid: "73727297"
---
# <a name="compute-summary-statistics-in-r-sql-server-and-revoscaler-tutorial"></a>Estadísticas de resumen de proceso en R (tutorial de SQL Server y RevoScaleR)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Esta lección forma parte del [tutorial de RevoScaleR](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md) sobre el uso de [funciones de RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) con SQL Server.

Usa los orígenes de datos establecidos y los contextos de proceso creados en lecciones anteriores para ejecutar scripts de R de alta eficacia en este. En esta lección, usará contextos de proceso de servidores locales y remotos para estas tareas:

> [!div class="checklist"]
> * Cambio del contexto de proceso a SQL Server
> * Obtener estadísticas de resumen sobre objetos de datos remotos
> * Procesar un resumen local

Si ha completado las lecciones anteriores, debería tener estos contextos de proceso remotos: sqlCompute y sqlComputeTrace. Más adelante, usará sqlCompute y el contexto de proceso local en lecciones posteriores.

Use un IDE de R o **Rgui** para ejecutar el script de R en esta lección.

## <a name="compute-summary-statistics-on-remote-data"></a>Procesar estadísticas de resumen en datos remotos

Antes de ejecutar cualquier código R de forma remota, debe especificar el contexto de proceso remoto. Todos los procesos posteriores tienen lugar en el equipo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] especificado en el parámetro *sqlCompute*.

Un contexto de proceso permanece activo hasta que se cambia. Pero todos los scripts de R que *no* se puedan ejecutar en un contexto de servidor remoto se ejecutarán localmente de forma automática.

Para ver cómo funciona un contexto de proceso, genere estadísticas de resumen en el origen de datos sqlFraudDS en el servidor SQL Server remoto. Este objeto de origen de datos se creó en la [lección dos](deepdive-create-sql-server-data-objects-using-rxsqlserverdata.md) y representa la tabla ccFraudSmall en la base de datos RevoDeepDive. 

1. Cambie el contexto de proceso a sqlCompute creado en la lección anterior:
  
    ```R
    rxSetComputeContext(sqlCompute)
    ```

2. Llame a la función [rxSummary](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsummary) y pase los argumentos necesarios, como la fórmula y el origen de datos, y asigne los resultados a la variable `sumOut`.
  
    ```R
    sumOut <- rxSummary(formula = ~gender + balance + numTrans + numIntlTrans + creditLine, data = sqlFraudDS)
    ```
  
    El lenguaje R proporciona muchas funciones de resumen, pero **rxSummary** en **RevoScaleR** admite la ejecución en varios contextos de proceso remotos, incluido [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para saber más sobre funciones similares, vea [Resúmenes de datos mediante RevoScaleR](https://docs.microsoft.com/machine-learning-server/r/how-to-revoscaler-data-summaries).
  
3. Imprima el contenido de sumOut en la consola.
  
    ```R
    sumOut
    ```
    > [!NOTE]
    > Si recibe un error, espere unos minutos a que finalice la ejecución antes de volver a intentar el comando.

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
  
2. Al extraer datos de SQL Server, a menudo puede obtener un mejor rendimiento si aumenta el número de filas extraídas para cada lectura, suponiendo que haya espacio para el tamaño de bloque ampliado en la memoria. Ejecute este comando para aumentar el valor del parámetro *rowsPerRead* en el origen de datos. Antes, el valor de *rowsPerRead* estaba establecido en 5000.
  
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

4. Vuelva al contexto de proceso remoto para las siguientes lecciones.

    ```R
    rxSetComputeContext(sqlCompute)
    ```

## <a name="next-steps"></a>Pasos siguientes

> [!div class="nextstepaction"]
> [Visualizar datos de SQL Server con R](../../advanced-analytics/tutorials/deepdive-visualize-sql-server-data-using-r.md)