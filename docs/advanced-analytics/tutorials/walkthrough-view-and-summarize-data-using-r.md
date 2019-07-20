---
title: Ver y resumir datos de SQL Server con funciones de R
description: Tutorial que muestra cómo visualizar y generar resúmenes estadísticos mediante las funciones de R para el análisis en base de datos en SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/26/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.openlocfilehash: 52ba1a8f036037ade42c8483b1735c84cc72867e
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/19/2019
ms.locfileid: "68345786"
---
# <a name="view-and-summarize-sql-server-data-using-r-walkthrough"></a>Ver y resumir datos de SQL Server mediante R (tutorial)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

En esta lección se presentan las funciones del paquete **RevoScaleR** y se explican las tareas siguientes:

> [!div class="checklist"]
> * Conexión con SQL Server
> * Definir una consulta con los datos que necesita o especificar una tabla o vista
> * Definir uno o más contextos de cálculo para usarlos al ejecutar código de R
> * Opcionalmente, defina las transformaciones que se aplican al origen de datos mientras se leen desde el origen.

## <a name="define-a-sql-server-compute-context"></a>Definir un contexto de cálculo de SQL Server

Ejecute las siguientes instrucciones de R en un entorno de R en la estación de trabajo del cliente. En esta sección se supone que se trata de una [estación de trabajo de ciencia de datos con Microsoft R Client](../r/set-up-a-data-science-client.md), ya que incluye todos los paquetes de RevoScaleR, así como un conjunto básico y ligero de herramientas de R. Por ejemplo, puede usar Rgui. exe para ejecutar el script de R en esta sección.

1. Si el paquete **RevoScaleR** todavía no está cargado, ejecute esta línea de código R:

    ```R
    library("RevoScaleR")
    ```

     Las comillas son opcionales, en este caso, aunque se recomienda.
     
     Si recibe un error, asegúrese de que el entorno de desarrollo de R usa una biblioteca que incluye el paquete RevoScaleR. Use un comando como `.libPaths()` para ver la ruta de acceso de la biblioteca actual.

2. Cree la cadena de conexión para SQL Server y guárdela en una variable de R, *connStr*.

   Debe cambiar el marcador de posición "nombredesuservidor" por un nombre de instancia de SQL Server válido. En el caso del nombre del servidor, es posible que pueda usar solo el nombre de la instancia, o puede que necesite completar el nombre, en función de la red.
    
   Para la autenticación de SQL Server, la sintaxis de conexión es la siguiente:

    ```R
    connStr <- "Driver=SQL Server;Server=your_server_name;Database=nyctaxi_sample;Uid=your-sql-login;Pwd=your-login-password"
    ```

    Para la autenticación de Windows, la sintaxis es un poco diferente:
    
    ```R
    connStr <- "Driver=SQL Server;Server=your_server_name;Database=nyctaxi_sample;Trusted_Connection=True"
    ```

    Por lo general, se recomienda usar la autenticación de Windows siempre que sea posible, para evitar guardar las contraseñas en el código de R.

3. Defina las variables que se usarán para crear un nuevo *contexto de cálculo*. Después de crear el objeto de contexto de proceso, puede usarlo para ejecutar el código de R en la instancia de SQL Server.

    ```R
    sqlShareDir <- paste("C:\\AllShare\\",Sys.getenv("USERNAME"),sep="")
    sqlWait <- TRUE
    sqlConsoleOutput <- FALSE
    ```

    - R usa un directorio temporal cuando serializa los objetos de R entre la estación de trabajo y el equipo con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Puede especificar el directorio local que se usa como *sqlShareDir*o aceptar el valor predeterminado.
  
    - Use *sqlWait* para indicar si desea que R espere los resultados del servidor.  Para obtener una explicación de los trabajos en espera frente a los que no están en espera, consulte computación [en paralelo y distribuida con RevoScaleR en Microsoft R](https://docs.microsoft.com/r-server/r/how-to-revoscaler-distributed-computing).
  
    - Use el argumento *sqlConsoleOutput* para indicar que no desea ver la salida de la consola de R.

4. Llame al constructor [RxInSqlServer](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxinsqlserver) para crear el objeto de contexto de cálculo con las variables y las cadenas de conexión ya definidas, y guarde el nuevo objeto en la variable de R *sqlcc*.
  
    ```R
    sqlcc <- RxInSqlServer(connectionString = connStr, shareDir = sqlShareDir, wait = sqlWait, consoleOutput = sqlConsoleOutput)
    ```

5. De forma predeterminada, el contexto de cálculo es local, por lo que debe establecer explícitamente el contexto de cálculo *activo* .

    ```R
    rxSetComputeContext(sqlcc)
    ```

    + [rxSetComputeContext](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsetcomputecontext) devuelve el contexto de cálculo activo previamente de forma invisible para que pueda usarlo
    + [rxGetComputeContext](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsetcomputecontext) devuelve el contexto de cálculo activo
    
    Tenga en cuenta que la configuración de un contexto de cálculo solo afecta a las operaciones que usan funciones en el paquete **RevoScaleR** . el contexto de cálculo no afecta a la manera en que se realizan las operaciones de R de código abierto.

## <a name="create-a-data-source-using-rxsqlserver"></a>Creación de un origen de datos mediante RxSqlServer

Cuando se usan las bibliotecas de Microsoft R como RevoScaleR y MicrosoftML, un *origen de datos* es un objeto que se crea mediante las funciones de RevoScaleR. El objeto de origen de datos especifica algún conjunto de datos que desea usar para una tarea, como el entrenamiento del modelo o la extracción de características. Puede obtener datos de diversos orígenes, como SQL Server. Para obtener la lista de orígenes admitidos actualmente, vea [RxDataSource](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdatasource).

Antes definía una cadena de conexión y guardaba esa información en una variable de R. Puede volver a usar esa información de conexión para especificar los datos que desea obtener.

1. Guarde una consulta SQL como una variable de cadena. La consulta define los datos para entrenar el modelo.

    ```R
    sampleDataQuery <- "SELECT TOP 1000 tipped, fare_amount, passenger_count,trip_time_in_secs,trip_distance, pickup_datetime, dropoff_datetime, pickup_longitude, pickup_latitude, dropoff_longitude, dropoff_latitude FROM nyctaxi_sample"
    ```

    Hemos usado una cláusula TOP aquí para que las cosas se ejecuten más rápido, pero las filas reales devueltas por la consulta pueden variar en función del orden. Por lo tanto, los resultados de resumen también pueden ser diferentes de los que se enumeran a continuación. No dude en quitar la cláusula TOP.

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
    
    + El argumento  *colClasses* especifica los tipos de columna que se usarán al mover los datos entre [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y R. Esto es importante porque [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa tipos de datos distintos a los de R y más tipos de datos. Para obtener más información, consulte [bibliotecas y tipos de datos de R](../r/r-libraries-and-data-types.md).
  
    + El argumento *rowsPerRead* es importante para administrar el uso de memoria y cálculos eficientes.  La mayoría de las funciones analíticas mejoradas de[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] procesan los datos en fragmentos y acumulan los resultados intermedios, devolviendo los cálculos finales después de que se han leído todos los datos.  Al agregar el parámetro *rowsPerRead* , puede controlar el número de filas de datos que se leen en cada fragmento para su procesamiento.  Si el valor de este parámetro es demasiado grande, el acceso a los datos puede ser lento porque no tiene suficiente memoria para procesar eficazmente un gran fragmento de datos.  En algunos sistemas, establecer *rowsPerRead* en un valor demasiado pequeño también puede proporcionar un rendimiento más lento.

3. En este punto, ha creado el objeto de *origen* de datos, pero no contiene ningún dato. Los datos no se extraen de la consulta SQL en el entorno local hasta que se ejecuta una función como [rxImport](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdatastep) o [rxSummary](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxsummary).

    Sin embargo, ahora que ha definido los objetos de datos, puede utilizarlos como argumento para otras funciones.

## <a name="use-the-sql-server-data-in-r-summaries"></a>Uso de los datos de SQL Server en resúmenes de R

En esta sección, probará algunas de las funciones proporcionadas en [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] que admiten contextos de cálculo remotos. Al aplicar funciones de R al origen de datos, puede explorar, resumir y representar gráficamente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] los datos.

1. Llame a la función [rxGetVarInfo](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxgetvarinfo) para obtener una lista de las variables en el origen de datos y sus tipos de datos.

    **rxGetVarInfo** es una función útil; puede llamarlo en cualquier trama de datos o en un conjunto de datos de un objeto de datos remoto para obtener información como los valores máximo y mínimo, el tipo de datos y el número de niveles en las columnas de factor.
    
    Considere la posibilidad de ejecutar esta función después de cualquier tipo de entrada de datos, transformación de características o ingeniería de características. Al hacerlo, puede asegurarse de que todas las características que desea utilizar en el modelo tienen el tipo de datos esperado y evitar errores.
  
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

    rxSummary se basa en la función `summary` de R, pero tiene algunas características y ventajas adicionales. rxSummary funciona en varios contextos de cálculo y admite la fragmentación.  También puede usar rxSummary para transformar valores o resumir en función de los niveles de factor.
    
    En este ejemplo, se resume el importe de la tarifa en función del número de pasajeros.
    
    ```R
    start.time <- proc.time()
    rxSummary(~fare_amount:F(passenger_count,1,6), data = inDataSource)
    used.time <- proc.time() - start.time
    print(paste("It takes CPU Time=", round(used.time[1]+used.time[2],2)," seconds,
      Elapsed Time=", round(used.time[3],2),
      " seconds to summarize the inDataSource.", sep=""))
    ```
    + El primer argumento de rxSummary especifica la fórmula o el término por el que resumir. En este caso `F()` , la función se usa para convertir los valores de recuento de _pasajeros\__ en factores antes de resumir. También debe especificar el valor mínimo (1) y el valor máximo (6) para la variable de factor de _número de pasajeros\__ .
    + Si no especifica las estadísticas de salida, de forma predeterminada, rxSummary genera media, StDev, min, Max y el número de observaciones válidas y que faltan.
    + Este ejemplo también incluye algo de código para realizar un seguimiento de la hora a la que empieza y finaliza la función, para que pueda comparar el rendimiento.
  
    **Resultado**

    Si la función rxSummary se ejecuta correctamente, debería ver resultados como estos, seguido de una lista de estadísticas por categoría. 

    ```R
    rxSummary(formula = ~fare_amount:F(passenger_count, 1,6), data = inDataSource)
    Data: inDataSource (RxSqlServerData Data Source)
    Number of valid observations: 1000
    ```

### <a name="bonus-exercise-on-big-data"></a>Ejercicio adicional sobre macrodatos

Intente definir una nueva cadena de consulta con todas las filas. Se recomienda configurar un nuevo objeto de origen de datos para este experimento. También puede intentar cambiar el parámetro *rowsToRead* para ver cómo afecta al rendimiento.

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
> Mientras se está ejecutando, puede usar una herramienta como el [Explorador de procesos](https://technet.microsoft.com/sysinternals/processexplorer.aspx) o SQL Server Profiler para ver cómo se establece la conexión y el código de R se ejecuta con SQL Server Services.
> 
> Otra opción es supervisar los trabajos de R que se ejecutan en SQL Server mediante estos [informes personalizados](../r/monitor-r-services-using-custom-reports-in-management-studio.md).

## <a name="next-steps"></a>Pasos siguientes

> [!div class="nextstepaction"]
> [Crear gráficos y trazados con R](walkthrough-create-graphs-and-plots-using-r.md)