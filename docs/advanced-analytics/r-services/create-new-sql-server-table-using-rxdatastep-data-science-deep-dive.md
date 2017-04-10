---
title: "Crear una nueva tabla de SQL Server mediante rxDataStep (An&#225;lisis detallado de ciencia de datos) | Microsoft Docs"
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
ms.assetid: 98cead96-6de7-4edf-98b9-a1efb09297b9
caps.latest.revision: 19
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
---
# Crear una nueva tabla de SQL Server mediante rxDataStep (An&#225;lisis detallado de ciencia de datos)
En esta lección, aprenderá a mover datos entre las tramas de datos en memoria, el contexto de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y archivos locales.  
  
> [!NOTE]  
> En esta lección usará un conjunto de datos diferente. El conjunto de datos de retraso de aerolíneas es un conjunto de datos público que se usa sobre todo en los experimentos de aprendizaje automático. Si está empezando a trabajar con R, este conjunto de datos es útil para mantener las pruebas ya que se usa en varios ejemplos de producto para [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] que se han publicado con [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Los archivos de datos que necesitará para este ejemplo están disponibles en el mismo directorio que otros ejemplos de producto.  
  
## Crear una tabla de SQL Server a partir de datos locales  
En la primera lección de este tutorial, usó la función *RxTextData* para importar datos en R de un archivo de texto y después la función *RxDataStep* para mover los datos a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
En esta lección, usará un enfoque diferente y obtendrá datos de un archivo guardado en [formato XDF](https://en.wikipedia.org/wiki/Extensible_Data_Format). El formato XDF es un estándar XML desarrollado para datos de dimensiones elevadas. Es un formato de archivo binario con una interfaz de R que optimiza el análisis y el procesamiento de columnas y filas.  Puede usarlo para mover datos y almacenar los subconjuntos de datos que son útiles para el análisis.
  
Después de realizar algunas transformaciones ligeras en los datos mediante el archivo XDF, guardará los datos transformados en una nueva tabla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!NOTE]  
> Necesitará permisos de DDL para este paso.  
  
1.  Establezca el contexto de cálculo en la estación de trabajo local.  
  
    ```R  
    rxSetComputeContext("local")   
    ```  
  
2.  Defina un nuevo objeto de origen de datos mediante la función *RxXdfData*. Para un origen de datos XDF, especifique simplemente la ruta al archivo de datos.  Puede especificar la ruta de acceso al archivo mediante una variable de texto pero, en este caso, hay un método abreviado muy útil, porque el archivo de datos de ejemplo (AirlineDemoSmall.xdf) está en el directorio devuelto por la función *rxGetOption*.
  
    ```R  
    xdfAirDemo <- RxXdfData(file.path(rxGetOption("sampleDataDir"),  "AirlineDemoSmall.xdf"))   
    ```  
  
  
3.  Llame a *rxGetVarInfo* en los datos en memoria para ver un resumen del conjunto de datos.  
  
    ```R  
    rxGetVarInfo(xdfAirDemo)    
    ```  
  
**Resultado**  
  
*Var 1: ArrDelay, Type: integer, Low/High: (-86, 1490)*   
*Var 2: CRSDepTime, Type: numeric, Storage: float32, Low/High: (0.0167, 23.9833)*   
*Var 3: DayOfWeek 7 factor levels: Monday Tuesday Wednesday Thursday Friday Saturday Sunday*  

> [!NOTE]
> 
> ¿Se ha dado cuenta de que no necesita llamar a ninguna función para cargar los datos en el archivo XDF y puede llamar a *rxGetVarInfo* en los datos inmediatamente? Eso es porque XDF es el método de almacenamiento provisional predeterminado para RevoScaleR. Para obtener más información sobre los archivos XDF, consulte la [Guía de introducción a ScaleR](https://msdn.microsoft.com/microsoft-r/scaler-user-guide-data-transform#using-the-data-step-to-create-an-xdf-file-from-a-data-frame). 
  
4.  Ahora, pondrá estos datos en una tabla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y almacenará _DayOfWeek_ como un entero con valores de 1 a 7.  
  
    Para ello, primero defina un origen de datos de SQL Server.  
  
    ```R  
    sqlServerAirDemo <- RxSqlServerData(table = "AirDemoSmallTest", connectionString = sqlConnString)   
    ```  
  
5.  Compruebe si existe una tabla con el mismo nombre y elimine la tabla, si existe.  
  
    ```R  
    if (rxSqlServerTableExists("AirDemoSmallTest",  connectionString = sqlConnString))  rxSqlServerDropTable("AirDemoSmallTest",  connectionString = sqlConnString)    
    ```  
  
6.  Cree la tabla y cargue los datos mediante `rxDataStep`.  
  
    ```R  
    rxDataStep(inData = xdfAirDemo, outFile = sqlServerAirDemo,    
            transforms = list( DayOfWeek = as.integer(DayOfWeek),   
            rowNum = .rxStartRow : (.rxStartRow + .rxNumRows - 1) ),   
            overwrite = TRUE )    
    ```  
  
7.  Establezca el contexto de cálculo de nuevo en el equipo de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
    ```R  
    rxSetComputeContext(sqlCompute)  
    ```  
  
8.  Defina un subconjunto de los datos mediante una instrucción SQL simple.  
  
    ```R    
    SqlServerAirDemo <- RxSqlServerData(  
        sqlQuery = "SELECT * FROM AirDemoSmallTest",      
        connectionString = sqlConnString,   
        rowsPerRead = 50000,      
        colInfo = list(DayOfWeek = list(type = "factor",  levels = as.character(1:7))))    
    ```  
  
9. Llame a *rxSummary* para revisar un resumen de los datos de la consulta.  
  
    ```R  
    rxSummary(~., data = sqlServerAirDemo)   
    ```  
  
## Paso siguiente  
[Realizar análisis de fragmentación mediante rxDataStep &#40;Análisis detallado de ciencia de datos&#41;](../../advanced-analytics/r-services/perform-chunking-analysis-using-rxdatastep-data-science-deep-dive.md)  
  
## Paso anterior  
[Cargar datos en memoria mediante rxImport &#40;Análisis detallado de ciencia de datos&#41;](../../advanced-analytics/r-services/load-data-into-memory-using-rximport-data-science-deep-dive.md)  
  
## Vea también  
[Análisis detallado de ciencia de datos: Usar los paquetes de RevoScaleR](../../advanced-analytics/r-services/data-science-deep-dive-using-the-revoscaler-packages.md)  
  
  
  
