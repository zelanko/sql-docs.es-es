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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68001374"
---
# <a name="escape-sequences"></a>Secuencias de escape
ODBC define secuencias de escape que contienen la gramática estándar para los literales de fecha, hora, marca de tiempo y intervalo de fecha y hora, llamadas a funciones escalares, **como** caracteres de escape de predicado, combinaciones externas y llamadas a procedimientos. Las aplicaciones interoperables deben usar estas secuencias siempre que sea posible.  
  
 Para determinar si un controlador admite las secuencias de escape para los literales de fecha, hora, marca de tiempo o intervalo de fecha y hora, una aplicación llama a **SQLGetTypeInfo**. Si el origen de datos admite un tipo de datos de fecha, hora, marca de tiempo o intervalo de fecha y hora, también debe admitir la secuencia de escape correspondiente. Para determinar si se admiten las otras secuencias de escape, una aplicación llama a **SQLGetInfo**.  
  
 Para obtener más información, vea [secuencias de escape en ODBC](../../../odbc/reference/develop-app/escape-sequences-in-odbc.md), más adelante en esta sección.
