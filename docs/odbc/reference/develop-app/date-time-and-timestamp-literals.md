---
title: Fecha, hora y marca de tiempo literales | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- escape sequences [ODBC], literals
ms.assetid: 2b42a52a-6353-494c-a179-3a7533cd729f
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e6191995c9d1c488fc5af056248ba39dd3eb4607
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68076982"
---
# <a name="date-time-and-timestamp-literals"></a>Fecha, hora y marca de tiempo literales
Es la secuencia de escape para literales de fecha, hora y marca de tiempo  
  
 **{** _-tipo_ **'** _valor_ **'}**  
  
 donde *literal de tipo* es uno de los valores enumerados en la tabla siguiente.  
  
|*literal-type*|Significado|Formato de *valor*|  
|---------------------|-------------|-----------------------|  
|**d**|Date|*aaaa*-*mm*-*dd*|  
|**t**|Hora *|*hh*:*mm*:*ss*[1]|  
|**ts**|Timestamp|*aaaa*-*mm*-*dd* *hh*:*mm*:*ss*[.*f...* ] [1]|  
  
 [1] el número de dígitos a la derecha del separador decimal en un intervalo de hora o marca de tiempo que contiene un componente de segundos de literal es dependiente de la precisión en segundos, la medida indicada en el campo de descriptor SQL_DESC_PRECISION. (Para obtener más información, consulte [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md).)  
  
 Para obtener más información acerca de la fecha, hora y las secuencias de escape de marca de tiempo, consulte [fecha, hora y las secuencias de Escape de marca de tiempo](../../../odbc/reference/appendixes/date-time-and-timestamp-escape-sequences.md) en el apéndice C: Gramática de SQL.  
  
 Por ejemplo, las dos siguientes instrucciones SQL actualizan la fecha de pedido de ventas 1023 en la tabla Orders abierta. La primera instrucción usa la sintaxis de la secuencia de escape. La segunda instrucción usa la sintaxis nativa de Rdb de Oracle para la columna de fecha y no es interoperable.  
  
```  
UPDATE Orders SET OpenDate={d '1995-01-15'} WHERE OrderID=1023  
UPDATE Orders SET OpenDate='15-Jan-1995' WHERE OrderID=1023  
```  
  
 La secuencia de escape para una fecha, hora o marca de tiempo literal también se puede colocar en una variable de caracteres que se enlaza a una fecha, hora o el parámetro de marca de tiempo. Por ejemplo, el código siguiente utiliza un parámetro de fecha enlazado a una variable de carácter para actualizar la fecha de pedido de ventas 1023 en la tabla Orders abierta:  
  
```  
SQLCHAR      OpenDate[56]; // The size of a date literal is 55.  
SQLINTEGER   OpenDateLenOrInd = SQL_NTS;  
  
// Bind the parameter.  
SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT, SQL_C_CHAR, SQL_TYPE_DATE, 0, 0,  
                  OpenDate, sizeof(OpenDate), &OpenDateLenOrInd);  
  
// Place the date in the OpenDate variable. In addition to the escape  
// sequence shown, it would also be possible to use either of the  
// strings "{d '1995-01-15'}" and "15-Jan-1995", although the latter  
// is data source-specific.  
strcpy_s( (char*) OpenDate, _countof(OpenDate), "{d '1995-01-15'}");  
  
// Execute the statement.  
SQLExecDirect(hstmt, "UPDATE Orders SET OpenDate=? WHERE OrderID = 1023", SQL_NTS);  
```  
  
 Sin embargo, es normalmente más eficaz para enlazar el parámetro directamente a una estructura de fecha:  
  
```  
SQL_DATE_STRUCT   OpenDate;  
SQLINTEGER        OpenDateInd = 0;  
  
// Bind the parameter.  
SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT, SQL_C_TYPE_DATE, SQL_TYPE_DATE, 0, 0,  
                  &OpenDate, 0, &OpenDateLen);  
  
// Place the date in the dsOpenDate structure.  
OpenDate.year = 1995;  
OpenDate.month = 1;  
OpenDate.day = 15;  
  
// Execute the statement.  
SQLExecDirect(hstmt, "UPDATE Employee SET OpenDate=? WHERE OrderID = 1023", SQL_NTS);  
```  
  
 Para determinar si un controlador es compatible con las secuencias de escape ODBC para fecha, hora o literales de marca de tiempo, una aplicación llama a **SQLGetTypeInfo**. Si el origen de datos admite un tipo de datos de fecha, hora o marca de tiempo, también debe admitir la secuencia de escape correspondiente.  
  
 Orígenes de datos también admiten los literales de fecha y hora definidos en la especificación ANSI SQL-92, que son diferentes de las secuencias de escape ODBC para fecha, hora o literales de marca de tiempo. Para determinar si un origen de datos admite los literales de ANSI, una aplicación llama a **SQLGetInfo** con la opción SQL_ANSI_SQL_DATETIME_LITERALS.  
  
 Para determinar si un controlador es compatible con las secuencias de escape ODBC para literales de intervalo, una aplicación llama a **SQLGetTypeInfo**. Si el origen de datos admite un tipo de datos de intervalo de fecha y hora, también debe admitir la secuencia de escape correspondiente.  
  
 Orígenes de datos también admiten los literales de fecha y hora definidos en la especificación ANSI SQL-92, que son diferentes de las secuencias de escape ODBC para los literales de intervalo de fecha y hora. Para determinar si un origen de datos admite los literales de ANSI, una aplicación llama a **SQLGetInfo** con la opción SQL_ANSI_SQL_DATETIME_LITERALS.
