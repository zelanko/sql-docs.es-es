---
title: Funciones (expresión de SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- functions [Integration Services]
- expressions [Integration Services], functions
- string functions
- SQL Server Integration Services, functions
- SSIS, functions
ms.assetid: e9a41a31-94f4-46a4-b737-c707dd59ce48
caps.latest.revision: 35
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 5b67a495d92d0bfc59288533d5f7c21e0f86d645
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37171036"
---
# <a name="functions-ssis-expression"></a>Funciones (expresión de SSIS)
  El lenguaje de expresiones incluye un conjunto de funciones que pueden usarse en las expresiones. Las expresiones pueden usar una sola función, pero generalmente utilizan varias funciones, combinándolas con operadores.  
  
 Las funciones pueden clasificarse en los grupos siguientes:  
  
-   Funciones matemáticas que realizan cálculos basados en valores numéricos de entrada que se proporcionan como parámetros a la función y devuelven valores numéricos.  
  
-   Funciones de cadenas de caracteres que realizan operaciones en valores de entrada de cadena o de tipo hexadecimal y que devuelven una cadena o un valor numérico.  
  
-   Funciones de fecha y hora que realizan operaciones en valores de fecha y hora, y devuelven valores de tipo cadena, numéricos o de fecha y hora.  
  
-   Funciones del sistema que devuelven información sobre una expresión.  
  
 El lenguaje de expresiones proporciona las siguientes funciones matemáticas.  
  
|Función|Descripción|  
|--------------|-----------------|  
|[ABS &#40;expresión de SSIS&#41;](abs-ssis-expression.md)|Devuelve el valor absoluto (positivo) de una expresión numérica.|  
|[EXP &#40;expresión de SSIS&#41;](exp-ssis-expression.md)|Devuelve el exponente de la base e de la expresión especificada.|  
|[CEILING &#40;expresión de SSIS&#41;](ceiling-ssis-expression.md)|Devuelve el menor entero mayor o igual que una expresión numérica.|  
|[FLOOR &#40;expresión de SSIS&#41;](floor-ssis-expression.md)|Devuelve el mayor entero que es menor o igual que una expresión numérica.|  
|[LN &#40;expresión de SSIS&#41;](ln-ssis-expression.md)|Devuelve el logaritmo natural de una expresión numérica.|  
|[Registro &#40;expresión de SSIS&#41;](log-ssis-expression.md)|Devuelve el logaritmo en base 10 de una expresión numérica.|  
|[POWER &#40;expresión de SSIS&#41;](power-ssis-expression.md)|Devuelve el resultado de elevar una expresión numérica a una determinada potencia.|  
|[REDONDEAR &#40;expresión de SSIS&#41;](round-ssis-expression.md)|Devuelve una expresión numérica, redondeada a la longitud o precisión especificada. .|  
|[Inicio de sesión &#40;expresión de SSIS&#41;](sign-ssis-expression.md)|Devuelve el signo positivo (+), cero (0) o negativo (-) de una expresión numérica.|  
|[CUADRADO &#40;expresión de SSIS&#41;](square-ssis-expression.md)|Devuelve el cuadrado de una expresión numérica.|  
|[SQRT &#40;expresión de SSIS&#41;](sqrt-ssis-expression.md)|Devuelve la raíz cuadrada de una expresión numérica.|  
  
 El evaluador de expresiones proporciona las siguientes funciones para cadenas.  
  
|Función|Descripción|  
|--------------|-----------------|  
|[CODEPOINT &#40;expresión de SSIS&#41;](codepoint-ssis-expression.md)|Devuelve el valor de código Unicode del carácter más a la izquierda de una expresión de caracteres.|  
|[FINDSTRING &#40;expresión de SSIS&#41;](findstring-ssis-expression.md)|Devuelve el índice (de base 1) de la repetición especificada de una cadena de caracteres dentro de una expresión.|  
|[HEX &#40;expresión de SSIS&#41;](hex-ssis-expression.md)|Devuelve una cadena que representa el valor hexadecimal de un entero.|  
|[LEN &#40;expresión de SSIS&#41;](len-ssis-expression.md)|Devuelve el número de caracteres de una expresión de caracteres.|  
|[IZQUIERDA &#40;expresión de SSIS&#41;](left-ssis-expression.md)|Devuelve el número de caracteres especificado de la parte más a la izquierda de la expresión de caracteres dada.|  
|[INFERIOR &#40;expresión de SSIS&#41;](lower-ssis-expression.md)|Devuelve una expresión de caracteres después de convertir los caracteres en mayúsculas a minúsculas.|  
|[LTRIM &#40;expresión de SSIS&#41;](trim-ssis-expression.md)|Devuelve una expresión de caracteres tras quitar todos los espacios iniciales en blanco.|  
|[Reemplace &#40;expresión de SSIS&#41;](replace-ssis-expression.md)|Devuelve una expresión de caracteres tras reemplazar una cadena dentro de la expresión por otra cadena diferente o por la cadena vacía.|  
|[REPLICAR &#40;expresión de SSIS&#41;](replicate-ssis-expression.md)|Devuelve una expresión de caracteres replicada un determinado número de veces.|  
|[INVERTIR &#40;expresión de SSIS&#41;](reverse-ssis-expression.md)|Devuelve una expresión de caracteres en orden inverso.|  
|[DERECHA &#40;expresión de SSIS&#41;](right-ssis-expression.md)|Devuelve el número de caracteres especificado de la parte más a la derecha de la expresión de caracteres dada.|  
|[RTRIM &#40;expresión de SSIS&#41;](rtrim-ssis-expression.md)|Devuelve una expresión de caracteres después de quitar los espacios finales.|  
|[SUBCADENA &#40;expresión de SSIS&#41;](substring-ssis-expression.md)|Devuelve una parte de una expresión de caracteres.|  
|[RECORTAR &#40;expresión de SSIS&#41;](trim-ssis-expression.md)|Devuelve una expresión de caracteres después de quitar los espacios iniciales y finales.|  
|[SUPERIOR &#40;expresión de SSIS&#41;](upper-ssis-expression.md)|Devuelve una expresión de caracteres tras convertir los caracteres en minúsculas a mayúsculas.|  
  
 El evaluador de expresiones proporciona las siguientes funciones de fecha y hora.  
  
|Función|Descripción|  
|--------------|-----------------|  
|[DATEADD &#40;expresión de SSIS&#41;](dateadd-ssis-expression.md)|Devuelve un nuevo valor de tipo DT_DBTIMESTAMP agregando una fecha o un intervalo de tiempo a una fecha indicada.|  
|[DATEDIFF &#40;expresión de SSIS&#41;](datediff-ssis-expression.md)|Devuelve el número de límites de fecha y hora entre dos fechas especificadas.|  
|[DATEPART &#40;expresión de SSIS&#41;](datepart-ssis-expression.md)|Devuelve un entero que representa una parte de una fecha.|  
|[DÍA &#40;expresión de SSIS&#41;](day-ssis-expression.md)|Devuelve un entero que representa la parte del día de la fecha especificada.|  
|[GETDATE &#40;expresión de SSIS&#41;](getdate-ssis-expression.md)|Devuelve la fecha actual del sistema.|  
|[GETUTCDATE &#40;expresión de SSIS&#41;](getutcdate-ssis-expression.md)|Devuelve el valor de fecha y hora que representa la hora UTC actual (Hora universal coordinada u Hora media de Greenwich).|  
|[MES &#40;expresión de SSIS&#41;](month-ssis-expression.md)|Devuelve un entero que representa la parte del mes de la fecha especificada.|  
|[AÑO &#40;expresión de SSIS&#41;](year-ssis-expression.md)|Devuelve un entero que representa la parte del año de la fecha especificada.|  
  
 El evaluador de expresiones proporciona las siguientes funciones para valores NULL.  
  
|Función|Descripción|  
|--------------|-----------------|  
|[ISNULL &#40;expresión de SSIS&#41;](null-ssis-expression.md)|Devuelve un resultado booleano en función de si una expresión es NULL.|  
|[NULL &#40;expresión de SSIS&#41;](null-ssis-expression.md)|Devuelve un valor NULL asociado al tipo de datos solicitado.|  
  
 Los nombres de expresión se muestran en mayúsculas, pero no se distinguen mayúsculas de minúsculas. Por ejemplo, "null" es equivalente a "NULL".  
  
## <a name="see-also"></a>Vea también  
 [Operadores &#40;expresión de SSIS&#41;](operators-ssis-expression.md)   
 [Ejemplos de expresiones avanzadas de Integration Services](examples-of-advanced-integration-services-expressions.md)   
 [Expresiones de Integration Services &#40;SSIS&#41;](integration-services-ssis-expressions.md)  
  
  
