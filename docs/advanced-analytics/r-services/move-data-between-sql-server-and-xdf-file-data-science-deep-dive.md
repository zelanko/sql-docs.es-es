---
title: "Move Data between SQL Server and XDF File (Data Science Deep Dive) (Mover datos entre SQL Server y el archivo XDF (An&#225;lisis detallado de ciencia de datos)) | Microsoft Docs"
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
ms.assetid: 40887cb3-ffbb-4769-9f54-c006d7f4798c
caps.latest.revision: 17
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
---
# Move Data between SQL Server and XDF File (Data Science Deep Dive) (Mover datos entre SQL Server y el archivo XDF (An&#225;lisis detallado de ciencia de datos))
Cuando trabaja en un contexto de cálculo local, tiene acceso a los archivos de datos locales y la base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (definida como un origen de datos *RxSqlServerData*).  
  
En esta sección, aprenderá cómo obtener datos y almacenarlos en un archivo en el equipo local para que pueda realizar transformaciones en los datos. Cuando termine, usará los datos en el archivo para crear una nueva tabla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mediante *rxDataStep*.  
  
## Crear una tabla de SQL Server desde un archivo XDF  

La función *rxImport* le permite importar datos desde cualquier origen de datos que se admita a un archivo XDF local. El uso de un archivo local puede ser conveniente si quiere realizar muchos análisis distintos en los datos almacenados en una base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y quiere evitar ejecutar la misma consulta una y otra vez.  
  
Para este ejercicio, usará de nuevo los datos de fraude de tarjetas de crédito. En este escenario, se le ha pedido realizar un análisis adicional de los usuarios en los estados de California, Oregon y Washington. Para que sea más eficaz, hemos decidido almacenar datos solo para estos estados en el equipo local y trabajar con las variables sexo, titular de la tarjeta, estado y saldo.  
  
1.  Vuelva a usar el vector *stateAbb* que ha creado anteriormente para identificar los niveles que quiere incluir y, después, imprima en la consola la nueva variable, *statesToKeep*.  
  
    ```  
    statesToKeep <- sapply(c("CA", "OR", "WA"), grep, stateAbb)   
  
    statesToKeep  
  
    ```  
 **Resultado**
CA |  O BIEN  | WA 
-- | -- | --
 5 |  38  | 48 
  
2.  Ahora, definirá los datos que quiere traer de SQL Server mediante una consulta de [!INCLUDE[tsql](../../includes/tsql-md.md)].  Más adelante usará esta variable como el argumento *inData* para *rxImport*.  
  
    ```R  
    importQuery <- paste("SELECT gender,cardholder,balance,state FROM",  sqlFraudTable,  "WHERE (state = 5 OR state = 38 OR state = 48)")  
  
    ```  
  
    Asegúrese de que no hay ningún carácter oculto como saltos de línea o tabulaciones en la consulta.  
  
3.  Después, definirá las columnas que se van a usar al trabajar con los datos en R.  
  Por ejemplo, en el conjunto de datos más pequeño, solo necesita tres niveles de factor, porque la consulta solo devuelve datos para tres estados.  Puede volver a usar la variable *statesToKeep* para identificar los niveles correctos que incluir.  
  
    ```R  
    importColInfo <- list(   
        gender = list( type = "factor",  levels = c("1", "2"), newLevels = c("Male", "Female")),       
        cardholder = list(  type = "factor",  levels = c("1", "2"), newLevels = c("Principal", "Secondary")),     
        state = list(   type = "factor",  levels = as.character(statesToKeep), newLevels = names(statesToKeep))   
            )  
  
    ```  
  
4.  Establezca el contexto de cálculo en **local**, ya que quiere todos los datos disponibles en el equipo local.  
  
    ```R  
    rxSetComputeContext("local")   
    ```  
  
5.  Cree el objeto de origen de datos pasando todas las variables que acaba de definir como argumentos a *RxSqlServerData*.  
  
    ```R  
    sqlServerImportDS <- RxSqlServerData(  
        connectionString = sqlConnString,   
        sqlQuery = importQuery,   
        colInfo = importColInfo)  
  
    ```  
  
6.  Después, llame a *rxImport* para guardar los datos en el directorio de trabajo actual, en un archivo denominado `ccFraudSub.xdf`.  
  
    ```R  
    localDS <- rxImport(inData = sqlServerImportDS,   
        outFile = "ccFraudSub.xdf",    
        overwrite = TRUE)  
  
    ```  
  
    El objeto *localDs* devuelto desde la función *rxImport* es un objeto de origen de datos *RxXdfData* ligero que representa el archivo de datos ccFraud.xdf almacenado localmente en el disco.  
  
7.  Llame a *rxGetVarInfo* en el archivo XDF para comprobar que el esquema de datos es el mismo.  
  
    ```R  
    rxGetVarInfo(data = localDS)   
    ```  
    **Resultado**
    
    *rxGetVarInfo(data = localDS)*    
    *Var 1: gender, Tipo: factor, no hay niveles de factor disponibles*    
    *Var 2: cardholder, Tipo: factor, no hay niveles de factor disponibles*    
    *Var 3: balance, Tipo: integer, Low/High: (0, 22463)*    
    *Var 4: state, Tipo: factor, no hay niveles de factor disponibles*
  
8.  Ahora puede llamar a varias funciones de R para analizar el objeto *localDs*, como haría con los datos de origen en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Por ejemplo:  
  
    ```R  
    rxSummary(~gender + cardholder + balance + state, data = localDS)    
    ```  
  
Ahora que ha aprendido a usar contextos de cálculo y trabajar con varios orígenes de datos, ha llegado el momento de probar algo divertido.  
  
En la siguiente y última lección, creará una simulación sencilla mediante una función personalizada de R y la ejecutará en el servidor remoto.  
  
## Paso siguiente  
[Lesson 5: Create a Simple Simulation &#40;Data Science Deep Dive&#41; (Lección 5: Crear una simulación sencilla &#40;Análisis detallado de ciencia de datos&#41;)](../../advanced-analytics/r-services/lesson-5-create-a-simple-simulation-data-science-deep-dive.md)  
  
## Paso anterior  
[Lesson 4: Analyze Data in Local Compute Context &#40;Data Science Deep Dive&#41; (Lección 4: Analizar datos en el contexto de cálculo local &#40;Análisis detallado de ciencia de datos&#41;)](../../advanced-analytics/r-services/lesson-4-analyze-data-in-local-compute-context-data-science-deep-dive.md)  
  
## Vea también  
[Análisis detallado de ciencia de datos: Usar los paquetes de RevoScaleR](../../advanced-analytics/r-services/data-science-deep-dive-using-the-revoscaler-packages.md)  
  
  
  
