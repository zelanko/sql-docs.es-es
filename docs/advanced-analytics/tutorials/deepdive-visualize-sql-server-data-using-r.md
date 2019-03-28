---
title: Visualizar datos de SQL Server con RevoScaleR rxHistogram - SQL Server Machine Learning
description: Tutorial del tutorial sobre cómo visualizar datos mediante el lenguaje R en SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: c39d19807cfe01ca9c96b47de020abb9227c43a0
ms.sourcegitcommit: 2827d19393c8060eafac18db3155a9bd230df423
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/27/2019
ms.locfileid: "58513082"
---
#  <a name="visualize-sql-server-data-using-r-sql-server-and-revoscaler-tutorial"></a>Visualizar datos de SQL Server con R (tutorial de SQL Server y RevoScaleR)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

En esta lección forma parte de la [RevoScaleR tutorial](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md) sobre cómo usar [funciones de RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) con SQL Server.

En esta lección, usará las funciones de R para ver la distribución de valores en el *creditLine* columna por género.

> [!div class="checklist"]
> * Crear variables de Mín. máx. para las entradas de histograma
> * Visualizar datos en un histograma mediante **rxHistogram** desde **RevoScaleR**
> * Visualización de gráficos de dispersión con **levelplot** desde **lattice** incluidas en la distribución de R base

Como se muestra en esta lección, puede combinar funciones específicas de Microsoft y de código abierto en el mismo script.

## <a name="add-maximum-and-minimum-values"></a>Agregar valores máximos y mínimos

En función de las estadísticas de resumen calculadas de la lección anterior, que haya descubierto información útil acerca de los datos que se pueden insertar en el origen de datos aún más los cálculos. Por ejemplo, los valores mínimo y máximos se pueden usar para calcular histogramas. En este ejercicio, agregue los valores máximo y mínimo para el **RxSqlServerData** origen de datos.

1. Empiece por configurar algunas variables temporales.
  
    ```R
    sumDF <- sumOut$sDataFrame
    var <- sumDF$Name
    ```
  
2. Use la variable *ccColInfo* que creó en la lección anterior para definir las columnas del origen de datos.
  
   Agregar nuevas columnas calculadas (*numTrans*, *numIntlTrans*, y *creditLine*) a la colección de columnas que reemplazar la definición original. El siguiente script agrega factores según los valores mínimos y máximo, obtenidos sumOut, que almacena el resultado en memoria de **rxSummary**. 
  
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
  
3. Después de actualizar la colección de columnas, se aplican a la siguiente instrucción para crear una versión actualizada de la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] origen de datos que definió anteriormente.
  
    ```R
    sqlFraudDS <- RxSqlServerData(
        connectionString = sqlConnString,
        table = sqlFraudTable,
        colInfo = ccColInfo,
        rowsPerRead = sqlRowsPerRead)
    ```
  
    El origen de datos sqlFraudDS ahora incluye las nuevas columnas que se agregan mediante *ccColInfo*.
  
En este momento, las modificaciones afectan a solo el objeto de origen de datos en R; No hay nuevos datos se ha escrito todavía en la tabla de base de datos. Sin embargo, puede usar los datos capturados en la variable sumOut para crear visualizaciones y resúmenes. 

> [!TIP]
> Si olvida qué contexto de proceso está usando, ejecute **rxGetComputeContext()**. Un valor devuelto de "Contexto de cálculo de RxLocalSeq" indica que se está ejecutando en el contexto de proceso local.

## <a name="visualize-data-using-rxhistogram"></a>Visualizar datos con rxHistogram

1. Use el siguiente código de R para llamar a la función [rxHistogram](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxhistogram) y pasar una fórmula y un origen de datos. Puede ejecutar esto localmente en primer lugar para ver los resultados esperados y cuánto tarda.
  
    ```R
    rxHistogram(~creditLine|gender, data = sqlFraudDS,  histType = "Percent")
    ```
 
    De manera interna, **rxHistogram** llama a la función [rxCube](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxcube) , que se incluye en el paquete **RevoScaleR** . **rxCube** genera una única lista (o trama de datos) que contiene una columna para cada variable especificada en la fórmula, además de una columna de recuento.
    
2. Ahora, establezca el contexto de proceso en el equipo remoto de SQL Server y ejecute **rxHistogram** nuevo.
  
    ```R
    rxSetComputeContext(sqlCompute)
    rxHistogram(~creditLine|gender, data = sqlFraudDS,  histType = "Percent")
    ```
 
3. Los resultados son exactamente el mismo porque está usando el mismo origen de datos, pero en el segundo paso, los cálculos se realizan en el servidor remoto. Después, los resultados se devuelven a la estación de trabajo local para el trazado.
   
  ![resultados del histograma](media/rsql-sue-histogramresults.jpg "resultados del histograma")


## <a name="visualize-with-scatter-plots"></a>Visualización de gráficos de dispersión

Gráficos de dispersión se usan a menudo durante la exploración de datos para comparar la relación entre dos variables. Puede utilizar paquetes de R integrados para este fin, con las entradas proporcionadas por **RevoScaleR** funciones.

1. Llame a la [rxCube](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxcrosstabs) función para calcular la media de *fraudRisk* para cada combinación de *numTrans* y *numIntlTrans*:
  
    ```R
    cube1 <- rxCube(fraudRisk~F(numTrans):F(numIntlTrans),  data = sqlFraudDS)
    ```
  
    Para especificar los grupos que se han usado para calcular medias de grupo, use la notación `F()` . En este ejemplo, `F(numTrans):F(numIntlTrans)` indica que los enteros de las variables `numTrans` y `numIntlTrans` deben tratarse como variables categóricas, con un nivel para cada valor entero.
  
    El valor predeterminado devuelve el valor de **rxCube** es un *objeto rxCube*, que representa una tabulación cruzada. 
  
2. Llame a [rxResultsDF](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxresultsdf) función para convertir los resultados en una trama de datos que puede usarse fácilmente en una de las funciones de trazado estándar de R.
  
    ```R
    cubePlot <- rxResultsDF(cube1)
    ```
  
    El **rxCube** función incluye un argumento opcional, *returnDataFrame* = **TRUE**, que puede usar para convertir los resultados en una trama de datos directamente. Por ejemplo:
    
    `print(rxCube(fraudRisk~F(numTrans):F(numIntlTrans), data = sqlFraudDS, returnDataFrame = TRUE))`
       
    Sin embargo, la salida de **rxResultsDF** es más limpio y conserva los nombres de las columnas de origen. Puede ejecutar `head(cube1)` seguido `head(cubePlot)` para comparar la salida.
  
3. Crear un mapa térmico mediante la **levelplot** funcionar desde el **lattice** paquete, que se incluye con todas las distribuciones de R.
  
    ```R
    levelplot(fraudRisk~numTrans*numIntlTrans, data = cubePlot)
    ```
  
    **Resultado**
  
    ![resultados del gráfico de dispersión](media/rsql-sue-scatterplotresults.jpg "resultados del gráfico de dispersión")
  
En este análisis rápido, puede ver que aumenta el riesgo de fraude con el número de transacciones y el número de transacciones internacionales.

Para obtener más información sobre la **rxCube** en general, consulte la función y las referencias cruzadas [resúmenes de los datos con RevoScaleR](https://docs.microsoft.com/machine-learning-server/r/how-to-revoscaler-data-summaries).

## <a name="next-steps"></a>Pasos siguientes

> [!div class="nextstepaction"]
> [Crear modelos de R con datos de SQL Server](../../advanced-analytics/tutorials/deepdive-create-models.md)