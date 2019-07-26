---
title: Puntuación de nuevos datos mediante RevoScaleR y rxPredict
description: Tutorial tutorial sobre cómo puntuar datos mediante el lenguaje R en SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.openlocfilehash: 8d38f2183078ee87fdb53e6333ecd13e85f3c65e
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/24/2019
ms.locfileid: "68469671"
---
# <a name="score-new-data-sql-server-and-revoscaler-tutorial"></a>Puntuación de nuevos datos (tutorial de SQL Server y RevoScaleR)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Esta lección forma parte del [tutorial de RevoScaleR](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md) sobre cómo usar [las funciones de RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) con SQL Server.

En este paso, utilizará el modelo de regresión logística que creó en la lección anterior para puntuar otro conjunto de datos que utilice las mismas variables independientes como entradas.

> [!div class="checklist"]
> * Puntuación de nuevos datos
> * Crear un histograma de las puntuaciones

> [!NOTE]
> Necesita privilegios de administrador de DDL para algunos de estos pasos.

## <a name="generate-and-save-scores"></a>Generar y guardar puntuaciones
  
1. Actualice el origen de datos de sqlScoreDS (creado en la [lección dos](deepdive-create-sql-server-data-objects-using-rxsqlserverdata.md)) para utilizar la información de columna creada en la lección anterior.
  
    ```R
    sqlScoreDS <- RxSqlServerData(
        connectionString = sqlConnString,
        table = sqlScoreTable,
        colInfo = ccColInfo,
        rowsPerRead = sqlRowsPerRead)
    ```
  
2. Para asegurarse de no perder los resultados, cree un nuevo objeto de origen de datos. A continuación, use el nuevo objeto de origen de datos para rellenar una nueva tabla en la base de datos RevoDeepDive.
  
    ```R
    sqlServerOutDS <- RxSqlServerData(table = "ccScoreOutput",
        connectionString = sqlConnString,
        rowsPerRead = sqlRowsPerRead )
    ```
    En este punto, la tabla no se ha creado. Esta instrucción solo define un contenedor para los datos.
     
3. Compruebe el contexto de cálculo actual mediante **rxGetComputeContext ()** y establezca el contexto de cálculo en el servidor si es necesario.
  
    ```R
    rxSetComputeContext(sqlCompute)
    ```
  
4. Como medida de precaución, Compruebe la existencia de la tabla de salida. Si ya existe una con el mismo nombre, obtendrá un error al intentar escribir la nueva tabla.
  
    Para hacer esto, llame a las funciones [rxSqlServerTableExists](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqlserverdroptable) y [rxSqlServerDropTable](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqlserverdroptable)pasando el nombre de la tabla como entrada.
  
    ```R
    if (rxSqlServerTableExists("ccScoreOutput"))     rxSqlServerDropTable("ccScoreOutput")
    ```
  
    + **rxSqlServerTableExists** consulta el controlador ODBC y devuelve true si la tabla existe; de lo contrario, devuelve false.
    + **rxSqlServerDropTable** ejecuta el DDL y devuelve true si la tabla se quita correctamente; de lo contrario, devuelve false.

5. Ejecute [rxPredict](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxpredict) para crear las puntuaciones y guárdelas en la nueva tabla definida en el origen de datos sqlScoreDS.
  
    ```R
    rxPredict(modelObject = logitObj,
        data = sqlScoreDS,
        outData = sqlServerOutDS,
        predVarNames = "ccFraudLogitScore",
          type = "link",
        writeModelVars = TRUE,
        overwrite = TRUE)
    ```
  
    La función **rxPredict** es otra función que admite la ejecución en contextos de cálculo remotos. Puede usar la función **rxPredict** para crear puntuaciones a partir de modelos basados en [rxLinMod](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlinmod), [rxLogit](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlogit)o [rxGlm](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxglm).
  
    - El parámetro *writeModelVars* está establecido en **TRUE** aquí. Esto significa que las variables que se han usado para la estimación se incluirán en la nueva tabla.
  
    - El parámetro *predVarNames* especifica la variable en la que se almacenarán los resultados. Aquí está pasando una nueva variable, `ccFraudLogitScore`.
  
    - El parámetro *type* para **rxPredict** define cómo quiere que se calculen las predicciones. Especifique la **respuesta** de palabra clave para generar puntuaciones basadas en la escala de la variable de respuesta. O bien, use el **vínculo** de palabra clave para generar puntuaciones basadas en la función de vínculo subyacente, en cuyo caso las predicciones se crean mediante una escala logística.

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

Una vez creada la nueva tabla, se calcula y muestra un histograma de las puntuaciones previstas 10.000. El cálculo es más rápido si se especifican los valores máximo y mínimo, por lo que debe obtenerlos de la base de datos y agregarlos a los datos de trabajo.

1. Cree un nuevo origen de datos, sqlMinMax, que realice una consulta a la base de datos para obtener los valores máximo y mínimo.
  
    ```R
    sqlMinMax <- RxSqlServerData(
        sqlQuery = paste("SELECT MIN(ccFraudLogitScore) AS minVal,",
        "MAX(ccFraudLogitScore) AS maxVal FROM ccScoreOutput"),
        connectionString = sqlConnString)
    ```

     Con este ejemplo puede ver lo fácil que es usar los objetos de origen de datos **RxSqlServerData** para definir conjuntos de datos arbitrarios basados en procedimientos almacenados, funciones o consultas de SQL y, después, usarlos en su código de R. La variable no almacena los valores actuales, solo la definición de origen de datos; la consulta se ejecuta para generar los valores solo cuando la usa en una función como **rxImport**.
      
2. Llame a la función [rxImport](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rximport) para colocar los valores en una trama de datos que se pueda compartir entre contextos de cálculo.
  
    ```R
    minMaxVals <- rxImport(sqlMinMax)
    minMaxVals <- as.vector(unlist(minMaxVals))
    ```

    **Resultado**
     
    ```R
    > minMaxVals
     
    [1] -23.970256   9.786345
    ```

3. Ahora que los valores máximo y mínimo están disponibles, use los valores para crear otro origen de datos para las puntuaciones generadas.
  
    ```R
    sqlOutScoreDS <- RxSqlServerData(sqlQuery = "SELECT ccFraudLogitScore FROM ccScoreOutput",
        connectionString = sqlConnString,
        rowsPerRead = sqlRowsPerRead,
            colInfo = list(ccFraudLogitScore = list(
                low = floor(minMaxVals[1]),
                        high = ceiling(minMaxVals[2]) ) ) )
    ```

4. Use el objeto de origen de datos sqlOutScoreDS para obtener las puntuaciones y calcular y mostrar un histograma. Agregue el código para establecer el contexto de cálculo si es necesario.
  
    ```R
    # rxSetComputeContext(sqlCompute)
    rxHistogram(~ccFraudLogitScore, data = sqlOutScoreDS)
    ```
  
    **Resultado**
  
    ![Histograma complejo creado por R](media/rsql-sue-complex-histogram.png "Histograma complejo creado por R")
  
## <a name="next-steps"></a>Pasos siguientes

> [!div class="nextstepaction"]
> [Transformar datos mediante R](../../advanced-analytics/tutorials/deepdive-transform-data-using-r.md)