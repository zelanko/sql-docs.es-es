---
title: Comando ESTABLECIDO DE LA PROGRAMA ( SET EXACT Command) Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SET EXACT command [ODBC]
ms.assetid: 9533d3e0-e7c1-49de-a3a3-0cc4373a91cb
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3e754fff35b6b948ac63d19361067b2d65a07fdd
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300875"
---
# <a name="set-exact-command"></a>Comando exacto de conjunto
Especifica las reglas para comparar dos cadenas de longitudes diferentes.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
SET EXACT ON | OFF  
```  
  
## <a name="arguments"></a>Argumentos  
 ACTIVAR  
 Especifica que las expresiones deben coincidir con el carácter para que el carácter sea equivalente. Los espacios en blanco finales de las expresiones se omiten para la comparación. Para la comparación, el más corto de las dos expresiones se rellena a la derecha con espacios en blanco para que coincidan con la longitud de la expresión más larga.  
  
 Apagado  
 (Predeterminado.) Especifica que, para que sean equivalentes, las expresiones deben coincidir con el carácter del carácter hasta que se alcance el final de la expresión en el lado derecho.  
  
## <a name="remarks"></a>Observaciones  
 El ajuste SET EXACT no tiene ningún efecto si ambas cadenas tienen la misma longitud.  
  
## <a name="string-comparisons"></a>Comparaciones de cadenas  
 Visual FoxPro tiene dos operadores relacionales que prueban la igualdad.  
  
 El operador de la clase á realiza una comparación entre dos valores del mismo tipo. Este operador es adecuado para comparar datos de caracteres, numéricos, de fecha y lógicos.  
  
 Sin embargo, cuando se comparan las expresiones de caracteres con el operador , es posible que los resultados no sean exactamente los esperados. Las expresiones de carácter se comparan caracteres para caracteres de izquierda a derecha hasta que una de las expresiones no es igual a la otra, hasta que se alcanza el final de la expresión en el lado derecho del operador de la clase (SET EXACT OFF) o hasta que se alcanzan los extremos de ambas expresiones (SET EXACT ON).  
  
 Se puede utilizar el operador de la clase . cuando se necesita una comparación exacta de los datos de caracteres. Si se comparan dos expresiones de caracteres con el operador , las expresiones en ambos lados del operador de la clase , deben contener exactamente los mismos caracteres, incluidos los espacios en blanco, para que se consideren iguales. El ajuste SET EXACT se omite cuando se comparan las cadenas de caracteres mediante el uso de .  
  
 En la tabla siguiente se muestra cómo la elección del operador y la configuración SET EXACT afectan a las comparaciones. (Un carácter de subrayado representa un espacio en blanco.)  
  
|De comparación|• EXACT OFF|• EXACT ON|• EXACT ON o OFF|  
|----------------|------------------|-----------------|--------------------------|  
|"abc" á "abc"|Match|Match|Match|  
|"ab" á "abc"|Ninguna coincidencia|Ninguna coincidencia|Ninguna coincidencia|  
|"abc" - "ab"|Match|Ninguna coincidencia|Ninguna coincidencia|  
|"abc" - "ab_"|Ninguna coincidencia|Ninguna coincidencia|Ninguna coincidencia|  
|"ab" - "ab_"|Ninguna coincidencia|Match|Ninguna coincidencia|  
|"ab_" - "ab"|Match|Match|Ninguna coincidencia|  
|"" - "ab"|Ninguna coincidencia|Ninguna coincidencia|Ninguna coincidencia|  
|"ab" á ""|Match|Ninguna coincidencia|Ninguna coincidencia|  
|"__" = ""|Match|Match|Ninguna coincidencia|  
|"" = "___"|Ninguna coincidencia|Match|Ninguna coincidencia|  
|TRIM("___") á ""|Match|Match|Match|  
|"" - TRIM("___")|Match|Match|Match|  
  
## <a name="see-also"></a>Consulte también  
 [Comando de ANSI SET](../../odbc/microsoft/set-ansi-command.md)
