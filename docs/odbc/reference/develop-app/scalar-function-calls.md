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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67897748"
---
# <a name="scalar-function-calls"></a>Llamadas a funciones escalares
Funciones escalares devuelven un valor para cada fila. Por ejemplo, la función escalar del valor absoluto toma una columna numérica como argumento y devuelve el valor absoluto de cada valor de la columna. Es la secuencia de escape para llamar a una función escalar  
  
 **{fn**_función escalar_ **}**  
  
 donde *función escalar* es una de las funciones enumeradas en [Apéndice E: Funciones escalares](../../../odbc/reference/appendixes/appendix-e-scalar-functions.md). Para obtener más información acerca de la secuencia de escape de la función escalar, vea [secuencia de Escape de función escalar](../../../odbc/reference/appendixes/scalar-function-escape-sequence.md) en el apéndice C: Gramática de SQL.  
  
 Por ejemplo, las siguientes instrucciones SQL crean el mismo conjunto de resultados del cliente en mayúsculas los nombres. La primera instrucción usa la sintaxis de la secuencia de escape. La segunda instrucción usa la sintaxis nativa para Ingres para OS/2 y no es interoperable.  
  
```  
SELECT {fn UCASE(Name)} FROM Customers  
  
SELECT uppercase(Name) FROM Customers  
```  
  
 Una aplicación puede combinar las llamadas a funciones escalares que utilice sintaxis nativa y las llamadas a funciones escalares que utilizan la sintaxis ODBC. Por ejemplo, suponga que los nombres de la tabla de empleados se almacenan como un apellido, una coma y un nombre. La instrucción SQL siguiente crea un conjunto de resultados de los apellidos de los empleados en la tabla Employee. La instrucción utiliza la función escalar de ODBC **SUBCADENA** y la función escalar de SQL Server **CHARINDEX** y se ejecutará correctamente sólo en SQL Server.  
  
```  
SELECT {fn SUBSTRING(Name, 1, CHARINDEX(',', Name) - 1)} FROM Customers  
```  
  
 Para obtener la máxima interoperatividad, las aplicaciones deben usar el **convertir** función escalar para asegurarse de que el resultado de una función escalar es el tipo requerido. El **convertir** función convierte los datos de un tipo de datos SQL en el tipo de datos SQL especificado. La sintaxis de la **convertir** es la función  
  
 **CONVERT(** _value_exp_ **,** _data_type_ **)**  
  
 donde *value_exp* es un nombre de columna, el resultado de otra función escalar o un valor literal, y *data_type* es una palabra clave que coincida con el **#define** nombre utilizado por un Identificador de tipo de datos SQL tal como se define en [apéndice D: Tipos de datos](../../../odbc/reference/appendixes/appendix-d-data-types.md). Por ejemplo, la siguiente instrucción SQL utiliza el **convertir** función para asegurarse de que la salida de la **CURDATE** función es una fecha, en lugar de una marca de tiempo o caracteres de datos:  
  
```  
INSERT INTO Orders (OrderID, CustID, OpenDate, SalesPerson, Status)  
   VALUES (?, ?, {fn CONVERT({fn CURDATE()}, SQL_DATE)}, ?, ?)  
```  
  
 Para determinar qué funciones escalares son compatibles con un origen de datos, una aplicación llama a **SQLGetInfo** SQL_CONVERT_FUNCTIONS, SQL_NUMERIC_FUNCTIONS, SQL_STRING_FUNCTIONS, SQL_SYSTEM_FUNCTIONS y SQL_TIMEDATE_ Opciones de funciones. Para determinar qué operaciones de conversión son compatibles con el **convertir** llama una aplicación de función, **SQLGetInfo** con cualquiera de las opciones que empiezan por SQL_CONVERT.
