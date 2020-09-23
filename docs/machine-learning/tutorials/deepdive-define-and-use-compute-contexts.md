---
title: Uso de contextos de cálculo RevoScaleR
description: Introducción a la función RxInSqlServer, que permite definir un contexto de cálculo para un SQL Server remoto.
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 62b18fbdd0a4c59b8458b2bc1f757ef189db5de3
ms.sourcegitcommit: 9b41725d6db9957dd7928a3620fe4db41eb51c6e
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/13/2020
ms.locfileid: "88178782"
---
# <a name="define-and-use-compute-contexts-sql-server-and-revoscaler-tutorial"></a>Definición y uso de contextos de cálculo (tutorial de SQL Server y RevoScaleR)
[!INCLUDE [SQL Server 2016 and later](../../includes/applies-to-version/sqlserver2016.md)]

Este es el tutorial 4 de la [serie de tutoriales de RevoScaleR](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md) sobre el uso de las [funciones de RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) con SQL Server.

En el tutorial anterior, ha usado las funciones **RevoScaleR** para inspeccionar los objetos de datos. En este tutorial se presenta la función [RxInSqlServer](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinsqlserver), que permite definir un contexto de cálculo para un servidor SQL Server remoto. Con un contexto de cálculo remoto, puede desplazar la ejecución de R de una sesión local a una sesión remota en el servidor. 

> [!div class="checklist"]
> * Obtener información sobre los elementos de un contexto de cálculo de SQL Server remoto.
> * Habilitar el seguimiento en un objeto de contexto de cálculo.

**RevoScaleR** admite varios contextos de cálculo: Hadoop, Spark en HDFS y SQL Server en la base de datos. Para SQL Server, la función **RxInSqlServer** se utiliza para las conexiones del servidor y para pasar objetos entre el equipo local y el contexto de ejecución remoto.

## <a name="create-and-set-a-compute-context"></a>Creación y establecimiento de un contexto de cálculo

La función **RxInSqlServer** que crea el contexto de cálculo SQL Server usa la siguiente información:

+ La cadena de conexión para la instancia [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]
+ Especificación de cómo se deben controlar los resultados
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
    
2. Especifique cómo quiere que se controlen los resultados. El siguiente script dirige la sesión local de R para esperar los resultados del trabajo de R en el servidor antes de procesar la siguiente operación. También suprime el resultado de los cálculos remotos para que no aparezcan en la sesión local.
  
    ```R
    sqlWait <- TRUE
    sqlConsoleOutput <- FALSE
    ```
  
    El argumento *wait* para **RxInSqlServer** es compatible con estas opciones:
  
    -   **TRUE**. El trabajo está configurado como bloqueado y no vuelve hasta que se haya completado o haya dado error.  Para obtener más información, vea [Informática en paralelo y distribuida Machine Learning Server](https://docs.microsoft.com/machine-learning-server/r/how-to-revoscaler-distributed-computing).
  
    -   **FALSE**. Los trabajos no se configuran como bloqueados y vuelven de forma inmediata, lo que le permite continuar la ejecución de otro código de R. En cambio, incluso en modo de no bloqueo, la conexión de cliente con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] debe mantenerse mientras se ejecuta el trabajo.

3. De manera opcional, especifique la ubicación de un directorio local para el uso compartido mediante la sesión de R local y mediante el equipo remoto de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y sus cuentas.

    ```R
    sqlShareDir <- paste("c:\\AllShare\\", Sys.getenv("USERNAME"), sep="")
    ```
    
   Si quiere crear de manera manual un directorio específico para compartir, puede agregar una línea como la siguiente:

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
    
    - En cambio, el contexto de cálculo, definido mediante la función [RxInSqlServer](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinsqlserver), indica dónde se realizarán las agregaciones y otros cálculos.
    
    Definir un contexto de cálculo no afecta a los demás cálculos genéricos de R que puede realizar en la estación de trabajo, y no cambia el origen de los datos. Por ejemplo, puede definir un archivo de texto local como el origen de datos pero cambiar el contexto de cálculo a SQL Server y realizar toda la lectura y los resúmenes en los datos del equipo de SQL Server.

5. Active el contexto de cálculo remoto.

    ```R
    rxSetComputeContext(sqlCompute)
    ```

6. Devuelva información sobre el contexto de cálculo, incluidas sus propiedades.

    ```R
    rxGetComputeContext()
    ```

7. Vuelva a restablecer el contexto de cálculo en el equipo local especificando la palabra clave "local" (en el siguiente tutorial se muestra cómo usar el contexto de cálculo remoto).

    ```R
    rxSetComputeContext("local")
    ```

> [!Tip]
> Para obtener una lista de otras palabras clave admitidas por esta función, escriba `help("rxSetComputeContext")` desde una línea de comandos de R.

## <a name="enable-tracing"></a>Habilitación del seguimiento

A veces, las operaciones funcionan en su contexto local pero experimentan problemas al ejecutarse en un contexto de cálculo remoto. Si quiere analizar los problemas o supervisar el rendimiento, puede habilitar el seguimiento en el contexto de cálculo para admitir la solución de problemas en tiempo de ejecución.

1. Cree un nuevo contexto de cálculo que use la misma cadena de conexión, pero agregue los argumentos *traceEnabled* y *traceLevel* en el constructor **RxInSqlServer**.

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

Obtenga información sobre cómo activar contextos de cálculo para ejecutar el código de R en el servidor o de forma local.

> [!div class="nextstepaction"]
> [Cálculo de estadísticas de resumen en contextos de cálculo locales y remotos](../../machine-learning/tutorials/deepdive-create-and-run-r-scripts.md)