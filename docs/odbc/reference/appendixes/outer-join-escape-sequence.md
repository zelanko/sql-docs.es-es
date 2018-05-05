---
title: Secuencia de Escape de combinación externa | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- outer join escape sequence [ODBC]
- escape sequences [ODBC], outer join
- ODBC escape sequences [ODBC], outer join
ms.assetid: 2cfd1525-6677-4d36-9b9e-730496853750
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: af6a98b3e1a7848fa242dfceb890c472e1d16f74
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="outer-join-escape-sequence"></a>Secuencia de Escape de combinación externa
ODBC utiliza secuencias de escape para las combinaciones externas. La sintaxis de esta secuencia de escape es como sigue:  
  
```  
{oj outer-join}  
```  
  
## <a name="remarks"></a>Comentarios  
 En la notación de BNF, la sintaxis es la siguiente:  
  
 *ODBC outer-join-escape* :: =  
  
 *Iniciador de esc de ODBC* oj *combinación externa terminador de esc de ODBC*  
  
 *combinación externa* :: = *nombre de la tabla* [*nombre de correlación*] {izquierda &#124; derecha &#124; completo}  
  
 COMBINACIÓN externa {*nombre de la tabla* [*nombre de correlación*] &#124; *combinación externa*} ON  
  
 *búsqueda:*  
  
 *condición*  
  
 *nombre de correlación* :: = *nombre definido por el usuario*  
  
 *Iniciador de esc de ODBC* :: = {  
  
 *Terminador de esc de ODBC* :: =}  
  
 Para determinar qué partes de esta instrucción son compatibles, llama a una aplicación **SQLGetInfo** con el tipo de información de SQL_OJ_CAPABILITIES. Para las combinaciones externas, *condición de búsqueda* debe contener la condición de combinación entre especificado *nombres de tabla*.
