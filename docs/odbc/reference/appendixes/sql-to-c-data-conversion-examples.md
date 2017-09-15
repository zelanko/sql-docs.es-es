---
title: "SQL a los ejemplos de conversión de datos de C | Documentos de Microsoft"
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
- data conversions from SQL to C types [ODBC], examples
- converting data from SQL to C types [ODBC], examples
ms.assetid: 0190c76c-7f9b-42f4-be9d-cef7284840fd
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: c7dd7b514ce4788a035e6f230f3d0a87a94440f2
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="sql-to-c-data-conversion-examples"></a>SQL a los ejemplos de conversión de datos de C
Los ejemplos que se muestra en la tabla siguiente muestra cómo el controlador convierte los datos de SQL a los datos de C:  
  
|Tipo SQL<br /><br /> identificador|SQL data<br /><br /> value|Tipo de C<br /><br /> identificador|Búfer<br /><br /> length|**TargetValuePtr*|SQLSTATE|  
|-----------------------------|------------------------|---------------------------|-----------------------|------------------------|--------------|  
|SQL_CHAR|abcdef|SQL_C_CHAR|7|abcdef\0 [a]|n/d|  
|SQL_CHAR|abcdef|SQL_C_CHAR|6|abcde\0 [a]|01004|  
|SQL_DECIMAL|1234.56|SQL_C_CHAR|8|1234.56\0 [a]|n/d|  
|SQL_DECIMAL|1234.56|SQL_C_CHAR|5|1234\0 [a]|01004|  
|SQL_DECIMAL|1234.56|SQL_C_CHAR|4|----|22003|  
|SQL_DECIMAL|1234.56|SQL_C_FLOAT|no se tiene en cuenta|1234.56|n/d|  
|SQL_DECIMAL|1234.56|SQL_C_SSHORT|no se tiene en cuenta|1234|01S07|  
|SQL_DECIMAL|1234.56|SQL_C_STINYINT|no se tiene en cuenta|----|22003|  
SQL_DOUBLE|1.2345678|SQL_C_DOUBLE|no se tiene en cuenta|1.2345678|n/d|  
|SQL_DOUBLE|1.2345678|SQL_C_FLOAT|no se tiene en cuenta|1.234567|n/d|  
|SQL_DOUBLE|1.2345678|SQL_C_STINYINT|no se tiene en cuenta|1|n/d|  
|SQL_TYPE_DATE|1992-12-31|SQL_C_CHAR|11|1992-12-31\0 [a]|n/d|  
|SQL_TYPE_DATE|1992-12-31|SQL_C_CHAR|10|-----|22003|  
|SQL_TYPE_DATE|1992-12-31|SQL_C_TIMESTAMP|no se tiene en cuenta|1992,12,31, 0,0,0,0 [b]|n/d|  
|SQL_TYPE_TIMESTAMP|1992-12-31 23:45:55.12|SQL_C_CHAR|23|1992-12-31 23:45:55.12\0 [a]|n/d|  
SQL_TYPE_TIMESTAMP|1992-12-31 23:45:55.12|SQL_C_CHAR|22|1992-12-31 23:45:55.1\0 [a]|01004|  
|SQL_TYPE_TIMESTAMP|1992-12-31 23:45:55.12|SQL_C_CHAR|18|----|22003|  
  
 [a] "\0" representa un byte de finalización en null. El controlador siempre termina en null datos SQL_C_CHAR.  
  
 [b] los números de esta lista son los números almacenados en los campos de la estructura TIMESTAMP_STRUCT.
