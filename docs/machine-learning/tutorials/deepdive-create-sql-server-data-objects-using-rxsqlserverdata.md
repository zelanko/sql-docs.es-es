---
title: Creación de objetos RxSqlServerData
description: 'Aprenda a usar las funciones de RevoScaleR con SQL Server. Este tutorial es una continuación de la creación de bases de datos: agregar tablas y cargar datos.'
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 11/26/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 664deeae61b664d3818f7d748ad6177b79917d86
ms.sourcegitcommit: 9b41725d6db9957dd7928a3620fe4db41eb51c6e
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/13/2020
ms.locfileid: "88178812"
---
# <a name="create-sql-server-data-objects-using-rxsqlserverdata-sql-server-and-revoscaler-tutorial"></a>Creación de objetos de datos de SQL Server con RxSqlServerData (tutorial de SQL Server y RevoScaleR)
[!INCLUDE [SQL Server 2016 and later](../../includes/applies-to-version/sqlserver2016.md)]

Este es el tutorial 2 de la [serie de tutoriales de RevoScaleR](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md) sobre el uso de las [funciones de RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) con SQL Server.

Este tutorial es una continuación de la creación de bases de datos: agregar tablas y cargar datos. Si un administrador de base de datos (DBA) ha creado la base de datos e inicia sesión en el [tutorial dos](deepdive-work-with-sql-server-data-using-r.md), puede agregar tablas mediante un IDE de R como RStudio o una herramienta integrada como **Rgui**.

Desde R, conéctese a SQL Server y use las funciones de **RevoScaleR** para realizar las tareas siguientes:

> [!div class="checklist"]
> * Creación de tablas para los datos de entrenamiento y las predicciones
> * Carga de tablas con datos de un archivo .csv local

Los datos de ejemplo son datos simulados de fraude de tarjetas de crédito (el conjunto de datos ccFraud), particionados en conjuntos de datos de entrenamiento y puntuación. El archivo de datos se incluye en **RevoScaleR**.

Use un IDE de R o **Rgui** para completar estas tareas. Asegúrese de usar los ejecutables de R que se encuentran en esta ubicación: C:\Archivos de programa\Microsoft\R Client\R_SERVER\bin\x64 (Rgui.exe si usa esa herramienta o un IDE de R que apunte a C:\Archivos de programa\Microsoft\R Client\R_SERVER). Disponer de una [estación de trabajo de cliente de R](../r/set-up-a-data-science-client.md) con estos ejecutables se considera un requisito previo de este tutorial.

## <a name="create-the-training-data-table"></a>Creación de la tabla de datos de entrenamiento

1. Almacene la cadena de conexión de base de datos en una variable de R. Aquí se ofrecen dos ejemplos de cadenas de conexión ODBC válidas para SQL Server: una que usa un inicio de sesión de SQL y otra para la autenticación integrada de Windows. 

   Asegúrese de modificar el nombre del servidor, el nombre de usuario y la contraseña según corresponda.

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
  
    Como la instancia del servidor y el nombre de la base de datos ya se han especificado como parte de la cadena de conexión, cuando se combinan las dos variables, el nombre *completo* de la nueva tabla se convierte en *instance.database.schema.ccFraudSmall*.
  
3.  Opcionalmente, especifique el parámetro *rowsPerRead* para controlar cuántas filas de datos se leen en cada lote.
  
    ```R
    sqlRowsPerRead = 5000
    ```
  
    Aunque este parámetro es opcional, su configuración puede traducirse en cálculos más eficientes. La mayoría de las funciones analíticas mejoradas en **RevoScaleR** y **MicrosoftML** procesan los datos en fragmentos. El parámetro *rowsPerRead* determina el número de filas de cada fragmento.
  
    Es posible que tenga que experimentar con esta configuración para encontrar el equilibrio adecuado. Si el valor es demasiado grande, puede que el acceso a los datos sea lento cuando no haya memoria suficiente para procesar los datos en fragmentos de ese tamaño. Por el contrario, en algunos sistemas, si el valor de *rowsPerRead* es demasiado pequeño, el rendimiento también puede disminuir.
  
    Como valor inicial, utilice el tamaño predeterminado de proceso por lotes definido por la instancia del motor de base de datos para controlar el número de filas de cada fragmento (5000 filas). Guarde el valor en la variable *sqlRowsPerRead*.
  
4.  Defina una variable para el nuevo objeto de origen de datos y pase los argumentos definidos previamente al constructor **RxSqlServerData**. Tenga en cuenta que esto solo crea el objeto de origen de datos y no lo rellena. La carga de datos es un paso independiente.
  
    ```R
    sqlFraudDS <- RxSqlServerData(connectionString = sqlConnString,
       table = sqlFraudTable,
       rowsPerRead = sqlRowsPerRead)
    ```

## <a name="create-the-scoring-data-table"></a>Creación de la tabla de datos de puntuación

Siguiendo los mismos pasos, cree la tabla que contiene los datos de puntuación con el mismo proceso.

1. Cree una nueva variable de R, *sqlScoreTable*, para almacenar el nombre de la tabla usada para la puntuación.
  
    ```R
    sqlScoreTable <- "ccFraudScoreSmall"
    ```
  
2. Proporcione esa variable como argumento a la función **RxSqlServerData** para definir un segundo objeto de origen de datos, *sqlScoreDS*.
  
    ```R
    sqlScoreDS <- RxSqlServerData(connectionString = sqlConnString,
       table = sqlScoreTable, rowsPerRead = sqlRowsPerRead)
    ```

Como ya se ha definido la cadena de conexión y otros parámetros como variables en el área de trabajo de R, se puede reutilizar con nuevos orígenes de datos que representen diferentes tablas, vistas o consultas.

> [!NOTE]
> La función utiliza distintos argumentos para definir un origen de datos en función de una tabla completa que para definir un origen de datos en función de una consulta. Esto se debe a que el motor de base de datos de SQL Server debe preparar las consultas de manera diferente. Más adelante en este tutorial aprenderá a crear un objeto de origen de datos en función de una consulta SQL.

## <a name="load-data-into-sql-tables-using-r"></a>Carga de datos en tablas de SQL con R

Ahora que ha creado las tablas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , puede cargar los datos en ellas mediante la correspondiente función **Rx** .

El paquete **RevoScaleR** contiene funciones específicas de los tipos de orígenes de datos. Con datos de texto, utilice [RxTextData](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxtextdata) para generar el objeto de origen de datos. Existen funciones adicionales para crear objetos de origen de datos a partir de datos de Hadoop, datos ODBC y así sucesivamente.

> [!NOTE]
> En esta sección, debe tener permisos para **Ejecutar DDL** en la base de datos.

### <a name="load-data-into-the-training-table"></a>Carga de datos en la tabla de entrenamiento

1. Cree una variable de R, *ccFraudCsv*, y asígnele la ruta de acceso del archivo CSV que contiene los datos de ejemplo. Este conjunto de datos se proporciona en **RevoScaleR**. "sampleDataDir" es una palabra clave en la función **rxGetOption**.
  
    ```R
    ccFraudCsv <- file.path(rxGetOption("sampleDataDir"), "ccFraudSmall.csv")
    ```
  
    Observe la llamada a **rxGetOption**, que es el método GET asociado a [rxOptions](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxoptions) en **RevoScaleR**. Use esta utilidad para establecer y mostrar opciones relacionadas con contextos de proceso locales y remotos, como el directorio compartido predeterminado o el número de procesadores (núcleos) que se utilizarán en los cálculos.
    
    Esta llamada en particular obtiene los ejemplos de la biblioteca correcta, independientemente de dónde se ejecute el código. Por ejemplo, pruebe a ejecutar la función en SQL Server y en su equipo de desarrollo para ver cómo difieren las rutas de acceso.
  
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
  
3. Llegados a este punto, tal vez quiera hacer una pausa y ver la base de datos en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Actualice la lista de tablas de la base de datos.
  
    Puede ver que, aunque los objetos de datos de R se han creado en el área de trabajo local, las tablas no se han creado en la base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Además, tampoco se ha cargado ningún dato del archivo de texto en la variable de R.
  
4. Inserte los datos llamando a la función [rxDataStep](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdatastep).
  
    ```R
    rxDataStep(inData = inTextData, outFile = sqlFraudDS, overwrite = TRUE)
    ```
    
    Suponiendo que no existen problemas con su cadena de conexión, después de una breve pausa, debería ver resultados como estos:
  
    *Total de filas escritas: 10 000, tiempo total: 0,466* *Filas leídas: 10 000, total de filas procesadas: 10 000, tiempo total de fragmentos: 0,577 segundos*
  
5. Actualice la lista de tablas. Para comprobar que cada variable tiene los tipos de datos correctos y que se ha importado correctamente, también puede hacer clic con el botón derecho en la tabla en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] y elegir **Seleccionar las 1000 primeras filas**.

### <a name="load-data-into-the-scoring-table"></a>Carga de datos en la tabla de puntuación

1. Repita los pasos necesarios para cargar en la base de datos el conjunto de datos usado para puntuación.
  
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
  
    - Si la tabla ya existe y no se usa la opción *sobrescribir*, los resultados se insertarán sin truncamiento.
  
De nuevo, si la conexión se ha realizado correctamente, debería ver un mensaje indicando la finalización y el tiempo requerido para escribir los datos en la tabla:

*Total de filas escritas: 10 000, Tiempo total: 0,384*
*Filas leídas: 10 000, Total de filas procesadas: 10 000, Tiempo total de fragmentos: 0,456 segundos*

## <a name="more-about-rxdatastep"></a>Más información sobre rxDataStep

[rxDataStep](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdatastep) es una función eficaz que puede realizar varias transformaciones en una trama de datos de R. También puede usar rxDataStep para convertir los datos en la representación requerida por el destino: en este caso, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].

Opcionalmente, puede especificar transformaciones en los datos mediante funciones de R en los argumentos para **rxDataStep**. Más adelante en este tutorial se ofrecen ejemplos de estas operaciones.

## <a name="next-steps"></a>Pasos siguientes

> [!div class="nextstepaction"]
> [Consultar y modificar los datos de SQL Server](../../machine-learning/tutorials/deepdive-query-and-modify-the-sql-server-data.md)