---
title: Crear un modelo de R y guardarlo en SQL Server (tutorial)
description: Tutorial que muestra cómo crear un modelo de lenguaje R usado para SQL Server análisis de base de datos.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/26/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.openlocfilehash: eec6d165b8e3aa4130246aae6d4aaf5b4102fc0f
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/19/2019
ms.locfileid: "68345826"
---
# <a name="build-an-r-model-and-save-to-sql-server-walkthrough"></a>Crear un modelo de R y guardarlo en SQL Server (tutorial)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

En este paso, aprenderá a crear un modelo de aprendizaje automático y guardar el modelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]en. Al guardar un modelo, puede llamarlo directamente desde [!INCLUDE[tsql](../../includes/tsql-md.md)] el código, mediante el procedimiento almacenado del sistema, [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) o la función PREDICT [(T-SQL)](https://docs.microsoft.com/sql/t-sql/queries/predict-transact-sql).

## <a name="prerequisites"></a>Requisitos previos

En este paso se supone que hay una sesión de R en curso basada en los pasos anteriores de este tutorial. Utiliza las cadenas de conexión y los objetos de origen de datos creados en esos pasos. Las siguientes herramientas y paquetes se utilizan para ejecutar el script.

+ Rgui. exe para ejecutar comandos de R
+ Management Studio para ejecutar T-SQL
+ Paquete ROCR
+ Paquete RODBC

### <a name="create-a-stored-procedure-to-save-models"></a>Crear un procedimiento almacenado para guardar modelos

Este paso utiliza un procedimiento almacenado para guardar un modelo entrenado en SQL Server. La creación de un procedimiento almacenado para realizar esta operación facilita la tarea.

Ejecute el siguiente código de T-SQL en una ventana de consulta de Management Studio para crear el procedimiento almacenado.

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
> Si recibe un error, asegúrese de que el inicio de sesión tiene permiso para crear objetos. Puede conceder permisos explícitos para crear objetos ejecutando una instrucción T-SQL como la siguiente `exec sp_addrolemember 'db_owner', '<user_name>'`:.

## <a name="create-a-classification-model-using-rxlogit"></a>Creación de un modelo de clasificación mediante rxLogit

El modelo es un clasificador binario que predice si es probable que el controlador de taxi obtenga una propina en una determinada conducción o no. Usará el origen de datos que creó en la lección anterior para entrenar el clasificador de propinas mediante la regresión logística.

1. Llame a la función [rxLogit](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxlogit) , incluida en el paquete **RevoScaleR** , para crear un modelo de regresión logística. 

    ```R
    system.time(logitObj <- rxLogit(tipped ~ passenger_count + trip_distance + trip_time_in_secs + direct_distance, data = featureDataSource));
    ```

    La llamada que compila el modelo está incluida en la función system.time. Esto le permite disponer del tiempo necesario para compilar el modelo.

2. Después de generar el modelo, puede inspeccionarlo mediante la `summary` función y ver los coeficientes.

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

1. En primer lugar, use la función [RxSqlServerData](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxsqlserverdata) para definir un objeto de origen de datos para almacenar el resultado de la puntuación.

    ```R
    scoredOutput <- RxSqlServerData(
      connectionString = connStr,
      table = "taxiScoreOutput"  )
    ```

    + Para que este ejemplo sea más sencillo, la entrada del modelo de regresión logística es el mismo origen de datos`sql_feature_ds`de características () que se usó para entrenar el modelo.  La mayoría de las veces tendrá datos nuevos con los que puntuar, o podría haber reservado algunos datos para realizar las pruebas y no el entrenamiento.
  
    + Los resultados de la predicción se guardarán en la tabla _taxiscoreOutput_. Tenga en cuenta que el esquema de esta tabla no está definido cuando se crea mediante rxSqlServerData. El esquema se obtiene de la salida de rxPredict.
  
    + Para crear la tabla que almacena los valores de predicción, el inicio de sesión de SQL que ejecuta la función de datos rxSqlServer debe tener privilegios DDL en la base de datos. Si el inicio de sesión no puede crear tablas, se produce un error en la instrucción.

2. Llame a la función [rxPredict](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxpredict) para generar resultados.

    ```R
    rxPredict(modelObject = logitObj,
        data = featureDataSource,
        outData = scoredOutput,
        predVarNames = "Score",
        type = "response",
        writeModelVars = TRUE, overwrite = TRUE)
    ```
    
    Si la instrucción se ejecuta correctamente, debería tardar algún tiempo en ejecutarse. Cuando haya finalizado, puede abrir SQL Server Management Studio y comprobar que la tabla se ha creado y que contiene la columna puntuación y otra salida esperada.

## <a name="plot-model-accuracy"></a>Precisión del modelo de trazado

Para hacerse una idea de la precisión del modelo, puede usar la función [rxRoc](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxroc) para trazar la curva operativa del receptor. Dado que rxRoc es una de las nuevas funciones proporcionadas por el paquete RevoScaleR que admite contextos de cálculo remotos, tiene dos opciones:

+ Puede usar la función rxRoc para ejecutar el trazado en el contexto de cálculo remoto y, a continuación, devolver el trazado al cliente local.

+ También puede importar los datos en el equipo cliente de R y usar otras funciones de trazado de R para crear el gráfico de rendimiento.

En esta sección, experimentará con ambas técnicas.

### <a name="execute-a-plot-in-the-remote-sql-server-compute-context"></a>Ejecutar un trazado en el contexto de cálculo remoto (SQL Server)

1. Llame a la función rxRoc y proporcione los datos definidos anteriormente como entrada.

    ```R
    scoredOutput = rxImport(scoredOutput);
    rxRoc(actualVarName= "tipped", predVarNames = "Score", scoredOutput);
    ```

    Esta llamada devuelve los valores utilizados para calcular el gráfico ROC. La columna de etiqueta _se incluye_en el marcador, que tiene los resultados reales que está intentando predecir, mientras que la columna _puntuación_ tiene la predicción.

2. Para trazar realmente el gráfico, puede guardar el objeto ROC y, a continuación, dibujarlo con la función de trazado. El gráfico se crea en el contexto de proceso remoto y se devuelve al entorno de R.

    ```R
    scoredOutput = rxImport(scoredOutput);
    rocObjectOut <- rxRoc(actualVarName= "tipped", predVarNames = "Score", scoredOutput);
    plot(rocObjectOut);
    ```

    Abra el dispositivo de gráficos de R o haga clic en la ventana de **trazado** en RStudio para ver el gráfico.

    ![Trazado ROC para el modelo](media/rsql-e2e-rocplot.png "Trazado ROC para el modelo")

### <a name="create-the-plots-in-the-local-compute-context-using-data-from-sql-server"></a>Crear los trazados en el contexto de cálculo local con datos de SQL Server

Para comprobar que el contexto de cálculo es local, ejecute `rxGetComputeContext()` en el símbolo del sistema. El valor devuelto debe ser "RxLocalSeq Compute context".

1. En el contexto de cálculo local, el proceso es prácticamente el mismo. La función [rxImport](https://docs.microsoft.com/r-server/r-reference/revoscaler/rximport) se usa para llevar los datos especificados al entorno local de R.

    ```R
    scoredOutput = rxImport(scoredOutput)
    ```

2. Con los datos de la memoria local, se carga el paquete **ROCR** y se usa la función de predicción de ese paquete para crear algunas predicciones nuevas.

    ```R
    library('ROCR');
    pred <- prediction(scoredOutput$Score, scoredOutput$tipped);
    ```

3. Generar un trazado local, en función de los valores almacenados en la variable `pred`de salida.

    ```R
    acc.perf = performance(pred, measure = 'acc');
    plot(acc.perf);
    ind = which.max( slot(acc.perf, 'y.values')[[1]] );
    acc = slot(acc.perf, 'y.values')[[1]][ind];
    cutoff = slot(acc.perf, 'x.values')[[1]][ind];
    ```

    ![Trazar el rendimiento del modelo mediante R](media/rsql-e2e-performanceplot.png "Trazar el rendimiento del modelo mediante R")

> [!NOTE]
> Los gráficos pueden tener un aspecto diferente al de estos, dependiendo de cuántos puntos de datos haya usado.

## <a name="deploy-the-model"></a>Implementar el modelo

Después de haber creado un modelo y de asegurarse de que funciona bien, es probable que desee implementarlo en un sitio en el que los usuarios o las personas de la organización puedan usar el modelo, o quizás volver a crear el entrenamiento y la calibración del modelo de forma periódica. Este proceso a veces se  denomina operacionalización de un modelo. En SQL Server, la operacionalización se logra mediante la incrustación del código de R en un procedimiento almacenado. Dado que el código reside en el procedimiento, se puede llamar desde cualquier aplicación que pueda conectarse a SQL Server.

Antes de poder llamar al modelo desde una aplicación externa, debe guardar el modelo en la base de datos que se usa para producción. Los modelos entrenados se almacenan en formato binario, en una sola columna de tipo **varbinary (Max)** .

Un flujo de trabajo de implementación típico consta de los siguientes pasos:

1. Serializar el modelo en una cadena hexadecimal
2. Transmitir el objeto serializado a la base de datos
3. Guardar el modelo en una columna varbinary (Max)

En esta sección, aprenderá a usar un procedimiento almacenado para conservar el modelo y hacer que esté disponible para las predicciones. El procedimiento almacenado que se usa en esta sección es PersistModel. La definición de PersistModel se encuentra en [requisitos previos](#prerequisites).

1. Vuelva a cambiar al entorno local de R Si aún no lo está usando, serialice el modelo y guárdelo en una variable.

    ```R
    rxSetComputeContext("local");
    modelbin <- serialize(logitObj, NULL);
    modelbinstr=paste(modelbin, collapse="");
    ```

2. Abra una conexión ODBC mediante **RODBC**. Puede omitir la llamada a RODBC si ya tiene el paquete cargado.

    ```R
    library(RODBC);
    conn <- odbcDriverConnect(connStr);
    ```

3. Llame al procedimiento almacenado PersistModel en SQL Server para transmitir el objeto serializado a la base de datos y almacenar la representación binaria del modelo en una columna. 

    ```R
    q <- paste("EXEC PersistModel @m='", modelbinstr,"'", sep="");
    sqlQuery (conn, q);
    ```

4. Use Management Studio para comprobar que el modelo existe. En Explorador de objetos, haga clic con el botón derecho en la tabla **nyc_taxi_models** y haga clic en **seleccionar las primeras 1000 filas**. En los resultados, debería ver una representación binaria en la columna **modelos** .

Para guardar un modelo en una tabla, solo hace falta una instrucción INSERT. Sin embargo, a menudo resulta más fácil cuando se incluyen en un procedimiento almacenado, como *PersistModel*.

## <a name="next-steps"></a>Pasos siguientes

En la lección siguiente y final, aprenderá a realizar la puntuación en el modelo guardado [!INCLUDE[tsql](../../includes/tsql-md.md)]con.

> [!div class="nextstepaction"]
> [Implementar el modelo de R y usarlo en SQL](walkthrough-deploy-and-use-the-model.md)
