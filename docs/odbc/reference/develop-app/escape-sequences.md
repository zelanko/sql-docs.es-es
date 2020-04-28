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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5d9589230183b198cb7d59cf9739dab75625441e
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "81298715"
---
# <a name="escape-sequences"></a>Secuencias de escape
ODBC define secuencias de escape que contienen la gramática estándar para los literales de fecha, hora, marca de tiempo y intervalo de fecha y hora, llamadas a funciones escalares, **como** caracteres de escape de predicado, combinaciones externas y llamadas a procedimientos. Las aplicaciones interoperables deben usar estas secuencias siempre que sea posible.  
  
 Para determinar si un controlador admite las secuencias de escape para los literales de fecha, hora, marca de tiempo o intervalo de fecha y hora, una aplicación llama a **SQLGetTypeInfo**. Si el origen de datos admite un tipo de datos de fecha, hora, marca de tiempo o intervalo de fecha y hora, también debe admitir la secuencia de escape correspondiente. Para determinar si se admiten las otras secuencias de escape, una aplicación llama a **SQLGetInfo**.  
  
 Para obtener más información, vea [secuencias de escape en ODBC](../../../odbc/reference/develop-app/escape-sequences-in-odbc.md), más adelante en esta sección.
