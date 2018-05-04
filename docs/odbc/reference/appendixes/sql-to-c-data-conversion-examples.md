---
title: SQL a los ejemplos de conversión de datos de C | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- data conversions from SQL to C types [ODBC], examples
- converting data from SQL to C types [ODBC], examples
ms.assetid: 0190c76c-7f9b-42f4-be9d-cef7284840fd
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5a2fa699cb8d57e9ec44ec133ec766b70414e00b
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
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
