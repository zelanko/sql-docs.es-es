---
title: Función SQLPutData | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLPutData
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLPutData
helpviewer_keywords:
- SQLPutData function [ODBC]
ms.assetid: 9a60f004-1477-4c54-a20c-7378e1116713
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5254b7bb3744e06dae300f33ff1b612b4aca2341
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "65537266"
---
# <a name="sqlputdata-function"></a>Función SQLPutData
**Conformidad**  
 Versión de introducción: Cumplimiento de estándares 1.0 de ODBC: ISO 92  
  
 **Resumen**  
 **SQLPutData** permite que una aplicación enviar datos de un parámetro o columna a del controlador en el tiempo de ejecución de la instrucción. Esta función puede utilizarse para enviar los valores de caracteres o datos binarios en partes a una columna con un tipo de datos específicos del origen de carácter, binario o datos (por ejemplo, los parámetros de los tipos de SQL_LONGVARBINARY y SQL_LONGVARCHAR). **SQLPutData** admite el enlace a un tipo de datos Unicode C, incluso si el controlador subyacente no admite datos Unicode.  
  
## <a name="syntax"></a>Sintaxis  
  
```cpp  
  
SQLRETURN SQLPutData(  
      SQLHSTMT     StatementHandle,  
      SQLPOINTER   DataPtr,  
      SQLLEN       StrLen_or_Ind);  
```  
  
## <a name="arguments"></a>Argumentos  
 *StatementHandle*  
 [Entrada] Identificador de instrucción.  
  
 *DataPtr*  
 [Entrada] Puntero a un búfer que contiene los datos reales para el parámetro o columna. Los datos deben estar en el tipo de datos C especificado en el *ValueType* argumento de **SQLBindParameter** (para datos de parámetro) o el *TargetType* argumento de  **SQLBindCol** (para datos de columna).  
  
 *StrLen_or_Ind*  
 [Entrada] Longitud de \* *DataPtr*. Especifica la cantidad de datos que se envían en una llamada a **SQLPutData**. La cantidad de datos puede variar con cada llamada para una columna o parámetro dado. *StrLen_or_Ind* se omite a menos que cumpla una de las condiciones siguientes:  
  
-   *StrLen_or_Ind* es SQL_NTS, SQL_NULL_DATA o SQL_DEFAULT_PARAM.  
  
-   El tipo de datos C especificado en **SQLBindParameter** o **SQLBindCol** es SQL_C_CHAR o SQL_C_BINARY.  
  
-   El tipo de datos C es SQL_C_DEFAULT, y el tipo de datos C predeterminado para el tipo de datos SQL especificado es SQL_C_CHAR o SQL_C_BINARY.  
  
 Para los demás tipos de datos de C, si *StrLen_or_Ind* no es SQL_NULL_DATA o SQL_DEFAULT_PARAM, el controlador se da por supuesto que el tamaño de la \* *DataPtr* búfer es el tamaño del tipo de datos C especificado con *ValueType* o *TargetType* y envía el valor de datos completo. Para obtener más información, consulte [convertir datos de C a tipos de datos SQL](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md) en el apéndice D: Tipos de datos.  
  
## <a name="returns"></a>Devuelve  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_STILL_EXECUTING, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Cuando **SQLPutData** devuelve SQL_ERROR o SQL_SUCCESS_WITH_INFO, un valor SQLSTATE asociado se puede obtener mediante una llamada a **SQLGetDiagRec** con un *HandleType* de SQL_ HANDLE_STMT y un *controlar* de *StatementHandle*. En la tabla siguiente se enumera los valores SQLSTATE devueltos normalmente por **SQLPutData** y se explica cada uno de ellos en el contexto de esta función; la notación "(DM)" precede a las descripciones de SQLSTATE devuelto por el Administrador de controladores. El código de retorno asociado a cada valor SQLSTATE es SQL_ERROR, a menos que se indique lo contrario.  
  
|SQLSTATE|Error|Descripción|  
|--------------|-----------|-----------------|  
|01000|Advertencia general|Específico del controlador de mensaje informativo. (La función devuelve SQL_SUCCESS_WITH_INFO).|  
|01004|Datos de cadena derecha truncados|Cadena o datos binarios devueltos para un parámetro de salida como resultado el truncamiento de carácter no en blanco o datos binarios que no son NULL. Si fuese un valor de cadena, era truncado a la derecha. (La función devuelve SQL_SUCCESS_WITH_INFO).|  
|07006|Infracción del atributo de tipo de datos restringido|El valor de datos identificado por el *ValueType* argumento en **SQLBindParameter** para el parámetro dependiente no se pudo convertir al tipo de datos identificado por el *ParameterType*argumento en **SQLBindParameter**.|  
|07S01|Uso no válido de parámetro predeterminado|Establece un valor de parámetro, con **SQLBindParameter**, era SQL_DEFAULT_PARAM y el parámetro correspondiente no tiene un valor predeterminado.|  
|08S01|Error de vínculo de comunicación|Error en el vínculo de comunicación entre el controlador y el origen de datos a la que se ha conectado el controlador antes del procesamiento de la función se ha completado.|  
|22001|Cadena de datos, truncamiento por la derecha|La asignación de un carácter o un valor binario a una columna producía el truncamiento de no están en blanco (carácter) o distinto de null (binarios) caracteres o bytes.<br /><br /> El tipo de información SQL_NEED_LONG_DATA_LEN **SQLGetInfo** era "S" y se ha enviado más datos para un parámetro largo (el tipo de datos era un tipo de datos específicos del origen de datos long, SQL_LONGVARBINARY o SQL_LONGVARCHAR) que se ha especificado con el *StrLen_or_IndPtr* argumento en **SQLBindParameter**.<br /><br /> El tipo de información SQL_NEED_LONG_DATA_LEN **SQLGetInfo** era "S" y se ha enviado más datos para una columna long (el tipo de datos era un tipo de datos específicos del origen de datos long, SQL_LONGVARBINARY o SQL_LONGVARCHAR) que se especificó en el búfer de longitud correspondiente a una columna en una fila de datos que se ha agregado o actualizado con **SQLBulkOperations** o actualizados con **SQLSetPos**.|  
|22003|Valor numérico fuera del intervalo|Los datos enviaron para un parámetro numérico enlazado o columna provocó la parte entera (en contraposición a fraccionarios) el número que se truncan cuando se asigna a la columna de tabla asociada.<br /><br /> Devuelve un valor numérico (como numérico o cadena) para uno o más parámetros de entrada y salida o de salida habría causado la parte entera (en contraposición a fraccionarios) del número que se va a truncar.|  
|22007|Formato de datetime no válido|Los datos enviados para un parámetro o columna que estaba enlazada a una fecha, hora o estructura de marca de tiempo eran, respectivamente, una fecha no válida, la hora o marca de tiempo.<br /><br /> Un parámetro de entrada y salida o de salida estaba enlazado a una fecha, hora o estructura de marca de tiempo C, y un valor en el parámetro devuelto era, respectivamente, una fecha no válida, la hora o marca de tiempo. (La función devuelve SQL_SUCCESS_WITH_INFO).|  
|22008|Desbordamiento del campo DateTime|Calcula una expresión de fecha y hora para una entrada y salida o parámetro de salida dieron lugar a una fecha, hora o estructura de C de la marca de tiempo que no era válido.|  
|22012|División por cero|Una expresión aritmética calculado para una entrada y salida o parámetro de salida dio como resultado de división por cero.|  
|22015|Desbordamiento de campo de intervalo|Los datos se envían de una columna numérica o de intervalo exacta o parámetro a un tipo de datos SQL de intervalo causó una pérdida de dígitos significativos.<br /><br /> Datos se enviaron para un parámetro con más de un campo o columna de intervalo, se convierten en un tipo de datos numéricos y no tenían ninguna representación en el tipo de datos numérico.<br /><br /> Los datos enviados para la columna o los datos de parámetro que se asignó a un intervalo de tipo SQL y no había ninguna representación del valor del tipo C en el intervalo de tipo SQL.<br /><br /> Los datos enviados para un valor numérico exacto o intervalo C columna o del parámetro a un tipo de intervalo C causó una pérdida de dígitos significativos.<br /><br /> Los datos enviados para la columna o los datos de parámetro que se asignó a una estructura de intervalo de C y no había ninguna representación de los datos de la estructura de datos de intervalo.|  
|22018|Valor de carácter no válido para especificación cast|El tipo C era un numérico exacto o aproximado, una fecha y hora o un tipo de datos del intervalo; el tipo SQL de la columna era un tipo de datos de caracteres; y el valor en la columna o parámetro no era un literal válido de tipo C enlazado.<br /><br /> El tipo SQL era un numérico exacto o aproximado, una fecha y hora o un tipo de datos del intervalo; el tipo de C era SQL_C_CHAR; y el valor en la columna o parámetro no era un literal válido del tipo SQL enlazado.|  
|HY000|Error general|Se produjo un error para que se ha producido ningún SQLSTATE específico y para los que se ha definido ningún SQLSTATE específicos de la implementación. El mensaje de error devuelto por **SQLGetDiagRec** en el  *\*MessageText* búfer describe el error y su causa.|  
|HY001|Error de asignación de memoria|El controlador no pudo asignar la memoria necesaria para admitir la ejecución o la finalización de la función.|  
|HY008|Operación cancelada|Procesamiento asincrónico se habilitó para la *StatementHandle*. Se llamó a la función, y antes que completó la ejecución, **SQLCancel** o **SQLCancelHandle** se ha llamado en el *StatementHandle*. A continuación, la función se llamó de nuevo en el *StatementHandle*.<br /><br /> Se llamó a la función, y antes que completó la ejecución, **SQLCancel** o **SQLCancelHandle** se ha llamado en el *StatementHandle* desde un subproceso diferente en un aplicaciones multiproceso.|  
|HY009|Uso no válido del puntero nulo|(DM) el argumento *DataPtr* era un puntero nulo y el argumento *StrLen_or_Ind* no era 0, SQL_DEFAULT_PARAM o SQL_NULL_DATA.|  
|HY010|Error de secuencia de función|(DM) la llamada de función anterior no era una llamada a **SQLPutData** o **SQLParamData**.<br /><br /> (DM) se llamó a una función que se ejecuta de forma asincrónica para el identificador de conexión que está asociado el *StatementHandle*. Esta función asincrónica todavía se estaba ejecutando cuando se llamó a la función SQLPutData.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, o **SQLMoreResults** se llamó para el *StatementHandle* y devuelven SQL_PARAM_DATA_ ESTÁ DISPONIBLE. Esta función se invoca antes de que se recuperan los datos para todos los parámetros transmitidos.<br /><br /> (DM) se llamó a una función que se ejecuta asincrónicamente (no ésta) para el *StatementHandle* y aún se estaba ejecutando cuando se llamó a esta función.|  
|HY013|Error de administración de memoria|No se pudo procesar la llamada de función porque los objetos de memoria subyacente no se podrían tener acceso, posiblemente debido a memoria insuficiente.|  
|HY019|Datos no binarios ni de caracteres que se enviaron por partes|**SQLPutData** fue llamado más de una vez para un parámetro o columna, y no se usaba para enviar datos de caracteres de C a una columna con un tipo de carácter, binario o datos específicos del origen de datos o para enviar datos binarios de C a una columna con un carácter , binario o tipo de datos específicos del origen de datos.|  
|HY020|Intento de concatenar un valor null|**SQLPutData** se llamó a más de una vez desde la llamada que devuelve SQL_NEED_DATA y en una de esas llamadas, el *StrLen_or_Ind* argumento contenidos SQL_NULL_DATA o SQL_DEFAULT_PARAM.|  
|HY090|Longitud de búfer o cadena no válida|El argumento *DataPtr* no era un puntero nulo y el argumento *StrLen_or_Ind* era menor que 0 pero no es igual a SQL_NTS o SQL_NULL_DATA.|  
|HY117|Conexión está suspendida debido al estado de transacción desconocido. Solo se desconecte y se permiten funciones de solo lectura.|(DM) para obtener más información sobre el estado suspendido, consulte [función SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYT01|Tiempo de espera de conexión agotado|Ha expirado el período de tiempo de espera de conexión antes de que el origen de datos que respondió a la solicitud. El período de tiempo de espera de conexión se establece a través de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Controlador no admite esta función|(DM) el controlador asociado con el *StatementHandle* no admite la función.|  
|IM017|Sondeo se deshabilita en modo de notificación asincrónica|Cada vez que se usa el modelo de notificación, se deshabilita el sondeo.|  
|IM018|**SQLCompleteAsync** no se ha llamado para completar la operación asincrónica anterior en este identificador.|Si la llamada de función anterior en el controlador devuelve SQL_STILL_EXECUTING y si está habilitado el modo de notificación, **SQLCompleteAsync** debe llamarse en el identificador para realizar el procesamiento posterior y completar la operación.|  
  
 Si **SQLPutData** se llama durante el envío de datos para un parámetro en una instrucción SQL, puede devolver cualquier SQLSTATE que puede ser devueltos por la función se llama para ejecutar la instrucción (**SQLExecute** o **SQLExecDirect**). Si se llama durante el envío de datos para una columna que se va a actualizar o agregar con **SQLBulkOperations** o se actualiza con **SQLSetPos**, puede devolver cualquier SQLSTATE, que puede devolver  **SQLBulkOperations** o **SQLSetPos**.  
  
## <a name="comments"></a>Comentarios  
 **SQLPutData** puede llamarse para suministrar datos a datos en ejecución para los dos usos: datos de parámetro que se utilizarán en una llamada a **SQLExecute** o **SQLExecDirect**, o datos de la columna que se usará cuando se actualiza una fila o agregar mediante una llamada a **SQLBulkOperations** o se actualiza mediante una llamada a **SQLSetPos**.  
  
 Cuando una aplicación llama **SQLParamData** para determinar qué datos se deben enviar, el controlador devuelve un indicador de que la aplicación puede usar para determinar los datos de parámetro para enviar o donde se pueden encontrar los datos de la columna. También devuelve SQL_NEED_DATA, que es un indicador para la aplicación que debe llamar a **SQLPutData** para enviar los datos. En el *DataPtr* argumento **SQLPutData**, la aplicación pasa un puntero al búfer que contiene los datos reales para el parámetro o columna.  
  
 Cuando el controlador devuelve SQL_SUCCESS para **SQLPutData**, la aplicación llama a **SQLParamData** nuevo. **SQLParamData** devuelve SQL_NEED_DATA si necesitan más datos enviar, en el que la aplicación llama a caso **SQLPutData** nuevo. Devuelve SQL_SUCCESS tanto si se han enviado datos de todos los datos en ejecución. La aplicación, a continuación, llama a **SQLParamData** nuevo. Si el controlador devuelve SQL_NEED_DATA y otro indicador en  *\*ValuePtrPtr*, requiere que los datos para otra columna o parámetro y **SQLPutData** se llama de nuevo. Si el controlador devuelve SQL_SUCCESS, a continuación, todos los datos en ejecución se han enviado datos y se puede ejecutar la instrucción SQL o el **SQLBulkOperations** o **SQLSetPos** se puede procesar la llamada.  
  
 Para obtener más información sobre los datos del parámetro cómo datos en ejecución se pasa en tiempo de ejecución de la instrucción, vea "Pasar valores de parámetro" en [SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md) y [enviar datos largos](../../../odbc/reference/develop-app/sending-long-data.md). Para obtener más información sobre los datos de columna de la forma de datos en ejecución se actualiza o agrega, vea la sección "Uso SQLSetPos" en [SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md), "Realizar masiva actualizaciones utilizando marcadores" [SQLBulkOperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md), y [Datos de tipo long y SQLSetPos y SQLBulkOperations](../../../odbc/reference/develop-app/long-data-and-sqlsetpos-and-sqlbulkoperations.md).  
  
> [!NOTE]  
>  Puede usar una aplicación **SQLPutData** para enviar datos de componentes solo cuando se envían datos de carácter C a una columna con un tipo de carácter, binario o datos específicos del origen de datos o al enviar datos binarios de C a una columna con un carácter, binario, o datos tipo de datos específico del origen. Si **SQLPutData** se llama varias veces en cualquier otra condición, devuelve SQL_ERROR y SQLSTATE HY019 (datos no binarios ni de caracteres, se han enviado partes).  
  
## <a name="example"></a>Ejemplo  
 El ejemplo siguiente se da por supuesto un nombre de origen de datos denominada "Test". La base de datos asociada debe tener una tabla que se puede crear, como se indica a continuación:  
  
```sql  
CREATE TABLE emp4 (NAME char(30), AGE int, BIRTHDAY datetime, Memo1 text)  
```  
  
```cpp  
// SQLPutData.cpp  
// compile with: odbc32.lib user32.lib  
#include <stdio.h>  
#include <windows.h>  
#include <sqlext.h>  
#include <odbcss.h>  
  
#define TEXTSIZE  12000  
#define MAXBUFLEN 256  
  
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
  
   // SQLBindParameter variables.  
   SQLLEN cbTextSize, lbytes;  
  
   // SQLParamData variable.  
   PTR pParmID;  
  
   // SQLPutData variables.  
   UCHAR  Data[] =   
      "abcdefghijklmnopqrstuvwxyzabcdefghijklmnopqrstuvwxyz"  
      "abcdefghijklmnopqrstuvwxyzabcdefghijklmnopqrstuvwxyz"  
      "abcdefghijklmnopqrstuvwxyzabcdefghijklmnopqrstuvwxyz"  
      "abcdefghijklmnopqrstuvwxyzabcdefghijklmnopqrstuvwxyz"  
      "abcdefghijklmnopqrstuvwxyzabcdefghijklmnopqrstuvwxyz"  
      "abcdefghijklmnopqrstuvwxyzabcdefghijklmnopqrstuvwxyz"  
      "abcdefghijklmnopqrstuvwxyzabcdefghijklmnopqrstuvwxyz"  
      "abcdefghijklmnopqrstuvwxyzabcdefghijklmnopqrstuvwxyz"  
      "abcdefghijklmnopqrstuvwxyzabcdefghijklmnopqrstuvwxyz"  
      "abcdefghijklmnopqrstuvwxyz";  
  
   SDWORD cbBatch = (SDWORD)sizeof(Data) - 1;  
  
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
  
   // Allocate ODBC connection handle and connect.  
   retcode = SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc1);  
   if ( (retcode != SQL_SUCCESS_WITH_INFO) && (retcode != SQL_SUCCESS)) {  
      printf("SQLAllocHandle(hdbc1) Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Sample uses Integrated Security, create SQL Server DSN using Windows NT authentication.   
   retcode = SQLConnect(hdbc1, (UCHAR*)"Test", SQL_NTS, (UCHAR*)"",SQL_NTS, (UCHAR*)"", SQL_NTS);  
   if ( (retcode != SQL_SUCCESS) && (retcode != SQL_SUCCESS_WITH_INFO) ) {  
      printf("SQLConnect() Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Allocate statement handle.  
   retcode = SQLAllocHandle(SQL_HANDLE_STMT, hdbc1, &hstmt1);  
   if ( (retcode != SQL_SUCCESS) && (retcode != SQL_SUCCESS_WITH_INFO) ) {  
      printf("SQLAllocHandle(hstmt1) Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Set parameters based on total data to send.  
   lbytes = (SDWORD)TEXTSIZE;  
   cbTextSize = SQL_LEN_DATA_AT_EXEC(lbytes);  
  
   // Bind the parameter marker.  
   retcode = SQLBindParameter (hstmt1,           // hstmt  
                               1,                // ipar  
                               SQL_PARAM_INPUT,  // fParamType  
                               SQL_C_CHAR,       // fCType  
                               SQL_LONGVARCHAR,  // FSqlType  
                               lbytes,           // cbColDef  
                               0,                // ibScale  
                               (VOID *)1,        // rgbValue  
                               0,                // cbValueMax  
                               &cbTextSize);     // pcbValue  
  
   if ( (retcode != SQL_SUCCESS) && (retcode != SQL_SUCCESS_WITH_INFO) ) {  
      printf("SQLBindParameter Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Execute the command.  
   retcode =   
      SQLExecDirect(hstmt1, (UCHAR*)"INSERT INTO emp4 VALUES('Paul Borm', 46,'1950-11-12 00:00:00', ?)", SQL_NTS);  
   if ( (retcode != SQL_SUCCESS) && (retcode != SQL_NEED_DATA) && (retcode != SQL_SUCCESS_WITH_INFO) ) {  
      printf("SQLExecDirect Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Check to see if NEED_DATA; if yes, use SQLPutData.  
   retcode = SQLParamData(hstmt1, &pParmID);  
   if (retcode == SQL_NEED_DATA) {  
      while (lbytes > cbBatch) {  
         SQLPutData(hstmt1, Data, cbBatch);  
         lbytes -= cbBatch;  
      }  
      // Put final batch.  
      retcode = SQLPutData(hstmt1, Data, lbytes);   
   }  
  
   if ( (retcode != SQL_SUCCESS) && (retcode != SQL_SUCCESS_WITH_INFO) ) {  
      printf("SQLParamData Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Make final SQLParamData call.  
   retcode = SQLParamData(hstmt1, &pParmID);  
   if ( (retcode != SQL_SUCCESS) && (retcode != SQL_SUCCESS_WITH_INFO) ) {  
      printf("Final SQLParamData Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Clean up.  
   SQLFreeHandle(SQL_HANDLE_STMT, hstmt1);  
   SQLDisconnect(hdbc1);  
   SQLFreeHandle(SQL_HANDLE_DBC, hdbc1);  
   SQLFreeHandle(SQL_HANDLE_ENV, henv);  
}  
```  
  
## <a name="related-functions"></a>Funciones relacionadas  
  
|Para obtener información acerca de|Vea|  
|---------------------------|---------|  
|Enlazar un búfer con un parámetro|[Función SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md)|  
|Procesamiento de una instrucción de cancelación|[Función SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Ejecutar una instrucción SQL|[Función SQLExecDirect](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|Ejecutar una instrucción SQL preparada|[Función SQLExecute](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|Devuelve el siguiente parámetro para enviar datos|[Función SQLParamData](../../../odbc/reference/syntax/sqlparamdata-function.md)|  
  
## <a name="see-also"></a>Vea también  
 [Referencia de la API de ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Archivos de encabezado de ODBC](../../../odbc/reference/install/odbc-header-files.md)
