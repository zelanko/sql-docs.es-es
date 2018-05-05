---
title: Tipos de datos C | Documentos de Microsoft
ms.custom: ''
ms.date: 07/12/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], C data types
- C data types [ODBC], about C data types
- C data types [ODBC]
- C buffers [ODBC]
ms.assetid: b681d260-3dbb-47df-a616-4910d727add7
caps.latest.revision: 19
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 288ca6cbd5553b963131d34b8e63640518f70ef4
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="c-data-types"></a>Tipos de datos C
Tipos de datos ODBC C indican el tipo de datos de búferes de C que se usa para almacenar datos en la aplicación.  
  
 Todos los controladores deben admitir todos los tipos de datos de C. Esto es necesario porque todos los controladores deben admitir todos los tipos de C a la que se pueden convertir tipos SQL que admiten, y todos los controladores admitir al menos un carácter de tipo SQL. Dado que el tipo SQL de caracteres se pueda convertir a y desde todos los tipos de C, todos los controladores deben admitir todos los tipos de C.  
  
 El tipo de datos de C se especifica en el **SQLBindCol** y **SQLGetData** funciona con el *TargetType* argumento y en los **SQLBindParameter**funcionando con la *ValueType* argumento. También puede especificarse mediante una llamada a **SQLSetDescField** para establecer el campo SQL_DESC_CONCISE_TYPE de un descartar o APD, o mediante una llamada a **SQLSetDescRec** con el *tipo* argumento (y el *subtipo* argumento si es necesario) y la *DescriptorHandle* establecido en el identificador de un descartar o APD.  
  
 Las siguientes tablas enumeran los identificadores de tipo válido para los tipos de datos C. La tabla también muestra el tipo de datos C de ODBC que corresponde a cada identificador y la definición de este tipo de datos.  
  
|Identificador de tipo de C|Definición de tipo C de ODBC|Tipo de C|  
|-----------------------|--------------------|------------|  
|SQL_C_CHAR|SQLCHAR *|unsigned char *|  
|SQL_C_WCHAR|SQLWCHAR *|wchar_t *|  
|SQL_C_SSHORT [j]|SQLSMALLINT|short int|  
|SQL_C_USHORT [j]|SQLUSMALLINT|int corto sin signo|  
|SQL_C_SLONG [j]|SQLINTEGER|long int|  
|SQL_C_ULONG [j]|SQLUINTEGER|int long sin signo|  
|SQL_C_FLOAT|SQLREAL|float|  
|SQL_C_DOUBLE|SQLDOUBLE, SQLFLOAT|double|  
|SQL_C_BIT|SQLCHAR|char sin signo|  
|SQL_C_STINYINT [j]|SQLSCHAR|char con signo|  
|SQL_C_UTINYINT [j]|SQLCHAR|char sin signo|  
|SQL_C_SBIGINT|SQLBIGINT|_int64 [h]|  
|SQL_C_UBIGINT|SQLUBIGINT|sin signo _int64 [h]|  
|SQL_C_BINARY|SQLCHAR *|unsigned char *|  
|SQL_C_BOOKMARK [i]|MARCADOR|int long sin signo [d]|  
|SQL_C_VARBOOKMARK|SQLCHAR *|unsigned char *|  
|Todos los tipos de datos interval de C|SQL_INTERVAL_STRUCT|Consulte la [estructura de intervalo de C](../../../odbc/reference/appendixes/c-interval-structure.md) sección, más adelante en este apéndice.|  
  
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
   SQLCHAR val[SQL_MAX_NUMERIC_LEN];[e], [f]   
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
  
 [b], el valor del campo de fracción es el número de milmillonésimas de segundo y oscila entre 0 y 999999999 (1 inferior a mil millones de 1). Por ejemplo, el valor del campo de fracción de un segundo mitad es 500,000,000, para una milésima de segundo (un milisegundo) es 1.000.000, para una millonésima de segundo (un microsegundo) es 1.000 y para un millonésimas de segundo (un nanosegundo) es 1.  
  
 [c] en ODBC 2. *x*, los tipos de datos de fecha, hora y marca de tiempo de C son SQL_C_DATE, SQL_C_TIME y SQL_C_TIMESTAMP.  
  
 [d] ODBC 3 *.x* las aplicaciones deben utilizar SQL_C_VARBOOKMARK, no SQL_C_BOOKMARK. Cuando una aplicación ODBC 3 *.x* aplicación funciona con una API ODBC 2. *x* controlador ODBC 3 *.x* el Administrador de controladores se asignarán SQL_C_VARBOOKMARK a SQL_C_BOOKMARK.  
  
 [e] un número se almacena en la *val* campo de la estructura SQL_NUMERIC_STRUCT como un entero con escala, en el modo little-endian (el byte más a la izquierda que se va al byte menos significativo). Por ejemplo, el número 10.001 en base 10, con una escala de 4, se escala a un entero de 100010. Dado que es 186AA en formato hexadecimal, el valor de SQL_NUMERIC_STRUCT sería "AA 86 01 00 00... 00", con el número de bytes definido por el SQL_MAX_NUMERIC_LEN **#define**.  
  
 Para obtener más información acerca de **SQL_NUMERIC_STRUCT**, consulte [Cómo: recuperar datos numéricos con SQL_NUMERIC_STRUCT](retrieve-numeric-data-sql-numeric-struct-kb222831.md).  
  
 [f], los campos de precisión y escala de los datos SQL_C_NUMERIC tipo areused para la entrada de una aplicación y para la salida desde el controlador a la aplicación. Cuando el controlador escribe un valor numérico en el SQL_NUMERIC_STRUCT, usará su propio predeterminados específicos del controlador como el valor de la *precisión* campo y se usará el valor del campo SQL_DESC_SCALE del descriptor de la aplicación () cuyo valor predeterminado es 0) para la *escala* campo. Una aplicación puede proporcionar sus propios valores para la precisión y escala estableciendo los campos SQL_DESC_PRECISION y SQL_DESC_SCALE del descriptor de la aplicación.  
  
 [g], el campo de inicio de sesión es 1 si es positivo, 0 si es negativo.  
  
 [h] algunos compiladores no podría proporcionar _int64.  
  
 [i] _SQL_C_BOOKMARK está en desuso en ODBC 3 *.x*.  
  
 [j] _SQL_C_SHORT, SQL_C_LONG y SQL_C_TINYINT se reemplazaron en ODBC por tipos signed y unsigned: SQL_C_SSHORT y SQL_C_USHORT, SQL_C_SLONG y SQL_C_ULONG y SQL_C_STINYINT y SQL_C_UTINYINT. Una aplicación ODBC 3 *.x* controlador que debe trabajar con ODBC 2. *x* las aplicaciones deben admitir SQL_C_SHORT, SQL_C_LONG y SQL_C_TINYINT, porque cuando se les llama, el Administrador de controladores pasa a través del controlador.  
  
 [k] SQL_C_GUID se puede convertir sólo a SQL_CHAR o SQL_WCHAR.  
  
 Esta sección contiene el siguiente tema.  
  
-   [Estructuras de entero de 64 bits](../../../odbc/reference/appendixes/64-bit-integer-structures.md)  
  
## <a name="see-also"></a>Vea también  
 [Tipos de datos C en ODBC](../../../odbc/reference/develop-app/c-data-types-in-odbc.md)
