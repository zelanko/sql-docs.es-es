---
title: SUBSTRING (expresión de SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- SUBSTRING function
- part of expression returned [Integration Services]
ms.assetid: 3a46748a-f5f8-4a6c-9108-673666754068
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 4a0f08864aa25ad7cb1d77f11e95e50c5a21d437
ms.sourcegitcommit: 7ccb8f28eafd79a1bddd523f71fe8b61c7634349
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/20/2019
ms.locfileid: "58277361"
---
# <a name="substring-ssis-expression"></a>SUBSTRING (expresión de SSIS)
  Devuelve la parte de una expresión de caracteres que empieza en la posición especificada y tiene la longitud especificada. Los parámetros *position* y *length* deben ser números enteros.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
SUBSTRING(character_expression, position, length)  
```  
  
## <a name="arguments"></a>Argumentos  
 *character_expression*  
 Expresión de caracteres de la que se van a extraer caracteres.  
  
 *position*  
 Entero que especifica el punto en que comienza la subcadena.  
  
 *length*  
 Entero que especifica la longitud de la subcadena como el número de caracteres.  
  
## <a name="result-types"></a>Tipos de resultado  
 DT_WSTR  
  
## <a name="remarks"></a>Notas  
 SUBSTRING utiliza un índice de base uno. Si *position* es 1, la subcadena empieza con el primer carácter de *character_expression*.  
  
 SUBSTRING solo funciona con el tipo de datos DT_WSTR. Un argumento *character_expression* que sea un literal de cadena o una columna de datos con el tipo de datos DT_STR, se convertirá implícitamente al tipo de datos DT_WSTR antes de que SUBSTRING realice su operación. Los otros tipos de datos deben convertirse explícitamente al tipo de datos DT_WSTR. Para obtener más información, vea [Tipos de datos de Integration Services](../../integration-services/data-flow/integration-services-data-types.md) y [Conversión &#40;expresión de SSIS&#41;](../../integration-services/expressions/cast-ssis-expression.md).  
  
 SUBSTRING devuelve un resultado NULL si el valor del argumento es NULL.  
  
 Todos los argumentos de la expresión pueden usar variables y columnas.  
  
 El valor del argumento *length* puede superar la longitud de la cadena. En tal caso, la función devuelve el resto de la cadena.  
  
## <a name="expression-examples"></a>Ejemplos de expresiones  
 Este ejemplo devuelve dos caracteres, empezando por el carácter 4, de un literal de cadena. El resultado devuelto es "ph".  
  
```  
SUBSTRING("elephant",4,2)  
```  
  
 Este ejemplo devuelve el resto de una cadena literal, empezando por el cuarto carácter. El resultado devuelto es "phant". Que el valor del argumento *length* supere la longitud de la cadena no es un error.  
  
```  
SUBSTRING ("elephant",4,50)  
```  
  
 Este ejemplo devuelve la primera letra de la columna **MiddleName** .  
  
```  
SUBSTRING(MiddleName,1,1)  
```  
  
 En este ejemplo se utilizan variables en los argumentos *position* y *length* . Si el valor de **Start** es 1 y el de **Length** es 5, la función devuelve los cinco primeros caracteres de la columna **Name** .  
  
```  
SUBSTRING(Name,@Start,@Length)  
```  
  
 Este ejemplo devuelve los cuatro últimos caracteres de la variable **PostalCode** , empezando por el sexto carácter.  
  
```  
SUBSTRING (@PostalCode,6,4)  
```  
  
 Este ejemplo devuelve una cadena de longitud cero de un literal de cadena.  
  
```  
SUBSTRING ("Redmond",4,0)  
```  
  
## <a name="see-also"></a>Consulte también  
 [Funciones &#40;expresión de SSIS&#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  
