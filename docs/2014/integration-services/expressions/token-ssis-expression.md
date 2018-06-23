---
title: TOKEN (expresión de SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 9fdd06bf-5bc9-445c-95bf-709e0ca5989b
caps.latest.revision: 9
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 9ce43a5f85ed5680a1775e0e58f34cda5bffd026
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36199194"
---
# <a name="token--ssis-expression"></a>TOKEN (expresión de SSIS)
  Devuelve un token (subcadena) de una cadena basándose en los delimitadores especificados que separan los tokens en la cadena y el número del token que indica qué token se va a devolver.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
TOKEN(character_expression, delimiter_string, occurrence)  
```  
  
## <a name="arguments"></a>Argumentos  
 *character_expression*  
 Cadena que contiene los tokens separados por delimitadores.  
  
 *delimiter_string*  
 Cadena que contiene caracteres delimitadores. Por ejemplo, "; ,” contiene tres caracteres delimitadores punto y coma, un espacio en blanco y una coma.  
  
 *occurrence*  
 Entero con o sin signo que especifica el token que se va a devolver. Por ejemplo, si especifica 3 como valor para este parámetro, se devuelve el tercer token de la cadena.  
  
## <a name="result-types"></a>Tipos de resultado  
 DT_WSTR  
  
## <a name="remarks"></a>Notas  
 Esta función divide la cadena <character_expression> en un conjunto de tokens separados por los delimitadores especificados en <delimiter_string> y devuelve el token número N, donde N es el número de concurrencia del token especificado por el parámetro \<occurrence>. Vea la sección Ejemplos para los usos de ejemplo de esta función.  
  
 Las observaciones siguientes se aplican a la función TOKEN:  
  
-   La cadena delimitadora puede contener uno o más caracteres delimitadores.  
  
-   Si el valor del parámetro \<occurrence> es mayor que el número total de tokens de la cadena, la función devuelve NULL.  
  
-   Los delimitadores iniciales se omiten.  
  
-   TOKEN solo funciona con el tipo de datos DT_WSTR. Un argumento *character_expression* que sea un literal de cadena o una columna de datos con el tipo de datos DT_STR se convertirá implícitamente al tipo de datos DT_WSTR antes de que TOKEN realice su operación. Los otros tipos de datos deben convertirse explícitamente al tipo de datos DT_WSTR.  
  
-   TOKEN devuelve un resultado NULL si el valor de character_expression es NULL.  
  
-   Puede usar variables y columnas como valores de todos los argumentos de la expresión.  
  
## <a name="expression-examples"></a>Ejemplos de expresiones  
 En el ejemplo siguiente, la función TOKEN devuelve "a". La cadena "a little white dog" tiene 4 tokens "a", "little", "white", "dog" separados por el delimitador " " (carácter de espacio). El segundo argumento, una cadena delimitadora, especifica que solo un delimitador, el carácter de espacio, se utiliza en la división de la cadena de entrada en tokens. El último argumento, 1, especifica que se va a devolver el primer token. El primer token es "a" en esta cadena de ejemplo.  
  
```  
TOKEN("a little white dog"," ",1)  
```  
  
 En el ejemplo siguiente, la función TOKEN devuelve "dog". La cadena delimitadora en este ejemplo contiene 5 delimitadores. La cadena de entrada contiene 4 tokens: "a", "little", "white", "dog".  
  
```  
TOKEN("a:little|white dog","| ,.:",4)  
```  
  
 En el ejemplo siguiente, la función TOKEN devuelve "" (una cadena vacía) porque no hay 99 tokens en la cadena.  
  
```  
TOKEN("a little white dog"," ",99)  
```  
  
 En el ejemplo siguiente, la función TOKEN devuelve la cadena completa. La función analiza la cadena de entrada para los delimitadores y, como hay ninguno en la cadena, simplemente agrega la cadena completa como primer token.  
  
```  
TOKEN("a little white dog","|",1)  
```  
  
 En el ejemplo siguiente, la función TOKEN devuelve "a". Omite todos los caracteres de espacio iniciales.  
  
```  
TOKEN("        a little white dog", " ", 1)  
```  
  
 En el ejemplo siguiente, la función TOKEN devuelve el año de una cadena de fecha.  
  
```  
TOKEN("2009/01/01", "/"), 1  
```  
  
 En el ejemplo siguiente, la función TOKEN devuelve el nombre de archivo a partir de la ruta de acceso especificada. Por ejemplo, si el valor de User::Path es "c:\program files\data\myfile.txt", la función TOKEN devuelve "myfile.txt". La función TOKENCOUNT devuelve 4 y la función TOKEN devuelve el cuarto token, "myfile.txt".  
  
```  
TOKEN(@[User::Path], "\\", TOKENCOUNT(@[User::Path], "\\"))  
```  
  
## <a name="see-also"></a>Vea también  
 [Funciones &#40;expresión de SSIS&#41;](functions-ssis-expression.md)  
  
  