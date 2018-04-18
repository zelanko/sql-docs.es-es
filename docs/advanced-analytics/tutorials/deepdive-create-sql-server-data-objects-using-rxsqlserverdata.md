---
title: Crear objetos de datos de SQL Server mediante RxSqlServerData (SQL y R profundización) | Documentos de Microsoft
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: e15c3e7c13c1be4f524c25bb1cec6da3c8e20c7e
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="create-sql-server-data-objects-using-rxsqlserverdata-sql-and-r-deep-dive"></a>Crear objetos de datos de SQL Server mediante RxSqlServerData (SQL y R profundización)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Este artículo forma parte del tutorial exhaustiva de ciencia de datos, acerca de cómo usar [RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) con SQL Server.

Hasta ahora ha creado el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] la base de datos y tiene los permisos necesarios para trabajar con los datos. En este paso, creará algunos objetos de R que le permiten trabajar con los datos.

## <a name="create-the-sql-server-data-objects"></a>Crear los objetos de datos de SQL Server

En este paso, utilice las funciones de la **RevoScaleR** paquete para crear y rellenar dos tablas. Una tabla se usa para entrenar los modelos y la otra para la puntuación. Ambas tablas contienen datos de fraude de tarjeta de crédito simulados.

Para crear tablas en el servidor remoto [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] equipo, llame a la **RxSqlServerData** (función).

> [!TIP]
> Si está usando R Tools para Visual Studio, seleccione **R Tools** en la barra de herramientas y haga clic en **Windows** para ver las opciones de depuración y ver las variables de R.

### <a name="create-the-training-data-table"></a>Crear la tabla de datos de entrenamiento

1. Guardar la cadena de conexión de base de datos en una variable de R. Dos ejemplos de cadenas de conexión ODBC válidas para SQL Server: uno con un inicio de sesión SQL y otro para la autenticación integrada de Windows.

    **Inicio de sesión de SQL**
    ```R
    sqlConnString <- "Driver=SQL Server;Server=instance_name; Database=DeepDive;Uid=user_name;Pwd=password"
    ```

    **Autenticación de Windows**
    ```R
    sqlConnString <- "Driver=SQL Server;Server=instance_name;Database=DeepDive;Trusted_Connection=True"
    ```

    Asegúrese de modificar el nombre de instancia, el nombre de la base de datos, el nombre de usuario y la contraseña según corresponda.
  
2. Especifique el nombre de la tabla que quiere crear y guárdelo en una variable de R.
  
    ```R
    sqlFraudTable <- "ccFraudSmall"
    ```
  
    Como la instancia y el nombre de la base de datos ya se han especificado como parte de la cadena de conexión, cuando se combinan las dos variables, el nombre *completo* de la nueva tabla se convierte en _instance.database.schema.ccFraudSmall_.
  
3.  Antes de crear instancias del objeto de origen de datos, agregue una línea que especifica un parámetro adicional, *rowsPerRead*.  El parámetro *rowsPerRead* controla cuántas filas de datos se leen en cada lote.
  
    ```R
    sqlRowsPerRead = 5000
    ```
  
    Aunque este parámetro es opcional, es importante para controlar el uso de memoria y cálculos eficaces.  La mayoría de las funciones analíticas mejoradas de [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] procesar datos en fragmentos y almacenar resultados intermedios, devolver los cálculos finales después de que todos los datos se ha leído.
  
    Si el valor de este parámetro es demasiado grande, es posible que el acceso a los datos sea lento porque no tiene suficiente memoria para procesar de forma eficaz un fragmento de datos tan grande.  En algunos sistemas, si el valor de *rowsPerRead* es demasiado pequeño, el rendimiento puede ser más lento. Por lo tanto, se recomienda que experimente con esta configuración en el sistema cuando se trabaja con un gran conjunto de datos.
  
    Para este tutorial, utilice el tamaño predeterminado del proceso de lote definido por el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instancia para controlar el número de filas de cada fragmento. Guardar dicho valor en la variable `sqlRowsPerRead`.
  
4.  Por último, defina una variable para el nuevo objeto de origen de datos y pasar los argumentos definidos anteriormente al constructor RxSqlServerData. Tenga en cuenta que esto solo crea el objeto de origen de datos y no lo rellena.
  
    ```R
    sqlFraudDS <- RxSqlServerData(connectionString = sqlConnString,
       table = sqlFraudTable,
       rowsPerRead = sqlRowsPerRead)
    ```

#### <a name="to-create-the-scoring-data-table"></a>Para crear la tabla de datos de puntuación

Con los mismos pasos, cree la tabla que contiene los datos de puntuación mediante el mismo proceso.

1. Cree una nueva variable de R, *sqlScoreTable*, para almacenar el nombre de la tabla usada para la puntuación.
  
    ```R
    sqlScoreTable <- "ccFraudScoreSmall"
    ```
  
2. Proporcionar esa variable como argumento a la función RxSqlServerData para definir un segundo objeto de origen de datos, *sqlScoreDS*.
  
    ```R
    sqlScoreDS \<- RxSqlServerData(connectionString = sqlConnString,
       table = sqlScoreTable, rowsPerRead = sqlRowsPerRead)
    ```

Dado que ya se ha definido la cadena de conexión y otros parámetros como variables en el área de trabajo de R, es fácil crear nuevos orígenes de datos de distintas tablas, vistas o consultas.

> [!NOTE]
> La función utiliza argumentos distintos para definir un origen de datos basado en una tabla completa que para un origen de datos basado en una consulta. Esto es porque el motor de base de datos de SQL Server debe preparar las consultas de forma diferente. Más adelante en este tutorial, aprenderá a crear un objeto de origen de datos basado en una consulta SQL.

## <a name="load-data-into-sql-tables-using-r"></a>Cargar datos en las tablas SQL mediante R

Ahora que ha creado las tablas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , puede cargar los datos en ellas mediante la correspondiente función **Rx** .

El **RevoScaleR** paquete contiene funciones que admiten muchos orígenes de datos diferentes: para datos de texto, utilice [RxTextData](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxtextdata) para generar el objeto de origen de datos. Existen funciones adicionales para crear objetos de origen de datos a partir de datos de Hadoop, datos ODBC y así sucesivamente.

> [!NOTE]
> Para esta sección, debe tener **Ejecutar DDL** permisos en la base de datos.

### <a name="load-data-into-the-training-table"></a>Cargar datos en la tabla de entrenamiento

1. Cree una variable de R, *ccFraudCsv*y asignar a la variable de la ruta de acceso de archivo para el archivo CSV que contiene los datos de ejemplo.
  
    ```R
    ccFraudCsv <- file.path(rxGetOption("sampleDataDir"), "ccFraudSmall.csv")
    ```
  
    Observe la llamada a **rxGetOption**, que es el método GET asociado [rxOptions](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxoptions) en **RevoScaleR**. Use esta utilidad para establecer y opciones de lista relacionados con contextos de proceso locales y remotos, como el directorio compartido predeterminado o el número de procesadores (núcleos) que se usarán en los cálculos.
    
    Esta llamada determinada obtiene los ejemplos de la biblioteca correcta, independientemente de donde se ejecuta el código. Por ejemplo, pruebe a ejecutar la función en SQL Server y en su equipo de desarrollo para ver cómo difieren las rutas de acceso.
  
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
  
3. En este momento, puede pausar un momento y ver la base de datos en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  Actualice la lista de tablas de la base de datos.
  
    Puede ver que, aunque los objetos de datos de R se ha creado en el área de trabajo local, las tablas no se crearon en el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] base de datos. Además, no hay datos se ha cargado desde el archivo de texto en la variable de R.
  
4. Ahora, llame a la función [rxDataStep](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdatastep) para insertar los datos en la tabla [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .
  
    ```R
    rxDataStep(inData = inTextData, outFile = sqlFraudDS, overwrite = TRUE)
    ```
  
    Suponiendo que no existen problemas con su cadena de conexión, después de una breve pausa, debería ver resultados como estos:
  
      *Total de filas escritas: 10 000, tiempo total: 0,466*

      *Filas leídas: 10 000, total de filas procesadas: 10 000, tiempo total de fragmentos: 0,577 segundos*
  
5. Por medio de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], actualice la lista de tablas. Para comprobar que cada variable tiene los tipos de datos correcto y se importó correctamente, también puede hacer clic en la tabla en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] y seleccione **seleccionar 1000 filas superiores**.

### <a name="load-data-into-the-scoring-table"></a>Cargar datos en la tabla de puntuación

1. Repita los pasos para cargar el conjunto de datos usado para puntuar en la base de datos.
  
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
  
    - Si la tabla ya existe y no se utiliza la *sobrescribir* opción, se insertan los resultados sin truncamiento.
  
De nuevo, si la conexión se ha realizado correctamente, debería ver un mensaje indicando la finalización y el tiempo requerido para escribir los datos en la tabla:

*Total de filas escritas: 10000, tiempo total: 0,384*

*Filas leídas: 10000, total de filas procesadas: 10000, tiempo total de fragmentos: 0,456 segundos*

## <a name="more-about-rxdatastep"></a>Más información sobre rxDataStep

[rxDataStep](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdatastep) es una función eficaz que puede realizar varias transformaciones en una trama de datos de R. También puede utilizar rxDataStep para convertir los datos en la representación requerida el destino: en este caso, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].

Si lo desea, puede especificar las transformaciones en los datos, mediante el uso de funciones de R en los argumentos de **rxDataStep**. Más adelante en este tutorial se proporcionan ejemplos de estas operaciones.

## <a name="next-step"></a>Paso siguiente

[Consultar y modificar los datos de SQL Server](../../advanced-analytics/tutorials/deepdive-query-and-modify-the-sql-server-data.md)

## <a name="previous-step"></a>Paso anterior

[Trabajar con datos de SQL Server con R](../../advanced-analytics/tutorials/deepdive-work-with-sql-server-data-using-r.md)
