---
title: "Consultar y modificar los datos de SQL Server (An&#225;lisis detallado de ciencia de datos) | Microsoft Docs"
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
ms.assetid: 8c7007a9-9a8f-4dcd-8068-40060d4f6444
caps.latest.revision: 17
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
---
# Consultar y modificar los datos de SQL Server (An&#225;lisis detallado de ciencia de datos)
Ahora que ha cargado los datos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], puede usar los orígenes de datos que ha creado como argumentos para funciones de R en [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] para obtener información básica sobre las variables y generar resúmenes e histogramas.  
  
En este paso, volverá a usar los orígenes de datos para realizar un análisis rápido y, después, mejorar los datos:  
  
## Consultar los datos  
En primer lugar, obtenga una lista de las columnas y sus tipos de datos.  
  
1.  Use la función *rxGetVarInfo* y especifique el origen de datos que quiera analizar:  
  
    ```R  
    rxGetVarInfo(data = sqlFraudDS)   
    ```  
  
  
**Resultado**  
*Var 1: custID, Type: integer*  
*Var 2: gender, Type: integer*  
*Var 3: state, Type: integer*  
*Var 4: cardholder, Type: integer*  
*Var 5: balance, Type: integer*  
*Var 6: numTrans, Type: integer*  
*Var 7: numIntlTrans, Type: integer*  
*Var 8: creditLine, Type: integer*  
*Var 9: fraudRisk, Type: integer*  
  
## Modificar los metadatos  
Todas las variables se almacenan como enteros, pero algunas de las variables representan datos categóricos denominados *variables de factor* en R. Por ejemplo, el *estado* de la columna contiene números que se usan como identificadores de los 50 estados, más el Distrito de Columbia.  Para facilitar la comprensión de los datos, reemplace los números con una lista de abreviaturas de estado.  
  
En este paso, proporcionará un vector de cadena que contenga las abreviaturas y, después, asignará estos valores categóricos a los identificadores enteros originales. Después de que esta variable esté lista, la usará en el argumento *colInfo* para especificar que esta columna se trate como un factor. Posteriormente, se usarán las abreviaturas y la columna se tratará como un factor siempre que se analicen o importen estos datos.  
  
1.  Empiece por crear una variable de R, *stateAbb*, y defina el vector de cadenas que se agregará, como sigue:  
  
    ```R  
    stateAbb <- c("AK", "AL", "AR", "AZ", "CA", "CO", "CT", "DC",     
        "DE", "FL", "GA", "HI","IA", "ID", "IL", "IN", "KS", "KY", "LA",   
        "MA", "MD", "ME", "MI", "MN", "MO", "MS", "MT", "NB", "NC", "ND",   
        "NH", "NJ", "NM", "NV", "NY", "OH", "OK", "OR", "PA", "RI","SC",   
        "SD", "TN", "TX", "UT", "VA", "VT", "WA", "WI", "WV", "WY")  
  
    ```  
  
2.  Después, cree un objeto de información de columna, denominado *ccColInfo*, que especifique la asignación de los valores enteros existentes con los niveles de categorías (las abreviaturas de los estados).  
  
    Esta instrucción también crea variables de factor para el género y el titular de tarjeta.  
  
    ```R  
    ccColInfo <- list(
    gender = list(
              type = "factor",
              levels = c("1", "2"), 
              newLevels = c("Male", "Female")
              ),
    cardholder = list(
                  type = "factor",
                  levels = c("1", "2"),
                  newLevels = c("Principal", "Secondary")
                   ),
    state = list(
             type = "factor",
             levels = as.character(1:51), 
             newLevels = stateAbb
             ),
    balance = list(type = "numeric")
    )  

    ```  
  
3.  Para crear el origen de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que usa los datos actualizados, llame a la función *RxSqlServerData* como antes pero agregue el argumento *colInfo*.  
  
    ```R  
    sqlFraudDS <- RxSqlServerData(connectionString = sqlConnString,  
    table = sqlFraudTable, colInfo = ccColInfo,  
    rowsPerRead = sqlRowsPerRead)   
    ```  
  
    -   Para el parámetro *table*, pase la variable *sqlFraudTable*, que contiene el origen de datos que ha creado anteriormente.    
    -   Para el parámetro *colInfo*, pase la variable *ccColInfo*, que contiene los tipos de datos de columna y los niveles de factor.
    -   Asignar la columna a las abreviaturas antes de usarla como un factor mejora realmente también el rendimiento. Para obtener más información, consulte [R y optimización de datos](https://msdn.microsoft.com/library/mt723575.aspx).  
  
4.  Ahora puede usar la función *rxGetVarInfo* para ver las variables en el nuevo origen de datos.  
  
    ```R  
    rxGetVarInfo(data = sqlFraudDS)   
    ```  
  
**Resultado**  
  
*Var 1: custID, Type: integer*  
*Var 2: gender       2 factor levels: Male Female*  
*Var 3: state       51 factor levels: AK AL AR AZ CA ... VT WA WI WV WY*  
*Var 4: cardholder       2 factor levels: Principal Secondary*  
*Var 5: balance, Type: integer*  
*Var 6: numTrans, Type: integer*  
*Var 7: numIntlTrans, Type: integer*  
*Var 8: creditLine, Type: integer*  
*Var 9: fraudRisk, Type: integer*  
  
Ahora las tres variables que ha especificado (_gender_, _state_ y _cardholder_) se tratan como factores.  
  
## Paso siguiente  
[Definir y usar contextos de cálculo &#40;Análisis detallado de ciencia de datos&#41;](../../advanced-analytics/r-services/define-and-use-compute-contexts-data-science-deep-dive.md)  
  
## Paso anterior  
[Crear objetos de datos de SQL Server mediante RxSqlServerData](../../advanced-analytics/r-services/create-sql-server-data-objects-using-rxsqlserverdata.md)  
  
## Vea también  
[Análisis detallado de ciencia de datos: Usar los paquetes de RevoScaleR](../../advanced-analytics/r-services/data-science-deep-dive-using-the-revoscaler-packages.md)  
  
  
  
