---
title: Definir y usar contextos de cálculo de RevoScaleR
description: Tutorial sobre cómo definir un contexto de cálculo mediante el lenguaje R en SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.openlocfilehash: 9f7d4911257d583126986cd4079ebe763aae2024
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/19/2019
ms.locfileid: "68344780"
---
# <a name="define-and-use-compute-contexts-sql-server-and-revoscaler-tutorial"></a>Definir y usar contextos de proceso (tutorial de SQL Server y RevoScaleR)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Esta lección forma parte del [tutorial de RevoScaleR](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md) sobre cómo usar [las funciones de RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) con SQL Server.

En la lección anterior, ha usado las funciones de **RevoScaleR** para inspeccionar los objetos de datos. En esta lección se presenta la función [RxInSqlServer](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinsqlserver) , que permite definir un contexto de cálculo para un SQL Server remoto. Con un contexto de cálculo remoto, puede desplazar la ejecución de R de una sesión local a una sesión remota en el servidor. 

> [!div class="checklist"]
> * Obtener información sobre los elementos de un contexto de proceso de SQL Server remoto
> * Habilitar el seguimiento en un objeto de contexto de cálculo

**RevoScaleR** admite varios contextos de cálculo: Hadoop, Spark en HDFS y SQL Server en la base de datos. Por SQL Server, la función **RxInSqlServer** se utiliza para las conexiones del servidor y para pasar objetos entre el equipo local y el contexto de ejecución remoto.

## <a name="create-and-set-a-compute-context"></a>Crear y establecer un contexto de cálculo

La función **RxInSqlServer** que crea el contexto de cálculo SQL Server usa la siguiente información:

+ Cadena de conexión para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] la instancia
+ Especificación de cómo debe controlarse la salida
+ Especificación opcional de un directorio de datos compartido
+ Argumentos opcionales que habilitan el seguimiento o especifican el nivel de seguimiento

Esta sección le guía a través de cada una de las partes.

1. Especifique la cadena de conexión para la instancia en la que se realizan los cálculos. Puede volver a usar la cadena de conexión que creó anteriormente.

    **Con un inicio de sesión de SQL**

    ```R
    sqlConnString <- "Driver=SQL Server;Server=<SQL Server instance name>; Database=<database name>;Uid=<SQL user nme>;Pwd=<password>"
      ```

    **Con la autenticación de Windows**

    ```R
    sqlConnString <- "Driver=SQL Server;Server=instance_name;Database=RevoDeepDive;Trusted_Connection=True"
    ```
    
2. Especifique cómo quiere que se controlen los resultados. El siguiente script dirige la sesión local de R para esperar los resultados del trabajo de R en el servidor antes de procesar la siguiente operación. También suprime la salida de los cálculos remotos para que no aparezcan en la sesión local.
  
    ```R
    sqlWait <- TRUE
    sqlConsoleOutput <- FALSE
    ```
  
    El argumento *wait* para **RxInSqlServer** es compatible con estas opciones:
  
    -   **TRUE**. El trabajo está configurado como bloqueo y no devuelve hasta que se haya completado o haya producido un error.  Para obtener más información, vea [informática paralela y distribuida en machine learning Server](https://docs.microsoft.com/machine-learning-server/r/how-to-revoscaler-distributed-computing).
  
    -   **FALSE**. Los trabajos se configuran como sin bloqueo y se devuelven inmediatamente, lo que le permite continuar ejecutando otro código de R. En cambio, incluso en modo de no bloqueo, la conexión de cliente con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] debe mantenerse mientras se ejecuta el trabajo.

3. Opcionalmente, especifique la ubicación de un directorio local para el uso compartido por la sesión de R local y por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] el equipo remoto y sus cuentas.

    ```R
    sqlShareDir <- paste("c:\\AllShare\\", Sys.getenv("USERNAME"), sep="")
    ```
    
   Si desea crear manualmente un directorio específico para compartir, puede Agregar una línea como la siguiente:

    ```R
    dir.create(sqlShareDir, recursive = TRUE)
    ```

4. Pase argumentos al constructor **RxInSqlServer** para crear el *objeto de contexto de cálculo*.

    ```R
    sqlCompute <- RxInSqlServer(  
         connectionString = sqlConnString,
         wait = sqlWait,
         consoleOutput = sqlConsoleOutput)
    ```
    
    La sintaxis de **RxInSqlServer** es casi idéntica a la de la función **RxSqlServerData** que usó anteriormente para definir el origen de datos. En cambio, hay algunas diferencias importantes.
      
    - El objeto del origen de datos, definido mediante la función [RxSqlServerData](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqlserverdata), especifica dónde se almacenan los datos.
    
    - En cambio, el contexto de cálculo, definido mediante la función [RxInSqlServer](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinsqlserver) indica dónde deben realizarse las agregaciones y otros cálculos.
    
    Definir un contexto de cálculo no afecta a los demás cálculos genéricos de R que puede realizar en la estación de trabajo, y no cambia el origen de los datos. Por ejemplo, puede definir un archivo de texto local como el origen de datos pero cambiar el contexto de cálculo a SQL Server y realizar toda la lectura y los resúmenes en los datos del equipo de SQL Server.

5. Active el contexto de cálculo remoto.

    ```R
    rxSetComputeContext(sqlCompute)
    ```

6. Devuelve información sobre el contexto de cálculo, incluidas sus propiedades.

    ```R
    rxGetComputeContext()
    ```

7. Vuelva a restablecer el contexto de cálculo en el equipo local especificando la palabra clave "local" (en la siguiente lección se muestra cómo usar el contexto de cálculo remoto).

    ```R
    rxSetComputeContext("local")
    ```

> [!Tip]
> Para obtener una lista de otras palabras clave admitidas por esta función, escriba `help("rxSetComputeContext")` desde una línea de comandos de R.

## <a name="enable-tracing"></a>Habilitar el seguimiento

A veces, las operaciones funcionan en su contexto local pero experimentan problemas al ejecutarse en un contexto de cálculo remoto. Si desea analizar problemas o supervisar el rendimiento, puede habilitar el seguimiento en el contexto de proceso para admitir la solución de problemas en tiempo de ejecución.

1. Cree un nuevo contexto de cálculo que use la misma cadena de conexión, pero agregue los argumentos *traceEnabled* y *TraceLevel* al constructor **RxInSqlServer** .

    ```R
    sqlComputeTrace <- RxInSqlServer(
        connectionString = sqlConnString,
        #shareDir = sqlShareDir,
        wait = sqlWait,
        consoleOutput = sqlConsoleOutput,
        traceEnabled = TRUE,
        traceLevel = 7)
    ```
  
   En este ejemplo, la propiedad *traceLevel* se establece en 7, que significa "mostrar toda la información de seguimiento".

2. Use la función [rxSetComputeContext](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsetcomputecontext) para especificar el contexto de cálculo habilitado para el seguimiento por nombre.

    ```R
    rxSetComputeContext(sqlComputeTrace)
    ```

## <a name="next-steps"></a>Pasos siguientes

Obtenga información sobre cómo cambiar contextos de cálculo para ejecutar código R en el servidor o localmente.

> [!div class="nextstepaction"]
> [Calcular estadísticas de resumen en contextos de cálculo locales y remotos](../../advanced-analytics/tutorials/deepdive-create-and-run-r-scripts.md)