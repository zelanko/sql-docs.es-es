---
title: "Crear objetos de datos de SQL Server mediante RxSqlServerData | Microsoft Docs"
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
ms.assetid: bcf5f7ff-795b-4815-b163-bcddd496efce
caps.latest.revision: 18
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
---
# Crear objetos de datos de SQL Server mediante RxSqlServerData
Ahora que ha creado la base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y tiene los permisos necesarios para trabajar con los datos, podrá crear objetos de R que le permiten trabajar con los datos, en el servidor y en su estación de trabajo.  
  
## Crear los objetos de datos de SQL Server  
En este paso, usará R para crear y rellenar dos tablas. Ambas tablas contienen datos de fraude de tarjeta de crédito simulados. Una tabla se usa para entrenar los modelos y la otra para la puntuación. 

Para crear tablas en el equipo remoto con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], usará la función `RxSqlServerData` proporcionada en el paquete **RevoScaleR**.  

> [!TIP]
> Si está usando R Tools para Visual Studio, seleccione **R Tools** en la barra de herramientas y haga clic en **Windows** para ver las opciones de depuración y ver las variables de R.
  
#### Para crear la tabla de datos de entrenamiento  
  
1.  Proporcione la cadena de conexión de base de datos en una variable de R. Aquí hemos proporcionado dos ejemplos de cadenas de conexión ODBC válidas para SQL Server: una que usa un inicio de sesión de SQL y otra para la autenticación integrada de Windows (recomendada).

    **Con un inicio de sesión de SQL**
    ```R  
    sqlConnString <- "Driver=SQL Server;Server=instance_name; Database=DeepDive;Uid=user_name;Pwd=password"   
    ```

    **Con la autenticación integrada de Windows**
    ```R  
    sqlConnString <- "Driver=SQL Server;Server=instance_name;Database=DeepDive;Trusted_Connection=True"
    ```

    Asegúrese de modificar el nombre de instancia, el nombre de la base de datos, el nombre de usuario y la contraseña según corresponda.  
  
2.  Especifique el nombre de la tabla que quiere crear y guárdelo en una variable de R.  
  
    ```R  
    sqlFraudTable <- "ccFraudSmall"       
    ```  
  
    Como la instancia y el nombre de la base de datos ya se han especificado como parte de la cadena de conexión, cuando se combinan las dos variables, el nombre *completo* de la nueva tabla se convierte en _instance.database.schema.ccFraudSmall_.  
  
3.  Antes de crear instancias del objeto de origen de datos, agregue una línea que especifica un parámetro adicional, *rowsPerRead*.  El parámetro *rowsPerRead* controla cuántas filas de datos se leen en cada lote.  
  
    ```R  
    sqlRowsPerRead = 5000   
    ```  
  
    Aunque este parámetro es opcional, es importante para controlar el uso de memoria y cálculos eficaces.  La mayoría de las funciones analíticas mejoradas de [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] procesan los datos en fragmentos y acumulan los resultados intermedios, devolviendo los cálculos finales después de que se han leído todos los datos.  
  
    Si el valor de este parámetro es demasiado grande, es posible que el acceso a los datos sea lento porque no tiene suficiente memoria para procesar de forma eficaz un fragmento de datos tan grande.  En algunos sistemas, si el valor de *rowsPerRead* es demasiado pequeño, el rendimiento puede ser más lento.  
  
    Para este tutorial, va a usar el tamaño de proceso por lotes definido por la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para controlar el número de filas de cada fragmento y guardar ese valor en la variable *sqlRowsPerRead*.  Se recomienda experimentar con esta configuración en el sistema cuando se trabaja con un gran conjunto de datos.  
  
4.  Por último, defina una variable para el nuevo origen de datos y pase los argumentos definidos previamente para el constructor *RxSqlServerData*. Tenga en cuenta que esto solo crea el objeto de origen de datos y no lo rellena.  
  
    ```R  
    sqlFraudDS <- RxSqlServerData(connectionString = sqlConnString,
       table = sqlFraudTable, 
       rowsPerRead = sqlRowsPerRead)  
    ```  

  
#### Para crear la tabla de datos de puntuación  

Podrá crear la tabla que contiene los datos de puntuación mediante el mismo proceso.  
  
1.  Cree una nueva variable de R, *sqlScoreTable*, para almacenar el nombre de la tabla usada para la puntuación.  
  
    ```R  
    sqlScoreTable <- "ccFraudScoreSmall"  
    ```  
  
2.  Proporcione esa variable como argumento a la función *RxSqlServerData* para definir un segundo objeto de origen de datos, *sqlScoreDS*.  
  
    ```R   
    sqlScoreDS <- RxSqlServerData(connectionString = sqlConnString,
       table = sqlScoreTable, rowsPerRead = sqlRowsPerRead) 
    ```  
  
  
Como ya se ha definido la cadena de conexión y otros parámetros como variables en el área de trabajo de R, es fácil crear nuevos orígenes de datos para distintas tablas, vistas o consultas. Solo hay que especificar un nombre de tabla diferente.  
  
Más adelante en este tutorial aprenderá a crear un objeto de origen de datos basado en una consulta SQL.  
  
## Cargar datos en tablas de SQL con R  
Ahora que ha creado las tablas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], puede cargar los datos en ellas mediante la correspondiente función **Rx**.  
  
El paquete **RevoScaleR** contiene funciones que admiten muchos orígenes de datos diferentes: para los datos de texto va a usar *RxTextData* para generar el objeto de origen de datos. Existen funciones adicionales para crear objetos de origen de datos a partir de datos de Hadoop, datos ODBC y así sucesivamente.  
  
> [!NOTE]  
> En esta sección, debe tener permisos de Ejecutar DDL en la base de datos.
  
#### Para cargar datos en la tabla de entrenamiento  
  
1.  Cree una variable de R, *ccFraudCsv*, y asigne a la variable la ruta de acceso del archivo CSV que contiene los datos de ejemplo que se incluyen en Microsoft R.  
  
    ```R  
    ccFraudCsv <- file.path(rxGetOption("sampleDataDir"), "ccFraudSmall.csv")   
    ```  
  
    Tenga en cuenta la función de utilidad, *rxGetOption*. Esta función se proporciona en el paquete **RevoScaleR** para ayudarle a configurar y administrar las opciones relacionadas con contextos cálculo locales y remotos, como el directorio compartido predeterminado, el número de procesadores (núcleos) para usar en cálculos, etc.  Esta función es útil porque obtiene los ejemplos de la biblioteca correcta independientemente de dónde esté ejecutando el código. Por ejemplo, pruebe a ejecutar la función en SQL Server y en su equipo de desarrollo para ver cómo difieren las rutas de acceso.
  
2.  Defina una variable para almacenar los nuevos datos y use la función *RxTextData* para especificar el origen de datos de texto.  
  
    ```R  
    inTextData <- RxTextData(file = ccFraudCsv,      colClasses = c(   
        "custID" = "integer", "gender" = "integer", "state" = "integer",   
        "cardholder" = "integer", "balance" = "integer",    
        "numTrans" = "integer",   
        "numIntlTrans" = "integer", "creditLine" = "integer",    
        "fraudRisk" = "integer"))    
    ```  
  
    El argumento *colClasses* es importante. Se usa para indicar el tipo de datos para asignar a cada columna de datos cargada desde el archivo de texto. En este ejemplo, todas las columnas se tratan como texto, excepto las columnas con nombre, que se tratan como enteros.  
  
3.  En este punto, puede hacer una pausa y ver la base de datos en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  Actualice la lista de tablas de la base de datos.  
  
    Verá que, aunque se crearon los objetos de datos de R en el área de trabajo local, todavía no se crearon las tablas en la base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Los datos tampoco se han cargado realmente del archivo de texto a la variable de R. 
  
4.  Ahora, llame a la función *rxDataStep* para insertar los datos en la tabla [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
    ```R  
    rxDataStep(inData = inTextData, outFile = sqlFraudDS, overwrite = TRUE)   
    ```  
  
    Suponiendo que no existen problemas con su cadena de conexión, después de una breve pausa, debería ver resultados como estos:  
  
      *Total de filas escritas: 10 000, tiempo total: 0,466*
      *Filas leídas: 10 000, total de filas procesadas: 10 000, tiempo total de fragmentos: 0,577 segundos*  
  
5.  Por medio de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], actualice la lista de tablas. Para comprobar que cada variable tiene los tipos de datos correcto y que se importó correctamente, también puede hacer clic con el botón derecho en la tabla [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] y seleccionar **Seleccionar las 1000 primeras filas**.  
  
#### Para cargar datos en la tabla de puntuación  
  
1.  Siga los mismos pasos para cargar en la base de datos el conjunto de datos usado para puntuación.  
  
    Primero proporcione la ruta de acceso al archivo de origen.  
  
    ```R  
    ccScoreCsv <- file.path(rxGetOption("sampleDataDir"), "ccFraudScoreSmall.csv")   
    ```  
  
2.  Use la función *RxTextData* para obtener los datos y guardarlos en la variable *inTextData*.  
  
    ```R  
    inTextData <- RxTextData(file = ccScoreCsv,      colClasses = c(   
        "custID" = "integer", "gender" = "integer", "state" = "integer",   
        "cardholder" = "integer", "balance" = "integer",    
        "numTrans" = "integer",   
        "numIntlTrans" = "integer", "creditLine" = "integer"))  
  
    ```  
  
3.  Llame a la función *rxDataStep* para sobrescribir la tabla actual con el nuevo esquema y los datos.  
  
    ```R  
    rxDataStep(inData = inTextData, sqlScoreDS, overwrite = TRUE)    
    ```  
  
    -   El argumento *inData* define el origen de datos que usar.  
  
    -   El argumento *outFile* especifica la tabla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] donde quiere guardar los datos.  
  
    -   Si la tabla ya existe y no usa la opción *sobrescribir*, los resultados se insertarán sin truncamiento.  
  
De nuevo, si la conexión se ha realizado correctamente, debería ver un mensaje indicando la finalización y el tiempo requerido para escribir los datos en la tabla: 

*Total de filas escritas: 10000, tiempo total: 0,384*
*Filas leídas: 10000, total de filas procesadas: 10000, tiempo total de fragmentos: 0,456 segundos*  
  
## Más información sobre rxDataStep  
*rxDataStep* es una función muy eficaz del paquete **RevoScaleR** que puede realizar varias transformaciones en una trama de datos R, para convertir los datos en la representación requerida por el destino. En este caso, el destino es [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
También puede especificar transformaciones en los datos, como indicar qué columnas se van a excluir, agregar columnas nuevas o cambiar tipos de datos, mediante las funciones de R en los argumentos de *rxDataStep*. Verá ejemplos de estas operaciones en la [Lección 4](../../advanced-analytics/r-services/lesson-4-analyze-data-in-local-compute-context-data-science-deep-dive.md).  
  
## Paso siguiente  
[Consultar y modificar los datos de SQL Server&#40;Análisis detallado de ciencia de datos&#41;](../../advanced-analytics/r-services/query-and-modify-the-sql-server-data-data-science-deep-dive.md)  
  
## Paso anterior  
[Lesson 1: Work with SQL Server Data using R &#40;Data Science Deep Dive&#41; (Lección 1: Trabajar con datos de SQL Server con R&#40;Análisis detallado de ciencia de datos&#41;)](../../advanced-analytics/r-services/lesson-1-work-with-sql-server-data-using-r-data-science-deep-dive.md)  
  
