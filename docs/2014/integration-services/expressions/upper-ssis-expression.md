---
title: UPPER (expresión de SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- UPPER function
- converting lowercase to uppercase
- uppercase characters [Integration Services]
- lowercase characters
ms.assetid: d33985f7-1048-4023-83e4-274090acda78
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 957b0ce9c43fd986cafc51807f212bd64eb4d9e0
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/26/2020
ms.locfileid: "85437022"
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
  
## <a name="remarks"></a>Observaciones  
 UPPER solo funciona con el tipo de datos DT_WSTR. Un argumento *character_expression* que sea un literal de cadena o una columna de datos con el tipo de datos DT_STR, se convertirá implícitamente al tipo de datos DT_WSTR antes de que UPPER realice su operación. Los otros tipos de datos deben convertirse explícitamente al tipo de datos DT_WSTR. Para obtener más información, vea [Tipos de datos de Integration Services](../data-flow/integration-services-data-types.md) y [Conversión &#40;expresión de SSIS&#41;](cast-ssis-expression.md).  
  
 UPPER devuelve un resultado NULL si el valor del argumento es NULL.  
  
## <a name="expression-examples"></a>Ejemplos de expresiones  
 Este ejemplo convierte un literal de cadena a caracteres en mayúsculas. El resultado devuelto es "HELLO".  
  
```  
UPPER("hello")  
```  
  
 Este ejemplo convierte el primer carácter de la columna **FirstName** en un carácter en mayúsculas. Si el valor de **FirstName** es anna, el resultado devuelto es "A". Para más información, vea [SUBSTRING &#40;expresión de SSIS&#41;](substring-ssis-expression.md).  
  
```  
UPPER(SUBSTRING(FirstName, 1, 1))  
```  
  
 Este ejemplo convierte el valor de la variable **PostalCode** a caracteres en mayúsculas. Si el valor de **PostalCode** es k4b1s2, el resultado devuelto es "K4B1S2".  
  
```  
UPPER(@PostalCode)  
```  
  
## <a name="see-also"></a>Consulte también  
 [LOWER &#40;expresión de SSIS&#41;](lower-ssis-expression.md)   
 [Funciones &#40;expresión de SSIS&#41;](functions-ssis-expression.md)  
  
  
