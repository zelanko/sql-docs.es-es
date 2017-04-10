---
title: "Ver y resumir datos mediante R (Tutorial integral de ciencia de datos) | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
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
ms.assetid: 358e1431-8f47-4d32-a02f-f90e519eef49
caps.latest.revision: 21
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
---
# Ver y resumir datos mediante R (Tutorial integral de ciencia de datos)
Ahora trabajará con los mismos datos usando código de R. También aprenderá cómo usar las funciones del paquete **RevoScaleR** incluido con [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] para generar los resúmenes de los datos en el contexto del servidor [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y enviar los resultados a su entorno de R.  

Con este tutorial se proporciona un script de R que incluye todo el código necesario para crear el objeto de datos, generar resúmenes y generar modelos. Puede encontrar el archivo de script de R **RSQL_RWalkthrough.R**en la ubicación donde instaló los archivos de script.  
+ Si tiene experiencia con R, puede ejecutar todo el script de una vez.
+ Para quienes aprenden a usar RevoScaleR, este tutorial explica el script línea a línea.
+ Para ejecutar líneas individuales del script, puede resaltar una o varias líneas en el archivo y presionar Ctrl + ENTRAR.    
  
> [!TIP]  Guarde el área de trabajo de R en caso de que quiera completar el resto del tutorial más adelante.  De esta forma los objetos de datos y otras variables estarán listos para su reutilización.   

## <a name="defining-sql-server-data-sources-and-compute-contexts"></a>Definición de orígenes de datos y contextos de cálculo de SQL Server
Para obtener datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y usarlos en el código de R, debe hacer lo siguiente:  
  
- Crear una conexión a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
- Definir una consulta con los datos que necesita o especificar una tabla o vista    
- Definir uno o más contextos de cálculo para usarlos cuando se ejecute el código de R    
-   De manera opcional, definir las funciones que se pueden aplicar al origen de datos  
 

### <a name="load-the-revoscaler-library"></a>Cargar la biblioteca de RevoScaleR

+  Si el **RevoScaleR** paquete ya no está cargado, ejecute:
    ```R
    library("RevoScaleR")`.  
    ```  
    Si recibe un error, asegúrese de que el entorno de desarrollo de R usa la biblioteca que contiene el paquete RevoScaleR. Use un comando como `.libPaths())` para ver la ruta de acceso actual:  

    Si es la primera vez que usa el paquete **RevoScaleR**, escriba `help("RevoScaleR")` o `help("RxSqlServerData")` para obtener la ayuda en línea en el entorno de R.  

### <a name="create-connection-strings"></a>Crear cadenas de conexión


1. Defina las cadenas de conexión. En este tutorial, incluimos ejemplos de inicios de sesión de SQL y de la autenticación integrada de Windows. Se recomienda que use la autenticación de Windows cada vez que sea posible, para así evitar tener que guardar contraseñas en el código de R.

    La cuenta que use debe tener permisos para leer los datos y crear nuevas tablas en la base de datos especificada. Para obtener información sobre cómo agregar usuarios a la base de datos SQL y concederles los permisos correctos, consulte [Post-Installation Server Configuration &#40;SQL Server R Services&#41; (Configuración posterior a la instalación del servidor &#40;SQL Server R Services&#41;)](../Topic/Post-Installation%20Server%20Configuration%20(SQL%20Server%20R%20Services).md). 

    ```R  
    # SQL authentication  
    connStrSql <- "Driver=SQL Server;Server=<SQL_instance_name>;Database=<database_name>;    Uid=<user_name>;Pwd=<user password>"  

    # Windows authentication  
    connStrWin <- "Driver=SQL Server;Server=<SQL_instance_name>;Database=<database_name>;Trusted_Connection=Yes" 
    
    # Use one of the connection strings
    connStr <- connStrWin 
    ```
    > [!NOTE] Asegúrese de editar el nombre del servidor, el nombre de la base de datos, el nombre de usuario y la contraseña según sea necesario. 
      
  
### <a name="define-and-set-a-compute-context"></a>Definir y establecer un contexto de cálculo  

A continuación, definirá un *contexto de cálculo* que permita que el código de R se ejecute en el equipo con SQL Server. Normalmente, cuando se usa R, todas las operaciones se ejecutan en memoria en el equipo. Sin embargo, si indica que las operaciones de R se deben ejecutar en la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], puede ejecutar algunas tareas en paralelo y usar los recursos del servidor.  

De manera predeterminada, el contexto de cálculo es local, por lo que deberá establecer explícitamente el contexto de cálculo según la operación.  


1.  Empiece por definir algunas variables que se usen para crear el contexto de cálculo.  
  
    ```R    
    sqlShareDir <- paste("C:\\AllShare\\",Sys.getenv("USERNAME"),sep="")  
    sqlWait <- TRUE  
    sqlConsoleOutput <- FALSE    
    ```    
    -   R usa un directorio temporal cuando serializa los objetos de R entre la estación de trabajo y el equipo con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Puede especificar el directorio local que se usa como *sqlShareDir* o aceptar el valor predeterminado.  
  
    -   Use *sqlWait* para indicar si desea que R espere los resultados o no.  Para ver un análisis sobre los trabajos de espera y los trabajos no en espera, consulte [ScaleR Distributed Computing](https://msdn.microsoft.com/microsoft-r/scaler-distributed-computing) (Computación distribuida de ScaleR).
  
    -   Use el argumento *sqlConsoleOutput* para indicar que no desea ver los resultados desde la consola de R.  
  
2.  Cree el objeto de contexto de cálculo con las variables y las cadenas de conexión ya definidas y guárdelo en la variable *sqlcc* de R.  
  
    ```  
    sqlcc <- RxInSqlServer(connectionString = connStr, shareDir = sqlShareDir,   
                        wait = sqlWait, consoleOutput = sqlConsoleOutput)  
    ```  

4. Establezca el contexto de cálculo.
    ```R
    rxSetComputeContext(sqlcc)  
    ```  
   + `rxSetComputeContext` devuelve el contexto de cálculo activo anteriormente invisible para que pueda usarlo
   + `rxGetComputeContext` devuelve el contexto de cálculo activo  
  
    Observe que establecer un contexto de cálculo solo afecta las operaciones que usan funciones en el paquete **RevoScaleR**; el contexto de cálculo no afecta la manera en que se realizan las operaciones de R de código abierto.  
  
### <a name="create-an-rxsqlserver-data-object"></a>Crear un objeto de datos RxSqlServer  

Ahora que definió la conexión a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con la que trabajar, puede usar ese objeto de conexión de datos como base para definir orígenes de datos diferentes. Un *origen de datos* especifica un conjunto de datos que quiere usar para una tarea, como entrenamiento, exploración, puntuación, o para generar características.  
    
Puede definir conjuntos de datos de SQL Server mediante el uso de la función *RxSqlServer* y pasar una cadena de conexión y la definición de los datos que se van a obtener.  
  
1. Guarde la instrucción SQL como una variable de cadena. Esta consulta define los datos que usará para entrenar el modelo.    
    ```R
    sampleDataQuery <- "SELECT TOP 1000 tipped, fare_amount, 
           passenger_count,trip_time_in_secs,trip_distance,   
           pickup_datetime, dropoff_datetime, pickup_longitude, 
           pickup_latitude, dropoff_longitude,    
           dropoff_latitude 
           FROM nyctaxi_sample"  
    ```

2. Pase la definición de consulta como argumento al origen de datos de SQL Server. El argumento *colClasses* especifica el esquema de los datos que se van a devolver a través de la asignación de SQL 

    ```R  
    inDataSource <- RxSqlServerData(sqlQuery = sampleDataQuery, 
         connectionString = connStr,
         colClasses = c(pickup_longitude = "numeric", pickup_latitude = "numeric",
         dropoff_longitude = "numeric", dropoff_latitude = "numeric"),  
         rowsPerRead=500)  
    ```
    
    + El argumento *colClasses* especifica los tipos de columna que se usarán al mover los datos entre [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y R. Esto es importante porque [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa tipos de datos distintos a los de R y más tipos de datos. Para obtener más información, consulte [Working with R Data Types (Trabajar con tipos de datos de R)](../../advanced-analytics/r-services/working-with-r-data-types.md).  
  
    + El argumento *rowsPerRead* es importante para controlar el uso de memoria y cálculos eficaces.  La mayoría de las funciones analíticas mejoradas de[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] procesan los datos en fragmentos y acumulan los resultados intermedios, devolviendo los cálculos finales después de que se han leído todos los datos.  Agregando el parámetro `rowsPerRead` , puede controlar cuántas filas de datos se leen en cada fragmento para su procesamiento.  Si el valor de este parámetro es demasiado grande, es posible que el acceso a los datos sea lento porque no tiene suficiente memoria para procesar de forma eficaz un fragmento de datos tan grande.  En algunos sistemas, establecer `rowsPerRead` en un valor demasiado pequeño también puede proporcionar un rendimiento más lento.  

> [!TIP] Después de crear el objeto *inDataSource* , puede volver a usar este objeto tantas veces como sea necesario, para obtener información básica sobre los datos y las variables usados, manipular y transformar los datos o usarlos para entrenar un modelo.  Sin embargo, el objeto *inDataSource* mismo todavía no contiene datos de la consulta SQL. Los datos no se extraen al entorno local hasta que se ejecuta una función como *rxImport* o *rxSummary*.          
  
## <a name="using-the-sql-server-data-in-r"></a>Uso de los datos de SQL Server en R  
Ahora puede aplicar funciones de R al origen de datos, explorar, resumir y mostrar los datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en un gráfico. En esta sección, probará algunas de las funciones proporcionadas en [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] que admiten contextos de cálculo remotos.  
  
-   `rxGetVarInfo`: use esta función con cualquier trama de datos o conjunto de datos en un objeto de datos remotos (además de algunas listas y matrices) para obtener información como los valores máximo y mínimo, el tipo de datos y el número de niveles en las columnas de factor.  
  
    Considere la posibilidad de ejecutar esta función después de cualquier tipo de entrada de datos, transformación de características o ingeniería de características. Al hacerlo, puede asegurarse de que todas las características que quiere usar en el modelo son del tipo de datos esperado y evitar errores.  
 
  
-   `rxSummary`: use esta función para obtener estadísticas más detalladas sobre las variables individuales. También puede transformar los valores, calcular resúmenes mediante niveles de factor y guardar los resúmenes para su reutilización.  
  
  
### <a name="inspect-variables-in-the-data-source"></a>Inspeccionar las variables en el origen de datos  
    
+ Llame a la función `rxGetVarInfo`, usando el origen de datos  `inDataSource` como argumento, para obtener una lista de las variables en el origen de datos y sus tipos de datos.  
  
    ```R  
    rxGetVarInfo(data = inDataSource)  
    ```  
  
    *Resultados:*  
    *Var 1: tipped, Type: integer*  
    *Var 2: fare_amount, Type: numeric*  
    *Var 3: passenger_count, Type: integer*  
    *Var 4: trip_time_in_secs, Type: numeric, Storage: int64*  
    *Var 5: trip_distance, Type: numeric*  
    *Var 6: pickup_datetime, Type: character*  
    *Var 7: dropoff_datetime, Type: character*  
    *Var 8: pickup_longitude, Type: numeric*  
    *Var 9: pickup_latitude, Type: numeric*  
    *Var 10: dropoff_longitude, Type: numeric*  
  
### <a name="create-a-summary-using-r"></a>Crear un resumen con R

+ Llame a la función `rxSummary` de RevoScaleR para resumir el importe de la tarifa en función del número de pasajeros. 
    ```R  
    start.time <- proc.time()  
    rxSummary(~fare_amount:F(passenger_count), data = inDataSource)  
    used.time <- proc.time() - start.time  
    print(paste("It takes CPU Time=", round(used.time[1]+used.time[2],2)," seconds,
      Elapsed Time=", round(used.time[3],2), 
      " seconds to summarize the inDataSource.", sep=""))
    ```  
 
    + El primer argumento de `rxSummary` especifica la fórmula o el término por el que resumir. Aquí se usa la función `F()` para convertir los valores de passenger_count en factores antes del resumen.  
    + Si no especifica las estadísticas de salida de forma predeterminada `rxSummary` genera Media, StDev, Min, Max y el número de observaciones válidas y que faltan.  
    + Este ejemplo también incluye algo de código para realizar un seguimiento de la hora a la que empieza y finaliza la función, para que pueda comparar el rendimiento.  
  
    *Resultados*  
    *rxSummary(formula = ~fare_amount:F(passenger_count), data = inDataSource)*  
    *Summary Statistics Results for: ~fare_amount:F(passenger_count)*  
    *Data: inDataSource (RxSqlServerData Data Source)*  
    *Number of valid observations: 1000*   
    *Name                          Mean    StdDev   Min Max ValidObs MissingObs*  
    *fare_amount:F_passenger_count 12.4875 9.682605 2.5 64  1000     0*   
    *Statistics by category (6 categories):   *Category                             F_passenger_count Means    StdDev    Min*   
    *fare_amount for F(passenger_count)=1 1                 12.00901  9.219458  2.5*  
    *fare_amount for F(passenger_count)=2 2                 11.61893  8.858739  3.0*  
    *fare_amount for F(passenger_count)=3 3                 14.40196 10.673340  3.5*  
    *fare_amount for F(passenger_count)=4 4                 13.69048  8.647942  4.5*  
    *fare_amount for F(passenger_count)=5 5                 19.30909 14.122969  3.5*  
    *fare_amount for F(passenger_count)=6 6                 12.00000        NA 12.0*  
    *Max ValidObs*  
    *55  666*   
    *52  206*   
    *52   51*   
    *39   21*   
    *64   55*   
    *12    1*   
    *"It takes CPU Time=0.5 seconds, Elapsed Time=4.59 seconds to summarize the inDataSource."*  
  

  
## <a name="next-step"></a>Paso siguiente  
[Crear gráficos y trazados con R &#40;Tutorial integral de ciencia de datos&#41;](../../advanced-analytics/r-services/create-graphs-and-plots-using-r-data-science-end-to-end-walkthrough.md)  
  
## <a name="previous-lesson"></a>Lección anterior  
[Lección 1: Preparar los datos &#40;Tutorial integral de ciencia de datos&#41;](../../advanced-analytics/r-services/lesson-1-prepare-the-data-data-science-end-to-end-walkthrough.md)  
  
  
  
