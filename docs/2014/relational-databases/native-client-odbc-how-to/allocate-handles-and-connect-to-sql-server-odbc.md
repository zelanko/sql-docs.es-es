---
title: Asignar identificadores y conectarse a SQL Server (ODBC) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
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
manager: craigg
ms.openlocfilehash: 322120624c612371b56029c2cf29c9ab457c81b5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63225503"
---
# <a name="allocate-handles-and-connect-to-sql-server-odbc"></a>Asignar identificadores y conectarse a SQL Server (ODBC)
    
### <a name="to-allocate-handles-and-connect-to-sql-server"></a>Para asignar los identificadores y conectarse a SQL Server  
  
1.  Incluya los archivos de encabezado ODBC Sql.h, Sqlext.h, Sqltypes.h.  
  
2.  Incluya el archivo de encabezado específico del controlador [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], Odbcss.h.  
  
3.  Llame a [SQLAllocHandle](https://go.microsoft.com/fwlink/?LinkId=58396) con un `HandleType` de SQL_HANDLE_ENV para inicializar ODBC y asignar un identificador de entorno.  
  
4.  Llame a [SQLSetEnvAttr](../native-client-odbc-api/sqlsetenvattr.md) con `Attribute` establecido en SQL_ATTR_ODBC_VERSION y `ValuePtr` establecido en SQL_OV_ODBC3 para indicar que la aplicación utilizará llamadas a funciones ODBC 3.x con formato.  
  
5.  Opcionalmente, llame a [SQLSetEnvAttr](../native-client-odbc-api/sqlsetenvattr.md) para establecer otro entorno de opciones o llamada [SQLGetEnvAttr](https://go.microsoft.com/fwlink/?LinkId=58403) para obtener las opciones de entorno.  
  
6.  Llame a [SQLAllocHandle](https://go.microsoft.com/fwlink/?LinkId=58396) con un `HandleType` de SQL_HANDLE_DBC para asignar un identificador de conexión.  
  
7.  Opcionalmente, llame a [SQLSetConnectAttr](../native-client-odbc-api/sqlsetconnectattr.md) para establecer opciones de conexión o llamada [SQLGetConnectAttr](../native-client-odbc-api/sqlgetconnectattr.md) para obtener las opciones de conexión.  
  
8.  Llame a SQLConnect para usar un origen de datos existente para conectarse a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
     o bien  
  
     Llame a [SQLDriverConnect](../native-client-odbc-api/sqldriverconnect.md) para usar una cadena de conexión para conectarse a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
     Una cadena de conexión [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] completa mínima tiene uno de dos formatos:  
  
    ```  
    DSN=dsn_name;Trusted_connection=yes;  
    DRIVER={SQL Server Native Client 10.0};SERVER=server;Trusted_connection=yes;  
    ```  
  
     Si la cadena de conexión no se ha completado, `SQLDriverConnect` puede solicitar la información necesaria. Esto se controla mediante el valor especificado para el *DriverCompletion* parámetro.  
  
     \- o -  
  
     Llame a [SQLBrowseConnect](../native-client-odbc-api/sqlbrowseconnect.md) varias veces en un modo iterativo para generar la cadena de conexión y conectarse a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
9. Opcionalmente, llame a [SQLGetInfo](../native-client-odbc-api/sqlgetinfo.md) para obtener los atributos de controladores y el comportamiento de la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] origen de datos.  
  
10. Asigne y utilice las instrucciones.  
  
11. Llame a SQLDisconnect para desconectarse [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y realizar la conexión controlar disponibles para una conexión nueva.  
  
12. Llame a [SQLFreeHandle](../native-client-odbc-api/sqlfreehandle.md) con un `HandleType` de SQL_HANDLE_DBC para liberar el identificador de conexión.  
  
13. Llame a `SQLFreeHandle` con un `HandleType` de SQL_HANDLE_ENV para liberar el identificador del entorno.  
  
> [!IMPORTANT]  
>  Siempre que sea posible, utilice la autenticación de Windows. Si la autenticación de Windows no está disponible, solicite a los usuarios que escriban sus credenciales en tiempo de ejecución. No guarde las credenciales en un archivo. Si tiene que conservar las credenciales, debería cifrarlas con la [API de criptografía de Win32](https://go.microsoft.com/fwlink/?LinkId=64532).  
  
## <a name="example"></a>Ejemplo  
 En este ejemplo se muestra una llamada a `SQLDriverConnect` para conectarse a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sin necesidad de un origen de datos ODBC existente. El paso de una cadena de conexión incompleta a `SQLDriverConnect`, hace que el controlador ODBC solicite al usuario que escriba la información que falta.  
  
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
  
  
