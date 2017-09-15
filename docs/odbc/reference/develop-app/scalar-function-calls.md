---
title: Llamadas a funciones escalares | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- escape sequences [ODBC], scalar function calls
ms.assetid: 10cb4dcf-4cd8-4a56-8725-d080bd3ffe47
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 3fb62d7c916584da7411f398f66a2acf134bfa24
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="scalar-function-calls"></a>Llamadas a funciones escalares
Funciones escalares devuelven un valor para cada fila. Por ejemplo, la función escalar del valor absoluto toma una columna numérica como argumento y devuelve el valor absoluto de cada valor de la columna. Es la secuencia de escape para llamar a una función escalar  
  
 **{fn***función escalar* **}  **  
  
 donde *función escalar* es una de las funciones mostradas en [funciones escalares de apéndice E:](../../../odbc/reference/appendixes/appendix-e-scalar-functions.md). Para obtener más información acerca de la secuencia de escape de la función escalar, vea [secuencia de Escape de función escalar](../../../odbc/reference/appendixes/scalar-function-escape-sequence.md) en Apéndice C: SQL gramática.  
  
 Por ejemplo, las siguientes instrucciones SQL crean el mismo conjunto de resultados de cliente en mayúsculas los nombres. La primera instrucción utiliza la sintaxis de la secuencia de escape. La segunda instrucción utiliza la sintaxis nativa para Ingres para OS/2 y no es interoperable.  
  
```  
SELECT {fn UCASE(Name)} FROM Customers  
  
SELECT uppercase(Name) FROM Customers  
```  
  
 Una aplicación puede mezclar llamadas a funciones escalares que usan una sintaxis nativa y las llamadas a funciones escalares que utilizan la sintaxis ODBC. Por ejemplo, suponga que los nombres en la tabla de empleados se almacenan como un apellido, una coma y un nombre. La instrucción SQL siguiente crea un conjunto de resultados de los últimos nombres de los empleados de la tabla Employee. La instrucción utiliza la función escalar de ODBC **SUBCADENA** y la función escalar de SQL Server **CHARINDEX** y se ejecutará correctamente sólo en SQL Server.  
  
```  
SELECT {fn SUBSTRING(Name, 1, CHARINDEX(',', Name) – 1)} FROM Customers  
```  
  
 Para obtener una interoperabilidad máxima, las aplicaciones deben utilizar la **convertir** función escalar para asegurarse de que el resultado de una función escalar es el tipo requerido. El **convertir** función convierte datos de un tipo de datos SQL en el tipo de datos SQL especificado. La sintaxis de la **convertir** es (función)  
  
 **CONVERTIR (** *value_exp* **,** *data_type***)**  
  
 donde *value_exp* es un nombre de columna, el resultado de otra función escalar o un valor literal, y *data_type* es una palabra clave que coincida con el **#define** nombre utilizado por un Identificador de tipo de datos SQL tal como se define en [tipos de datos de apéndice D:](../../../odbc/reference/appendixes/appendix-d-data-types.md). Por ejemplo, la siguiente instrucción SQL utiliza el **convertir** función para asegurarse de que el resultado de la **CURDATE** función es una fecha, en lugar de una marca de tiempo o caracteres de datos:  
  
```  
INSERT INTO Orders (OrderID, CustID, OpenDate, SalesPerson, Status)  
   VALUES (?, ?, {fn CONVERT({fn CURDATE()}, SQL_DATE)}, ?, ?)  
```  
  
 Para determinar qué funciones escalares son compatibles con un origen de datos, una aplicación llama **SQLGetInfo** con SQL_CONVERT_FUNCTIONS, SQL_NUMERIC_FUNCTIONS, SQL_STRING_FUNCTIONS, SQL_SYSTEM_FUNCTIONS y SQL_TIMEDATE_ Opciones de funciones. Para determinar qué operaciones de conversión son compatibles con el **convertir** función, llama a una aplicación **SQLGetInfo** con cualquiera de las opciones que empiezan por SQL_CONVERT.
