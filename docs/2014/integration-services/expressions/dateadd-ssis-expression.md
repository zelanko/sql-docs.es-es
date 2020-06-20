---
title: DATEADD (expresión de SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- dates [Integration Services], DATEADD
- dates [Integration Services]
- DATEADD function
ms.assetid: fa5c37b1-2ddc-4857-8f8e-f6d5643b654f
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 8eb32407c6e8fdd79593e7710a2bf1e332f5e4a9
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2020
ms.locfileid: "84966675"
---
# <a name="dateadd-ssis-expression"></a>DATEADD (expresión de SSIS)
  Devuelve un nuevo valor de tipo DT_DBTIMESTAMP tras agregar un número que representa una fecha o un intervalo de tiempo a la parte de fecha especificada de una fecha determinada. La evaluación del parámetro number debe devolver un entero y la del parámetro date debe devolver una fecha válida.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
DATEADD(datepart, number, date)  
```  
  
## <a name="arguments"></a>Argumentos  
 *datepart*  
 Parámetro que especifica a qué parte de la fecha se agregará un número.  
  
 *número*  
 Valor que se usa para incrementar *datepart*. El valor debe ser de tipo entero y debe conocerse al analizar la expresión.  
  
 *date*  
 Expresión que devuelve una fecha válida o una cadena con formato de fecha.  
  
## <a name="result-types"></a>Tipos de resultado  
 DT_DBTIMESTAMP  
  
## <a name="remarks"></a>Observaciones  
 En la tabla siguiente se incluyen las partes de fecha y las abreviaturas reconocidas por el evaluador de expresiones. En los nombres de partes de fecha no se distinguen mayúsculas de minúsculas.  
  
|parte de fecha|Abreviaturas|  
|--------------|-------------------|  
|Year|yy, yyyy|  
|Trimestre|qq, q|  
|Month|mm, m|  
|Dayofyear|dy, y|  
|Día|dd, d|  
|Semana|wk, ww|  
|Día de la semana|dw, w|  
|Hour|Hh|  
|Minute|mi, n|  
|Segundo|ss, s|  
|Millisecond|Ms|  
  
 El argumento *number* debe estar disponible al analizar la expresión. Puede ser una constante o una variable. No pueden usarse valores de columnas porque estos valores no se conocen en el momento de analizar la expresión.  
  
 El argumento *datepart* debe entrecomillarse.  
  
 Un literal de tipo fecha debe convertirse explícitamente en uno de los tipos de datos de fecha. Para obtener más información, vea [Integration Services Data Types](../data-flow/integration-services-data-types.md).  
  
 DATEADD devuelve un resultado NULL si el valor del argumento es NULL.  
  
 Se producen errores si la fecha no es válida, si la unidad de fecha o de hora no se indica mediante una cadena, o si el incremento no es un entero estático.  
  
## <a name="ssis-expression-examples"></a>Ejemplos de expresiones de SSIS  
 Este ejemplo agrega un mes a la fecha actual.  
  
```  
DATEADD("Month", 1,GETDATE())  
```  
  
 Este ejemplo agrega 21 días a las fechas de la columna **ModifiedDate** .  
  
```  
DATEADD("day", 21, ModifiedDate)  
```  
  
 Este ejemplo agrega 2 años a un literal de fecha.  
  
```  
DATEADD("yyyy", 2, (DT_DBTIMESTAMP)"8/6/2003")  
```  
  
## <a name="see-also"></a>Consulte también  
 [DATEDIFF &#40;expresión de SSIS&#41;](datediff-ssis-expression.md)   
 [DATEPART &#40;expresión de SSIS&#41;](datepart-ssis-expression.md)   
 [DAY &#40;expresión de SSIS&#41;](day-ssis-expression.md)   
 [MONTH &#40;expresión de SSIS&#41;](month-ssis-expression.md)   
 [YEAR &#40;expresión de SSIS&#41;](year-ssis-expression.md)   
 [Funciones &#40;expresión de SSIS&#41;](functions-ssis-expression.md)  
  
  
