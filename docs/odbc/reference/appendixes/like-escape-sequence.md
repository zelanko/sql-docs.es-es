---
description: Secuencia de escape LIKE
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 19d20f80f9fea4df2c508ec4ec4bcc2ee6718986
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429656"
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
