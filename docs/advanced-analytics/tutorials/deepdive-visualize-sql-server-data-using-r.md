---
title: Visualizar datos de SQL Server con R (análisis detallado R y SQL) | Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 0d34ece68c421dbb7aabd845e117c9f07e00d013
ms.sourcegitcommit: 2420c57d2952add3697dbe0467ee1d755c5c2ee5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/26/2018
ms.locfileid: "47217520"
---
#  <a name="visualize-sql-server-data-using-r-sql-and-r-deep-dive"></a>Visualizar datos de SQL Server con R (análisis detallado SQL y R)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Este artículo forma parte del tutorial de análisis detallado de ciencia de datos, acerca de cómo usar [RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) con SQL Server.

Los paquetes mejorados en [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] incluyen varias funciones que se han optimizado para la escalabilidad y el procesamiento paralelo. Normalmente, estas funciones incluyen el prefijo **rx** o **Rx**.

Para este tutorial, se usa el **rxHistogram** función para ver la distribución de valores en el _creditLine_ columna por género.

## <a name="visualize-data-using-rxhistogram"></a>Visualizar datos con rxHistogram

1. Use el siguiente código de R para llamar a la función [rxHistogram](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxhistogram) y pasar una fórmula y un origen de datos. Puede ejecutar esto localmente en primer lugar para ver los resultados esperados y cuánto tarda.
  
    ```R
    rxHistogram(~creditLine|gender, data = sqlFraudDS,  histType = "Percent")
    ```
 
    De manera interna, **rxHistogram** llama a la función [rxCube](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxcube) , que se incluye en el paquete **RevoScaleR** . **rxCube** genera una única lista (o trama de datos) que contiene una columna para cada variable especificada en la fórmula, además de una columna de recuento.
    
2. Ahora, establezca el contexto de proceso en el equipo remoto de SQL Server y ejecute **rxHistogram** nuevo.
  
    ```R
    rxSetComputeContext(sqlCompute)
    ```
 
3. Los resultados son exactamente los mismos ya que está usando el mismo origen de datos. En cambio, los cálculos se realizan en el equipo de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  Después, los resultados se devuelven a la estación de trabajo local para el trazado.
   
![resultados del histograma](media/rsql-sue-histogramresults.jpg "resultados del histograma")

4. También puede llamar a la **rxCube** de función y pasar los resultados a una función de trazado de R.  Por ejemplo, el siguiente ejemplo usa **rxCube** para calcular la media de *fraudRisk* de cada combinación de *numTrans* y *numIntlTrans*:
  
    ```R
    cube1 <- rxCube(fraudRisk~F(numTrans):F(numIntlTrans),  data = sqlFraudDS)
    ```
  
    Para especificar los grupos que se han usado para calcular medias de grupo, use la notación `F()` . En este ejemplo, `F(numTrans):F(numIntlTrans)` indica que los enteros de las variables `numTrans` y `numIntlTrans` deben tratarse como variables categóricas, con un nivel para cada valor entero.
  
    Dado que ya se han agregado los niveles superior e inferior al origen de datos `sqlFraudDS` (mediante el `colInfo` parámetro), se usan automáticamente los niveles en el histograma.
  
5. El valor predeterminado devuelve el valor de **rxCube** es un *objeto rxCube*, que representa una tabulación cruzada. En cambio, puede usar la función [rxResultsDF](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxresultsdf) para convertir los resultados en una trama de datos que pueda usarse fácilmente en una de las funciones de trazado estándar de R.
  
    ```R
    cubePlot <- rxResultsDF(cube1)
    ```
  
    El **rxCube** función incluye un argumento opcional, *returnDataFrame* = **TRUE**, que puede usar para convertir los resultados en una trama de datos directamente. Por ejemplo:
    
    `print(rxCube(fraudRisk~F(numTrans):F(numIntlTrans), data = sqlFraudDS, returnDataFrame = TRUE))`
       
    En cambio, el resultado de **rxResultsDF** es mucho más limpio y conserva los nombres de las columnas de origen.
  
6. Por último, ejecute el siguiente código para crear un mapa térmico mediante la `levelplot` funcionar desde el **lattice** paquete, que se incluye con todas las distribuciones de R.
  
    ```R
    levelplot(fraudRisk~numTrans*numIntlTrans, data = cubePlot)
    ```
  
    **Resultado**
  
    ![resultados del gráfico de dispersión](media/rsql-sue-scatterplotresults.jpg "resultados del gráfico de dispersión")
  
Incluso en este análisis rápido puede ver que aumenta el riesgo de fraude tanto en el número de transacciones como en el número de transacciones internacionales.

Para obtener más información sobre la **rxCube** en general, consulte la función y las referencias cruzadas [resúmenes de los datos con RevoScaleR](https://docs.microsoft.com/machine-learning-server/r/how-to-revoscaler-data-summaries).

## <a name="next-step"></a>Paso siguiente

[Crear modelos de R con datos de SQL Server](../../advanced-analytics/tutorials/deepdive-create-models.md)

## <a name="previous-step"></a>Paso anterior

[Crear y ejecutar scripts de R](../../advanced-analytics/tutorials/deepdive-create-and-run-r-scripts.md)
