---
title: Niveles de compatibilidad de SQL | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- conformance levels [ODBC], SQL
- SQL conformance levels [ODBC]
- data sources [ODBC], conformance levels
- ODBC drivers [ODBC], conformance levels
ms.assetid: 3529df2c-a09b-4c16-9c60-eae7a06d903a
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1b9e352aad9c99b56c08767ca57547b9b6594a17
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="sql-conformance-levels"></a>Niveles de compatibilidad de SQL
El nivel de gramática de SQL-92 compatible con un controlador se indica mediante el valor devuelto por una llamada a **SQLGetInfo** con el tipo de información de SQL_SQL_CONFORMANCE. Esto indica si el controlador es compatible con los niveles de entrada, la transición de FIPS, intermedio o completo definidos en SQL-92.  
  
 Todos los controladores ODBC deben ser compatible con la gramática mínima de SQL que se describe en [gramática mínima de SQL](../../../odbc/reference/appendixes/sql-minimum-grammar.md) en la gramática de SQL de apéndice C:. Esta gramática es un subconjunto del nivel de entrada de SQL-92. Controladores pueden admitir SQL adicionales y sea compatible en el nivel de entrada de SQL-92, intermedio o completo, o para el estándar FIPS 127-2 nivel de transición. Controladores que cumplan con un nivel determinado de SQL-92 o FIPS 127-2 pueden admitir características adicionales en cualquiera de los niveles superiores aún no sea totalmente compatible con ese nivel. Para determinar si se admite una característica, una aplicación debe llamar a **SQLGetInfo** con el tipo de información adecuada. El nivel de conformidad de una característica SQL se describe en el tipo de información correspondiente. (Consulte la [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) descripción de la función.)
