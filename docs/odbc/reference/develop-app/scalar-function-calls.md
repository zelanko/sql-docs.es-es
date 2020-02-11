---
title: Llamadas a funciones escalares | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 37209a75c03a051e3def4d26fa0d4e7f85d0e91d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "67897748"
---
# <a name="scalar-function-calls"></a>Llamadas a funciones escalares
Las funciones escalares devuelven un valor para cada fila. Por ejemplo, la función escalar de valor absoluto toma una columna numérica como argumento y devuelve el valor absoluto de cada valor de la columna. La secuencia de escape para llamar a una función escalar es  
  
 **{FN**  _función escalar_ **}**  
  
 donde *función escalar* es una de las funciones enumeradas en el [Apéndice E: funciones escalares](../../../odbc/reference/appendixes/appendix-e-scalar-functions.md). Para obtener más información sobre la secuencia de escape de la función escalar, vea [secuencia de escape de función escalar](../../../odbc/reference/appendixes/scalar-function-escape-sequence.md) en el Apéndice C: gramática de SQL.  
  
 Por ejemplo, las siguientes instrucciones SQL crean el mismo conjunto de resultados de nombres de clientes en mayúsculas. La primera instrucción usa la sintaxis de secuencia de escape. La segunda instrucción usa la sintaxis nativa para Ingres para OS/2 y no es interoperable.  
  
```  
SELECT {fn UCASE(Name)} FROM Customers  
  
SELECT uppercase(Name) FROM Customers  
```  
  
 Una aplicación puede mezclar llamadas a funciones escalares que usan la sintaxis nativa y llamadas a funciones escalares que usan la sintaxis ODBC. Por ejemplo, suponga que los nombres de la tabla Employee se almacenan como apellidos, una coma y un nombre. La siguiente instrucción SQL crea un conjunto de resultados de los apellidos de los empleados de la tabla Employee. La instrucción utiliza la **SUBcadena** de la función escalar de ODBC y la función escalar SQL Server **CHARINDEX** y se ejecutará correctamente solo en SQL Server.  
  
```  
SELECT {fn SUBSTRING(Name, 1, CHARINDEX(',', Name) - 1)} FROM Customers  
```  
  
 Para obtener la máxima interoperabilidad, las aplicaciones deben usar la función escalar **Convert** para asegurarse de que la salida de una función escalar es el tipo necesario. La función **Convert** convierte los datos de un tipo de datos SQL al tipo de datos SQL especificado. La sintaxis de la función **Convert** es  
  
 **Convert (** _value_exp_ **,** _data_type_**)**  
  
 donde *value_exp* es un nombre de columna, el resultado de otra función escalar o un valor literal, y *data_type* es una palabra clave que coincide con el nombre de **#define** que usa un identificador de tipo de datos de SQL, tal y como se define en el [Apéndice D: tipos de datos](../../../odbc/reference/appendixes/appendix-d-data-types.md). Por ejemplo, la siguiente instrucción SQL usa la función **Convert** para asegurarse de que la salida de la función **CURDATE** es una fecha, en lugar de una marca de tiempo o datos de caracteres:  
  
```  
INSERT INTO Orders (OrderID, CustID, OpenDate, SalesPerson, Status)  
   VALUES (?, ?, {fn CONVERT({fn CURDATE()}, SQL_DATE)}, ?, ?)  
```  
  
 Para determinar qué funciones escalares se admiten en un origen de datos, una aplicación llama a **SQLGetInfo** con las opciones SQL_CONVERT_FUNCTIONS, SQL_NUMERIC_FUNCTIONS, SQL_STRING_FUNCTIONS, SQL_SYSTEM_FUNCTIONS y SQL_TIMEDATE_FUNCTIONS. Para determinar qué operaciones de conversión son compatibles con la función **Convert** , una aplicación llama a **SQLGetInfo** con cualquiera de las opciones que comienzan con SQL_CONVERT.
