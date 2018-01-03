---
title: "Función de conversión de tipos de datos explícitos | Documentos de Microsoft"
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
- explicit data type conversion functions [ODBC]
- data type conversion functions [ODBC]
- functions [ODBC], explicit data type conversion functions
ms.assetid: d5789450-b668-4753-96c8-6789e955e7ed
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: c1520ca18c42d2efbc2822630fe7ccae9f90302a
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="explicit-data-type-conversion-function"></a>Función de conversión de tipo de datos explícito
Conversión de tipos de datos explícitos se especifica en términos de definiciones de tipo de datos SQL.  
  
 La sintaxis ODBC para la función de conversión de tipo de datos explícito no restringe las conversiones. Se puede determinar la validez de las conversiones específicas de un tipo de datos a otro tipo de datos por cada implementación específicos del controlador. El controlador rechazará, tal y como se traduce la sintaxis ODBC en la sintaxis nativo, aquellas conversiones que, aunque legal en la sintaxis ODBC, no son compatibles con el origen de datos. La función ODBC **SQLGetInfo**, con la conversión opciones (por ejemplo, SQL_CONVERT_BIGINT, SQL_CONVERT_BINARY, SQL_CONVERT_INTERVAL_YEAR_MONTH y así sucesivamente), proporciona una manera de realizar consultas sobre las conversiones compatibles con el origen de datos .  
  
 El formato de la **convertir** función es:  
  
 **CONVERTIR (** *value_exp*, *data_type***)**  
  
 La función devuelve el valor especificado por *value_exp* convertir al especificado *data_type*, donde *data_type* es una de las siguientes palabras clave:  
  
|||  
|-|-|  
|SQL_BIGINT|SQL_INTERVAL_HOUR_TO_MINUTE|  
|SQL_BINARY|SQL_INTERVAL_HOUR_TO_SECOND|  
|SQL_BIT|SQL_INTERVAL_MINUTE_TO_SECOND|  
|SQL_CHAR|SQL_LONGVARBINARY|  
|SQL_DECIMAL|SQL_LONGVARCHAR|  
|SQL_DOUBLE|SQL_NUMERIC|  
|SQL_FLOAT|SQL_REAL|  
|SQL_GUID|SQL_SMALLINT|  
|SQL_INTEGER|SQL_DATE|  
|SQL_INTERVAL_MONTH|SQL_TIME|  
|SQL_INTERVAL_YEAR|SQL_TIMESTAMP|  
|SQL_INTERVAL_YEAR_TO_MONTH|SQL_TINYINT|  
|SQL_INTERVAL_DAY|SQL_VARBINARY|  
|SQL_INTERVAL_HOUR|SQL_VARCHAR|  
|SQL_INTERVAL_MINUTE|SQL_WCHAR|  
|SQL_INTERVAL_SECOND|SQL_WLONGVARCHAR|  
|SQL_INTERVAL_DAY_TO_HOUR|SQL_WVARCHAR|  
|SQL_INTERVAL_DAY_TO_MINUTE||  
|SQL_INTERVAL_DAY_TO_SECOND||  
  
 La sintaxis ODBC para la función de conversión de tipo de datos explícito no admite la especificación de formato de conversión. Si la especificación de formatos explícitos es compatible con el origen de datos subyacente, un controlador debe especificar un valor predeterminado o implementar la especificación de formato.  
  
 El argumento *value_exp* puede ser un nombre de columna, el resultado de otra función escalar o un valor numérico o cadena literal. Por ejemplo:  
  
```  
{ fn CONVERT( { fn CURDATE() }, SQL_CHAR ) }  
```  
  
 Convierte el resultado de la función escalar CURDATE en una cadena de caracteres.  
  
 Dado que ODBC no impone un tipo de datos para los valores devueltos de funciones escalares (dado que las funciones son a menudo específico del origen de datos), las aplicaciones deben utilizar la función escalar CONVERT siempre que sea posible forzar la conversión de tipo de datos.  
  
 Los dos ejemplos siguientes muestran el uso de la **convertir** función. Estos ejemplos supone la existencia de una tabla denominada a EMPLOYEES, con una columna EMPNO de tipo SQL_SMALLINT y una columna EMPNAME de tipo SQL_CHAR.  
  
 Si una aplicación especifica la siguiente instrucción SQL:  
  
```  
SELECT EMPNO FROM EMPLOYEES WHERE {fn CONVERT(EMPNO,SQL_CHAR)} LIKE '1%'  
```  
  
-   La instrucción SQL que traduce en un controlador para ORACLE:  
  
    ```  
    SELECT EMPNO FROM EMPLOYEES WHERE to_char(EMPNO) LIKE '1%'  
    ```  
  
-   Un controlador de SQL Server traduce la instrucción SQL para:  
  
    ```  
    SELECT EMPNO FROM EMPLOYEES WHERE convert(char,EMPNO) LIKE '1%'  
    ```  
  
 Si una aplicación especifica la siguiente instrucción SQL:  
  
```  
SELECT {fn ABS(EMPNO)}, {fn CONVERT(EMPNAME,SQL_SMALLINT)}  
   FROM EMPLOYEES WHERE EMPNO <> 0  
```  
  
-   La instrucción SQL que traduce en un controlador para ORACLE:  
  
    ```  
    SELECT abs(EMPNO), to_number(EMPNAME) FROM EMPLOYEES WHERE EMPNO <> 0  
    ```  
  
-   Un controlador de SQL Server traduce la instrucción SQL para:  
  
    ```  
    SELECT abs(EMPNO), convert(smallint, EMPNAME) FROM EMPLOYEES  
       WHERE EMPNO <> 0  
    ```  
  
-   Un controlador para Ingres traduce la instrucción SQL para:  
  
    ```  
    SELECT abs(EMPNO), int2(EMPNAME) FROM EMPLOYEES WHERE EMPNO <> 0  
    ```
