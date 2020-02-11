---
title: LIKE (secuencia de escape) | Microsoft Docs
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68041710"
---
# <a name="like-escape-sequence"></a>Secuencia de escape LIKE
ODBC usa secuencias de escape para la cláusula LIKE. La sintaxis de esta secuencia de escape es la siguiente:  
  
```  
{'escape-character'}  
```  
  
## <a name="remarks"></a>Observaciones  
 En la notación BNF, la sintaxis es la siguiente:  
  
 *ODBC-like-escape* :: =  
  
 *ODBC-ESC-Initiator* escape '*carácter de escape*' *ODBC-ESC-Terminator*  
  
 carácter *de escape* : *: =*  
  
 *ODBC-ESC-Initiator* :: = {  
  
 *ODBC-ESC-Terminator* :: =}  
  
 Para determinar si el controlador admite la secuencia de escape LIKE, una aplicación puede llamar a **SQLGetInfo** con el tipo de información SQL_LIKE_ESCAPE_CLAUSE.
