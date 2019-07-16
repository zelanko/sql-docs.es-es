---
title: Secuencia de Escape de combinación externa | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- outer join escape sequence [ODBC]
- escape sequences [ODBC], outer join
- ODBC escape sequences [ODBC], outer join
ms.assetid: 2cfd1525-6677-4d36-9b9e-730496853750
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 576fe7268ccf71a8c926f6b1124ebbf8a8c711b0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68100638"
---
# <a name="outer-join-escape-sequence"></a>Secuencia de escape de combinación externa
ODBC utiliza secuencias de escape para las combinaciones externas. La sintaxis de esta secuencia de escape es como sigue:  
  
```  
{oj outer-join}  
```  
  
## <a name="remarks"></a>Comentarios  
 En la notación de BNF, la sintaxis es como sigue:  
  
 *Outer-join-escape ODBC* :: =  
  
 *Iniciador de esc de ODBC* jugo *combinación externa ODBC terminador esc*  
  
 *combinación externa* :: = *nombre-tabla* [*nombre de correlación*] {izquierda &#124; derecha &#124; completa}  
  
 COMBINACIÓN externa {*nombre-tabla* [*nombre de correlación*] &#124; *combinación externa*} ON  
  
 *search-*  
  
 *condition*  
  
 *nombre de correlación* :: = *nombre definido por el usuario*  
  
 *Iniciador de esc de ODBC* :: = {  
  
 *ODBC-esc-terminator* ::= }  
  
 Para determinar qué partes de esta instrucción son compatibles, una aplicación llama a **SQLGetInfo** con el tipo de información SQL_OJ_CAPABILITIES. Para las combinaciones externas, *condición de búsqueda* debe contener la condición de combinación entre especificado *nombres de tabla*.
