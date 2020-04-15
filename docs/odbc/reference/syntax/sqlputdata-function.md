---
title: Función SQLPutData (SQLPutData) Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7c4e704d96924942812904ea63d0e3d4fce8748e
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300045"
---
# <a name="sqlputdata-function"></a>Función SQLPutData
**Conformidad**  
 Versión introducida: Cumplimiento de normas ODBC 1.0: ISO 92  
  
 **Resumen**  
 **SQLPutData** permite a una aplicación enviar datos para un parámetro o columna al controlador en tiempo de ejecución de la instrucción. Esta función se puede utilizar para enviar valores de caracteres o datos binarios en partes a una columna con un tipo de datos específico de carácter, binario o origen de datos (por ejemplo, parámetros de los tipos SQL_LONGVARBINARY o SQL_LONGVARCHAR). **SQLPutData** admite el enlace a un tipo de datos Unicode C, incluso si el controlador subyacente no admite datos Unicode.  
  
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
 [Entrada] Puntero a un búfer que contiene los datos reales del parámetro o columna. Los datos deben estar en el tipo de datos C especificado en el *valueType* argumento de **SQLBindParameter** (para los datos de parámetro) o el *TargetType* argumento de **SQLBindCol** (para los datos de columna).  
  
 *StrLen_or_Ind*  
 [Entrada] Longitud \*de *DataPtr*. Especifica la cantidad de datos enviados en una llamada a **SQLPutData**. La cantidad de datos puede variar con cada llamada para un parámetro o columna determinado. *StrLen_or_Ind* se ignora a menos que cumpla una de las siguientes condiciones:  
  
-   *StrLen_or_Ind* es SQL_NTS, SQL_NULL_DATA o SQL_DEFAULT_PARAM.  
  
-   El tipo de datos de C especificado en **SQLBindParameter** o **SQLBindCol** es SQL_C_CHAR o SQL_C_BINARY.  
  
-   El tipo de datos C es SQL_C_DEFAULT y el tipo de datos C predeterminado para el tipo de datos SQL especificado es SQL_C_CHAR o SQL_C_BINARY.  
  
 Para todos los demás tipos de datos de C, si *no* se \*SQL_NULL_DATA StrLen_or_Ind o SQL_DEFAULT_PARAM, el controlador supone que el tamaño del búfer *DataPtr* es el tamaño del tipo de datos C especificado con *ValueType* o *TargetType* y envía todo el valor de datos. Para obtener más información, vea [Convertir datos de C a tipos](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md) de datos SQL en apéndice D: tipos de datos.  
  
## <a name="returns"></a>Devuelve  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_STILL_EXECUTING, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnóstico  
 Cuando **SQLPutData** devuelve SQL_ERROR o SQL_SUCCESS_WITH_INFO, se puede obtener un valor SQLSTATE asociado llamando a **SQLGetDiagRec** con un *HandleType* de SQL_HANDLE_STMT y un *Control* de *StatementHandle*. En la tabla siguiente se enumeran los valores SQLSTATE devueltos normalmente por **SQLPutData** y se explica cada uno de ellos en el contexto de esta función; la notación "(DM)" precede a las descripciones de SQLSTATEs devueltas por el Administrador de controladores. El código de retorno asociado a cada valor SQLSTATE se SQL_ERROR, a menos que se indique lo contrario.  
  
|SQLSTATE|Error|Descripción|  
|--------------|-----------|-----------------|  
|01000|Advertencia general|Mensaje informativo específico del controlador. (La función devuelve SQL_SUCCESS_WITH_INFO.)|  
|01004|Datos de cadena truncados a la derecha|Los datos de cadena o binarios devueltos para un parámetro de salida dieron como resultado el truncamiento de caracteres no en blanco o datos binarios no NULL. Si era un valor de cadena, se truncaba a la derecha. (La función devuelve SQL_SUCCESS_WITH_INFO.)|  
|07006|Infracción de atributo de tipo de datos restringido|El valor de datos identificado por el *ValueType* argumento en **SQLBindParameter** para el parámetro enlazado no se pudo convertir al tipo de datos identificado por el *ParameterType* argumento en **SQLBindParameter**.|  
|07S01|Uso no válido del parámetro predeterminado|Un valor de parámetro, establecido con **SQLBindParameter**, se SQL_DEFAULT_PARAM y el parámetro correspondiente no tenía un valor predeterminado.|  
|08S01|Fallo del enlace de comunicación|Error en el vínculo de comunicación entre el controlador y el origen de datos al que estaba conectado el controlador antes de que la función completara el procesamiento.|  
|22001|Datos de cadena, truncamiento a la derecha|La asignación de un carácter o valor binario a una columna dio lugar a la truncación de caracteres o bytes no en blanco (carácter) o no nulos (binarios).<br /><br /> El tipo de información SQL_NEED_LONG_DATA_LEN de **SQLGetInfo** era "Y" y se enviaron más datos para un parámetro long (el tipo de datos se SQL_LONGVARCHAR, SQL_LONGVARBINARY o un tipo de datos específico del origen de datos largo) que se especificó con el argumento *StrLen_or_IndPtr* en **SQLBindParameter**.<br /><br /> El tipo de información SQL_NEED_LONG_DATA_LEN **de SQLGetInfo** era "Y" y se enviaron más datos para una columna larga (el tipo de datos se SQL_LONGVARCHAR, SQL_LONGVARBINARY o un tipo de datos específico del origen de datos largo) que se especificó en el búfer de longitud correspondiente a una columna de una fila de datos que se agregó o actualizó con **SQLBulkOperations** o se actualizó con **SQLSetPos**.|  
|22003|Valor numérico fuera del rango|Los datos enviados para un parámetro numérico enlazado o columna hicieron que la parte completa (en lugar de fraccionaria) del número se truncaran cuando se asignaaa a la columna de tabla asociada.<br /><br /> Devolver un valor numérico (como numérico o cadena) para uno o más parámetros de entrada/salida o salida habría provocado que se truncase la parte total (en lugar de fracción) del número.|  
|22007|Formato de fecha y hora no válido|Los datos enviados para un parámetro o columna que estaba enlazado a una estructura de fecha, hora o marca de tiempo era, respectivamente, una fecha, hora o marca de tiempo no válidas.<br /><br /> Un parámetro de entrada/salida o salida se enlazaba a una estructura C de fecha, hora o marca de tiempo, y un valor en el parámetro devuelto era, respectivamente, una fecha, hora o marca de tiempo no válida. (La función devuelve SQL_SUCCESS_WITH_INFO.)|  
|22008|Desbordamiento de campo de fecha y hora|Una expresión datetime calculada para un parámetro de entrada/salida o salida dio como resultado una estructura C de fecha, hora o marca de tiempo que no era válida.|  
|22012|División por cero|Una expresión aritmética calculada para un parámetro de entrada/salida o salida dio como resultado la división por cero.|  
|22015|Desbordamiento de campo de intervalo|Los datos enviados para una columna o parámetro numérico o de intervalo exacto a un tipo de datos SQL de intervalo causaron una pérdida de dígitos significativos.<br /><br /> Los datos se enviaron para una columna o parámetro de intervalo con más de un campo, se convirtió en un tipo de datos numérico y no tenía ninguna representación en el tipo de datos numérico.<br /><br /> Los datos enviados para los datos de columna o parámetro se asignaron a un tipo SQL de intervalo y no había ninguna representación del valor del tipo C en el tipo SQL de intervalo.<br /><br /> Los datos enviados para una columna o parámetro numérico o de intervalo C exacto a un tipo de intervalo C causaron una pérdida de dígitos significativos.<br /><br /> Los datos enviados para los datos de columna o parámetro se asignaron a una estructura de intervalo C y no hubo ninguna representación de los datos en la estructura de datos de intervalo.|  
|22018|Valor de carácter no válido para la especificación de conversión|El tipo C era un número exacto o aproximado, una fecha y hora o un tipo de datos de intervalo; el tipo SQL de la columna era un tipo de datos de carácter; y el valor de la columna o parámetro no era un literal válido del tipo C enlazado.<br /><br /> El tipo SQL era un número exacto o aproximado, una fecha y hora o un tipo de datos de intervalo; el tipo C se SQL_C_CHAR; y el valor de la columna o parámetro no era un literal válido del tipo SQL enlazado.|  
|HY000|Error general|Se ha producido un error para el que no se ha definido sqlSTATE específico y para el que no se ha definido sqlSTATE específico de la implementación. El mensaje de error devuelto por **SQLGetDiagRec** en el * \*messageText* búfer describe el error y su causa.|  
|HY001|Error de asignación de memoria|El controlador no pudo asignar la memoria necesaria para admitir la ejecución o finalización de la función.|  
|HY008|Operación cancelada|El procesamiento asincrónico se ha habilitado para *StatementHandle*. Se llamó a la función y antes de completar la ejecución, **SQLCancel** o **SQLCancelHandle** se llamó en el *StatementHandle*. A continuación, se volvió a llamar a la función en *StatementHandle*.<br /><br /> Se llamó a la función y antes de completar la ejecución, **SQLCancel** o **SQLCancelHandle** se llamó en el *StatementHandle* desde un subproceso diferente en una aplicación multiproceso.|  
|HY009|Uso no válido de puntero nulo|(DM) el argumento *DataPtr* era un puntero nulo y el argumento *StrLen_or_Ind* no era 0, SQL_DEFAULT_PARAM o SQL_NULL_DATA.|  
|HY010|Error de secuencia de funciones|(DM) La llamada de función anterior no era una llamada a **SQLPutData** o **SQLParamData**.<br /><br /> (DM) se llamó a una función de ejecución asincrónica para el identificador de conexión asociado a *StatementHandle*. Esta función asincrónica todavía se estaba ejecutando cuando se llamó a la función SQLPutData.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**o **SQLMoreResults** se llamó para el *StatementHandle* y devuelto SQL_PARAM_DATA_AVAILABLE. Se llamó a esta función antes de recuperar los datos para todos los parámetros transmitidos.<br /><br /> (DM) se llamó a una función de ejecución asincrónica (no esta) para el *StatementHandle* y todavía se estaba ejecutando cuando se llamó a esta función.|  
|HY013|Error de administración de memoria|No se pudo procesar la llamada de función porque no se pudo tener acceso a los objetos de memoria subyacentes, posiblemente debido a condiciones de poca memoria.|  
|HY019|Datos no caracteres y no binarios enviados en partes|**SQLPutData** se llamó más de una vez para un parámetro o columna y no se utilizaba para enviar datos de caracteres C a una columna con un tipo de datos de carácter, binario o específico del origen de datos o para enviar datos C binarios a una columna con un tipo de datos específico de carácter, binario o origen de datos.|  
|HY020|Intento de concatenar un valor nulo|**SQLPutData** se llamó más de una vez desde la llamada que devolvió SQL_NEED_DATA y en una de esas llamadas, el *argumento StrLen_or_Ind* contenía SQL_NULL_DATA o SQL_DEFAULT_PARAM.|  
|HY090|Cadena no válida o longitud de búfer|El argumento *DataPtr* no era un puntero nulo y el argumento *StrLen_or_Ind* era menor que 0 pero no igual a SQL_NTS o SQL_NULL_DATA.|  
|HY117|La conexión se suspende debido al estado de transacción desconocido. Solo se permiten funciones de desconexión y de solo lectura.|(DM) Para obtener más información sobre el estado suspendido, vea [SqlEndTran (función).](../../../odbc/reference/syntax/sqlendtran-function.md)|  
|HYT01|Tiempo de espera de conexión expirado|El período de tiempo de espera de conexión expiró antes de que el origen de datos respondiera a la solicitud. El período de tiempo de espera de conexión se establece a través de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|El controlador no admite esta función|(DM) El controlador asociado con el *StatementHandle* no admite la función.|  
|IM017|El sondeo está deshabilitado en el modo de notificación asincrónica|Siempre que se utiliza el modelo de notificación, el sondeo está deshabilitado.|  
|IM018|**SQLCompleteAsync** no se ha llamado para completar la operación asincrónica anterior en este identificador.|Si la llamada de función anterior en el identificador devuelve SQL_STILL_EXECUTING y si el modo de notificación está habilitado, **sqlCompleteAsync** debe llamarse en el identificador para realizar el procesamiento posterior y completar la operación.|  
  
 Si se llama a **SQLPutData** al enviar datos para un parámetro en una instrucción SQL, puede devolver cualquier SQLSTATE que pueda devolver la función llamada para ejecutar la instrucción (**SQLExecute** o **SQLExecDirect**). Si se llama al enviar datos de una columna que se actualiza o agrega con **SQLBulkOperations** o se actualiza con **SQLSetPos**, puede devolver cualquier SQLSTATE que **SQLBulkOperations** o **SQLSetPos**pueda devolver .  
  
## <a name="comments"></a>Comentarios  
 **SQLPutData** se puede llamar para proporcionar datos en ejecución para dos usos: datos de parámetro que se usarán en una llamada a **SQLExecute** o **SQLExecDirect**, o datos de columna que se usarán cuando una fila se actualiza o se agrega mediante una llamada a **SQLBulkOperations** o se actualiza mediante una llamada a **SQLSetPos**.  
  
 Cuando una aplicación llama a **SQLParamData** para determinar qué datos debe enviar, el controlador devuelve un indicador que la aplicación puede usar para determinar qué datos de parámetro enviar o dónde se pueden encontrar los datos de columna. También devuelve SQL_NEED_DATA, que es un indicador a la aplicación que debe llamar a **SQLPutData** para enviar los datos. En el *DataPtr* argumento a **SQLPutData**, la aplicación pasa un puntero al búfer que contiene los datos reales para el parámetro o columna.  
  
 Cuando el controlador devuelve SQL_SUCCESS para **SQLPutData**, la aplicación llama **sqlParamData** de nuevo. **SQLParamData** devuelve SQL_NEED_DATA si es necesario enviar más datos, en cuyo caso la aplicación llama a **SQLPutData** de nuevo. Devuelve SQL_SUCCESS si se han enviado todos los datos en ejecución. A continuación, la aplicación llama a **SQLParamData** de nuevo. Si el controlador devuelve SQL_NEED_DATA y otro indicador en * \*ValuePtrPtr*, requiere datos para otro parámetro o columna y **SQLPutData** se llama de nuevo. Si el controlador devuelve SQL_SUCCESS, se han enviado todos los datos en ejecución y se puede ejecutar la instrucción SQL o se puede procesar la llamada **SQLBulkOperations** o **SQLSetPos.**  
  
 Para obtener más información sobre cómo se pasan los datos de parámetros de datos en ejecución en tiempo de ejecución de la instrucción, vea "Pasar valores de parámetro" en [SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md) y [Enviar datos largos](../../../odbc/reference/develop-app/sending-long-data.md). Para obtener más información sobre cómo se actualizan o agregan los datos de columna de datos en ejecución, vea la sección "Uso de SQLSetPos" en [SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md), "Realizar actualizaciones masivas mediante marcadores" en [SQLBulkOperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md)y [Datos largos y SQLSetPos y SQLBulkOperations](../../../odbc/reference/develop-app/long-data-and-sqlsetpos-and-sqlbulkoperations.md).  
  
> [!NOTE]  
>  Una aplicación puede usar **SQLPutData** para enviar datos en partes solo cuando envía datos de carácter C a una columna con un tipo de datos específico de carácter, binario o origen de datos o al enviar datos binarios de C a una columna con un tipo de datos de carácter, binario o específico del origen de datos. Si **sqlPutData** se llama más de una vez en cualquier otra condición, devuelve SQL_ERROR y SQLSTATE HY019 (datos no binarios y no caracteres enviados en partes).  
  
## <a name="example"></a>Ejemplo  
 En el ejemplo siguiente se supone un nombre de origen de datos denominado Test. La base de datos asociada debe tener una tabla que pueda crear, como se indica a continuación:  
  
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
  
|Para información acerca de|Vea|  
|---------------------------|---------|  
|Enlazar un búfer a un parámetro|[Función SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md)|  
|Cancelación del procesamiento de extractos|[Función SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Ejecución de una instrucción SQL|[Función SQLExecDirect](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|Ejecución de una instrucción SQL preparada|[Función SQLExecute](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|Devolver el siguiente parámetro para enviar datos|[Función SQLParamData](../../../odbc/reference/syntax/sqlparamdata-function.md)|  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de la API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Archivos de encabezado de ODBC](../../../odbc/reference/install/odbc-header-files.md)
