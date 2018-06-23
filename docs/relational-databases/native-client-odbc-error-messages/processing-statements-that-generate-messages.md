---
title: Procesar instrucciones que generan mensajes | Documentos de Microsoft
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- PRINT statement
- messages [ODBC], statements generating messages
- statements [ODBC], message generation
- errors [ODBC], statements generating messages
- SQL Server Native Client ODBC driver, errors
- STATISTICS IO option
- STATISTICS TIME option
- DBCC statements
- SQLExecute function
- RAISERROR statement
- SQLGetDiagRec function
- ODBC error handling, statements generating messages
- SQLExecDirect function
ms.assetid: 672ebdc5-7fa1-4ceb-8d52-fd25ef646654
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 5ff2141bb8b84fa27d9aefe00f3a48281d5c017e
ms.sourcegitcommit: a78fa85609a82e905de9db8b75d2e83257831ad9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2018
ms.locfileid: "35703746"
---
# <a name="processing-statements-that-generate-messages"></a>Procesar instrucciones que generan mensajes
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Las opciones STATISTICS TIME y STATISTICS IO de la instrucción SET de [!INCLUDE[tsql](../../includes/tsql-md.md)] se utilizan para obtener información que ayuda a diagnosticar las consultas de ejecución prolongada. Las versiones anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] también admiten la opción SHOWPLAN para analizar los planes de consulta. Una aplicación ODBC puede establecer estas opciones ejecutando las instrucciones siguientes:  
  
```  
SQLExecDirect(hstmt, "SET SHOWPLAN ON", SQL_NTS);  
SQLExecDirect(hstmt, "SET STATISTICS TIME ON", SQL_NTS90  
);  
SQLExecDirect(hstmt, "SET STATISTICS IO ON", SQL_NTS);  
```  
  
 Cuando SET STATISTICS TIME o SET SHOWPLAN son ON, **SQLExecute** y **SQLExecDirect** devuelvan SQL_SUCCESS_WITH_INFO y, en ese momento, la aplicación puede recuperar la salida SHOWPLAN o las estadísticas de tiempo mediante una llamada a **SQLGetDiagRec** hasta que devuelva SQL_NO_DATA. Cada línea de datos de SHOWPLAN se devuelve en el formato:  
  
```  
szSqlState="01000", *pfNativeError=6223,  
szErrorMsg="[Microsoft][SQL Server Native Client][SQL Server]   
              Table Scan"  
```  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] versión 7.0 reemplazó la opción SHOWPLAN por SHOWPLAN_ALL y SHOWPLAN_TEXT, las dos devuelven la salida como un conjunto de resultados, no como un conjunto de mensajes.  
  
 Cada línea de STATISTICS TIME se devuelve en el formato:  
  
```  
szSqlState="01000", *pfNativeError= 3613,  
szErrorMsg="[Microsoft][SQL Server Native Client][SQL Server]  
   SQL Server Parse and Compile Time: cpu time = 0 ms."  
```  
  
 La salida de SET STATISTICS IO no está disponible hasta el final de un conjunto de resultados. Para obtener la salida de STATISTICS IO, la aplicación llama **SQLGetDiagRec** en el momento de **SQLFetch** o [SQLFetchScroll](../../relational-databases/native-client-odbc-api/sqlfetchscroll.md) devuelve SQL_NO_DATA. La salida de STATISTICS IO se devuelve en el formato:  
  
```  
szSqlState="01000", *pfNativeError= 3615,  
szErrorMsg="[Microsoft][ SQL Server Native Client][SQL Server]  
   Table: testshow  scan count 1,  logical reads: 1,  
   physical reads: 0."  
```  
  
## <a name="using-dbcc-statements"></a>Utilizar instrucciones DBCC  
 Las instrucciones DBCC devuelven los datos como mensajes, no como conjuntos de resultados. **SQLExecDirect** o **SQLExecute** devuelve SQL_SUCCESS_WITH_INFO y la aplicación recupera el resultado mediante una llamada a **SQLGetDiagRec** hasta que devuelva SQL_NO_DATA.  
  
 Por ejemplo, la instrucción siguiente devuelve SQL_SUCCESS_WITH_INFO:  
  
```  
SQLExecDirect(hstmt, "DBCC CHECKTABLE(Authors)", SQL_NTS);  
```  
  
 Las llamadas a **SQLGetDiagRec** devolver:  
  
```  
szSqlState = "01000", *pfNativeError = 2536,  
szErrorMsg="[Microsoft][ SQL Server Native Client][SQL Server]  
   Checking authors"  
szSqlState = "01000", *pfNativeError = 2579,  
szErrorMsg="[Microsoft][ SQL Server Native Client][SQL Server]  
   The total number of data pages in this table is 1."  
szSqlState = "01000", *pfNativeError = 7929,  
szErrorMsg="[Microsoft][ SQL Server Native Client][SQL Server]  
   Table has 23 data rows."  
szSqlState = "01000", *pfNativeError = 2528  
szErrorMsg="[Microsoft][ SQL Server Native Client][SQL Server]  
   DBCC execution completed. If DBCC printed error messages,  
   see your System Administrator."  
```  
  
## <a name="using-print-and-raiserror-statements"></a>Utilizar instrucciones RAISERROR y PRINT  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] Las instrucciones PRINT y RAISERROR también devuelven datos mediante una llamada a **SQLGetDiagRec**. Las instrucciones PRINT hacen que la ejecución de la instrucción SQL devuelva SQL_SUCCESS_WITH_INFO y una llamada subsiguiente a **SQLGetDiagRec** devuelve un *SQLState* de 01000. Un RAISERROR con una gravedad de diez o inferior se comporta igual que PRINT. Una instrucción RAISERROR con una gravedad de 11 o superior hace que la ejecución devuelva SQL_ERROR y una llamada subsiguiente a **SQLGetDiagRec** devuelve *SQLState* 42000. Por ejemplo, la instrucción siguiente devuelve SQL_SUCCESS_WITH_INFO:  
  
```  
SQLExecDirect (hstmt, "PRINT  'Some message' ", SQL_NTS);  
```  
  
 Al llamar a **SQLGetDiagRec** devuelve:  
  
```  
szSQLState = "01000", *pfNative Error = 0,  
szErrorMsg= "[Microsoft] [SQL Server Native Client][SQL Server]  
   Some message"  
```  
  
 La instrucción siguiente devuelve SQL_SUCCESS_WITH_INFO:  
  
```  
SQLExecDirect (hstmt, "RAISERROR ('Sample error 1.', 10, -1)",  
   SQL_NTS)  
```  
  
 Al llamar a **SQLGetDiagRec** devuelve:  
  
```  
szSQLState = "01000", *pfNative Error = 50000,  
szErrorMsg= "[Microsoft] [SQL Server Native Client][SQL Server]  
   Sample error 1."  
```  
  
 La siguiente instrucción devuelve SQL_ERROR.  
  
```  
SQLExecDirect (hstmt, "RAISERROR ('Sample error 2.', 11, -1)", SQL_NTS)  
```  
  
 Al llamar a **SQLGetDiagRec** devuelve:  
  
```  
szSQLState = "42000", *pfNative Error = 50000,  
szErrorMsg= "[Microsoft] [SQL Server Native Client][SQL Server]  
   Sample error 2."  
```  
  
 El tiempo de llamar al método **SQLGetDiagRec** es fundamental cuando la salida de instrucciones PRINT o RAISERROR se incluye en un conjunto de resultados. La llamada a **SQLGetDiagRec** para recuperar la función PRINT o RAISERROR se debe realizar la salida inmediatamente después de la instrucción que recibe SQL_ERROR o SQL_SUCCESS_WITH_INFO. Esto es sencillo cuando solo se ejecuta una instrucción SQL única, como en los ejemplos anteriores. En estos casos, la llamada a **SQLExecDirect** o **SQLExecute** devuelve SQL_ERROR o SQL_SUCCESS_WITH_INFO y **SQLGetDiagRec** , a continuación, se puede llamar. Es menos sencillo al codificar los bucles para administrar la salida de un lote de instrucciones SQL o al ejecutar los procedimientos almacenados de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 En este caso, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] devuelve un conjunto de resultados para cada instrucción SELECT ejecutada en un lote o procedimiento almacenado. Si el lote o procedimiento contiene instrucciones RAISERROR o PRINT, la salida de éstas se intercala con los conjuntos de resultados de la instrucción SELECT. Si la primera instrucción del lote o procedimiento es PRINT o RAISERROR, el **SQLExecute** o **SQLExecDirect** devuelve SQL_SUCCESS_WITH_INFO o SQL_ERROR y la aplicación necesita llamar a **SQLGetDiagRec** hasta que devuelva SQL_NO_DATA para recuperar la información de PRINT o RAISERROR.  
  
 Si la instrucción PRINT o RAISERROR viene después de una instrucción SQL (por ejemplo, una instrucción SELECT), la información de PRINT o RAISERROR se devuelve cuando [SQLMoreResults](../../relational-databases/native-client-odbc-api/sqlmoreresults.md)posiciones en el resultado de conjunto que contiene el error. **SQLMoreResults** devuelve SQL_SUCCESS_WITH_INFO o SQL_ERROR según la gravedad del mensaje. Los mensajes se recuperan mediante una llamada a **SQLGetDiagRec** hasta que devuelva SQL_NO_DATA.  
  
## <a name="see-also"></a>Vea también  
 [Controlar errores y mensajes](../../relational-databases/native-client-odbc-error-messages/handling-errors-and-messages.md)  
  
  
