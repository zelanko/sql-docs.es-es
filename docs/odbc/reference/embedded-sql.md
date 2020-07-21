---
title: SQL incrustado | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "81306678"
---
# <a name="embedded-sql"></a>SQL incrustado
La primera técnica para enviar instrucciones SQL al DBMS es Embedded SQL. Dado que SQL no utiliza variables y instrucciones de control de flujo, a menudo se usa como un subidioma de base de datos que se puede Agregar a un programa escrito en un lenguaje de programación convencional, como C o COBOL. Se trata de una idea central de SQL incrustado: colocar instrucciones SQL en un programa escrito en un lenguaje de programación de host. Brevemente, se usan las técnicas siguientes para insertar instrucciones SQL en un idioma host:  
  
-   Las instrucciones SQL incrustadas las procesa un precompilador de SQL especial. Todas las instrucciones SQL comienzan con un presentador y finalizan con un terminador, que marcan la instrucción SQL para el precompilador. El presentador y el terminador varían con el idioma del host. Por ejemplo, el presentador es "EXEC SQL" en C y "&SQL (" en las PAPERas, y el terminador es un punto y coma (;) en C y un paréntesis derecho en PAPERs.  
  
-   Las variables del programa de aplicación, denominadas variables de host, se pueden usar en instrucciones SQL incrustadas siempre que se permitan constantes. Se pueden usar en la entrada para adaptar una instrucción SQL a una situación determinada y en la salida para recibir los resultados de una consulta.  
  
-   Las consultas que devuelven una única fila de datos se administran con una instrucción SELECT de singleton; Esta instrucción especifica la consulta y las variables de host en las que se van a devolver los datos.  
  
-   Las consultas que devuelven varias filas de datos se controlan con cursores. Un cursor realiza un seguimiento de la fila actual dentro de un conjunto de resultados. La instrucción DECLARE CURSOR define la consulta, la instrucción OPEN comienza el procesamiento de la consulta, la instrucción FETCH recupera filas sucesivas de datos y la instrucción CLOSE finaliza el procesamiento de la consulta.  
  
-   Mientras un cursor está abierto, se pueden usar las instrucciones Update y DELETE posicionadas para actualizar o eliminar la fila seleccionada actualmente por el cursor.  
  
 Esta sección contiene los temas siguientes.  
  
-   [Ejemplo de SQL incrustado](../../odbc/reference/embedded-sql-example.md)  
  
-   [Compilar un programa SQL incrustado](../../odbc/reference/compiling-an-embedded-sql-program.md)  
  
-   [SQL estático](../../odbc/reference/static-sql.md)  
  
-   [SQL dinámico](../../odbc/reference/dynamic-sql.md)
