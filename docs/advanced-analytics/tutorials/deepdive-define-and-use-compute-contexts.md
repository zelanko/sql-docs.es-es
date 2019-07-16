---
title: 'Definir y usar contextos de proceso de RevoScaleR: SQL Server Machine Learning'
description: Tutorial del tutorial sobre cómo definir un contexto de cálculo usando el lenguaje R en SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.openlocfilehash: 3131dfc65d8964232073d37aba697f62de9fcc2a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67962236"
---
# <a name="define-and-use-compute-contexts-sql-server-and-revoscaler-tutorial"></a>Definir y usar contextos de cálculo (tutorial de SQL Server y RevoScaleR)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

En esta lección forma parte de la [RevoScaleR tutorial](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md) sobre cómo usar [funciones de RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) con SQL Server.

En la lección anterior, usó **RevoScaleR** funciones para inspeccionar los objetos de datos. Esta lección se presenta la [RxInSqlServer](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinsqlserver) función, que le permite definir un contexto de cálculo para un servidor SQL remoto. Con un contexto de cálculo remoto, puede desplazar la ejecución de R desde una sesión local a una sesión remota en el servidor. 

> [!div class="checklist"]
> * Obtenga información sobre el que contexto de cálculo de los elementos de un servidor SQL remoto
> * Habilitar el seguimiento de un objeto de contexto de proceso

**RevoScaleR** es compatible con varios contextos de proceso: Hadoop, Spark en HDFS y SQL Server en bases de datos. Para SQL Server, el **RxInSqlServer** función se utiliza para las conexiones de servidor y pasar objetos entre el equipo local y el contexto de ejecución remoto.

## <a name="create-and-set-a-compute-context"></a>Crear y establecer un contexto de proceso

El **RxInSqlServer** función que crea el contexto de cálculo de SQL Server utiliza la siguiente información:

+ Cadena de conexión para el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instancia
+ Especificación de cómo deben controlar los resultados
+ Especificación opcional de un directorio de datos compartido
+ Argumentos opcionales que habilitación el seguimiento o especificar el nivel de seguimiento

En esta sección le guiará a través de cada parte.

1. Especifique la cadena de conexión para la instancia donde se realizan los cálculos. Puede volver a usar la cadena de conexión que creó anteriormente.

    **Con un inicio de sesión de SQL**

    ```R
    sqlConnString <- "Driver=SQL Server;Server=<SQL Server instance name>; Database=<database name>;Uid=<SQL user nme>;Pwd=<password>"
      ```

    **Con la autenticación de Windows**

    ```R
    sqlConnString <- "Driver=SQL Server;Server=instance_name;Database=RevoDeepDive;Trusted_Connection=True"
    ```
    
2. Especifique cómo quiere que se controlen los resultados. El script siguiente dirige la sesión local de R para esperar los resultados del trabajo de R en el servidor antes de procesar la operación siguiente. También suprime la salida de cálculos remotos que aparezca en la sesión local.
  
    ```R
    sqlWait <- TRUE
    sqlConsoleOutput <- FALSE
    ```
  
    El argumento *wait* para **RxInSqlServer** es compatible con estas opciones:
  
    -   **TRUE**. El trabajo está configurado como el bloqueo y no vuelve hasta que se haya completado o ha producido un error.  Para obtener más información, consulte [distribuida e informática en paralelo en Machine Learning Server](https://docs.microsoft.com/machine-learning-server/r/how-to-revoscaler-distributed-computing).
  
    -   **FALSE**. Los trabajos están configurados como sin bloqueo y devuelven inmediatamente, lo que le permite continuar la ejecución de otro código de R. En cambio, incluso en modo de no bloqueo, la conexión de cliente con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] debe mantenerse mientras se ejecuta el trabajo.

3. Si lo desea, especifique la ubicación de un directorio local para el uso compartido mediante la sesión de R local y remoto [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] equipo y sus cuentas.

    ```R
    sqlShareDir <- paste("c:\\AllShare\\", Sys.getenv("USERNAME"), sep="")
    ```
    
   Si desea crear manualmente un directorio específico para el uso compartido, puede agregar una línea similar al siguiente:

    ```R
    dir.create(sqlShareDir, recursive = TRUE)
    ```

4. Pasar argumentos a la **RxInSqlServer** constructor para crear el *objeto de contexto de proceso*.

    ```R
    sqlCompute <- RxInSqlServer(  
         connectionString = sqlConnString,
         wait = sqlWait,
         consoleOutput = sqlConsoleOutput)
    ```
    
    La sintaxis de **RxInSqlServer** es casi idéntico al de la **RxSqlServerData** función que usó anteriormente para definir el origen de datos. En cambio, hay algunas diferencias importantes.
      
    - El objeto del origen de datos, definido mediante la función [RxSqlServerData](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqlserverdata), especifica dónde se almacenan los datos.
    
    - En cambio, el contexto de cálculo definido mediante la función [RxInSqlServer](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinsqlserver) indica dónde se tienen lugar las agregaciones y otros cálculos.
    
    Definir un contexto de cálculo no afecta a los demás cálculos genéricos de R que puede realizar en la estación de trabajo, y no cambia el origen de los datos. Por ejemplo, puede definir un archivo de texto local como el origen de datos pero cambiar el contexto de cálculo a SQL Server y realizar toda la lectura y los resúmenes en los datos del equipo de SQL Server.

5. Activar el contexto de cálculo remoto.

    ```R
    rxSetComputeContext(sqlCompute)
    ```

6. Devolver información sobre el contexto de proceso, incluidas sus propiedades.

    ```R
    rxGetComputeContext()
    ```

7. Restablecer el contexto de cálculo en el equipo local especificando la palabra clave "local" (la lección siguiente se muestra cómo utilizar el contexto de cálculo remoto).

    ```R
    rxSetComputeContext("local")
    ```

> [!Tip]
> Para obtener una lista de otras palabras clave admitidas por esta función, escriba `help("rxSetComputeContext")` desde una línea de comandos de R.

## <a name="enable-tracing"></a>Habilitar el seguimiento

A veces, las operaciones funcionan en su contexto local pero experimentan problemas al ejecutarse en un contexto de cálculo remoto. Si desea analizar los problemas o supervisar el rendimiento, puede habilitar el seguimiento en el contexto de cálculo para admitir la solución de problemas de tiempo de ejecución.

1. Cree un nuevo contexto de cálculo que usa la misma cadena de conexión, pero agregue los argumentos *traceEnabled* y *traceLevel* a la **RxInSqlServer** constructor.

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

2. Use la [rxSetComputeContext](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsetcomputecontext) función para especificar el contexto de cálculo de seguimiento habilitado por su nombre.

    ```R
    rxSetComputeContext(sqlComputeTrace)
    ```

## <a name="next-steps"></a>Pasos siguientes

Obtenga información sobre cómo cambiar contextos de proceso para ejecutar código R en el servidor o localmente.

> [!div class="nextstepaction"]
> [Contextos de cálculo de estadísticas de resumen de proceso en local y remota](../../advanced-analytics/tutorials/deepdive-create-and-run-r-scripts.md)