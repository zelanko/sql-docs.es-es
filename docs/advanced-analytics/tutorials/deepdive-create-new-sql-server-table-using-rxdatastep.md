---
title: "Crear nueva tabla de SQL Server mediante rxDataStep (SQL y R profundización) | Documentos de Microsoft"
ms.custom: 
ms.date: 12/14/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: tutorial
applies_to:
- SQL Server 2016
- SQL Server 2017
dev_langs: R
ms.assetid: 98cead96-6de7-4edf-98b9-a1efb09297b9
caps.latest.revision: "19"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: 5a414c590f72a1b1cfef9a3dbd8082a500592140
ms.sourcegitcommit: 23433249be7ee3502c5b4d442179ea47305ceeea
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/20/2017
---
# <a name="create-new-sql-server-table-using-rxdatastep-sql-and-r-deep-dive"></a>Crear nueva tabla de SQL Server mediante rxDataStep (SQL y R profundización)

Este artículo forma parte del tutorial exhaustiva de ciencia de datos, acerca de cómo usar [RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) con SQL Server.

En esta lección, aprenderá a mover datos entre los marcos de datos en memoria, la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] contexto y archivos locales.

> [!NOTE]
> En esta lección se utiliza un conjunto de datos diferente. El conjunto de datos de retrasos de Airline es un conjunto de datos público que se usa ampliamente para experimentos de aprendizaje automático. Los archivos de datos usados en este ejemplo están disponibles en el mismo directorio que otros ejemplos del producto.

## <a name="create-sql-server-table-from-local-data"></a>Crear tabla de SQL Server a partir de datos locales

En la primera mitad de este tutorial, ha utilizado la **RxTextData** de función para importar datos en R desde un archivo de texto y, a continuación, usar el **RxDataStep** función para mover los datos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].

En esta lección adopta un enfoque diferente y usa datos desde un archivo guardan en el [formato xdf.](https://en.wikipedia.org/wiki/Extensible_Data_Format). Una vez hecho algunas transformaciones a los datos usando el archivo xdf. ligeras, guardar los datos transformados en un nuevo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tabla.

**¿Qué es xdf.?**

El formato xdf. es un estándar XML desarrollado para datos muy dimensionales y se utiliza el formato de archivo nativo por [servidor de aprendizaje de máquina](https://docs.microsoft.com/machine-learning-server/r/concept-what-is-xdf). Es un formato de archivo binario con una interfaz de R que optimiza el análisis y el procesamiento de columnas y filas.  Puede usarlo para mover datos y almacenar los subconjuntos de datos que son útiles para el análisis.

1. Establezca el contexto de cálculo en la estación de trabajo local. **Se necesitan permisos de DDL para este paso.**

  
    ```R
    rxSetComputeContext("local")
    ```
  
2. Defina un nuevo objeto de origen de datos mediante la función **RxXdfData** . Para definir un origen de datos xdf., especifique la ruta de acceso al archivo de datos.  

    Puede especificar la ruta de acceso al archivo mediante una variable de texto. Sin embargo, en este caso, hay un método abreviado muy útil, que consiste en usar la **rxGetOption** función y obtenga el archivo (AirlineDemoSmall.xdf) desde el directorio de datos de ejemplo.
  
    ```R
    xdfAirDemo <- RxXdfData(file.path(rxGetOption("sampleDataDir"),  "AirlineDemoSmall.xdf"))
    ```

3. Llame a [rxGetVarInfo](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxgetvarinfoxdf) en los datos en memoria para ver un resumen del conjunto de datos.
  
    ```R
    rxGetVarInfo(xdfAirDemo)
    ```

**Resultado**

*Var 1: ArrDelay, Type: integer, Low/High: (-86, 1490)*

*Var 2: CRSDepTime, Type: numeric, Storage: float32, Low/High: (0.0167, 23.9833)*

*Var 3: DayOfWeek 7 factor levels: Monday Tuesday Wednesday Thursday Friday Saturday Sunday*

> [!NOTE]
> 
> ¿Se ha dado cuenta de que no necesita llamar a ninguna función para cargar los datos en el archivo XDF y puede llamar a **rxGetVarInfo** en los datos inmediatamente? Eso es porque XDF es el método de almacenamiento provisional predeterminado para RevoScaleR. Además de archivos xdf., el **rxGetVarInfo** función ahora es compatible con varios tipos de origen.
  
4. Coloca estos datos en un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tabla, almacenar _DayOfWeek_ como un entero con valores de 1 a 7.
  
    Para ello, primero defina un origen de datos de SQL Server.
  
    ```R
    sqlServerAirDemo <- RxSqlServerData(table = "AirDemoSmallTest", connectionString = sqlConnString)
    ```
  
5. Compruebe si ya existe una tabla con el mismo nombre y elimínela en caso de que exista.
  
    ```R
    if (rxSqlServerTableExists("AirDemoSmallTest",  connectionString = sqlConnString))  rxSqlServerDropTable("AirDemoSmallTest",  connectionString = sqlConnString)
    ```
  
6. Cree la tabla y cargue los datos mediante **rxDataStep**. Esta función se mueve datos entre dos ya definido orígenes de datos y, opcionalmente, pueden transformar los datos en el camino.
  
    ```R
    rxDataStep(inData = xdfAirDemo, outFile = sqlServerAirDemo,
            transforms = list( DayOfWeek = as.integer(DayOfWeek),
            rowNum = .rxStartRow : (.rxStartRow + .rxNumRows - 1) ),
            overwrite = TRUE )
    ```
  
    Se trata de una tabla bastante grande, por lo que espere hasta que vea un mensaje de estado final como esta: *filas leídas: 200000, de filas totales procesados: 600000*.
     
7. Establezca el contexto de cálculo de nuevo en el equipo de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .

    ```R
    rxSetComputeContext(sqlCompute)
    ```
  
8. Cree un origen de datos de SQL Server mediante una consulta SQL simple en la nueva tabla. Esta definición agrega niveles factor para la *DayOfWeek* columna, mediante la *colInfo* argumento pasado a **RxSqlServerData**.
  
    ```R
    SqlServerAirDemo <- RxSqlServerData(
        sqlQuery = "SELECT * FROM AirDemoSmallTest",
        connectionString = sqlConnString,
        rowsPerRead = 50000,
        colInfo = list(DayOfWeek = list(type = "factor",  levels = as.character(1:7))))
    ```
  
9. Llame a **rxSummary** otra vez para revisar un resumen de los datos de la consulta.
  
    ```R
    rxSummary(~., data = sqlServerAirDemo)
    ```

## <a name="next-step"></a>Paso siguiente

[Realizar análisis de fragmentación mediante rxDataStep](../../advanced-analytics/tutorials/deepdive-perform-chunking-analysis-using-rxdatastep.md)

## <a name="previous-step"></a>Paso anterior

[Cargar datos en memoria mediante rxImport](../../advanced-analytics/tutorials/deepdive-load-data-into-memory-using-rximport.md)
