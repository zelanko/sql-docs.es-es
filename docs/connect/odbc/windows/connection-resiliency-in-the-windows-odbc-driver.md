---
title: Resistencia de conexión en el controlador ODBC de Windows | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 614fa0b4-e9fd-4c68-aab3-183f9b9df143
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e2b27a848773b09d651d748bd321ace69ab2a6b4
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "32852870"
---
# <a name="connection-resiliency-in-the-windows-odbc-driver"></a>Resistencia de conexión en el controlador Windows ODBC
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

  Para asegurarse de que las aplicaciones permanezcan conectadas a un [!INCLUDE[ssAzure](../../../includes/ssazure_md.md)], el controlador ODBC en Windows puede restaurar conexiones inactivas.  
  
> [!IMPORTANT]  
>  La característica de resistencia de conexión es compatible con versiones de bases de datos SQL de Microsoft Azure y SQL Server 2014 (y posterior).  
  
 Para obtener información adicional sobre la resistencia de conexión inactiva, consulte [artículo técnico – resistencia de conexión inactiva](http://go.microsoft.com/fwlink/?LinkId=393996).  
  
 Para controlar el comportamiento de reconexión, ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] en Windows, tiene dos opciones:  
  
-   Número de reintentos de conexión.  
  
     La opción de número de reintentos de conexión controla las veces que se realizan intentos de reconexión si se produce un error de conexión. Los valores válidos oscilan entre 0 y 255. Cero (0) significa que no se intentará realizar la reconexión. El valor predeterminado es un intento de reconexión.  
  
     Puede modificar el número de reintentos de conexión:  
  
    -   Cuando defina o modifique un origen de datos que utiliza ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] con el control de **número de reintentos de conexión** .  
  
    -   Cuando utilice la palabra clave de cadena de conexión **ConnectRetryCount** .  
  
     Para recuperar el número de reintentos de conexión, utilice la **SQL_COPT_SS_CONNECT_RETRY_COUNT** (solo lectura) atributo de conexión. Si una aplicación se conecta a un servidor que no es compatible con la resistencia de conexión, **SQL_COPT_SS_CONNECT_RETRY_COUNT** devuelve 0.  
  
-   Intervalo de reintentos de conexión.  
  
     La opción de intervalo de reintentos de conexión especifica el número de segundos entre cada reintento de conexión. Los valores válidos oscilan entre 1 y 60. El tiempo total para volver a realizar la reconexión no puede superar el de espera de conexión (SQL_ATTR_QUERY_TIMEOUT en SQLSetStmtAttr). El valor predeterminado es 10 segundos.  
  
     Puede modificar el intervalo de reintentos de conexión:  
  
    -   Cuando defina o modifique un origen de datos que utiliza ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] con el control de **intervalo de reintentos de conexión** .  
  
    -   Cuando utilice la palabra clave de cadena de conexión **ConnectRetryInterval** .  
  
     Para recuperar la longitud del intervalo de reintento de conexión, utilice la **SQL_COPT_SS_CONNECT_RETRY_INTERVAL** (solo lectura) atributo de conexión.  
  
 Si una aplicación establece una conexión con SQL_DRIVER_COMPLETE_REQUIRED y después trata de ejecutar una instrucción en una conexión  interrumpida, el controlador ODBC no mostrará nuevamente el cuadro de diálogo. Además, durante la recuperación en curso:  
  
-   Durante la recuperación, todas las llamadas a **SQLGetConnectAttr (sql_copt_ss_connection_dead)**, debe devolver **SQL_CD_FALSE**.  
  
-   Si se producen errores recuperación, las llamadas a **SQLGetConnectAttr (sql_copt_ss_connection_dead)**, debe devolver **SQL_CD_TRUE**.  
  
 Cualquier función que ejecuta un comando en el servidor devuelve los siguientes códigos de estado:  
  
|State|de mensaje|  
|-----------|-------------|  
|IMC01|La conexión se interrumpe y no es posible realizar la recuperación. El controlador cliente intentó recuperar el error una o más veces y todos los intentos fallaron. Aumente el valor de ConnectRetryCount para aumentar el número de intentos de recuperación.|  
|IMC02|El servidor no reconoció un intento de recuperación y no es posible recuperar la conexión.|  
|IMC03|El servidor no conservó la versión TDS exacta de cliente solicitada durante un intento de recuperación y no es posible recuperar la conexión.|  
|IMC04|El servidor no conservó la versión exacta de servidor solicitada durante un intento de recuperación y no es posible recuperar la conexión.|  
|IMC05|La conexión se interrumpe y no es posible realizar la recuperación. El servidor marca la conexión como irrecuperable. No se ha intentado restaurar la conexión.|  
|IMC06|La conexión se interrumpe y no es posible realizar la recuperación. El controlador cliente marca la conexión como irrecuperable. No se ha intentado restaurar la conexión.|  
  
## <a name="example"></a>Ejemplo  
 El siguiente ejemplo contiene dos funciones. **func1** muestra cómo puede conectarse con un nombre de origen de datos (DSN) que utiliza ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] en Windows. El DSN utiliza la autenticación de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] y especifica el id. de usuario. **func1** , a continuación, recupera el número de reintentos de conexión con **SQL_COPT_SS_CONNECT_RETRY_COUNT**.  
  
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
  
   SQLCHAR ConnStrIn[MAXBUFLEN] = "DRIVER={ODBC Driver 13 for SQL Server};SERVER=server_that_supports_connection_resiliency;UID=userID;PWD= password_for_userID;ConnectRetryCount=2";
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
  
## <a name="see-also"></a>Vea también  
 [Microsoft ODBC Driver for SQL Server en Windows](../../../connect/odbc/windows/microsoft-odbc-driver-for-sql-server-on-windows.md)  
  
  
