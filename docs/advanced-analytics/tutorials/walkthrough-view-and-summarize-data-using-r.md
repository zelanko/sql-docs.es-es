---
title: 'Ver y resumir datos de SQL Server mediante funciones de R: SQL Server Machine Learning'
description: Tutorial que muestra cómo visualizar y generar resúmenes estadísticos mediante funciones de R para realizar análisis en bases de datos en SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/26/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 368caa21545e534c393aca29ce8fd3a59f9d9837
ms.sourcegitcommit: ee76332b6119ef89549ee9d641d002b9cabf20d2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/20/2018
ms.locfileid: "53644564"
---
# <a name="view-and-summarize-sql-server-data-using-r-walkthrough"></a>Ver y resumir datos de SQL Server con R (tutorial)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

En esta lección le presenta las funciones de la **RevoScaleR** empaquetar y le guiará en las siguientes tareas:

> [!div class="checklist"]
> * Conectar a SQL Server
> * Definir una consulta con los datos que necesita o especificar una tabla o vista
> * Definir uno o más contextos de cálculo para usarlos al ejecutar código de R
> * Opcionalmente, puede definir las transformaciones que se aplican al origen de datos mientras se leen desde el origen

## <a name="define-a-sql-server-compute-context"></a>Definir un contexto de cálculo de SQL Server

Ejecute las siguientes instrucciones de R en un entorno de R en la estación de trabajo cliente. En esta sección se da por supuesto un [estación de trabajo de ciencia de datos con Microsoft R Client](../r/set-up-a-data-science-client.md), ya que incluye todos los paquetes de RevoScaleR, así como un conjunto de herramientas de R básico y ligero. Por ejemplo, puede usar Rgui.exe para ejecutar el script de R en esta sección.

1. Si el **RevoScaleR** paquete no está ya cargado, ejecutamos esta línea de código de R:

    ```R
    library("RevoScaleR")
    ```

     En este caso, las comillas son opcionales, aunque se recomienda.
     
     Si se produce un error, asegúrese de que el entorno de desarrollo de R usa una biblioteca que contiene el paquete RevoScaleR. Use un comando como `.libPaths()` para ver la ruta de acceso de la biblioteca actual.

2. Crea la cadena de conexión para SQL Server y lo guarda en una variable de R, *connStr*.

   Debe cambiar el marcador de posición "nombreDeSuServidor" por un nombre de instancia de SQL Server válido. Para el nombre del servidor, es posible que pueda usar solo el nombre de instancia o, es posible que deba calificar totalmente el nombre, dependiendo de la red.
    
   Para la autenticación de SQL Server, la sintaxis de conexión es como sigue:

    ```R
    connStr <- "Driver=SQL Server;Server=your_server_name;Database=nyctaxi_sample;Uid=your-sql-login;Pwd=your-login-password"
    ```

    Para la autenticación de Windows, la sintaxis es un poco diferente:
    
    ```R
    connStr <- "Driver=SQL Server;Server=your_server_name;Database=nyctaxi_sample;Trusted_Connection=True"
    ```

    Por lo general, se recomienda que use la autenticación de Windows cuando sea posible, evite guardar contraseñas en el código de R.

3. Defina las variables que se usará al crear un nuevo *contexto de proceso*. Después de crear el objeto de contexto de proceso, puede utilizarlo para ejecutar código R en la instancia de SQL Server.

    ```R
    sqlShareDir <- paste("C:\\AllShare\\",Sys.getenv("USERNAME"),sep="")
    sqlWait <- TRUE
    sqlConsoleOutput <- FALSE
    ```

    - R usa un directorio temporal cuando serializa los objetos de R entre la estación de trabajo y el equipo con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Puede especificar el directorio local que se usa como *sqlShareDir*o aceptar el valor predeterminado.
  
    - Use *sqlWait* para indicar si desea que R espere los resultados desde el servidor.  Para obtener una explicación de espera frente a los trabajos no en espera, consulte [distribuida e informática en paralelo con RevoScaleR en Microsoft R](https://docs.microsoft.com/r-server/r/how-to-revoscaler-distributed-computing).
  
    - Use el argumento *sqlConsoleOutput* para indicar que no desea ver el resultado de la consola de R.

4. Se llama a la [RxInSqlServer](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxinsqlserver) constructor para crear el objeto de contexto de proceso con las variables y las cadenas de conexión ya definidas y guardar el nuevo objeto en la variable de R *sqlcc*.
  
    ```R
    sqlcc <- RxInSqlServer(connectionString = connStr, shareDir = sqlShareDir, wait = sqlWait, consoleOutput = sqlConsoleOutput)
    ```

5. De forma predeterminada, el contexto de cálculo es local, por lo que deberá establecer explícitamente el *active* contexto de proceso.

    ```R
    rxSetComputeContext(sqlcc)
    ```

    + [rxSetComputeContext](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsetcomputecontext) devuelve el contexto de cálculo activo anteriormente invisible para que se pueda usar
    + [rxGetComputeContext](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsetcomputecontext) devuelve el contexto de cálculo activo
    
    Tenga en cuenta que establecer un contexto de cálculo afecta solo a las operaciones que utilizan las funciones de la **RevoScaleR** paquete; el proceso contexto no afecta a la forma en que se realizan las operaciones de R de código abierto.

## <a name="create-a-data-source-using-rxsqlserver"></a>Crear un origen de datos con RxSqlServer

Al usar las bibliotecas de R de Microsoft como RevoScaleR y MicrosoftML, un *origen de datos* es un objeto que se crea mediante las funciones de RevoScaleR. El objeto de origen de datos especifica un conjunto de datos que desea usar para una tarea, como la extracción del modelo entrenamiento o característica. Puede obtener datos desde una variedad de orígenes como SQL Server. Para obtener la lista de orígenes admitidos actualmente, consulte [RxDataSource](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdatasource).

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
  
    + El argumento *rowsPerRead* es importante para administrar el uso de memoria y cálculos eficaces.  La mayoría de las funciones analíticas mejoradas de[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] procesan los datos en fragmentos y acumulan los resultados intermedios, devolviendo los cálculos finales después de que se han leído todos los datos.  Agregando el *rowsPerRead* parámetro, puede controlar cuántas filas de datos se leen en cada fragmento para su procesamiento.  Si el valor de este parámetro es demasiado grande, el acceso a datos puede ser lenta porque no tiene suficiente memoria para procesar de forma eficaz un gran bloque de datos.  En algunos sistemas, establecer *rowsPerRead* en un valor demasiado pequeño también puede proporcionar un rendimiento más lento.

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
    
    ```R
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

    ```R
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

## <a name="next-steps"></a>Pasos siguientes

> [!div class="nextstepaction"]
> [Crear gráficos y trazados con R](walkthrough-create-graphs-and-plots-using-r.md)