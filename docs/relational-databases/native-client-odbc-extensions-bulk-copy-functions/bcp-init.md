---
title: bcp_init | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apiname:
- bcp_init
- bcp_initW
apilocation:
- sqlncli11.dll
apitype: DLLExport
helpviewer_keywords:
- bcp_init function
ms.assetid: 6a25862c-7f31-4873-ab65-30f3abde89d2
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: d10c8d721b44fc372ee5a17a39c653797925dd46
ms.sourcegitcommit: 8732161f26a93de3aa1fb13495e8a6a71519c155
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2019
ms.locfileid: "71707560"
---
# <a name="bcp_init"></a>bcp_init
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

Inicializa la operación de copia masiva.  

## <a name="syntax"></a>Sintaxis  
  
```  
RETCODE bcp_init (  
        HDBC hdbc,  
        LPCTSTR szTable,  
        LPCTSTR szDataFile,  
        LPCTSTR szErrorFile,  
        INT eDirection);  
```  

Nombres Unicode y ANSI:
- bcp_initA (ANSI)
- bcp_initW (Unicode)

## <a name="arguments"></a>Argumentos  
 *hdbc*  
 Es el identificador de la conexión ODBC habilitada para la copia masiva.  
  
 *szTable*  
 Es el nombre de la tabla de base de datos en o de la que se va a copiar. Este nombre también puede incluir el nombre de la base de datos o el nombre del propietario. Por ejemplo, **pubs. Gracie. titles**, **pubs.. titles**, **Gracie. titles**y **titles** son nombres de tabla válidos.  
  
 Si *eDirection* es DB_OUT, *szTable* también puede ser el nombre de una vista de base de datos.  
  
 Si *eDirection* es DB_OUT y se especifica una instrucción SELECT con [bcp_control](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-control.md) antes de que se llame a [bcp_exec](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-exec.md) , **bcp_init** *szTable* debe establecerse en NULL.  
  
 *szDataFile*  
 Es el nombre del archivo de usuario en o del que se va a copiar. Si los datos se copian directamente de las variables mediante [bcp_sendrow](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-sendrow.md), establezca *szDataFile* en NULL.  
  
 *szErrorFile*  
 Es el nombre del archivo de error que se va a rellenar con mensajes de progreso, mensajes de error y copias de filas que, por cualquier razón, no se puedan copiar de un archivo de usuario en una tabla. Si se pasa NULL como *szErrorFile*, no se utiliza ningún archivo de error.  
  
 *eDirection*  
 Es la dirección de la copia, DB_IN o DB_OUT. DB_IN indica una copia de variables de programa o de un archivo de usuario en una tabla. DB_OUT indica una copia de una tabla de base de datos en un archivo de usuario. Se debe especificar un nombre de archivo de usuario con DB_OUT.  
  
## <a name="returns"></a>Devuelve  
 SUCCEED o FAIL.  
  
## <a name="remarks"></a>Comentarios  
 Llame a **bcp_init** antes de llamar a cualquier otra función de copia masiva. **bcp_init** realiza las inicializaciones necesarias para una copia masiva de datos entre la estación de trabajo y [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 La función **bcp_init** debe proporcionarse con un identificador de conexión ODBC habilitado para su uso con funciones de copia masiva. Para habilitar el identificador, use [SQLSetConnectAttr](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md) con SQL_COPT_SS_BCP establecido en SQL_BCP_ON en un identificador de conexión asignado, pero no conectado. Intentar asignar el atributo en un identificador conectado produce un error.  
  
 Cuando se especifica un archivo de datos, **bcp_init** examina la estructura de la tabla de origen o de destino de la base de datos, no el archivo de datos. **bcp_init** especifica los valores de formato de datos para el archivo de datos basándose en cada columna de la tabla, vista o conjunto de resultados de la base de datos. Esta especificación incluye el tipo de datos de cada columna, la presencia o ausencia de cadenas de bytes de un indicador de longitud o nulo y de terminador en los datos, y el ancho de los tipos de datos de longitud fija. **bcp_init** establece estos valores de la manera siguiente:  
  
-   El tipo de datos especificado es el tipo de datos de la columna de la tabla de base de datos, la vista o el conjunto de resultados de una instrucción SELECT. Los tipos de datos nativos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] especificados en sqlncli.h enumeran el tipo de datos. Los propios datos están representados en el formato del equipo. Es decir, los datos de una columna de tipo de datos **enteros** se representan mediante una secuencia de cuatro bytes que es grande o Little-Endian según el equipo que creó el archivo de datos.  
  
-   Si un tipo de datos de base de datos es de longitud fija, los datos del archivo de datos también serán de longitud fija. Las funciones de copia masiva que procesan los datos (por ejemplo, [bcp_exec](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-exec.md)) analizan las filas de datos que esperan que la longitud de los datos en el archivo de datos sea idéntica a la longitud de los datos especificados en la tabla de base de datos, la vista o la lista de columnas Select. Por ejemplo, los datos de una columna de base de datos definida como **Char (13)** deben estar representados por 13 caracteres para cada fila de datos del archivo. Los datos de longitud fija pueden tener como prefijo un indicador nulo si la columna de base de datos permite valores nulos.  
  
-   Cuando se define la secuencia de bytes del terminador, la longitud de dicha secuencia se establece en 0.  
  
-   Cuando se copia en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], el archivo de datos debe tener datos para cada columna de la tabla de base de datos. Cuando se copia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], los datos de todas las columnas de la tabla de base de datos, la vista o el conjunto de resultados de la instrucción SELECT se copian en el archivo de datos.  
  
-   Cuando se copia en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], la posición ordinal de una columna en el archivo de datos debe ser idéntica a la posición ordinal de la columna en la tabla de base de datos. Al copiar desde [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], **bcp_exec** coloca los datos basándose en la posición ordinal de la columna en la tabla de base de datos.  
  
-   Si un tipo de datos de la base de datos es de longitud variable (por ejemplo, **varbinary (22)** ) o si una columna de base de datos puede contener valores NULL, los datos del archivo de datos van precedidos por un indicador de longitud/nulo. El ancho del indicador varía en función del tipo de datos y de la versión de copia masiva.  
  
 Para cambiar los valores de formato de datos especificados para un archivo de datos, llame a [bcp_columns](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-columns.md) y [bcp_colfmt](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-colfmt.md).  
  
 Las copias masivas en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se pueden optimizar para tablas que no contienen índices estableciendo el modelo de recuperación de la base de datos en SIMPLE o BULK_LOGGED. Para obtener más información, consulte [requisitos previos para el registro mínimo en la importación en bloque](../../relational-databases/import-export/prerequisites-for-minimal-logging-in-bulk-import.md) y [ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql.md).  
  
 Si no se usa ningún archivo de datos, debe llamar a [bcp_bind](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-bind.md) para especificar el formato y la ubicación en memoria de los datos de cada columna y, a continuación, copiar las filas de datos en el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mediante [bcp_sendrow](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-sendrow.md).  
  
## <a name="example"></a>Ejemplo  
 En este ejemplo se muestra cómo se usa la función ODBC bcp_init con un archivo de formato.  
  
 Antes de compilar y ejecutar el código de C++, debe hacer lo siguiente:  
  
-   Crear un origen de datos ODBC denominado Test. Puede asociar este origen de datos a cualquier base de datos.  
  
-   Ejecutar la consulta siguiente [!INCLUDE[tsql](../../includes/tsql-md.md)] en la base de datos:  
  
    ```  
    CREATE TABLE BCPDate (cola int, colb datetime);  
    ```  
  
-   En el directorio donde ejecutará la aplicación, agregue un archivo con el nombre Bcpfmt.fmt y agregue esto al archivo:  
  
    ```  
    8.0  
    2  
    1SQLCHAR04"\t"1colaSQL_Latin1_General_Cp437_Bin  
    2SQLCHAR08"\r\n"2colbSQL_Latin1_General_Cp437_Bin  
    ```  
  
-   En el directorio donde ejecutará la aplicación, agregue un archivo con el nombre Bcpodbc.bcp y agregue esto al archivo:  
  
    ```  
    1  
    2  
    ```  
  
 Ahora puede compilar y ejecutar el código de C++.  
  
```  
// compile with: odbc32.lib sqlncli11.lib  
#include <stdio.h>  
#include <windows.h>  
#include <sql.h>  
#include <sqlext.h>  
#include <odbcss.h>  
  
SQLHENV henv = SQL_NULL_HENV;  
HDBC hdbc1 = SQL_NULL_HDBC;   
  
void Cleanup() {  
   if (hdbc1 != SQL_NULL_HDBC) {  
      SQLDisconnect(hdbc1);  
      SQLFreeHandle(SQL_HANDLE_DBC, hdbc1);  
   }  
  
   if (henv != SQL_NULL_HENV)  
      SQLFreeHandle(SQL_HANDLE_ENV, henv);  
}  
  
int main() {  
   RETCODE retcode;  
   SDWORD cRows;  
  
   // Allocate the ODBC environment and save handle.  
   retcode = SQLAllocHandle (SQL_HANDLE_ENV, NULL, &henv);  
   if ( (retcode != SQL_SUCCESS_WITH_INFO) && (retcode != SQL_SUCCESS)) {  
      printf("SQLAllocHandle(Env) Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Notify ODBC that this is an ODBC 3.0 app.  
   retcode = SQLSetEnvAttr(henv, SQL_ATTR_ODBC_VERSION, (SQLPOINTER) SQL_OV_ODBC3, SQL_IS_INTEGER);  
   if ( (retcode != SQL_SUCCESS_WITH_INFO) && (retcode != SQL_SUCCESS)) {  
      printf("SQLSetEnvAttr(ODBC version) Failed\n\n");  
      Cleanup();  
      return(9);      
   }  
  
   // Allocate ODBC connection handle, set BCP mode, and connect.  
   retcode = SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc1);  
   if ( (retcode != SQL_SUCCESS_WITH_INFO) && (retcode != SQL_SUCCESS)) {  
      printf("SQLAllocHandle(hdbc1) Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   retcode = SQLSetConnectAttr(hdbc1, SQL_COPT_SS_BCP, (void *)SQL_BCP_ON, SQL_IS_INTEGER);  
   if ( (retcode != SQL_SUCCESS_WITH_INFO) && (retcode != SQL_SUCCESS)) {  
      printf("SQLSetConnectAttr(hdbc1) Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Sample uses Integrated Security. Create SQL Server DSN using Windows NT authentication.  
   retcode = SQLConnect(hdbc1, (UCHAR*)"Test", SQL_NTS, (UCHAR*)"", SQL_NTS, (UCHAR*)"", SQL_NTS);  
   if ( (retcode != SQL_SUCCESS) && (retcode != SQL_SUCCESS_WITH_INFO) ) {  
      printf("SQLConnect() Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Initialize the bulk copy.  
   retcode = bcp_init(hdbc1, "BCPDate", "BCPODBC.bcp", NULL, DB_IN);  
   if ( (retcode != SUCCEED) ) {  
      printf("bcp_init(hdbc1) Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Read the format file.  
   retcode = bcp_readfmt(hdbc1, "BCPFMT.fmt");  
   if ( (retcode != SUCCEED) ) {  
      printf("bcp_readfmt(hdbc1) Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Execute the bulk copy.  
   retcode = bcp_exec(hdbc1, &cRows);  
   if ( (retcode != SUCCEED) ) {  
      printf("bcp_exec(hdbc1) Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   printf("Number of rows bulk copied in = %d.\n", cRows);  
  
   // Cleanup  
   SQLDisconnect(hdbc1);  
   SQLFreeHandle(SQL_HANDLE_DBC, hdbc1);  
   SQLFreeHandle(SQL_HANDLE_ENV, henv);  
}  
  
```  

## <a name="see-also"></a>Vea también  
 [Funciones de copia masiva](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
