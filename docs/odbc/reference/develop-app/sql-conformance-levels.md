---
title: Niveles de conformidad de SQL ( SQL Conformance Levels) Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 875330ac78588566b4b1c212f7a65d2841127a61
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301386"
---
# <a name="sql-conformance-levels"></a>Niveles de compatibilidad de SQL
El nivel de gramática SQL-92 admitido por un controlador se indica mediante el valor devuelto por una llamada a **SQLGetInfo** con el tipo de información SQL_SQL_CONFORMANCE. Esto indica si el controlador se ajusta a los niveles Entry, FIPS Transitional, Intermediate o Full definidos en SQL-92.  
  
 Todos los controladores ODBC deben admitir la gramática SQL mínima descrita en [Gramática mínima](../../../odbc/reference/appendixes/sql-minimum-grammar.md) de SQL en el Apéndice C: Gramática SQL. Esta gramática es un subconjunto del nivel de entrada de SQL-92. Los controladores pueden admitir SQL adicional y ser conformes con el nivel de entrada, intermedio o completo de SQL-92, o al nivel de transición FIPS 127-2. Los controladores que cumplen con un nivel determinado de SQL-92 o FIPS 127-2 pueden admitir características adicionales en cualquiera de los niveles superiores pero no ser totalmente conformes con ese nivel. Para determinar si se admite una característica, una aplicación debe llamar a **SQLGetInfo** con el tipo de información adecuado. El nivel de conformidad de una característica SQL se describe en el tipo de información correspondiente. (Consulte la descripción de la función [SQLGetInfo.)](../../../odbc/reference/syntax/sqlgetinfo-function.md)
