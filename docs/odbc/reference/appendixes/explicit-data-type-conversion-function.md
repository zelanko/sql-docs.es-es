---
title: Función explícita de conversión de tipos de datos ( Data Type Conversion) Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- explicit data type conversion functions [ODBC]
- data type conversion functions [ODBC]
- functions [ODBC], explicit data type conversion functions
ms.assetid: d5789450-b668-4753-96c8-6789e955e7ed
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2de8a8cb6177e9210e8d48c0ce097d13c9a276fd
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306996"
---
# <a name="explicit-data-type-conversion-function"></a>Función de conversión de tipo de datos explícito
La conversión explícita de tipos de datos se especifica en términos de definiciones de tipos de datos SQL.  
  
 La sintaxis ODBC para la función de conversión de tipos de datos explícita no restringe las conversiones. La validez de las conversiones específicas de un tipo de datos a otro tipo de datos se determinará por cada implementación específica del controlador. El controlador, ya que traduce la sintaxis ODBC en la sintaxis nativa, rechazará aquellas conversiones que, aunque legales en la sintaxis ODBC, no son compatibles con el origen de datos. La función ODBC **SQLGetInfo**, con las opciones de conversión (como SQL_CONVERT_BIGINT, SQL_CONVERT_BINARY, SQL_CONVERT_INTERVAL_YEAR_MONTH, etc.), proporciona una manera de consultar las conversiones admitidas por el origen de datos.  
  
 El formato de la función **CONVERT** es:  
  
 **CONVERT(** _value_exp_, _data_type_**)**  
  
 La función devuelve el valor especificado por *value_exp* convierte al *data_type*especificado, donde *data_type* es una de las siguientes palabras clave:  
  
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
  
 La sintaxis ODBC para la función de conversión de tipos de datos explícita no admite la especificación del formato de conversión. Si el origen de datos subyacente admite la especificación de formatos explícitos, un controlador debe especificar un valor predeterminado o implementar la especificación de formato.  
  
 El argumento *value_exp* puede ser un nombre de columna, el resultado de otra función escalar o un literal numérico o de cadena. Por ejemplo:  
  
```  
{ fn CONVERT( { fn CURDATE() }, SQL_CHAR ) }  
```  
  
 convierte la salida de la función escalar CURDATE en una cadena de caracteres.  
  
 Dado que ODBC no exige un tipo de datos para los valores devueltos de funciones escalares (porque las funciones suelen ser específicas del origen de datos), las aplicaciones deben usar la función escalar CONVERT siempre que sea posible para forzar la conversión de tipos de datos.  
  
 Los dos ejemplos siguientes ilustran el uso de la función **CONVERT.** En estos ejemplos se supone la existencia de una tabla denominada EMPLOYEES, con una columna EMPNO de tipo SQL_SMALLINT y una columna EMPNAME de tipo SQL_CHAR.  
  
 Si una aplicación especifica la siguiente instrucción SQL:  
  
```  
SELECT EMPNO FROM EMPLOYEES WHERE {fn CONVERT(EMPNO,SQL_CHAR)} LIKE '1%'  
```  
  
-   Un controlador para ORACLE traduce la instrucción SQL a:  
  
    ```  
    SELECT EMPNO FROM EMPLOYEES WHERE to_char(EMPNO) LIKE '1%'  
    ```  
  
-   Un controlador para SQL Server convierte la instrucción SQL en:  
  
    ```  
    SELECT EMPNO FROM EMPLOYEES WHERE convert(char,EMPNO) LIKE '1%'  
    ```  
  
 Si una aplicación especifica la siguiente instrucción SQL:  
  
```  
SELECT {fn ABS(EMPNO)}, {fn CONVERT(EMPNAME,SQL_SMALLINT)}  
   FROM EMPLOYEES WHERE EMPNO <> 0  
```  
  
-   Un controlador para ORACLE traduce la instrucción SQL a:  
  
    ```  
    SELECT abs(EMPNO), to_number(EMPNAME) FROM EMPLOYEES WHERE EMPNO <> 0  
    ```  
  
-   Un controlador para SQL Server convierte la instrucción SQL en:  
  
    ```  
    SELECT abs(EMPNO), convert(smallint, EMPNAME) FROM EMPLOYEES  
       WHERE EMPNO <> 0  
    ```  
  
-   Un controlador para Ingres traduce la instrucción SQL a:  
  
    ```  
    SELECT abs(EMPNO), int2(EMPNAME) FROM EMPLOYEES WHERE EMPNO <> 0  
    ```
