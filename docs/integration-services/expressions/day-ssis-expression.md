---
title: "DAY (expresión de SSIS) | Documentos de Microsoft"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- DAY function
- dates [Integration Services], DAY
ms.assetid: d8447187-49df-45b7-a98e-142ad44fd3e2
caps.latest.revision: 38
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 5e297f7021239ded4aa76ad61e75fddba528ccf6
ms.contentlocale: es-es
ms.lasthandoff: 08/03/2017

---
# <a name="day-ssis-expression"></a>DAY (expresión de SSIS)
  Devuelve un entero que representa la parte del día de una fecha.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
DAY(date)  
```  
  
## <a name="arguments"></a>Argumentos  
 *date*  
 Expresión que devuelve una fecha válida o una cadena con formato de fecha.  
  
## <a name="result-types"></a>Tipos de resultado  
 DT_I4  
  
## <a name="remarks"></a>Comentarios  
 DAY devuelve un resultado NULL si el valor del argumento es NULL.  
  
 Un literal de tipo fecha debe convertirse explícitamente en uno de los tipos de datos de fecha. Para más información, consulte [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md).  
  
> [!NOTE]  
>  La expresión no puede validarse cuando un literal de fecha se convierte explícitamente en uno de estos tipos de datos de fecha: DT_DBTIMESTAMPOFFSET y DT_DBTIMESTAMP2.  
  
 Utilizar la función DAY es más sencillo pero equivalente a utilizar la función DATEPART("Day", date).  
  
## <a name="expression-examples"></a>Ejemplos de expresiones  
 Este ejemplo devuelve el número del día de un literal de fecha. Si la fecha tiene el formato "mm/dd/aaaa", este ejemplo devuelve 23.  
  
```  
DAY((DT_DBTIMESTAMP)"11/23/2002")  
```  
  
 Este ejemplo devuelve el entero que representa el día en la columna **ModifiedDate** .  
  
```  
DAY(ModifiedDate)  
```  
  
 Este ejemplo devuelve el entero que representa el día de la fecha actual.  
  
```  
DAY(GETDATE())  
```  
  
## <a name="see-also"></a>Vea también  
 [DATEADD &#40; Expresión de SSIS &#41;](../../integration-services/expressions/dateadd-ssis-expression.md)   
 [DATEDIFF &#40; Expresión de SSIS &#41;](../../integration-services/expressions/datediff-ssis-expression.md)   
 [DATEPART &#40; Expresión de SSIS &#41;](../../integration-services/expressions/datepart-ssis-expression.md)   
 [MES &#40; Expresión de SSIS &#41;](../../integration-services/expressions/month-ssis-expression.md)   
 [AÑO &#40; Expresión de SSIS &#41;](../../integration-services/expressions/year-ssis-expression.md)   
 [Funciones &#40; Expresión de SSIS &#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  
