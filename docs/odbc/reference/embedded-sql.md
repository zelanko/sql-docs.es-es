---
title: SQL integrado ? Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9ad6fd2753d026f026d72a7aa8f68d5d48ce03cb
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306678"
---
# <a name="embedded-sql"></a>SQL incrustado
La primera técnica para enviar instrucciones SQL al DBMS es SQL incrustado. Dado que SQL no utiliza variables ni instrucciones de control de flujo, a menudo se utiliza como un sublenguaje de base de datos que se puede agregar a un programa escrito en un lenguaje de programación convencional, como C o COBOL. Esta es una idea central de SQL incrustado: colocar instrucciones SQL en un programa escrito en un lenguaje de programación host. En resumen, se utilizan las siguientes técnicas para incrustar instrucciones SQL en un lenguaje host:  
  
-   Las instrucciones SQL incrustadas se procesan mediante un precompilador SQL especial. Todas las instrucciones SQL comienzan con un introductor y terminan con un terminador, que marcan la instrucción SQL para el precompilador. El introductor y el terminador varían según el idioma del host. Por ejemplo, el introductor es "EXEC SQL" en C y "&SQL(" en MUMPS, y el terminador es un punto y coma (;) en C y un paréntesis derecho en MUMPS.  
  
-   Las variables del programa de aplicación, denominadas variables de host, se pueden utilizar en instrucciones SQL incrustadas siempre que se permitan constantes. Se pueden utilizar en la entrada para adaptar una instrucción SQL a una situación determinada y en la salida para recibir los resultados de una consulta.  
  
-   Las consultas que devuelven una sola fila de datos se controlan con una instrucción SELECT singleton; esta instrucción especifica la consulta y las variables de host en las que se devuelven datos.  
  
-   Las consultas que devuelven varias filas de datos se controlan con cursores. Un cursor realiza un seguimiento de la fila actual dentro de un conjunto de resultados. La instrucción DECLARE CURSOR define la consulta, la instrucción OPEN comienza el procesamiento de consultas, la instrucción FETCH recupera filas sucesivas de datos y la instrucción CLOSE finaliza el procesamiento de consultas.  
  
-   Mientras un cursor está abierto, las instrucciones de actualización y eliminación posicionadas se pueden utilizar para actualizar o eliminar la fila seleccionada actualmente por el cursor.  
  
 Esta sección contiene los temas siguientes.  
  
-   [Ejemplo de SQL incrustado](../../odbc/reference/embedded-sql-example.md)  
  
-   [Compilar un programa SQL incrustado](../../odbc/reference/compiling-an-embedded-sql-program.md)  
  
-   [SQL estático](../../odbc/reference/static-sql.md)  
  
-   [SQL dinámico](../../odbc/reference/dynamic-sql.md)
