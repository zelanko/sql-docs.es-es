---
title: Procesamiento de declaraciones que generan mensajes Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
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
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 9820e202f5032423292c4306aa63b175bce550b6
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304706"
---
# <a name="processing-statements-that-generate-messages"></a>Procesar instrucciones que generan mensajes
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Las opciones STATISTICS TIME y STATISTICS IO de la instrucción SET de [!INCLUDE[tsql](../../includes/tsql-md.md)] se utilizan para obtener información que ayuda a diagnosticar las consultas de ejecución prolongada. Las versiones anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] también admiten la opción SHOWPLAN para analizar los planes de consulta. Una aplicación ODBC puede establecer estas opciones ejecutando las instrucciones siguientes:  
  
```  
SQLExecDirect(hstmt, "SET SHOWPLAN ON", SQL_NTS);  
SQLExecDirect(hstmt, "SET STATISTICS TIME ON", SQL_NTS90  
);  
SQLExecDirect(hstmt, "SET STATISTICS IO ON", SQL_NTS);  
```  
  
 Cuando SET STATISTICS TIME o SET SHOWPLAN están activados, **SQLExecute** y **SQLExecDirect** devuelven SQL_SUCCESS_WITH_INFO y, en ese momento, la aplicación puede recuperar la salida SHOWPLAN o STATISTICS TIME llamando a **SQLGetDiagRec** hasta que devuelve SQL_NO_DATA. Cada línea de datos de SHOWPLAN se devuelve en el formato:  
  
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
  
 La salida de SET STATISTICS IO no está disponible hasta el final de un conjunto de resultados. Para obtener la salida de E/S de STATISTICS, la aplicación llama a **SQLGetDiagRec** en el momento en que **SQLFetch** o [SQLFetchScroll](../../relational-databases/native-client-odbc-api/sqlfetchscroll.md) devuelve SQL_NO_DATA. La salida de STATISTICS IO se devuelve en el formato:  
  
```  
szSqlState="01000", *pfNativeError= 3615,  
szErrorMsg="[Microsoft][ SQL Server Native Client][SQL Server]  
   Table: testshow  scan count 1,  logical reads: 1,  
   physical reads: 0."  
```  
  
## <a name="using-dbcc-statements"></a>Utilizar instrucciones DBCC  
 Las instrucciones DBCC devuelven los datos como mensajes, no como conjuntos de resultados. **SQLExecDirect** o **SQLExecute** devuelven SQL_SUCCESS_WITH_INFO y la aplicación recupera la salida mediante una llamada a **SQLGetDiagRec** hasta que devuelve SQL_NO_DATA.  
  
 Por ejemplo, la instrucción siguiente devuelve SQL_SUCCESS_WITH_INFO:  
  
```  
SQLExecDirect(hstmt, "DBCC CHECKTABLE(Authors)", SQL_NTS);  
```  
  
 Las llamadas a **SQLGetDiagRec** devuelven:  
  
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
 [!INCLUDE[tsql](../../includes/tsql-md.md)]Las instrucciones PRINT y RAISERROR también devuelven datos llamando a **SQLGetDiagRec**. Las instrucciones PRINT hacen que la ejecución de la instrucción SQL devuelva SQL_SUCCESS_WITH_INFO y una llamada posterior a **SQLGetDiagRec** devuelve un *SQLState* de 01000. Un RAISERROR con una gravedad de diez o inferior se comporta igual que PRINT. Un RAISERROR con una gravedad de 11 o superior hace que la ejecución devuelva SQL_ERROR y una llamada posterior a **SQLGetDiagRec** devuelve *SQLState* 42000. Por ejemplo, la instrucción siguiente devuelve SQL_SUCCESS_WITH_INFO:  
  
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
  
 El momento de llamar a **SQLGetDiagRec** es crítico cuando la salida de las instrucciones PRINT o RAISERROR se incluye en un conjunto de resultados. La llamada a **SQLGetDiagRec** para recuperar la salida PRINT o RAISERROR debe realizarse inmediatamente después de la instrucción que recibe SQL_ERROR o SQL_SUCCESS_WITH_INFO. Esto es sencillo cuando solo se ejecuta una instrucción SQL única, como en los ejemplos anteriores. En estos casos, la llamada a **SQLExecDirect** o **SQLExecute** devuelve SQL_ERROR o SQL_SUCCESS_WITH_INFO y **SQLGetDiagRec,** a continuación, se puede llamar. Es menos sencillo al codificar los bucles para administrar la salida de un lote de instrucciones SQL o al ejecutar los procedimientos almacenados de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 En este caso, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] devuelve un conjunto de resultados para cada instrucción SELECT ejecutada en un lote o procedimiento almacenado. Si el lote o procedimiento contiene instrucciones RAISERROR o PRINT, la salida de éstas se intercala con los conjuntos de resultados de la instrucción SELECT. Si la primera instrucción del lote o procedimiento es PRINT o RAISERROR, **SQLExecute** o **SQLExecDirect** devuelve SQL_SUCCESS_WITH_INFO o SQL_ERROR y la aplicación debe llamar a **SQLGetDiagRec** hasta que devuelve SQL_NO_DATA recuperar la información PRINT o RAISERROR.  
  
 Si la instrucción PRINT o RAISERROR procede después de una instrucción SQL (como una instrucción SELECT), se devuelve la información PRINT o RAISERROR cuando [SQLMoreResults](../../relational-databases/native-client-odbc-api/sqlmoreresults.md)se posiciona en el conjunto de resultados que contiene el error. **SQLMoreResults** devuelve SQL_SUCCESS_WITH_INFO o SQL_ERROR en función de la gravedad del mensaje. Los mensajes se recuperan mediante una llamada a **SQLGetDiagRec** hasta que devuelve SQL_NO_DATA.  
  
## <a name="see-also"></a>Consulte también  
 [Controlar errores y mensajes](../../relational-databases/native-client-odbc-error-messages/handling-errors-and-messages.md)  
  
  
