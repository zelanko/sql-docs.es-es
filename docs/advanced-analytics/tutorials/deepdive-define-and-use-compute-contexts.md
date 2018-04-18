---
title: Definir y utilizar los contextos de proceso (SQL y R profundización) | Documentos de Microsoft
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: cb559b0acfc77ddb7e48cc0b3cacf76d421481ac
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="define-and-use-compute-contexts-sql-and-r-deep-dive"></a>Definir y utilizar los contextos de proceso (SQL y R profundización)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Este artículo forma parte del tutorial exhaustiva de ciencia de datos, acerca de cómo usar [RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) con SQL Server.

Esta lección se presenta la [RxInSqlServer](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinsqlserver) función, que le permite definir un contexto de proceso para SQL Server y, a continuación, ejecutar cálculos complejos en el servidor, en lugar de en el equipo local. 

RevoScaleR admite varios contextos de proceso, por lo que puede ejecutar código R en Hadoop, Spark o en bases de datos. Para SQL Server, debe definir el servidor y la función controla las tareas de creación de objetos de conexión y al pasar entre el equipo local y el contexto de ejecución remota de la base de datos.

La función que crea el servidor SQL Server de proceso contexto utiliza la siguiente información:

- Cadena de conexión para el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instancia
- Especificación de cómo debe controlarse salida
- Argumentos opcionales que habilita el seguimiento o que especifique el nivel de seguimiento
- Especificación opcional de un directorio de datos compartido

## <a name="create-and-set-a-compute-context"></a>Crear y establecer un contexto de proceso

1. Especifique la cadena de conexión para la instancia donde se realizan los cálculos.  Puede reutilizar la cadena de conexión que creó anteriormente. Puede crear una cadena de conexión diferente si desea mover los cálculos en un servidor diferente, o usar otro inicio de sesión para realizar algunas tareas.

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
  
    -   **TRUE**. El trabajo está configurado como bloqueo y no vuelve hasta que se ha completado o ha generado errores.  Para obtener más información, consulte [distribuida y la informática en paralelo en el servidor de aprendizaje de máquina](https://docs.microsoft.com/machine-learning-server/r/how-to-revoscaler-distributed-computing).
  
    -   **FALSE**. Los trabajos están configurados como antibloqueo y devuelvan inmediatamente, lo que le permite continuar ejecutando otro código de R. En cambio, incluso en modo de no bloqueo, la conexión de cliente con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] debe mantenerse mientras se ejecuta el trabajo.

3. Si lo desea, puede especificar la ubicación de un directorio local para el uso compartido por la sesión de R local y remoto [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] equipo y sus cuentas.

    ```R
    sqlShareDir <- paste("c:\\AllShare\\", Sys.getenv("USERNAME"), sep="")
    ```
    
4. Si desea crear manualmente un directorio específico para el uso compartido, puede agregar una línea similar al siguiente:

    ```
    dir.create(sqlShareDir, recursive = TRUE)
    ```

    Para determinar qué carpeta se está usando actualmente para el uso compartido, ejecute `rxGetComputeContext()`, que devuelve detalles acerca de este contexto de proceso. Para obtener más información, consulte [Funciones RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/).

4. Tener preparada todas las variables, proporcionarlos como argumentos para la **RxInSqlServer** constructor para crear el *objeto de contexto de proceso*.

    ```R
    sqlCompute <- RxInSqlServer(  
         connectionString = sqlConnString,
         wait = sqlWait,
         consoleOutput = sqlConsoleOutput)
    ```
    
    La sintaxis de **RxInSqlServer** es casi idéntico de la **RxSqlServerData** función a la que usó previamente para definir el origen de datos. En cambio, hay algunas diferencias importantes.
      
    - El objeto del origen de datos, definido mediante la función [RxSqlServerData](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqlserverdata), especifica dónde se almacenan los datos.
    
    - En cambio, el contexto de proceso, se definen mediante la función [RxInSqlServer](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinsqlserver) indica que son agregaciones y otros cálculos que se realicen.
    
    Definir un contexto de cálculo no afecta a los demás cálculos genéricos de R que puede realizar en la estación de trabajo, y no cambia el origen de los datos. Por ejemplo, puede definir un archivo de texto local como el origen de datos pero cambiar el contexto de cálculo a SQL Server y realizar toda la lectura y los resúmenes en los datos del equipo de SQL Server.

## <a name="enable-tracing-on-the-compute-context"></a>Habilitar el seguimiento en el contexto de proceso.

A veces, las operaciones funcionan en su contexto local pero experimentan problemas al ejecutarse en un contexto de cálculo remoto. Si quiere analizar los problemas o supervisar el rendimiento, puede habilitar el seguimiento en el contexto de cálculo para admitir la solución de problemas en tiempo de ejecución.

1. Crear un nuevo contexto de proceso que usa la misma cadena de conexión, pero agregue los argumentos *traceEnabled* y *traceLevel* a la **RxInSqlServer** constructor.

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
    > Para este tutorial, use el contexto de proceso que no tiene habilitado el seguimiento. 
    > 
    > Sin embargo, si decide usar el seguimiento, tenga en cuenta que puede verse afectada su experiencia de conectividad de red. También tenga en cuenta que dado que no se ha probado el rendimiento para la opción de seguimiento habilitado para todas las operaciones.

En el paso siguiente que aprenderá a usar calcular contextos, para ejecutar código R en el servidor o localmente.

## <a name="next-step"></a>Paso siguiente

[Crear y ejecutar scripts de R](../../advanced-analytics/tutorials/deepdive-create-and-run-r-scripts.md)

## <a name="previous-step"></a>Paso anterior

[Consultar y modificar los datos de SQL Server](../../advanced-analytics/tutorials/deepdive-query-and-modify-the-sql-server-data.md)
