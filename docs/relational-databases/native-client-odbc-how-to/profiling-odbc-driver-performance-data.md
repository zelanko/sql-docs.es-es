---
title: Datos de rendimiento del controlador de perfil (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- driver performance data [ODBC]
ms.assetid: b997790a-8cc6-4800-8867-74c1bef07be3
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: eab6ed2d2f02526d8167275b24800c267001b194
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.contentlocale: es-ES
ms.lasthandoff: 07/06/2020
ms.locfileid: "86001125"
---
# <a name="profiling-odbc-driver-performance-data"></a>Generar perfiles de datos de rendimiento del controlador ODBC
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  En este ejemplo se muestran las opciones específicas del controlador ODBC de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para registrar estadísticas de rendimiento. En el ejemplo se crea un archivo: odbcperf.log. En este ejemplo se muestra la creación de un registro de datos de rendimiento y se muestran estos datos directamente a partir de la estructura de datos SQLPERF (la estructura de datos SQLPERF se define en Odbcss.h). Este ejemplo se desarrolló para la versión 3.0 o posterior de ODBC.  
  
> [!IMPORTANT]  
>  Siempre que sea posible, utilice la autenticación de Windows. Si la autenticación de Windows no está disponible, solicite a los usuarios que escriban sus credenciales en tiempo de ejecución. No guarde las credenciales en un archivo. Si debe conservar las credenciales, debe cifrarlas con la [API Crypto de Win32](https://go.microsoft.com/fwlink/?LinkId=64532).  
  
### <a name="to-log-driver-performance-data-using-odbc-administrator"></a>Para registrar los datos de rendimiento del controlador mediante el Administrador ODBC  
  
1.  En el **Panel de control**, haga doble clic en **herramientas administrativas** y, a continuación, haga doble clic en **orígenes de datos (ODBC)**. De modo alternativo, puede invocar odbcad32.exe.  
  
2.  Haga clic en la pestaña **DSN de usuario**, **DSN de sistema**o DSN de **archivo** .  
  
3.  Haga clic en el origen de datos para el que desea registrar el rendimiento.  
  
4.  Haga clic en **Configurar**.  
  
5.  En el Asistente para configurar DSN de Microsoft SQL Server, vaya a la página con el **registro de estadísticas del controlador ODBC de registro en el archivo de registro**.  
  
6.  Seleccione **registrar estadísticas del controlador ODBC en el archivo de registro**. En el cuadro, incluya el nombre del archivo donde se deben registrar las estadísticas. Opcionalmente, haga clic en **examinar** para buscar el registro de estadísticas en el sistema de archivos.  
  
### <a name="to-log-driver-performance-data-programmatically"></a>Para registrar mediante programación los datos de rendimiento del controlador  
  
1.  Llame a [SQLSetConnectAttr](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md) con SQL_COPT_SS_PERF_DATA_LOG y la ruta de acceso completa y el nombre de archivo del archivo de registro de datos de rendimiento. Por ejemplo:  
  
    ```  
    "C:\\Odbcperf.log"  
    ```  
  
2.  Llame a [SQLSetConnectAttr](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md) con SQL_COPT_SS_PERF_DATA y SQL_PERF_START para iniciar el registro de datos de rendimiento.  
  
3.  Opcionalmente, llame a [SQLSetConnectAttr](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md) con SQL_COPT_SS_LOG_NOW y null para escribir un registro delimitado por tabuladores de datos de rendimiento en el archivo de registro de datos de rendimiento. Esto se puede hacer varias veces cuando se ejecuta la aplicación.  
  
4.  Llame a [SQLSetConnectAttr](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md) con SQL_COPT_SS_PERF_DATA y SQL_PERF_STOP para detener el registro de datos de rendimiento.  
  
### <a name="to-pull-driver-performance-data-into-an-application"></a>Para extraer los datos de rendimiento del controlador en una aplicación  
  
1.  Llame a [SQLSetConnectAttr](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md) con SQL_COPT_SS_PERF_DATA y SQL_PERF_START para iniciar la generación de perfiles de datos de rendimiento.  
  
2.  Llame a [SQLGetConnectAttr](../../relational-databases/native-client-odbc-api/sqlgetconnectattr.md) con SQL_COPT_SS_PERF_DATA y la dirección de un puntero a una estructura SQLPERF. La primera vez dicha llamada establece el puntero en la dirección de una estructura SQLPERF válida que contiene los datos de rendimiento actuales. El controlador no actualiza continuamente los datos de la estructura de rendimiento. La aplicación debe repetir la llamada a [SQLGetConnectAttr](../../relational-databases/native-client-odbc-api/sqlgetconnectattr.md) cada vez que necesite actualizar la estructura con datos de rendimiento más actuales.  
  
3.  Llame a [SQLSetConnectAttr](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md) con SQL_COPT_SS_PERF_DATA y SQL_PERF_STOP para detener el registro de datos de rendimiento.  
  
## <a name="example"></a>Ejemplo  
 Necesitará un origen de datos ODBC denominado AdventureWorks, cuya base de datos predeterminada sea la base de datos de ejemplo AdventureWorks. (Puede descargar la base de datos de ejemplo AdventureWorks de la Página principal de [ejemplos y proyectos](https://go.microsoft.com/fwlink/?LinkID=85384) de la comunidad de Microsoft SQL Server). Este origen de datos debe estar basado en el controlador ODBC proporcionado por el sistema operativo (el nombre del controlador es "SQL Server"). Si genera y ejecuta este ejemplo como una aplicación de 32 bits en un sistema operativo de 64 bits, debe crear el origen de datos ODBC con el Administrador ODBC en %windir%\SysWOW64\odbcad32.exe.  
  
 Este ejemplo se conecta a la instancia predeterminada de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] del equipo. Para conectarse a una instancia con nombre, cambie la definición del origen de datos ODBC para especificar la instancia utilizando el formato servidor\instanciaConNombre. De forma predeterminada, [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] se instala en una instancia con nombre.  
  
 Compilación con odbc32.lib.  
  
```  
// compile with: odbc32.lib  
#include <stdio.h>  
#include <string.h>  
#include <windows.h>  
#include <sql.h>  
#include <sqlext.h>  
#include <odbcss.h>  
  
SQLHENV henv = SQL_NULL_HENV;  
SQLHDBC hdbc1 = SQL_NULL_HDBC;       
SQLHSTMT hstmt1 = SQL_NULL_HSTMT;  
  
void Cleanup() {  
   if (hstmt1 != SQL_NULL_HSTMT)  
      SQLFreeHandle(SQL_HANDLE_STMT, hstmt1);  
  
   if (hdbc1 != SQL_NULL_HDBC) {  
      SQLDisconnect(hdbc1);  
      SQLFreeHandle(SQL_HANDLE_DBC, hdbc1);  
   }  
  
   if (henv != SQL_NULL_HENV)  
      SQLFreeHandle(SQL_HANDLE_ENV, henv);  
}  
  
int main() {  
   RETCODE retcode;  
  
   // Pointer to the ODBC driver performance structure.  
   SQLPERF *PerfPtr;  
   SQLINTEGER cbPerfPtr;  
  
   // Allocate the ODBC environment and save handle.  
   retcode = SQLAllocHandle (SQL_HANDLE_ENV, NULL, &henv);  
   if( (retcode != SQL_SUCCESS_WITH_INFO) && (retcode != SQL_SUCCESS)) {  
      printf("SQLAllocHandle(Env) Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Notify ODBC that this is an ODBC 3.0 app.  
   retcode = SQLSetEnvAttr(henv, SQL_ATTR_ODBC_VERSION, (SQLPOINTER) SQL_OV_ODBC3, SQL_IS_INTEGER);  
   if( (retcode != SQL_SUCCESS_WITH_INFO) && (retcode != SQL_SUCCESS)) {  
      printf("SQLSetEnvAttr(ODBC version) Failed\n\n");  
      Cleanup();  
      return(9);      
   }  
  
   // Allocate ODBC connection handle and connect.  
   retcode = SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc1);  
   if( (retcode != SQL_SUCCESS_WITH_INFO) && (retcode != SQL_SUCCESS)) {  
      printf("SQLAllocHandle(hdbc1) Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // This sample use Integrated Security. Please create the SQL Server   
   // DSN by using the Windows NT authentication.   
   retcode = SQLConnect(hdbc1, (UCHAR*)"AdventureWorks", SQL_NTS, (UCHAR*)"", SQL_NTS, (UCHAR*)"", SQL_NTS);  
   if( (retcode != SQL_SUCCESS) && (retcode != SQL_SUCCESS_WITH_INFO) ) {  
      printf("SQLConnect() Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Set options to log performance statistics.  Specify file to use for the log.  
   retcode = SQLSetConnectAttr( hdbc1, SQL_COPT_SS_PERF_DATA_LOG, &"odbcperf.log", SQL_NTS);  
   if( (retcode != SQL_SUCCESS) && (retcode != SQL_SUCCESS_WITH_INFO) ) {  
      printf("SQLSetConnectAttr() Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Start the performance statistics log.  
   retcode =   
      SQLSetConnectAttr( hdbc1, SQL_COPT_SS_PERF_DATA, (SQLPOINTER)SQL_PERF_START, SQL_IS_UINTEGER);  
   if( (retcode != SQL_SUCCESS) && (retcode != SQL_SUCCESS_WITH_INFO) ) {  
      printf("SQLSetConnectAttr() Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Allocate statement handle, then execute command.  
   retcode = SQLAllocHandle(SQL_HANDLE_STMT, hdbc1, &hstmt1);  
   if( (retcode != SQL_SUCCESS) && (retcode != SQL_SUCCESS_WITH_INFO) ) {  
      printf("SQLAllocHandle() Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   retcode = SQLExecDirect(hstmt1, (UCHAR*)"SELECT * FROM Purchasing.Vendor", SQL_NTS);  
   if( (retcode != SQL_SUCCESS) && (retcode != SQL_SUCCESS_WITH_INFO) ) {  
      printf("SQLExecDirect() Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Clear any result sets generated.  
   while ( ( retcode = SQLMoreResults(hstmt1) ) != SQL_NO_DATA ) {  
      if( (retcode != SQL_SUCCESS) && (retcode != SQL_SUCCESS_WITH_INFO) ) {  
         printf("SQLMoreResults() Failed\n\n");  
         Cleanup();  
         return(9);  
      }  
   }  
  
   retcode = SQLExecDirect(hstmt1, (UCHAR*)"SELECT * FROM Sales.Store", SQL_NTS);  
   if( (retcode != SQL_SUCCESS) && (retcode != SQL_SUCCESS_WITH_INFO) ) {  
      printf("SQLExecDirect() Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Clear any result sets generated.  
   while ( ( retcode = SQLMoreResults(hstmt1) ) != SQL_NO_DATA ) {  
      if( (retcode != SQL_SUCCESS) && (retcode != SQL_SUCCESS_WITH_INFO) ) {  
         printf("SQLMoreResults() Failed\n\n");  
         Cleanup();  
         return(9);  
      }  
   }  
  
   // Generate a long-running query.  
   retcode = SQLExecDirect(hstmt1, (UCHAR*)"waitfor delay '00:00:04' ", SQL_NTS);  
   if( (retcode != SQL_SUCCESS) && (retcode != SQL_SUCCESS_WITH_INFO) ) {  
      printf("SQLExecDirect() Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Clear any result sets generated.  
   while ( ( retcode = SQLMoreResults(hstmt1) ) != SQL_NO_DATA ) {  
      if( (retcode != SQL_SUCCESS) && (retcode != SQL_SUCCESS_WITH_INFO) ) {  
         printf("SQLMoreResults() Failed\n\n");  
         Cleanup();  
         return(9);  
      }  
   }  
  
   // Write current statistics to the performance log.  
   retcode =   
      SQLSetConnectAttr( hdbc1, SQL_COPT_SS_PERF_DATA_LOG_NOW, (SQLPOINTER)NULL, SQL_IS_UINTEGER);  
   if( (retcode != SQL_SUCCESS) && (retcode != SQL_SUCCESS_WITH_INFO) ) {  
      printf("SQLSetConnectAttr() Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Get pointer to current SQLPerf structure.  
   // Print a couple of statistics.  
   retcode =   
      SQLGetConnectAttr( hdbc1, SQL_COPT_SS_PERF_DATA, (SQLPOINTER)&PerfPtr, SQL_IS_POINTER, &cbPerfPtr);  
   if( (retcode != SQL_SUCCESS) && (retcode != SQL_SUCCESS_WITH_INFO) ) {  
      printf("SQLGetConnectAttr() Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   printf("SQLSelects = %d, SQLSelectRows = %d\n", PerfPtr->SQLSelects, PerfPtr->SQLSelectRows);  
  
   // Cleanup  
   SQLFreeHandle(SQL_HANDLE_STMT, hstmt1);  
   SQLDisconnect(hdbc1);  
   SQLFreeHandle(SQL_HANDLE_DBC, hdbc1);  
   SQLFreeHandle(SQL_HANDLE_ENV, henv);  
}  
```  
  
## <a name="see-also"></a>Consulte también  
 [Temas de procedimientos de generación de perfiles de rendimiento del controlador ODBC &#40;ODBC&#41;](../../relational-databases/native-client-odbc-how-to/profiling-odbc-driver-performance-odbc.md)   
 [Generar perfiles del rendimiento del controlador ODBC](../../relational-databases/native-client/odbc/profiling-odbc-driver-performance.md)  
  
  
