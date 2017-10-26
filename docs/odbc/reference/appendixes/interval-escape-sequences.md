---
title: Secuencias de Escape Interval | Documentos de Microsoft
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
- interval literals [ODBC]
- escape sequences [ODBC], interval
- ODBC escape sequences [ODBC], interval
ms.assetid: 303e8dab-8f13-4fa5-857f-15cc1f75bdd6
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 8088c0cb3f85b375423f636d2def8c08c04bbe28
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="interval-escape-sequences"></a>Secuencias de Escape Interval
ODBC utiliza secuencias de escape para literales de intervalo. La sintaxis de esta secuencia de escape es como sigue:  
  
 {*intervalo literal*}  
  
 Para obtener la sintaxis BNF de *intervalo literal*, consulte el [sintaxis de literales de intervalo](../../../odbc/reference/appendixes/interval-literal-syntax.md) sección más adelante en este apéndice.  
  
 Se admite la secuencia de escape de literales de intervalo si los tipos de datos de intervalo son compatibles con el origen de datos. Una aplicación debe llamar a **SQLGetTypeInfo** para determinar si se admiten estos tipos de datos.

