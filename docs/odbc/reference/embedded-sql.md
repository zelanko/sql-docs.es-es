---
title: Incrustar SQL | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQL [ODBC], embedded SQL
- sending SQL statements to DBMS [ODBC]
- SQL statements [ODBC], embedded SQL
- ODBC [ODBC], SQL
- embedded SQL [ODBC]
ms.assetid: 8eee3527-f225-4aa2-bd18-a16bd3ab0fb7
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: db7c9b02f885c09df1eccbdc27ef2fd895168848
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="embedded-sql"></a>SQL incrustado
La primera técnica para enviar instrucciones SQL en el DBMS se incrusta SQL. Dado que SQL no usa las variables y las instrucciones de control de flujo, se usa a menudo como una variante de idioma de la base de datos que se puede agregar a un programa escrito en un lenguaje de programación convencional, como C o COBOL. Se trata de una idea central de SQL incrustado: colocar instrucciones SQL en un programa escrito en un host del lenguaje de programación. En pocas palabras, las técnicas siguientes se utilizan para incrustar instrucciones SQL en un lenguaje host:  
  
-   Instrucciones SQL incrustadas se procesan por un precompilador especial de SQL. Todas las instrucciones SQL comienzan con un iniciador y finalizan con un terminador, que marca el precompilador que la instrucción SQL. El iniciador y el terminador varían con el lenguaje del host. Por ejemplo, el iniciador es "EXEC SQL" en C y "& SQL (" en PAPERAS, y el terminador es un punto y coma (;) en C y un paréntesis de cierre en PAPERAS.  
  
-   Variables desde el programa de aplicación, que se denominan variables de host, pueden utilizarse en instrucciones SQL incrustadas donde se permiten constantes. Se pueden usar en la entrada para adaptarse a una instrucción SQL a su situación particular y en la salida para recibir los resultados de una consulta.  
  
-   Las consultas que devuelven una única fila de datos se controlan con una instrucción SELECT de singleton; Esta instrucción especifica la consulta y las variables de host en el que se va a devolver datos.  
  
-   Las consultas que devuelven varias filas de datos se controlan con cursores. Un cursor realiza un seguimiento de la fila actual en un conjunto de resultados. La instrucción DECLARE CURSOR define la consulta, la instrucción OPEN comienza el procesamiento de consulta, la instrucción FETCH recupera las filas sucesivas de los datos y la instrucción CLOSE finaliza el procesamiento de consultas.  
  
-   Mientras el cursor está abierto, actualización por posición y las instrucciones delete posicionadas pueden utilizarse para actualizar o eliminar la fila seleccionada actualmente el cursor.  
  
 Esta sección contiene los temas siguientes.  
  
-   [Ejemplo de SQL incrustado](../../odbc/reference/embedded-sql-example.md)  
  
-   [Compilar un programa SQL incrustado](../../odbc/reference/compiling-an-embedded-sql-program.md)  
  
-   [SQL estático](../../odbc/reference/static-sql.md)  
  
-   [SQL dinámico](../../odbc/reference/dynamic-sql.md)
