---
title: Secuencia de escape de unión externa ? Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 37ce446328d263f492cdfd369f6e8f9f64fe6dfc
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303616"
---
# <a name="outer-join-escape-sequence"></a>Secuencia de escape de combinación externa
ODBC usa secuencias de escape para combinaciones externas. La sintaxis de esta secuencia de escape es la siguiente:  
  
```  
{oj outer-join}  
```  
  
## <a name="remarks"></a>Observaciones  
 En la notación BNF, la sintaxis es la siguiente:  
  
 *ODBC-outer-join-escape* ::  
  
 *ODBC-esc-iniciador* oj *outer-join ODBC-esc-terminator*  
  
 *unión externa* ::- *nombre-tabla* [*nombre-correlación*] -IZQUIERDA &#124; DERECHA &#124; COMPLETO?  
  
 OUTER JOIN-*nombre-tabla* [*nombre-correlación*] &#124; *unión externa*? ON  
  
 *búsqueda-*  
  
 *condition*  
  
 *nombre de correlación* ::- *nombre definido por* el usuario  
  
 *ODBC-esc-iniciador* ::-  
  
 *ODBC-esc-terminator* ::-  
  
 Para determinar qué partes de esta instrucción se admiten, una aplicación llama a **SQLGetInfo** con el tipo de información SQL_OJ_CAPABILITIES. Para las combinaciones externas, *la condición de búsqueda* debe contener solo la condición de combinación entre los nombres de tabla *especificados.*
