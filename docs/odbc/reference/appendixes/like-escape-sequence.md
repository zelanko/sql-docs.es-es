---
title: Secuencia de Escape LIKE | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC escape sequences [ODBC], LIKE
- LIKE escape sequence [ODBC]
- escape sequences [ODBC], LIKE
ms.assetid: 798d75ea-be9d-4bef-b297-318bc327f1ca
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 629ceaf666ae732d0838a216272c308dcb5b5658
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68041710"
---
# <a name="like-escape-sequence"></a>Secuencia de escape LIKE
ODBC utiliza secuencias de escape para la cláusula LIKE. La sintaxis de esta secuencia de escape es como sigue:  
  
```  
{'escape-character'}  
```  
  
## <a name="remarks"></a>Comentarios  
 En la notación de BNF, la sintaxis es como sigue:  
  
 *Escape de ODBC como* :: =  
  
 *Iniciador de esc de ODBC* escape '*carácter de escape*' *terminador de esc de ODBC*  
  
 *escape-character* ::= *character*  
  
 *Iniciador de esc de ODBC* :: = {  
  
 *ODBC-esc-terminator* ::= }  
  
 Para determinar si el controlador admite el escape LIKE secuencia, puede llamar una aplicación **SQLGetInfo** con el tipo de información SQL_LIKE_ESCAPE_CLAUSE.
