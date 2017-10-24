---
title: Generar un modelo de R y guardar en SQL Server | Documentos de Microsoft
ms.custom: 
ms.date: 07/14/2017
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
ms.assetid: 69b374c1-2042-4861-8f8b-204a6297c0db
caps.latest.revision: 21
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 29122bdf543e82c1f429cf401b5fe1d8383515fc
ms.openlocfilehash: 281f5026bc3aa7dc67cff418eb0868eeb81bc80a
ms.contentlocale: es-es
ms.lasthandoff: 10/10/2017

---
# <a name="build-an-r-model-and-save-to-sql-server"></a>Generar un modelo de R y guardar en SQL Server

En este paso, obtendrá información sobre cómo crear un modelo de aprendizaje automático y guardar el modelo en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].

## <a name="create-a-classification-model-using-rxlogit"></a>Crear un modelo de clasificación con rxLogit

El modelo que se genera es un clasificador binario que predice si el controlador de taxi es probable que se obtengan un Consejo acerca de un transporte determinado o no. Deberá usar el origen de datos que creó en la lección anterior para entrenar al clasificador tip, usar la regresión logística.

1. Llame a la función [rxLogit](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxlogit) , incluida en el paquete **RevoScaleR** , para crear un modelo de regresión logística. 

    ```R
    system.time(logitObj <- rxLogit(tipped ~ passenger_count + trip_distance + trip_time_in_secs + direct_distance, data = sql_feature_ds));
    ```

    La llamada que compila el modelo está incluida en la función system.time. Esto le permite disponer del tiempo necesario para compilar el modelo.

2. Después de crear el modelo, puede inspeccionar con el `summary` función y ver los coeficientes.

    ```R
    summary(logitObj);
    ```

     *Resultado*

     *Resultados de regresión logística para:-superpuesto ~ passenger_count + trip_distance + trip_time_in_secs +*
     <br/>*direct_distance*
     <br/>*Datos: featureDataSource (origen de datos de RxSqlServerData)*
     <br/>*Dependent variable(s): superpuesto*
     <br/>*Total de las variables independientes: 5*
     <br/>*Número de observaciones válidas: 17068*
     <br/>*Número de observaciones que faltan: 0*
     <br/>*-2\*LogLikelihood: 23540.0602 (desviación Residual en grados de 17063 libertad)*
     <br/>*Coeficientes:*
     <br/>*Estimate Std. Valor de error z Pr (> | z |)*
     <br/>*(Interceptar) - 2.509e-03 3.223e-02-0.078 0.93793*
     <br/>*passenger_count-5.753e-02 1.088e-02-5.289 1. 23E-07\*\*\**
     <br/>*trip_distance-3.896e-02 1.466e-02-2.658 0.00786\*\**
     <br/>*trip_time_in_secs 2.115e-04 4.336e-05 4.878 1.07e-06\*\*\**
     <br/>*direct_distance 6.156e-02 2.076e-02 2.966 0.00302\*\**
     <br/>*---*
     <br/>*Signif. codes:  0 ‘\*\*\*’ 0.001 ‘\*\*’ 0.01 ‘\*’ 0.05 ‘.’ 0.1 ‘ ’ 1*
     <br/>*Número de la matriz de covarianza de varianza final de la condición: 48.3933*
     <br/>*Number of iterations: 4*

## <a name="use-the-logistic-regression-model-for-scoring"></a>Usar el modelo de regresión logística para la puntuación

Ahora que ha generado el modelo, puede usarlo para predecir si es probable que el taxista obtenga una propina en un viaje determinado.

1. En primer lugar, use la [RxSqlServerData](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxsqlserverdata) función para definir un objeto de origen de datos para almacenar la puntuación resul

    ```R
    scoredOutput <- RxSqlServerData(
      connectionString = connStr,
      table = "taxiScoreOutput"  )
    ```

    + Para simplificar este ejemplo, la entrada para el modelo de regresión logística es el mismo origen de datos de característica (`sql_feature_ds`) que se usa para entrenar el modelo.  La mayoría de las veces tendrá datos nuevos con los que puntuar, o podría haber reservado algunos datos para realizar las pruebas y no el entrenamiento.
  
    + Los resultados de predicción se guardará en la tabla, _taxiscoreOutput_. Tenga en cuenta que no está definido el esquema de esta tabla cuando se crea mediante rxSqlServerData. El esquema se obtiene de la salida de rxPredict.
  
    + Para crear la tabla que almacena los valores de predicción, el inicio de sesión SQL que ejecuta la función de datos de rxSqlServer debe tener privilegios DDL en la base de datos. Si el inicio de sesión no puede crear tablas, se produce un error en la instrucción.

2. Llame a la función [rxPredict](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxpredict) para generar resultados.

    ```R
    rxPredict(modelObject = logitObj,
        data = sql_feature_ds,
        outData = scoredOutput,
        predVarNames = "Score",
        type = "response",
        writeModelVars = TRUE, overwrite = TRUE)
    ```
    
    Si la instrucción se realiza correctamente, tardará algún tiempo en ejecutarse. Cuando haya finalizado, puede abrir SQL Server Management Studio y compruebe que se creó la tabla y que contiene la columna de puntuación y otros resultado esperado.

## <a name="plot-model-accuracy"></a>Gráfico de precisión del modelo

Para hacerse una idea de la precisión del modelo, puede usar el [rxRoc](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxroc) función para trazar la curva de funcionamiento de receptor. Dado que rxRoc es una de las nuevas funciones proporcionadas por el paquete RevoScaleR es compatible con contextos de proceso remoto, tienes dos opciones:

+ Puede usar la función rxRoc para ejecutar el trazado en el contexto de proceso remoto y, a continuación, devolver el gráfico a su cliente local.

+ También puede importar los datos en el equipo cliente de R y usar otras funciones de trazado de R para crear el gráfico de rendimiento.

En esta sección, podrá experimentar con ambas técnicas.

### <a name="execute-a-plot-in-the-remote-sql-server-compute-context"></a>Ejecutar un trazado en el contexto de cálculo remoto (SQL Server)

1. Llame a la función rxRoc y proporcione los datos que se definió anteriormente como entrada.

    ```R
    scoredOutput = rxImport(scoredOutput);
    rxRoc(actualVarName= "tipped", predVarNames = "Score", scoredOutput);
    ```

    Esta llamada devuelve los valores utilizados para calcular el gráfico ROC. La columna de etiqueta es _superpuesto_, que tiene los resultados reales que está intentando predecir, mientras el _puntuación_ columna tiene la predicción.

2. Para trazar realmente el gráfico, puede guardar el objeto ROC y, a continuación, dibuje con el `plot` función. El gráfico se crea en el contexto de proceso remoto y se devuelve al entorno de R.

    ```R
    scoredOutput = rxImport(scoredOutput);
    rocObjectOut <- rxRoc(actualVarName= "tipped", predVarNames = "Score", scoredOutput);
    plot(rocObjectOut);
    ```

    Ver el gráfico al abrir el dispositivo de gráficos de R, o haciendo clic en el **trazar** ventana en RStudio.

    ![Trazado ROC para el modelo](media/rsql-e2e-rocplot.png "Trazado ROC para el modelo")

### <a name="create-the-plots-in-the-local-compute-context-using-data-from-sql-server"></a>Crear los trazados en el contexto de cálculo local con datos de SQL Server

1. Para el contexto de proceso local, el proceso es igual. Usa el [rxImport](https://docs.microsoft.com/r-server/r-reference/revoscaler/rximport) función para poner los datos especificados en su entorno local de R.

    ```R
    scoredOutput = rxImport(scoredOutput)
    ```

2. Con los datos en la memoria local, cargar el **ROCR** del paquete y use la función de predicción de ese paquete para crear algunas nuevas predicciones.

    ```R
    library('ROCR');
    pred <- prediction(scoredOutput$Score, scoredOutput$tipped);
    ```

3. Generar un gráfico local, en función de los valores almacenados en la variable de salida `pred`.

    ```R
    acc.perf = performance(pred, measure = 'acc');
    plot(acc.perf);
    ind = which.max( slot(acc.perf, 'y.values')[[1]] );
    acc = slot(acc.perf, 'y.values')[[1]][ind];
    cutoff = slot(acc.perf, 'x.values')[[1]][ind];
    ```

    ![Trazar el rendimiento del modelo mediante R](media/rsql-e2e-performanceplot.png "Trazar el rendimiento del modelo mediante R")

> [!NOTE]
> Los gráficos pueden parecer diferentes de estos, dependiendo de cuántos puntos de datos que utiliza.

## <a name="deploy-the-model"></a>Implementar el modelo

Después de haber compilado un modelo y determina que esté funcionando correctamente, probablemente desee implementar en un sitio donde los usuarios o personas de su organización pueden hacer usar del modelo, o quizás entrenar el modelo y volver a calibrar el modelo de forma regular. Este proceso se denomina a veces *en marcha la* un modelo.

Dado que [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] permite invocar un modelo de R con una [!INCLUDE[tsql](../../includes/tsql-md.md)] procedimiento almacenado, resulta muy sencillo usar R en una aplicación cliente.

Pero antes de llamar al modelo desde una aplicación externa, debe guardarlo en la base de datos que se usa en producción. En [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], los modelos entrenados se almacenan en formato binario, en una sola columna de tipo **varbinary(max)**.

Por lo tanto, mover un modelo entrenado de R a SQL Server incluye estos pasos:

+ Serializar el modelo en una cadena hexadecimal

+ Transmitir el objeto serializado a la base de datos

+ Guardar el modelo en una columna varbinary(max)

En esta sección, aprenderá cómo conservar el modelo y cómo llamar para realizar predicciones.

1. Cambiar a su entorno de R local si ya no usa lo, serializa el modelo y guardarla en una variable.

    ```R
    rxSetComputeContext("local");
    modelbin <- serialize(logitObj, NULL);
    modelbinstr=paste(modelbin, collapse="");
    ```

2. Abra una conexión ODBC mediante **RODBC**.

    ```R
    library(RODBC);
    conn <- odbcDriverConnect(connStr);
    ```

    Puede omitir la llamada a RODBC si ya tiene el paquete cargado.

3. Llame al procedimiento almacenado creado por el script de PowerShell, para almacenar la representación binaria del modelo en una columna de la base de datos.

    ```R
    q <- paste("EXEC PersistModel @m='", modelbinstr,"'", sep="");
    sqlQuery (conn, q);
    ```

    Para guardar un modelo en una tabla, solo hace falta una instrucción INSERT. Sin embargo, resulta más sencillo cuando se ajusta en un procedimiento almacenado, como _PersistModel_.

    > [!NOTE]
    > Si se produce un error, como "EXECUTE se denegó el permiso en el objeto PersistModel", asegúrese de que el inicio de sesión tiene permiso. Puede conceder permisos explícitos simplemente el procedimiento almacenado mediante la ejecución de una instrucción de T-SQL como ésta:`GRANT EXECUTE ON [dbo].[PersistModel] TO <user_name>`

4. Después de crear un modelo y guardarlo en una base de datos, se puede llamar directamente desde [!INCLUDE[tsql](../../includes/tsql-md.md)] de código, mediante el procedimiento almacenado del sistema, [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md).

    Sin embargo, con todos los modelos de que uso frecuente es más fácil ajustar la consulta de entrada y la llamada al modelo, junto con otros parámetros, en un procedimiento almacenado personalizado.

    Este es el código completo de uno dicho procedimiento almacenado. Se recomienda crear un procedimiento almacenado como éste para que resulten más fáciles de administrar y actualizar los modelos de R en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].

    ```tsql
    CREATE PROCEDURE [dbo].[PersistModel]  @m nvarchar(max)
    AS
    BEGIN
      SET NOCOUNT ON;
      INSERT INTO nyc_taxi_models (model) values (convert(varbinary(max),@m,2))
    END
    ```

  > [!NOTE]
  > Use la **SET NOCOUNT ON** cláusula para evitar resultados adicionales establece interfiera con las instrucciones SELECT.


En la segunda y última lección, aprenderá a realizar puntuar en el modelo guardado con [!INCLUDE[tsql](../../includes/tsql-md.md)].

## <a name="next-lesson"></a>Lección siguiente

[Implementar el modelo de R y usar en SQL](walkthrough-deploy-and-use-the-model.md)

## <a name="previous-lesson"></a>Lección anterior

[Crear características de datos mediante R y SQL](walkthrough-create-data-features.md)


