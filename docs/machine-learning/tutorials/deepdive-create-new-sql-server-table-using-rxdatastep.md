---
title: Creación de una tabla mediante rxDataStep
description: 'Tutorial 11 de RevoScaleR: Creación de una tabla de SQL Server usando el lenguaje R en SQL Server.'
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 11144b95eb22cac9991fcf0f5eb60821ac730f89
ms.sourcegitcommit: 68583d986ff5539fed73eacb7b2586a71c37b1fa
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/04/2020
ms.locfileid: "81116958"
---
# <a name="create-new-sql-server-table-using-rxdatastep-sql-server-and-revoscaler-tutorial"></a>Creación de una tabla de SQL Server con rxDataStep (tutorial de SQL Server y RevoScaleR)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Este es el tutorial 11 de la [serie de tutoriales de RevoScaleR](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md) sobre el uso de las [funciones de RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) con SQL Server.

En este tutorial, aprenderá a mover datos entre las tramas de datos en memoria, el contexto de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y archivos locales.

> [!NOTE]
> En este tutorial se usa un conjunto de datos diferente. El conjunto de datos Airline Delays es un conjunto de datos público que se usa profusamente en los experimentos de Machine Learning. Los archivos de datos que se usan en este ejemplo están disponibles en el mismo directorio que otros ejemplos de producto.

## <a name="load-data-from-a-local-xdf-file"></a>Carga de datos desde un archivo XDF local

En la primera parte de esta serie de tutoriales, usó la función **RxTextData** para importar datos en R de un archivo de texto y, después, la función **RxDataStep** para mover los datos a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].

En este tutorial se usa un enfoque diferente, y se usan datos de un archivo guardado en [formato XDF](https://en.wikipedia.org/wiki/Extensible_Data_Format). Después de realizar algunas transformaciones ligeras en los datos mediante el archivo XDF, los datos transformados se guardan en una nueva tabla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].

**¿Qué es XDF?**

El formato XDF es un estándar XML desarrollado para datos de gran dimensionalidad, y es el formato de archivo nativo que [Machine Learning Server](https://docs.microsoft.com/machine-learning-server/r/concept-what-is-xdf) usa. Es un formato de archivo binario con una interfaz de R que optimiza el análisis y el procesamiento de columnas y filas.  Puede usarlo para mover datos y almacenar los subconjuntos de datos que son útiles para el análisis.

1. Establezca el contexto de cálculo en la estación de trabajo local. **En este paso se necesitan permisos DDL.**

    ```R
    rxSetComputeContext("local")
    ```
  
2. Defina un nuevo objeto de origen de datos mediante la función **RxXdfData** . Para definir un origen de datos XDF, especifique la ruta de acceso al archivo de datos.  

    La ruta de acceso al archivo podría especificarse con una variable de texto, pero en este caso existe un método abreviado útil, que consiste en usar la función **rxGetOption** y obtener el archivo (AirlineDemoSmall.xdf) del directorio de datos de ejemplo.
  
    ```R
    xdfAirDemo <- RxXdfData(file.path(rxGetOption("sampleDataDir"),  "AirlineDemoSmall.xdf"))
    ```

3. Llame a [rxGetVarInfo](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxgetvarinfoxdf) en los datos en memoria para ver un resumen del conjunto de datos.
  
    ```R
    rxGetVarInfo(xdfAirDemo)
    ```

**Resultados**

```R
Var 1: ArrDelay, Type: integer, Low/High: (-86, 1490)
Var 2: CRSDepTime, Type: numeric, Storage: float32, Low/High: (0.0167, 23.9833)
Var 3: DayOfWeek 7 factor levels: Monday Tuesday Wednesday Thursday Friday Saturday Sunday
```

> [!NOTE]
> 
> ¿Se ha dado cuenta de que no necesita llamar a ninguna función para cargar los datos en el archivo XDF y puede llamar a **rxGetVarInfo** en los datos inmediatamente? Eso es porque XDF es el método de almacenamiento provisional predeterminado en **RevoScaleR**. Además de los archivos XDF, ahora la función **rxGetVarInfo** admite varios tipos de orígenes.

## <a name="move-contents-to-sql-server"></a>Traslado del contenido a SQL Server

Con el origen de datos XDF creado en la sesión de R local, ahora puede pasar estos datos a una tabla de base de datos y almacenar *DayOfWeek* como un entero con valores de 1 a 7.

1. Defina un objeto de origen de datos de SQL Server, especificando una tabla que contenga los datos y la conexión al servidor remoto.
  
    ```R
    sqlServerAirDemo <- RxSqlServerData(table = "AirDemoSmallTest", connectionString = sqlConnString)
    ```
  
2. Como medida de precaución, incluya un paso que compruebe si ya existe una tabla con el mismo nombre y elimínela en caso de que exista. Una tabla existente con el mismo nombre evitará que se cree una nueva.
  
    ```R
    if (rxSqlServerTableExists("AirDemoSmallTest",  connectionString = sqlConnString))  rxSqlServerDropTable("AirDemoSmallTest",  connectionString = sqlConnString)
    ```
  
3. Cargue los datos en la tabla mediante **rxDataStep**. Esta función mueve los datos entre dos orígenes de datos ya definidos y, opcionalmente, puede transformar los datos en tránsito.
  
    ```R
    rxDataStep(inData = xdfAirDemo, outFile = sqlServerAirDemo,
        transforms = list( DayOfWeek = as.integer(DayOfWeek),
        rowNum = .rxStartRow : (.rxStartRow + .rxNumRows - 1) ),
        overwrite = TRUE )
    ```
  
    Se trata de una tabla bastante grande, por lo que debe esperar hasta que vea un mensaje de estado final como este: *Filas leídas: 200000, Total de filas procesadas: 600000*.
     
## <a name="load-data-from-a-sql-table"></a>Carga de datos desde una tabla SQL

Una vez que los datos existen en la tabla, puede cargarlos usando una sencilla consulta SQL. 

1. Cree un origen de datos de SQL Server. La entrada es una consulta sobre la nueva tabla que acaba de crear y cargar con los datos. Esta definición agrega niveles de factor para la columna *DayOfWeek* mediante el argumento *colInfo* en **RxSqlServerData**.
  
    ```R
    sqlServerAirDemo2 <- RxSqlServerData(
        sqlQuery = "SELECT * FROM AirDemoSmallTest",
        connectionString = sqlConnString,
        rowsPerRead = 50000,
        colInfo = list(DayOfWeek = list(type = "factor",  levels = as.character(1:7))))
    ```
  
2. Llame a **rxSummary** otra vez para revisar un resumen de los datos de la consulta.
  
    ```R
    rxSummary(~., data = sqlServerAirDemo2)
    ```

## <a name="next-steps"></a>Pasos siguientes

> [!div class="nextstepaction"]
> [Realizar análisis de fragmentación mediante rxDataStep](../../machine-learning/tutorials/deepdive-perform-chunking-analysis-using-rxdatastep.md)