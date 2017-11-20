---
title: "Elegir una gramática SQL | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQL statements [ODBC], interoperability
- interoperability of SQL statements [ODBC], SQL grammar
- SQL grammar [ODBC], selecting
ms.assetid: 4e0d189b-e407-47e0-92a9-f9982230dd0e
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: cc1da3dfbe7f06e7d98430c5cec8fbaab3176971
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="choosing-an-sql-grammar"></a>Elegir una gramática SQL
La primera decisión que debe tomar al crear instrucciones SQL es qué gramática para usar. Además de las gramáticas disponibles en los diferentes organismos de estándares, como Open Group, ANSI e ISO, prácticamente todos los proveedores de DBMS define su propia gramática, cada uno de los cuales varía ligeramente del estándar.  
  
 [Apéndice C: gramática SQL](../../../odbc/reference/appendixes/appendix-c-sql-grammar.md), describe la gramática mínima de SQL deben ser compatible con todos los controladores ODBC. Esta gramática es un subconjunto del nivel de entrada de SQL-92. Los controladores pueden admitir gramática adicional para que se ajuste al nivel intermedio, completo o FIPS 127-2 transitorios niveles definidos por SQL-92. Para obtener más información, consulte [gramática de SQL mínimo](../../../odbc/reference/appendixes/sql-minimum-grammar.md) en la gramática de apéndice C: SQL y SQL-92.  
  
 Apéndice C también define *secuencias de escape* que contiene la gramática estándar para las características de lenguaje disponibles habitualmente, como las combinaciones externas, que no están cubiertos por la gramática de SQL-92. Para obtener más información, consulte [secuencias de Escape de ODBC](../../../odbc/reference/appendixes/odbc-escape-sequences.md) en la gramática de SQL de apéndice C:, y [secuencias de Escape](../../../odbc/reference/develop-app/escape-sequences.md), más adelante en esta sección.  
  
 La gramática elegido afecta a cómo el controlador procesa la instrucción. Deben modificar controladores de SQL de SQL-92 y las secuencias de escape definida por ODBC para DBMS específicos SQL. Dado que las gramáticas SQL mayoría se basan en uno o varios de los distintos estándares, mayoría de los controladores realizar poco o ningún trabajo para satisfacer este requisito. A menudo se compone solo de búsqueda para las secuencias de escape que se define mediante ODBC y reemplazarlos con gramática específica del DBMS. Cuando encuentra con un controlador de gramática no reconoce, se supone la gramática es específica del DBMS y pasa la instrucción SQL sin modificar el origen de datos para su ejecución.  
  
 Por lo tanto, realmente hay dos opciones de gramática para usar: la gramática de SQL-92 (y la secuencias de escape de ODBC) y una gramática específicos del DBMS. De los dos, solo la gramática de SQL-92 es interoperable, por lo que todas las aplicaciones interoperables deberían utilizarlo. Las aplicaciones que no son interoperables pueden usar la gramática de SQL-92 o una gramática específicos del DBMS. Específicos de DBMS gramáticas tienen dos ventajas: pueden aprovechar las características no cubiertas por SQL-92 y son ligeramente más rápidos porque el controlador no tienen que modificarse. La última característica se puede aplicar parcialmente estableciendo el atributo de instrucción SQL_ATTR_NOSCAN, que detiene el controlador de buscar y reemplazar las secuencias de escape.  
  
 Si se utiliza la gramática de SQL-92, la aplicación puede detectar cómo se modifica el controlador mediante una llamada a **SQLNativeSql**. A menudo resulta útil al depurar las aplicaciones. **SQLNativeSql** acepta una instrucción SQL y devuelve después de que el controlador lo ha modificado. Dado que esta función está en el nivel de conformidad de interfaz de núcleo, es compatible con todos los controladores.

