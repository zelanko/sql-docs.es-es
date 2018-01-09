---
title: " Visualizar datos de SQL Server con R (SQL y R profundización) | Documentos de Microsoft"
ms.date: 12/14/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: 
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: tutorial
applies_to:
- SQL Server 2016
- SQL Server 2017
dev_langs: R
ms.assetid: 10def0b3-9b09-4df9-b8aa-69516f7d7659
caps.latest.revision: "14"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: 575212c27cf82cd55e085fc0760839c28b4695be
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/08/2018
---
#  <a name="visualize-sql-server-data-using-r-sql-and-r-deep-dive"></a>Visualizar datos de SQL Server con R (SQL y R profundización)

Este artículo forma parte del tutorial exhaustiva de ciencia de datos, acerca de cómo usar [RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) con SQL Server.

Los paquetes mejorados en [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] incluyen varias funciones que se han optimizado para la escalabilidad y el procesamiento paralelo. Normalmente, estas funciones incluyen el prefijo **rx** o **Rx**.

En este tutorial, use la **rxHistogram** función para ver la distribución de valores en el _creditLine_ columna por género.

## <a name="visualize-data-using-rxhistogram"></a>Visualizar datos mediante rxHistogram

1. Use el siguiente código de R para llamar a la función [rxHistogram](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxhistogram) y pasar una fórmula y un origen de datos. Puede ejecutar esto localmente en primer lugar para ver los resultados esperados y cuánto tarda.
  
    ```R
    rxHistogram(~creditLine|gender, data = sqlFraudDS,  histType = "Percent")
    ```
 
    De manera interna, **rxHistogram** llama a la función [rxCube](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxcube) , que se incluye en el paquete **RevoScaleR** . **rxCube** genera una sola lista (o una trama de datos) que contiene una columna para cada variable especificada en la fórmula, además de una columna de números.
    
2. Ahora, establecer el contexto de proceso en el equipo remoto de SQL Server y ejecute **rxHistogram** nuevo.
  
    ```R
    rxSetComputeContext(sqlCompute)
    ```
 
3. Los resultados son exactamente los mismos ya que está usando el mismo origen de datos. En cambio, los cálculos se realizan en el equipo de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  Después, los resultados se devuelven a la estación de trabajo local para el trazado.
   
![resultados del histograma](media/rsql-sue-histogramresults.jpg "resultados del histograma")

4. También puede llamar a la **rxCube** función y pasar los resultados a un R trazar la función.  Por ejemplo, el siguiente ejemplo usa **rxCube** para calcular la media de *fraudRisk* de cada combinación de *numTrans* y *numIntlTrans*:
  
    ```R
    cube1 <- rxCube(fraudRisk~F(numTrans):F(numIntlTrans),  data = sqlFraudDS)
    ```
  
    Para especificar los grupos que se han usado para calcular medias de grupo, use la notación `F()` . En este ejemplo, `F(numTrans):F(numIntlTrans)` indica que los enteros en las variables `_numTrans` y `numIntlTrans` deben tratarse como variables de categorías, con un nivel para cada valor entero.
  
    Dado que los niveles inferiores y superiores ya se han agregado al origen de datos `sqlFraudDS` (mediante el `colInfo` parámetro), automáticamente se usan los niveles en el histograma.
  
5. El valor predeterminado devuelve el valor de **rxCube** es un *rxCube objeto*, que representa una tabulación cruzada. En cambio, puede usar la función [rxResultsDF](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxresultsdf) para convertir los resultados en una trama de datos que pueda usarse fácilmente en una de las funciones de trazado estándar de R.
  
    ```R
    cubePlot <- rxResultsDF(cube1)
    ```
  
    El **rxCube** función incluye un argumento opcional, *returnDataFrame* = **TRUE**, que puede usar para convertir los resultados en una trama de datos directamente. Por ejemplo:
    
    `print(rxCube(fraudRisk~F(numTrans):F(numIntlTrans), data = sqlFraudDS, returnDataFrame = TRUE))`
       
    En cambio, el resultado de **rxResultsDF** es mucho más limpio y conserva los nombres de las columnas de origen.
  
6. Por último, ejecute el código siguiente para crear un mapa de calor mediante la `levelplot` funcionar desde el **celosía** paquete, que se incluye con todas las distribuciones de R.
  
    ```R
    levelplot(fraudRisk~numTrans*numIntlTrans, data = cubePlot)
    ```
  
    **Resultado**
  
    ![resultados del gráfico de dispersión](media/rsql-sue-scatterplotresults.jpg "resultados del gráfico de dispersión")
  
Incluso en este análisis rápido puede ver que aumenta el riesgo de fraude tanto en el número de transacciones como en el número de transacciones internacionales.

Para obtener más información sobre la **rxCube** función y referencias cruzadas en general, vea [resúmenes de los datos con RevoScaleR](https://docs.microsoft.com/machine-learning-server/r/how-to-revoscaler-data-summaries).

## <a name="next-step"></a>Paso siguiente

[Crear modelos en R mediante datos de SQL Server](../../advanced-analytics/tutorials/deepdive-create-models.md)

## <a name="previous-step"></a>Paso anterior

[Crear y ejecutar scripts de R](../../advanced-analytics/tutorials/deepdive-create-and-run-r-scripts.md)
