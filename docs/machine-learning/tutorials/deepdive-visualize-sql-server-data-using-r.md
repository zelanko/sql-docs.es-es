---
title: Visualización de datos mediante RevoScaleR
description: Aprenda a usar funciones de R para visualizar la distribución de valores de la columna creditLine por género.
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 23f3eb157a76a9a197cf0f15a72ae0e51f7cf13b
ms.sourcegitcommit: 9b41725d6db9957dd7928a3620fe4db41eb51c6e
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/13/2020
ms.locfileid: "88180392"
---
#  <a name="visualize-sql-server-data-using-r-sql-server-and-revoscaler-tutorial"></a>Visualizar datos de SQL Server mediante R (tutorial de SQL Server y RevoScaleR)
[!INCLUDE [SQL Server 2016 and later](../../includes/applies-to-version/sqlserver2016.md)]

Este es el tutorial 6 de la [serie de tutoriales de RevoScaleR](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md) sobre el uso de las [funciones de RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) con SQL Server.

En este tutorial, usará funciones de R para ver la distribución de valores de la columna *creditLine* por género.

> [!div class="checklist"]
> * Creación de variables mínimo-máximo para entradas de histograma
> * Visualización de datos en un histograma mediante **rxHistogram** de **RevoScaleR**
> * Visualización de gráficos de dispersión con **levelplot** de **lattice** incluido en la distribución de R base

Como se muestra en este tutorial, puede combinar funciones de código abierto y específicas de Microsoft en el mismo script.

## <a name="add-maximum-and-minimum-values"></a>Adición de valores máximos y mínimos

Según las estadísticas de resumen calculadas del tutorial anterior, ha descubierto alguna información útil sobre los datos que quiere insertar en el origen de datos para llevar a cabo cálculos adicionales. Por ejemplo, puede usar los valores mínimos y máximos para calcular histogramas. En este ejercicio, agregará los valores máximos y mínimos al origen de datos **RxSqlServerData**.

1. Empiece por configurar algunas variables temporales.
  
    ```R
    sumDF <- sumOut$sDataFrame
    var <- sumDF$Name
    ```
  
2. Use la variable *ccColInfo* que ha creado en el tutorial anterior para definir las columnas del origen de datos.
  
   Agregue nuevas columnas calculadas (*numTrans*, *numIntlTrans* y *creditLine*) a la colección de columnas que reemplazan la definición original. El siguiente script agrega factores basados en los valores mínimos y máximos, obtenidos de sumOut, que almacena la salida en memoria de **rxSummary**. 
  
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
  
3. Después de actualizar la colección de columnas, aplique la siguiente instrucción para crear una versión actualizada del origen de datos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que ha definido anteriormente.
  
    ```R
    sqlFraudDS <- RxSqlServerData(
        connectionString = sqlConnString,
        table = sqlFraudTable,
        colInfo = ccColInfo,
        rowsPerRead = sqlRowsPerRead)
    ```
  
    El origen de datos sqlFraudDS ahora incluye las nuevas columnas que ha agregado mediante *ccColInfo*.
  
En este momento, las modificaciones solo afectan al objeto de origen de datos en R; aún no se ha escrito ningún dato nuevo en la tabla de la base de datos. En cambio, puede usar los datos que se han capturado en la variable sumOut para crear visualizaciones y resúmenes. 

> [!TIP]
> Si olvida qué contexto de proceso está usando, ejecute **rxGetComputeContext()** . El valor devuelto "RxLocalSeq Compute Context" indica que se está ejecutando en el contexto de proceso local.

## <a name="visualize-data-using-rxhistogram"></a>Visualización de los datos mediante rxHistogram

1. Use el siguiente código de R para llamar a la función [rxHistogram](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxhistogram) y pasar una fórmula y un origen de datos. Puede ejecutar esto localmente en primer lugar para ver los resultados esperados y cuánto tarda.
  
    ```R
    rxHistogram(~creditLine|gender, data = sqlFraudDS,  histType = "Percent")
    ```
 
    De manera interna, **rxHistogram** llama a la función [rxCube](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxcube) , que se incluye en el paquete **RevoScaleR** . **rxCube** genera una única lista (o trama de datos) que contiene una columna para cada variable que se ha especificado en la fórmula, además de una columna de recuentos.
    
2. Ahora, establezca el contexto de proceso en el equipo remoto de SQL Server y ejecute **rxHistogram** de nuevo.
  
    ```R
    rxSetComputeContext(sqlCompute)
    rxHistogram(~creditLine|gender, data = sqlFraudDS,  histType = "Percent")
    ```
 
3. Los resultados son exactamente los mismos, ya que está usando el mismo origen de datos, pero, en el segundo paso, los cálculos se realizan en el servidor remoto. Después, los resultados se devuelven a la estación de trabajo local para el trazado.
   
  ![resultados del histograma](media/rsql-sue-histogramresults.jpg "resultados del histograma")


## <a name="visualize-with-scatter-plots"></a>Visualización con gráficos de dispersión

Los gráficos de dispersión se suelen usar durante la exploración de datos para comparar la relación entre dos variables. Puede usar paquetes de R integrados con este fin; las funciones de **RevoScaleR** proporcionarán las entradas.

1. Llame a la función [rxCube](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxcrosstabs) para calcular la media de *fraudRisk* de cada combinación de *numTrans* y *numIntlTrans*:
  
    ```R
    cube1 <- rxCube(fraudRisk~F(numTrans):F(numIntlTrans),  data = sqlFraudDS)
    ```
  
    Para especificar los grupos que se han usado para calcular medias de grupo, use la notación `F()` . En este ejemplo, `F(numTrans):F(numIntlTrans)` indica que los enteros de las variables `numTrans` y `numIntlTrans` deben tratarse como variables categóricas, con un nivel para cada valor entero.
  
    El valor devuelto predeterminado de **rxCube** es un *objeto rxCube* que representa una tabulación cruzada. 
  
2. Llame a la función [rxResultsDF](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxresultsdf) para convertir los resultados en una trama de datos que pueda usarse fácilmente en una de las funciones de trazado estándar de R.
  
    ```R
    cubePlot <- rxResultsDF(cube1)
    ```
  
    La función **rxCube** incluye un argumento opcional, *returnDataFrame* = **TRUE**, que puede usar para convertir los resultados en una trama de datos directamente. Por ejemplo:
    
    `print(rxCube(fraudRisk~F(numTrans):F(numIntlTrans), data = sqlFraudDS, returnDataFrame = TRUE))`
       
    En cambio, el resultado de **rxResultsDF** es más limpio y conserva los nombres de las columnas de origen. Puede ejecutar `head(cube1)` seguido de `head(cubePlot)` para comparar el resultado.
  
3. Cree un mapa térmico mediante la función **levelplot** del paquete **lattice** que se incluye en todas las distribuciones de R.
  
    ```R
    levelplot(fraudRisk~numTrans*numIntlTrans, data = cubePlot)
    ```
  
    **Resultados**
  
    ![resultados del gráfico de dispersión](media/rsql-sue-scatterplotresults.jpg "resultados del gráfico de dispersión")
  
En este análisis rápido puede ver que aumenta el riesgo de fraude tanto en el número de transacciones como en el número de transacciones internacionales.

Para más información sobre la función **rxCube** y las referencias cruzadas, vea [Resúmenes de datos mediante RevoScaleR](https://docs.microsoft.com/machine-learning-server/r/how-to-revoscaler-data-summaries).

## <a name="next-steps"></a>Pasos siguientes

> [!div class="nextstepaction"]
> [Creación de modelos de R con datos de SQL Server](../../machine-learning/tutorials/deepdive-create-models.md)