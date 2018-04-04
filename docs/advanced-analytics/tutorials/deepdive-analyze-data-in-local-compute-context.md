---
title: Analizar los datos de contexto de proceso local (SQL y R profundización) | Documentos de Microsoft
ms.date: 12/18/2017
ms.reviewer: ''
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: ''
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: tutorial
applies_to:
- SQL Server 2016
- SQL Server 2017
dev_langs:
- R
ms.author: heidist
author: HeidiSteen
manager: cgronlun
ms.workload: Inactive
ms.openlocfilehash: e521ae9ab359ac210383cfb56ded80da4ed181ff
ms.sourcegitcommit: 059fc64ba858ea2adaad2db39f306a8bff9649c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/04/2018
---
# <a name="analyze-data-in-local-compute-context-sql-and-r-deep-dive"></a>Analizar los datos de contexto de proceso local (SQL y R profundización)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Este artículo forma parte del tutorial exhaustiva de ciencia de datos, acerca de cómo usar [RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) con SQL Server.

En esta sección, aprenderá a cambiar a un contexto de proceso local y mover datos entre los contextos para optimizar el rendimiento.

Aunque i puede ser más rápido ejecutar código R complejo utilizando el contexto de servidor, a veces resulta más cómodo obtener los datos fuera de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y analizarlos en una estación de trabajo local.

## <a name="create-a-local-summary"></a>Crear un resumen local

1. Cambie el contexto de proceso para hacer todo el trabajo localmente.
  
    ```R
    rxSetComputeContext ("local")
    ```
  
2. Al extraer datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], a menudo puede conseguir un mejor rendimiento si aumenta el número de filas que se extraen para cada lectura.  Para ello, aumente el valor del parámetro *rowsPerRead* en el origen de datos. Antes, el valor de *rowsPerRead* estaba establecido en 5000.
  
    ```R
    sqlServerDS1 <- RxSqlServerData(
       connectionString = sqlConnString,
       table = sqlFraudTable,
       colInfo = ccColInfo,
       rowsPerRead = 10000)
    ```

3. Llame a **rxSummary** en el nuevo origen de datos.
  
    ```R
    rxSummary(formula = ~gender + balance + numTrans + numIntlTrans + creditLine, data = sqlServerDS1)
    ```
  
    Los resultados actuales deben ser los mismos que cuando ejecuta **rxSummary** en el contexto del equipo de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  En cambio, la operación puede ser más rápida o más lenta. Depende en gran medida de la conexión a la base de datos, ya que los datos se transfieren al equipo local para el análisis.

## <a name="next-step"></a>Paso siguiente

[Mover datos entre SQL Server y el archivo xdf.](../../advanced-analytics/tutorials/deepdive-move-data-between-sql-server-and-xdf-file.md)

## <a name="previous-step"></a>Paso anterior

[Realizar análisis de fragmentación mediante rxDataStep](../../advanced-analytics/tutorials/deepdive-perform-chunking-analysis-using-rxdatastep.md)
