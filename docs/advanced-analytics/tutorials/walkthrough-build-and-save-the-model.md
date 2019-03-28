---
title: 'Generar un modelo de R y guardar en SQL Server (tutorial): SQL Server Machine Learning'
description: Tutorial que muestra cómo crear un modelo de lenguaje de R usado para el análisis en bases de datos de SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/26/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 039e5a8970b2161bfe54b1836f3bd12b48477e1a
ms.sourcegitcommit: 2827d19393c8060eafac18db3155a9bd230df423
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/27/2019
ms.locfileid: "58513062"
---
# <a name="build-an-r-model-and-save-to-sql-server-walkthrough"></a>Generar un modelo de R y guardar en SQL Server (tutorial)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

En este paso, aprenderá a crear un modelo de aprendizaje automático y guardar el modelo en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Al guardar un modelo, puede llamarlo directamente desde [!INCLUDE[tsql](../../includes/tsql-md.md)] de código, mediante el procedimiento almacenado del sistema, [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) o [función PREDICT (T-SQL)](https://docs.microsoft.com/sql/t-sql/queries/predict-transact-sql).

## <a name="prerequisites"></a>Requisitos previos

Este paso presupone una sesión de R en curso según los pasos anteriores en este tutorial. Usa cadenas y datos de origen creados objetos de conexión en esos pasos. Las siguientes herramientas y los paquetes se utilizan para ejecutar el script.

+ Rgui.exe para ejecutar comandos de R
+ Management Studio para ejecutar T-SQL
+ Paquete ROCR
+ Paquete RODBC

### <a name="create-a-stored-procedure-to-save-models"></a>Crear un procedimiento almacenado para guardar los modelos

Este paso usa un procedimiento almacenado para guardar un modelo entrenado en SQL Server. Creación de un procedimiento almacenado para realizar esta operación facilita la tarea.

Ejecute el siguiente código Transact-SQL en una ventana de consulta en Management Studio para crear el procedimiento almacenado.

```sql
USE [NYCTaxi_Sample]
GO

SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO

IF EXISTS (SELECT * FROM sys.objects WHERE type = 'P' AND name = 'PersistModel')
  DROP PROCEDURE PersistModel
GO

CREATE PROCEDURE [dbo].[PersistModel] @m nvarchar(max)
AS
BEGIN
    -- SET NOCOUNT ON added to prevent extra result sets from
    -- interfering with SELECT statements.
    SET NOCOUNT ON;
    insert into nyc_taxi_models (model) values (convert(varbinary(max),@m,2))
END
GO
```

> [!NOTE]
> Si se produce un error, asegúrese de que el inicio de sesión tiene permiso para crear objetos. Puede conceder permisos explícitos para crear objetos mediante la ejecución de una instrucción de Transact-SQL similar al siguiente: `exec sp_addrolemember 'db_owner', '<user_name>'`.

## <a name="create-a-classification-model-using-rxlogit"></a>Crear un modelo de clasificación mediante rxLogit

El modelo es un clasificador binario que predice si es probable que obtenga una propina en un viaje determinado o no el conductor del taxi. Usará el origen de datos que creó en la lección anterior para entrenar el clasificador de propinas mediante la regresión logística.

1. Llame a la función [rxLogit](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxlogit) , incluida en el paquete **RevoScaleR** , para crear un modelo de regresión logística. 

    ```R
    system.time(logitObj <- rxLogit(tipped ~ passenger_count + trip_distance + trip_time_in_secs + direct_distance, data = featureDataSource));
    ```

    La llamada que compila el modelo está incluida en la función system.time. Esto le permite disponer del tiempo necesario para compilar el modelo.

2. Después de crear el modelo, puede inspeccionar mediante el `summary` función y ver los coeficientes.

    ```R
    summary(logitObj);
    ```

    **Resultado**
    
    ```R
     *Logistic Regression Results for: tipped ~ passenger_count + trip_distance + trip_time_in_secs +*
     direct_distance* 
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
   ```

## <a name="use-the-logistic-regression-model-for-scoring"></a>Usar el modelo de regresión logística para la puntuación

Ahora que ha generado el modelo, puede usarlo para predecir si es probable que el taxista obtenga una propina en un viaje determinado.

1. En primer lugar, use el [RxSqlServerData](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxsqlserverdata) función para definir un objeto de origen de datos para almacenar el resultado de puntuación.

    ```R
    scoredOutput <- RxSqlServerData(
      connectionString = connStr,
      table = "taxiScoreOutput"  )
    ```

    + Para simplificar este ejemplo, la entrada para el modelo de regresión logística es el mismo origen de datos de característica (`sql_feature_ds`) que usó para entrenar el modelo.  La mayoría de las veces tendrá datos nuevos con los que puntuar, o podría haber reservado algunos datos para realizar las pruebas y no el entrenamiento.
  
    + Los resultados de predicción se guardará en la tabla, _taxiscoreOutput_. Tenga en cuenta que no está definido el esquema de esta tabla cuando se crea mediante rxSqlServerData. El esquema se obtiene de la salida de rxPredict.
  
    + Para crear la tabla que almacena los valores de predicción, el inicio de sesión SQL que ejecuta la función de datos rxSqlServer debe tener privilegios DDL en la base de datos. Si el inicio de sesión no puede crear tablas, se produce un error en la instrucción.

2. Llame a la función [rxPredict](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxpredict) para generar resultados.

    ```R
    rxPredict(modelObject = logitObj,
        data = featureDataSource,
        outData = scoredOutput,
        predVarNames = "Score",
        type = "response",
        writeModelVars = TRUE, overwrite = TRUE)
    ```
    
    Si la instrucción se realiza correctamente, tardará algún tiempo en ejecutarse. Cuando haya terminado, puede abrir SQL Server Management Studio y compruebe que se creó la tabla y que contiene la columna de puntuación y otros salida esperada.

## <a name="plot-model-accuracy"></a>Gráfico de precisión del modelo

Para obtener una idea de la precisión del modelo, puede usar el [rxRoc](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxroc) función para trazar la curva de funcionamiento del receptor. Dado que rxRoc es una de las nuevas funciones proporcionadas por el paquete RevoScaleR es compatible con contextos de cálculo remoto, tiene dos opciones:

+ Puede usar la función rxRoc para ejecutar el trazado en el contexto de proceso remoto y, a continuación, devolver el trazado al cliente local.

+ También puede importar los datos en el equipo cliente de R y usar otras funciones de trazado de R para crear el gráfico de rendimiento.

En esta sección, podrá experimentar con ambas técnicas.

### <a name="execute-a-plot-in-the-remote-sql-server-compute-context"></a>Ejecutar un trazado en el contexto de cálculo remoto (SQL Server)

1. Llame a la función rxRoc y proporcione los datos definidos anteriormente como entrada.

    ```R
    scoredOutput = rxImport(scoredOutput);
    rxRoc(actualVarName= "tipped", predVarNames = "Score", scoredOutput);
    ```

    Esta llamada devuelve los valores que se usan en la informática el gráfico ROC. La columna de etiqueta es _tipped_, que tiene los resultados reales que se está intentando predecir, mientras que el _puntuación_ columna tiene la predicción.

2. Para trazar realmente el gráfico, puede guardar el objeto ROC y, a continuación, se dibuja con la función de trazado. El gráfico se crea en el contexto de proceso remoto y devuelve al entorno de R.

    ```R
    scoredOutput = rxImport(scoredOutput);
    rocObjectOut <- rxRoc(actualVarName= "tipped", predVarNames = "Score", scoredOutput);
    plot(rocObjectOut);
    ```

    Ver el gráfico, abra el dispositivo de gráficos de R, o haga clic en el **trazar** ventana en RStudio.

    ![Trazado ROC para el modelo](media/rsql-e2e-rocplot.png "Trazado ROC para el modelo")

### <a name="create-the-plots-in-the-local-compute-context-using-data-from-sql-server"></a>Crear los trazados en el contexto de cálculo local con datos de SQL Server

Puede comprobar el contexto de cálculo es local mediante la ejecución de `rxGetComputeContext()` en el símbolo del sistema. El valor devuelto debe ser "Contexto de cálculo de RxLocalSeq".

1. Para el contexto de proceso local, el proceso es prácticamente igual. Usa el [rxImport](https://docs.microsoft.com/r-server/r-reference/revoscaler/rximport) función para poner los datos especificados en el entorno local de R.

    ```R
    scoredOutput = rxImport(scoredOutput)
    ```

2. Con los datos en la memoria local, cargue el **ROCR** empaquetar y usar la función de predicción de ese paquete para crear algunas nuevas predicciones.

    ```R
    library('ROCR');
    pred <- prediction(scoredOutput$Score, scoredOutput$tipped);
    ```

3. Generar un trazado local, en función de los valores almacenados en la variable de salida `pred`.

    ```R
    acc.perf = performance(pred, measure = 'acc');
    plot(acc.perf);
    ind = which.max( slot(acc.perf, 'y.values')[[1]] );
    acc = slot(acc.perf, 'y.values')[[1]][ind];
    cutoff = slot(acc.perf, 'x.values')[[1]][ind];
    ```

    ![Trazar el rendimiento del modelo mediante R](media/rsql-e2e-performanceplot.png "Trazar el rendimiento del modelo mediante R")

> [!NOTE]
> Los gráficos podrían ser diferentes de estos, dependiendo de cuántos puntos de datos que se ha usado.

## <a name="deploy-the-model"></a>Implementar el modelo

Después de haber creado un modelo y comprobar que funciona correctamente, probablemente desee implementarla en un sitio donde los usuarios o las personas de su organización pueden hacer utilizar del modelo, o quizás volver a entrenar y vuelva a calibrar el modelo de forma periódica. Este proceso se denomina a veces *operacionalización* un modelo. En SQL Server, puesta en marcha se logra mediante la inserción de código de R en un procedimiento almacenado. Como código reside en el procedimiento, se puede llamar desde cualquier aplicación que puede conectarse a SQL Server.

Antes de que el modelo se puede llamar desde una aplicación externa, debe guardar el modelo en la base de datos utilizada para la producción. Modelos entrenados se almacenan en formato binario, en una sola columna de tipo **varbinary (max)**.

Un flujo de trabajo de implementación típico consta de los pasos siguientes:

1. Serializa el modelo en una cadena hexadecimal
2. Transmitir el objeto serializado a la base de datos
3. Guardar el modelo en una columna varbinary (max)

En esta sección, aprenda a usar un procedimiento almacenado para conservar el modelo y que esté disponible para las predicciones. El procedimiento almacenado usado en esta sección es PersistModel. La definición de PersistModel consta de [requisitos previos](#prerequisites).

1. Cambie al entorno de R local si ya no usa lo, serializa el modelo y guardarlo en una variable.

    ```R
    rxSetComputeContext("local");
    modelbin <- serialize(logitObj, NULL);
    modelbinstr=paste(modelbin, collapse="");
    ```

2. Abra una conexión ODBC con **RODBC**. Puede omitir la llamada a RODBC si ya tiene el paquete cargado.

    ```R
    library(RODBC);
    conn <- odbcDriverConnect(connStr);
    ```

3. Llame al procedimiento de PersistModel almacenado en SQL Server que transmite el objeto serializado a la base de datos y almacenar la representación binaria del modelo en una columna. 

    ```R
    q <- paste("EXEC PersistModel @m='", modelbinstr,"'", sep="");
    sqlQuery (conn, q);
    ```

4. Use Management Studio para comprobar el modelo existe. En el Explorador de objetos, haga doble clic en el **nyc_taxi_models** de tabla y haga clic en **seleccionar 1000 filas superiores**. En los resultados, debería ver una representación binaria en el **modelos** columna.

Para guardar un modelo en una tabla, solo hace falta una instrucción INSERT. Sin embargo, a menudo resulta más fácil cuando se ajusta en un procedimiento almacenado, como *PersistModel*.

## <a name="next-steps"></a>Pasos siguientes

En la siguiente y última lección, aprenderá a realizar la puntuación en el modelo guardado con [!INCLUDE[tsql](../../includes/tsql-md.md)].

> [!div class="nextstepaction"]
> [Implementar el modelo de R y usar en SQL](walkthrough-deploy-and-use-the-model.md)
