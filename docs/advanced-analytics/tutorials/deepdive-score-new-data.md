---
title: Puntuación de datos mediante RevoScaleR
description: 'Tutorial 8 de RevoScaleR: Puntuación de datos mediante el lenguaje R en SQL Server.'
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 26f5c7b56298e6a3bd5f1fa9d8bc1d4db79d60af
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/29/2020
ms.locfileid: "74947208"
---
# <a name="score-new-data-sql-server-and-revoscaler-tutorial"></a>Puntuación de datos nuevos (tutorial de SQL Server y RevoScaleR)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Este es el tutorial 8 de la [serie de tutoriales de RevoScaleR](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md) sobre el uso de las [funciones de RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) con SQL Server.

En este tutorial, se usa el modelo de regresión logística que creó en el tutorial anterior para puntuar otro conjunto de datos que use las mismas variables independientes como entradas.

> [!div class="checklist"]
> * Puntuación de nuevos datos
> * Creación de un histograma de las puntuaciones

> [!NOTE]
> Se necesitan privilegios de administrador de DDL para algunos de estos pasos.

## <a name="generate-and-save-scores"></a>Generar y almacenar puntuaciones
  
1. Actualice el origen de datos de sqlScoreDS (creado en el [tutorial dos](deepdive-create-sql-server-data-objects-using-rxsqlserverdata.md)) para usar la información de columna creada en el tutorial anterior.
  
    ```R
    sqlScoreDS <- RxSqlServerData(
        connectionString = sqlConnString,
        table = sqlScoreTable,
        colInfo = ccColInfo,
        rowsPerRead = sqlRowsPerRead)
    ```
  
2. Para asegurarse de que no pierde los resultados, cree un nuevo objeto de origen de datos. Después, use el nuevo objeto de origen de datos para rellenar una nueva tabla en la base de datos RevoDeepDive.
  
    ```R
    sqlServerOutDS <- RxSqlServerData(table = "ccScoreOutput",
        connectionString = sqlConnString,
        rowsPerRead = sqlRowsPerRead )
    ```
    En este punto, la tabla no se ha creado. Esta instrucción solo define un contenedor para los datos.
     
3. Compruebe el contexto de proceso actual mediante **rxGetComputeContext()** y establezca el contexto de proceso en el servidor si es necesario.
  
    ```R
    rxSetComputeContext(sqlCompute)
    ```
  
4. Como medida de precaución, compruebe la existencia de la tabla de salida. Si ya existe una con el mismo nombre, obtendrá un error al intentar escribir en la nueva tabla.
  
    Para hacer esto, llame a las funciones [rxSqlServerTableExists](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqlserverdroptable) y [rxSqlServerDropTable](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqlserverdroptable)pasando el nombre de la tabla como entrada.
  
    ```R
    if (rxSqlServerTableExists("ccScoreOutput"))     rxSqlServerDropTable("ccScoreOutput")
    ```
  
    + **rxSqlServerTableExists** consulta al controlador ODBC y devuelve TRUE si la tabla existe o FALSE en caso contrario.
    + **rxSqlServerDropTable** ejecuta el DDL y devuelve TRUE si la tabla se ha quitado correctamente o FALSE en caso contrario.

5. Ejecute [rxPredict](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxpredict) para crear las puntuaciones y guardarlas en la nueva tabla definida en el origen de datos sqlScoreDS.
  
    ```R
    rxPredict(modelObject = logitObj,
        data = sqlScoreDS,
        outData = sqlServerOutDS,
        predVarNames = "ccFraudLogitScore",
          type = "link",
        writeModelVars = TRUE,
        overwrite = TRUE)
    ```
  
    La función **rxPredict** es otra función que admite la ejecución en contextos de cálculo remotos. Puede usar la función **rxPredict** para crear puntuaciones de modelos basados en [rxLinMod](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlinmod), [rxLogit](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlogit)o [rxGlm](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxglm).
  
    - El parámetro *writeModelVars* está establecido en **TRUE** aquí. Esto significa que las variables que se han usado para la estimación se incluirán en la nueva tabla.
  
    - El parámetro *predVarNames* especifica la variable en la que se almacenarán los resultados. Aquí está pasando una nueva variable, `ccFraudLogitScore`.
  
    - El parámetro *type* para **rxPredict** define cómo quiere que se calculen las predicciones. Especifique la palabra clave **response** para generar puntuaciones basadas en la escala de la variable de respuesta. O use la palabra clave **link** para generar puntuaciones basadas en la función de vínculo subyacente, en cuyo caso las predicciones se crean mediante una escala logística.

6. Después de un tiempo, puede actualizar la lista de tablas en Management Studio para ver la nueva tabla y sus datos.

7. Para agregar variables adicionales para las predicciones de salida, use el argumento *extraVarsToWrite*.  Por ejemplo, en el siguiente código, se agrega la variable *custID* de la tabla de datos de puntuación a la tabla de salida de predicciones.
  
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

## <a name="display-scores-in-a-histogram"></a>Mostrar puntuaciones en un histograma

Una vez creada la nueva tabla, calcule y muestre un histograma de las 10 000 puntuaciones de predicción. El proceso es más rápido si se especifican los valores superior e inferior, así que obténgalos de la base de datos y agréguelos a los datos de trabajo.

1. Cree un nuevo origen de datos, sqlMinMax, que envíe una consulta a la base de datos para obtener los valores altos y bajos.
  
    ```R
    sqlMinMax <- RxSqlServerData(
        sqlQuery = paste("SELECT MIN(ccFraudLogitScore) AS minVal,",
        "MAX(ccFraudLogitScore) AS maxVal FROM ccScoreOutput"),
        connectionString = sqlConnString)
    ```

     Con este ejemplo puede ver lo fácil que es usar los objetos de origen de datos **RxSqlServerData** para definir conjuntos de datos arbitrarios basados en procedimientos almacenados, funciones o consultas de SQL y, después, usarlos en su código de R. La variable no almacena los valores actuales, solo la definición de origen de datos; la consulta se ejecuta para generar los valores solo cuando la usa en una función como **rxImport**.
      
2. Use la función [rxImport](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rximport) para colocar los valores en una trama de datos que se pueda compartir entre varios contextos de proceso.
  
    ```R
    minMaxVals <- rxImport(sqlMinMax)
    minMaxVals <- as.vector(unlist(minMaxVals))
    ```

    **Resultados**
     
    ```R
    > minMaxVals
     
    [1] -23.970256   9.786345
    ```

3. Ahora que los valores máximo y mínimo están disponibles, úselos para crear otro origen de datos para las puntuaciones generadas.
  
    ```R
    sqlOutScoreDS <- RxSqlServerData(sqlQuery = "SELECT ccFraudLogitScore FROM ccScoreOutput",
        connectionString = sqlConnString,
        rowsPerRead = sqlRowsPerRead,
            colInfo = list(ccFraudLogitScore = list(
                low = floor(minMaxVals[1]),
                        high = ceiling(minMaxVals[2]) ) ) )
    ```

4. Use el objeto de origen de datos sqlOutScoreDS para obtener las puntuaciones, y calcular y mostrar un histograma. Agregue el código para establecer el contexto de cálculo si es necesario.
  
    ```R
    # rxSetComputeContext(sqlCompute)
    rxHistogram(~ccFraudLogitScore, data = sqlOutScoreDS)
    ```
  
    **Resultados**
  
    ![Histograma complejo creado por R](media/rsql-sue-complex-histogram.png "Histograma complejo creado por R")
  
## <a name="next-steps"></a>Pasos siguientes

> [!div class="nextstepaction"]
> [Transformar datos mediante R](../../advanced-analytics/tutorials/deepdive-transform-data-using-r.md)