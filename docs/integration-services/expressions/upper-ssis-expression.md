---
title: "UPPER (expresión de SSIS) | Documentos de Microsoft"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: expressions
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- UPPER function
- converting lowercase to uppercase
- uppercase characters [Integration Services]
- lowercase characters
ms.assetid: d33985f7-1048-4023-83e4-274090acda78
caps.latest.revision: 36
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 1764b39b0242ce7e23d56c9c74f7b953f45009b2
ms.contentlocale: es-es
ms.lasthandoff: 08/03/2017

---
# <a name="upper-ssis-expression"></a>UPPER (expresión de SSIS)
  Devuelve una expresión de caracteres tras convertir los caracteres en minúsculas a mayúsculas.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
UPPER(character_expression)  
```  
  
## <a name="arguments"></a>Argumentos  
 *character_expression*  
 Expresión de caracteres para convertir a caracteres en mayúsculas.  
  
## <a name="result-types"></a>Tipos de resultado  
 DT_WSTR  
  
## <a name="remarks"></a>Comentarios  
 UPPER solo funciona con el tipo de datos DT_WSTR. Un argumento *character_expression* que sea un literal de cadena o una columna de datos con el tipo de datos DT_STR, se convertirá implícitamente al tipo de datos DT_WSTR antes de que UPPER realice su operación. Los otros tipos de datos deben convertirse explícitamente al tipo de datos DT_WSTR. Para más información, vea [Tipos de datos de Integration Services](../../integration-services/data-flow/integration-services-data-types.md) y [Conversión &#40;expresión de SSIS&#41;](../../integration-services/expressions/cast-ssis-expression.md).  
  
 UPPER devuelve un resultado NULL si el valor del argumento es NULL.  
  
## <a name="expression-examples"></a>Ejemplos de expresiones  
 Este ejemplo convierte un literal de cadena a caracteres en mayúsculas. El resultado devuelto es "HELLO".  
  
```  
UPPER("hello")  
```  
  
 Este ejemplo convierte el primer carácter de la columna **FirstName** en un carácter en mayúsculas. Si el valor de **FirstName** es anna, el resultado devuelto es "A". Para más información, vea [SUBSTRING &#40;expresión de SSIS&#41;](../../integration-services/expressions/substring-ssis-expression.md).  
  
```  
UPPER(SUBSTRING(FirstName, 1, 1))  
```  
  
 Este ejemplo convierte el valor de la variable **PostalCode** a caracteres en mayúsculas. Si el valor de **PostalCode** es k4b1s2, el resultado devuelto es "K4B1S2".  
  
```  
UPPER(@PostalCode)  
```  
  
## <a name="see-also"></a>Vea también  
 [INFERIOR &#40; Expresión de SSIS &#41;](../../integration-services/expressions/lower-ssis-expression.md)   
 [Funciones &#40; Expresión de SSIS &#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  

