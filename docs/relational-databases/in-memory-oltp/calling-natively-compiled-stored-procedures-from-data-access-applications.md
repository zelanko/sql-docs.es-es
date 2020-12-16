---
title: 'Procedimientos almacenados compilados de forma nativa: aplicaciones de acceso a datos'
description: Busque instrucciones para llamar a procedimientos almacenados compilados de forma nativa desde aplicaciones de acceso a datos, con un ejemplo que utiliza el controlador ODBC de SQL Server Native Client.
ms.custom: seo-dt-2019
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 9cf6c5ff-4548-401a-b3ec-084f47ff0eb8
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 77c9d57563fb926a777a20edc89e8dbde7bf204d
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/14/2020
ms.locfileid: "97465416"
---
# <a name="calling-natively-compiled-stored-procedures-from-data-access-applications"></a>Llamar a procedimientos almacenados compilados de forma nativa desde aplicaciones de acceso a datos

[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]

Este tema describe instrucciones para llamar a procedimientos almacenados compilados de forma nativa desde aplicaciones de acceso a datos.

## <a name="guidance-points"></a>Puntos de orientación

- Los cursores no pueden iterar sobre un procedimiento almacenado compilado de forma nativa.

- No se permite llamar a procedimientos almacenados compilados de forma nativa desde módulos CLR con la conexión de contexto.

### <a name="sqlclient"></a>SqlClient

- Para SqlClient, no se distingue entre la ejecución *preparada* y la *directa*. Ejecute los procedimientos almacenados mediante SqlCommand con `CommandType = CommandType.StoredProcedure`.

- SqlClient no admite las llamadas a procedimiento RPC preparadas.

- SqlClient no admite la recuperación de información solo de esquema (detección de metadatos) sobre los conjuntos de resultados devueltos por un procedimiento almacenado compilado de forma nativa (`CommandType.SchemaOnly`).
  - Use en su lugar [sp_describe_first_result_set &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-describe-first-result-set-transact-sql.md).

### <a name="sql-server-native-client"></a>SQL Server Native Client

- La versiones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client anteriores a [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] no permiten recuperar información solo de esquema (detección de metadatos) sobre los conjuntos de resultados devueltos por un procedimiento almacenado compilado de forma nativa.
- Use en su lugar [sp_describe_first_result_set &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-describe-first-result-set-transact-sql.md).

### <a name="odbc"></a>ODBC

Las siguientes recomendaciones se aplican a las llamadas a procedimientos almacenados compilados de forma nativa con el controlador ODBC de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client.

*Llamada una vez:* La forma más eficaz de llamar a un procedimiento almacenado es emitir una llamada RPC directa con **SQLExecDirect** y cláusulas ODBC CALL. No use la instrucción [!INCLUDE[tsql](../../includes/tsql-md.md)] **EXECUTE**. Si un procedimiento almacenado se llama más de una vez, la ejecución preparada es más eficaz.

*Llamada muchas veces:* La forma más eficaz de llamar a un procedimiento almacenado de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] más de una vez es a través de llamadas a procedimientos RPC preparadas. Las llamadas a RPC preparadas se realizan como se indica a continuación con el controlador ODBC de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client:

1. Abra una conexión a la base de datos.
2. Enlace los parámetros con **SQLBindParameter**.
3. Prepare la llamada a procedimiento con **SQLPrepare**.
4. Ejecute varias veces el procedimiento almacenado con **SQLExecute**.

#### <a name="c-code-for-odbc"></a>Código de C para ODBC

El fragmento de código de C siguiente muestra la ejecución preparada de un procedimiento almacenado para agregar elementos de línea a un pedido. **SQLPrepare** se llama solo una vez. Y **SQLExecute** se llama varias veces, una por cada ejecución de procedimiento.

```cpp
// Bind parameters
// 1 - OrdNo
SQLRETURN returnCode = SQLBindParameter(
                     hstmt, 1, SQL_PARAM_INPUT, SQL_C_LONG, SQL_INTEGER, 10, 0,
                     &order.OrdNo, sizeof(SQLINTEGER), NULL);
if (returnCode != SQL_SUCCESS && returnCode != SQL_SUCCESS_WITH_INFO) {
   ODBCError(henv, hdbc, hstmt, NULL, true);
   exit(-1);
}

// 2, 3, 4 - ItemNo, ProdCode, Qty
...

// Prepare stored procedure
returnCode = SQLPrepare(hstmt, (SQLTCHAR *) _T("{call ItemInsert(?, ?, ?, ?)}"),
                        SQL_NTS);

for (unsigned int i = 0; i < order.ItemCount; i++) {
   ItemNo = order.ItemNo[i];
   ProdCode = order.ProdCode[i];
   Qty = order.Qty[i];

   // Execute stored procedure
   returnCode = SQLExecute(hstmt);
   if (returnCode != SQL_SUCCESS && returnCode != SQL_SUCCESS_WITH_INFO) {
      ODBCError(henv, hdbc, hstmt, NULL, true);
      exit(-1);
   }
}
```

## <a name="using-odbc-to-execute-a-natively-compiled-stored-procedure"></a>Usar ODBC para ejecutar un procedimiento almacenado compilado de forma nativa

En este ejemplo se muestra cómo enlazar parámetros y ejecutar procedimientos almacenados con el controlador ODBC de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client. En el ejemplo se compila a una aplicación de consola que inserta un solo pedido mediante una ejecución directa, e inserta los detalles del pedido mediante una ejecución preparada.

Para ejecutar este ejemplo:

1. Cree una base de datos de ejemplo con un grupo de archivos de datos optimizados para memoria. Para obtener más información sobre cómo crear una base de datos con un grupo de archivos optimizados para memoria, vea [Crear una tabla optimizada para memoria y un procedimiento almacenado compilado de forma nativa](../../relational-databases/in-memory-oltp/creating-a-memory-optimized-table-and-a-natively-compiled-stored-procedure.md).

2. Cree un origen de datos ODBC denominado PrepExecSample que apunte a la base de datos. Utilice el controlador de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client. También podría modificar el ejemplo y utilizar [Microsoft ODBC Driver for SQL Server](../../connect/odbc/windows/microsoft-odbc-driver-for-sql-server-on-windows.md).

3. Ejecute el script [!INCLUDE[tsql](../../includes/tsql-md.md)] (a continuación) en la base de datos de ejemplo.

4. Compile y ejecute el ejemplo.

5. Compruebe que el programa se está ejecutando correctamente; para ello, consulte el contenido de las tablas:

    ```sql
    SELECT * FROM dbo.Ord;
    ```

    ```sql
    SELECT * FROM dbo.Item;
    ```

## <a name="preliminary-transact-sql"></a>Transact-SQL preliminar

A continuación se muestra el código de [!INCLUDE[tsql](../../includes/tsql-md.md)] que crea los objetos de base de datos optimizada para memoria.

```sql
IF EXISTS (SELECT * FROM SYS.OBJECTS WHERE OBJECT_ID=OBJECT_ID('dbo.OrderInsert'))
DROP PROCEDURE dbo.OrderInsert;  
GO
IF EXISTS (SELECT * FROM SYS.OBJECTS WHERE OBJECT_ID=OBJECT_ID('dbo.ItemInsert'))
DROP PROCEDURE dbo.ItemInsert;  
GO  
IF EXISTS (SELECT * FROM SYS.OBJECTS WHERE OBJECT_ID=OBJECT_ID('dbo.Ord'))
DROP TABLE dbo.Ord;  
GO  
IF EXISTS (SELECT * FROM SYS.OBJECTS WHERE OBJECT_ID=OBJECT_ID('dbo.Item'))
DROP TABLE dbo.Item;  
GO

CREATE TABLE dbo.Ord  
(  
   OrdNo INTEGER NOT NULL PRIMARY KEY NONCLUSTERED,  
   OrdDate DATETIME NOT NULL,   
   CustCode VARCHAR(5) NOT NULL)   
 WITH (MEMORY_OPTIMIZED=ON);  
GO  
  
CREATE TABLE dbo.Item  
(  
   OrdNo INTEGER NOT NULL,   
   ItemNo INTEGER NOT NULL,   
   ProdCode INTEGER NOT NULL,   
   Qty INTEGER NOT NULL,  
   CONSTRAINT PK_Item PRIMARY KEY NONCLUSTERED (OrdNo,ItemNo))  
   WITH (MEMORY_OPTIMIZED=ON);  
GO  
  
CREATE PROCEDURE dbo.OrderInsert(
    @OrdNo INTEGER, @CustCode VARCHAR(5))  
WITH NATIVE_COMPILATION, SCHEMABINDING, EXECUTE AS OWNER  
AS BEGIN ATOMIC WITH  
   (TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE = 'english')  
  
  DECLARE @OrdDate datetime = GETDATE();  
  INSERT INTO dbo.Ord (OrdNo, CustCode, OrdDate)
  VALUES (@OrdNo, @CustCode, @OrdDate);
END;  
GO  
  
CREATE PROCEDURE dbo.ItemInsert(
    @OrdNo INTEGER, @ItemNo INTEGER, @ProdCode INTEGER, @Qty INTEGER)
WITH NATIVE_COMPILATION, SCHEMABINDING, EXECUTE AS OWNER  
AS BEGIN ATOMIC WITH  
   (TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE = N'us_english')  
  
  INSERT INTO dbo.Item (OrdNo, ItemNo, ProdCode, Qty)
  VALUES (@OrdNo, @ItemNo, @ProdCode, @Qty)
END  
GO  
```

## <a name="c-code"></a>Código de C

El siguiente es el código C.

```cpp
// compile with: user32.lib odbc32.lib
#pragma once  
#define WIN32_LEAN_AND_MEAN  // Exclude rarely-used stuff from Windows headers.
#include <stdio.h>  
#include <stdlib.h>  
#include <tchar.h>  
#include <windows.h>  
#include "sql.h"  
#include "sqlext.h"  
#include "sqlncli.h"  
  
// cardinality of order item related array variables
#define ITEM_ARRAY_SIZE 20  
  
// struct to pass order entry data  
typedef struct OrdEntry_struct {  
   SQLINTEGER OrdNo;  
   SQLTCHAR CustCode[6];  
   SQLUINTEGER ItemCount;  
   SQLINTEGER ItemNo[ITEM_ARRAY_SIZE];  
   SQLINTEGER ProdCode[ITEM_ARRAY_SIZE];  
   SQLINTEGER Qty[ITEM_ARRAY_SIZE];  
} OrdEntryData;  
  
SQLHANDLE henv, hdbc, hstmt;  
  
void ODBCError(
      SQLHANDLE henv, SQLHANDLE hdbc,
      SQLHANDLE hstmt, SQLHANDLE hdesc,
      bool ShowError)
{  
   SQLRETURN r = 0;  
   SQLTCHAR szSqlState[6] = {0};  
   SQLINTEGER fNativeError = 0;  
   SQLTCHAR szErrorMsg[256] = {0};  
   SQLSMALLINT cbErrorMsgMax = sizeof(szErrorMsg) - 1;
   SQLSMALLINT cbErrorMsg = 0;  
   TCHAR text[1024] = {0}, title[256] = {0};  
  
   if (hdesc != NULL)  
      r = SQLGetDiagRec(SQL_HANDLE_DESC, hdesc, 1, szSqlState,
              &fNativeError, szErrorMsg, cbErrorMsgMax, &cbErrorMsg);
   else {  
      if (hstmt != NULL)  
         r = SQLGetDiagRec(SQL_HANDLE_STMT, hstmt, 1, szSqlState,
                 &fNativeError, szErrorMsg, cbErrorMsgMax, &cbErrorMsg);
      else {  
         if (hdbc != NULL)  
            r = SQLGetDiagRec(SQL_HANDLE_DBC, hdbc, 1, szSqlState,
                    &fNativeError, szErrorMsg, cbErrorMsgMax, &cbErrorMsg);
         else  
            r = SQLGetDiagRec(SQL_HANDLE_ENV, henv, 1, szSqlState,
                    &fNativeError, szErrorMsg, cbErrorMsgMax, &cbErrorMsg);
      }  
   }  
  
   if (ShowError) {  
      _sntprintf_s(title, _countof(title), _TRUNCATE, _T("ODBC Error %i"),
                      fNativeError);  
      _sntprintf_s(text, _countof(text), _TRUNCATE, _T("[%s] - %s"),
                      szSqlState, szErrorMsg);  
  
      MessageBox(NULL, (LPCTSTR) text, (LPCTSTR) _T("ODBC Error"), MB_OK);
   }  
}  
  
void connect() {  
   SQLRETURN r;  
  
   r = SQLAllocHandle(SQL_HANDLE_ENV, NULL, &henv);  
  
   // This is an ODBC v3 application  
   r = SQLSetEnvAttr(henv, SQL_ATTR_ODBC_VERSION, (SQLPOINTER) SQL_OV_ODBC3, 0);
   if (r != SQL_SUCCESS && r != SQL_SUCCESS_WITH_INFO) {  
      ODBCError(henv, NULL, NULL, NULL, true);  
      exit(-1);  
   }  
  
   r = SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc);  
  
   // Run in ANSI/implicit transaction mode  
   r = SQLSetConnectAttr(hdbc, SQL_ATTR_AUTOCOMMIT,
                          (SQLPOINTER) SQL_AUTOCOMMIT_OFF, SQL_IS_INTEGER);
   if (r != SQL_SUCCESS && r != SQL_SUCCESS_WITH_INFO) {  
      ODBCError(henv, NULL, NULL, NULL, true);  
      exit(-1);  
   }  
  
   TCHAR szConnStrIn[256] = _T("DSN=PrepExecSample");  
  
   r = SQLDriverConnect(hdbc, NULL, (SQLTCHAR *) szConnStrIn, SQL_NTS,
                          NULL, 0, NULL, SQL_DRIVER_NOPROMPT);
   if (r != SQL_SUCCESS && r != SQL_SUCCESS_WITH_INFO) {  
      ODBCError(henv, hdbc, NULL, NULL, true);  
      exit(-1);  
   }  
}  
  
void setup_ODBC_basics() {  
   SQLRETURN r;  
  
   r = SQLAllocHandle(SQL_HANDLE_STMT, hdbc, &hstmt);  
   if (r != SQL_SUCCESS && r != SQL_SUCCESS_WITH_INFO) {  
      ODBCError(henv, hdbc, hstmt, NULL, true);  
      exit(-1);  
   }  
}  
  
void OrdEntry(OrdEntryData& order) {  
   // Simple order entry  
   SQLRETURN r;  
  
   SQLINTEGER ItemNo, ProdCode, Qty;  
  
   // Bind parameters for the Order  
   // 1 - OrdNo input  
   r = SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT, SQL_C_LONG, SQL_INTEGER,
                          0, 0, &order.OrdNo, sizeof(SQLINTEGER), NULL);
   if (r != SQL_SUCCESS && r != SQL_SUCCESS_WITH_INFO) {  
      ODBCError(henv, hdbc, hstmt, NULL, true);   
      exit(-1);  
   }  
  
   // 2 - Custcode input  
   r = SQLBindParameter(hstmt, 2, SQL_PARAM_INPUT,SQL_C_TCHAR, SQL_VARCHAR, 5, 0,
                          &order.CustCode, sizeof(order.CustCode), NULL);
   if (r != SQL_SUCCESS && r != SQL_SUCCESS_WITH_INFO) {  
      ODBCError(henv, hdbc, hstmt, NULL, true);   
      exit(-1);  
   }  
  
   // Insert the order  
   r = SQLExecDirect(hstmt, (SQLTCHAR *) _T("{call OrderInsert(?, ?)}"),SQL_NTS);
   if (r != SQL_SUCCESS && r != SQL_SUCCESS_WITH_INFO) {  
      ODBCError(henv, hdbc, hstmt, NULL, true);   
      exit(-1);  
   }  
  
   // Flush results & reset hstmt  
   r = SQLMoreResults(hstmt);  
   if (r != SQL_NO_DATA) {  
      ODBCError(henv, hdbc, hstmt, NULL, true);   
      exit(-1);  
   }  
  
   r = SQLFreeStmt(hstmt, SQL_RESET_PARAMS);  
   if (r != SQL_SUCCESS && r != SQL_SUCCESS_WITH_INFO) {  
      ODBCError(henv, hdbc, hstmt, NULL, true);   
      exit(-1);  
   }  
  
   // Bind parameters for the Items  
   // 1 - OrdNo   
   r = SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT, SQL_C_LONG, SQL_INTEGER, 10, 0,
                          &order.OrdNo, sizeof(SQLINTEGER), NULL);  
   if (r != SQL_SUCCESS && r != SQL_SUCCESS_WITH_INFO) {  
      ODBCError(henv, hdbc, hstmt, NULL, true);   
      exit(-1);  
   }  
  
   // 2 - ItemNo   
   r = SQLBindParameter(hstmt, 2, SQL_PARAM_INPUT, SQL_C_LONG, SQL_INTEGER, 10, 0,
                          &ItemNo, sizeof(SQLINTEGER), NULL);  
   if (r != SQL_SUCCESS && r != SQL_SUCCESS_WITH_INFO) {  
      ODBCError(henv, hdbc, hstmt, NULL, true);   
      exit(-1);  
   }  
  
   // 3 - ProdCode  
   r = SQLBindParameter(hstmt, 3, SQL_PARAM_INPUT, SQL_C_LONG, SQL_INTEGER, 10, 0,
                          &ProdCode, sizeof(SQLINTEGER), NULL);  
   if (r != SQL_SUCCESS && r != SQL_SUCCESS_WITH_INFO) {  
      ODBCError(henv, hdbc, hstmt, NULL, true);   
      exit(-1);  
   }  
  
   // 4 - Qty  
   r = SQLBindParameter(hstmt, 4, SQL_PARAM_INPUT, SQL_C_LONG, SQL_INTEGER, 10, 0,
                          &Qty, sizeof(SQLINTEGER), NULL);  
   if (r != SQL_SUCCESS && r != SQL_SUCCESS_WITH_INFO) {  
      ODBCError(henv, hdbc, hstmt, NULL, true);   
      exit(-1);  
   }  
  
   // Prepare to insert items one at a time  
   r = SQLPrepare(hstmt, (SQLTCHAR *) _T("{call ItemInsert(?, ?, ?, ?)}"),SQL_NTS);
  
   for (unsigned int i = 0; i < order.ItemCount; i++) {  
  ItemNo = order.ItemNo[i];  
      ProdCode = order.ProdCode[i];  
      Qty = order.Qty[i];  
      r = SQLExecute(hstmt);  
      if (r != SQL_SUCCESS && r != SQL_SUCCESS_WITH_INFO) {  
         ODBCError(henv, hdbc, hstmt, NULL, true);   
         exit(-1);  
      }  
   }  
  
   // Flush results & reset hstmt  
   r = SQLMoreResults(hstmt);  
   if (r != SQL_NO_DATA) {  
      ODBCError(henv, hdbc, hstmt, NULL, true);   
      exit(-1);  
   }  
  
   r = SQLFreeStmt(hstmt, SQL_RESET_PARAMS);  
   if (r != SQL_SUCCESS && r != SQL_SUCCESS_WITH_INFO) {  
      ODBCError(henv, hdbc, hstmt, NULL, true);   
      exit(-1);  
   }  
  
   // Commit the transaction  
   r = SQLEndTran(SQL_HANDLE_DBC, hdbc, SQL_COMMIT);  
   if (r != SQL_SUCCESS && r != SQL_SUCCESS_WITH_INFO) {  
      ODBCError(henv, hdbc, hstmt, NULL, true);   
      exit(-1);  
   }  
}  
  
void testOrderEntry() {  
  
   OrdEntryData order;  
  
   order.OrdNo = 1;  
   _tcscpy_s((TCHAR *) order.CustCode, _countof(order.CustCode), _T("CUST1"));
   order.ItemNo[0] = 1;  
   order.ProdCode[0] = 10;  
   order.Qty[0] = 1;  
   order.ItemNo[1] = 2;  
   order.ProdCode[1] = 20;  
   order.Qty[1] = 2;  
   order.ItemNo[2] = 3;  
   order.ProdCode[2] = 30;  
   order.Qty[2] = 3;  
   order.ItemNo[3] = 4;  
   order.ProdCode[3] = 40;  
   order.Qty[3] = 4;  
   order.ItemCount = 4;  
  
   OrdEntry(order);  
}  
int _tmain() {  
   connect();  
   setup_ODBC_basics();  
  
   testOrderEntry();  
}  
```

## <a name="see-also"></a>Consulte también
[Procedimientos almacenados compilados de forma nativa](./a-guide-to-query-processing-for-memory-optimized-tables.md)