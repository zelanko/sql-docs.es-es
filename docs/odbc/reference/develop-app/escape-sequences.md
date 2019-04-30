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
manager: craigg
ms.openlocfilehash: c1423d7bcc0f0b943b490fdcf8f931efb6b533c6
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63259266"
---
# <a name="escape-sequences"></a>Secuencias de escape
ODBC define secuencias de escape que contiene la gramática de estándar de fecha, hora, marca de tiempo y literales de intervalo de fecha y hora, llamadas a funciones escalares **como** predicado caracteres de escape, combinaciones externas y las llamadas a procedimiento. Aplicaciones interoperables deben usar estas secuencias siempre que sea posible.  
  
 Para determinar si un controlador es compatible con las secuencias de escape para fecha, hora, marca de hora o literales de intervalo de fecha y hora, una aplicación llama a **SQLGetTypeInfo**. Si el origen de datos admite una fecha, hora, marca de tiempo o tipo de datos de intervalo de fecha y hora, también debe admitir la secuencia de escape correspondiente. Para determinar si son compatibles con las otras secuencias de escape, una aplicación llama a **SQLGetInfo**.  
  
 Para obtener más información, consulte [secuencias de Escape de ODBC](../../../odbc/reference/develop-app/escape-sequences-in-odbc.md), más adelante en esta sección.
