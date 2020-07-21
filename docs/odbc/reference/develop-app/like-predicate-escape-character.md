---
title: LIKE (carácter de escape de predicado) | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "81306156"
---
# <a name="like-predicate-escape-character"></a>COMO carácter de Escape de predicado
En un predicado **like** , el signo de porcentaje (%) coincide con cero o más caracteres y el carácter de subrayado (_) coincide con cualquier carácter. Para buscar coincidencias con un signo de porcentaje real o un carácter de subrayado en un predicado **like** , un carácter de escape debe aparecer antes del signo de porcentaje o el carácter de subrayado. La secuencia de escape que define el carácter de escape del predicado **like** es:  
  
 **{escape '** *carácter de escape* **'}**  
  
 donde el *carácter de escape* es cualquier carácter admitido por el origen de datos.  
  
 Para obtener más información acerca de la secuencia de escape LIKE, consulte [like Sequence (secuencia de escape](../../../odbc/reference/appendixes/like-escape-sequence.md) ) en el Apéndice C: gramática de SQL.  
  
 Por ejemplo, las siguientes instrucciones SQL crean el mismo conjunto de resultados de nombres de cliente que comienzan con los caracteres "% AAA". La primera instrucción usa la sintaxis de secuencia de escape. La segunda instrucción usa la sintaxis nativa de Microsoft® Access y no es interoperable. Observe que el segundo carácter de porcentaje de cada predicado **like** es un carácter comodín que coincide con cero o más caracteres.  
  
```  
SELECT Name FROM Customers WHERE Name LIKE '\%AAA%' {escape '\'}  
  
SELECT Name FROM Customers WHERE Name LIKE '[%]AAA%'  
```  
  
 Para determinar si un origen de datos admite el carácter de escape de predicado **like** , una aplicación llama a **SQLGetInfo** con la opción SQL_LIKE_ESCAPE_CLAUSE.
