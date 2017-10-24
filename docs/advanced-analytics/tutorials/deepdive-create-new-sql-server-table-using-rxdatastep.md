---
title: Crear nueva tabla de SQL Server mediante rxDataStep | Documentos de Microsoft
ms.custom: 
ms.date: 05/18/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
dev_langs:
- R
ms.assetid: 98cead96-6de7-4edf-98b9-a1efb09297b9
caps.latest.revision: 19
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 4a5a8aaa8df1df4d34216f9d55806ccf5594292a
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="create-new-sql-server-table-using-rxdatastep"></a>Crear una nueva tabla de SQL Server mediante rxDataStep

En esta lección, aprenderá a mover datos entre las tramas de datos en memoria, el contexto de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y archivos locales.

> [!NOTE]
> En esta lección usará un conjunto de datos diferente. El conjunto de datos de retrasos de Airline es un conjunto de datos público que se usa ampliamente para experimentos de aprendizaje automático. Si está empezando a trabajar con R, este conjunto de datos es útil para mantener las pruebas ya que se usa en varios ejemplos de producto para [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] que se han publicado con [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Los archivos de datos que necesitará para este ejemplo están disponibles en el mismo directorio que otros ejemplos de producto.

## <a name="create-sql-server-table-from-local-data"></a>Crear una tabla de SQL Server a partir de datos locales

En la primera parte de este tutorial, ha utilizado la **RxTextData** de función para importar datos en R desde un archivo de texto y, a continuación, usar el **RxDataStep** función para mover los datos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].

En esta lección, usará un enfoque diferente y obtendrá datos de un archivo guardado en [formato XDF](https://en.wikipedia.org/wiki/Extensible_Data_Format). El formato XDF es un estándar XML desarrollado para datos de dimensiones elevadas. Es un formato de archivo binario con una interfaz de R que optimiza el análisis y el procesamiento de columnas y filas.  Puede usarlo para mover datos y almacenar los subconjuntos de datos que son útiles para el análisis.

Después de realizar algunas transformaciones ligeras en los datos mediante el archivo XDF, guardará los datos transformados en una nueva tabla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .

> [!NOTE]
> Necesitará permisos de DDL para este paso.

1. Establezca el contexto de cálculo en la estación de trabajo local.
  
    ```R
    rxSetComputeContext("local")
    ```
  
2. Defina un nuevo objeto de origen de datos mediante la función **RxXdfData** . Para un origen de datos XDF, especifique simplemente la ruta al archivo de datos.  Puede especificar la ruta de acceso al archivo mediante una variable de texto, pero en este caso, hay un método abreviado muy útil, porque el archivo de datos de ejemplo (AirlineDemoSmall.xdf) está en el directorio devuelto por la función rxGetOption.
  
    ```R
    xdfAirDemo <- RxXdfData(file.path(rxGetOption("sampleDataDir"),  "AirlineDemoSmall.xdf"))
    ```

3. Llamar a rxGetVarInfo en los datos en memoria para ver un resumen del conjunto de datos.
  
    ```R
    rxGetVarInfo(xdfAirDemo)
    ```

**Resultado**

*Var 1: ArrDelay, Type: integer, Low/High: (-86, 1490)*

*Var 2: CRSDepTime, Type: numeric, Storage: float32, Low/High: (0.0167, 23.9833)*

*Var 3: DayOfWeek 7 factor levels: Monday Tuesday Wednesday Thursday Friday Saturday Sunday*

> [!NOTE]
> 
> ¿Ha observado que no era necesario llamar a otras funciones para cargar los datos en el archivo xdf. y podría llamar rxGetVarInfo en los datos inmediatamente? Eso es porque XDF es el método de almacenamiento provisional predeterminado para RevoScaleR. Para obtener más información acerca de los archivos xdf., vea [crear un xdf.](https://msdn.microsoft.com/microsoft-r/scaler-data-xdf).
  
4. Ahora, pondrá estos datos en una tabla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y almacenará _DayOfWeek_ como un entero con valores de 1 a 7.
  
    Para ello, primero defina un origen de datos de SQL Server.
  
    ```R
    sqlServerAirDemo <- RxSqlServerData(table = "AirDemoSmallTest", connectionString = sqlConnString)
    ```
  
5. Compruebe si ya existe una tabla con el mismo nombre y elimínela en caso de que exista.
  
    ```R
    if (rxSqlServerTableExists("AirDemoSmallTest",  connectionString = sqlConnString))  rxSqlServerDropTable("AirDemoSmallTest",  connectionString = sqlConnString)
    ```
  
6. Cree la tabla y cargue los datos mediante **rxDataStep**. Esta función se mueve datos entre dos ya definido orígenes de datos y pueden transformar los datos en la ruta.
  
    ```R
    rxDataStep(inData = xdfAirDemo, outFile = sqlServerAirDemo,
            transforms = list( DayOfWeek = as.integer(DayOfWeek),
            rowNum = .rxStartRow : (.rxStartRow + .rxNumRows - 1) ),
            overwrite = TRUE )
    ```
  
    Se trata de una tabla muy grande, por lo que espere hasta ver el mensaje de estado final: *Rows Read: 200000, Total Rows Processed: 600000* (Filas leídas: 200 000, total de filas procesadas: 600 000).
     
7. Establezca el contexto de cálculo de nuevo en el equipo de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .

    ```R
    rxSetComputeContext(sqlCompute)
    ```
  
8. Cree un origen de datos de SQL Server mediante una consulta SQL simple en la nueva tabla. Esta definición agrega niveles de factor para la columna *DayOfWeek* mediante el argumento *colInfo* en RxSqlServerData.
  
    ```R
    SqlServerAirDemo <- RxSqlServerData(
        sqlQuery = "SELECT * FROM AirDemoSmallTest",
        connectionString = sqlConnString,
        rowsPerRead = 50000,
        colInfo = list(DayOfWeek = list(type = "factor",  levels = as.character(1:7))))
    ```
  
9. Llame a rxSummary una vez más para ver un resumen de los datos de la consulta.
  
    ```R
    rxSummary(~., data = sqlServerAirDemo)
    ```

## <a name="next-step"></a>Paso siguiente

[Realizar análisis de fragmentación con rxDataStep](../../advanced-analytics/tutorials/deepdive-perform-chunking-analysis-using-rxdatastep.md)

## <a name="previous-step"></a>Paso anterior

[Cargar datos en memoria mediante rxImport](../../advanced-analytics/tutorials/deepdive-load-data-into-memory-using-rximport.md)



