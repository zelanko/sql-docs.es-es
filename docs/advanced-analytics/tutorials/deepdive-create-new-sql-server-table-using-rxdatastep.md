---
title: Crear una nueva tabla de SQL Server con RevoScaleR rxDataStep
description: Tutorial sobre cómo crear una tabla de SQL Server mediante el lenguaje R en SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.openlocfilehash: 5f5d65bf3b57f40ca881aa9e6f0285fab0432a1e
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/19/2019
ms.locfileid: "68344793"
---
# <a name="create-new-sql-server-table-using-rxdatastep-sql-server-and-revoscaler-tutorial"></a>Creación de una nueva tabla de SQL Server con rxDataStep (tutorial de SQL Server y RevoScaleR)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Esta lección forma parte del [tutorial de RevoScaleR](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md) sobre cómo usar [las funciones de RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) con SQL Server.

En esta lección, aprenderá a trasladar datos entre tramas de datos en memoria, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] el contexto y archivos locales.

> [!NOTE]
> En esta lección se usa un conjunto de datos diferente. El conjunto de los retrasos de la línea aérea es un conjunto de información público que se usa ampliamente para los experimentos de aprendizaje automático. Los archivos de datos que se usan en este ejemplo están disponibles en el mismo directorio que otros ejemplos de productos.

## <a name="load-data-from-a-local-xdf-file"></a>Carga de datos desde un archivo XDF local

En la primera mitad de este tutorial, ha usado la función **RxTextData** para importar datos en R desde un archivo de texto y, a continuación, ha usado la función **RxDataStep** para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]trasladar los datos a.

En esta lección adopta un enfoque diferente y usa datos desde un archivo guardan en el [formato xdf](https://en.wikipedia.org/wiki/Extensible_Data_Format). Después de realizar algunas transformaciones ligeras en los datos con el archivo XDF, guarde los datos transformados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en una nueva tabla.

**¿Qué es XDF?**

El formato XDF es un estándar XML desarrollado para datos de gran dimensionalidad y es el formato de archivo nativo que usa [machine learning Server](https://docs.microsoft.com/machine-learning-server/r/concept-what-is-xdf). Es un formato de archivo binario con una interfaz de R que optimiza el análisis y el procesamiento de columnas y filas.  Puede usarlo para mover datos y almacenar los subconjuntos de datos que son útiles para el análisis.

1. Establezca el contexto de cálculo en la estación de trabajo local. **Se necesitan permisos DDL para este paso.**

    ```R
    rxSetComputeContext("local")
    ```
  
2. Defina un nuevo objeto de origen de datos mediante la función **RxXdfData** . Para definir un origen de datos de XDF, especifique la ruta de acceso al archivo de datos.  

    Puede especificar la ruta de acceso al archivo mediante una variable de texto. Sin embargo, en este caso, hay un método abreviado útil, que consiste en usar la función **rxGetOption** y obtener el archivo (AirlineDemoSmall. xdf) del directorio de datos de ejemplo.
  
    ```R
    xdfAirDemo <- RxXdfData(file.path(rxGetOption("sampleDataDir"),  "AirlineDemoSmall.xdf"))
    ```

3. Llame a [rxGetVarInfo](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxgetvarinfoxdf) en los datos en memoria para ver un resumen del conjunto de datos.
  
    ```R
    rxGetVarInfo(xdfAirDemo)
    ```

**Resultado**

```R
Var 1: ArrDelay, Type: integer, Low/High: (-86, 1490)
Var 2: CRSDepTime, Type: numeric, Storage: float32, Low/High: (0.0167, 23.9833)
Var 3: DayOfWeek 7 factor levels: Monday Tuesday Wednesday Thursday Friday Saturday Sunday
```

> [!NOTE]
> 
> ¿Se ha dado cuenta de que no necesita llamar a ninguna función para cargar los datos en el archivo XDF y puede llamar a **rxGetVarInfo** en los datos inmediatamente? Esto se debe a que XDF es el método de almacenamiento provisional predeterminado para **RevoScaleR**. Además de los archivos XDF, la función **rxGetVarInfo** admite ahora varios tipos de orígenes.

## <a name="move-contents-to-sql-server"></a>Mueva el contenido a SQL Server

Con el origen de datos XDF creado en la sesión local de R, ahora puede trasladar estos datos a una tabla de base de datos, almacenando *DayOfWeek* como un entero con valores de 1 a 7.

1. Defina un SQL Server objeto de origen de datos, especificando una tabla que contenga los datos y la conexión al servidor remoto.
  
    ```R
    sqlServerAirDemo <- RxSqlServerData(table = "AirDemoSmallTest", connectionString = sqlConnString)
    ```
  
2. Como medida de precaución, incluya un paso que compruebe si ya existe una tabla con el mismo nombre y elimine la tabla si existe. Una tabla existente con el mismo nombre evita que se cree una nueva.
  
    ```R
    if (rxSqlServerTableExists("AirDemoSmallTest",  connectionString = sqlConnString))  rxSqlServerDropTable("AirDemoSmallTest",  connectionString = sqlConnString)
    ```
  
3. Cargue los datos en la tabla mediante **rxDataStep**. Esta función mueve los datos entre dos orígenes de datos ya definidos y, opcionalmente, puede transformar los datos en la ruta.
  
    ```R
    rxDataStep(inData = xdfAirDemo, outFile = sqlServerAirDemo,
        transforms = list( DayOfWeek = as.integer(DayOfWeek),
        rowNum = .rxStartRow : (.rxStartRow + .rxNumRows - 1) ),
        overwrite = TRUE )
    ```
  
    Se trata de una tabla bastante grande, por lo que debe esperar hasta que vea un mensaje de estado final como este: *Filas leídas: 200000, total de filas procesadas: 600000*.
     
## <a name="load-data-from-a-sql-table"></a>Carga de datos de una tabla SQL

Una vez que los datos existen en la tabla, puede cargarlos mediante una consulta SQL simple. 

1. Cree un nuevo origen de datos de SQL Server. La entrada es una consulta en la nueva tabla que acaba de crear y se cargó con los datos. Esta definición agrega niveles de factor para la columna *DayOfWeek* mediante el argumento *colInfo* a **RxSqlServerData**.
  
    ```R
    sqlServerAirDemo2 <- RxSqlServerData(
        sqlQuery = "SELECT * FROM AirDemoSmallTest",
        connectionString = sqlConnString,
        rowsPerRead = 50000,
        colInfo = list(DayOfWeek = list(type = "factor",  levels = as.character(1:7))))
    ```
  
2. Llame a **rxSummary** una vez más para revisar un resumen de los datos de la consulta.
  
    ```R
    rxSummary(~., data = sqlServerAirDemo2)
    ```

## <a name="next-steps"></a>Pasos siguientes

> [!div class="nextstepaction"]
> [Realizar análisis de fragmentación mediante rxDataStep](../../advanced-analytics/tutorials/deepdive-perform-chunking-analysis-using-rxdatastep.md)