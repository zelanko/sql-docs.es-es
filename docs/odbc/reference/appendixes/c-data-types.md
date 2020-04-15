---
title: C Tipos de datos de C Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 979bfe85e1e78b55718e1f12fdcfcc7583097bb4
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81292305"
---
# <a name="c-data-types"></a>Tipos de datos C
Los tipos de datos ODBC C indican el tipo de datos de los búferes de C utilizados para almacenar datos en la aplicación.  
  
 Todos los controladores deben admitir todos los tipos de datos de C. Esto es necesario porque todos los controladores deben admitir todos los tipos de C a los que se pueden convertir los tipos SQL que admiten y todos los controladores admiten al menos un tipo SQL de caracteres. Dado que el tipo SQL de carácter se puede convertir a y desde todos los tipos de C, todos los controladores deben admitir todos los tipos de C.  
  
 El tipo de datos C se especifica en el **SQLBindCol** y **SQLGetData** funciones con el *TargetType* argumento y en el **SQLBindParameter** función con el *ValueType* argumento. También se puede especificar llamando a **SQLSetDescField** para establecer el campo SQL_DESC_CONCISE_TYPE de un ARD o APD, o llamando a **SQLSetDescRec** con el *Type* argumento (y el *SubType* argumento si es necesario) y el *DescriptorHandle* argumento establecido en el identificador de un ARD o APD.  
  
 En las tablas siguientes se enumeran los identificadores de tipo válidos para los tipos de datos de C. La tabla también enumera el tipo de datos ODBC C que corresponde a cada identificador y la definición de este tipo de datos.  
  
|Identificador de tipo C|ODBC C typedef|Tipo de C|  
|-----------------------|--------------------|------------|  
|SQL_C_CHAR|SQLCHAR *|unsigned char *|  
|SQL_C_WCHAR|SQLWCHAR *|wchar_t *|  
|SQL_C_SSHORT[j]|SQLSMALLINT|short int|  
|SQL_C_USHORT[j]|SQLUSMALLINT|unsigned short int|  
|SQL_C_SLONG[j]|SQLINTEGER|long int|  
|SQL_C_ULONG[j]|SQLUINTEGER|unsigned long int|  
|SQL_C_FLOAT|SQLREAL|FLOAT|  
|SQL_C_DOUBLE|SQLDOUBLE, SQLFLOAT|double|  
|SQL_C_BIT|SQLCHAR|unsigned char|  
|SQL_C_STINYINT[j]|SQLSCHAR|signed char|  
|SQL_C_UTINYINT[j]|SQLCHAR|unsigned char|  
|SQL_C_SBIGINT|SQLBIGINT|_int64[h]|  
|SQL_C_UBIGINT|SQLUBIGINT|_int64 sin firmar[h]|  
|SQL_C_BINARY|SQLCHAR *|unsigned char *|  
|SQL_C_BOOKMARK[i]|Marcador|unsigned long int[d]|  
|SQL_C_VARBOOKMARK|SQLCHAR *|unsigned char *|  
|Todos los tipos de datos de intervalo C|SQL_INTERVAL_STRUCT|Consulte la sección [Estructura de intervalo C,](../../../odbc/reference/appendixes/c-interval-structure.md) más adelante en este apéndice.|  
  
 **Identificador de tipo C** SQL_C_TYPE_DATE[c]  
  
 **ODBC C typedef** SQL_DATE_STRUCT  
  
 **Tipo de C**  
  
```  
struct tagDATE_STRUCT {  
   SQLSMALLINT year;  
   SQLUSMALLINT month;  
   SQLUSMALLINT day;    
} DATE_STRUCT;[a]  
```  
  
 **Identificador de tipo C** SQL_C_TYPE_TIME[c]  
  
 **ODBC C typedef** SQL_TIME_STRUCT  
  
 **Tipo de C**  
  
```  
struct tagTIME_STRUCT {  
   SQLUSMALLINT hour;  
   SQLUSMALLINT minute;  
   SQLUSMALLINT second;  
} TIME_STRUCT;[a]  
```  
  
 **Identificador de tipo C** SQL_C_TYPE_TIMESTAMP[c]  
  
 **ODBC C typedef** SQL_TIMESTAMP_STRUCT  
  
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
  
 **ODBC C typedef** SQL_NUMERIC_STRUCT  
  
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
  
 **ODBC C typedef** SQLGUID  
  
 **Tipo de C**  
  
```  
struct tagSQLGUID {  
   DWORD Data1;  
   WORD Data2;  
   WORD Data3;  
   BYTE Data4[8];  
} SQLGUID;[k]  
```  
  
 [a] Los valores de los campos year, month, day, hour, minute y second de los tipos de datos datetime C deben ajustarse a las restricciones del calendario gregoriano. (Consulte [Restricciones del calendario gregoriano](../../../odbc/reference/appendixes/constraints-of-the-gregorian-calendar.md) más adelante en este apéndice.)  
  
 [b] El valor del campo de fracción es el número de milmillonésimas de segundo y oscila entre 0 y 999.999.999 (1 menos de 1.000 millones). Por ejemplo, el valor del campo de fracción durante medio segundo es 500.000.000, para una milésima de segundo (un milisegundo) es 1.000.000, para una millonésima parte de un segundo (un microsegundo) es 1.000 y para una milmillonésima de segundo (un nanosegundo) es 1.  
  
 [c] En ODBC 2. *x*, los tipos de datos de fecha, hora y marca de tiempo de C se SQL_C_DATE, SQL_C_TIME y SQL_C_TIMESTAMP.  
  
 [d] Las aplicaciones ODBC 3 *.x* deben usar SQL_C_VARBOOKMARK, no SQL_C_BOOKMARK. Cuando una aplicación ODBC 3 *.x* funciona con un ODBC 2. *x* controlador, el Administrador de controladores ODBC 3 *.x* asignará SQL_C_VARBOOKMARK a SQL_C_BOOKMARK.  
  
 [e] Un número se almacena en el campo *val* de la estructura SQL_NUMERIC_STRUCT como un entero escalado, en modo endian pequeño (el byte más a la izquierda es el byte menos significativo). Por ejemplo, el número 10.001 base 10, con una escala de 4, se escala a un entero de 100010. Debido a que esto es 186AA en formato hexadecimal, el valor en SQL_NUMERIC_STRUCT sería "AA 86 01 00 00 ... 00", con el número de bytes definido por el SQL_MAX_NUMERIC_LEN **#define**.  
  
 Para obtener más información acerca **de SQL_NUMERIC_STRUCT**, vea [HOWTO: Recuperar datos numéricos con SQL_NUMERIC_STRUCT](retrieve-numeric-data-sql-numeric-struct-kb222831.md).  
  
 [f] Los campos de precisión y escala del tipo de datos SQL_C_NUMERIC se utilizan para la entrada de una aplicación y para la salida desde el controlador a la aplicación. Cuando el controlador escribe un valor numérico en el SQL_NUMERIC_STRUCT, usará su propio valor predeterminado específico del controlador como valor para el campo de *precisión* y usará el valor en el campo SQL_DESC_SCALE del descriptor de la aplicación (cuyo valor predeterminado es 0) para el campo *de escala.* Una aplicación puede proporcionar sus propios valores de precisión y escala estableciendo los campos SQL_DESC_PRECISION y SQL_DESC_SCALE del descriptor de la aplicación.  
  
 [g] El campo de signo es 1 si es positivo, 0 si es negativo.  
  
 [h] es posible que algunos compiladores no _int64 no las suministen.  
  
 [i] _SQL_C_BOOKMARK ha quedado en desuso en ODBC 3 *.x*.  
  
 [j] _SQL_C_SHORT, SQL_C_LONG y SQL_C_TINYINT se han reemplazado en ODBC por tipos firmados y sin signo: SQL_C_SSHORT y SQL_C_USHORT, SQL_C_SLONG y SQL_C_ULONG, y SQL_C_STINYINT y SQL_C_UTINYINT. Un controlador ODBC 3 *.x* que debe funcionar con ODBC 2. *x* las aplicaciones deben admitir SQL_C_SHORT, SQL_C_LONG y SQL_C_TINYINT, porque cuando se llaman, el Administrador de controladores las pasa al controlador.  
  
 [k] SQL_C_GUID solo se puede convertir en SQL_CHAR o SQL_WCHAR.  
  
 Esta sección contiene el tema siguiente.  
  
-   [Estructuras de entero de 64 bits](../../../odbc/reference/appendixes/64-bit-integer-structures.md)  
  
## <a name="see-also"></a>Consulte también  
 [Tipos de datos C en ODBC](../../../odbc/reference/develop-app/c-data-types-in-odbc.md)
