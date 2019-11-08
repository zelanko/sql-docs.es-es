---
title: Asignar identificadores y conectarse a SQL Server (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- handles [ODBC]
- handles [ODBC], connection
- handles [ODBC], about handles
ms.assetid: 6172cd52-9c9a-467d-992f-def07f3f3bb1
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: ce294636c4d01a143b640126832bc6cca31ece14
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/07/2019
ms.locfileid: "73782069"
---
# <a name="allocate-handles-and-connect-to-sql-server-odbc"></a>Asignar identificadores y conectarse a SQL Server (ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

    
### <a name="to-allocate-handles-and-connect-to-sql-server"></a>Para asignar los identificadores y conectarse a SQL Server  
  
1.  Incluya los archivos de encabezado ODBC Sql.h, Sqlext.h, Sqltypes.h.  
  
2.  Incluya el archivo de encabezado específico del controlador [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], Odbcss.h.  
  
3.  Llame a [SQLAllocHandle](https://go.microsoft.com/fwlink/?LinkId=58396) con un **HandleType** de SQL_HANDLE_ENV para inicializar ODBC y asignar un identificador de entorno.  
  
4.  Llame a [SQLSetEnvAttr](../../relational-databases/native-client-odbc-api/sqlsetenvattr.md) con el **atributo** establecido en SQL_ATTR_ODBC_VERSION y **ValuePtr** establecido en SQL_OV_ODBC3 para indicar que la aplicación va a usar las llamadas de función de formato ODBC 3. x.  
  
5.  Opcionalmente, llame a [SQLSetEnvAttr](../../relational-databases/native-client-odbc-api/sqlsetenvattr.md) para establecer otras opciones de entorno, o llame a [SQLGetEnvAttr](https://go.microsoft.com/fwlink/?LinkId=58403) para obtener opciones de entorno.  
  
6.  Llame a [SQLAllocHandle](https://go.microsoft.com/fwlink/?LinkId=58396) con un **HandleType** de SQL_HANDLE_DBC para asignar un identificador de conexión.  
  
7.  Opcionalmente, llame a [SQLSetConnectAttr](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md) para establecer las opciones de conexión o llame a [SQLGetConnectAttr](../../relational-databases/native-client-odbc-api/sqlgetconnectattr.md) para obtener las opciones de conexión.  
  
8.  Llame a SQLConnect para usar un origen de datos existente con el fin de conectarse a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
     O bien  
  
     Llame a [SQLDriverConnect](../../relational-databases/native-client-odbc-api/sqldriverconnect.md) para usar una cadena de conexión para conectarse a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
     Una cadena de conexión [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] completa mínima tiene uno de dos formatos:  
  
    ```  
    DSN=dsn_name;Trusted_connection=yes;  
    DRIVER={SQL Server Native Client 10.0};SERVER=server;Trusted_connection=yes;  
    ```  
  
     Si la cadena de conexión no está completa, **SQLDriverConnect** puede solicitar la información necesaria. Esto se controla mediante el valor especificado para el parámetro *DriverCompletion* .  
  
     \- O bien  
  
     Llame a [SQLBrowseConnect](../../relational-databases/native-client-odbc-api/sqlbrowseconnect.md) varias veces de manera iterativa para compilar la cadena de conexión y conectarse a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
9. Opcionalmente, llame a [SQLGetInfo](../../relational-databases/native-client-odbc-api/sqlgetinfo.md) para obtener los atributos y el comportamiento del controlador para el origen de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
10. Asigne y utilice las instrucciones.  
  
11. Llame a SQLDisconnect para desconectarse de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y haga que el identificador de conexión esté disponible para una nueva conexión.  
  
12. Llame a [SQLFreeHandle](../../relational-databases/native-client-odbc-api/sqlfreehandle.md) con un **HandleType** de SQL_HANDLE_DBC para liberar el identificador de conexión.  
  
13. Llame a **SQLFreeHandle** con un **HandleType** de SQL_HANDLE_ENV para liberar el identificador del entorno.  
  
> [!IMPORTANT]  
>  Siempre que sea posible, utilice la autenticación de Windows. Si la autenticación de Windows no está disponible, solicite a los usuarios que escriban sus credenciales en tiempo de ejecución. No guarde las credenciales en un archivo. Si tiene que conservar las credenciales, debería cifrarlas con la [API de criptografía de Win32](https://go.microsoft.com/fwlink/?LinkId=64532).  
  
## <a name="example"></a>Ejemplo  
 En este ejemplo se muestra una llamada a **SQLDriverConnect** para conectarse a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sin necesidad de un origen de datos ODBC existente. Al pasar una cadena de conexión incompleta a **SQLDriverConnect**, hace que el controlador ODBC solicite al usuario que escriba la información que falta.  
  
```  
#define MAXBUFLEN   255  
  
SQLHENV      henv = SQL_NULL_HENV;  
SQLHDBC      hdbc1 = SQL_NULL_HDBC;  
SQLHSTMT      hstmt1 = SQL_NULL_HSTMT;  
  
SQLCHAR      ConnStrIn[MAXBUFLEN] =  
         "DRIVER={SQL Server Native Client 10.0};SERVER=MyServer";  
  
SQLCHAR      ConnStrOut[MAXBUFLEN];  
SQLSMALLINT   cbConnStrOut = 0;  
  
// Make connection without data source. Ask that driver   
// prompt if insufficient information. Driver returns  
// SQL_ERROR and application prompts user  
// for missing information. Window handle not needed for  
// SQL_DRIVER_NOPROMPT.  
retcode = SQLDriverConnect(hdbc1,      // Connection handle  
                  NULL,         // Window handle  
                  ConnStrIn,      // Input connect string  
                  SQL_NTS,         // Null-terminated string  
                  ConnStrOut,      // Address of output buffer  
                  MAXBUFLEN,      // Size of output buffer  
                  &cbConnStrOut,   // Address of output length  
                  SQL_DRIVER_PROMPT);  
```  
  
  
