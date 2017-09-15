---
title: "Secuencia de Escape de combinación externa | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- outer join escape sequence [ODBC]
- escape sequences [ODBC], outer join
- ODBC escape sequences [ODBC], outer join
ms.assetid: 2cfd1525-6677-4d36-9b9e-730496853750
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: d208b7de815f090e5f61d3d807912c53c4253e31
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

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
  
 *combinación externa* :: = *nombre de la tabla* [*nombre de correlación*] {izquierda &#124; DERECHA &#124; COMPLETA}  
  
 OUTER JOIN {*nombre de la tabla* [*nombre de correlación*] &#124; *combinación externa*} ON  
  
 *búsqueda:*  
  
 *condición*  
  
 *nombre de correlación* :: = *nombre definido por el usuario*  
  
 *Iniciador de esc de ODBC* :: = {  
  
 *Terminador de esc de ODBC* :: =}  
  
 Para determinar qué partes de esta instrucción son compatibles, llama a una aplicación **SQLGetInfo** con el tipo de información de SQL_OJ_CAPABILITIES. Para las combinaciones externas, *condición de búsqueda* debe contener la condición de combinación entre especificado *nombres de tabla*.
