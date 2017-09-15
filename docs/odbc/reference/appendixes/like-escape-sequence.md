---
title: Al igual que la secuencia de Escape | Documentos de Microsoft
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
- ODBC escape sequences [ODBC], LIKE
- LIKE escape sequence [ODBC]
- escape sequences [ODBC], LIKE
ms.assetid: 798d75ea-be9d-4bef-b297-318bc327f1ca
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 678f2f8f720823ef5658ba7ee1e1391bbebc1c50
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="like-escape-sequence"></a>Al igual que la secuencia de Escape
ODBC utiliza secuencias de escape para la cláusula LIKE. La sintaxis de esta secuencia de escape es como sigue:  
  
```  
{'escape-character'}  
```  
  
## <a name="remarks"></a>Comentarios  
 En la notación de BNF, la sintaxis es la siguiente:  
  
 *Escape de ODBC-like* :: =  
  
 *Iniciador de esc de ODBC* escape '*carácter de escape*' *terminador de esc de ODBC*  
  
 *carácter de escape* :: = *caracteres*  
  
 *Iniciador de esc de ODBC* :: = {  
  
 *Terminador de esc de ODBC* :: =}  
  
 Para determinar si el controlador admite el escape LIKE secuencia, puede llamar una aplicación **SQLGetInfo** con el tipo de información de SQL_LIKE_ESCAPE_CLAUSE.
