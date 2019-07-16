---
title: 'SQL a C: Numérico | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data conversions from SQL to C types [ODBC], numeric
- numeric data type [ODBC], converting
- converting data from SQL to C types [ODBC], numeric
ms.assetid: 76f8b5d5-4bd0-4dcb-a90a-698340e0d36e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a23e60b161c09367cfb079cea1f7ca146b4ebee5
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68056853"
---
# <a name="sql-to-c-numeric"></a>SQL a C: Numeric

Los identificadores para los tipos de datos SQL de ODBC numéricos son los siguientes:

- SQL_DECIMAL  
- SQL_BIGINT  
- SQL_NUMERIC  
- SQL_REAL  
- SQL_TINYINT  
- SQL_FLOAT  
- SQL_SMALLINT  
- SQL_DOUBLE SQL_INTEGER  

La siguiente tabla muestra los tipos de datos a la que se pueden convertir datos numéricos de SQL de la C de ODBC. Para obtener una explicación de las columnas y los términos de la tabla, vea [convertir datos de SQL a tipos de datos C](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md).  

|Identificador de tipo de C|Prueba|**TargetValuePtr*|**StrLen_or_IndPtr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|SQL_C_CHAR|Longitud de bytes de caracteres < *BufferLength*<br /><br /> Número de dígitos de entero (en contraposición a fraccionarios) < *BufferLength*<br /><br /> Número de dígitos de entero (en contraposición a fraccionarios) > = *BufferLength*|Datos<br /><br /> Datos truncados<br /><br /> No definido|Longitud de datos en bytes<br /><br /> Longitud de datos en bytes<br /><br /> No definido|N/D<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_WCHAR|Longitud de caracteres < *BufferLength*<br /><br /> Número de dígitos de entero (en contraposición a fraccionarios) < *BufferLength*<br /><br /> Número de dígitos de entero (en contraposición a fraccionarios) > = *BufferLength*|Datos<br /><br /> Datos truncados<br /><br /> No definido|Longitud de datos de caracteres<br /><br /> Longitud de datos de caracteres<br /><br /> No definido|N/D<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_STINYINT<br /><br /> SQL_C_UTINYINT<br /><br /> SQL_C_TINYINT<br /><br /> SQL_C_SBIGINT<br /><br /> SQL_C_UBIGINT<br /><br /> SQL_C_SSHORT<br /><br /> SQL_C_USHORT<br /><br /> SQL_C_SHORT<br /><br /> SQL_C_SLONG<br /><br /> SQL_C_ULONG<br /><br /> SQL_C_LONG<br /><br /> SQL_C_NUMERIC|Convierten datos sin truncamiento [a]<br /><br /> Convierten datos con el truncamiento de dígitos fraccionarios [a]<br /><br /> Conversión de datos daría lugar a pérdida de dígitos de entero (en contraposición a fraccionarios) [a]|Datos<br /><br /> Datos truncados<br /><br /> No definido|Tamaño del tipo de datos C<br /><br /> Tamaño del tipo de datos C<br /><br /> No definido|N/D<br /><br /> 01S07<br /><br /> 22003|  
|SQL_C_FLOAT<br /><br /> SQL_C_DOUBLE|Datos están dentro del intervalo del tipo de datos a la que se va a convertir el número de [a]<br /><br /> Datos están fuera del intervalo del tipo de datos a la que se va a convertir el número de [a]|Datos<br /><br /> No definido|Tamaño del tipo de datos C<br /><br /> No definido|N/D<br /><br /> 22003|  
|SQL_C_BIT|Datos están 0 o 1, [a]<br /><br /> Datos están mayores que 0, inferior a 2 y no es igual a 1 [a]<br /><br /> Datos están menor que 0 o mayor que o igual a 2 [a]|Datos<br /><br /> Datos truncados<br /><br /> No definido|1[b]<br /><br /> 1[b]<br /><br /> No definido|N/D<br /><br /> 01S07<br /><br /> 22003|  
|SQL_C_BINARY|Longitud de bytes de datos < = *BufferLength*<br /><br /> Longitud de bytes de datos > *BufferLength*|Datos<br /><br /> No definido|Longitud de datos<br /><br /> No definido|N/D<br /><br /> 22003|  
|SQL_C_INTERVAL_MONTH[c] SQL_C_INTERVAL_YEAR[c] SQL_C_INTERVAL_DAY[c] SQL_C_INTERVAL_HOUR[c] SQL_C_INTERVAL_MINUTE[c] SQL_C_INTERVAL_SECOND[c]|No se truncan los datos<br /><br /> Parte de los segundos fraccionarios truncado<br /><br /> Parte entera del número truncado|Datos<br /><br /> Datos truncados<br /><br /> No definido|Longitud de datos en bytes<br /><br /> Longitud de datos en bytes<br /><br /> No definido|N/D<br /><br /> 01S07<br /><br /> 22015|  
|SQL_C_INTERVAL_YEAR_TO_MONTH SQL_C_INTERVAL_DAY_TO_HOUR SQL_C_INTERVAL_DAY_TO_MINUTE SQL_C_INTERVAL_DAY_TO_SECOND SQL_C_INTERVAL_HOUR_TO_MINUTE SQL_C_INTERVAL_HOUR_TO_SECOND|Parte entera del número truncado|No definido|No definido|22015|  
  
 [a] el valor de *BufferLength* se omite para esta conversión. El controlador se da por supuesto que el tamaño de **TargetValuePtr* es el tamaño del tipo de datos C.  
  
 [b] trata del tamaño del tipo de datos C correspondiente.  
  
 [c] esta conversión solo se admite para los tipos de datos numéricos exactos (SQL_DECIMAL, SQL_NUMERIC, SQL_TINYINT, SQL_SMALLINT, SQL_INTEGER y SQL_BIGINT). No se admite para los tipos de datos numéricos aproximados (SQL_REAL, SQL_FLOAT o SQL_DOUBLE).  

## <a name="sqlcnumeric-and-sqlsetdescfield"></a>SQL_C_NUMERIC y SQLSetDescField

 El [función SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md) es necesario para realizar el enlace manual con valores SQL_C_NUMERIC. (Tenga en cuenta que se ha agregado SQLSetDescField en ODBC 3.0). Para realizar el enlace manual, primero debe obtener el identificador de descriptor.  

```cpp
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
