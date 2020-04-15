---
title: Literales de fecha, hora y marca de tiempo ? Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d899938be4689daab50a773f189219a797794006
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81288301"
---
# <a name="date-time-and-timestamp-literals"></a>Fecha, hora y marca de tiempo literales
La secuencia de escape para los literales de fecha, hora y marca de tiempo es  
  
 **-**  _-tipo_ **'** _valor_ ' **?**  
  
 donde *literal-type* es uno de los valores enumerados en la tabla siguiente.  
  
|*tipo literal*|Significado|Formato de *valor*|  
|---------------------|-------------|-----------------------|  
|**D**|Date|*aaaa*-*mm*-*dd*|  
|**T**|Tiempo*|*hh*:*mm*:*ss*[1]|  
|**Ts**|Timestamp|*aaaa*-*mm*-*dd* *hh*:*mm*:*ss*[.* f...*] [1]|  
  
 [1] El número de dígitos a la derecha del punto decimal en un literal de intervalo de tiempo o marca de tiempo que contiene un componente de segundos depende de la precisión de segundos, como se incluye en el campo descriptor de SQL_DESC_PRECISION. (Para obtener más información, vea [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md).)  
  
 Para obtener más información acerca de las secuencias de escape de fecha, hora y marca de tiempo, vea Secuencias de escape de [fecha, hora y marca](../../../odbc/reference/appendixes/date-time-and-timestamp-escape-sequences.md) de tiempo en apéndice C: gramática SQL.  
  
 Por ejemplo, las dos instrucciones SQL siguientes actualizan la fecha de apertura del pedido de ventas 1023 en la tabla Pedidos. La primera instrucción utiliza la sintaxis de secuencia de escape. La segunda instrucción utiliza la sintaxis nativa de Oracle Rdb para la columna DATE y no es interoperable.  
  
```  
UPDATE Orders SET OpenDate={d '1995-01-15'} WHERE OrderID=1023  
UPDATE Orders SET OpenDate='15-Jan-1995' WHERE OrderID=1023  
```  
  
 La secuencia de escape de un literal de fecha, hora o marca de tiempo también se puede colocar en una variable de carácter enlazada a un parámetro de fecha, hora o marca de tiempo. Por ejemplo, el código siguiente utiliza un parámetro de fecha enlazado a una variable de carácter para actualizar la fecha de apertura del pedido de ventas 1023 en la tabla Pedidos:  
  
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
  
 Sin embargo, suele ser más eficaz enlazar el parámetro directamente a una estructura de fecha:  
  
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
  
 Para determinar si un controlador admite las secuencias de escape ODBC para literales de fecha, hora o marca de tiempo, una aplicación llama a **SQLGetTypeInfo**. Si el origen de datos admite un tipo de datos de fecha, hora o marca de tiempo, también debe admitir la secuencia de escape correspondiente.  
  
 Los orígenes de datos también pueden admitir los literales datetime definidos en la especificación ANSI SQL-92, que son diferentes de las secuencias de escape ODBC para los literales de fecha, hora o marca de tiempo. Para determinar si un origen de datos admite los literales ANSI, una aplicación llama a **SQLGetInfo** con la opción SQL_ANSI_SQL_DATETIME_LITERALS.  
  
 Para determinar si un controlador admite las secuencias de escape ODBC para literales de intervalo, una aplicación llama a **SQLGetTypeInfo**. Si el origen de datos admite un tipo de datos de intervalo de fecha y hora, también debe admitir la secuencia de escape correspondiente.  
  
 Los orígenes de datos también pueden admitir los literales datetime definidos en la especificación ANSI SQL-92, que son diferentes de las secuencias de escape ODBC para literales de intervalo de fecha y hora. Para determinar si un origen de datos admite los literales ANSI, una aplicación llama a **SQLGetInfo** con la opción SQL_ANSI_SQL_DATETIME_LITERALS.
