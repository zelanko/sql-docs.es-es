---
title: 'SQL a C: Intervalos de tiempo diurno ? Microsoft Docs'
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1318da5285ba2384dd23e4c235e698aa72c7658e
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81296475"
---
# <a name="sql-to-c-day-time-intervals"></a>SQL a C: Intervalos de día y hora

Los identificadores para los tipos de datos SQL ODBC de intervalo de tiempo diurno son los siguientes:

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

En la tabla siguiente se muestran los tipos de datos ODBC C a los que se pueden convertir los datos SQL de intervalo de tiempo diurno. Para obtener una explicación de las columnas y los términos de la tabla, vea [Convertir datos de SQL a tipos](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)de datos C .

|Identificador de tipo C|Prueba|**TargetValuePtr*|**StrLen_or_IndPtr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|Todos los tipos de intervalos C durante el día|Parte de los campos finales no truncada<br /><br /> Parte de los campos finales truncada<br /><br /> La precisión principal del objetivo no es lo suficientemente grande como para contener datos del origen|data<br /><br /> Datos truncados<br /><br /> No definido|Longitud de los datos<br /><br /> Longitud de los datos<br /><br /> No definido|N/D<br /><br /> 01S07<br /><br /> 22015|  
|SQL_C_STINYINT[b] SQL_C_UTINYINT[b] SQL_C_USHORT[b] SQL_C_SHORT[b] SQL_C_SLONG[b] SQL_C_ULONG[b] SQL_C_NUMERIC[b] SQL_C_BIGINT[b]|La precisión del intervalo era un solo campo y los datos se convirtieron sin truncamiento<br /><br /> La precisión del intervalo era un solo campo y se truncaba fraccional<br /><br /> La precisión del intervalo era un solo campo y se truncaba todo<br /><br /> La precisión del intervalo no era un solo campo|data<br /><br /> Datos truncados<br /><br /> Datos truncados<br /><br /> No definido|Tamaño del tipo de datos C<br /><br /> Longitud de los datos<br /><br /> Longitud de los datos<br /><br /> Tamaño del tipo de datos C|N/D<br /><br /> 01S07<br /><br /> 22003<br /><br /> 07006|  
|SQL_C_BINARY|Longitud de bytes de los datos <- *BufferLength*<br /><br /> Longitud de bytes de los datos > *BufferLength*|data<br /><br /> No definido|Longitud de los datos<br /><br /> No definido|N/D<br /><br /> 22003|  
|SQL_C_CHAR|Longitud de byte de caracteres < *BufferLength*<br /><br /> Número de dígitos enteros (a diferencia de los fracciones) < *BufferLength*<br /><br /> Número de dígitos enteros (a diferencia de los fracciones) >- *BufferLength*|data<br /><br /> Datos truncados<br /><br /> No definido|Tamaño del tipo de datos C<br /><br /> Tamaño del tipo de datos C<br /><br /> No definido|N/D<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_WCHAR|Longitud del carácter < *BufferLength*<br /><br /> Número de dígitos enteros (a diferencia de los fracciones) < *BufferLength*<br /><br /> Número de dígitos enteros (a diferencia de los fracciones) >- *BufferLength*|data<br /><br /> Datos truncados<br /><br /> No definido|Tamaño del tipo de datos C<br /><br /> Tamaño del tipo de datos C<br /><br /> No definido|N/D<br /><br /> 01004<br /><br /> 22003|  
  
 [a] Un tipo SQL de intervalo de tiempo diurno se puede convertir a cualquier tipo de intervalo de tiempo diurno C.  
  
 [b] Si la precisión del intervalo es un solo campo (uno de DAY, HOUR, MINUTE o SECOND), el tipo SQL de intervalo se puede convertir a cualquier número exacto (SQL_C_STINYINT, SQL_C_UTINYINT, SQL_C_USHORT, SQL_C_SHORT, SQL_C_SLONG, SQL_C_ULONG o SQL_C_NUMERIC).  
  
La conversión predeterminada de un tipo SQL de intervalo es al tipo de datos de intervalo C correspondiente. A continuación, la aplicación enlaza la columna o parámetro (o establece el campo SQL_DESC_DATA_PTR en el registro adecuado de la ARD) para que apunte a la estructura de SQL_INTERVAL_STRUCT inicializada (o pasa un puntero a la estructura INTERVAL_STRUCT SQL_ como el *TargetValuePtr* argumento en una llamada a **SQLGetData**).  
  
En el ejemplo siguiente se muestra cómo transferir datos de una columna de tipo SQL_INTERVAL_DAY_TO_MINUTE a la estructura SQL_INTERVAL_STRUCT de modo que vuelva a ser un intervalo de DAY_TO_HOUR.  

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
