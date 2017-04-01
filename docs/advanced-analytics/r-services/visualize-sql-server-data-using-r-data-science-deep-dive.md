---
title: "Visualizar datos de SQL Server con R (An&#225;lisis detallado de ciencia de datos) | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to: 
  - "SQL Server 2016"
dev_langs: 
  - "R"
ms.assetid: 10def0b3-9b09-4df9-b8aa-69516f7d7659
caps.latest.revision: 14
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
---
# Visualizar datos de SQL Server con R (An&#225;lisis detallado de ciencia de datos)
Los paquetes mejorados en [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] incluyen varias funciones que se han optimizado para la escalabilidad y el procesamiento paralelo. Normalmente, estas funciones incluyen el prefijo *rx* o *Rx*.  
  
En esta visita guiada usará la función *rxHistogram* para ver la distribución de valores de la columna _creditLine_ por género.  
  
## Visualizar datos con rxHistogram y rxCube  
  
1.  Use el siguiente código de R para llamar a la función *rxHistogram* y pasar una fórmula y un origen de datos. Puede ejecutar esto localmente en primer lugar para ver los resultados esperados y cuánto tarda.
  
    ```R  
    rxHistogram(~creditLine|gender, data = sqlFraudDS,  histType = "Percent")   
    ```  
 
    De manera interna, *rxHistogram* llama a la función *rxCube*, que se incluye en el paquete **RevoScaleR**. La función *rxCube* genera una única lista (o trama de datos) que contiene una columna para cada variable que se ha especificado en la fórmula, además de una columna de recuento.
    
2. Ahora, establezca el contexto de cálculo en el equipo remoto de SQL Server y ejecute *rxHistogram* de nuevo.
  
    ```R  
    rxSetComputeContext(sqlCompute)  
    ```  
 
3.    Los resultados son exactamente los mismos ya que está usando el mismo origen de datos. En cambio, los cálculos se realizan en el equipo de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  Después, los resultados se devuelven a la estación de trabajo local para el trazado.  
   
![histogram results](../../advanced-analytics/r-services/media/rsql-sue-histogramresults.jpg "histogram results")  

  
4.  También puede llamar a la función *rxCube* y pasar los resultados a una función de trazado de R.  Por ejemplo, el siguiente ejemplo usa *rxCube* para calcular la media de *fraudRisk* de cada combinación de *numTrans* y *numIntlTrans*:  
  
    ```R  
    cube1 <- rxCube(fraudRisk~F(numTrans):F(numIntlTrans),  data = sqlFraudDS)   
    ```  
  
    Para especificar los grupos que se han usado para calcular medias de grupo, use la notación `F()`. En este ejemplo, `F(numTrans):F(numIntlTrans)` indica que los enteros de las variables _numTrans_ y _numIntlTrans_ deben tratarse como variables categóricas, con un nivel para cada valor entero.  
  
    Como ya se han agregado los niveles superior e inferior al origen de datos *sqlFraudDS* (mediante el parámetro *colInfo*), los niveles se usarán automáticamente en el histograma.  
  
5.  El valor devuelto de *rxCube* es, de manera predeterminada, un *objeto rxCube* que representa una tabulación cruzada. En cambio, puede usar la función *rxResultsDF* para convertir los resultados en una trama de datos que pueda usarse fácilmente en una de las funciones de trazado estándar de R.  
  
    ```R  
    cubePlot <- rxResultsDF(cube1)   
    ```  
  
    > [!TIP]  
    > Tenga en cuenta que la función *rxCube* incluye un argumento opcional, *returnDataFrame* = TRUE, que puede usar para convertir los resultados en una trama de datos directamente. Por ejemplo:  
    >   
    > `print(rxCube(fraudRisk~F(numTrans):F(numIntlTrans), data = sqlFraudDS, returnDataFrame = TRUE))`  
    >   
    > En cambio, el resultado de *rxResultsDF* es mucho más limpio y conserva los nombres de las columnas de origen.  
  
6.  Por último, ejecute el siguiente código para crear un mapa térmico mediante la función *levelplot* del paquete **lattice** que se incluye en todas las distribuciones de R.  
  
    ```R  
    levelplot(fraudRisk~numTrans*numIntlTrans, data = cubePlot)   
    ```  
  
    **Resultado**  
  
    ![scatterplot results](../../advanced-analytics/r-services/media/rsql-sue-scatterplotresults.jpg "scatterplot results")  
  
Incluso en este análisis rápido puede ver que aumenta el riesgo de fraude tanto en el número de transacciones como en el número de transacciones internacionales.

Para obtener más información general sobre la función *rxCube* y las referencias cruzadas, consulte [Resúmenes de datos](https://msdn.microsoft.com/microsoft-r/scaler-user-guide-data-summaries).  
  
## Paso siguiente  
[Create Models &#40;Data Science Deep Dive&#41; (Crear modelos &#40;Análisis detallado de ciencia de datos&#41;)](../../advanced-analytics/r-services/create-models-data-science-deep-dive.md)  
  
## Paso anterior  
[Lesson 2: Create and Run R Scripts &#40;Data Science Deep Dive&#41; (Lección 2: Crear y ejecutar scripts de R &#40;Análisis detallado de ciencia de datos&#41;)](../../advanced-analytics/r-services/lesson-2-create-and-run-r-scripts-data-science-deep-dive.md)  
  
## Vea también  
[Análisis detallado de ciencia de datos: Usar los paquetes de RevoScaleR](../../advanced-analytics/r-services/data-science-deep-dive-using-the-revoscaler-packages.md)  
  
  
  
