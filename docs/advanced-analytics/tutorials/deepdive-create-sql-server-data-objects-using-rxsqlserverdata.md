---
title: 'Crear objetos de datos de SQL Server mediante RevoScaleR RxSqlServerData: SQL Server Machine Learning'
description: Tutorial del tutorial sobre cómo crear objetos de datos mediante el lenguaje R en SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/26/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 45643dbcdc2876fe0794ddb731abe6334537169c
ms.sourcegitcommit: 2827d19393c8060eafac18db3155a9bd230df423
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/27/2019
ms.locfileid: "58510362"
---
# <a name="create-sql-server-data-objects-using-rxsqlserverdata-sql-server-and-revoscaler-tutorial"></a>Crear objetos de datos de SQL Server mediante RxSqlServerData (tutorial de SQL Server y RevoScaleR)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

En esta lección forma parte de la [RevoScaleR tutorial](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md) sobre cómo usar [funciones de RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) con SQL Server.

Lección dos es una continuación de la creación de la base de datos: agregar tablas y carga de datos. Si un DBA crea la base de datos y el inicio de sesión en [lección uno](deepdive-work-with-sql-server-data-using-r.md), puede agregar las tablas mediante un IDE de R como RStudio o como una herramienta integrada **Rgui**.

Desde R, conéctese a SQL Server y use **RevoScaleR** funciones para realizar las tareas siguientes:

> [!div class="checklist"]
> * Crear tablas de datos de entrenamiento y las predicciones
> * Cargar tablas con datos de un archivo .csv local

Datos de ejemplo son datos de fraude de tarjeta de crédito simulados (ccFraud conjunto de datos), con particiones en entrenamiento y conjuntos de datos de puntuación. El archivo de datos se incluye en **RevoScaleR**.

Usar un IDE de R o **Rgui** para completar estos tarda. Asegúrese de usar los archivos ejecutables de R que se encuentra en esta ubicación: C:\Program Files\Microsoft\R Client\R_SERVER\bin\x64 (ya sea Rgui.exe si usa esa herramienta o un IDE de R que apunte a C:\Program Files\Microsoft\R Client\R_SERVER). Tener un [estación de trabajo de R cliente](../r/set-up-a-data-science-client.md) con estos archivos ejecutables se consideran un requisito previo de este tutorial.

## <a name="create-the-training-data-table"></a>Crear la tabla de datos de entrenamiento

1. Store la cadena de conexión de base de datos en una variable de R. A continuación se muestran dos ejemplos de cadenas de conexión ODBC válidas para SQL Server: uno con un inicio de sesión SQL y otro para la autenticación integrada de Windows. 

   No olvide modificar el nombre del servidor, el nombre de usuario y la contraseña según corresponda.

    **Inicio de sesión de SQL**
    ```R
    sqlConnString <- "Driver=SQL Server;Server=<server-name>; Database=RevoDeepDive;Uid=<user_name>;Pwd=<password>"
    ```

    **Autenticación de Windows**
    ```R
    sqlConnString <- "Driver=SQL Server;Server=<server-name>;Database=RevoDeepDive;Trusted_Connection=True"
    ```

2. Especifique el nombre de la tabla que quiere crear y guárdelo en una variable de R.
  
    ```R
    sqlFraudTable <- "ccFraudSmall"
    ```
  
    Dado que la instancia del servidor y el nombre de la base de datos ya se especifican como parte de la cadena de conexión, cuando se combinan las dos variables, la *completo* nombre de la nueva tabla se convierte en  *instance.database.schema.ccFraudSmall*.
  
3.  Opcionalmente, especifique *rowsPerRead* para controlar el número de filas de datos se lee en cada lote.
  
    ```R
    sqlRowsPerRead = 5000
    ```
  
    Aunque este parámetro es opcional, si se establece puede producir cálculos más eficaces. La mayoría de las funciones analíticas mejoradas de **RevoScaleR** y **MicrosoftML** procesar datos en fragmentos. El *rowsPerRead* parámetro determina el número de filas de cada fragmento.
  
    Es posible que deba experimentar con esta opción para buscar el equilibrio adecuado. Si el valor es demasiado grande, el acceso a datos podría ser lento si no hay suficiente memoria para procesar los datos en fragmentos de ese tamaño. Por el contrario, en algunos sistemas, si el valor de *rowsPerRead* es demasiado pequeño, rendimiento puede también ralentizan.
  
    Como un valor inicial, use el tamaño de proceso de batch predeterminado definido por la instancia del motor de base de datos para controlar el número de filas de cada fragmento (5000 filas). Guardar ese valor en la variable *sqlRowsPerRead*.
  
4.  Defina una variable para el nuevo objeto de origen de datos y pase los argumentos definidos previamente para el **RxSqlServerData** constructor. Tenga en cuenta que esto solo crea el objeto de origen de datos y no lo rellena. Carga de datos es un paso independiente.
  
    ```R
    sqlFraudDS <- RxSqlServerData(connectionString = sqlConnString,
       table = sqlFraudTable,
       rowsPerRead = sqlRowsPerRead)
    ```

## <a name="create-the-scoring-data-table"></a>Crear la tabla de datos de puntuación

Con los mismos pasos, cree la tabla que contiene los datos de puntuación mediante el mismo proceso.

1. Cree una nueva variable de R, *sqlScoreTable*, para almacenar el nombre de la tabla usada para la puntuación.
  
    ```R
    sqlScoreTable <- "ccFraudScoreSmall"
    ```
  
2. Proporcione esa variable como argumento a la función **RxSqlServerData** para definir un segundo objeto de origen de datos, *sqlScoreDS*.
  
    ```R
    sqlScoreDS <- RxSqlServerData(connectionString = sqlConnString,
       table = sqlScoreTable, rowsPerRead = sqlRowsPerRead)
    ```

Dado que ya se han definido la cadena de conexión y otros parámetros como variables en el área de trabajo de R, puede volver a usar para nuevos orígenes de datos que representa las diferentes tablas, vistas o consultas.

> [!NOTE]
> La función usa argumentos distintos para definir un origen de datos basado en una tabla completa a un origen de datos basado en una consulta. Esto es porque el motor de base de datos de SQL Server debe preparar las consultas de forma diferente. Más adelante en este tutorial, obtendrá información sobre cómo crear un objeto de origen de datos basado en una consulta SQL.

## <a name="load-data-into-sql-tables-using-r"></a>Cargar datos en tablas de SQL con R

Ahora que ha creado las tablas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , puede cargar los datos en ellas mediante la correspondiente función **Rx** .

El **RevoScaleR** paquete contiene las funciones específicas de tipos de orígenes de datos. Para los datos de texto, utilice [RxTextData](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxtextdata) para generar el objeto de origen de datos. Existen funciones adicionales para crear objetos de origen de datos a partir de datos de Hadoop, datos ODBC y así sucesivamente.

> [!NOTE]
> Esta sección, debe tener **Ejecutar DDL** permisos en la base de datos.

### <a name="load-data-into-the-training-table"></a>Cargar datos en la tabla de entrenamiento

1. Cree una variable de R, *ccFraudCsv*y asigne a la variable la ruta de acceso del archivo CSV que contiene los datos de ejemplo. Este conjunto de datos se proporciona en **RevoScaleR**. El "sampleDataDir" es una palabra clave en el **rxGetOption** función.
  
    ```R
    ccFraudCsv <- file.path(rxGetOption("sampleDataDir"), "ccFraudSmall.csv")
    ```
  
    Observe la llamada a **rxGetOption**, que es el método GET asociado [rxOptions](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxoptions) en **RevoScaleR**. Use esta utilidad para establecer y las opciones de lista relacionadas con contextos cálculo locales y remotos, como el directorio compartido predeterminado o el número de procesadores (núcleos) que se usarán en los cálculos.
    
    Esta particular llamada obtiene los ejemplos de la biblioteca correcta independientemente de dónde se ejecute el código. Por ejemplo, pruebe a ejecutar la función en SQL Server y en su equipo de desarrollo para ver cómo difieren las rutas de acceso.
  
2. Defina una variable para almacenar los nuevos datos y use la función **RxTextData** para especificar el origen de datos de texto.
  
    ```R
    inTextData <- RxTextData(file = ccFraudCsv,      colClasses = c(
        "custID" = "integer", "gender" = "integer", "state" = "integer",
        "cardholder" = "integer", "balance" = "integer",
        "numTrans" = "integer",
        "numIntlTrans" = "integer", "creditLine" = "integer",
        "fraudRisk" = "integer"))
    ```
  
    El argumento *colClasses* es importante. Se usa para indicar el tipo de datos para asignar a cada columna de datos cargada desde el archivo de texto. En este ejemplo, todas las columnas se tratan como texto, excepto las columnas con nombre, que se tratan como enteros.
  
3. En este momento, es posible que desee pausar un momento y ver la base de datos en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Actualice la lista de tablas de la base de datos.
  
    Puede ver que, aunque se crearon los objetos de datos de R en el área de trabajo local, las tablas no se han creado en el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] base de datos. Además, no hay datos se ha cargado desde el archivo de texto en la variable de R.
  
4. Insertar los datos mediante una llamada a la función [rxDataStep](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdatastep) función.
  
    ```R
    rxDataStep(inData = inTextData, outFile = sqlFraudDS, overwrite = TRUE)
    ```
    
    Suponiendo que no existen problemas con su cadena de conexión, después de una breve pausa, debería ver resultados como estos:
  
    *Total de filas escritas: 10000, tiempo total: 0,466* *filas leídas: 10 000, filas procesadas: 10000, tiempo total de fragmentos: 0,577 segundos*
  
5. Actualice la lista de tablas. Para comprobar que cada variable tiene los tipos de datos correcto y que se importó correctamente, también puede haga clic en la tabla de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] y seleccione **seleccionar 1000 filas superiores**.

### <a name="load-data-into-the-scoring-table"></a>Cargar datos en la tabla de puntuación

1. Repita los pasos para cargar el conjunto de datos usado para la puntuación en la base de datos.
  
    Primero proporcione la ruta de acceso al archivo de origen.
  
    ```R
    ccScoreCsv <- file.path(rxGetOption("sampleDataDir"), "ccFraudScoreSmall.csv")
    ```
  
2. Use la función **RxTextData** para obtener los datos y guardarlos en la variable *inTextData*.
  
    ```R
    inTextData <- RxTextData(file = ccScoreCsv,      colClasses = c(
        "custID" = "integer", "gender" = "integer", "state" = "integer",
        "cardholder" = "integer", "balance" = "integer",
        "numTrans" = "integer",
        "numIntlTrans" = "integer", "creditLine" = "integer"))
    ```
  
3.  Llame a la función **rxDataStep** para sobrescribir la tabla actual con el nuevo esquema y los datos.
  
    ```R
    rxDataStep(inData = inTextData, sqlScoreDS, overwrite = TRUE)
    ```
  
    - El argumento *inData* define el origen de datos que usar.
  
    - El argumento *outFile* especifica la tabla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] donde quiere guardar los datos.
  
    - Si la tabla ya existe y no usa el *sobrescribir* opción, los resultados se insertarán sin truncamiento.
  
De nuevo, si la conexión se ha realizado correctamente, debería ver un mensaje indicando la finalización y el tiempo requerido para escribir los datos en la tabla:

*Total de filas escritas: 10000, tiempo total: 0,384*
*filas leídas: 10 000, filas procesadas: 10000, tiempo total de fragmentos: 0,456 segundos*

## <a name="more-about-rxdatastep"></a>Más información sobre rxDataStep

[rxDataStep](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdatastep) es una función muy eficaz que puede realizar varias transformaciones en una trama de datos de R. También puede usar rxDataStep para convertir datos en la representación requerida por el destino: en este caso, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].

Si lo desea, puede especificar las transformaciones en los datos, mediante el uso de funciones de R en los argumentos de **rxDataStep**. Más adelante en este tutorial se proporcionan ejemplos de estas operaciones.

## <a name="next-steps"></a>Pasos siguientes

> [!div class="nextstepaction"]
> [Consultar y modificar los datos de SQL Server](../../advanced-analytics/tutorials/deepdive-query-and-modify-the-sql-server-data.md)