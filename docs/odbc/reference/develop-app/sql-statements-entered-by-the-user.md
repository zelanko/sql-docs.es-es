---
title: Instrucciones SQL escritas por el usuario | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- user-entered SQL statements [ODBC]
- SQL statements [ODBC], constructing
- SQL statements [ODBC], entered by user
ms.assetid: 109af162-93ba-425a-8fe5-49c7dc7cc784
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: bf2f8cf36be392cb42a970fa2fb0b19c35daeb39
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "81301966"
---
# <a name="sql-statements-entered-by-the-user"></a>Instrucciones SQL escritas por el usuario
Las aplicaciones que realizan el análisis ad hoc también permiten normalmente al usuario escribir instrucciones SQL directamente. Por ejemplo:  
  
```  
SQLCHAR *     Statement, SqlState[6], Msg[SQL_MAX_MESSAGE_LENGTH];  
SQLSMALLINT   i, MsgLen;  
SQLINTEGER    NativeError;  
SQLRETURN     rc1, rc2;  
  
// Prompt user for SQL statement.  
GetSQLStatement(Statement);  
  
// Execute the statement directly. Because it will be executed only once,  
// do not prepare it.  
rc1 = SQLExecDirect(hstmt, Statement, SQL_NTS);  
  
// Process any errors or returned information.  
if ((rc1 == SQL_ERROR) || rc1 == SQL_SUCCESS_WITH_INFO) {  
   i = 1;  
   while ((rc2 = SQLGetDiagRec(SQL_HANDLE_STMT, hstmt, i, SqlState, &NativeError,  
         Msg, sizeof(Msg), &MsgLen)) != SQL_NO_DATA) {  
      DisplayError(SqlState, NativeError, Msg, MsgLen);  
      i++;  
   }  
}  
```  
  
 Este enfoque simplifica la codificación de aplicaciones; la aplicación se basa en el usuario para compilar la instrucción SQL y en el origen de datos para comprobar la validez de la instrucción. Dado que es difícil escribir una interfaz gráfica de usuario que exponga adecuadamente las complejidades de SQL, basta con solicitar al usuario que escriba el texto de la instrucción SQL que puede ser una alternativa preferible. Sin embargo, esto requiere que el usuario conozca no solo SQL sino también el esquema del origen de datos que se consulta. Algunas aplicaciones proporcionan una interfaz gráfica de usuario por la que el usuario puede crear una instrucción SQL básica y proporcionar también una interfaz de texto con la que el usuario puede modificarla.
