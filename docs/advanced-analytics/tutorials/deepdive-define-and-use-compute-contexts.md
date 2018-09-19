---
title: Definir y usar contextos de cálculo (análisis detallado R y SQL) | Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 6a76e07cb2ecd03a59112f6c39e3fa2f7895e0a2
ms.sourcegitcommit: aa9d2826e3c451f4699c0e69c9fcc8a2781c6213
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/17/2018
ms.locfileid: "45975644"
---
# <a name="define-and-use-compute-contexts-sql-and-r-deep-dive"></a>Definir y usar contextos de cálculo (análisis detallado SQL y R)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Este artículo forma parte del tutorial de análisis detallado de ciencia de datos, acerca de cómo usar [RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) con SQL Server.

Esta lección se presenta la [RxInSqlServer](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinsqlserver) función, que le permite definir un contexto de proceso para SQL Server y, a continuación, ejecutar cálculos complejos en el servidor, en lugar de en el equipo local. 

RevoScaleR admite varios contextos de cálculo, por lo que puede ejecutar código R en Hadoop, Spark o en bases de datos. Para SQL Server, debe definir el servidor y la función controla las tareas de crear la base de datos de conexión y se pasen objetos entre el equipo local y el contexto de ejecución remoto.

La función que crea SQL Server compute contexto utiliza la siguiente información:

- Cadena de conexión para el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instancia
- Especificación de cómo deben controlar los resultados
- Argumentos opcionales que habilitación el seguimiento o especificar el nivel de seguimiento
- Especificación opcional de un directorio de datos compartido

## <a name="create-and-set-a-compute-context"></a>Crear y establecer un contexto de proceso

1. Especifique la cadena de conexión para la instancia donde se realizan los cálculos.  Puede volver a usar la cadena de conexión que creó anteriormente. Puede crear una cadena de conexión diferente si desea mover los cálculos en un servidor diferente, o usar otro inicio de sesión para realizar algunas tareas.

    **Con un inicio de sesión de SQL**

      ```R
      sqlConnString <- "Driver=SQL Server;Server=<SQL Server instance name>; Database=<database name>;Uid=<SQL user name>;Pwd=<password>"
      ```

    **Con la autenticación de Windows**

      ```R
      sqlConnString <- "Driver=SQL Server;Server=instance_name;Database=DeepDive;Trusted_Connection=True"
      ```
2. Especifique cómo quiere que se controlen los resultados. En el siguiente código, indica que la sesión de R en la estación de trabajo debe esperar siempre los resultados del trabajo de R, pero no devolver resultados de la consola de cálculos remotos.
  
    ```R
    sqlWait <- TRUE
    sqlConsoleOutput <- FALSE
    ```
  
    El argumento *wait* para **RxInSqlServer** es compatible con estas opciones:
  
    -   **TRUE**. El trabajo está configurado como el bloqueo y no vuelve hasta que se haya completado o ha producido un error.  Para obtener más información, consulte [distribuida e informática en paralelo en Machine Learning Server](https://docs.microsoft.com/machine-learning-server/r/how-to-revoscaler-distributed-computing).
  
    -   **FALSE**. Los trabajos están configurados como sin bloqueo y devuelven inmediatamente, lo que le permite continuar la ejecución de otro código de R. En cambio, incluso en modo de no bloqueo, la conexión de cliente con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] debe mantenerse mientras se ejecuta el trabajo.

3. Si lo desea, puede especificar la ubicación de un directorio local para el uso compartido mediante la sesión de R local y remoto [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] equipo y sus cuentas.

    ```R
    sqlShareDir <- paste("c:\\AllShare\\", Sys.getenv("USERNAME"), sep="")
    ```
    
4. Si desea crear manualmente un directorio específico para el uso compartido, puede agregar una línea similar al siguiente:

    ```
    dir.create(sqlShareDir, recursive = TRUE)
    ```

    Para determinar qué carpeta se está usando actualmente para el uso compartido, ejecute `rxGetComputeContext()`, que devuelve el contexto de cálculo de los detalles sobre la actual. Para obtener más información, consulte [Funciones RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/).

4. Tenga preparadas las variables y proporciónelas como argumentos para el **RxInSqlServer** constructor para crear el *objeto de contexto de proceso*.

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

## <a name="enable-tracing-on-the-compute-context"></a>Habilitar el seguimiento en el contexto de cálculo

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

2. Para cambiar este contexto de cálculo, use la función [rxSetComputeContext](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsetcomputecontext) y especifique el contexto por su nombre.

    ```R
    rxSetComputeContext( sqlComputeTrace)
    ```

    > [!NOTE]
    > 
    > Para este tutorial, use el contexto de cálculo que no tiene habilitada la traza. 
    > 
    > Sin embargo, si decide utilizar el seguimiento, tenga en cuenta que su experiencia puede verse afectada por la conectividad de red. También tenga en cuenta que dado que no se ha probado el rendimiento de la opción de seguimiento habilitado para todas las operaciones.

En el paso siguiente que aprenderá a usar contextos de proceso de, para ejecutar código R en el servidor o localmente.

## <a name="next-step"></a>Paso siguiente

[Crear y ejecutar scripts de R](../../advanced-analytics/tutorials/deepdive-create-and-run-r-scripts.md)

## <a name="previous-step"></a>Paso anterior

[Consultar y modificar los datos de SQL Server](../../advanced-analytics/tutorials/deepdive-query-and-modify-the-sql-server-data.md)
