---
title: 'Crear nueva tabla de SQL Server mediante rxDataStep RevoScaleR: SQL Server Machine Learning'
description: Tutorial del tutorial sobre cómo crear una tabla de SQL Server usando el lenguaje R en SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 1fb3f83cd3bbd39e3af4936ce8dfb8f16bad82d8
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62641462"
---
# <a name="create-new-sql-server-table-using-rxdatastep-sql-server-and-revoscaler-tutorial"></a>Crear nueva tabla de SQL Server mediante rxDataStep (tutorial de SQL Server y RevoScaleR)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

En esta lección forma parte de la [RevoScaleR tutorial](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md) sobre cómo usar [funciones de RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) con SQL Server.

En esta lección, obtendrá información sobre cómo mover datos entre las tramas de datos en memoria, el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] contexto y los archivos locales.

> [!NOTE]
> En esta lección se usa un conjunto de datos diferente. El conjunto de datos de retrasos de aerolíneas es un conjunto de datos público que se usa ampliamente para los experimentos de aprendizaje automático. En este ejemplo utilizados los archivos de datos están disponibles en el mismo directorio que otros ejemplos de producto.

## <a name="load-data-from-a-local-xdf-file"></a>Cargar datos desde un archivo XDF local

En la primera mitad de este tutorial, ha utilizado el **RxTextData** de función para importar datos en R desde un archivo de texto y, a continuación, usar el **RxDataStep** función para mover los datos a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].

En esta lección adopta un enfoque diferente y usa datos desde un archivo guardan en el [formato xdf](https://en.wikipedia.org/wiki/Extensible_Data_Format). Después de realizar algunas transformaciones ligeras en los datos mediante el archivo XDF, guardar los datos transformados en un nuevo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tabla.

**¿Qué es XDF?**

El formato XDF es un estándar XML desarrollado para datos de dimensiones elevadas y está usando el formato de archivo nativo [Machine Learning Server](https://docs.microsoft.com/machine-learning-server/r/concept-what-is-xdf). Es un formato de archivo binario con una interfaz de R que optimiza el análisis y el procesamiento de columnas y filas.  Puede usarlo para mover datos y almacenar los subconjuntos de datos que son útiles para el análisis.

1. Establezca el contexto de cálculo en la estación de trabajo local. **En este paso, se necesitan permisos de DDL.**

    ```R
    rxSetComputeContext("local")
    ```
  
2. Defina un nuevo objeto de origen de datos mediante la función **RxXdfData** . Para definir un origen de datos XDF, especifique la ruta de acceso al archivo de datos.  

    Puede especificar la ruta de acceso al archivo mediante una variable de texto. Sin embargo, en este caso, hay un método abreviado muy útil, que consiste en usar el **rxGetOption** funcionan y obtener el archivo (AirlineDemoSmall.xdf) desde el directorio de datos de ejemplo.
  
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
> ¿Se ha dado cuenta de que no necesita llamar a ninguna función para cargar los datos en el archivo XDF y puede llamar a **rxGetVarInfo** en los datos inmediatamente? Eso es porque XDF es el método de almacenamiento provisional predeterminado para **RevoScaleR**. Además de los archivos XDF, el **rxGetVarInfo** función ahora admite varios tipos de origen.

## <a name="move-contents-to-sql-server"></a>Mover contenido a SQL Server

Con el origen de datos XDF creado en la sesión local de R, ahora puede pasar estos datos en una tabla de base de datos, almacenando *DayOfWeek* como un entero con valores de 1 a 7.

1. Defina un objeto de origen de datos de SQL Server, especificar una tabla para que contenga los datos y la conexión al servidor remoto.
  
    ```R
    sqlServerAirDemo <- RxSqlServerData(table = "AirDemoSmallTest", connectionString = sqlConnString)
    ```
  
2. Como medida de precaución, incluyen un paso que comprueba si una tabla con el mismo nombre ya existe y elimine la tabla si existe. Una tabla existente de los mismos nombres impide que una nueva desde la que se está creando.
  
    ```R
    if (rxSqlServerTableExists("AirDemoSmallTest",  connectionString = sqlConnString))  rxSqlServerDropTable("AirDemoSmallTest",  connectionString = sqlConnString)
    ```
  
3. Cargar los datos en la tabla mediante **rxDataStep**. Esta función mueve datos entre dos ya definen los orígenes de datos y, opcionalmente, pueden transformar los datos en tránsito.
  
    ```R
    rxDataStep(inData = xdfAirDemo, outFile = sqlServerAirDemo,
        transforms = list( DayOfWeek = as.integer(DayOfWeek),
        rowNum = .rxStartRow : (.rxStartRow + .rxNumRows - 1) ),
        overwrite = TRUE )
    ```
  
    Se trata de una tabla muy grande, por lo que espere hasta que vea un mensaje de estado final como esta: *Filas leídas: 200000, filas procesadas: 600000*.
     
## <a name="load-data-from-a-sql-table"></a>Cargar datos de una tabla SQL

Una vez que existen datos en la tabla, se puede cargar mediante el uso de una consulta SQL simple. 

1. Crear un nuevo origen de datos de SQL Server. La entrada es una consulta en la nueva tabla que acaba de crear y cargar con los datos. Esta definición agrega niveles de factor para la *DayOfWeek* columna, mediante la *colInfo* argumento **RxSqlServerData**.
  
    ```R
    sqlServerAirDemo2 <- RxSqlServerData(
        sqlQuery = "SELECT * FROM AirDemoSmallTest",
        connectionString = sqlConnString,
        rowsPerRead = 50000,
        colInfo = list(DayOfWeek = list(type = "factor",  levels = as.character(1:7))))
    ```
  
2. Llame a **rxSummary** una vez más para revisar un resumen de los datos en la consulta.
  
    ```R
    rxSummary(~., data = sqlServerAirDemo2)
    ```

## <a name="next-steps"></a>Pasos siguientes

> [!div class="nextstepaction"]
> [Realizar análisis de fragmentación mediante rxDataStep](../../advanced-analytics/tutorials/deepdive-perform-chunking-analysis-using-rxdatastep.md)