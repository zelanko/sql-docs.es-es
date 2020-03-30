---
title: 'Tutorial de R: Generar y guardar el modelo'
description: Tutorial en el que se explica cómo crear un modelo de lenguaje R usado para el análisis en base de datos de SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/26/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 4cb806c0a6286ec8a6608b346d12e666a8e9a09f
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/29/2020
ms.locfileid: "73724530"
---
# <a name="build-an-r-model-and-save-to-sql-server-walkthrough"></a>Compilación de un modelo de R y almacenamiento en SQL Server (tutorial)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

En este paso, aprenderá a generar un modelo de Machine Learning y a guardarlo en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Cuando un modelo se guarda, se puede llamar directamente a él desde código de [!INCLUDE[tsql](../../includes/tsql-md.md)] mediante el procedimiento almacenado del sistema, [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md), o la [función PREDICT (T-SQL)](https://docs.microsoft.com/sql/t-sql/queries/predict-transact-sql).

## <a name="prerequisites"></a>Prerrequisitos

En este paso se da por supuesto que hay una sesión de R en curso basada en los pasos anteriores de este tutorial. Usaremos las cadenas de conexión y los objetos de origen de datos creados en esos pasos. También emplearemos las siguientes herramientas y paquetes para ejecutar el script.

+ Rgui.exe para ejecutar comandos de R
+ Management Studio para ejecutar T-SQL
+ Paquete ROCR
+ Paquete RODBC

### <a name="create-a-stored-procedure-to-save-models"></a>Creación de un procedimiento almacenado para guardar modelos

En este paso se usa un procedimiento almacenado para guardar un modelo entrenado en SQL Server. La tarea será más sencilla si se crea un procedimiento almacenado para realizar esta operación.

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
> Si recibe un error, asegúrese de que su inicio de sesión tiene permiso para crear objetos. Para conceder permisos explícitos para crear objetos, ejecute una instrucción T-SQL como esta: `exec sp_addrolemember 'db_owner', '<user_name>'`.

## <a name="create-a-classification-model-using-rxlogit"></a>Creación de un modelo de clasificación mediante rxLogit

El modelo es un clasificador binario que predice si es probable que el taxista obtenga una propina en un trayecto determinado. Usará el origen de datos que creó en la lección anterior para entrenar el clasificador de propinas mediante la regresión logística.

1. Llame a la función [rxLogit](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxlogit) , incluida en el paquete **RevoScaleR** , para crear un modelo de regresión logística. 

    ```R
    system.time(logitObj <- rxLogit(tipped ~ passenger_count + trip_distance + trip_time_in_secs + direct_distance, data = featureDataSource));
    ```

    La llamada que compila el modelo está incluida en la función system.time. Esto le permite disponer del tiempo necesario para compilar el modelo.

2. Después de generar el modelo, se puede inspeccionar con la función `summary` y ver los coeficientes.

    ```R
    summary(logitObj);
    ```

    **Resultados**
    
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

1. Primero, use la función [RxSqlServerData](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxsqlserverdata) para definir un objeto de origen de datos donde almacenar el resultado de la puntuación.

    ```R
    scoredOutput <- RxSqlServerData(
      connectionString = connStr,
      table = "taxiScoreOutput"  )
    ```

    + Para simplificar este ejemplo, la entrada en el modelo de regresión logística es el mismo origen de datos de características (`sql_feature_ds`) que usó para entrenar el modelo.  La mayoría de las veces tendrá datos nuevos con los que puntuar, o podría haber reservado algunos datos para realizar las pruebas y no el entrenamiento.
  
    + Los resultados de predicción se guardarán en la tabla _taxiscoreOutput_. Tenga en cuenta que el esquema de esta tabla no está definido cuando se crea mediante rxSqlServerData. Dicho esquema se obtiene de la salida de rxPredict.
  
    + Para crear la tabla que almacena los valores predichos, el inicio de sesión de SQL que ejecuta la función de datos rxSqlServer debe tener privilegios DDL en la base de datos. Si el inicio de sesión no puede crear tablas, se producirá un error en la instrucción.

2. Llame a la función [rxPredict](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxpredict) para generar resultados.

    ```R
    rxPredict(modelObject = logitObj,
        data = featureDataSource,
        outData = scoredOutput,
        predVarNames = "Score",
        type = "response",
        writeModelVars = TRUE, overwrite = TRUE)
    ```
    
    Si la instrucción se ejecuta correctamente, debe tardar algo de tiempo en ejecutarse. Cuando finalice, puede abrir SQL Server Management Studio y comprobar que la tabla se ha creado y que contiene la columna de puntuación (Score) y otra salida prevista.

## <a name="plot-model-accuracy"></a>Trazado de la precisión del modelo

Para hacerse una idea de la precisión del modelo, puede usar la función [rxRoc](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxroc) para trazar la curva de funcionamiento del receptor. Dado que rxRoc es una de las nuevas funciones proporcionadas por el paquete RevoScaleR que es compatible con contextos de proceso remoto, tiene dos opciones:

+ Puede usar la función rxRoc para ejecutar el trazado en el contexto del equipo remoto y, después, devolver el trazado al cliente local.

+ También puede importar los datos en el equipo cliente de R y usar otras funciones de trazado de R para crear el gráfico de rendimiento.

En esta sección, experimentará con ambas técnicas.

### <a name="execute-a-plot-in-the-remote-sql-server-compute-context"></a>Ejecutar un trazado en el contexto de cálculo remoto (SQL Server)

1. Llame a la función rxRoc y facilite los datos definidos anteriormente como entrada.

    ```R
    scoredOutput = rxImport(scoredOutput);
    rxRoc(actualVarName= "tipped", predVarNames = "Score", scoredOutput);
    ```

    Esta llamada devuelve los valores usados para calcular el gráfico de ROC. La columna de etiqueta es _tipped_, que contiene los resultados reales que está intentando predecir, mientras que la columna _Score_ contiene la predicción.

2. Para trazar el gráfico de facto, puede guardar el objeto ROC y, después, dibujarlo con la función de trazado. El gráfico se crea en el contexto de cálculo remoto y luego se devuelve al entorno de R.

    ```R
    scoredOutput = rxImport(scoredOutput);
    rocObjectOut <- rxRoc(actualVarName= "tipped", predVarNames = "Score", scoredOutput);
    plot(rocObjectOut);
    ```

    Para verlo, abra el dispositivo de gráficos de R o haga clic en la ventana **Trazar** en RStudio.

    ![Trazado de ROC del modelo](media/rsql-e2e-rocplot.png "Trazado de ROC del modelo")

### <a name="create-the-plots-in-the-local-compute-context-using-data-from-sql-server"></a>Crear los trazados en el contexto de cálculo local con datos de SQL Server

Para comprobar que el contexto de cálculo es local, ejecute `rxGetComputeContext()` en el símbolo del sistema. El valor devuelto debe ser "RxLocalSeq Compute Context".

1. En el contexto de cálculo local, el proceso es prácticamente el mismo. Para incluir los datos especificados del entorno local de R se usa la función [rxImport](https://docs.microsoft.com/r-server/r-reference/revoscaler/rximport).

    ```R
    scoredOutput = rxImport(scoredOutput)
    ```

2. Usando los datos de la memoria local, hay que cargar el paquete **ROCR** y usar la función de predicción de ese paquete para crear algunas predicciones nuevas.

    ```R
    library('ROCR');
    pred <- prediction(scoredOutput$Score, scoredOutput$tipped);
    ```

3. Genere un trazado local según los valores almacenados en la variable de salida `pred`.

    ```R
    acc.perf = performance(pred, measure = 'acc');
    plot(acc.perf);
    ind = which.max( slot(acc.perf, 'y.values')[[1]] );
    acc = slot(acc.perf, 'y.values')[[1]][ind];
    cutoff = slot(acc.perf, 'x.values')[[1]][ind];
    ```

    ![Trazado del rendimiento del modelo mediante R](media/rsql-e2e-performanceplot.png "Trazado del rendimiento del modelo mediante R")

> [!NOTE]
> Sus gráficos pueden tener un aspecto diferente al de estos, dependiendo de cuántos puntos de datos haya usado.

## <a name="deploy-the-model"></a>Implementación del modelo

Después de haber creado un modelo y de asegurarse de que funciona bien, lo más probable es que quiera implementarlo en un sitio en el que los usuarios o las personas de la organización puedan usarlo o, quizás, volver a entrenarlo y recalibrarlo de forma periódica. Este proceso se denomina a veces *operacionalizar* un modelo. En SQL Server, la operacionalización se logra al insertar código de R en un procedimiento almacenado. Como el código reside en el procedimiento, se puede llamar desde cualquier aplicación que pueda conectarse a SQL Server.

Antes de llamar al modelo desde una aplicación externa, debe guardarlo en la base de datos que se usa en producción. Los modelos entrenados se almacenan en formato binario, en una sola columna de tipo **varbinary(max)** .

Un flujo de trabajo de implementación típico consta de los siguientes pasos:

1. Serializar el modelo en una cadena hexadecimal
2. Transmitir el objeto serializado a la base de datos
3. Guardar el modelo en una columna varbinary(max)

En esta sección, aprenderá a usar un procedimiento almacenado para conservar el modelo y hacer que esté disponible para las predicciones. El procedimiento almacenado que se usa en esta sección es PersistModel. La definición de PersistModel se encuentra en los [requisitos previos](#prerequisites).

1. Cambie al entorno local de R si aún no lo está usando, serialice el modelo y guárdelo en una variable.

    ```R
    rxSetComputeContext("local");
    modelbin <- serialize(logitObj, NULL);
    modelbinstr=paste(modelbin, collapse="");
    ```

2. Abra una conexión ODBC con **RODBC**. La llamada a RODBC se puede omitir si ya tiene el paquete cargado.

    ```R
    library(RODBC);
    conn <- odbcDriverConnect(connStr);
    ```

3. Llame al procedimiento almacenado PersistModel en SQL Server para transmitir el objeto serializado a la base de datos y almacenar la representación binaria del modelo en una columna. 

    ```R
    q <- paste("EXEC PersistModel @m='", modelbinstr,"'", sep="");
    sqlQuery (conn, q);
    ```

4. Use Management Studio para confirmar que el modelo existe. En el Explorador de objetos, haga clic con el botón derecho en la tabla **nyc_taxi_models** y haga clic en **Seleccionar las primeras 1000 filas**. En Resultados, debería ver una representación binaria en la columna **models**.

Para guardar un modelo en una tabla, solo hace falta una instrucción INSERT. Con todo, esto a menudo resulta más fácil cuando se incluyen en un procedimiento almacenado, como *PersistModel*.

## <a name="next-steps"></a>Pasos siguientes

En la siguiente (y última) lección, aprenderá a realizar la puntuación en el modelo guardado con [!INCLUDE[tsql](../../includes/tsql-md.md)].

> [!div class="nextstepaction"]
> [Implementación del modelo de R y uso en SQL](walkthrough-deploy-and-use-the-model.md)
