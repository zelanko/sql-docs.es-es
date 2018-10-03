---
title: Llamar a SQLColumns sobre una tabla con columnas dispersas | Documentos de Microsoft
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
yms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: afd35e13-2370-43c2-9cbc-f8da6248c39c
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 73bd92ad269d8b5593c1245b30d44a9bb5728708
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47685413"
---
# <a name="call-sqlcolumns-on-a-table-with-sparse-columns"></a>Llamar a SQLColumns sobre una tabla con columnas dispersas
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  En este ejemplo, se muestra cómo llamar a SQLColumns sobre una tabla con columnas dispersas definidas mediante ODBC en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client.  
  
 No funcionará con ninguna versión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] anterior a [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)].  
  
 Para obtener más información acerca de esta característica de columnas dispersas, vea [Sparse Columns Support in SQL Server Native Client](../../relational-databases/native-client/features/sparse-columns-support-in-sql-server-native-client.md).  
  
## <a name="example"></a>Ejemplo  
 La primera lista de código es el código fuente de C++. Cambie “MyServer” por un nombre de servidor válido. Asegúrese de que la variable de entorno INCLUDE incluye el directorio que contiene sqlncli.h. Si genera y ejecuta este ejemplo como una aplicación de 32 bits en un sistema operativo de 64 bits, debe crear el origen de datos ODBC con el Administrador ODBC en %windir%\SysWOW64\odbcad32.exe.  
  
 Este ejemplo se conecta a la instancia predeterminada de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] del equipo. Para conectarse a una instancia con nombre, cambie la definición del origen de datos ODBC para especificar la instancia utilizando el formato servidor\instanciaConNombre. De forma predeterminada, [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] se instala en una instancia con nombre.  
  
 Compile con /EHsc /D, "UNICODE", y odbc32.lib.  
  
 La segunda lista de código ([!INCLUDE[tsql](../../includes/tsql-md.md)]) elimina la tabla creada por este ejemplo.  
  
```  
// compile with: /EHsc /D "UNICODE" odbc32.lib  
#include <windows.h>  
#include <stdio.h>  
#include <sqlext.h>  
  
#include <sqlncli.h>  
  
#define SUCCESS(x) (!((x) & 0xFFFE))  
  
#define CHKRC(stmt) rc = (stmt); \  
   if (!SUCCESS(rc)) \  
   throw (RETCODE) rc;  
  
void PrintError(SQLSMALLINT HandleType, SQLHANDLE Handle) {  
   RETCODE rc = SQL_SUCCESS;  
   SQLTCHAR szSqlState[6], szMessage[1024];  
   SQLSMALLINT i = 1, msgLen = 0;  
   SQLINTEGER NativeError;  
  
   do {  
      i = 1;  
      while (SQL_NO_DATA != (rc = SQLGetDiagRec(HandleType, Handle, i, szSqlState, &NativeError,   
         szMessage, sizeof(szMessage)/sizeof(SQLTCHAR), &msgLen)) && SUCCESS(rc)) {  
            wprintf(L"SQLState=%s, NativeError=%ld, Message=%s\r\n", szSqlState, NativeError, szMessage);  
            i++;  
      }  
   }   
   while (SQL_NO_DATA != (rc = SQLMoreResults(Handle)) && SUCCESS(rc));  
}  
  
#define STR_LEN 128 + 1  
#define REM_LEN 254 + 1  
  
void ProcessSQLColumnsResult(SQLHSTMT hstmt) {  
   SQLCHAR szSchema[STR_LEN];  
   SQLCHAR szCatalog[STR_LEN];  
   SQLCHAR szColumnName[STR_LEN];  
   SQLCHAR szTableName[STR_LEN];  
   SQLCHAR szTypeName[STR_LEN];  
   SQLCHAR szRemarks[REM_LEN];  
   SQLCHAR szColumnDefault[STR_LEN];  
   SQLCHAR szIsNullable[STR_LEN];  
  
   SQLINTEGER ColumnSize;  
   SQLINTEGER BufferLength;  
   SQLINTEGER CharOctetLength;  
   SQLINTEGER OrdinalPosition;  
  
   SQLSMALLINT DataType;  
   SQLSMALLINT DecimalDigits;  
   SQLSMALLINT NumPrecRadix;  
   SQLSMALLINT Nullable;  
   SQLSMALLINT SQLDataType;  
   SQLSMALLINT DatetimeSubtypeCode;  
   SQLLEN cbCatalog;  
   SQLLEN cbSchema;  
   SQLLEN cbTableName;  
   SQLLEN cbColumnName;  
   SQLLEN cbDataType;  
   SQLLEN cbTypeName;  
   SQLLEN cbColumnSize;  
   SQLLEN cbBufferLength;  
   SQLLEN cbDecimalDigits;  
   SQLLEN cbNumPrecRadix;  
   SQLLEN cbNullable;  
   SQLLEN cbRemarks;  
   SQLLEN cbColumnDefault;  
   SQLLEN cbSQLDataType;  
   SQLLEN cbDatetimeSubtypeCode;  
   SQLLEN cbCharOctetLength;  
   SQLLEN cbOrdinalPosition;  
   SQLLEN cbIsNullable;  
  
   SQLRETURN rc = SQL_SUCCESS;  
  
   CHKRC(SQLColumns(hstmt, L"tempdb", SQL_NTS, L"dbo", SQL_NTS, L"tbl_sparse_test", SQL_NTS, NULL, 0 ));  
  
   // Bind columns in result set to buffers  
   SQLBindCol(hstmt, 1,  SQL_C_CHAR,   szCatalog,              STR_LEN,    &cbCatalog);  
   SQLBindCol(hstmt, 2,  SQL_C_CHAR,   szSchema,               STR_LEN,    &cbSchema);  
   SQLBindCol(hstmt, 3,  SQL_C_CHAR,   szTableName,            STR_LEN,    &cbTableName);  
   SQLBindCol(hstmt, 4,  SQL_C_CHAR,   szColumnName,           STR_LEN,    &cbColumnName);  
   SQLBindCol(hstmt, 5,  SQL_C_SSHORT, &DataType,              0,          &cbDataType);  
   SQLBindCol(hstmt, 6,  SQL_C_CHAR,   szTypeName,             STR_LEN,    &cbTypeName);  
   SQLBindCol(hstmt, 7,  SQL_C_SLONG,  &ColumnSize,            0,          &cbColumnSize);  
   SQLBindCol(hstmt, 8,  SQL_C_SLONG,  &BufferLength,          0,          &cbBufferLength);  
   SQLBindCol(hstmt, 9,  SQL_C_SSHORT, &DecimalDigits,         0,          &cbDecimalDigits);  
   SQLBindCol(hstmt, 10, SQL_C_SSHORT, &NumPrecRadix,          0,          &cbNumPrecRadix);  
   SQLBindCol(hstmt, 11, SQL_C_SSHORT, &Nullable,              0,          &cbNullable);  
   SQLBindCol(hstmt, 12, SQL_C_CHAR,   szRemarks,              REM_LEN,    &cbRemarks);  
   SQLBindCol(hstmt, 13, SQL_C_CHAR,   szColumnDefault,        STR_LEN,    &cbColumnDefault);  
   SQLBindCol(hstmt, 14, SQL_C_SSHORT, &SQLDataType,           0,          &cbSQLDataType);  
   SQLBindCol(hstmt, 15, SQL_C_SSHORT, &DatetimeSubtypeCode,   0,          &cbDatetimeSubtypeCode);  
   SQLBindCol(hstmt, 16, SQL_C_SLONG,  &CharOctetLength,       0,          &cbCharOctetLength);  
   SQLBindCol(hstmt, 17, SQL_C_SLONG,  &OrdinalPosition,       0,          &cbOrdinalPosition);  
   SQLBindCol(hstmt, 18, SQL_C_CHAR,   szIsNullable,           STR_LEN,    &cbIsNullable);  
  
   try {  
      while (SQL_SUCCESS == rc) {  
         CHKRC(SQLFetch(hstmt));  
         wprintf(L"Column name: %hs\tIsNullable: %hs\tType: %hs\n", szColumnName, szIsNullable, szTypeName);  
      }  
   }  
   catch (RETCODE retcode) {  
      if (SQL_NO_DATA != retcode)  
         throw retcode;  
   }  
   SQLFreeStmt(hstmt, SQL_CLOSE);  
}  
  
int main() {  
   RETCODE rc = SQL_SUCCESS;  
   HENV henv = SQL_NULL_HENV;  
   HDBC hdbc = SQL_NULL_HDBC;  
   SQLHSTMT hstmt = SQL_NULL_HSTMT;  
   SQLTCHAR * pszConnection = L"DRIVER={SQL Server Native Client 10.0}; Server=MyServer; Trusted_Connection=Yes;";  
  
   try {  
      CHKRC(SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HENV, &henv));  
      CHKRC(SQLSetEnvAttr(henv, SQL_ATTR_ODBC_VERSION, (SQLPOINTER)SQL_OV_ODBC3, 0));  
      CHKRC(SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc));  
      CHKRC(SQLDriverConnect( hdbc, NULL, pszConnection, SQL_NTS, NULL, 0, NULL, SQL_DRIVER_NOPROMPT));  
      CHKRC(SQLAllocHandle(SQL_HANDLE_STMT, hdbc, &hstmt));  
      CHKRC(SQLExecDirect(hstmt,  
         L"if object_id('tempdb.dbo.tbl_sparse_test','U') is not null drop table tempdb.dbo.tbl_sparse_test",  
         SQL_NTS));  
  
      // Create a new table  
      CHKRC(SQLExecDirect(hstmt,  
         L"create table tempdb.dbo.tbl_sparse_test (col1 int SPARSE, col2 int, col3 XML column_set for all_sparse_columns)",  
         SQL_NTS));  
  
      // Insert a row into the table  
      CHKRC(SQLExecDirect(hstmt,  
         L"insert tempdb.dbo.tbl_sparse_test (col1, col2) values (1,2)",  
         SQL_NTS));  
  
      wprintf(L"Checking default SQLColumns behavior.\nYou should not see the first sparse column.\n");  
  
      ProcessSQLColumnsResult(hstmt);  
  
      wprintf(L"\nChecking SQLColumns with the statement attribute SQL_SS_NAME_SCOPE_EXTENDED.\nYou should see all the columns\n");  
      CHKRC(SQLSetStmtAttr(hstmt, SQL_SOPT_SS_NAME_SCOPE, (SQLPOINTER)SQL_SS_NAME_SCOPE_EXTENDED, SQL_IS_SMALLINT));  
  
      ProcessSQLColumnsResult(hstmt);  
  
      wprintf(L"\nChecking SQLColumns with the statement attribute SQL_SS_NAME_SCOPE_SPARSE_COLUMN_SET.\nYou should see only the sparse columns\n");  
      CHKRC(SQLSetStmtAttr(hstmt, SQL_SOPT_SS_NAME_SCOPE, (SQLPOINTER)SQL_SS_NAME_SCOPE_SPARSE_COLUMN_SET, SQL_IS_SMALLINT));  
  
      ProcessSQLColumnsResult(hstmt);  
  
   }  
   catch (RETCODE retcode) {  
      rc = retcode;  
   }  
  
   if (!SUCCESS(rc)) {  
      if (hstmt)  
         PrintError(SQL_HANDLE_STMT, hstmt);  
      else if (hdbc)  
         PrintError(SQL_HANDLE_DBC, hdbc);  
      else if(henv)  
         PrintError(SQL_HANDLE_ENV, henv);  
   }  
  
   if (hstmt)  
      SQLFreeHandle(SQL_HANDLE_STMT, hstmt);  
   if (hdbc) {  
      SQLDisconnect(hdbc);  
      SQLFreeHandle(SQL_HANDLE_DBC, hdbc);  
   }  
   if (henv)  
      SQLFreeHandle(SQL_HANDLE_ENV, henv);  
}  
```  
  
```  
use tempdb  
IF EXISTS (SELECT name FROM sysobjects WHERE name = 'tbl_sparse_test')  
     DROP TABLE tbl_sparse_test  
GO  
```  
  
  
