---
title: 'SQL a intervalos de tiempo de día C: | Documentos de Microsoft'
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
ms.topic: article
helpviewer_keywords:
- converting data from SQL to C types [ODBC], day-time intervals
- day-time intervals [ODBC]
- data conversions from SQL to C types [ODBC], day-time intervals
- intervals [ODBC], converting
ms.assetid: 8ea84d69-2292-4128-89a0-f184f68abb98
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 9df3ee4fdd01d5296e547bb445f3e4e47cee3561
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="sql-to-c-day-time-intervals"></a>SQL a intervalos de tiempo de día C:
Los identificadores para los tipos de datos SQL de ODBC de intervalo de tiempo del día son:  
  
 SQL_INTERVAL_DAY  
  
 SQL_INTERVAL_DAY_TO_MINUTE  
  
 SQL_INTERVAL_HOUR  
  
 SQL_INTERVAL_DAY_TO_SECOND  
  
 SQL_INTERVAL_MINUTE  
  
 SQL_INTERVAL_HOUR_TO_MINUTE  
  
 SQL_INTERVAL_SECOND  
  
 SQL_INTERVAL_HOUR_TO_SECOND  
  
 SQL_INTERVAL_DAY_TO_HOUR  
  
 SQL_INTERVAL_MINUTE_TO_SECOND  
  
 La siguiente tabla muestra los tipos de datos a la que se puede convertir la hora del día intervalo de datos de SQL de la C de ODBC. Para obtener una explicación de las columnas y los términos de la tabla, vea [convertir datos de SQL a tipos de datos C](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md).  
  
|Identificador de tipo de C|Prueba|**TargetValuePtr*|**StrLen_or_IndPtr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|Todos los tipos de intervalo de hora diurna C|No se trunca la parte campos final<br /><br /> Parte de campos finales truncado<br /><br /> Precisión de destino del principio no es lo suficientemente grande como para contener los datos de origen|data<br /><br /> Datos truncados<br /><br /> No definido|Longitud de datos<br /><br /> Longitud de datos<br /><br /> No definido|n/d<br /><br /> 01S07<br /><br /> 22015|  
|SQL_C_STINYINT [b] SQL_C_UTINYINT [b] SQL_C_USHORT [b] SQL_C_SHORT [b] SQL_C_SLONG [b] SQL_C_ULONG [b] SQL_C_NUMERIC [b] SQL_C_BIGINT [b]|Precisión de intervalo era de un solo campo y los datos se convierten sin truncamiento<br /><br /> Precisión de intervalo era un único campo y truncado fraccionario<br /><br /> Precisión de intervalo era de un único campo y todo truncado<br /><br /> Precisión de intervalo no era un campo único|data<br /><br /> Datos truncados<br /><br /> Datos truncados<br /><br /> No definido|Tamaño del tipo de datos C<br /><br /> Longitud de datos<br /><br /> Longitud de datos<br /><br /> Tamaño del tipo de datos C|n/d<br /><br /> 01S07<br /><br /> 22003<br /><br /> 07006|  
|SQL_C_BINARY|Longitud de bytes de datos < = *BufferLength*<br /><br /> Longitud de bytes de datos > *BufferLength*|data<br /><br /> No definido|Longitud de datos<br /><br /> No definido|n/d<br /><br /> 22003|  
|SQL_C_CHAR|Longitud de bytes de caracteres < *BufferLength*<br /><br /> Número de dígitos enteros (en lugar de fracciones) < *BufferLength*<br /><br /> Número de dígitos enteros (en lugar de fracciones) > = *BufferLength*|data<br /><br /> Datos truncados<br /><br /> No definido|Tamaño del tipo de datos C<br /><br /> Tamaño del tipo de datos C<br /><br /> No definido|n/d<br /><br /> 01004<br /><br /> 22003|  
_C_WCHAR|Longitud de caracteres < *BufferLength*<br /><br /> Número de dígitos enteros (en lugar de fracciones) < *BufferLength*<br /><br /> Número de dígitos enteros (en lugar de fracciones) > = *BufferLength*|data<br /><br /> Datos truncados<br /><br /> No definido|Tamaño del tipo de datos C<br /><br /> Tamaño del tipo de datos C<br /><br /> No definido|n/d<br /><br /> 01004<br /><br /> 22003|  
  
 [a] intervalo de hora del día de un tipo de SQL se puede convertir a cualquier tipo de intervalo de hora diurna C.  
  
 [b] si la precisión de intervalo es un campo único (uno de día, hora, minuto y segundo), se puede convertir el tipo SQL de intervalo para cualquier valor numérico exacto (SQL_C_STINYINT, SQL_C_UTINYINT, SQL_C_USHORT, SQL_C_SHORT, SQL_C_SLONG, SQL_C_ULONG o SQL_C_NUMERIC).  
  
 La conversión de valor predeterminado de un intervalo de tipo SQL es el tipo de datos de intervalo de C correspondiente. La aplicación, a continuación, enlaza la columna o parámetro (o establece el campo SQL_DESC_DATA_PTR en el registro adecuado de la descartar) para que apunte a la estructura SQL_INTERVAL_STRUCT inicializada (o se pasa un puntero a la estructura de SQL_ INTERVAL_STRUCT como el *TargetValuePtr* argumento en una llamada a **SQLGetData**).  
  
 En el ejemplo siguiente se muestra cómo transferir los datos de una columna de tipo SQL_INTERVAL_DAY_TO_MINUTE en la estructura SQL_INTERVAL_STRUCT, que vuelve a estar como un intervalo DAY_TO_HOUR.  
  
```  
SQL_INTERVAL_STRUCT is;  
SQLINTEGER    cbValue;  
SQLUINTEGER   days, hours;  
  
// Execute a select statement; "interval_column" is a column  
// whose data type is SQL_INTERVAL_DAY_TO_MINUTE.  
SQLExecDirect(hstmt, "SELECT interval_column FROM table", SQL_NTS);  
  
// Bind  
SQLBindCol(hstmt, 1, SQL_C_INTERVAL_DAY_TO_MINUTE, &is, sizeof(SQL_INTERVAL_STRUCT), &cbValue);  
  
// Fetch  
SQLFetch(hstmt);  
  
// Process data  
days = is.intval.day_second.day;  
hours = is.intval.day_second.hour;  
```
