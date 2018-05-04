---
title: Al igual que la secuencia de Escape | Documentos de Microsoft
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
- ODBC escape sequences [ODBC], LIKE
- LIKE escape sequence [ODBC]
- escape sequences [ODBC], LIKE
ms.assetid: 798d75ea-be9d-4bef-b297-318bc327f1ca
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3a9ae849aa255b5427d1efca50d6e429ee6a2afb
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
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
