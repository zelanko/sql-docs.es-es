---
title: "LOWER (expresión de SSIS) | Documentos de Microsoft"
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
- converting uppercase to lowercase
- LOWER function
- uppercase characters [Integration Services]
- lowercase characters
ms.assetid: 109328e1-5604-40ff-895e-f2e7c13fff41
caps.latest.revision: 33
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 1d8887035d26ba829dae2153e4e9261836ada70d
ms.contentlocale: es-es
ms.lasthandoff: 08/03/2017

---
# <a name="lower-ssis-expression"></a>LOWER (expresión de SSIS)
  Devuelve una expresión de caracteres después de convertir los caracteres en mayúsculas a minúsculas.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
LOWER(character_expression)  
```  
  
## <a name="arguments"></a>Argumentos  
 *character_expression*  
 Expresión de caracteres para convertir a caracteres en minúsculas.  
  
## <a name="result-types"></a>Tipos de resultado  
 DT_WSTR  
  
## <a name="remarks"></a>Comentarios  
 LOWER solo funciona con el tipo de datos DT_WSTR. Un argumento *character_expression* que sea un literal de cadena o una columna de datos con el tipo de datos DT_STR, se convertirá implícitamente al tipo de datos DT_WSTR antes de que LOWER realice su operación. Los otros tipos de datos deben convertirse explícitamente al tipo de datos DT_WSTR. Para obtener más información, vea [Tipos de datos de Integration Services](../../integration-services/data-flow/integration-services-data-types.md) y [Conversión &#40;expresión de SSIS&#41;](../../integration-services/expressions/cast-ssis-expression.md).  
  
 LOWER devuelve un resultado NULL si el valor del argumento es NULL.  
  
## <a name="expression-examples"></a>Ejemplos de expresiones  
 Este ejemplo convierte un literal de cadena a caracteres en minúsculas. El resultado devuelto es "new york".  
  
```  
LOWER("New York")  
```  
  
 Este ejemplo convierte todos los caracteres de la columna de entrada **Color** , a excepción del primer carácter, a caracteres en minúsculas. Si el valor de Color es YELLOW, el resultado devuelto es "Yellow". Para obtener más información, vea [SUBSTRING &#40;expresión de SSIS&#41;](../../integration-services/expressions/substring-ssis-expression.md).  
  
```  
LOWER(SUBSTRING(Color, 2, 15))  
```  
  
 Este ejemplo convierte el valor de la variable **CityName** a caracteres en minúsculas.  
  
```  
LOWER(@CityName)  
```  
  
## <a name="see-also"></a>Vea también  
 [SUPERIOR &#40; Expresión de SSIS &#41;](../../integration-services/expressions/upper-ssis-expression.md)   
 [Funciones &#40; Expresión de SSIS &#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  
