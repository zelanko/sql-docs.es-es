---
title: "YEAR (expresión de SSIS) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: expressions
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- dates [Integration Services], YEAR
- YEAR function
ms.assetid: 9d88dead-ace8-44b9-b8e2-916c1842e155
caps.latest.revision: "35"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ea267c8f94fd2fb20c9c73bc29ec24820c0555a1
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/20/2017
---
# <a name="year-ssis-expression"></a>YEAR (expresión de SSIS)
  Devuelve un entero que representa la parte del año de una fecha.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
YEAR(date)  
```  
  
## <a name="arguments"></a>Argumentos  
 *date*  
 Fecha con cualquier formato de fecha.  
  
## <a name="result-types"></a>Tipos de resultado  
 DT_I4  
  
## <a name="remarks"></a>Comentarios  
 YEAR devuelve un resultado NULL si el valor del argumento es NULL.  
  
 Un literal de tipo fecha debe convertirse explícitamente en uno de los tipos de datos de fecha. Para más información, consulte [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md).  
  
> [!NOTE]  
>  La expresión no puede validarse cuando un literal de fecha se convierte explícitamente en uno de estos tipos de datos de fecha: DT_DBTIMESTAMPOFFSET y DT_DBTIMESTAMP2.  
  
 Utilizar la función YEAR es más sencillo pero equivalente a utilizar la función DATEPART("Year", date).  
  
## <a name="expression-examples"></a>Ejemplos de expresiones  
 Este ejemplo devuelve el número del año de un literal de fecha. Si la fecha tiene el formato mm/dd/aaaa, este ejemplo devuelve "2002".  
  
```  
YEAR((DT_DBTIMESTAMP)"11/23/2002")  
```  
  
 Este ejemplo devuelve el entero que representa el año en la columna **ModifiedDate** .  
  
```  
YEAR(ModifiedDate)  
```  
  
 Este ejemplo devuelve el entero que representa el año de la fecha actual.  
  
```  
YEAR(GETDATE())  
```  
  
## <a name="see-also"></a>Vea también  
 [DATEADD &#40;expresión de SSIS&#41;](../../integration-services/expressions/dateadd-ssis-expression.md)   
 [DATEDIFF &#40;expresión de SSIS&#41;](../../integration-services/expressions/datediff-ssis-expression.md)   
 [DATEPART &#40;expresión de SSIS&#41;](../../integration-services/expressions/datepart-ssis-expression.md)   
 [DAY &#40;expresión de SSIS&#41;](../../integration-services/expressions/day-ssis-expression.md)   
 [MONTH &#40;expresión de SSIS&#41;](../../integration-services/expressions/month-ssis-expression.md)   
 [Funciones &#40;expresión de SSIS&#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  
