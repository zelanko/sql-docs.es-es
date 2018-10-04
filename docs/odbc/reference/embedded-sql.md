---
title: SQL incrustadas | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL [ODBC], embedded SQL
- sending SQL statements to DBMS [ODBC]
- SQL statements [ODBC], embedded SQL
- ODBC [ODBC], SQL
- embedded SQL [ODBC]
ms.assetid: 8eee3527-f225-4aa2-bd18-a16bd3ab0fb7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 47936b5c085514fca4ecc1c81057ef78a19f05c5
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47855290"
---
# <a name="embedded-sql"></a>SQL incrustado
La primera técnica para enviar instrucciones SQL para el DBMS se incrusta SQL. Dado que no usan SQL variables y las instrucciones de control de flujo, se utiliza a menudo como una variante de idioma de la base de datos que se puede agregar a un programa escrito en un lenguaje de programación convencional, como C o COBOL. Se trata de una idea central de SQL incrustado: colocar instrucciones SQL en un programa escrito en un host de lenguaje de programación. En pocas palabras, las técnicas siguientes se utilizan para incrustar instrucciones SQL en un lenguaje de host:  
  
-   Instrucciones SQL insertadas se procesan por un precompilador SQL especial. Todas las instrucciones SQL comienzan con un iniciador y terminan con un terminador, que marca la instrucción SQL para el precompilador. El iniciador y el terminador varían con el lenguaje del host. Por ejemplo, el iniciador es "EXEC SQL" en C y "& SQL (" en PAPERAS, y el terminador es un punto y coma (;) en C y un paréntesis derecho en PAPERAS.  
  
-   Variables desde el programa de aplicación, que se denominan variables de host, pueden usarse en instrucciones SQL insertadas siempre que se permiten constantes. Estos se pueden usar en la entrada para adaptar una instrucción SQL para una situación determinada y en la salida para recibir los resultados de una consulta.  
  
-   Las consultas que devuelven una única fila de datos se controlan con una instrucción SELECT singleton; Esta instrucción especifica que la consulta y las variables de host en el que se va a devolver los datos.  
  
-   Las consultas que devuelven varias filas de datos se controlan con cursores. Un cursor realiza un seguimiento de la fila actual dentro de un conjunto de resultados. La instrucción DECLARE CURSOR define la consulta, la instrucción OPEN comienza el procesamiento de consultas, la instrucción FETCH recupera las sucesivas filas de datos y la instrucción CLOSE finaliza el procesamiento de consultas.  
  
-   Mientras el cursor está abierto, pueden utilizarse para actualizar o eliminar la fila seleccionada actualmente por el cursor actualización posicionada y las instrucciones delete posicionadas.  
  
 Esta sección contiene los temas siguientes.  
  
-   [Ejemplo de SQL incrustado](../../odbc/reference/embedded-sql-example.md)  
  
-   [Compilar un programa SQL incrustado](../../odbc/reference/compiling-an-embedded-sql-program.md)  
  
-   [SQL estático](../../odbc/reference/static-sql.md)  
  
-   [SQL dinámico](../../odbc/reference/dynamic-sql.md)
