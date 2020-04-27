---
title: HEX (expresión de SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- hexadecimal data
- HEX function
ms.assetid: f5d471ee-aeef-421c-b6e1-55b9676c3842
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 4dfd342647f6d355ee34e1e815db9431a212dbc9
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "62897860"
---
# <a name="hex-ssis-expression"></a>HEX (expresión de SSIS)
  Devuelve una cadena que representa el valor hexadecimal de un entero.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
HEX(integer_expression)  
```  
  
## <a name="arguments"></a>Argumentos  
 *integer_expression*  
 Entero con o sin signo.  
  
## <a name="result-types"></a>Tipos de resultado  
 DT_WSTR  
  
## <a name="remarks"></a>Observaciones  
 HEX devuelve null si *integer_expression* es null.  
  
 El argumento *integer_expression* debe devolver un entero. Para obtener más información, vea [Integration Services Data Types](../data-flow/integration-services-data-types.md).  
  
 El resultado devuelto no incluye calificadores, como el prefijo 0x. Para incluir un prefijo utilice el operador + (Concatenar). Para más información, vea [+ &#40;Concatenar&#41; &#40;expresión de SSIS&#41;](concatenate-ssis-expression.md).  
  
 En la notación hexadecimal, las letras A-F siempre aparecen en mayúscula.  
  
 La longitud de la cadena resultante depende del tipo de datos entero usado, como se indica a continuación:  
  
-   DT_I1 y DT_UI1 devuelven una cadena con una longitud máxima de 2.  
  
-   DT_I2 y DT_UI2 devuelven una cadena con una longitud máxima de 4.  
  
-   DT_I4 y DT_UI4 devuelven una cadena con una longitud máxima de 8.  
  
-   DT_I8 y DT_UI8 devuelven una cadena con una longitud máxima de 16.  
  
## <a name="expression-examples"></a>Ejemplos de expresiones  
 Este ejemplo usa un literal numérico. La función devuelve el valor 190.  
  
```  
HEX(400)   
```  
  
 Este ejemplo usa la columna **ReorderPoint** . El tipo de datos de la columna es `smallint`. Si el valor de **ReorderPoint** es 750, la función devuelve 2EE.  
  
```  
HEX(ReorderPoint)   
```  
  
 Este ejemplo usa **LocaleID**, una variable del sistema. Si el valor de **LocaleID** es 1033, la función devuelve 409.  
  
```  
HEX(@LocaleID)  
```  
  
## <a name="see-also"></a>Consulte también  
 [Funciones &#40;expresión de SSIS&#41;](functions-ssis-expression.md)  
  
  
