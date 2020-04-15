---
title: Información ODBC de 64 bits Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ed9851ce-44ee-4c8e-b626-1d0b52da30fe
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b9cb8e3fc42d0ad71ac83f1432c165f243f39012
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298305"
---
# <a name="odbc-64-bit-information"></a>Información sobre ODBC de 64 bits
A partir de Windows Server 2003, los sistemas operativos de Microsoft han admitido las bibliotecas ODBC de 64 bits. Los encabezados ODBC y las bibliotecas que se incluyen por primera vez con el SDK de MDAC 2.7 contienen cambios para permitir a los programadores escribir código fácilmente para las nuevas plataformas de 64 bits. Al asegurarse de que el código usa los tipos definidos por ODBC que se enumeran a continuación, puede compilar el mismo código fuente para plataformas de 64 bits y 32 bits basadas en las macros **_WIN64** o **WIN32.**  
  
 Hay varios puntos a tener en cuenta al programar para un procesador de 64 bits:  
  
-   Aunque el tamaño de un puntero ha cambiado de 4 bytes a 8 bytes, los enteros y los longs siguen siendo valores de 4 bytes. Los tipos **INT64** y **UINT64** se han definido para enteros de 8 bytes. Los nuevos tipos ODBC **SQLLEN** y **SQLULEN** se definen en el archivo de encabezado ODBC como **INT64** y **UINT64** cuando se ha definido **_WIN64.**  
  
-   Varias funciones de ODBC se declaran como tomar un parámetro de puntero. En ODBC de 32 bits, los parámetros definidos como punteros se usaban con frecuencia para pasar un valor entero o un puntero a un búfer en función del contexto de la llamada. Esto era, por supuesto, posible debido al hecho de que los punteros y enteros tenían el mismo tamaño. En Windows de 64 bits, este no es el caso.  
  
-   Algunas funciones ODBC que se definieron anteriormente con parámetros **SQLINTEGER** y **SQLUINTEGER** se han cambiado cuando procede para utilizar las nuevas definiciones de tipo **SQLLEN** y **SQLULEN.** Estos cambios se enumeran en la siguiente sección, Cambios de declaración de función.  
  
-   Algunos de los campos descriptores que se pueden establecer a través de las diversas funciones **SQLSet** y **SQLGet** se han cambiado para dar cabida a valores de 64 bits, mientras que otros siguen siendo valores de 32 bits. Asegúrese de utilizar la variable de tamaño adecuada al establecer y recuperar estos campos. Los detalles de los campos descriptores que han cambiado se enumeran en Cambios de declaración de función.  
  
## <a name="function-declaration-changes"></a>Cambios en la declaración de funciones  
 Las siguientes firmas de función han cambiado para la programación de 64 bits. Los elementos en negrita son los parámetros específicos que son diferentes.  
  
```cpp
SQLBindCol (SQLHSTMT StatementHandle, SQLUSMALLINT ColumnNumber,  
   SQLSMALLINT TargetType, SQLPOINTER TargetValuePtr, SQLLEN BufferLength,   SQLLEN * StrLen_or_Ind);  
  
SQLBindParam (SQLHSTMT StatementHandle, SQLUSMALLINT ParameterNumber,  
   SQLSMALLINT ValueType, SQLSMALLINT ParameterType,   
   SQLULEN ColumnSize, SQLSMALLINT DecimalDigits,   
   SQLPOINTER ParameterValuePtr, SQLLEN *StrLen_or_Ind);  
  
SQLBindParameter (SQLHSTMT StatementHandle, SQLUSMALLINT ParameterNumber,   
   SQLSMALLINT InputOutputType, SQLSMALLINT ValueType,   
   SQLSMALLINT ParameterType, SQLULEN ColumnSize, SQLSMALLINT DecimalDigits,   
   SQLPOINTER ParameterValuePtr, SQLLEN BufferLength, SQLLEN *StrLen_or_IndPtr);  
  
SQLColAttribute (SQLHSTMT StatementHandle, SQLUSMALLINT ColumnNumber,  
    SQLUSMALLINT FieldIdentifier, SQLPOINTER CharacterAttributePtr,   
   SQLSMALLINT BufferLength, SQLSMALLINT * StringLengthPtr,   
   SQLLEN* NumericAttributePtr)  
  
SQLColAttributes (SQLHSTMT hstmt, SQLUSMALLINT icol,   
   SQLUSMALLINT fDescType, SQLPOINTER rgbDesc,   
   SQLSMALLINT cbDescMax, SQLSMALLINT *pcbDesc, SQLLEN * pfDesc);  
  
SQLDescribeCol (SQLHSTMT StatementHandle, SQLUSMALLINT ColumnNumber,   
   SQLCHAR *ColumnName, SQLSMALLINT BufferLength,   
   SQLSMALLINT *NameLengthPtr, SQLSMALLINT *DataTypePtr, SQLULEN *ColumnSizePtr,   
   SQLSMALLINT *DecimalDigitsPtr, SQLSMALLINT *NullablePtr);  
  
SQLDescribeParam (SQLHSTMT StatementHandle, SQLUSMALLINT ParameterNumber,   
   SQLSMALLINT *DataTypePtr, SQLULEN *ParameterSizePtr, SQLSMALLINT *DecimalDigitsPtr,   
   SQLSMALLINT *NullablePtr);  
  
SQLExtendedFetch(SQLHSTMT StatementHandle, SQLUSMALLINT FetchOrientation, SQLLEN FetchOffset,   
   SQLULEN * RowCountPtr, SQLUSMALLINT * RowStatusArray);  
  
SQLFetchScroll (SQLHSTMT StatementHandle, SQLSMALLINT FetchOrientation,   
   SQLLEN FetchOffset);  
  
SQLGetData (SQLHSTMT StatementHandle, SQLUSMALLINT ColumnNumber,   
   SQLSMALLINT TargetType, SQLPOINTER TargetValuePtr, SQLLEN BufferLength,    SQLLEN *StrLen_or_Ind);  
  
SQLGetDescRec (SQLHDESC DescriptorHandle, SQLSMALLINT RecNumber,   
   SQLCHAR *Name, SQLSMALLINT BufferLength,   
   SQLSMALLINT *StringLengthPtr, SQLSMALLINT *TypePtr,   
   SQLSMALLINT *SubTypePtr, SQLLEN *LengthPtr,   
   SQLSMALLINT *PrecisionPtr, SQLSMALLINT *ScalePtr,   
   SQLSMALLINT *NullablePtr);  
  
SQLParamOptions(SQLHSTMT hstmt, SQLULEN crow, SQLULEN * pirow);  
  
SQLPutData (SQLHSTMT StatementHandle, SQLPOINTER DataPtr,   
   SQLLEN StrLen_or_Ind);  
  
SQLRowCount (SQLHSTMT StatementHandle, SQLLEN* RowCountPtr);  
  
SQLSetConnectOption(SQLHDBC ConnectHandle, SQLUSMALLINT Option,   
   SQLULEN Value);  
  
SQLSetPos (SQLHSTMT StatementHandle, SQLSETPOSIROW RowNumber, SQLUSMALLINT Operation,  
   SQLUSMALLINT LockType);  
  
SQLSetParam (SQLHSTMT StatementHandle, SQLUSMALLINT ParameterNumber,   
   SQLSMALLINT ValueType, SQLSMALLINT ParameterType,   
   SQLULEN LengthPrecision, SQLSMALLINT ParameterScale,   
   SQLPOINTER ParameterValue, SQLLEN *StrLen_or_Ind);  
  
SQLSetDescRec (SQLHDESC DescriptorHandle, SQLSMALLINT RecNumber,   
   SQLSMALLINT Type, SQLSMALLINT SubType, SQLLEN Length,   
   SQLSMALLINT Precision, SQLSMALLINT Scale, SQLPOINTER DataPtr,   
   SQLLEN *StringLengthPtr, SQLLEN *IndicatorPtr);  
  
SQLSetScrollOptions (SQLHSTMT hstmt, SQLUSMALLINT fConcurrency,   
   SQLLEN crowKeyset, SQLUSMALLINT crowRowset);  
  
SQLSetStmtOption (SQLHSTMT StatementHandle, SQLUSMALLINT Option,   
   SQLULEN Value);  
```  
  
## <a name="changes-in-sql-data-types"></a>Cambios en los tipos de datos SQL  
 Los siguientes cuatro tipos SQL todavía se admiten solo en 32 bits; no están definidos para compiladores de 64 bits. Estos tipos ya no se utilizan para ningún parámetro en MDAC 2.7; el uso de estos tipos provocará errores del compilador en plataformas de 64 bits.  
  
```cpp
#ifdef WIN32   
typedef SQLULEN SQLROWCOUNT;   
typedef SQLULEN SQLROWSETSIZE;   
typedef SQLULEN SQLTRANSID;   
typedef SQLLEN SQLROWOFFSET;   
#endif  
```  
  
 La definición de SQLSETPOSIROW ha cambiado para los compiladores de 32 y 64 bits:  
  
```cpp
#ifdef _WIN64   
typedef UINT64 SQLSETPOSIROW;   
#else   
#define SQLSETPOSIROW SQLUSMALLINT   
#endif  
```  
  
 Las definiciones de SQLLEN y SQLULEN han cambiado para los compiladores de 64 bits:  
  
```cpp
#ifdef _WIN64   
typedef INT64 SQLLEN;   
typedef UINT64 SQLULEN;   
#else   
#define SQLLEN SQLINTEGER   
#define SQLULEN SQLUINTEGER   
#endif  
```  
  
 Aunque SQL_C_BOOKMARK está en desuso en ODBC 3.0, para los compiladores de 64 bits en clientes 2.0, este valor ha cambiado:  
  
```cpp
#ifdef _WIN64   
#define SQL_C_BOOKMARK SQL_C_UBIGINT   
#else   
#define SQL_C_BOOKMARK SQL_C_ULONG   
#endif  
```  
  
 El tipo BOOKMARK se define de forma diferente en los encabezados más recientes:  
  
```cpp
typedef SQLULEN BOOKMARK;  
```  
  
## <a name="values-returned-from-odbc-api-calls-through-pointers"></a>Valores devueltos desde llamadas a la API ODBC a través de punteros  
 Las siguientes llamadas a funciones ODBC toman como parámetro de entrada un puntero a un búfer en el que se devuelven datos desde el controlador. El contexto y el significado de los datos devueltos viene determinado por otros parámetros de entrada para las funciones. En algunos casos, estos métodos ahora pueden devolver valores de 64 bits (entero de 8 bytes) en lugar de los valores enteros típicos de 32 bits (4 bytes). Estos casos son los siguientes:  
  
 **SQLColAttribute**  
  
 Cuando el parámetro *FieldIdentifier* tiene uno de los siguientes valores, se devuelve un valor de 64 bits en **NumericAttribute*:  
  
 SQL_DESC_AUTO_UNIQUE_VALUE  
  
 SQL_DESC_CASE_SENSITIVE  
  
 SQL_DESC_CONCISE_TYPE  
  
 SQL_DESC_COUNT  
  
 SQL_DESC_DISPLAY_SIZE  
  
 SQL_DESC_FIXED_PREC_SCALE  
  
 SQL_DESC_LENGTH  
  
 SQL_DESC_NULLABLE  
  
 SQL_DESC_NUM_PREC_RADIX  
  
 SQL_DESC_OCTET_LENGTH  
  
 SQL_DESC_PRECISION  
  
 SQL_DESC_SCALE  
  
 SQL_DESC_SEARCHABLE  
  
 SQL_DESC_TYPE  
  
 SQL_DESC_UNNAMED  
  
 SQL_DESC_UNSIGNED  
  
 SQL_DESC_UPDATABLE  
  
 **SQLColAttributes**  
  
 Cuando el parámetro *fDescType* tiene uno de los siguientes valores, se devuelve un valor de 64 bits en **pfDesc*:  
  
 SQL_COLUMN_COUNT  
  
 SQL_COLUMN_DISPLAY_SIZE  
  
 SQL_COLUMN_LENGTH  
  
 SQL_DESC_AUTO_UNIQUE_VALUE  
  
 SQL_DESC_CASE_SENSITIVE  
  
 SQL_DESC_CONCISE_TYPE  
  
 SQL_DESC_FIXED_PREC_SCALE  
  
 SQL_DESC_SEARCHABLE  
  
 SQL_DESC_UNSIGNED  
  
 SQL_DESC_UPDATABLE  
  
 **SQLGetConnectAttr**  
  
 Cuando el parámetro *Attribute* tiene uno de los siguientes valores, se devuelve un valor de 64 bits en *Value*:  
  
 SQL_ATTR_ASYNC_ENABLE  
  
 SQL_ATTR_ENLIST_IN_DTC  
  
 SQL_ATTR_ODBC_CURSORS  
  
 SQL_ATTR_QUIET_MODE  
  
 **SQLGetConnectOption**  
  
 Cuando el parámetro *Attribute* tiene uno de los siguientes valores, se devuelve un valor de 64 bits en *Value*:  
  
 SQL_ATTR_QUIET_MODE  
  
 **SQLGetDescField**  
  
 Cuando el parámetro *FieldIdentifier* tiene uno de los siguientes valores, se devuelve un valor de 64 bits en **ValuePtr:*  
  
 SQL_DESC_ARRAY_SIZE  
  
 SQL_DESC_ARRAY_STATUS_PTR  
  
 SQL_DESC_BIND_OFFSET_PTR  
  
 SQL_DESC_DATA_PTR  
  
 SQL_DESC_DISPLAY_SIZE  
  
 SQL_DESC_INDICATOR_PTR  
  
 SQL_DESC_LENGTH  
  
 SQL_DESC_OCTET_LENGTH  
  
 SQL_DESC_OCTET_LENGTH_PTR  
  
 SQL_DESC_ROWS_PROCESSED_PTR  
  
 **SQLGetDiagField**  
  
 Cuando el parámetro *DiagIdentifier* tiene uno de los siguientes valores, se devuelve un valor de 64 bits en **DiagInfoPtr:*  
  
 SQL_DIAG_CURSOR_ROW_COUNT  
  
 SQL_DIAG_ROW_COUNT  
  
 SQL_DIAG_ROW_NUMBER  
  
 **SQLGetInfo**  
  
 Cuando el parámetro *InfoType* tiene uno de los siguientes valores, se devuelve un valor de 64 bits en **InfoValuePtr*:  
  
 SQL_DRIVER_HDBC  
  
 SQL_DRIVER_HENV  
  
 SQL_DRIVER_HLIB  
  
 Cuando *InfoType* tiene cualquiera de los 2 valores siguientes **InfoValuePtr* es 64 bits tanto en la entrada como en la salida:  
  
 SQL_DRIVER_HDESC  
  
 SQL_DRIVER_HSTMT  
  
 **SQLGetStmtAttr**  
  
 Cuando el parámetro *Attribute* tiene uno de los siguientes valores, se devuelve un valor de 64 bits en **ValuePtr:*  
  
 SQL_ATTR_APP_PARAM_DESC  
  
 SQL_ATTR_APP_ROW_DESC  
  
 SQL_ATTR_ASYNC_ENABLE  
  
 SQL_ATTR_CONCURRENCY  
  
 SQL_ATTR_CURSOR_SCROLLABLE  
  
 SQL_ATTR_CURSOR_SENSITIVITY  
  
 SQL_ATTR_CURSOR_TYPE  
  
 SQL_ATTR_ENABLE_AUTO_IPD  
  
 SQL_ATTR_FETCH_BOOKMARK_PTR  
  
 SQL_ATTR_ROWS_FETCHED_PTR  
  
 SQL_ATTR_IMP_PARAM_DESC  
  
 SQL_ATTR_IMP_ROW_DESC  
  
 SQL_ATTR_KEYSET_SIZE  
  
 SQL_ATTR_MAX_LENGTH  
  
 SQL_ATTR_MAX_ROWS  
  
 SQL_ATTR_METADATA_ID  
  
 SQL_ATTR_NOSCAN  
  
 SQL_ATTR_PARAM_BIND_OFFSET_PTR  
  
 SQL_ATTR_PARAM_BIND_TYPE  
  
 SQL_ATTR_PARAM_OPERATION_PTR  
  
 SQL_ATTR_PARAM_STATUS_PTR  
  
 SQL_ATTR_PARAMS_PROCESSED_PTR  
  
 SQL_ATTR_PARAMSET_SIZE  
  
 SQL_ATTR_QUERY_TIMEOUT  
  
 SQL_ATTR_RETRIEVE_DATA  
  
 SQL_ATTR_ROW_ARRAY_SIZE  
  
 SQL_ATTR_ROW_BIND_OFFSET_PTR  
  
 SQL_ATTR_ROW_NUMBER  
  
 SQL_ATTR_ROW_OPERATION_PTR  
  
 SQL_ATTR_ROW_STATUS_PTR  
  
 SQL_ATTR_SIMULATE_CURSOR  
  
 SQL_ATTR_USE_BOOKMARKS  
  
 **SQLGetStmtOption**  
  
 Cuando el parámetro *Option* tiene uno de los siguientes valores, se devuelve un valor de 64 bits en **Value*:  
  
 SQL_KEYSET_SIZE  
  
 SQL_MAX_LENGTH  
  
 SQL_MAX_ROWS  
  
 SQL_ROWSET_SIZE  
  
 **SQLSetConnectAttr**  
  
 Cuando el parámetro *Attribute* tiene uno de los siguientes valores, se pasa un valor de 64 bits en *Value*:  
  
 SQL_ATTR_ASYNC_ENABLE  
  
 SQL_ATTR_ENLIST_IN_DTC  
  
 SQL_ATTR_ODBC_CURSORS  
  
 SQL_ATTR_QUIET_MODE  
  
 **SQLSetConnectOption**  
  
 Cuando el parámetro *Attribute* tiene uno de los siguientes valores, se pasa un valor de 64 bits en *Value*:  
  
 SQL_ATTR_QUIET_MODE  
  
 **SQLSetDescField**  
  
 Cuando el parámetro *FieldIdentifier* tiene uno de los siguientes valores, se pasa un valor de 64 bits en *ValuePtr:*  
  
 SQL_DESC_ARRAY_SIZE  
  
 SQL_DESC_ARRAY_STATUS_PTR  
  
 SQL_DESC_BIND_OFFSET_PTR  
  
 SQL_DESC_DATA_PTR  
  
 SQL_DESC_DISPLAY_SIZE  
  
 SQL_DESC_INDICATOR_PTR  
  
 SQL_DESC_LENGTH  
  
 SQL_DESC_OCTET_LENGTH  
  
 SQL_DESC_OCTET_LENGTH_PTR  
  
 SQL_DESC_ROWS_PROCESSED_PTR  
  
 **SQLSetStmtAttr**  
  
 Cuando el parámetro *Attribute* tiene uno de los siguientes valores, se pasa un valor de 64 bits en *ValuePtr:*  
  
 SQL_ATTR_APP_PARAM_DESC  
  
 SQL_ATTR_APP_ROW_DESC  
  
 SQL_ATTR_ASYNC_ENABLE  
  
 SQL_ATTR_CONCURRENCY  
  
 SQL_ATTR_CURSOR_SCROLLABLE  
  
 SQL_ATTR_CURSOR_SENSITIVITY  
  
 SQL_ATTR_CURSOR_TYPE  
  
 SQL_ATTR_ENABLE_AUTO_IPD  
  
 SQL_ATTR_FETCH_BOOKMARK_PTR  
  
 SQL_ATTR_IMP_PARAM_DESC  
  
 SQL_ATTR_IMP_ROW_DESC  
  
 SQL_ATTR_KEYSET_SIZE  
  
 SQL_ATTR_MAX_LENGTH  
  
 SQL_ATTR_MAX_ROWS  
  
 SQL_ATTR_METADATA_ID  
  
 SQL_ATTR_NOSCAN  
  
 SQL_ATTR_PARAM_BIND_OFFSET_PTR  
  
 SQL_ATTR_PARAM_BIND_TYPE  
  
 SQL_ATTR_PARAM_OPERATION_PTR  
  
 SQL_ATTR_PARAM_STATUS_PTR  
  
 SQL_ATTR_PARAMS_PROCESSED_PTR  
  
 SQL_ATTR_PARAMSET_SIZE  
  
 SQL_ATTR_QUERY_TIMEOUT  
  
 SQL_ATTR_RETRIEVE_DATA  
  
 SQL_ATTR_ROW_ARRAY_SIZE  
  
 SQL_ATTR_ROW_BIND_OFFSET_PTR  
  
 SQL_ATTR_ROW_NUMBER  
  
 SQL_ATTR_ROW_OPERATION_PTR  
  
 SQL_ATTR_ROW_STATUS_PTR  
  
 SQL_ATTR_ROWS_FETCHED_PTR  
  
 SQL_ATTR_SIMULATE_CURSOR  
  
 SQL_ATTR_USE_BOOKMARKS  
  
 **SQLSetStmtOption**  
  
 Cuando el parámetro *Option* tiene uno de los siguientes valores, se pasa un valor de 64 bits en *Value*:  
  
 SQL_KEYSET_SIZE  
  
 SQL_MAX_LENGTH  
  
 SQL_MAX_ROWS  
  
 SQL_ROWSET_SIZE  
  
## <a name="see-also"></a>Consulte también  
 [Introducción a ODBC](../../odbc/reference/introduction-to-odbc.md)
