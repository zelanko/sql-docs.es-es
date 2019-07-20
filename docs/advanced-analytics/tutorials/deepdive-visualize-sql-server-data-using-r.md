---
title: Visualización de datos de SQL Server mediante RevoScaleR rxHistogram
description: Tutorial tutorial sobre cómo visualizar datos mediante el lenguaje R en SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.openlocfilehash: 210fade2820c53ba585043827e7e3d2c36315319
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/19/2019
ms.locfileid: "68344653"
---
#  <a name="visualize-sql-server-data-using-r-sql-server-and-revoscaler-tutorial"></a>Visualización de datos de SQL Server mediante R (tutorial de SQL Server y RevoScaleR)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Esta lección forma parte del [tutorial de RevoScaleR](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md) sobre cómo usar [las funciones de RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) con SQL Server.

En esta lección, use las funciones de R para ver la distribución de los valores de la columna *creditLine* por sexo.

> [!div class="checklist"]
> * Crear variables Min-Max para entradas de histograma
> * Visualización de datos en un histograma mediante **rxHistogram** de **RevoScaleR**
> * Visualización con gráficos de dispersión mediante **levelplot** de **Lattice** incluido en la distribución de R base

Como se muestra en esta lección, puede combinar funciones de código abierto y específicas de Microsoft en el mismo script.

## <a name="add-maximum-and-minimum-values"></a>Agregar valores máximo y mínimo

En función de las estadísticas de Resumen calculadas de la lección anterior, ha descubierto información útil sobre los datos que puede insertar en el origen de datos para realizar cálculos adicionales. Por ejemplo, los valores mínimo y máximo se pueden usar para calcular histogramas. En este ejercicio, agregue los valores máximo y mínimo al origen de datos **RxSqlServerData** .

1. Empiece por configurar algunas variables temporales.
  
    ```R
    sumDF <- sumOut$sDataFrame
    var <- sumDF$Name
    ```
  
2. Use la variable *ccColInfo* que creó en la lección anterior para definir las columnas en el origen de datos.
  
   Agregue nuevas columnas calculadas (*numTrans*, *numIntlTrans*y *creditLine*) a la colección de columnas que invalide la definición original. El script siguiente agrega factores basados en los valores mínimo y máximo, obtenidos de sumOut, que almacena la salida en memoria de **rxSummary**. 
  
    ```R 
    ccColInfo <- list(
        gender = list(type = "factor",
          levels = c("1", "2"), 
          newLevels = c("Male", "Female")),
        cardholder = list(type = "factor",
          levels = c("1", "2"), 
          newLevels = c("Principal", "Secondary")), 
        state = list(type = "factor", 
          levels = as.character(1:51), 
          newLevels = stateAbb), 
        balance  = list(type = "numeric"),
        numTrans = list(type = "factor", 
          levels = as.character(sumDF[var == "numTrans", "Min"]:sumDF[var == "numTrans", "Max"])),
        numIntlTrans = list(type = "factor",  
            levels = as.character(sumDF[var == "numIntlTrans", "Min"]:sumDF[var =="numIntlTrans", "Max"])),
        creditLine = list(type = "numeric")
            )
    ```
  
3. Una vez actualizada la colección de columnas, aplique la instrucción siguiente para crear una versión actualizada [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] del origen de datos que definió anteriormente.
  
    ```R
    sqlFraudDS <- RxSqlServerData(
        connectionString = sqlConnString,
        table = sqlFraudTable,
        colInfo = ccColInfo,
        rowsPerRead = sqlRowsPerRead)
    ```
  
    El origen de datos sqlFraudDS ahora incluye las nuevas columnas agregadas con *ccColInfo*.
  
En este momento, las modificaciones solo afectan al objeto de origen de datos en R; todavía no se ha escrito ningún dato nuevo en la tabla de base de datos. Sin embargo, puede usar los datos capturados en la variable sumOut para crear visualizaciones y resúmenes. 

> [!TIP]
> Si olvida qué contexto de cálculo está usando, ejecute **rxGetComputeContext ()** . Un valor devuelto de "RxLocalSeq Compute context" indica que se está ejecutando en el contexto de proceso local.

## <a name="visualize-data-using-rxhistogram"></a>Visualizar datos mediante rxHistogram

1. Use el siguiente código de R para llamar a la función [rxHistogram](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxhistogram) y pasar una fórmula y un origen de datos. Puede ejecutar esto localmente en primer lugar para ver los resultados esperados y cuánto tarda.
  
    ```R
    rxHistogram(~creditLine|gender, data = sqlFraudDS,  histType = "Percent")
    ```
 
    De manera interna, **rxHistogram** llama a la función [rxCube](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxcube) , que se incluye en el paquete **RevoScaleR** . **rxCube** genera una única lista (o trama de datos) que contiene una columna para cada variable especificada en la fórmula, además de una columna de recuentos.
    
2. Ahora, establezca el contexto de proceso en el equipo de SQL Server remoto y vuelva a ejecutar **rxHistogram** .
  
    ```R
    rxSetComputeContext(sqlCompute)
    rxHistogram(~creditLine|gender, data = sqlFraudDS,  histType = "Percent")
    ```
 
3. Los resultados son exactamente los mismos porque está utilizando el mismo origen de datos, pero en el segundo paso, los cálculos se realizan en el servidor remoto. Después, los resultados se devuelven a la estación de trabajo local para el trazado.
   
  ![resultados del histograma](media/rsql-sue-histogramresults.jpg "resultados del histograma")


## <a name="visualize-with-scatter-plots"></a>Visualizar con gráficos de dispersión

Los gráficos de dispersión se suelen usar durante la exploración de datos para comparar la relación entre dos variables. Puede usar paquetes de R integrados con este fin, con las entradas proporcionadas por las funciones de **RevoScaleR** .

1. Llame a la función [rxCube](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxcrosstabs) para calcular la media de *fraudRisk* para cada combinación de *numTrans* y *numIntlTrans*:
  
    ```R
    cube1 <- rxCube(fraudRisk~F(numTrans):F(numIntlTrans),  data = sqlFraudDS)
    ```
  
    Para especificar los grupos que se han usado para calcular medias de grupo, use la notación `F()` . En este ejemplo, `F(numTrans):F(numIntlTrans)` indica que los enteros de las variables `numTrans` y `numIntlTrans` deben tratarse como variables de categorías, con un nivel para cada valor entero.
  
    El valor devuelto predeterminado de **rxCube** es un *objeto rxCube*, que representa una tabulación cruzada. 
  
2. Llame a la función [rxResultsDF](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxresultsdf) para convertir los resultados en una trama de datos que se puede usar fácilmente en una de las funciones de trazado estándar de R.
  
    ```R
    cubePlot <- rxResultsDF(cube1)
    ```
  
    La función **rxCube** incluye un argumento opcional, *returnDataFrame* = **true**, que puede usar para convertir los resultados en una trama de datos directamente. Por ejemplo:
    
    `print(rxCube(fraudRisk~F(numTrans):F(numIntlTrans), data = sqlFraudDS, returnDataFrame = TRUE))`
       
    Sin embargo, el resultado de **rxResultsDF** es más limpio y conserva los nombres de las columnas de origen. Puede ejecutar `head(cube1)` `head(cubePlot)` seguido de para comparar la salida.
  
3. Cree un mapa térmico mediante la función **levelplot** del paquete **Lattice** , incluido en todas las distribuciones de R.
  
    ```R
    levelplot(fraudRisk~numTrans*numIntlTrans, data = cubePlot)
    ```
  
    **Resultado**
  
    ![resultados del gráfico de dispersión](media/rsql-sue-scatterplotresults.jpg "resultados del gráfico de dispersión")
  
En este análisis rápido, puede ver que el riesgo de fraude aumenta con el número de transacciones y el número de transacciones internacionales.

Para obtener más información sobre la función **rxCube** y referencias cruzadas en general, vea [resúmenes de datos con RevoScaleR](https://docs.microsoft.com/machine-learning-server/r/how-to-revoscaler-data-summaries).

## <a name="next-steps"></a>Pasos siguientes

> [!div class="nextstepaction"]
> [Creación de modelos de R con datos de SQL Server](../../advanced-analytics/tutorials/deepdive-create-models.md)