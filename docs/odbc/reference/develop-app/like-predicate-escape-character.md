---
title: COMO Carácter de escape de predicado ( Predicate Escape Character) Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- LIKE predicate [ODBC]
- escape sequences [ODBC], LIKE predicate
ms.assetid: 185d6109-48cf-4981-bc40-ec2a4a90cafc
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2e4f04b12911145eede3354532736cb92f1ae413
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306156"
---
# <a name="like-predicate-escape-character"></a>COMO carácter de Escape de predicado
En un predicado **LIKE,** el signo de porcentaje (%) coincide con cero o más de cualquier carácter y el carácter de subrayado (_) coincide con cualquier carácter. Para que coincida con un signo de porcentaje real o un carácter de subrayado en un predicado **LIKE,** un carácter de escape debe presentarse antes del signo de porcentaje o subrayado. La secuencia de escape que define el carácter de escape del predicado **LIKE** es:  
  
 **'escape'** *'carácter de escape'* **'}**  
  
 donde *el carácter de escape* es cualquier carácter admitido por el origen de datos.  
  
 Para obtener más información acerca de la secuencia de escape LIKE, vea [LIKE Escape Sequence](../../../odbc/reference/appendixes/like-escape-sequence.md) en el Apéndice C: Gramática SQL.  
  
 Por ejemplo, las siguientes instrucciones SQL crean el mismo conjunto de resultados de nombres de cliente que comienzan con los caracteres "%AAA". La primera instrucción utiliza la sintaxis de secuencia de escape. La segunda instrucción utiliza la sintaxis nativa para Microsoft® Access y no es interoperable. Observe que el segundo carácter de porcentaje en cada predicado **LIKE** es un carácter comodín que coincide con cero o más de cualquier carácter.  
  
```  
SELECT Name FROM Customers WHERE Name LIKE '\%AAA%' {escape '\'}  
  
SELECT Name FROM Customers WHERE Name LIKE '[%]AAA%'  
```  
  
 Para determinar si un origen de datos admite el carácter de escape de predicado **LIKE,** una aplicación llama a **SQLGetInfo** con la opción SQL_LIKE_ESCAPE_CLAUSE.
