---
title: Llamadas a funciones escalares ? Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- escape sequences [ODBC], scalar function calls
ms.assetid: 10cb4dcf-4cd8-4a56-8725-d080bd3ffe47
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 349599a51b2996f419e6c8656a71bc9e30146542
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304266"
---
# <a name="scalar-function-calls"></a>Llamadas a funciones escalares
Las funciones escalares devuelven un valor para cada fila. Por ejemplo, la función escalar de valor absoluto toma una columna numérica como argumento y devuelve el valor absoluto de cada valor de la columna. La secuencia de escape para llamar a una función escalar es  
  
 **•fn**  _función escalar_ **?**  
  
 donde *la función escalar* es una de las funciones enumeradas en el Apéndice [E: Funciones escalares](../../../odbc/reference/appendixes/appendix-e-scalar-functions.md). Para obtener más información acerca de la secuencia de escape de función escalar, vea Secuencia de escape de [función escalar](../../../odbc/reference/appendixes/scalar-function-escape-sequence.md) en Apéndice C: gramática SQL.  
  
 Por ejemplo, las siguientes instrucciones SQL crean el mismo conjunto de resultados de nombres de cliente en mayúsculas. La primera instrucción utiliza la sintaxis de secuencia de escape. La segunda instrucción utiliza la sintaxis nativa para Ingres para OS/2 y no es interoperable.  
  
```  
SELECT {fn UCASE(Name)} FROM Customers  
  
SELECT uppercase(Name) FROM Customers  
```  
  
 Una aplicación puede mezclar llamadas a funciones escalares que usan sintaxis nativa y llamadas a funciones escalares que usan sintaxis ODBC. Por ejemplo, supongamos que los nombres de la tabla Employee se almacenan como un apellido, una coma y un nombre. La siguiente instrucción SQL crea un conjunto de resultados de apellidos de empleados en la tabla Employee. La instrucción utiliza la función escalar ODBC **SUBSTRING** y la función escalar **charindex** de SQL Server y se ejecutará correctamente solo en SQL Server.  
  
```  
SELECT {fn SUBSTRING(Name, 1, CHARINDEX(',', Name) - 1)} FROM Customers  
```  
  
 Para lograr la máxima interoperabilidad, las aplicaciones deben utilizar la función escalar **CONVERT** para asegurarse de que la salida de una función escalar es el tipo necesario. La función **CONVERT** convierte los datos de un tipo de datos SQL al tipo de datos SQL especificado. La sintaxis de la función **CONVERT** es  
  
 **CONVERT(** _value_exp_ **,** _data_type_**)**  
  
 donde *value_exp* es un nombre de columna, el resultado de otra función escalar o un valor literal, y *data_type* es una palabra clave que coincide con el nombre **de #define** que utiliza un identificador de tipo de datos SQL tal como se define en Apéndice [D: Tipos](../../../odbc/reference/appendixes/appendix-d-data-types.md)de datos . Por ejemplo, la siguiente instrucción SQL utiliza la función **CONVERT** para asegurarse de que la salida de la función **CURDATE** es una fecha, en lugar de una marca de tiempo o datos de caracteres:  
  
```  
INSERT INTO Orders (OrderID, CustID, OpenDate, SalesPerson, Status)  
   VALUES (?, ?, {fn CONVERT({fn CURDATE()}, SQL_DATE)}, ?, ?)  
```  
  
 Para determinar qué funciones escalares son compatibles con un origen de datos, una aplicación llama a **SQLGetInfo** con las opciones SQL_CONVERT_FUNCTIONS, SQL_NUMERIC_FUNCTIONS, SQL_STRING_FUNCTIONS, SQL_SYSTEM_FUNCTIONS y SQL_TIMEDATE_FUNCTIONS. Para determinar qué operaciones de conversión son compatibles con la función **CONVERT,** una aplicación llama a **SQLGetInfo** con cualquiera de las opciones que comienzan con SQL_CONVERT.
