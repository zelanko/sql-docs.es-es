---
title: Analizar los datos de contexto de proceso Local | Documentos de Microsoft
ms.custom: 
ms.date: 05/18/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
dev_langs:
- R
ms.assetid: 787bb526-4a13-40fa-9343-75d3bf5ba6a2
caps.latest.revision: 13
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 1efbf5b6d3835759ccce74c820ea2829e6fa41dc
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="analyze-data-in-local-compute-context-data-science-deep-dive"></a>Analizar los datos de contexto de proceso Local (datos ciencia profundización)

Aunque puede ser más rápido ejecutar código R complejo utilizando el contexto de servidor, a veces es simplemente más cómodo obtener los datos fuera de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y analizar en la estación de trabajo privada.

En esta sección aprenderá a volver a un contexto de proceso local y a mover datos entre contextos para optimizar el rendimiento.

## <a name="create-a-local-summary"></a>Crear un resumen local

1. Cambie el contexto de proceso para hacer todo el trabajo localmente.
  
    ```R
    rxSetComputeContext ("local")
    ```
  
2. Al extraer datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], a menudo puede conseguir un mejor rendimiento si aumenta el número de filas que se extraen para cada lectura.  Para ello, aumente el valor del parámetro *rowsPerRead* en el origen de datos.
  
    ```R
    sqlServerDS1 <- RxSqlServerData(
       connectionString = sqlConnString,
       table = sqlFraudTable,
       colInfo = ccColInfo,
       rowsPerRead = 10000)
    ```
  
    Antes, el valor de *rowsPerRead* estaba establecido en 5000.
  
3. Ahora, llame a **rxSummary** en el nuevo origen de datos.
  
    ```R
    rxSummary(formula = ~gender + balance + numTrans + numIntlTrans + creditLine, data = sqlServerDS1)
    ```
  
    Los resultados reales deben ser el mismo que al ejecutar rxSummary en el contexto de la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] equipo.  En cambio, la operación puede ser más rápida o más lenta. Depende en gran medida de la conexión a la base de datos, ya que los datos se transfieren al equipo local para el análisis.


## <a name="next--step"></a>Paso siguiente

[Mover datos entre SQL Server y el archivo xdf.](../../advanced-analytics/tutorials/deepdive-move-data-between-sql-server-and-xdf-file.md)

## <a name="previous-step"></a>Paso anterior

[Realizar análisis de fragmentación con rxDataStep](../../advanced-analytics/tutorials/deepdive-perform-chunking-analysis-using-rxdatastep.md)



