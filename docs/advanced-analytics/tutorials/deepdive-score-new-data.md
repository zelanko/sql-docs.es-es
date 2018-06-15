---
title: Puntuar nuevos datos (SQL y R profundización) | Documentos de Microsoft
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 2de06b0159c432ac1d53d9e51bbdf0cd820efd7a
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
ms.locfileid: "31202337"
---
# <a name="score-new-data-sql-and-r-deep-dive"></a>Puntuar nuevos datos (SQL y R profundización)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Este artículo forma parte del tutorial exhaustiva de ciencia de datos, acerca de cómo usar [RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) con SQL Server.

En este paso, se utiliza el modelo de regresión logística que creó anteriormente, para crear puntuaciones para otro conjunto de datos que usa las mismas variables independientes como entradas.

> [!NOTE]
> Se necesitan privilegios de administrador DDL para algunos de estos pasos.

## <a name="generate-and-save-scores"></a>Generar y guardar las puntuaciones
  
1. Actualizar el origen de datos que configuró anteriormente, `sqlScoreDS`, para agregar la información de columna necesaria.
  
    ```R
    sqlScoreDS <- RxSqlServerData(
        connectionString = sqlConnString,
        table = sqlScoreTable,
        colInfo = ccColInfo,
        rowsPerRead = sqlRowsPerRead)
    ```
  
2. Para asegurarse de que no perderá los resultados, cree un nuevo objeto de origen de datos. A continuación, utilice el nuevo objeto de origen de datos para rellenar una tabla nueva en la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] base de datos.
  
    ```R
    sqlServerOutDS <- RxSqlServerData(table = "ccScoreOutput",
        connectionString = sqlConnString,
        rowsPerRead = sqlRowsPerRead )
    ```
    En este punto, la tabla no se ha creado. Esta instrucción solo define un contenedor para los datos.
     
3. Compruebe el contexto del proceso actual y establezca el contexto de proceso en el servidor si es necesario.
  
    ```R
    rxSetComputeContext(sqlCompute)
    ```
  
4. Antes de ejecutar la función de predicción que genera los resultados, debe comprobar que haya una tabla de salida. De lo contrario, obtendrá un error al intentar escribir la nueva tabla.
  
    Para hacer esto, llame a las funciones **rxSqlServerTableExists** y **rxSqlServerDropTable**pasando el nombre de la tabla como entrada.
  
    ```R
    if (rxSqlServerTableExists("ccScoreOutput"))     rxSqlServerDropTable("ccScoreOutput")
    ```
  
    -  La función **rxSqlServerTableExists** consulta el controlador ODBC y devuelve TRUE si la tabla existe o FALSE en caso contrario.
    -  La función **rxSqlServerDropTable** ejecuta el DDL y devuelve TRUE si la tabla está correctamente quita, FALSE en caso contrario.
    - Referencia para las dos funciones se pueden encontrar aquí: [rxSqlServerDropTable](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqlserverdroptable)
  
5. Ahora está listo para usar el [rxPredict](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxpredict) función para crear las puntuaciones y guardarlas en la nueva tabla definida en el origen de datos `sqlScoreDS`.
  
    ```R
    rxPredict(modelObject = logitObj,
        data = sqlScoreDS,
        outData = sqlServerOutDS,
        predVarNames = "ccFraudLogitScore",
          type = "link",
        writeModelVars = TRUE,
        overwrite = TRUE)
    ```
  
    La función **rxPredict** es otra función que admite la ejecución en contextos de cálculo remotos. Puede usar la función **rxPredict** para crear puntuaciones de modelos que se han creado mediante [rxLinMod](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlinmod), [rxLogit](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlogit)o [rxGlm](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxglm).
  
    - El parámetro *writeModelVars* está establecido en **TRUE** aquí. Esto significa que las variables que se han usado para la estimación se incluirán en la nueva tabla.
  
    - El parámetro *predVarNames* especifica la variable en la que se almacenarán los resultados. Aquí está pasando una nueva variable, `ccFraudLogitScore`.
  
    - El parámetro *type* para **rxPredict** define cómo quiere que se calculen las predicciones. Especifica la palabra clave **respuesta** para generar puntuaciones de acuerdo con la escala de la variable de respuesta. O bien, use la palabra clave **vínculo** para generar puntuaciones basadas en la función de enlace subyacente, en cuyo caso se crean predicciones utilizando una escala logística.

6. Después de un tiempo, puede actualizar la lista de tablas en Management Studio para ver la nueva tabla y sus datos.

7. Para agregar variables adicionales para las predicciones de salida, use el argumento *extraVarsToWrite*.  Por ejemplo, en el código siguiente, la variable `custID` se agregan desde la tabla de datos de puntuación en la tabla de salida de las predicciones.
  
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

## <a name="display-scores-in-a-histogram"></a>Puntuaciones de presentación en un histograma

Una vez creada la nueva tabla, puede calcular y mostrar un histograma de los 10.000 puntuaciones de predicción. Cálculo es más rápido si especifica los valores altos y bajos, por lo que obtenerlos de la base de datos y agregarlas a los datos de trabajo.

1. Crear un nuevo origen de datos, `sqlMinMax`, que consulta la base de datos para obtener los valores altos y bajos.
  
    ```R
    sqlMinMax <- RxSqlServerData(
        sqlQuery = paste("SELECT MIN(ccFraudLogitScore) AS minVal,",
        "MAX(ccFraudLogitScore) AS maxVal FROM ccScoreOutput"),
        connectionString = sqlConnString)
    ```

     Con este ejemplo puede ver lo fácil que es usar los objetos de origen de datos **RxSqlServerData** para definir conjuntos de datos arbitrarios basados en procedimientos almacenados, funciones o consultas de SQL y, después, usarlos en su código de R. La variable no almacena los valores actuales, solo la definición de origen de datos; la consulta se ejecuta para generar los valores solo cuando la usa en una función como **rxImport**.
      
2. Llame a la [rxImport](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rximport) función para colocar los valores en una trama de datos que se pueden compartir entre los contextos de proceso.
  
    ```R
    minMaxVals <- rxImport(sqlMinMax)
    minMaxVals \<- as.vector(unlist(minMaxVals))
  
    ```
     **Resultado**
     
     *> minMaxVals*
     
     *[1] -23.970256   9.786345*
  
3. Ahora que están disponibles los valores máximos y mínimo, utilice los valores para crear otro origen de datos de las puntuaciones generadas.
  
    ```R
    sqlOutScoreDS <- RxSqlServerData(sqlQuery = "SELECT ccFraudLogitScore FROM ccScoreOutput",
        connectionString = sqlConnString,
        rowsPerRead = sqlRowsPerRead,
            colInfo = list(ccFraudLogitScore = list(
                low = floor(minMaxVals[1]),
                        high = ceiling(minMaxVals[2]) ) ) )
    ```

4. Utilice el objeto de origen de datos `sqlOutScoreDS` para obtener las puntuaciones y calcular y mostrar un histograma. Agregue el código para establecer el contexto de cálculo si es necesario.
  
    ```R
    # rxSetComputeContext(sqlCompute)
    rxHistogram(~ccFraudLogitScore, data = sqlOutScoreDS)
    ```
  
    **Resultado**
  
    ![Histograma complejo creado por R](media/rsql-sue-complex-histogram.png "Histograma complejo creado por R")
  
## <a name="next-step"></a>Paso siguiente

[Transformar datos mediante R](../../advanced-analytics/tutorials/deepdive-transform-data-using-r.md)

## <a name="previous-step"></a>Paso anterior

[Crear modelos](../../advanced-analytics/tutorials/deepdive-create-models.md)


