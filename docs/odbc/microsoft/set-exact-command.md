---
title: Comando exacto que conjunto | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SET EXACT command [ODBC]
ms.assetid: 9533d3e0-e7c1-49de-a3a3-0cc4373a91cb
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d40e662bf6af67246e3d5ae8eecd491cb2d263a5
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="set-exact-command"></a>Comando exacto de conjunto
Especifica las reglas para comparar dos cadenas de longitudes diferentes.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
SET EXACT ON | OFF  
```  
  
## <a name="arguments"></a>Argumentos  
 ON  
 Especifica que las expresiones deben coincidir con carácter por carácter sean equivalentes. Se omiten los espacios en blanco finales en las expresiones para la comparación. Para la comparación, la cadena más corta de las dos expresiones se rellena a la derecha con espacios en blanco para que coincida con la longitud de la expresión más larga.  
  
 OFF  
 (Valor predeterminado). Especifica que, para que sea equivalente, expresiones deben coincidir con carácter por carácter hasta que se alcanza el final de la expresión en el lado derecho.  
  
## <a name="remarks"></a>Comentarios  
 La configuración de SET EXACT no tiene ningún efecto si las dos cadenas tienen la misma longitud.  
  
## <a name="string-comparisons"></a>Comparaciones de cadenas  
 Visual FoxPro tiene dos operadores relacionales que comprobar la igualdad.  
  
 El = operador realiza una comparación entre dos valores del mismo tipo. Este operador es adecuado para comparar caracteres, numéricos, fecha y lógica de los datos.  
  
 Sin embargo, cuando se comparan expresiones de caracteres con el operador =, los resultados no estén exactamente lo que espera. Expresiones de caracteres se comparan caracteres para caracteres de izquierda a derecha, hasta que una de las expresiones no es igual que la otra, hasta el final de la expresión en el lado derecho de la = operador se alcanza (SET EXACT OFF), o hasta que los extremos de ambas expresiones son alcanzado (SET EXACT ON).  
  
 El == operador puede usarse cuando se necesita una comparación exacta de los datos de caracteres. Si se comparan dos expresiones de caracteres con el operador ==, las expresiones en ambos lados de la == operador debe contener exactamente los mismos caracteres, incluidos los espacios en blanco, que se consideran iguales. Se omite el valor de SET EXACT cuando se comparan las cadenas de caracteres mediante ==.  
  
 En la tabla siguiente se muestra cómo la elección del operador y la configuración de SET EXACT afectar a las comparaciones. (Un carácter de subrayado representa un espacio en blanco).  
  
|Comparación|= EXACTA DESACTIVADO|= EXACT ACTIVADO|== EXACT ON u OFF|  
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
