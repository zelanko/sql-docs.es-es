---
title: Secuencia de escape de combinación externa | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "81303616"
---
# <a name="outer-join-escape-sequence"></a>Secuencia de escape de combinación externa
ODBC utiliza secuencias de escape para las combinaciones externas. La sintaxis de esta secuencia de escape es la siguiente:  
  
```  
{oj outer-join}  
```  
  
## <a name="remarks"></a>Observaciones  
 En la notación BNF, la sintaxis es la siguiente:  
  
 *ODBC-outer-join-escape* :: =  
  
 *ODBC-ESC-Initiator* do *outer-join ODBC-ESC-Terminator*  
  
 *outer-join* :: = *nombre de tabla* [*nombre de correlación*] {izquierda &#124; derecha &#124; completo}  
  
 COMBINACIÓN externa {*nombre de tabla* [*nombre de correlación*] &#124; *outer-join*} en  
  
 *buscan*  
  
 *condition*  
  
 *correlación: nombre* :: = *nombre definido por el usuario*  
  
 *ODBC-ESC-Initiator* :: = {  
  
 *ODBC-ESC-Terminator* :: =}  
  
 Para determinar qué partes de esta instrucción se admiten, una aplicación llama a **SQLGetInfo** con el tipo de información SQL_OJ_CAPABILITIES. En las combinaciones externas, la *condición de búsqueda* debe contener solo la condición de combinación entre los *nombres de tabla*especificados.
