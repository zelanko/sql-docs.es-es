---
title: Secuencias de escape | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], interoperability
- escape sequences [ODBC], determining if supported
- interoperability of SQL statements [ODBC], escape sequences
ms.assetid: 5913abfa-d280-43e4-a2f1-05a924388bf9
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d73282cde4d0598d7e6a35ac6273935626b96969
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68001374"
---
# <a name="escape-sequences"></a>Secuencias de escape
ODBC define secuencias de escape que contiene la gramática de estándar de fecha, hora, marca de tiempo y literales de intervalo de fecha y hora, llamadas a funciones escalares **como** predicado caracteres de escape, combinaciones externas y las llamadas a procedimiento. Aplicaciones interoperables deben usar estas secuencias siempre que sea posible.  
  
 Para determinar si un controlador es compatible con las secuencias de escape para fecha, hora, marca de hora o literales de intervalo de fecha y hora, una aplicación llama a **SQLGetTypeInfo**. Si el origen de datos admite una fecha, hora, marca de tiempo o tipo de datos de intervalo de fecha y hora, también debe admitir la secuencia de escape correspondiente. Para determinar si son compatibles con las otras secuencias de escape, una aplicación llama a **SQLGetInfo**.  
  
 Para obtener más información, consulte [secuencias de Escape de ODBC](../../../odbc/reference/develop-app/escape-sequences-in-odbc.md), más adelante en esta sección.
