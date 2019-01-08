---
title: DAY (expresión de SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- DAY function
- dates [Integration Services], DAY
ms.assetid: d8447187-49df-45b7-a98e-142ad44fd3e2
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 8d530819e235efd233df3247d2e85d7da8c2cf1d
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/03/2018
ms.locfileid: "52805137"
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
  
 Un literal de tipo fecha debe convertirse explícitamente en uno de los tipos de datos de fecha. Para obtener más información, vea [Integration Services Data Types](../data-flow/integration-services-data-types.md).  
  
> [!NOTE]  
>  La expresión no puede validarse cuando un literal de fecha se convierte explícitamente a uno de estos tipos de datos de fecha: DT_DBTIMESTAMPOFFSET y DT_DBTIMESTAMP2.  
  
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
 [DATEADD &#40;expresión de SSIS&#41;](dateadd-ssis-expression.md)   
 [DATEDIFF &#40;expresión de SSIS&#41;](datediff-ssis-expression.md)   
 [DATEPART &#40;expresión de SSIS&#41;](datepart-ssis-expression.md)   
 [MONTH &#40;expresión de SSIS&#41;](month-ssis-expression.md)   
 [YEAR &#40;expresión de SSIS&#41;](year-ssis-expression.md)   
 [Funciones &#40;expresión de SSIS&#41;](functions-ssis-expression.md)  
  
  
