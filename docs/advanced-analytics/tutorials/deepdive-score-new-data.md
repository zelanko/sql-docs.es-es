---
title: Puntuar nuevos datos con RevoScaleR y rxPredict - SQL Server Machine Learning
description: Tutorial del tutorial sobre cómo puntuar datos mediante el lenguaje R en SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.openlocfilehash: 386daeb62262182d40ea0b15cca3eb9714c23d64
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67962196"
---
# <a name="score-new-data-sql-server-and-revoscaler-tutorial"></a>Puntuar nuevos datos (tutorial de SQL Server y RevoScaleR)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

En esta lección forma parte de la [RevoScaleR tutorial](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md) sobre cómo usar [funciones de RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) con SQL Server.

En este paso, utilice el modelo de regresión logística que ha creado en la lección anterior para puntuar el otro conjunto de datos que usa las mismas variables independientes como entradas.

> [!div class="checklist"]
> * Puntuación de nuevos datos
> * Crear un histograma de las puntuaciones

> [!NOTE]
> Necesita privilegios de administrador DDL para algunos de estos pasos.

## <a name="generate-and-save-scores"></a>Generar y guardar las puntuaciones
  
1. Actualizar el origen de datos sqlScoreDS (creado en [lección dos](deepdive-create-sql-server-data-objects-using-rxsqlserverdata.md)) para usar la información de columna que creó en la lección anterior.
  
    ```R
    sqlScoreDS <- RxSqlServerData(
        connectionString = sqlConnString,
        table = sqlScoreTable,
        colInfo = ccColInfo,
        rowsPerRead = sqlRowsPerRead)
    ```
  
2. Para asegurarse de que no perder los resultados, cree un nuevo objeto de origen de datos. A continuación, usar el nuevo objeto de origen de datos para rellenar una nueva tabla en la base de datos RevoDeepDive.
  
    ```R
    sqlServerOutDS <- RxSqlServerData(table = "ccScoreOutput",
        connectionString = sqlConnString,
        rowsPerRead = sqlRowsPerRead )
    ```
    En este punto, la tabla no se ha creado. Esta instrucción solo define un contenedor para los datos.
     
3. Compruebe el contexto de proceso actual mediante **rxGetComputeContext()** y establezca el contexto de cálculo en el servidor si es necesario.
  
    ```R
    rxSetComputeContext(sqlCompute)
    ```
  
4. Como medida de precaución, compruebe la existencia de la tabla de salida. Si ya existe uno con el mismo nombre, obtendrá un error al intentar escribir la nueva tabla.
  
    Para hacer esto, llame a las funciones [rxSqlServerTableExists](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqlserverdroptable) y [rxSqlServerDropTable](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqlserverdroptable)pasando el nombre de la tabla como entrada.
  
    ```R
    if (rxSqlServerTableExists("ccScoreOutput"))     rxSqlServerDropTable("ccScoreOutput")
    ```
  
    + **rxSqlServerTableExists** consulta el controlador ODBC y devuelve TRUE si la tabla existe, FALSE en caso contrario.
    + **rxSqlServerDropTable** ejecuta el DDL y devuelve TRUE si la tabla correctamente se ha quitado, FALSE en caso contrario.

5. Ejecutar [rxPredict](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxpredict) para crear las puntuaciones y guardarlas en la nueva tabla definida en sqlScoreDS del origen de datos.
  
    ```R
    rxPredict(modelObject = logitObj,
        data = sqlScoreDS,
        outData = sqlServerOutDS,
        predVarNames = "ccFraudLogitScore",
          type = "link",
        writeModelVars = TRUE,
        overwrite = TRUE)
    ```
  
    La función **rxPredict** es otra función que admite la ejecución en contextos de cálculo remotos. Puede usar el **rxPredict** según la función para crear puntuaciones a partir de modelos [rxLinMod](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlinmod), [rxLogit](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlogit), o [rxGlm](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxglm).
  
    - El parámetro *writeModelVars* está establecido en **TRUE** aquí. Esto significa que las variables que se han usado para la estimación se incluirán en la nueva tabla.
  
    - El parámetro *predVarNames* especifica la variable en la que se almacenarán los resultados. Aquí está pasando una nueva variable, `ccFraudLogitScore`.
  
    - El parámetro *type* para **rxPredict** define cómo quiere que se calculen las predicciones. Especifique la palabra clave **respuesta** para generar puntuaciones según la escala de la variable de respuesta. O bien, use la palabra clave **vínculo** para generar puntuaciones según la función subyacente de vínculo, en cuyo caso se crean predicciones utilizando una escala logística.

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

Una vez creada la nueva tabla, calcule y muestre un histograma de las 10 000 puntuaciones previstas. Cálculo es más rápido si especificar los valores superior e inferior, por lo que los obtenga de la base de datos y agregarlos a los datos de trabajo.

1. Crear un nuevo origen de datos, sqlMinMax, que consulta la base de datos para obtener los valores superior e inferior.
  
    ```R
    sqlMinMax <- RxSqlServerData(
        sqlQuery = paste("SELECT MIN(ccFraudLogitScore) AS minVal,",
        "MAX(ccFraudLogitScore) AS maxVal FROM ccScoreOutput"),
        connectionString = sqlConnString)
    ```

     Con este ejemplo puede ver lo fácil que es usar los objetos de origen de datos **RxSqlServerData** para definir conjuntos de datos arbitrarios basados en procedimientos almacenados, funciones o consultas de SQL y, después, usarlos en su código de R. La variable no almacena los valores actuales, solo la definición de origen de datos; la consulta se ejecuta para generar los valores solo cuando la usa en una función como **rxImport**.
      
2. Llame a la [rxImport](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rximport) función para colocar los valores en una trama de datos que se puede compartir en contextos de cálculo.
  
    ```R
    minMaxVals <- rxImport(sqlMinMax)
    minMaxVals <- as.vector(unlist(minMaxVals))
    ```

    **Resultado**
     
    ```R
    > minMaxVals
     
    [1] -23.970256   9.786345
    ```

3. Ahora que los valores máximos y mínimo están disponibles, utilice los valores para crear otro origen de datos de las puntuaciones generadas.
  
    ```R
    sqlOutScoreDS <- RxSqlServerData(sqlQuery = "SELECT ccFraudLogitScore FROM ccScoreOutput",
        connectionString = sqlConnString,
        rowsPerRead = sqlRowsPerRead,
            colInfo = list(ccFraudLogitScore = list(
                low = floor(minMaxVals[1]),
                        high = ceiling(minMaxVals[2]) ) ) )
    ```

4. Utilice el sqlOutScoreDS de objeto de origen de datos para obtener las puntuaciones y calcular y mostrar un histograma. Agregue el código para establecer el contexto de cálculo si es necesario.
  
    ```R
    # rxSetComputeContext(sqlCompute)
    rxHistogram(~ccFraudLogitScore, data = sqlOutScoreDS)
    ```
  
    **Resultado**
  
    ![Histograma complejo creado por R](media/rsql-sue-complex-histogram.png "Histograma complejo creado por R")
  
## <a name="next-steps"></a>Pasos siguientes

> [!div class="nextstepaction"]
> [Transformar datos mediante R](../../advanced-analytics/tutorials/deepdive-transform-data-using-r.md)