---
title: Comando exacto de conjunto | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 16651df836ac3fb87c5e28b4b8fa25088e9dd86a
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63159342"
---
# <a name="set-exact-command"></a>Comando exacto de conjunto
Especifica las reglas para comparar dos cadenas de longitudes diferentes.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
SET EXACT ON | OFF  
```  
  
## <a name="arguments"></a>Argumentos  
 ON  
 Especifica que las expresiones deben coincidir carácter por carácter son equivalentes. Se omiten los espacios en blanco finales en las expresiones para la comparación. Para la comparación, la cadena más corta de las dos expresiones se rellena a la derecha con espacios en blanco para que coincida con la longitud de la expresión más larga.  
  
 OFF  
 (Valor predeterminado). Especifica que, para que sea equivalente, las expresiones deben coincidir carácter por carácter hasta que se alcanza el final de la expresión en el lado derecho.  
  
## <a name="remarks"></a>Comentarios  
 La configuración exacta de conjunto no tiene ningún efecto si las dos cadenas tienen la misma longitud.  
  
## <a name="string-comparisons"></a>Comparaciones de cadenas  
 Visual FoxPro tiene dos operadores relacionales que para comprobar la igualdad.  
  
 El = operador realiza una comparación entre dos valores del mismo tipo. Este operador es adecuado para la comparación de caracteres, numéricos, fecha y datos lógicos.  
  
 Sin embargo, cuando se comparan expresiones de carácter con el operador =, los resultados no es posible que sea exactamente lo que espera. Expresiones de caracteres se comparan caracteres para el carácter de izquierda a derecha hasta que una de las expresiones no es igual a otro, hasta el final de la expresión en el lado derecho de la = se alcanza el operador (SET EXACT OFF), o hasta que los extremos de ambas expresiones son se alcanzó el (SET EXACT ON).  
  
 El == operador puede usarse cuando se necesita una comparación exacta de los datos de caracteres. Si se comparan dos expresiones de caracteres con el operador ==, las expresiones en ambos lados de la == (operador) debe contener exactamente los mismos caracteres, incluidos espacios en blanco, que se consideran iguales. La configuración de SET EXACT se omite cuando se comparan las cadenas de caracteres mediante ==.  
  
 En la tabla siguiente se muestra cómo la elección del operador y la configuración de SET EXACT afectan a las comparaciones. (Un carácter de subrayado representa un espacio en blanco).  
  
|Comparación|= EXACTA DESACTIVADO|= ON EXACTA|== EXACT ON u OFF|  
|----------------|------------------|-----------------|--------------------------|  
|"abc" = "abc"|Coincidencia|Coincidencia|Coincidencia|  
|"ab" = "abc"|Ninguna coincidencia|Ninguna coincidencia|Ninguna coincidencia|  
|"abc" = "ab"|Coincidencia|Ninguna coincidencia|Ninguna coincidencia|  
|"abc" = "ab_"|Ninguna coincidencia|Ninguna coincidencia|Ninguna coincidencia|  
|"ab" = "ab_"|Ninguna coincidencia|Coincidencia|Ninguna coincidencia|  
|"ab_" = "ab"|Coincidencia|Coincidencia|Ninguna coincidencia|  
|"" = "ab"|Ninguna coincidencia|Ninguna coincidencia|Ninguna coincidencia|  
|"ab" = ""|Coincidencia|Ninguna coincidencia|Ninguna coincidencia|  
|"__" = ""|Coincidencia|Coincidencia|Ninguna coincidencia|  
|"" = "___"|Ninguna coincidencia|Coincidencia|Ninguna coincidencia|  
|TRIM("___") = ""|Coincidencia|Coincidencia|Coincidencia|  
|"" = TRIM("___")|Coincidencia|Coincidencia|Coincidencia|  
  
## <a name="see-also"></a>Vea también  
 [Comando de ANSI SET](../../odbc/microsoft/set-ansi-command.md)
