---
title: Niveles de cumplimiento de SQL | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- conformance levels [ODBC], SQL
- SQL conformance levels [ODBC]
- data sources [ODBC], conformance levels
- ODBC drivers [ODBC], conformance levels
ms.assetid: 3529df2c-a09b-4c16-9c60-eae7a06d903a
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 7862b2e3a86c6d98a51c73ecb470d59bcfe29dc9
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68107520"
---
# <a name="sql-conformance-levels"></a>Niveles de compatibilidad de SQL
El nivel de gramática SQL-92 compatible con un controlador se indica mediante el valor devuelto por una llamada a **SQLGetInfo** con el tipo de información SQL_SQL_CONFORMANCE. Esto indica si el controlador se ajusta a la entrada, a los niveles de transición de FIPS, intermedio o completo definidos en SQL-92.  
  
 Todos los controladores ODBC deben ser compatibles con la gramática mínima de SQL descrita en la gramática [mínima de SQL](../../../odbc/reference/appendixes/sql-minimum-grammar.md) en el Apéndice C: gramática de SQL. Esta gramática es un subconjunto del nivel de entrada de SQL-92. Los controladores pueden admitir SQL adicional y ser conformes con la entrada SQL-92, el nivel intermedio o completo, o con el nivel de transición FIPS 127-2. Los controladores que cumplen un nivel determinado de SQL-92 o FIPS 127-2 pueden admitir características adicionales en cualquiera de los niveles superiores, pero no se ajustan totalmente a ese nivel. Para determinar si se admite una característica, una aplicación debe llamar a **SQLGetInfo** con el tipo de información adecuado. El nivel de conformidad de una característica SQL se describe en el tipo de información correspondiente. (Vea la descripción de la función [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) ).
