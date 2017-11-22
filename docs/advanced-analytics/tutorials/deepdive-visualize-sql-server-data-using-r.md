---
title: "Visualizar datos de SQL Server con R (Análisis detallado de ciencia de datos) | Microsoft Docs"
ms.custom: SQL2016_New_Updated
ms.date: 05/18/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to: SQL Server 2016
dev_langs: R
ms.assetid: 10def0b3-9b09-4df9-b8aa-69516f7d7659
caps.latest.revision: "14"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: a67480daf011a021002e1688b006a1f0593f8e5f
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2017
---
# <a name="visualize-sql-server-data-using-r"></a>Visualizar datos de SQL Server con R

Los paquetes mejorados en [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] incluyen varias funciones que se han optimizado para la escalabilidad y el procesamiento paralelo. Normalmente, estas funciones incluyen el prefijo *rx* o *Rx*.

En esta visita guiada usará la función **rxHistogram** para ver la distribución de valores de la columna _creditLine_ por género.

## <a name="visualize-data-using-rxhistogram"></a>Visualizar datos mediante rxHistogram

1. Utilizar el siguiente código R para llamar a la función rxHistogram y pasar un fórmula y origen de datos. Puede ejecutar esto localmente en primer lugar para ver los resultados esperados y cuánto tarda.
  
    ```R
    rxHistogram(~creditLine|gender, data = sqlFraudDS,  histType = "Percent")
    ```
 
    Internamente, rxHistogram llama a la función rxCube, que se incluye en el **RevoScaleR** paquete. La función rxCube genera una sola lista (o una trama de datos) que contiene una columna para cada variable especificada en la fórmula, además de una columna de números.
    
2. Ahora, establecer el contexto de proceso en el equipo remoto de SQL Server y vuelva a ejecutar rxHistogram.
  
    ```R
    rxSetComputeContext(sqlCompute)
    ```
 
3. Los resultados son exactamente los mismos ya que está usando el mismo origen de datos. En cambio, los cálculos se realizan en el equipo de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  Después, los resultados se devuelven a la estación de trabajo local para el trazado.
   
![resultados del histograma](media/rsql-sue-histogramresults.jpg "resultados del histograma")

4. También puede llamar a la función rxCube y pasar los resultados a una función de trazado de R.  Por ejemplo, en el ejemplo siguiente se utiliza rxCube para calcular la media de *fraudRisk* para cada combinación de *numTrans* y *numIntlTrans*:
  
    ```R
    cube1 <- rxCube(fraudRisk~F(numTrans):F(numIntlTrans),  data = sqlFraudDS)
    ```
  
    Para especificar los grupos que se han usado para calcular medias de grupo, use la notación `F()` . En este ejemplo, `F(numTrans):F(numIntlTrans)` indica que los enteros de las variables _numTrans_ y _numIntlTrans_ deben tratarse como variables categóricas, con un nivel para cada valor entero.
  
    Como ya se han agregado los niveles superior e inferior al origen de datos *sqlFraudDS* (mediante el parámetro *colInfo* ), los niveles se usarán automáticamente en el histograma.
  
5. El valor devuelto de rxCube es de forma predeterminada un *rxCube objeto*, que representa una tabulación cruzada. En cambio, puede usar la función **rxResultsDF** para convertir los resultados en una trama de datos que pueda usarse fácilmente en una de las funciones de trazado estándar de R.
  
    ```R
    cubePlot <- rxResultsDF(cube1)
    ```
  
    > [!TIP]
    > 
    > Tenga en cuenta que la función rxCube incluye un argumento opcional, *returnDataFrame* = TRUE, que puede utilizar para convertir los resultados en una trama de datos directamente. Por ejemplo:
    >   
    > `print(rxCube(fraudRisk~F(numTrans):F(numIntlTrans), data = sqlFraudDS, returnDataFrame = TRUE))`
    >   
    > Sin embargo, la salida de rxResultsDF es mucho más limpia y conserva los nombres de las columnas de origen.
  
6. Por último, ejecute el código siguiente para crear un mapa de calor mediante la `levelplot` funcionar desde el **celosía** paquete, que se incluye con todas las distribuciones de R.
  
    ```R
    levelplot(fraudRisk~numTrans*numIntlTrans, data = cubePlot)
    ```
  
    **Resultado**
  
    ![resultados del gráfico de dispersión](media/rsql-sue-scatterplotresults.jpg "resultados del gráfico de dispersión")
  
Incluso en este análisis rápido puede ver que aumenta el riesgo de fraude tanto en el número de transacciones como en el número de transacciones internacionales.

Para obtener más información sobre la función de rxCube y referencias cruzadas en general, vea [resúmenes de los datos](https://msdn.microsoft.com/microsoft-r/scaler-user-guide-data-summaries).

## <a name="next-step"></a>Paso siguiente

[Crear modelos](../../advanced-analytics/tutorials/deepdive-create-models.md)

## <a name="previous-step"></a>Paso anterior

[Lección 2: Crear y ejecutar scripts de R](../../advanced-analytics/tutorials/deepdive-create-and-run-r-scripts.md)


