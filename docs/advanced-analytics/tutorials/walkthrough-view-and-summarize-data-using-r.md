---
title: Ver y resumir datos mediante R (tutorial) | Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/02/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 1d6c225b3ec6b2a7a80dea155b564b94ecab60fb
ms.sourcegitcommit: af1d9fc4a50baf3df60488b4c630ce68f7e75ed1
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/06/2018
ms.locfileid: "51032892"
---
# <a name="view-and-summarize-data-using-r"></a>Ver y resumir datos mediante R
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Ahora vamos a trabajar con los mismos datos mediante código de R. En esta lección, obtendrá información sobre cómo usar las funciones de la **RevoScaleR** paquete.

Con este tutorial se proporciona un script de R que incluye todo el código necesario para crear el objeto de datos, generar resúmenes y generar modelos. Puede encontrar el archivo de script de R **RSQL_RWalkthrough.R**en la ubicación donde instaló los archivos de script.

+ Si tiene experiencia con R, puede ejecutar todo el script de una vez.
+ Para quienes aprenden a usar RevoScaleR, este tutorial recorre la secuencia de comandos línea por línea.
+ Para ejecutar líneas individuales del script, puede resaltar una o varias líneas en el archivo y presionar Ctrl + ENTRAR.

> [!TIP]
> Guarde el área de trabajo de R en caso de que quiera completar el resto del tutorial más adelante.  De este modo los objetos de datos y otras variables están listos para su reutilización.

## <a name="define-a-sql-server-compute-context"></a>Definir un contexto de cálculo de SQL Server

Microsoft R facilita la obtención de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a usar en el código de R. El proceso es el siguiente:
  
- Crear una conexión a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]
- Definir una consulta con los datos que necesita o especificar una tabla o vista
- Definir uno o más contextos de cálculo para usarlos al ejecutar código de R
- Opcionalmente, puede definir las transformaciones que se aplican al origen de datos mientras se leen desde el origen

Los pasos siguientes forman parte del código R y deben ejecutarse en un entorno de R. Microsoft R Client, se usa porque incluye todos los paquetes de RevoScaleR, así como un conjunto de herramientas de R básico y ligero.

1. Si el **RevoScaleR** paquete no está ya cargado, ejecutamos esta línea de código de R:

    ```R
    library("RevoScaleR")
    ```

     En este caso, las comillas son opcionales, aunque se recomienda.
     
     Si se produce un error, asegúrese de que el entorno de desarrollo de R usa una biblioteca que contiene el paquete RevoScaleR. Use un comando como `.libPaths()` para ver la ruta de acceso de la biblioteca actual.

2. Crea la cadena de conexión para SQL Server y lo guarda en una variable de R, _connStr_.
    
    ```R
    connStr <- "Driver=SQL Server;Server=your_server_name;Database=nyctaxi_sample;Uid=your-sql-login;Pwd=your-login-password"
    ```

    Para el nombre del servidor, es posible que pueda usar solo el nombre de instancia o, es posible que deba calificar totalmente el nombre, dependiendo de la red.

    Para la autenticación de Windows, la sintaxis es un poco diferente:
    
    ```R
    connStr <- "Driver=SQL Server;Server=your_server_name;Database=nyctaxi_sample;Trusted_Connection=True"
    ```

    El script de R disponible para la descarga solo usa inicios de sesión de SQL. Por lo general, se recomienda que use la autenticación de Windows cuando sea posible, evite guardar contraseñas en el código de R. Sin embargo, para asegurarse de que el código de este tutorial coincide con el código descargado desde Github, vamos a usar un inicio de sesión SQL para el resto del tutorial.

3. Defina las variables que se usará al crear un nuevo *contexto de proceso*. Después de crear el objeto de contexto de proceso, puede utilizarlo para ejecutar código R en la instancia de SQL Server.

    ```R
    sqlShareDir <- paste("C:\\AllShare\\",Sys.getenv("USERNAME"),sep="")
    sqlWait <- TRUE
    sqlConsoleOutput <- FALSE
    ```

    - R usa un directorio temporal cuando serializa los objetos de R entre la estación de trabajo y el equipo con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Puede especificar el directorio local que se usa como *sqlShareDir*o aceptar el valor predeterminado.
  
    - Use *sqlWait* para indicar si desea que R espere los resultados desde el servidor.  Para obtener una explicación de espera frente a los trabajos no en espera, consulte [distribuida e informática en paralelo con ScaleR de Microsoft R](https://docs.microsoft.com/r-server/r/how-to-revoscaler-distributed-computing).
  
    - Use el argumento *sqlConsoleOutput* para indicar que no desea ver el resultado de la consola de R.


4. Se llama a la [RxInSqlServer](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxinsqlserver) constructor para crear el objeto de contexto de proceso con las variables y las cadenas de conexión ya definidas y guardar el nuevo objeto en la variable de R *sqlcc*.
  
    ```R
    sqlcc <- RxInSqlServer(connectionString = connStr, shareDir = sqlShareDir, wait = sqlWait, consoleOutput = sqlConsoleOutput)
    ```

5. De forma predeterminada, el contexto de cálculo es local, por lo que deberá establecer explícitamente el *active* contexto de proceso.

    ```R
    rxSetComputeContext(sqlcc)
    ```

    + `rxSetComputeContext` devuelve el contexto de cálculo activo anteriormente invisible para que pueda usarlo
    + `rxGetComputeContext` devuelve el contexto de cálculo activo
    
    Observe que establecer un contexto de cálculo solo afecta las operaciones que usan funciones en el paquete **RevoScaleR** ; el contexto de cálculo no afecta la manera en que se realizan las operaciones de R de código abierto.

## <a name="create-a-data-source-using-rxsqlserver"></a>Crear un origen de datos con RxSqlServer

En Microsoft R, un *origen de datos* es un objeto que se crea mediante las funciones de RevoScaleR. El objeto de origen de datos especifica un conjunto de datos que desea usar para una tarea, como la extracción del modelo entrenamiento o característica. Puede obtener datos desde una variedad de orígenes; Para obtener la lista de orígenes admitidos actualmente, consulte [RxDataSource](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdatasource).

Anteriormente se define una cadena de conexión y había guardado esa información en una variable de R. Puede volver a usar esa información de conexión para especificar los datos que desea obtener.

1. Guardar una consulta SQL como una variable de cadena. La consulta define los datos para entrenar el modelo.

    ```R
    sampleDataQuery <- "SELECT TOP 1000 tipped, fare_amount, passenger_count,trip_time_in_secs,trip_distance, pickup_datetime, dropoff_datetime, pickup_longitude, pickup_latitude, dropoff_longitude, dropoff_latitude FROM nyctaxi_sample"
    ```

    Hemos usado aquí una cláusula TOP para acelerar la ejecución de las cosas, pero las filas reales devueltas por la consulta pueden variar según el orden. Por lo tanto, el resumen de resultados también puede variar de los que aparecen a continuación. No dude en quitar la cláusula TOP.

2. Pase la definición de consulta como argumento a la función [RxSqlServerData](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxsqlserverdata).

    ```R
    inDataSource <- RxSqlServerData(
      sqlQuery = sampleDataQuery,
      connectionString = connStr,
      colClasses = c(pickup_longitude = "numeric", pickup_latitude = "numeric",
      dropoff_longitude = "numeric", dropoff_latitude = "numeric"),
      rowsPerRead=500
      )
    ```
    
    + El argumento  *colClasses* especifica los tipos de columna que se usarán al mover los datos entre [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y R. Esto es importante porque [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa tipos de datos distintos a los de R y más tipos de datos. Para obtener más información, consulte [bibliotecas de R y tipos de datos](../r/r-libraries-and-data-types.md).
  
    + El argumento *rowsPerRead* es importante para administrar el uso de memoria y cálculos eficaces.  La mayoría de las funciones analíticas mejoradas de[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] procesan los datos en fragmentos y acumulan los resultados intermedios, devolviendo los cálculos finales después de que se han leído todos los datos.  Agregando el *rowsPerRead* parámetro, puede controlar cuántas filas de datos se leen en cada fragmento para su procesamiento.  Si el valor de este parámetro es demasiado grande, es posible que el acceso a los datos sea lento porque no tiene suficiente memoria para procesar de forma eficaz un fragmento de datos tan grande.  En algunos sistemas, establecer *rowsPerRead* en un valor demasiado pequeño también puede proporcionar un rendimiento más lento.

3. En este momento, ha creado el *inDataSource* objeto, pero no contiene ningún dato. Los datos no se extraen de la consulta SQL en el entorno local hasta que se ejecuta como una función [rxImport](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdatastep) o [rxSummary](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxsummary).

    Sin embargo, ahora que ha definido los objetos de datos, puede usar como argumento a otras funciones.

## <a name="use-the-sql-server-data-in-r-summaries"></a>Usar los datos de SQL Server en los resúmenes de R

En esta sección, probará algunas de las funciones proporcionadas en [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] contextos de cálculo que compatibilidad con el extremo remoto. Aplicando funciones de R al origen de datos, puede explorar, resumir y gráfico el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] datos.

1. Llame a la función [rxGetVarInfo](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxgetvarinfo) para obtener una lista de las variables en el origen de datos y sus tipos de datos.

    **rxGetVarInfo** es una práctica función; se puede llamar en cualquier trama de datos o en un conjunto de datos en un objeto de datos remoto, para obtener información como el valor máximo y mínimo valores, el tipo de datos y el número de niveles en las columnas de factor.
    
    Considere la posibilidad de ejecutar esta función después de cualquier tipo de entrada de datos, transformación de características o ingeniería de características. Al hacerlo, puede asegurarse de que todas las características que desee utilizar en el modelo son los datos esperados, escriba y evitar errores.
  
    ```R
    rxGetVarInfo(data = inDataSource)
    ```

    **Resultado**
    
    ```
    Var 1: tipped, Type: integer
    Var 2: fare_amount, Type: numeric
    Var 3: passenger_count, Type: integer
    Var 4: trip_time_in_secs, Type: numeric, Storage: int64
    Var 5: trip_distance, Type: numeric
    Var 6: pickup_datetime, Type: character
    Var 7: dropoff_datetime, Type: character
    Var 8: pickup_longitude, Type: numeric
    Var 9: pickup_latitude, Type: numeric
    Var 10: dropoff_longitude, Type: numeric
    ```

2. Ahora, llame a la función RevoScaleR [rxSummary](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxsummary) para obtener estadísticas más detalladas sobre las variables individuales.

    rxSummary se basa en el objeto de R `summary` funcionando, pero tiene algunas ventajas y características adicionales. rxSummary funciona en varios contextos de proceso y admite la fragmentación.  También puede usar rxSummary para transformar los valores o resumir basándose en los niveles de factor.
    
    En este ejemplo, resume el importe en función del número de pasajeros.
    
    ```R
    start.time <- proc.time()
    rxSummary(~fare_amount:F(passenger_count,1,6), data = inDataSource)
    used.time <- proc.time() - start.time
    print(paste("It takes CPU Time=", round(used.time[1]+used.time[2],2)," seconds,
      Elapsed Time=", round(used.time[3],2),
      " seconds to summarize the inDataSource.", sep=""))
    ```
    + El primer argumento rxSummary especifica la fórmula o el término por el que resumir. En este caso, el `F()` función se utiliza para convertir los valores de _pasajeros\_recuento_ en factores antes del resumen. También debe especificar el valor mínimo (1) y el valor máximo (6) para el _pasajeros\_recuento_ variable de factor.
    + Si no especifica las estadísticas de salida, de forma predeterminada rxSummary genera Media, StDev, Min, Max y el número de observaciones válidas y que faltan.
    + Este ejemplo también incluye algo de código para realizar un seguimiento de la hora a la que empieza y finaliza la función, para que pueda comparar el rendimiento.
  
    **Resultado**

    Si la función rxSummary se ejecuta correctamente, debería ver resultados como estos, seguido de una lista de las estadísticas por categoría. 

    ```
    rxSummary(formula = ~fare_amount:F(passenger_count, 1,6), data = inDataSource)
    Data: inDataSource (RxSqlServerData Data Source)
    Number of valid observations: 1000
    ```

### <a name="bonus-exercise-on-big-data"></a>Ejercicio adicional sobre big data

Pruebe a definir una nueva cadena de consulta con todas las filas. se recomienda que configurar un nuevo objeto de origen de datos para este experimento. También es posible que intente cambiar el *rowsToRead* parámetro para ver cómo afecta al rendimiento.

```R
bigDataQuery  <- "SELECT tipped, fare_amount, passenger_count,trip_time_in_secs,trip_distance, pickup_datetime, dropoff_datetime, pickup_longitude, pickup_latitude, dropoff_longitude, dropoff_latitude FROM nyctaxi_sample"

bigDataSource <- RxSqlServerData(
      sqlQuery = bigDataQuery,
      connectionString = connStr,
      colClasses = c(pickup_longitude = "numeric", pickup_latitude = "numeric",
      dropoff_longitude = "numeric", dropoff_latitude = "numeric"),
      rowsPerRead=500
      )

start.time <- proc.time()
rxSummary(~fare_amount:F(passenger_count,1,6), data = bigDataSource)
used.time <- proc.time() - start.time
print(paste("It takes CPU Time=", round(used.time[1]+used.time[2],2)," seconds,
  Elapsed Time=", round(used.time[3],2),
  " seconds to summarize the inDataSource.", sep=""))
```

> [!TIP]
> Mientras se está ejecutando, puede usar una herramienta como [Process Explorer](https://technet.microsoft.com/sysinternals/processexplorer.aspx) o SQL Profiler para ver cómo se realiza la conexión y el código de R se ejecute con servicios de SQL Server.
> 
> Otra opción consiste en supervisar trabajos de R que se ejecutan en SQL Server con estos [informes personalizados](../r/monitor-r-services-using-custom-reports-in-management-studio.md).

## <a name="next-lesson"></a>Lección siguiente

[Crear gráficos y trazados con R](walkthrough-create-graphs-and-plots-using-r.md)

## <a name="previous-lesson"></a>Lección anterior

[Explorar los datos con SQL](walkthrough-view-and-explore-the-data.md)
