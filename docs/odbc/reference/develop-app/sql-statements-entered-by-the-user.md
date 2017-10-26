---
title: Instrucciones SQL especificados por el usuario | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- user-entered SQL statements [ODBC]
- SQL statements [ODBC], constructing
- SQL statements [ODBC], entered by user
ms.assetid: 109af162-93ba-425a-8fe5-49c7dc7cc784
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: b234123c01d4bdf4590c000b996a4febe4ad485e
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="sql-statements-entered-by-the-user"></a>Instrucciones SQL escritas por el usuario
Las aplicaciones que realizan análisis ad hoc suelen permiten al usuario escribir instrucciones SQL directamente. Por ejemplo:  
  
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
  
 Este enfoque simplifica el código de aplicación; la aplicación se basa en el usuario para generar la instrucción SQL y en el origen de datos para comprobar la validez de la instrucción. Dado que es difícil de escribir una interfaz gráfica de usuario que expone adecuadamente las complejidades de SQL, simplemente pidiendo al usuario que escriba el texto de la instrucción SQL puede ser una alternativa preferible. Sin embargo, esto requiere que el usuario saber no solo SQL, sino también el esquema del origen de datos que se está consultando. Algunas aplicaciones proporcionan una interfaz gráfica de usuario mediante el cual el usuario puede crear una instrucción básica de SQL y también proporcionan una interfaz de texto con el que el usuario puede modificar.

