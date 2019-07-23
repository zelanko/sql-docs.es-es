---
title: DATEPART (expresión de SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- dates [Integration Services], DATEPART
- DATEPART function
ms.assetid: 3e590094-fc49-4144-805f-fdc1bf2fe509
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 29890b85ccd19d17d74a560a2c1264de879a4e1c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68081108"
---
# <a name="datepart-ssis-expression"></a>DATEPART (expresión de SSIS)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Devuelve un entero que representa una parte de una fecha.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
DATEPART(datepart, date)  
```  
  
## <a name="arguments"></a>Argumentos  
 *parte de fecha*  
 Parámetro que especifica para qué parte de la fecha se devuelve un valor nuevo.  
  
 *date*  
 Expresión que devuelve una fecha válida o una cadena con formato de fecha.  
  
## <a name="result-types"></a>Tipos de resultado  
 DT_I4  
  
## <a name="remarks"></a>Notas  
 DATEPART devuelve un resultado NULL si el valor del argumento es NULL.  
  
 Un literal de tipo fecha debe convertirse explícitamente en uno de los tipos de datos de fecha. Para obtener más información, vea [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md).  
  
 En la tabla siguiente se incluyen las partes de fecha y las abreviaturas reconocidas por el evaluador de expresiones. En los nombres de partes de fecha no se distinguen mayúsculas de minúsculas.  
  
|parte de fecha|Abreviaturas|  
|--------------|-------------------|  
|Year|yy, yyyy|  
|Trimestre|qq, q|  
|Month|mm, m|  
|Dayofyear|dy, y|  
|Day|dd, d|  
|Semana|wk, ww|  
|Weekday|dw|  
|Hour|Hh|  
|Minute|mi, n|  
|Second|ss, s|  
|Millisecond|Ms|  
  
## <a name="ssis-expression-examples"></a>Ejemplos de expresiones de SSIS  
 Este ejemplo devuelve el entero que representa el mes de un literal de fecha. Si la fecha tiene el formato mm/dd/aaaa, este ejemplo devuelve 11.  
  
```  
DATEPART("month", (DT_DBTIMESTAMP)"11/04/2002")  
```  
  
 Este ejemplo devuelve el entero que representa el día en la columna **ModifiedDate** .  
  
```  
DATEPART("dd", ModifiedDate)  
```  
  
 Este ejemplo devuelve el entero que representa el año de la fecha actual.  
  
```  
DATEPART("yy",GETDATE())  
```  
  
## <a name="see-also"></a>Consulte también  
 [DATEADD &#40;expresión de SSIS&#41;](../../integration-services/expressions/dateadd-ssis-expression.md)   
 [DATEDIFF &#40;expresión de SSIS&#41;](../../integration-services/expressions/datediff-ssis-expression.md)   
 [DAY &#40;expresión de SSIS&#41;](../../integration-services/expressions/day-ssis-expression.md)   
 [MONTH &#40;expresión de SSIS&#41;](../../integration-services/expressions/month-ssis-expression.md)   
 [YEAR &#40;expresión de SSIS&#41;](../../integration-services/expressions/year-ssis-expression.md)   
 [Funciones &#40;expresión de SSIS&#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  
