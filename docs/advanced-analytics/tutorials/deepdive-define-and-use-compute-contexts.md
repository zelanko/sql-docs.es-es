---
title: "Definir y usar contextos de cálculo (Análisis detallado de ciencia de datos) | Microsoft Docs"
ms.custom: 
ms.date: 05/22/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to: SQL Server 2016
dev_langs: R
ms.assetid: b13058d0-9c6a-44e1-849b-72189d9050ba
caps.latest.revision: "17"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 9de0e06c73a91637735f7dc6855a3c14db1c7f10
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2017
---
# <a name="define-and-use-compute-contexts"></a>Definir y usar contextos de cálculo


Supongamos que quiere realizar algunos de los cálculos más complejos en el servidor, en lugar de en el equipo local. Para ello, puede crear un contexto de cálculo, que permite que el código de R se ejecute en el servidor.

La función **RxInSqlServer** es una de las funciones mejoradas de R proporcionadas en el paquete [RevoScaleR](https://msdn.microsoft.com/microsoft-r/scaler/scaler) . La función controla que se cree la conexión de la base de datos y se pasen objetos entre el equipo local y el contexto de ejecución remota.

En este paso, aprenderá a usar la función **RxInSqlServer** para definir un contexto de cálculo en su código de R.

Para crear un contexto de cálculo se requiere la siguiente información básica sobre la instancia [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] :

- La cadena de conexión para la instancia
- Una especificación sobre cómo se deben controlar los resultados
- Argumentos opcionales para habilitar el seguimiento o para especificar un directorio compartido

## <a name="create-and-set-a-compute-context"></a>Crear y establecer un contexto de cálculo

1. Especifique la cadena de conexión para la instancia en la que llevará a cabo los cálculos.  Esta es solo una de varias variables que pasará a la función *RxInSqlServer* para crear el contexto de cálculo. Puede volver a usar la cadena de conexión que ha creado anteriormente, o bien crear una diferente si quiere mover los cálculos a otro servidor o utilizar una identidad distinta.

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
  
    El argumento *wait* para *RxInSqlServer* es compatible con estas opciones:
  
    -   **TRUE**. El trabajo se bloqueará y no volverá hasta que se haya completado o haya dado error.  Para obtener más información, consulte [distribuida y la informática en paralelo en Microsoft R](https://msdn.microsoft.com/microsoft-r/scaler-distributed-computing).
  
    -   **FALSE**. Los trabajos no se bloquearán y volverán de forma inmediata, lo que le permite continuar la ejecución de otro código de R. En cambio, incluso en modo de no bloqueo, la conexión de cliente con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] debe mantenerse mientras se ejecuta el trabajo.

3. De manera opcional, puede especificar la ubicación de un directorio local para el uso compartido mediante la sesión de R local y mediante el equipo remoto de  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y sus cuentas.

    ```R
    sqlShareDir <- paste("c:\\AllShare\\", Sys.getenv("USERNAME"), sep="")
    ```
    
4. Si desea crear manualmente un directorio específico para el uso compartido, puede agregar una línea similar al siguiente. Para determinar qué carpeta se está usando actualmente para el uso compartido, ejecute `rxGetComputeContext`, que devuelve detalles acerca de este contexto de proceso. Para obtener más información, consulte [Funciones RevoScaleR](https://msdn.microsoft.com/microsoft-r/scaler/packagehelp/rxinsqlserver).

    ```
    dir.create(sqlShareDir, recursive = TRUE)
    ```

4. Tener preparada todas las variables, proporcionarlos como argumentos al constructor RxInSqlServer para crear el *objeto de contexto de proceso*.

    ```R
    sqlCompute <- RxInSqlServer(  
         connectionString = sqlConnString,
         wait = sqlWait,
         consoleOutput = sqlConsoleOutput)
    ```
    
    Se puede observar que la sintaxis para RxInSqlServer * es casi idéntica de la función RxSqlServerData que ha usado anteriormente para definir el origen de datos. En cambio, hay algunas diferencias importantes.
      
    - El objeto de origen de datos definido mediante la función RxSqlServerData, especifica dónde se almacenan los datos.
    
    - En cambio, el contexto de proceso (definido mediante la función RxInSqlServer) indica donde se realicen las agregaciones y otros cálculos.
    
    Definir un contexto de cálculo no afecta a los demás cálculos genéricos de R que puede realizar en la estación de trabajo, y no cambia el origen de los datos. Por ejemplo, puede definir un archivo de texto local como el origen de datos pero cambiar el contexto de cálculo a SQL Server y realizar toda la lectura y los resúmenes en los datos del equipo de SQL Server.

## <a name="enable-tracing-on-the-compute-context"></a>Habilitar el seguimiento en el contexto de cálculo

A veces, las operaciones funcionan en su contexto local pero experimentan problemas al ejecutarse en un contexto de cálculo remoto. Si quiere analizar los problemas o supervisar el rendimiento, puede habilitar el seguimiento en el contexto de cálculo para admitir la solución de problemas en tiempo de ejecución.

1. Crear un nuevo contexto de proceso que usa la misma cadena de conexión, pero agregue los argumentos *traceEnabled* y *traceLevel* a la *RxInSqlServer* constructor.

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

2. Para cambiar el contexto de proceso, use la función rxSetComputeContext y especifique el contexto por su nombre.

    ```R
    rxSetComputeContext( sqlComputeTrace)
    ```

    > [!NOTE]
    > 
    > Para este tutorial, usaremos el contexto de cálculo que no tiene el seguimiento habilitado. Eso es porque no se ha probado el rendimiento para la opción de seguimiento habilitado para todas las operaciones.
    > 
    > Sin embargo, si decide usar el seguimiento, tenga en cuenta que puede verse afectada su experiencia de conectividad de red.

Ahora que ha creado un contexto de cálculo remoto, obtendrá información sobre cómo cambiar los contextos de cálculo para ejecutar el código de R en el servidor o localmente.

## <a name="next-step"></a>Paso siguiente

[Crear y ejecutar Scripts de R](../../advanced-analytics/tutorials/deepdive-create-and-run-r-scripts.md)


## <a name="previous-step"></a>Paso anterior

[Consultar y modificar los datos de SQL Server](../../advanced-analytics/tutorials/deepdive-query-and-modify-the-sql-server-data.md)


