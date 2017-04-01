---
title: "Lecci&#243;n 4: Generar y guardar el modelo (Tutorial integral de ciencia de datos) | Microsoft Docs"
ms.custom: ""
ms.date: "11/22/2016"
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
ms.assetid: 69b374c1-2042-4861-8f8b-204a6297c0db
caps.latest.revision: 20
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 18
---
# Lecci&#243;n 4: Generar y guardar el modelo (Tutorial integral de ciencia de datos)
En esta lección, aprenderá a generar un modelo de aprendizaje automático y a guardarlo en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="creating-a-classification-model"></a>Crear un modelo de clasificación  
El modelo que va a generar es un clasificador binario que predice si es probable que el taxista obtenga una propina en un viaje determinado. Usará el origen de datos que creó en la lección anterior, `featureDataSource,` para entrenar el clasificador de propinas mediante la regresión logística.  
  
Estas son las características que usará en el modelo:  
  
-   passenger_count  
  
-   trip_distance  
  
-   trip_time_in_secs  
  
-   direct_distance  

### <a name="create-the-model-using-rxlogit"></a>Crear el modelo con rxLogit  
1.  Llame a la función *rxLogit*, incluida en el paquete **RevoScaleR**, para crear un modelo de regresión logística.  
  
    ```R  
    system.time(logitObj <- rxLogit(tipped ~ passenger_count + trip_distance + trip_time_in_secs + direct_distance, data = featureDataSource))    
    ```  
  
2.  Después de generar el modelo, deberá inspeccionarlo con la función `summary` y ver los coeficientes.  
  
    ```  
    summary(logitObj)  
    ```  

     *Resultados*

     *Logistic Regression Results for: tipped ~ passenger_count + trip_distance + trip_time_in_secs +*  
     *direct_distance*  
     *Data: featureDataSource (RxSqlServerData Data Source)*  
     *Dependent variable(s): tipped*  
     *Total independent variables: 5*   
     *Number of valid observations: 17068*  
     *Number of missing observations: 0*   
     *-2\*LogLikelihood: 23540.0602 (Residual deviance on 17063 degrees of freedom)*  
     *Coefficients:*  
     *Estimate Std. Error z value Pr(>|z|)*   
     *(Intercept)       -2.509e-03  3.223e-02  -0.078  0.93793*   
     *passenger_count   -5.753e-02  1.088e-02  -5.289 1.23e-07 \*\*\**  
     *trip_distance     -3.896e-02  1.466e-02  -2.658  0.00786 \*\**   
     *trip_time_in_secs  2.115e-04  4.336e-05   4.878 1.07e-06 \*\*\**  
     *direct_distance    6.156e-02  2.076e-02   2.966  0.00302 \*\**   
     *---*  
     *Signif. codes:  0 ‘\*\*\*’ 0.001 ‘\*\*’ 0.01 ‘\*’ 0.05 ‘.’ 0.1 ‘ ’ 1*  
     *Condition number of final variance-covariance matrix: 48.3933*   
     *Number of iterations: 4*  
  
### <a name="use-the-logistic-regression-model-for-scoring"></a>Usar el modelo de regresión logística para la puntuación  
Ahora que ha generado el modelo, puede usarlo para predecir si es probable que el taxista obtenga una propina en un viaje determinado.  
  
1.  En primer lugar, defina el objeto de datos que se va a usar para almacenar los resultados de puntuación.  
  
    ```R  
    scoredOutput <- RxSqlServerData(  
      connectionString = connStr,  
      table = "taxiScoreOutput"  )  
    ```  
    + Para simplificar este ejemplo, la entrada en el modelo de regresión logística es el mismo origen de datos `featureDataSource` que usó para entrenar el modelo.  La mayoría de las veces tendrá datos nuevos con los que puntuar, o podría haber reservado algunos datos para realizar las pruebas y no el entrenamiento.  
  
    + Los resultados de predicción se guardan en la tabla _taxiscoreOutput_. Observe que el esquema de esta tabla no está definido cuando se crea mediante `rxSqlServerData`, sino que se obtiene de la salida del objeto *scoredOutput* de `rxPredict`.  
  
    + Para crear la tabla que almacena los valores predichos, el inicio de sesión de SQL que ejecuta la función de datos `rxSqlServer` debe tener privilegios DDL en la base de datos. Si el inicio de sesión no puede crear tablas, se producirá un error en la instrucción.  
  
2.  Llame a la función *rxPredict* para generar resultados.  
  
    ```R  
    rxPredict(modelObject = logitObj, data = featureDataSource, outData = scoredOutput,   
                       predVarNames = "Score", type = "response",   
                       writeModelVars = TRUE, overwrite = TRUE)  
    ```  

  
## <a name="plotting-model-accuracy"></a>Precisión del modelo de trazado  
Para hacerse una idea de la precisión del modelo, puede usar la función *rxRocCurve* para trazar la curva de funcionamiento del receptor. Dado que *rxRovCurve* es una de las nuevas funciones proporcionadas por el paquete RevoScaleR que es compatible con contextos de proceso remoto, tiene dos opciones:  
  
+ Puede usar la función `rxRocCurve` para ejecutar el trazado en el contexto del equipo remoto y, después, devolver el trazado al cliente local.
+ También puede importar los datos en el equipo cliente de R y usar otras funciones de trazado de R para crear el gráfico de rendimiento.  
  
En esta sección, usará ambas técnicas.  
  
### <a name="execute-a-plot-in-the-remote-sql-server-compute-context"></a>Ejecutar un trazado en el contexto de cálculo remoto (SQL Server)  
  
1.  Llame a la función *rxRocCurve* y proporcione los datos definidos anteriormente como entrada.  
  
    ```R  
    rxRocCurve( "tipped", "Score", scoredOutput)  
    ```  
  
    Tenga en cuenta que también debe especificar la columna de etiqueta "tipped" (la variable que intenta predecir) y el nombre de la columna que almacena la predicción (_Score_).  
  
2.  Para ver el gráfico generado, abra el dispositivo de gráficos de R o haga clic en la ventana **Trazar** en RStudio.  
  
    ![ROC plot for the model](../../advanced-analytics/r-services/media/rsql-e2e-rocplot.png "ROC plot for the model")  

    El gráfico se crea en el contexto de cálculo remoto y, luego, se devuelve al entorno de R.   
    
### <a name="create-the-plots-in-the-local-compute-context-using-data-from-sql-server"></a>Crear los trazados en el contexto de cálculo local con datos de SQL Server  
  
1.  Use la función *rxImport* para llevar los datos especificados del entorno local de R.  
  
    ```R  
    scoredOutput = rxImport(scoredOutput)  
    ```  
  
2.  Después de cargar los datos en la memoria local, puede llamar a la biblioteca **ROCR** para crear algunas predicciones y generar el trazado.  
  
    ```R  
    library('ROCR')  
    pred <- prediction(scoredOutput$Score, scoredOutput$tipped)  
  
    acc.perf = performance(pred, measure = 'acc')  
    plot(acc.perf)  
    ind = which.max( slot(acc.perf, 'y.values')[[1]] )  
    acc = slot(acc.perf, 'y.values')[[1]][ind]  
    cutoff = slot(acc.perf, 'x.values')[[1]][ind]  
    ```  
  
3.  En ambos casos, se genera el trazado siguiente.  
  
    ![plotting model performance using R](../../advanced-analytics/r-services/media/rsql-e2e-performanceplot.png "plotting model performance using R")  
  
## <a name="deploying-a-model"></a>Implementar un modelo  

Una vez que haya creado un modelo y que esté seguro de que funciona correctamente, es posible que desee *hacerlo operativo*. Dado que [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] permite invocar un modelo de R con un procedimiento almacenado de [!INCLUDE[tsql](../../includes/tsql-md.md)] , es muy fácil usar R en una aplicación cliente.  
  
Pero antes de llamar al modelo desde una aplicación externa, debe guardarlo en la base de datos que se usa en producción. En [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], los modelos entrenados se almacenan en formato binario, en una sola columna de tipo **varbinary(max)**.

Por lo tanto, mover un modelo entrenado de R a SQL Server incluye estos pasos:  
  
+ Serializar el modelo en una cadena hexadecimal
+ Transmitir el objeto serializado a la base de datos
+ Guardar el modelo en una columna varbinary(max)  
  
En esta sección, obtendrá información sobre cómo conservar el modelo y cómo llamarlo para realizar predicciones.  
  
### <a name="serialize-the-model"></a>Serializar el modelo  
  
+  En el entorno local de R, serialice el modelo y guárdelo en una variable.  
  
    ```R  
    modelbin <- serialize(logitObj, NULL)  
    modelbinstr=paste(modelbin, collapse="")  
    ```  
  
    La función *serialize* se incluye en el paquete **base** de R y proporciona una sencilla interfaz de bajo nivel para serializar en conexiones. Para obtener más información, consulte [http://www.inside-r.org/r-doc/base/serialize](http://www.inside-r.org/r-doc/base/serialize).  
  
### <a name="move-the-model-to-sql-server"></a>Mover el modelo a SQL Server

+ Abra una conexión ODBC y llame a un procedimiento almacenado para almacenar la representación binaria del modelo en una columna de la base de datos. 
  
    ```R  
    library(RODBC)  
    conn <- odbcDriverConnect(connStr )  
  
    # persist model by calling a stored procedure from SQL  
    q<-paste("EXEC PersistModel @m='", modelbinstr,"'", sep="")  
    sqlQuery (conn, q)    
    ```  

Para guardar un modelo en una tabla, solo hace falta una instrucción INSERT. Pero para que resulte más fácil, aquí se usa el procedimiento almacenado _PersistModel_ . 
 
Como referencia, aquí se muestra el código completo del procedimiento almacenado:  
  
```tsql  
CREATE PROCEDURE [dbo].[PersistModel]  @m nvarchar(max)  
AS  
BEGIN  
        -- SET NOCOUNT ON added to prevent extra result sets from  
        -- interfering with SELECT statements.  
        SET NOCOUNT ON;  
        insert into nyc_taxi_models (model) values (convert(varbinary(max),@m,2))  
END   
```  
> [!TIP] Se recomienda crear funciones auxiliares como este procedimiento almacenado para facilitar la administración y la actualización de los modelos de R en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
  
### <a name="invoke-the-saved-model"></a>Invocar el modelo guardado  
Después de guardar el modelo en la base de datos, se puede llamar directamente a él desde código de [!INCLUDE[tsql](../../includes/tsql-md.md)] mediante el procedimiento almacenado del sistema [sp_execute_external_script &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md).  
  
Por ejemplo, para generar predicciones, basta con que se conecte a la base de datos y ejecute un procedimiento almacenado que use el modelo guardado como entrada, junto con algunos datos de entrada.  
  
Pero si tiene un modelo que usa a menudo, es más sencillo ajustar la consulta de entrada y la llamada al modelo, así como los demás parámetros, en un procedimiento almacenado personalizado.  
  
En la siguiente lección, aprenderá a realizar la puntuación en el modelo guardado con [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
## <a name="next-lesson"></a>Lección siguiente  
[Lección 5: Implementar y usar el modelo &#40;Tutorial integral de ciencia de datos &#41;](../../advanced-analytics/r-services/lesson-5-deploy-and-use-the-model-data-science-end-to-end-walkthrough.md)  
  
## <a name="previous-lesson"></a>Lección anterior  
[Lección 3: Crear características de datos &#40;Tutorial integral de ciencia de datos&#41;](../../advanced-analytics/r-services/lesson-3-create-data-features-data-science-end-to-end-walkthrough.md)  
  
  
  
