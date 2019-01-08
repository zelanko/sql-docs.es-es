---
title: Tipos de datos de C | Microsoft Docs
ms.custom: ''
ms.date: 07/12/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], C data types
- C data types [ODBC], about C data types
- C data types [ODBC]
- C buffers [ODBC]
ms.assetid: b681d260-3dbb-47df-a616-4910d727add7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3f948b50fae0995e16024ac41d8dd891630d1dbe
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/11/2018
ms.locfileid: "53208467"
---
# <a name="c-data-types"></a>Tipos de datos C
Tipos de datos ODBC C indican el tipo de datos de los búferes de C que se utiliza para almacenar datos en la aplicación.  
  
 Todos los controladores deben admitir todos los tipos de datos C. Esto es necesario porque todos los controladores deben admitir todos los tipos de C a la que se pueden convertir los tipos SQL que admiten, y todos los controladores son compatibles con al menos un carácter de tipo SQL. Dado que el tipo de carácter SQL puede convertirse a y desde todos los tipos de C, todos los controladores deben admitir todos los tipos de C.  
  
 El tipo de datos C se especifica en el **SQLBindCol** y **SQLGetData** funciona con el *TargetType* argumento y, en el **SQLBindParameter**funcionando con el *ValueType* argumento. También puede especificarse mediante una llamada a **SQLSetDescField** para establecer el campo de un descartar o APD o mediante una llamada de SQL_DESC_CONCISE_TYPE **SQLSetDescRec** con el *tipo* argumento (y el *subtipo* argumento si es necesario) y el *DescriptorHandle* argumento establecido en el identificador de un descartar o APD.  
  
 Las siguientes tablas se enumeran los identificadores de tipo válido para los tipos de datos C. La tabla también enumera el tipo de datos ODBC C que corresponde a cada identificador y la definición de este tipo de datos.  
  
|Identificador de tipo de C|Definición de tipo C de ODBC|Tipo de C|  
|-----------------------|--------------------|------------|  
|SQL_C_CHAR|SQLCHAR *|unsigned char *|  
|SQL_C_WCHAR|SQLWCHAR *|wchar_t *|  
|SQL_C_SSHORT [j]|SQLSMALLINT|short int|  
|SQL_C_USHORT [j]|SQLUSMALLINT|int short sin signo|  
|SQL_C_SLONG [j]|SQLINTEGER|long int|  
|SQL_C_ULONG [j]|SQLUINTEGER|int long sin signo|  
|SQL_C_FLOAT|SQLREAL|FLOAT|  
|SQL_C_DOUBLE|SQLDOUBLE, SQLFLOAT|double|  
|SQL_C_BIT|SQLCHAR|char sin signo|  
|SQL_C_STINYINT [j]|SQLSCHAR|carácter con signo|  
|SQL_C_UTINYINT [j]|SQLCHAR|char sin signo|  
|SQL_C_SBIGINT|SQLBIGINT|_int64 [h]|  
|SQL_C_UBIGINT|SQLUBIGINT|__int64 sin signo [h]|  
|SQL_C_BINARY|SQLCHAR *|unsigned char *|  
|SQL_C_BOOKMARK [i]|MARCADOR|int long sin signo [d]|  
|SQL_C_VARBOOKMARK|SQLCHAR *|unsigned char *|  
|Todos los tipos de datos de intervalo de C|SQL_INTERVAL_STRUCT|Consulte la [estructura de intervalo de C](../../../odbc/reference/appendixes/c-interval-structure.md) sección más adelante en este apéndice.|  
  
 **Identificador de tipo C** SQL_C_TYPE_DATE [c]  
  
 **Definición de tipo C de ODBC** SQL_DATE_STRUCT  
  
 **Tipo de C**  
  
```  
struct tagDATE_STRUCT {  
   SQLSMALLINT year;  
   SQLUSMALLINT month;  
   SQLUSMALLINT day;    
} DATE_STRUCT;[a]  
```  
  
 **Identificador de tipo C** SQL_C_TYPE_TIME [c]  
  
 **Definición de tipo C de ODBC** SQL_TIME_STRUCT  
  
 **Tipo de C**  
  
```  
struct tagTIME_STRUCT {  
   SQLUSMALLINT hour;  
   SQLUSMALLINT minute;  
   SQLUSMALLINT second;  
} TIME_STRUCT;[a]  
```  
  
 **Identificador de tipo C** SQL_C_TYPE_TIMESTAMP [c]  
  
 **Definición de tipo C de ODBC** SQL_TIMESTAMP_STRUCT  
  
 **Tipo de C**  
  
```  
struct tagTIMESTAMP_STRUCT {  
   SQLSMALLINT year;  
   SQLUSMALLINT month;  
   SQLUSMALLINT day;  
   SQLUSMALLINT hour;  
   SQLUSMALLINT minute;  
   SQLUSMALLINT second;  
   SQLUINTEGER fraction;[b]   
} TIMESTAMP_STRUCT;[a]  
```  
  
 **Identificador de tipo C** SQL_C_NUMERIC  
  
 **Definición de tipo C de ODBC** SQL_NUMERIC_STRUCT  
  
 **Tipo de C**  
  
```  
struct tagSQL_NUMERIC_STRUCT {  
   SQLCHAR precision;  
   SQLSCHAR scale;  
   SQLCHAR sign[g];  
   SQLCHAR val[SQL_MAX_NUMERIC_LEN];[e], [f]   
} SQL_NUMERIC_STRUCT;  
```  
  
 **Identificador de tipo C** SQL_C_GUID  
  
 **Definición de tipo C de ODBC** SQLGUID  
  
 **Tipo de C**  
  
```  
struct tagSQLGUID {  
   DWORD Data1;  
   WORD Data2;  
   WORD Data3;  
   BYTE Data4[8];  
} SQLGUID;[k]  
```  
  
 [a] los valores del año, mes, día, hora, minuto y segundo campos en los tipos de datos de fecha y hora C deben ajustarse a las restricciones del calendario gregoriano. (Consulte [restricciones del calendario gregoriano](../../../odbc/reference/appendixes/constraints-of-the-gregorian-calendar.md) más adelante en este apéndice.)  
  
 [b] el valor del campo de fracción es el número de milmillonésimas de segundo y los intervalos de 0 a 999.999.999 (menos de 1 000 millones de 1). Por ejemplo, el valor del campo de fracción de medio segundo es 500,000,000 para una milésima de segundo (un milisegundo) es 1.000.000, para una millonésima de segundo (un microsegundo) es 1000 y para un milmillonésima parte de un segundo (un nanosegundo) es 1.  
  
 [c] en ODBC 2. *x*, los tipos de datos de fecha, hora y marca de tiempo de C son SQL_C_DATE, SQL_C_TIME y SQL_C_TIMESTAMP.  
  
 [d] ODBC 3 *.x* las aplicaciones deben usar SQL_C_VARBOOKMARK, no SQL_C_BOOKMARK. Cuando una aplicación ODBC 3 *.x* aplicación trabaja con un ODBC 2. *x* controlador, el 3 de ODBC *.x* Administrador de controladores se asignarán SQL_C_VARBOOKMARK a SQL_C_BOOKMARK.  
  
 [e] un número se almacena en el *val* campo de la estructura SQL_NUMERIC_STRUCT como un entero escalado, en el modo little-endian (el byte más a la izquierda está el byte menos significativo). Por ejemplo, el número 10.001 en base 10, con una escala de 4, se escala a un entero de 100010. Dado que esto es 186AA en formato hexadecimal, el valor en SQL_NUMERIC_STRUCT sería "AA 86 01 00 00... 00", con el número de bytes definido por el SQL_MAX_NUMERIC_LEN **#define**.  
  
 Para obtener más información acerca de **SQL_NUMERIC_STRUCT**, consulte [HOWTO: Recuperar datos numéricos con SQL_NUMERIC_STRUCT](retrieve-numeric-data-sql-numeric-struct-kb222831.md).  
  
 [f] los campos de precisión y escala de los datos SQL_C_NUMERIC escriba areused para la entrada de una aplicación y para la salida desde el controlador a la aplicación. Cuando el controlador escribe un valor numérico en el SQL_NUMERIC_STRUCT, usará su propia predeterminado específico del controlador como el valor de la *precisión* campo y usará el valor del campo SQL_DESC_SCALE del descriptor de aplicación () cuyo valor predeterminado es 0) para el *escala* campo. Una aplicación puede proporcionar sus propios valores de precisión y escala estableciendo los campos SQL_DESC_PRECISION y SQL_DESC_SCALE del descriptor de aplicación.  
  
 [g] el campo de inicio de sesión es 1 si es positivo, 0 si es negativo.  
  
 [h] _int64 no se puede proporcionar algunos compiladores.  
  
 [i] _SQL_C_BOOKMARK ha quedado obsoleto en ODBC 3 *.x*.  
  
 [j] _SQL_C_SHORT, SQL_C_LONG y SQL_C_TINYINT han sido reemplazados en ODBC por tipos con signo y sin signo: SQL_C_SSHORT y SQL_C_USHORT, SQL_C_SLONG y SQL_C_ULONG y SQL_C_STINYINT y SQL_C_UTINYINT. Una aplicación ODBC 3 *.x* controlador que deban trabajar con ODBC 2. *x* aplicaciones deberían admitir SQL_C_SHORT, SQL_C_LONG y SQL_C_TINYINT, porque cuando se les llama, el Administrador de controladores pasa a través del controlador.  
  
 [k] SQL_C_GUID puede convertirse solo a SQL_CHAR o SQL_WCHAR.  
  
 Esta sección contiene el siguiente tema.  
  
-   [Estructuras de entero de 64 bits](../../../odbc/reference/appendixes/64-bit-integer-structures.md)  
  
## <a name="see-also"></a>Vea también  
 [Tipos de datos C en ODBC](../../../odbc/reference/develop-app/c-data-types-in-odbc.md)
