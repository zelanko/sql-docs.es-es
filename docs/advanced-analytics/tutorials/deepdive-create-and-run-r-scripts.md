---
title: Crear y ejecutar scripts de R (SQL y R profundización) | Documentos de Microsoft
ms.date: 12/14/2017
ms.reviewer: ''
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: ''
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: tutorial
applies_to:
- SQL Server 2016
- SQL Server 2017
dev_langs:
- R
ms.author: heidist
author: HeidiSteen
manager: cgronlun
ms.workload: Inactive
ms.openlocfilehash: 38e32f66f52c442090927296db6cd3d1bec62fd0
ms.sourcegitcommit: 059fc64ba858ea2adaad2db39f306a8bff9649c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/04/2018
---
# <a name="create-and-run-r-scripts-sql-and-r-deep-dive"></a>Crear y ejecutar scripts de R (SQL y R profundización)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Este artículo forma parte del tutorial exhaustiva de ciencia de datos, acerca de cómo usar [RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) con SQL Server.

Ahora que ha configurado los orígenes de datos y ha establecido uno o varios contextos de cálculo, está listo para ejecutar scripts de R de alta potencia mediante [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  En esta lección, se utiliza el contexto de proceso de servidor para realizar algunas tareas de aprendizaje de automático comunes:

- Visualizar datos y generar estadísticas de resumen
- Crear un modelo de regresión lineal
- Crear un modelo de regresión logística
- Puntuar nuevos datos y crear un histograma de las puntuaciones

## <a name="change-compute-context-to-the-server"></a>Cambio de contexto en el servidor de proceso

Antes de ejecutar cualquier código R, debe especificar el contexto de cálculo *actual* o *activo* .

1. Para activar un contexto de cálculo que ya ha definido mediante R, use la función **rxSetComputeContext** como se muestra aquí:
  
    ```R
    rxSetComputeContext(sqlCompute)
    ```
  
    En cuanto se ejecuta esta instrucción, todos los cálculos posteriores tienen lugar el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] equipo especificado en el *sqlCompute* parámetro.
  
2. Si decide que prefiere ejecutar el código R en su estación de trabajo, puede cambiar el contexto de cálculo al equipo local mediante la palabra clave  **local** .
  
    ```R
    rxSetComputeContext ("local")
    ```
  
    Para obtener una lista de otras palabras clave admitidas por esta función, escriba `help("rxSetComputeContext")` desde una línea de comandos de R.
  
3. Después de especificar un contexto de cálculo, permanece activo hasta que lo cambie. Pero todos los scripts de R que *no* se puedan ejecutar en un contexto de servidor remoto se ejecutarán localmente.

## <a name="compute-some-summary-statistics"></a>Proceso de algunas estadísticas de resumen

Para ver cómo funciona el contexto de proceso, intente generar algunas estadísticas de resumen utilizando el `sqlFraudDS` origen de datos.  Recuerde que el objeto de origen de datos solo define los datos que se utilice; no cambia el contexto de proceso.

+ Para realizar el resumen de forma local, utilice **rxSetComputeContext** y especifique la _local_ palabra clave.
+ Para crear los mismos cálculos en el equipo de SQL Server, cambie al contexto de cálculo de SQL que ha definido anteriormente.

1. Llame a la [rxSummary](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsummary) función y pasar los argumentos necesarios, por ejemplo, la fórmula y el origen de datos y asigne los resultados a la variable `sumOut`.
  
    ```R
    sumOut <- rxSummary(formula = ~gender + balance + numTrans + numIntlTrans + creditLine, data = sqlFraudDS)
    ```
  
    El lenguaje R proporciona muchas funciones de resumen, pero **rxSummary** admite la ejecución en varios contextos de proceso remoto, incluidos los [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obtener información acerca de funciones similares, vea [resúmenes de los datos con RevoScaleR](https://docs.microsoft.com/machine-learning-server/r/how-to-revoscaler-data-summaries).
  
2. Cuando se realiza el procesamiento, puede imprimir el contenido de la `sumOut` variable en la consola.
  
    ```R
    sumOut
    ```
  
    > [!NOTE]
    > No intente imprimir los resultados antes de que se devuelvan desde el equipo con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o es posible que se produzca un error.

**Resultado**

*Summary Statistics Results for: ~gender + balance + numTrans +*

 *numIntlTrans + creditLine*

 *Data: sqlFraudDS (RxSqlServerData Data Source)*

 *Number of valid observations: 10000*

 *Name  Mean    StdDev  Min Max ValidObs    MissingObs*

 *balance       4075,0318 3926,558714            0   25626 100000*

 *numTrans        29,1061   26,619923 0     100 10000    0           100000*

 *numIntlTrans     4,0868    8,726757 0      60 10000    0           100000*

 *creditLine       9.1856    9.870364 1      75 10000    0          100000*

 *Recuentos de categoría género*

 *Number of categories: 2*

 *Number of valid observations: 10000*

 *Number of missing observations: 0*

 *gender Counts*

 *Male   6154*

  *Female 3846*

## <a name="add-maximum-and-minimum-values"></a>Agregar los valores máximos y mínimos

Según las estadísticas de resumen calculadas, ha descubierto información útil sobre los datos que quiere incluir en el origen de datos para su uso en cálculos adicionales. Por ejemplo, los valores mínimo y máximos se pueden utilizar para calcular los histogramas. Por este motivo, vamos a agregar los valores máximo y mínimo para el **RxSqlServerData** origen de datos.

Afortunadamente [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] incluye funciones optimizadas que pueden convertir eficazmente los datos enteros a los datos de categorías factor.

1. Empiece por configurar algunas variables temporales.
  
    ```R
    sumDF <- sumOut$sDataFrame
    var <- sumDF$Name
    ```
  
2. Use la variable `ccColInfo` que creó anteriormente para definir las columnas del origen de datos.
  
    También, agregar algunas de las columnas calculan nuevas (`numTrans`, `numIntlTrans`, y `creditLine`) a la colección de columnas.
  
    ```R 
    ccColInfo <- list(
        gender = list(type = "factor",
          levels = c("1", "2"), 
          newLevels = c("Male", "Female")),
        cardholder = list(type = "factor",
          levels = c("1", "2"), 
          newLevels = c("Principal", "Secondary")), 
        state = list(type = "factor", 
          levels = as.character(1:51), 
          newLevels = stateAbb), 
        balance  = list(type = "numeric"),
        numTrans = list(type = "factor", 
          levels = as.character(sumDF[var == "numTrans", "Min"]:sumDF[var == "numTrans", "Max"])),
        numIntlTrans = list(type = "factor",  
            levels = as.character(sumDF[var == "numIntlTrans", "Min"]:sumDF[var =="numIntlTrans", "Max"])),
        creditLine = list(type = "numeric")
            )
    ```
  
3. Necesidad de actualizar la colección de columnas, se aplica la siguiente instrucción para crear una versión actualizada de la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] origen de datos que definió anteriormente.
  
    ```R
    sqlFraudDS <- RxSqlServerData(
        connectionString = sqlConnString,
        table = sqlFraudTable,
        colInfo = ccColInfo,
        rowsPerRead = sqlRowsPerRead)
    ```
  
    El `sqlFraudDS` origen de datos ahora incluye las nuevas columnas que se agregan mediante `ccColInfo`.
  

En este momento, las modificaciones afectan únicamente al objeto de origen de datos en R; No hay nuevos datos se ha escrito aún en la tabla de base de datos. Sin embargo, puede usar los datos capturados en el `sumOut` variable para crear visualizaciones y resúmenes. En el paso siguiente aprenderá a hacerlo al cambio de contextos de proceso.

> [!TIP]
> Si olvida qué contexto de proceso que está usando, ejecute `rxGetComputeContext()`.  Un valor devuelto de "Contexto de cálculo de RxLocalSeq" indica que está ejecutando en el contexto de proceso local.

## <a name="next-step"></a>Paso siguiente

[Visualizar datos de SQL Server con R](../../advanced-analytics/tutorials/deepdive-visualize-sql-server-data-using-r.md)

## <a name="previous-step"></a>Paso anterior

[Definir y usar contextos de cálculo](../../advanced-analytics/tutorials/deepdive-define-and-use-compute-contexts.md)
