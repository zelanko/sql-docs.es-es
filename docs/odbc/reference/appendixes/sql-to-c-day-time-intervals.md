---
title: 'SQL a C: Intervalos de tiempo del día | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- converting data from SQL to C types [ODBC], day-time intervals
- day-time intervals [ODBC]
- data conversions from SQL to C types [ODBC], day-time intervals
- intervals [ODBC], converting
ms.assetid: 8ea84d69-2292-4128-89a0-f184f68abb98
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ee08f42a4ccd7eb51f45e1654f20e264f80c49d2
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63270432"
---
# <a name="sql-to-c-day-time-intervals"></a>SQL a C: Intervalos de día y hora

Los identificadores de los tipos de datos SQL de ODBC de intervalo de día y hora son los siguientes:

- SQL_INTERVAL_DAY
- SQL_INTERVAL_DAY_TO_MINUTE
- SQL_INTERVAL_HOUR
- SQL_INTERVAL_DAY_TO_SECOND
- SQL_INTERVAL_MINUTE
- SQL_INTERVAL_HOUR_TO_MINUTE
- SQL_INTERVAL_SECOND
- SQL_INTERVAL_HOUR_TO_SECOND
- SQL_INTERVAL_DAY_TO_HOUR
- SQL_INTERVAL_MINUTE_TO_SECOND

La siguiente tabla muestra los tipos de datos al que se puede convertir el intervalo de día y hora de datos de SQL de la C de ODBC. Para obtener una explicación de las columnas y los términos de la tabla, vea [convertir datos de SQL a tipos de datos C](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md).

|Identificador de tipo de C|Prueba|**TargetValuePtr*|**StrLen_or_IndPtr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|Todos los tipos de intervalo de C de día y hora|No se trunca la parte de los campos final<br /><br /> Parte de los campos finales truncado<br /><br /> La precisión de destino inicial no es lo suficientemente grande como para contener los datos de origen|Datos<br /><br /> Datos truncados<br /><br /> No definido|Longitud de datos<br /><br /> Longitud de datos<br /><br /> No definido|n/d<br /><br /> 01S07<br /><br /> 22015|  
|SQL_C_STINYINT[b] SQL_C_UTINYINT[b] SQL_C_USHORT[b] SQL_C_SHORT[b] SQL_C_SLONG[b] SQL_C_ULONG[b] SQL_C_NUMERIC[b] SQL_C_BIGINT[b]|Precisión de intervalo era de un solo campo y los datos se convierten sin truncamiento<br /><br /> Precisión de intervalo era un solo campo y trunca fraccionario<br /><br /> Precisión de intervalo era de un solo campo y totalmente truncado<br /><br /> Precisión de intervalo no era un solo campo|Datos<br /><br /> Datos truncados<br /><br /> Datos truncados<br /><br /> No definido|Tamaño del tipo de datos C<br /><br /> Longitud de datos<br /><br /> Longitud de datos<br /><br /> Tamaño del tipo de datos C|n/d<br /><br /> 01S07<br /><br /> 22003<br /><br /> 07006|  
|SQL_C_BINARY|Longitud de bytes de datos < = *BufferLength*<br /><br /> Longitud de bytes de datos > *BufferLength*|Datos<br /><br /> No definido|Longitud de datos<br /><br /> No definido|n/d<br /><br /> 22003|  
|SQL_C_CHAR|Longitud de bytes de caracteres < *BufferLength*<br /><br /> Número de dígitos de entero (en contraposición a fraccionarios) < *BufferLength*<br /><br /> Número de dígitos de entero (en contraposición a fraccionarios) > = *BufferLength*|Datos<br /><br /> Datos truncados<br /><br /> No definido|Tamaño del tipo de datos C<br /><br /> Tamaño del tipo de datos C<br /><br /> No definido|n/d<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_WCHAR|Longitud de caracteres < *BufferLength*<br /><br /> Número de dígitos de entero (en contraposición a fraccionarios) < *BufferLength*<br /><br /> Número de dígitos de entero (en contraposición a fraccionarios) > = *BufferLength*|Datos<br /><br /> Datos truncados<br /><br /> No definido|Tamaño del tipo de datos C<br /><br /> Tamaño del tipo de datos C<br /><br /> No definido|n/d<br /><br /> 01004<br /><br /> 22003|  
  
 [a] intervalo de hora del día de un tipo SQL puede convertirse a cualquier tipo de intervalo de día y hora C.  
  
 [b] si la precisión de intervalo es un único campo (uno de día, hora, minuto o segundo), se puede convertir el intervalo de tipo SQL a cualquier valor numérico exacto (SQL_C_STINYINT, SQL_C_UTINYINT, SQL_C_USHORT, SQL_C_SHORT, SQL_C_SLONG, SQL_C_ULONG o SQL_C_NUMERIC).  
  
La conversión predeterminada de un intervalo de tipo SQL es el tipo de datos de intervalo de C correspondiente. La aplicación, a continuación, enlaza la columna o parámetro (o establece el campo SQL_DESC_DATA_PTR en el registro adecuado de la descartar) para que apunte a la estructura SQL_INTERVAL_STRUCT inicializada (o se pasa un puntero a la estructura de SQL_ INTERVAL_STRUCT como el *TargetValuePtr* argumento en una llamada a **SQLGetData**).  
  
El ejemplo siguiente muestra cómo transferir datos desde una columna de tipo SQL_INTERVAL_DAY_TO_MINUTE a la estructura SQL_INTERVAL_STRUCT tal que vuelve como un intervalo DAY_TO_HOUR.  

```cpp
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
