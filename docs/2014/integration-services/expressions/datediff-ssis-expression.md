---
title: DATEDIFF (expresión de SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- DATEDIFF statement
- dates [Integration Services], DATEDIFF
ms.assetid: 449b327f-47c7-4709-8bc6-4ee9a35cc330
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 790cfc41d4ff4b1cd3265f9a0042a6822a546ddc
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/03/2018
ms.locfileid: "52810127"
---
# <a name="datediff-ssis-expression"></a>DATEDIFF (expresión de SSIS)
  Devuelve el número de límites de fecha y hora entre dos fechas especificadas. El parámetro *datepart* identifica los límites de fecha y hora que se van a comparar.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
DATEDIFF(datepart, startdate, endate)  
```  
  
## <a name="arguments"></a>Argumentos  
 *datepart*  
 Parámetro que especifica la parte de la fecha que se va a comparar y para la que se devuelve un valor.  
  
 *startdate*  
 Fecha de inicio del intervalo.  
  
 *endate*  
 Fecha de finalización del intervalo.  
  
## <a name="result-types"></a>Tipos de resultado  
 DT_I4  
  
## <a name="remarks"></a>Comentarios  
 En la tabla siguiente se incluyen las partes de fecha y las abreviaturas reconocidas por el evaluador de expresiones.  
  
|datepart|Abreviaturas|  
|--------------|-------------------|  
|Year|yy, yyyy|  
|Trimestre|qq, q|  
|Month|mm, m|  
|Dayofyear|dy, y|  
|Day|dd, d|  
|Semana|wk, ww|  
|Weekday|dw, w|  
|Hour|Hh|  
|Minute|mi, n|  
|Second|ss, s|  
|Millisecond|Ms|  
  
 DATEDIFF devuelve un resultado NULL si alguno de los argumentos es NULL.  
  
 Un literal de tipo fecha debe convertirse explícitamente en uno de los tipos de datos de fecha. Para obtener más información, vea [Integration Services Data Types](../data-flow/integration-services-data-types.md).  
  
 Se produce un error si una fecha no es válida, si la fecha o unidad de tiempo no es una cadena, si la fecha de inicio no es una fecha o si la fecha de finalización no es una fecha.  
  
 Si la fecha de finalización es anterior a la fecha de inicio, la función devuelve un número negativo. Si las fechas de inicio y de finalización coinciden o están dentro del mismo intervalo, la función devuelve cero.  
  
## <a name="ssis-expression-examples"></a>Ejemplos de expresiones de SSIS  
 Este ejemplo calcula el número de días entre dos literales de fecha. Si la fecha tiene el formato "mm/dd/aaaa", la función devuelve 7.  
  
```  
DATEDIFF("dd", (DT_DBTIMESTAMP)"8/1/2003", (DT_DBTIMESTAMP)"8/8/2003")  
```  
  
 Este ejemplo devuelve el número de meses entre un literal de fecha y la fecha actual.  
  
```  
DATEDIFF("mm", (DT_DBTIMESTAMP)"8/1/2003",GETDATE())  
```  
  
 Este ejemplo devuelve el número de semanas entre la fecha de la columna **ModifiedDate** y la variable **YearEndDate** . Si **YearEndDate** tiene un `date` tipo de datos, se requiere ninguna conversión explícita.  
  
```  
DATEDIFF("Week", ModifiedDate,@YearEndDate)  
```  
  
## <a name="see-also"></a>Vea también  
 [DATEADD &#40;expresión de SSIS&#41;](dateadd-ssis-expression.md)   
 [DATEPART &#40;expresión de SSIS&#41;](datepart-ssis-expression.md)   
 [DAY &#40;expresión de SSIS&#41;](day-ssis-expression.md)   
 [MONTH &#40;expresión de SSIS&#41;](month-ssis-expression.md)   
 [YEAR &#40;expresión de SSIS&#41;](year-ssis-expression.md)   
 [Funciones &#40;expresión de SSIS&#41;](functions-ssis-expression.md)  
  
  
