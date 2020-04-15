---
title: Elección de una gramática SQL ( SQL Grammar) Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], interoperability
- interoperability of SQL statements [ODBC], SQL grammar
- SQL grammar [ODBC], selecting
ms.assetid: 4e0d189b-e407-47e0-92a9-f9982230dd0e
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2ca9911d3c88f2f540ff1332d77a2e1ebc6a4942
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299165"
---
# <a name="choosing-an-sql-grammar"></a>Elegir una gramática SQL
La primera decisión a tomar al construir instrucciones SQL es qué gramática usar. Además de las gramáticas disponibles en los distintos organismos de estándares, como Open Group, ANSI e ISO, prácticamente cada proveedor de DBMS define su propia gramática, cada una de las cuales varía ligeramente del estándar.  
  
 [Apéndice C: Gramática SQL](../../../odbc/reference/appendixes/appendix-c-sql-grammar.md), describe la gramática SQL mínima que todos los controladores ODBC deben admitir. Esta gramática es un subconjunto del nivel de entrada de SQL-92. Los controladores pueden admitir gramática adicional para cumplir con los niveles Intermedio, Completo o FIPS 127-2 Transitional definidos por SQL-92. Para obtener más información, vea [Gramática mínima](../../../odbc/reference/appendixes/sql-minimum-grammar.md) de SQL en el Apéndice C: Gramática SQL y SQL-92.  
  
 El Apéndice C también define *secuencias* de escape que contienen gramática estándar para características de lenguaje comúnmente disponibles, como combinaciones externas, que no están cubiertas por la gramática SQL-92. Para obtener más información, vea [Secuencias](../../../odbc/reference/appendixes/odbc-escape-sequences.md) de escape ODBC en apéndice C: gramática SQL y [secuencias](../../../odbc/reference/develop-app/escape-sequences.md)de escape, más adelante en esta sección.  
  
 La gramática elegida afecta a la forma en que el controlador procesa la instrucción. Los controladores deben modificar SQL SQL-92 y las secuencias de escape definidas por ODBC a SQL específico de DBMS. Debido a que la mayoría de las gramáticas SQL se basan en uno o más de los diversos estándares, la mayoría de los controladores hacen poco o ningún trabajo para cumplir con este requisito. A menudo consiste únicamente en buscar las secuencias de escape definidas por ODBC y reemplazarlas por gramática específica de DBMS. Cuando un controlador encuentra gramática que no reconoce, asume que la gramática es específica de DBMS y pasa la instrucción SQL sin modificaciones al origen de datos para su ejecución.  
  
 Por lo tanto, realmente hay dos opciones de gramática para usar: la gramática SQL-92 (y las secuencias de escape ODBC) y una gramática específica de DBMS. De los dos, sólo la gramática SQL-92 es interoperable, por lo que todas las aplicaciones interoperables deben usarla. Las aplicaciones que no son interoperables pueden utilizar la gramática SQL-92 o una gramática específica de DBMS. Las gramáticas específicas de DBMS tienen dos ventajas: pueden explotar cualquier característica no cubierta por SQL-92, y son marginalmente más rápidas porque el controlador no tiene que modificarlas. Esta última característica se puede aplicar parcialmente estableciendo el atributo de instrucción SQL_ATTR_NOSCAN, que impide que el controlador busque y reemplace las secuencias de escape.  
  
 Si se utiliza la gramática SQL-92, la aplicación puede descubrir cómo el controlador la modifica llamando a **SQLNativeSql**. Esto suele ser útil al depurar aplicaciones. **SQLNativeSql** acepta una instrucción SQL y la devuelve después de que el controlador la haya modificado. Dado que esta función está en el nivel de conformidad de la interfaz Core, es compatible con todos los controladores.
