---
title: Elección de una gramática de SQL | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "81299165"
---
# <a name="choosing-an-sql-grammar"></a>Elegir una gramática SQL
La primera decisión que debe tomarse al construir instrucciones SQL es la gramática que se va a usar. Además de las gramáticas disponibles de los distintos cuerpos de estándares, como Open Group, ANSI e ISO, prácticamente todos los proveedores de DBMS definen su propia gramática, cada una de las cuales varía ligeramente con respecto al estándar.  
  
 En el [Apéndice C: gramática de SQL](../../../odbc/reference/appendixes/appendix-c-sql-grammar.md), se describe la gramática de SQL mínima que todos los controladores ODBC deben admitir. Esta gramática es un subconjunto del nivel de entrada de SQL-92. Los controladores pueden admitir gramática adicional para ajustarse a los niveles de transición intermedio, completo o FIPS 127-2 definidos por SQL-92. Para obtener más información, vea [gramática mínima de SQL](../../../odbc/reference/appendixes/sql-minimum-grammar.md) en el Apéndice C: gramática de SQL y sql-92.  
  
 En el Apéndice C también se definen *secuencias de escape* que contienen gramática estándar para las características de lenguaje disponibles con frecuencia, como las combinaciones externas, que no se incluyen en la gramática de SQL-92. Para obtener más información, vea [secuencias de escape de ODBC](../../../odbc/reference/appendixes/odbc-escape-sequences.md) en el Apéndice C: gramática de SQL y secuencias de [escape](../../../odbc/reference/develop-app/escape-sequences.md), más adelante en esta sección.  
  
 La gramática elegida afecta a la forma en que el controlador procesa la instrucción. Los controladores deben modificar SQL-92 SQL y las secuencias de escape definidas por ODBC a SQL específico del DBMS. Dado que la mayoría de las gramáticas de SQL se basan en uno o varios de los distintos estándares, la mayoría de los controladores realizan pocos o ningún trabajo para cumplir este requisito. A menudo, solo consiste en buscar las secuencias de escape definidas por ODBC y reemplazarlas por una gramática específica del DBMS. Cuando un controlador encuentra la gramática que no reconoce, supone que la gramática es específica de DBMS y pasa la instrucción SQL sin modificar el origen de datos para su ejecución.  
  
 Por lo tanto, en realidad hay dos opciones de gramática para usar: la gramática de SQL-92 (y las secuencias de escape de ODBC) y una gramática específica del DBMS. De ambos, solo la gramática de SQL-92 es interoperable, por lo que todas las aplicaciones interoperables deben utilizarla. Las aplicaciones que no son interoperables pueden usar la gramática de SQL-92 o una gramática específica del DBMS. Las gramáticas específicas de DBMS tienen dos ventajas: pueden aprovechar las características que no se incluyen en SQL-92 y son ligeramente más rápidas, ya que el controlador no tiene que modificarlas. Esta última característica se puede aplicar parcialmente estableciendo el atributo de instrucción SQL_ATTR_NOSCAN, que impide que el controlador busque y reemplace secuencias de escape.  
  
 Si se usa la gramática SQL-92, la aplicación puede detectar cómo la modifica el controlador mediante una llamada a **SQLNativeSql**. Esto suele ser útil al depurar aplicaciones. **SQLNativeSql** acepta una instrucción SQL y la devuelve una vez que el controlador la ha modificado. Dado que esta función está en el nivel de conformidad de la interfaz básica, es compatible con todos los controladores.
