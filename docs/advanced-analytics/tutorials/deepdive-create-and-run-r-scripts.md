---
title: Tutorial de Compute Summary Statistics RevoScaleR
description: Tutorial tutorial sobre cómo calcular estadísticas de resumen estadístico con el lenguaje R en SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.openlocfilehash: 5f90cc0e6101e168e15ed7c1145d286f799375ac
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/19/2019
ms.locfileid: "68344709"
---
# <a name="compute-summary-statistics-in-r-sql-server-and-revoscaler-tutorial"></a>Estadísticas de Resumen de proceso en R (tutorial de SQL Server y RevoScaleR)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Esta lección forma parte del [tutorial de RevoScaleR](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md) sobre cómo usar [las funciones de RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) con SQL Server.

Usa los orígenes de datos y contextos de cálculo establecidos creados en lecciones anteriores para ejecutar scripts de R de alta potencia en este. En esta lección, usará contextos de cálculo de servidores locales y remotos para las siguientes tareas:

> [!div class="checklist"]
> * Cambiar el contexto de cálculo a SQL Server
> * Obtener estadísticas de resumen sobre objetos de datos remotos
> * Calcular un resumen local

Si ha completado las lecciones anteriores, debería tener estos contextos de cálculo remotos: sqlCompute y sqlComputeTrace. En el futuro, usará sqlCompute y el contexto de proceso local en lecciones posteriores.

Use un IDE de R o **Rgui** para ejecutar el script de r en esta lección.

## <a name="compute-summary-statistics-on-remote-data"></a>Calcular estadísticas de resumen en datos remotos

Antes de poder ejecutar cualquier código R de forma remota, debe especificar el contexto de cálculo remoto. Todos los cálculos subsiguientes tienen lugar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en el equipo especificado en el parámetro *sqlCompute* .

Un contexto de cálculo permanece activo hasta que se cambia. Sin embargo, los scripts de R que *no se pueden* ejecutar en un contexto de servidor remoto se ejecutarán automáticamente de forma local.

Para ver cómo funciona un contexto de cálculo, genere estadísticas de resumen en el origen de datos sqlFraudDS en el SQL Server remoto. Este objeto de origen de datos se creó en la [lección dos](deepdive-create-sql-server-data-objects-using-rxsqlserverdata.md) y representa la tabla ccFraudSmall en la base de datos RevoDeepDive. 

1. Cambie el contexto de cálculo a sqlCompute creado en la lección anterior:
  
    ```R
    rxSetComputeContext(sqlCompute)
    ```

2. Llame a la función [rxSummary](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsummary) y pase los argumentos necesarios, como la fórmula y el origen de datos, y asigne los resultados a `sumOut`la variable.
  
    ```R
    sumOut <- rxSummary(formula = ~gender + balance + numTrans + numIntlTrans + creditLine, data = sqlFraudDS)
    ```
  
    El lenguaje R proporciona muchas funciones de Resumen, pero **rxSummary** en **RevoScaleR** admite la ejecución en varios contextos de cálculo remotos, incluido [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obtener información sobre funciones similares, vea [resúmenes de datos con RevoScaleR](https://docs.microsoft.com/machine-learning-server/r/how-to-revoscaler-data-summaries).
  
3. Imprime el contenido de sumOut en la consola.
  
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
  
2. Al extraer datos de SQL Server, a menudo puede obtener un mejor rendimiento si aumenta el número de filas extraídas para cada lectura, suponiendo que se pueda acomodar el mayor tamaño de bloque en la memoria. Ejecute el siguiente comando para aumentar el valor del parámetro *rowsPerRead* en el origen de datos. Antes, el valor de *rowsPerRead* estaba establecido en 5000.
  
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

4. Vuelva al contexto de cálculo remoto para las siguientes lecciones.

    ```R
    rxSetComputeContext(sqlCompute)
    ```

## <a name="next-steps"></a>Pasos siguientes

> [!div class="nextstepaction"]
> [Visualizar datos de SQL Server con R](../../advanced-analytics/tutorials/deepdive-visualize-sql-server-data-using-r.md)