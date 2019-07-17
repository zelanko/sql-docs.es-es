---
title: Niveles de compatibilidad de SQL | Microsoft Docs
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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68107520"
---
# <a name="sql-conformance-levels"></a>Niveles de compatibilidad de SQL
El nivel de gramática de SQL-92 compatible con un controlador se indica mediante el valor devuelto por una llamada a **SQLGetInfo** con el tipo de información SQL_SQL_CONFORMANCE. Indica si el controlador se ajusta a los niveles de entrada, la transición de FIPS, intermedio o completo definidos en SQL-92.  
  
 Todos los controladores ODBC deben admitir la gramática mínima de SQL que se describe en [gramática mínima de SQL](../../../odbc/reference/appendixes/sql-minimum-grammar.md) en el apéndice C: Gramática de SQL. Esta gramática es un subconjunto del nivel de entrada de SQL-92. Los controladores pueden admite SQL adicional y ser conforme al nivel básico de SQL-92, intermedio o completo, así como el estándar FIPS 127-2 nivel de transición. Los controladores que cumplan con un nivel determinado de SQL-92 o FIPS 127-2 pueden admitir características adicionales en cualquiera de los niveles más altos aún no sea totalmente compatible con ese nivel. Para determinar si se admite una característica, una aplicación debe llamar a **SQLGetInfo** con el tipo de información. El nivel de cumplimiento de una característica SQL se describe en el tipo de información correspondiente. (Consulte la [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) descripción de la función.)
