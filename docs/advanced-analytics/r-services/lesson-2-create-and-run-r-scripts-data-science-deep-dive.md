---
title: "Lecci&#243;n 2: Crear y ejecutar scripts de R (An&#225;lisis detallado de ciencia de datos) | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "10/26/2016"
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
ms.assetid: 51e8e66f-a0a5-4e96-aa71-f5c870e6d0d4
caps.latest.revision: 18
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 18
---
# Lecci&#243;n 2: Crear y ejecutar scripts de R (An&#225;lisis detallado de ciencia de datos)
Ahora que ha configurado los orígenes de datos y ha establecido uno o varios contextos de cálculo, está listo para ejecutar scripts de R de alta potencia mediante [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  En esta lección, va a usar el contexto de cálculo del servidor para realizar algunas tareas de aprendizaje automático comunes:  
  
-   Visualizar datos y generar estadísticas de resumen    
-   Crear un modelo de regresión lineal    
-   Crear un modelo de regresión logística    
-   Puntuar nuevos datos y crear un histograma de las puntuaciones  
  
## Cambiar el contexto de cálculo al servidor  
Antes de ejecutar cualquier código R, debe especificar el contexto de cálculo *actual* o *activo*.  
  
1.  Para activar un contexto de cálculo que ya ha definido mediante R, use la función *rxSetComputeContext* como se muestra aquí:  
  
    ```R  
    rxSetComputeContext(sqlCompute)   
    ```  
  
    Cuando ejecute esta instrucción, todos los cálculos posteriores se llevarán a cabo en el equipo con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] especificado en el parámetro *sqlCompute*.  
  
  
2.  Si decide que prefiere ejecutar el código R en su estación de trabajo, puede cambiar el contexto de cálculo al equipo local mediante la palabra clave  **local** .  
  
    ```R  
    rxSetComputeContext ("local")    
    ```  
  
    Para obtener una lista de otras palabras clave admitidas por esta función, escriba `help("rxSetComputeContext")` desde una línea de comandos de R.  
  
> [!NOTE]  
> Después de especificar un contexto de cálculo, permanece activo hasta que lo cambie. Pero todos los scripts de R que *no* se puedan ejecutar en un contexto de servidor remoto se ejecutarán localmente.  
  
## Calcular las estadísticas de resumen  
Para ver cómo funciona el contexto de cálculo, pruebe a generar algunas estadísticas de resumen mediante el origen de datos *sqlFraudDS*.  Recuerde que el objeto de origen de datos solo define los datos que usará; no cambia el contexto de cálculo.

+ Para realizar el resumen de manera local, use *rxSetComputeContext* y especifique la palabra clave "local".
+ Para crear los mismos cálculos en el equipo de SQL Server, cambie al contexto de cálculo de SQL que ha definido anteriormente.  

  
1.  Llame a la función *rxSummary* y pase los argumentos necesarios, como la fórmula y el origen de datos, y asigne los resultados a la variable *sumOut*.  
  
    ```R  
    sumOut <- rxSummary(formula = ~gender + balance + numTrans + numIntlTrans + creditLine, data = sqlFraudDS)  
  
    ```  
  
    El lenguaje R proporciona muchas funciones de resumen, pero *rxSummary* admite la ejecución en varios contextos de cálculo remotos, incluido [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  Para obtener más información sobre funciones similares, consulte [Resúmenes de datos](https://msdn.microsoft.com/microsoft-r/scaler-user-guide-data-summaries) en [Funciones RevoScaleR](https://msdn.microsoft.com/microsoft-r/scaler/scaler).
  
2.  Cuando se haya realizado el procesamiento, puede imprimir el contenido de la variable *sumOut* en la consola.  
  
    ```R  
    sumOut  
    ```  
  
    > [!NOTE]  
    > No intente imprimir los resultados antes de que se devuelvan desde el equipo con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o es posible que se produzca un error.  
  
  
**Resultado**  
  
*Summary Statistics Results for: ~gender + balance + numTrans +*   
 *numIntlTrans + creditLine*    
 *Data: sqlFraudDS (RxSqlServerData Data Source)*    
 *Number of valid observations: 10000*    
 *Name  Mean    StdDev  Min Max ValidObs    MissingObs*    
 *balance       4075,0318 3926,558714            0   25626 100000*    
 *numTrans        29,1061   26,619923 0     100 10000    0           100000*    
 *numIntlTrans     4,0868    8,726757 0      60 10000    0           100000*    
 *creditLine       9.1856    9.870364 1      75 10000    0          100000 Category Counts for gender*    
 *Number of categories: 2*    
 *Number of valid observations: 10000*   
 *Number of missing observations: 0*    
 *gender Counts*    
 *Male   6154*    
  *Female 3846*  
  
## Agregar valores máximos y mínimos  
Según las estadísticas de resumen calculadas, ha descubierto información útil sobre los datos que quiere incluir en el origen de datos para su uso en cálculos adicionales. Por ejemplo, los valores mínimo y máximo se pueden usar para calcular histogramas, por lo que decide agregar los valores máximo y mínimo al origen de datos *RxSqlServerData*.  
  
Afortunadamente [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] incluye funciones optimizadas que pueden convertir de forma muy eficaz datos enteros en datos factoriales de categorías.  
  
1.  Empiece por configurar algunas variables temporales.  
  
    ```R  
    sumDF <- sumOut$sDataFrame   
    var <- sumDF$Name    
    ```  
  
2.  Use la variable *ccColInfo* que ha creado anteriormente para definir las columnas del origen de datos.  
  
    También agregaremos nuevas columnas calculadas (*numTrans*, *numIntlTrans* y *creditLine*) a la colección de columnas.  
  
    ```R 
    ccColInfo <- list(
        gender = list(type = "factor",  
          levels = c("1", "2"), 
          newLevels = c("Male", "Female")), 
        cardholder = list(type = "factor",  
          levels = c("1", "2"), 
          newLevels = c("Principal", "Secondary")), 
        state = list(type = "factor", 
          levels = as.character(1:51), 
          newLevels = stateAbb), 
        balance  = list(type = "numeric"),
        numTrans = list(type = "factor", 
          levels = as.character(sumDF[var == "numTrans", "Min"]:sumDF[var == "numTrans", "Max"])),
        numIntlTrans = list(type = "factor",  
            levels = as.character(sumDF[var == "numIntlTrans", "Min"]:sumDF[var =="numIntlTrans", "Max"])),
        creditLine = list(type = "numeric")
            )
  
    ```  
  
3.  Después de actualizar la colección de columnas, puede aplicar la siguiente instrucción para crear una versión actualizada del origen de datos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que definió anteriormente.  
  
    ```R  
    sqlFraudDS <- RxSqlServerData(  
        connectionString = sqlConnString,   
        table = sqlFraudTable,   
        colInfo = ccColInfo,        
        rowsPerRead = sqlRowsPerRead)   
    ```  
  
    El origen de datos *sqlFraudDS* ahora incluye las nuevas columnas que ha agregado en *ccColInfo*.  
  
Estas modificaciones solo afectan al objeto de origen de datos en R; no se ha escrito ningún dato en la tabla de la base de datos. En cambio, puede usar los datos que se han capturado en la variable *sumOut* para crear visualizaciones y resúmenes. En el siguiente paso, aprenderá cómo hacerlo mientras cambia los contextos de cálculo. 

> [!TIP]
> Si olvida qué contexto de cálculo está usando, use `rxGetComputeContext()`.  Si el valor devuelto es `RxLocalSeq Compute Context`, está usando el contexto de cálculo local.
  
## Paso siguiente  
[Visualizar datos de SQL Server con R &#40;Análisis detallado de ciencia de datos&#41;](../../advanced-analytics/r-services/visualize-sql-server-data-using-r-data-science-deep-dive.md)  
  
## Paso anterior  
[Definir y usar contextos de cálculo &#40;Análisis detallado de ciencia de datos&#41;](../../advanced-analytics/r-services/define-and-use-compute-contexts-data-science-deep-dive.md)  
  
  
  
