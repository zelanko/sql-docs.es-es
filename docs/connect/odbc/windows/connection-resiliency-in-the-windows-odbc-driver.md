---
title: Resistencia de conexión en el controlador Windows ODBC
description: Obtenga información sobre cómo la resistencia de la conexión del controlador ODBC restaura de forma transparente las conexiones y mejora el comportamiento de la aplicación cuando el servidor cierra las conexiones inactivas.
ms.custom: ''
ms.date: 09/01/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 614fa0b4-e9fd-4c68-aab3-183f9b9df143
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 01b8da5d2a7f7c0e49d54a9fe237367ab3ed405f
ms.sourcegitcommit: b6ee0d434b3e42384b5d94f1585731fd7d0eff6f
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/02/2020
ms.locfileid: "89288127"
---
# <a name="connection-resiliency-in-the-windows-odbc-driver"></a>Resistencia de conexión en el controlador Windows ODBC
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

  Para asegurarse de que las aplicaciones permanezcan conectadas a una [!INCLUDE[ssAzure](../../../includes/ssazure_md.md)], el controlador ODBC en Windows puede restaurar las conexiones inactivas.  
  
> [!IMPORTANT]  
>  La característica de resistencia de conexión es compatible con las versiones de servidores de Microsoft Azure SQL Database y SQL Server 2014 y posteriores.  
  
 Para obtener más información sobre la resistencia de conexión inactiva, vea [el artículo técnico sobre esta característica](https://download.microsoft.com/download/D/2/0/D20E1C5F-72EA-4505-9F26-FEF9550EFD44/Idle%20Connection%20Resiliency.docx).
  
 Para controlar el comportamiento de reconexión, ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] en Windows, tiene dos opciones:  
  
-   Número de reintentos de conexión.  
  
     La opción de número de reintentos de conexión controla las veces que se realizan intentos de reconexión si se produce un error de conexión. Los valores válidos oscilan entre 0 y 255. Cero (0) significa que no se intentará realizar la reconexión. El valor predeterminado es un intento de reconexión.  
  
     Puede modificar el número de reintentos de conexión:  
  
    -   Cuando defina o modifique un origen de datos que utiliza ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] con el control de **número de reintentos de conexión**.  
  
    -   Cuando utilice la palabra clave de cadena de conexión **ConnectRetryCount** .  
  
     Para recuperar el número de reintentos de conexión, utilice el atributo de conexión **SQL_COPT_SS_CONNECT_RETRY_COUNT** (solo lectura). Si una aplicación se conecta a un servidor que no es compatible con la resistencia de conexión, **SQL_COPT_SS_CONNECT_RETRY_COUNT** devuelve 0.  
  
-   Intervalo de reintentos de conexión.  
  
     La opción de intervalo de reintentos de conexión especifica el número de segundos entre cada reintento de conexión. Los valores válidos oscilan entre 1 y 60. El tiempo total para volver a realizar la reconexión no puede superar el de espera de conexión (SQL_ATTR_QUERY_TIMEOUT en SQLSetStmtAttr). El valor predeterminado es 10 segundos.  
  
     Puede modificar el intervalo de reintentos de conexión:  
  
    -   Cuando defina o modifique un origen de datos que utiliza ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] con el control de **intervalo de reintentos de conexión**.  
  
    -   Cuando utilice la palabra clave de cadena de conexión **ConnectRetryInterval** .  
  
     Para recuperar la longitud del intervalo de reintentos de conexión, utilice el atributo de conexión **SQL_COPT_SS_CONNECT_RETRY_INTERVAL** (solo lectura).  
  
 Si una aplicación establece una conexión con SQL_DRIVER_COMPLETE_REQUIRED y después trata de ejecutar una instrucción en una conexión  interrumpida, el controlador ODBC no mostrará nuevamente el cuadro de diálogo. Además, durante la recuperación en curso:  
  
-   Durante la recuperación, las llamadas a **SQLGetConnectAttr(SQL_COPT_SS_CONNECTION_DEAD)**, deben devolver **SQL_CD_FALSE**.  
  
-   Si se produce un error de recuperación, las llamadas a **SQLGetConnectAttr(SQL_COPT_SS_CONNECTION_DEAD)**, deben devolver **SQL_CD_TRUE**.  
  
 Cualquier función que ejecuta un comando en el servidor devuelve los siguientes códigos de estado:  
  
|State|Mensaje|  
|-----------|-------------|  
|IMC01|La conexión se interrumpe y no es posible realizar la recuperación. El controlador cliente intentó recuperar el error una o más veces y todos los intentos fallaron. Aumente el valor de ConnectRetryCount para aumentar el número de intentos de recuperación.|  
|IMC02|El servidor no reconoció un intento de recuperación y no es posible recuperar la conexión.|  
|IMC03|El servidor no conservó la versión TDS exacta de cliente solicitada durante un intento de recuperación y no es posible recuperar la conexión.|  
|IMC04|El servidor no conservó la versión exacta de servidor solicitada durante un intento de recuperación y no es posible recuperar la conexión.|  
|IMC05|La conexión se interrumpe y no es posible realizar la recuperación. El servidor marca la conexión como irrecuperable. No se ha intentado restaurar la conexión.|  
|IMC06|La conexión se interrumpe y no es posible realizar la recuperación. El controlador cliente marca la conexión como irrecuperable. No se ha intentado restaurar la conexión.|  
  
## <a name="example"></a>Ejemplo  
 El siguiente ejemplo contiene dos funciones. **func1** muestra cómo puede conectarse con un nombre de origen de datos (DSN) que usa ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] en Windows. El DSN utiliza la autenticación de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] y especifica el id. de usuario. **func1** recupera entonces el número de reintentos de conexión con **SQL_COPT_SS_CONNECT_RETRY_COUNT**.  
  
 **func2** usa **SQLDriverConnect**, la palabra clave de conexión **ConnectRetryCount** y los atributos de conexión para recuperar la configuración de los reintentos de conexión y el intervalo de reintentos.  
  
```  
// Connection_resiliency.cpp  
// compile with: odbc32.lib  
#include <windows.h>  
#include <stdio.h>  
#include <sqlext.h>  
#include <msodbcsql.h>  
  
void func1() {  
   SQLHENV henv;  
   SQLHDBC hdbc;  
   SQLHSTMT hstmt;  
   SQLRETURN retcode;  
   SQLSMALLINT i = 21;  

   // Allocate environment handle  
   retcode = SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, &henv);  
  
   // Set the ODBC version environment attribute  
   if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
      retcode = SQLSetEnvAttr(henv, SQL_ATTR_ODBC_VERSION, (void*)SQL_OV_ODBC3, 0);   
  
      // Allocate connection handle  
      if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
         retcode = SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc);   
  
         // Set login timeout to 5 seconds  
         if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
            SQLSetConnectAttr(hdbc, SQL_LOGIN_TIMEOUT, (SQLPOINTER)5, 0);  
  
            // Connect to data source  
            retcode = SQLConnect(hdbc, (SQLCHAR*) "MyDSN", SQL_NTS, (SQLCHAR*) "userID", SQL_NTS, (SQLCHAR*) "password_for_userID", SQL_NTS);  
            retcode = SQLGetConnectAttr(hdbc, SQL_COPT_SS_CONNECT_RETRY_COUNT, &i, SQL_IS_INTEGER, NULL);  
  
            // Allocate statement handle  
            if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
               retcode = SQLAllocHandle(SQL_HANDLE_STMT, hdbc, &hstmt);   
  
               // Process data  
               if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
                  SQLFreeHandle(SQL_HANDLE_STMT, hstmt);  
               }  
  
               SQLDisconnect(hdbc);  
            }  
  
            SQLFreeHandle(SQL_HANDLE_DBC, hdbc);  
         }  
      }  
      SQLFreeHandle(SQL_HANDLE_ENV, henv);  
   }  
}
  
void func2() {  
   SQLHENV henv;  
   SQLHDBC hdbc1;  
   SQLHSTMT hstmt;  
   SQLRETURN retcode;  
   SQLSMALLINT i = 21;  
  
#define MAXBUFLEN 255  
  
   SQLCHAR ConnStrIn[MAXBUFLEN] = "DRIVER={ODBC Driver 17 for SQL Server};SERVER=server_that_supports_connection_resiliency;UID=userID;PWD= password_for_userID;ConnectRetryCount=2";
   SQLCHAR ConnStrOut[MAXBUFLEN];

   SQLSMALLINT cbConnStrOut = 0;  
 
   // Allocate environment handle  
   retcode = SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, &henv);  
  
   // Set the ODBC version environment attribute  
   if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
  
      retcode = SQLSetEnvAttr(henv, SQL_ATTR_ODBC_VERSION, (SQLPOINTER*)SQL_OV_ODBC3_80, SQL_IS_INTEGER);   
  
      // Allocate connection handle  
      if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
         retcode = SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc1);   
  
         // Set login timeout to 5 seconds  
         if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
            // SQLSetConnectAttr(hdbc1, SQL_LOGIN_TIMEOUT, (SQLPOINTER)5, 0);  
  
            retcode = SQLDriverConnect(hdbc1, NULL, ConnStrIn, SQL_NTS, NULL, 0, NULL, SQL_DRIVER_NOPROMPT);  
         }  
         retcode = SQLGetConnectAttr(hdbc1, SQL_COPT_SS_CONNECT_RETRY_COUNT, &i, SQL_IS_INTEGER, NULL);  
         retcode = SQLGetConnectAttr(hdbc1, SQL_COPT_SS_CONNECT_RETRY_INTERVAL, &i, SQL_IS_INTEGER, NULL);  
      }  
   }  
}  
  
int main() {  
   func1();  
   func2();  
}  
```  
  
## <a name="see-also"></a>Consulte también  
 [Microsoft ODBC Driver for SQL Server en Windows](../../../connect/odbc/windows/microsoft-odbc-driver-for-sql-server-on-windows.md)  
  
  
