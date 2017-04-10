---
title: "Lecci&#243;n 4: Analizar datos en el contexto del proceso local (An&#225;lisis detallado de ciencia de datos) | Microsoft Docs"
ms.custom: ""
ms.date: "10/03/2016"
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
ms.assetid: 787bb526-4a13-40fa-9343-75d3bf5ba6a2
caps.latest.revision: 13
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 12
---
# Lecci&#243;n 4: Analizar datos en el contexto del proceso local (An&#225;lisis detallado de ciencia de datos)
Aunque suele ser mucho más rápido ejecutar código R complejo usando el contexto de servidor, a veces es más cómodo extraer los datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y analizarlos en una estación de trabajo privada.  
  
En esta sección aprenderá a volver a un contexto de proceso local y a mover datos entre contextos para optimizar el rendimiento.  
  
## Crear un resumen local  
  
1.  Cambie el contexto de proceso para hacer todo el trabajo localmente.  
  
    ```R  
    rxSetComputeContext ("local")    
    ```  
  
2.  Al extraer datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], a menudo puede conseguir un mejor rendimiento si aumenta el número de filas que se extraen para cada lectura.  Para ello, aumente el valor del parámetro *rowsPerRead* en el origen de datos.  
  
    ```R  
    sqlServerDS1 <- RxSqlServerData(  
       connectionString = sqlConnString,        
       table = sqlFraudTable,   
       colInfo = ccColInfo,   
       rowsPerRead = 10000)  
    ```  
  
    Antes, el valor de *rowsPerRead* estaba establecido en 5000.  
  
3.  Ahora, llame a *rxSummary* en el nuevo origen de datos.  
  
    ```R  
    rxSummary(formula = ~gender + balance + numTrans + numIntlTrans + creditLine, data = sqlServerDS1)    
    ```  
  
    Los resultados actuales deben ser los mismos que cuando ejecuta *rxSummary* en el contexto del equipo de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  En cambio, la operación puede ser más rápida o más lenta. Depende en gran medida de la conexión a la base de datos, ya que los datos se transfieren al equipo local para el análisis.  
  

## Paso siguiente  
[Mover datos entre SQL Server y el archivo XDF &#40;Análisis detallado de ciencia de datos&#41;](../../advanced-analytics/r-services/move-data-between-sql-server-and-xdf-file-data-science-deep-dive.md)  
  
## Paso anterior  
[Realizar análisis de fragmentación mediante rxDataStep &#40;Análisis detallado de ciencia de datos&#41;](../../advanced-analytics/r-services/perform-chunking-analysis-using-rxdatastep-data-science-deep-dive.md)  
  
  
  
