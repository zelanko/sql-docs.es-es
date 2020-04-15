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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298715"
---
# <a name="escape-sequences"></a>Secuencias de escape
ODBC define secuencias de escape que contienen gramática estándar para literales de fecha, hora, marca de tiempo e intervalo de fecha y hora, llamadas a funciones escalares, caracteres de escape de predicado **LIKE,** combinaciones externas y llamadas a procedimientos. Las aplicaciones interoperables deben utilizar estas secuencias siempre que sea posible.  
  
 Para determinar si un controlador admite las secuencias de escape para literales de fecha, hora, marca de tiempo o intervalo de fecha y hora, una aplicación llama a **SQLGetTypeInfo**. Si el origen de datos admite un tipo de datos de fecha, hora, marca de tiempo o intervalo de fecha y hora, también debe admitir la secuencia de escape correspondiente. Para determinar si se admiten las otras secuencias de escape, una aplicación llama a **SQLGetInfo**.  
  
 Para obtener más información, vea [Secuencias](../../../odbc/reference/develop-app/escape-sequences-in-odbc.md)de escape en ODBC , más adelante en esta sección.
