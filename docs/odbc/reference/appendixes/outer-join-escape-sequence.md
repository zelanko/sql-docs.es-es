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
manager: craigg
ms.openlocfilehash: ba08d33efca6fa90531f89bd57a307f42f343ebd
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63018365"
---
# <a name="outer-join-escape-sequence"></a>Secuencia de escape de combinación externa
ODBC utiliza secuencias de escape para las combinaciones externas. La sintaxis de esta secuencia de escape es como sigue:  
  
```  
{oj outer-join}  
```  
  
## <a name="remarks"></a>Comentarios  
 En la notación de BNF, la sintaxis es como sigue:  
  
 *ODBC-outer-join-escape* ::=  
  
 *Iniciador de esc de ODBC* jugo *combinación externa ODBC terminador esc*  
  
 *outer-join* ::= *table-name* [*correlation-name*] {LEFT &#124; RIGHT &#124; FULL}  
  
 COMBINACIÓN externa {*nombre-tabla* [*nombre de correlación*] &#124; *combinación externa*} ON  
  
 *search-*  
  
 *condition*  
  
 *correlation-name* ::= *user-defined-name*  
  
 *ODBC-esc-initiator* ::= {  
  
 *ODBC-esc-terminator* ::= }  
  
 Para determinar qué partes de esta instrucción son compatibles, una aplicación llama a **SQLGetInfo** con el tipo de información SQL_OJ_CAPABILITIES. Para las combinaciones externas, *condición de búsqueda* debe contener la condición de combinación entre especificado *nombres de tabla*.
