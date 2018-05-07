---
title: Usar SQLGetDiagRec y SQLGetDiagField | Documentos de Microsoft
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
- diagnostic information [ODBC], SqlGetDiagField
- SQLGetDiagField function [ODBC], and SQLGetDiagRec
- SQLGetDiagRec function [ODBC], and SQLGetDiagField
- diagnostic information [ODBC], SqlGetDiagRec
- retrieving diagnostic information [ODBC]
ms.assetid: 4f486bb1-fad8-4064-ac9d-61f2de85b68b
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 555bc3ba25ba895b54384acb8772a4b4293e61c1
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="using-sqlgetdiagrec-and-sqlgetdiagfield"></a>Uso de SQLGetDiagRec y SQLGetDiagField
Aplicaciones llaman a **SQLGetDiagRec** o **SQLGetDiagField** para recuperar información de diagnóstico. Estas funciones aceptan un identificador de entorno, conexión, instrucción o descriptor de y devuelven diagnósticos de la función que se utilizó por última vez ese identificador. Los diagnósticos de un determinado identificador de la sesión se descartan cuando se llama a una función nueva con el mismo identificador. Si la función devuelve varios registros de diagnóstico, la aplicación llama a estas funciones varias veces; el número total de registros de estado se recupera mediante una llamada a **SQLGetDiagField** para el registro de encabezado (registro 0) con la opción SQL_DIAG_NUMBER.  
  
 Las aplicaciones que recuperar los campos de diagnóstico individuales mediante una llamada a **SQLGetDiagField** y especificar el campo que desea recuperar. Determinados campos de diagnóstico no tiene ningún significado para ciertos tipos de identificadores. Para obtener una lista de campos de diagnóstico y sus significados, vea el [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md) descripción de la función.  
  
 Las aplicaciones que recuperar el SQLSTATE, el código de error nativo y el mensaje de diagnóstico en una sola llamada mediante una llamada a **SQLGetDiagRec**; **SQLGetDiagRec** no se puede usar para recuperar información desde el registro de encabezado.  
  
 Por ejemplo, el siguiente código pide al usuario una instrucción SQL y lo ejecuta. Si se ha devuelto ninguna información de diagnóstico, llama a **SQLGetDiagField** para obtener el número de registros de estado y **SQLGetDiagRec** para obtener el SQLSTATE, el código de error nativo y el mensaje de diagnóstico de los registros.  
  
```  
SQLCHAR       SqlState[6], SQLStmt[100], Msg[SQL_MAX_MESSAGE_LENGTH];  
SQLINTEGER    NativeError;  
SQLSMALLINT   i, MsgLen;  
SQLRETURN     rc1, rc2;  
SQLHSTMT      hstmt;  
  
// Prompt the user for an SQL statement.  
GetSQLStmt(SQLStmt);  
  
// Execute the SQL statement and return any errors or warnings.  
rc1 = SQLExecDirect(hstmt, SQLStmt, SQL_NTS);  
if ((rc1 == SQL_SUCCESS_WITH_INFO) || (rc1 == SQL_ERROR)) {
   SQLLEN numRecs = 0;
   SQLGetDiagField(SQL_HANDLE_STMT, hstmt, 0, SQL_DIAG_NUMBER, &numRecs, 0, 0);
   // Get the status records.
   i = 1;  
   while (i <= numRecs && (rc2 = SQLGetDiagRec(SQL_HANDLE_STMT, hstmt, i, SqlState, &NativeError,  
            Msg, sizeof(Msg), &MsgLen)) != SQL_NO_DATA) {  
      DisplayError(SqlState,NativeError,Msg,MsgLen);  
      i++;  
   }  
}  
  
if ((rc1 == SQL_SUCCESS) || (rc1 == SQL_SUCCESS_WITH_INFO)) {  
   // Process statement results, if any.  
}  
```
