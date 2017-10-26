---
title: Secuencias de escape | Documentos de Microsoft
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
- SQL statements [ODBC], interoperability
- escape sequences [ODBC], determining if supported
- interoperability of SQL statements [ODBC], escape sequences
ms.assetid: 5913abfa-d280-43e4-a2f1-05a924388bf9
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 1c648549b41ff607ad34175475c6a2b75603625f
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="escape-sequences"></a>Secuencias de escape
ODBC define secuencias de escape que contienen gramática estándar para fecha, hora, marca de tiempo y literales de intervalo de fecha y hora, llamadas a funciones escalares, **como** predicado caracteres de escape, combinaciones externas y llamadas a procedimiento. Aplicaciones interoperables deben usar estas secuencias siempre que sea posible.  
  
 Para determinar si un controlador es compatible con las secuencias de escape para fecha, hora, marca de hora o literales de intervalo de fecha y hora, una aplicación llama **SQLGetTypeInfo**. Si el origen de datos admite una fecha, hora, marca de tiempo o tipo de datos del intervalo de fecha y hora, también debe admitir la secuencia de escape correspondiente. Para determinar si se admiten las otras secuencias de escape, llama a una aplicación **SQLGetInfo**.  
  
 Para obtener más información, consulte [secuencias de Escape de ODBC](../../../odbc/reference/develop-app/escape-sequences-in-odbc.md), más adelante en esta sección.

