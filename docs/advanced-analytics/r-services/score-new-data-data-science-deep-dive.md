---
title: "Puntuaci&#243;n de nuevos datos (An&#225;lisis detallado de ciencia de datos) | Microsoft Docs"
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
ms.assetid: 87056467-f67f-4d72-a83c-ac052736d85d
caps.latest.revision: 17
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
---
# Puntuaci&#243;n de nuevos datos (An&#225;lisis detallado de ciencia de datos)
Ahora que tiene un modelo que puede usar para las predicciones, introducirá datos de la base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para generar algunas predicciones.  
  
## Puntuación de nuevos datos  
Usará el modelo de regresión logística, *logitObj*, para crear puntuaciones para otro conjunto de datos que usa las mismas variables independientes como entradas.  
  
> [!NOTE]  
> Se necesitan privilegios de administrador de DDL para algunos de estos pasos.  
  
1.  Actualice el origen de datos que ha configurado anteriormente, *sqlScoreDS*, para agregar la información de columna requerida.  
  
    ```R  
    sqlScoreDS <- RxSqlServerData(  
        connectionString = sqlConnString,   
        table = sqlScoreTable,   
        colInfo = ccColInfo,   
        rowsPerRead = sqlRowsPerRead)    
    ```  
  
2.  Para asegurarse de no perder los resultados, creará un nuevo objeto de origen de datos y lo usará para rellenar una nueva tabla en la base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
    ```R    
    sqlServerOutDS <- RxSqlServerData(table = "ccScoreOutput",   
        connectionString = sqlConnString,   
        rowsPerRead = sqlRowsPerRead )    
    ```  
     En este punto, la tabla no se ha creado. Esta instrucción solo define un contenedor para los datos.
     
3.  Compruebe el contexto del proceso actual y establezca el contexto de proceso en el servidor si es necesario.  
  
    ```R  
    rxSetComputeContext(sqlCompute)  
    ```  
  
4.  Antes de ejecutar la función de predicción que genera los resultados, debe comprobar que haya una tabla de salida. De lo contrario, obtendrá un error al intentar escribir la nueva tabla  
  
    Para hacer esto, llame a las funciones *rxSqlServerTableExists* y *rxSqlServerDropTable* pasando el nombre de la tabla como entrada.  
  
    ```R  
    if (rxSqlServerTableExists("ccScoreOutput"))     rxSqlServerDropTable("ccScoreOutput")   
    ```  
  
    -   La función *rxSqlServerTableExists* consulta el controlador ODBC y devuelve TRUE si la tabla existe o FALSE en caso contrario.    
    -   La función *rxSqlServerDropTable* ejecuta el DDL y devuelve TRUE si la tabla se ha quitado correctamente o FALSE en caso contrario.   
  
5.  Ahora ya está listo para usar la función *rxPredict* para crear las puntuaciones y guardarlas en la nueva tabla definida en el origen de datos *sqlScoreDS*.  
  
    ```R  
    rxPredict(modelObject = logitObj,   
        data = sqlScoreDS,        
        outData = sqlServerOutDS,     
        predVarNames = "ccFraudLogitScore",   
          type = "link",      
        writeModelVars = TRUE,        
        overwrite = TRUE)    
    ```  
  
    La función *rxPredict* es otra función que admite la ejecución en contextos de cálculo remotos. Puede usar la función *rxPredict* para crear puntuaciones de modelos que se han creado mediante *rxLinMod*, *rxLogit* o *rxGlm*.  
  
    -   El parámetro *writeModelVars* está establecido en **TRUE** aquí. Esto significa que las variables que se han usado para la estimación se incluirán en la nueva tabla.  
  
    -   El parámetro *predVarNames* especifica la variable en la que se almacenarán los resultados. Aquí está pasando una nueva variable, *ccFraudLogitScore*.  
  
    -   El parámetro *type* para *rxPredict* define cómo quiere que se calculen las predicciones. Especifique la palabra clave **response** para generar puntuaciones según la escala de la variable de respuesta, o use la palabra clave **link** para generar puntuaciones según la función de vínculo subyacente, en cuyo caso las predicciones estarán en una escala logística.  

6. Después de un tiempo, puede actualizar la lista de tablas en Management Studio para ver la nueva tabla y sus datos.

7. Para agregar variables adicionales para las predicciones de salida, puede usar el argumento *extraVarsToWrite*.  Por ejemplo, en el siguiente código, se agrega la variable *custID* de la tabla de datos de puntuación a la tabla de salida de predicciones.  
  
    ```R   
    rxPredict(modelObject = logitObj,    
            data = sqlScoreDS,        
            outData = sqlServerOutDS,     
            predVarNames = "ccFraudLogitScore",   
              type = "link",      
            writeModelVars = TRUE,        
            extraVarsToWrite = "custID",      
            overwrite = TRUE)    
    ```  
  
## Mostrar puntuaciones en un histograma  
Una vez creada la nueva tabla, se calcula y muestra un histograma de las 10 000 puntuaciones de predicción. El cálculo será más rápido si se especifican los valores superior e inferior, de modo que los obtenga de la base de datos y los agregue a los datos de trabajo.  
  
1.  Cree un nuevo origen de datos, *sqlMinMax*, que consulte la base de datos para obtener los valores altos y bajos.  
  
    ```R  
    sqlMinMax <- RxSqlServerData(  
        sqlQuery = paste("SELECT MIN(ccFraudLogitScore) AS minVal,",   
        "MAX(ccFraudLogitScore) AS maxVal FROM ccScoreOutput"),   
        connectionString = sqlConnString)    
    ```  
     Con este ejemplo puede ver lo fácil que es usar los objetos de origen de datos *RxSqlServerData* para definir conjuntos de datos arbitrarios basados en procedimientos almacenados, funciones o consultas de SQL y, después, usarlos en su código de R. La variable no almacena los valores actuales, solo la definición de origen de datos; la consulta se ejecuta para generar los valores solo cuando la usa en una función como *rxImport*.  
      
2.  Use la función *rxImport* para colocar los valores en una trama de datos que se pueda compartir en los contextos de proceso.  
  
    ```R  
    minMaxVals <- rxImport(sqlMinMax)   
    minMaxVals <- as.vector(unlist(minMaxVals))  
  
    ```  
     **Resultado**
 
     *> minMaxVals*
     
     *[1] -23.970256   9.786345*
  
3.  Ahora que los valores máximos y mínimo están disponibles, úselos para crear el origen de datos de puntuación.  
  
    ```R  
    sqlOutScoreDS <- RxSqlServerData(sqlQuery = "SELECT ccFraudLogitScore FROM ccScoreOutput",    
        connectionString = sqlConnString,   
        rowsPerRead = sqlRowsPerRead,   
            colInfo = list(ccFraudLogitScore = list(   
                low = floor(minMaxVals[1]),    
                        high = ceiling(minMaxVals[2]) ) ) )  
  
    ```  

  
4.  Por último, use el objeto de origen de datos de puntuación para obtener los datos de puntuación, y calcular y mostrar un histograma. Agregue el código para establecer el contexto de cálculo si es necesario.  
  
    ```R  
    # rxSetComputeContext(sqlCompute)   
    rxHistogram(~ccFraudLogitScore, data = sqlOutScoreDS)  
  
    ```  
  
    **Resultado**  
  
    ![complex histogram created by R](../../advanced-analytics/r-services/media/rsql-sue-complex-histogram.png "complex histogram created by R")  
  
## Paso siguiente  
[Lesson 3: Transform Data Using R &#40;Data Science Deep Dive&#41; (Lección 3: Transformar datos mediante R &#40;Análisis detallado de ciencia de datos&#41;)](../../advanced-analytics/r-services/lesson-3-transform-data-using-r-data-science-deep-dive.md)  
  
## Paso anterior  
[Create Models &#40;Data Science Deep Dive&#41; (Crear modelos &#40;Análisis detallado de ciencia de datos&#41;)](../../advanced-analytics/r-services/create-models-data-science-deep-dive.md)  
  
## Vea también  
[Data Science Deep Dive: Overview &#40;SQL Server R Services&#41; (Análisis detallado de ciencia de datos: Información general &#40;SQL Server R Services&#41;)](http://msdn.microsoft.com/library/mt637368(SQL.130).aspx)  
  
  
  
