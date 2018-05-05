---
title: 'SQL en C: numérico | Documentos de Microsoft'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- data conversions from SQL to C types [ODBC], numeric
- numeric data type [ODBC], converting
- converting data from SQL to C types [ODBC], numeric
ms.assetid: 76f8b5d5-4bd0-4dcb-a90a-698340e0d36e
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 72714e2bf41a820bec154487d23fb0fcf0c66ac0
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="sql-to-c-numeric"></a>SQL en C: numérico
Los identificadores para los tipos de datos de ODBC SQL numéricos son:  
  
 SQL_DECIMAL  
  
 SQL_BIGINT  
  
 SQL_NUMERIC  
  
 SQL_REAL  
  
 SQL_TINYINT  
  
 SQL_FLOAT  
  
 SQL_SMALLINT  
  
 SQL_INTEGER SQL_DOUBLE  
  
 La siguiente tabla muestra los tipos de datos a la que se pueden convertir los datos SQL numéricos de C de ODBC. Para obtener una explicación de las columnas y los términos de la tabla, vea [convertir datos de SQL a tipos de datos C](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md).  
  
|Identificador de tipo de C|Prueba|**TargetValuePtr*|**StrLen_or_IndPtr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|SQL_C_CHAR|Longitud de bytes de caracteres < *BufferLength*<br /><br /> Número de dígitos enteros (en lugar de fracciones) < *BufferLength*<br /><br /> Número de dígitos enteros (en lugar de fracciones) > = *BufferLength*|data<br /><br /> Datos truncados<br /><br /> No definido|Longitud de los datos en bytes<br /><br /> Longitud de los datos en bytes<br /><br /> No definido|n/d<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_WCHAR|Longitud de caracteres < *BufferLength*<br /><br /> Número de dígitos enteros (en lugar de fracciones) < *BufferLength*<br /><br /> Número de dígitos enteros (en lugar de fracciones) > = *BufferLength*|data<br /><br /> Datos truncados<br /><br /> No definido|Longitud de datos de caracteres<br /><br /> Longitud de datos de caracteres<br /><br /> No definido|n/d<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_STINYINT<br /><br /> SQL_C_UTINYINT<br /><br /> SQL_C_TINYINT<br /><br /> SQL_C_SBIGINT<br /><br /> SQL_C_UBIGINT<br /><br /> SQL_C_SSHORT<br /><br /> SQL_C_USHORT<br /><br /> SQL_C_SHORT<br /><br /> SQL_C_SLONG<br /><br /> SQL_C_ULONG<br /><br /> SQL_C_LONG<br /><br /> SQL_C_NUMERIC|Los datos se convierten sin truncamiento [a]<br /><br /> Los datos se convierten con el truncamiento de los dígitos fraccionarios [a]<br /><br /> Conversión de datos dé como resultado la pérdida de dígitos enteros (en lugar de fracciones) [a]|data<br /><br /> Datos truncados<br /><br /> No definido|Tamaño del tipo de datos C<br /><br /> Tamaño del tipo de datos C<br /><br /> No definido|n/d<br /><br /> 01S07<br /><br /> 22003|  
_C_FLOAT<br /><br /> SQL_C_DOUBLE|Datos están dentro del intervalo del tipo de datos a la que se va a convertir el número [a]<br /><br /> Datos están fuera del intervalo del tipo de datos a la que se va a convertir el número [a]|data<br /><br /> No definido|Tamaño del tipo de datos C<br /><br /> No definido|n/d<br /><br /> 22003|  
|SQL_C_BIT|Los datos son 0 ó 1, [a]<br /><br /> Datos están mayores que 0, inferior a 2 y no es igual a 1 [a]<br /><br /> Datos están menor que 0 o mayor que o igual a 2 [a]|data<br /><br /> Datos truncados<br /><br /> No definido|1 [b]<br /><br /> 1 [b]<br /><br /> No definido|n/d<br /><br /> 01S07<br /><br /> 22003|  
|SQL_C_BINARY|Longitud de bytes de datos < = *BufferLength*<br /><br /> Longitud de bytes de datos > *BufferLength*|data<br /><br /> No definido|Longitud de datos<br /><br /> No definido|n/d<br /><br /> 22003|  
|SQL_C_INTERVAL_MONTH [c] SQL_C_INTERVAL_YEAR [c] SQL_C_INTERVAL_DAY [c] SQL_C_INTERVAL_HOUR [c] SQL_C_INTERVAL_MINUTE [c] SQL_C_INTERVAL_SECOND [c]|No se truncan los datos<br /><br /> Parte de las fracciones de segundo truncado<br /><br /> Parte entera del número truncado|data<br /><br /> Datos truncados<br /><br /> No definido|Longitud de los datos en bytes<br /><br /> Longitud de los datos en bytes<br /><br /> No definido|n/d<br /><br /> 01S07<br /><br /> 22015|  
_C_INTERVAL_YEAR_TO_MONTH SQL_C_INTERVAL_DAY_TO_HOUR SQL_C_INTERVAL_DAY_TO_MINUTE SQL_C_INTERVAL_DAY_TO_SECOND SQL_C_INTERVAL_HOUR_TO_MINUTE SQL_C_INTERVAL_HOUR_TO_SECOND|Parte entera del número truncado|No definido|No definido|22015|  
  
 [a] el valor de *BufferLength* se pasa por alto para esta conversión. El controlador se da por supuesto que el tamaño de **TargetValuePtr* es el tamaño del tipo de datos C.  
  
 [b] es el tamaño del tipo de datos C correspondiente.  
  
 [c] esta conversión solo se admite para los tipos de datos numéricos exactos (SQL_DECIMAL de ODBC, SQL_NUMERIC, SQL_TINYINT, SQL_SMALLINT, SQL_INTEGER y SQL_BIGINT). No se admite para los tipos de datos numéricos aproximados (SQL_REAL, SQL_FLOAT o SQL_DOUBLE).  
  
## <a name="sqlcnumeric-and-sqlsetdescfield"></a>SQL_C_NUMERIC y SQLSetDescField  
 El [sqlsetdescfield, función](../../../odbc/reference/syntax/sqlsetdescfield-function.md) es necesario para realizar el enlace manual con valores SQL_C_NUMERIC. (Tenga en cuenta que se ha agregado SQLSetDescField en ODBC 3.0). Para realizar un enlace manual, primero debe obtener el identificador de descriptor.  
  
```  
if (fCType == SQL_C_NUMERIC) {   
   // special processing required for NUMERIC to get right scale & precision  
   // Modify the fields in the implicit application parameter descriptor  
   SQLHDESC hdesc=NULL;  
  
   // Use SQL_ATTR_APP_ROW_DESC for calls to SQLBindCol()  
   // Use SQL_ATTR_APP_PARAM_DESC for calls to SQLBindParameter()  
   //  
   // retcode = SQLGetStmtAttr(hstmt, SQL_ATTR_APP_ROW_DESC, &hdesc, 0, NULL);  
   retcode = SQLGetStmtAttr(hstmt, SQL_ATTR_APP_PARAM_DESC, &hdesc, 0, NULL);  
   if (!ODBC_CALL_SUCCESS(retcode)) {  
      printf ("\nSQLGetStmtAttr failed");  
      i = 1;  
      sqlstate[7] = '\0';  
      while (SQLGetDiagRec(SQL_HANDLE_STMT, hstmt, i, sqlstate, &NativeError, wrkbuf, sizeof(wrkbuf), &len) != SQL_NO_DATA) {  
         printf("\niTestCase = %d Failed...Precision = %d, Scale = %d\nNativeError=%d, State=%s, \n  Message=%s",   
            iTestCase, Precision, Scale, NativeError, sqlstate, wrkbuf);  
         i++;  
      }  
      continue;  
   }  
   retcode = SQLSetDescField(hdesc, iCol, SQL_DESC_TYPE, (SQLPOINTER) SQL_C_NUMERIC, 0);  
   if (!ODBC_CALL_SUCCESS(retcode))  
      goto error;  
   retcode = SQLSetDescField(hdesc, iCol, SQL_DESC_PRECISION, (SQLPOINTER)num.precision, 0);  
   if (!ODBC_CALL_SUCCESS(retcode))  
      goto error;  
   retcode = SQLSetDescField(hdesc, iCol, SQL_DESC_SCALE, (SQLPOINTER)num.scale, 0);  
   if (!ODBC_CALL_SUCCESS(retcode))  
      goto error;  
   retcode = SQLSetDescField(hdesc, iCol, SQL_DESC_DATA_PTR, (SQLPOINTER) &(num), sizeof(num));  
```
