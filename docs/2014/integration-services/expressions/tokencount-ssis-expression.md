---
title: TOKENCOUNT (expresión de SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 1c0efed1-c2b3-4f20-a3a1-ad91283b7c0a
author: chugugrace
ms.author: chugu
ms.openlocfilehash: c6675c9c6ca2a5e0549a1e5c20f9108cac439ac1
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/26/2020
ms.locfileid: "85437092"
---
# <a name="tokencount-ssis-expression"></a>TOKENCOUNT (expresión de SSIS)
  Devuelve el número de tokens en una cadena que contiene los tokens separados por los delimitadores especificados.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
TOKENCOUNT(character_expression, delimiter_string)  
```  
  
## <a name="arguments"></a>Argumentos  
 *character_expression*  
 Cadena que contiene los tokens separados por delimitadores.  
  
 *delimiter_string*  
 Cadena que contiene caracteres delimitadores. Por ejemplo, “; ,” contiene tres caracteres delimitadores: punto y coma, un espacio en blanco y una coma.  
  
## <a name="result-types"></a>Tipos de resultado  
 DT_I4  
  
## <a name="remarks"></a>Observaciones  
 Las observaciones siguientes se aplican a la función TOKEN:  
  
-   La cadena delimitadora puede contener uno o más caracteres delimitadores.  
  
-   Los delimitadores iniciales se omiten.  
  
-   TOKENCOUNT funciona solo con el tipo de datos DT_WSTR. Un argumento *character_expression* que sea un literal de cadena o una columna de datos con el tipo de datos DT_STR se convertirá implícitamente al tipo de datos DT_WSTR antes de que TOKEN realice su operación. Los otros tipos de datos deben convertirse explícitamente al tipo de datos DT_WSTR.  
  
-   TOKENCOUNT devuelve 0 (cero) si character_expression es NULL.  
  
-   Puede usar variables y columnas como argumentos de esta expresión.  
  
## <a name="expression-examples"></a>Ejemplos de expresiones  
 En el ejemplo siguiente, la función TOKENCOUNT devuelve 3 porque la cadena contiene tres tokens: “01”, “12”, “2011”.  
  
```  
TOKENCOUNT("01/12/2011", "/")  
```  
  
 En el ejemplo siguiente, la función TOKENCOUNT devuelve 4 porque hay cuatro tokens (“a”, “little”, “white”, “dog”).  
  
```  
TOKENCOUNT("a little white dog"," ")  
```  
  
 En el ejemplo siguiente, la función TOKENCOUNT devuelve 1. La función analiza la cadena de entrada para los delimitadores y, como hay ninguno en la cadena, simplemente agrega la cadena completa como primer token.  
  
```  
TOKENCOUNT("a little white dog","|")  
```  
  
 En el ejemplo siguiente, la función TOKENCOUNT devuelve 4. La cadena delimitadora en este ejemplo contiene 5 delimitadores. La cadena de entrada contiene 4 tokens: “a”, “little”, “white”, “dog”.  
  
```  
TOKENCOUNT("a:little|white dog","| ,.:")  
```  
  
 En el ejemplo siguiente, la función TOKENCOUNT devuelve 4. Omite todos los caracteres de espacio iniciales.  
  
```  
TOKENCOUNT("        a little white dog", " ")  
```  
  
## <a name="see-also"></a>Consulte también  
 [Funciones &#40;expresión de SSIS&#41;](functions-ssis-expression.md)  
  
  
