---
title: LOWER (expresión de SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- converting uppercase to lowercase
- LOWER function
- uppercase characters [Integration Services]
- lowercase characters
ms.assetid: 109328e1-5604-40ff-895e-f2e7c13fff41
author: chugugrace
ms.author: chugu
ms.openlocfilehash: d8c595260f6611fde605e24922ce1877674dc822
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/22/2020
ms.locfileid: "86908201"
---
# <a name="lower-ssis-expression"></a>LOWER (expresión de SSIS)

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


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
  
## <a name="remarks"></a>Observaciones  
 LOWER solo funciona con el tipo de datos DT_WSTR. Un argumento *character_expression* que sea un literal de cadena o una columna de datos con el tipo de datos DT_STR, se convertirá implícitamente al tipo de datos DT_WSTR antes de que LOWER realice su operación. Los otros tipos de datos deben convertirse explícitamente al tipo de datos DT_WSTR. Para obtener más información, vea [Tipos de datos de Integration Services](../../integration-services/data-flow/integration-services-data-types.md) y [Conversión &#40;expresión de SSIS&#41;](../../integration-services/expressions/cast-ssis-expression.md).  
  
 LOWER devuelve un resultado NULL si el valor del argumento es NULL.  
  
## <a name="expression-examples"></a>Ejemplos de expresiones  
 Este ejemplo convierte un literal de cadena a caracteres en minúsculas. El resultado devuelto es "new york".  
  
```  
LOWER("New York")  
```  
  
 Este ejemplo convierte todos los caracteres de la columna de entrada **Color** , a excepción del primer carácter, a caracteres en minúsculas. Si el valor de Color es YELLOW, el resultado devuelto es "Yellow". Para más información, vea [SUBSTRING &#40;expresión de SSIS&#41;](../../integration-services/expressions/substring-ssis-expression.md).  
  
```  
LOWER(SUBSTRING(Color, 2, 15))  
```  
  
 Este ejemplo convierte el valor de la variable **CityName** a caracteres en minúsculas.  
  
```  
LOWER(@CityName)  
```  
  
## <a name="see-also"></a>Consulte también  
 [UPPER &#40;expresión de SSIS&#41;](../../integration-services/expressions/upper-ssis-expression.md)   
 [Funciones &#40;expresión de SSIS&#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  
