---
title: Elegir una gramática SQL | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 670ed0adbbd5ad993af0942d492ee19f75fa9628
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47848033"
---
# <a name="choosing-an-sql-grammar"></a>Elegir una gramática SQL
La primera decisión tomar al crear instrucciones SQL es qué gramática para usar. Además de las gramáticas disponibles en los diferentes organismos de estándares, como Open Group, ANSI e ISO, prácticamente todos los proveedores de DBMS define su propio gramatical, cada uno de los cuales varía ligeramente del estándar.  
  
 [Apéndice C: gramática SQL](../../../odbc/reference/appendixes/appendix-c-sql-grammar.md), se describe la gramática mínima de SQL que deben admitir todos los controladores ODBC. Esta gramática es un subconjunto del nivel de entrada de SQL-92. Los controladores pueden admitir gramática adicional para que se ajuste al nivel intermedio, completo o FIPS 127-2 transitorios niveles definidos en SQL-92. Para obtener más información, consulte [gramática mínima de SQL](../../../odbc/reference/appendixes/sql-minimum-grammar.md) en la gramática de apéndice C: SQL y SQL-92.  
  
 Apéndice C también define *secuencias de escape* que contiene la gramática estándar para características de lenguaje disponibles habitualmente, como las combinaciones externas, que no están cubiertos por la gramática de SQL-92. Para obtener más información, consulte [secuencias de Escape ODBC](../../../odbc/reference/appendixes/odbc-escape-sequences.md) en la gramática de SQL de apéndice C:, y [secuencias de Escape](../../../odbc/reference/develop-app/escape-sequences.md), más adelante en esta sección.  
  
 La gramática que se ha elegido afecta a cómo el controlador procesa la instrucción. Deben modificar los controladores de SQL de SQL-92 y las secuencias de escape definida por ODBC para SQL específicos para DBMS. Porque la mayoría de las gramáticas SQL se basan en uno o varios de los distintos estándares, mayoría de los controladores realizan poco o ningún trabajo para satisfacer este requisito. A menudo se compone solo de búsqueda para las secuencias de escape definidas mediante ODBC y reemplazarlos con gramática específicos para DBMS. Cuando encuentra con un controlador de gramática que no reconoce, se supone la gramática es específico de DBMS y pasa la instrucción SQL sin necesidad de modificar el origen de datos para su ejecución.  
  
 Por lo tanto, realmente hay dos opciones de gramática para usar: la gramática de SQL-92 (y la secuencias de escape de ODBC) y una gramática específicos para DBMS. De los dos, solo la gramática de SQL-92 es interoperable, por lo que todas las aplicaciones interoperables deberían usarlo. La gramática de SQL-92 o de una gramática específicos para DBMS, pueden usar las aplicaciones que no son interoperables. Gramáticas específicos para DBMS tienen dos ventajas: puede aprovecharse de las características no cubiertas por SQL-92 y son ligeramente más rápidos porque no tiene el controlador modificarlos. La última característica se puede aplicar parcialmente estableciendo el atributo de instrucción SQL_ATTR_NOSCAN, que detiene el controlador de buscar y reemplazar las secuencias de escape.  
  
 Si se usa la gramática de SQL-92, la aplicación puede descubrir cómo se modifica el controlador mediante una llamada a **SQLNativeSql**. A menudo resulta útil al depurar aplicaciones. **SQLNativeSql** acepta una instrucción SQL y lo devuelve después de que el controlador lo ha modificado. Dado que esta función está en el nivel de conformidad de interfaz de Core, es compatible con todos los controladores.
