---
title: "Definir y usar contextos de c&#225;lculo (An&#225;lisis detallado de ciencia de datos) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to: 
  - "SQL Server 2016"
dev_langs: 
  - "R"
ms.assetid: b13058d0-9c6a-44e1-849b-72189d9050ba
caps.latest.revision: 17
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
---
# Definir y usar contextos de c&#225;lculo (An&#225;lisis detallado de ciencia de datos)
Ha decidido que quiere realizar algunos de los cálculos más complejos en el servidor, en lugar de en el equipo local. Para ello, debe crear un contexto de cálculo que le permita ejecutar código R en el servidor.  
  
La función [RxInSqlServer](https://msdn.microsoft.com/microsoft-r/scaler/rxinsqlserver) es una de las funciones mejoradas de R proporcionadas en el paquete [RevoScaleR](https://msdn.microsoft.com/microsoft-r/scaler/scaler). La función controla que se cree la conexión de la base de datos y se pasen objetos entre el equipo local y el contexto de ejecución remota.  
  
En este paso, aprenderá a usar la función *RxInSqlServer* para definir un contexto de cálculo en su código de R.  


  
## Crear y establecer un contexto de cálculo  
Para crear un contexto de cálculo se requiere la siguiente información básica sobre la instancia [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
-   La cadena de conexión para la instancia  
-   Una especificación sobre cómo se deben controlar los resultados  
-   Argumentos opcionales para habilitar el seguimiento o para especificar un directorio compartido


 Comencemos.

1.  Especifique la cadena de conexión para la instancia en la que llevará a cabo los cálculos.  Esta es solo una de varias variables que pasará a la función *RxInSqlServer* para crear el contexto de cálculo. 

    **Con un inicio de sesión de SQL**

      ```R
      sqlConnString <- "Driver=SQL Server;Server=<SQL Server instance name>; Database=<database name>;Uid=<SQL user name>;Pwd=<password>" 
      ```

    **Con la autenticación de Windows integrada**

      ```R
      sqlConnString <- "Driver=SQL Server;Server=instance_name;Database=DeepDive;Trusted_Connection=True"" 
      ```
2.  Especifique cómo quiere que se controlen los resultados. En el siguiente código, indica que la sesión de R en la estación de trabajo debe esperar siempre los resultados del trabajo de R, pero no devolver resultados de la consola de cálculos remotos.  
  
    ```R  
    sqlWait <- TRUE   
    sqlConsoleOutput <- FALSE   
    ```  
  
    El argumento *wait* para *RxInSqlServer* es compatible con estas opciones:  
  
    -   **TRUE**. El trabajo se bloqueará y no volverá hasta que se haya completado o haya dado error.  Para obtener más información sobre los trabajos de bloqueo y de no bloqueo, consulte 
  
    -   **FALSE**. Los trabajos no se bloquearán y volverán de forma inmediata, lo que le permite continuar la ejecución de otro código de R. En cambio, incluso en modo de no bloqueo, la conexión de cliente con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] debe mantenerse mientras se ejecuta el trabajo.  

3. De manera opcional, puede especificar la ubicación de un directorio local para el uso compartido mediante la sesión de R local y mediante el equipo remoto de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y sus cuentas.
    
    ```R  
    sqlShareDir <- paste("c:\\AllShare\\", Sys.getenv("USERNAME"), sep="")   
    
    ## Add this line to create directory if it does not exist
    dir.create(sqlShareDir, recursive = TRUE) 
    ```  
    Recomendamos que use la ubicación predeterminada en lugar de especificar manualmente una carpeta para este argumento. Para obtener más información, consulte [Funciones RevoScaleR](https://msdn.microsoft.com/microsoft-r/scaler/rxinsqlserver).
    
    Si solo quiere saber qué carpeta se está usando, puede ejecutar `rxGetComputeContext` para ver detalles sobre el contexto de cálculo actual. 
  

4.  Tenga preparadas las variables y proporciónelas como argumentos al constructor `RxInSqlServer` para definir el objeto de contexto de cálculo.  
  
    ```R  
    sqlCompute <- RxInSqlServer(  
         connectionString = sqlConnString,        
         #shareDir = sqlShareDir,       
         wait = sqlWait,   
         consoleOutput = sqlConsoleOutput)  
    ```  
  
    Puede observar que la sintaxis de *RxInSqlServer* es casi idéntica a la de la función *RxSqlServerData* que usó anteriormente para definir el origen de datos. En cambio, hay algunas diferencias importantes.  
  
    -   El objeto del origen de datos, definido mediante la función *RxSqlServerData*, especifica dónde se almacenan los datos.  
  
    -   En cambio, el contexto de cálculo (definido mediante la función *RxInSqlServer*) indica dónde se realizarán las agregaciones y otros cálculos.  
  
    Definir un contexto de cálculo no afecta a los demás cálculos genéricos de R que puede realizar en la estación de trabajo, y no cambia el origen de los datos. Por ejemplo, puede definir un archivo de texto local como el origen de datos pero cambiar el contexto de cálculo a SQL Server y realizar toda la lectura y los resúmenes en los datos del equipo de SQL Server. 
  
## Habilitar el seguimiento en el contexto de cálculo  
A veces, las operaciones que funcionan en su contexto local experimentan problemas al ejecutarse en un contexto de cálculo remoto determinado. Si quiere analizar los problemas o supervisar el rendimiento, puede habilitar el seguimiento en el contexto de cálculo para admitir la solución de problemas en tiempo de ejecución.  
  
1. Cree un nuevo contexto de cálculo que use la misma cadena de conexión, pero agregue los argumentos *traceEnabled* y *traceLevel* en el constructor *RxInSqlServer*.  
  
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

2. Para cambiar este contexto de cálculo en algún momento, use la función *rxSetComputeContext* y especifique el contexto por su nombre.

    ```R  
    rxSetComputeContext( sqlComputeTrace)
    ```

    Para este tutorial, usaremos el contexto de cálculo que no tiene el seguimiento habilitado. El rendimiento de la opción con el seguimiento habilitado no se ha probado en todas las operaciones, y su experiencia puede variar dependiendo de la conectividad de red.  
  
Ahora que ha creado un contexto de cálculo remoto, obtendrá información sobre cómo cambiar los contextos de cálculo para ejecutar el código de R en el servidor o localmente.  
  
## Paso siguiente  
[Lesson 2: Create and Run R Scripts &#40;Data Science Deep Dive&#41; (Lección 2: Crear y ejecutar scripts de R &#40;Análisis detallado de ciencia de datos&#41;)](../../advanced-analytics/r-services/lesson-2-create-and-run-r-scripts-data-science-deep-dive.md)  
  
## Paso anterior  
[Consultar y modificar los datos de SQL Server&#40;Análisis detallado de ciencia de datos&#41;](../../advanced-analytics/r-services/query-and-modify-the-sql-server-data-data-science-deep-dive.md)  
  
## Vea también  
[Análisis detallado de ciencia de datos: Usar los paquetes de RevoScaleR](../../advanced-analytics/r-services/data-science-deep-dive-using-the-revoscaler-packages.md)  
  
  
  
