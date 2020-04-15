---
title: FUNción SQLDescribeCol ? Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLDescribeCol
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLDescribeCol
helpviewer_keywords:
- SQLDescribeCol function [ODBC]
ms.assetid: eddef353-83f3-4a3c-8f24-f9ed888890a4
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c727f6b36930b0d2ad0d5a61592b83bcd4995426
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301175"
---
# <a name="sqldescribecol-function"></a>SQLDescribeCol (función)
**Conformidad**  
 Versión introducida: Cumplimiento de normas ODBC 1.0: ISO 92  
  
 **Resumen**  
 **SQLDescribeCol** devuelve el descriptor de resultado - nombre de columna, tipo, tamaño de columna, dígitos decimales y nulabilidad - para una columna en el conjunto de resultados. Esta información también está disponible en los campos del IRD.  
  
## <a name="syntax"></a>Sintaxis  
  
```cpp  
  
SQLRETURN SQLDescribeCol(  
      SQLHSTMT       StatementHandle,  
      SQLUSMALLINT   ColumnNumber,  
      SQLCHAR *      ColumnName,  
      SQLSMALLINT    BufferLength,  
      SQLSMALLINT *  NameLengthPtr,  
      SQLSMALLINT *  DataTypePtr,  
      SQLULEN *      ColumnSizePtr,  
      SQLSMALLINT *  DecimalDigitsPtr,  
      SQLSMALLINT *  NullablePtr);  
```  
  
## <a name="arguments"></a>Argumentos  
 *StatementHandle*  
 [Entrada] Identificador de instrucción.  
  
 *ColumnNumber*  
 [Entrada] Número de columna de datos de resultados, ordenados secuencialmente en orden de columna creciente, a partir de 1. El *argumento ColumnNumber* también se puede establecer en 0 para describir la columna de marcador.  
  
 *ColumnName*  
 [Salida] Puntero a un búfer terminado en null en el que se va a devolver el nombre de columna. Este valor se lee desde el campo SQL_DESC_NAME del IRD. Si la columna no tiene nombre o no se puede determinar el nombre de la columna, el controlador devuelve una cadena vacía.  
  
 Si *ColumnName* es NULL, *NameLengthPtr* seguirá devolviendo el número total de caracteres (excluyendo el carácter de terminación nula para los datos de caracteres) disponibles para devolver en el búfer al que apunta *ColumnName*.  
  
 *BufferLength*  
 [Entrada] Longitud del búfer **ColumnName,* en caracteres.  
  
 *NameLengthPtr*  
 [Salida] Puntero a un búfer en el que se va a devolver el \*número total de caracteres (excluyendo la terminación nula) disponibles para devolver en *ColumnName*. Si el número de caracteres disponibles para devolver es mayor \*o igual que *BufferLength*, el nombre de columna en *ColumnName* se trunca en *BufferLength* menos la longitud de un carácter de terminación nula.  
  
 *DataTypePtr*  
 [Salida] Puntero a un búfer en el que se va a devolver el tipo de datos SQL de la columna. Este valor se lee desde el campo SQL_DESC_CONCISE_TYPE del IRD. Este será uno de los valores de Tipos de [datos SQL](../../../odbc/reference/appendixes/sql-data-types.md)o un tipo de datos SQL específico del controlador. Si no se puede determinar el tipo de datos, el controlador devuelve SQL_UNKNOWN_TYPE.  
  
 En ODBC 3. *x*, SQL_TYPE_DATE, SQL_TYPE_TIME o SQL_TYPE_TIMESTAMP se devuelve en * \*DataTypePtr* para los datos de fecha, hora o marca de tiempo, respectivamente; en ODBC 2. *x*, SQL_DATE, SQL_TIME o SQL_TIMESTAMP se devuelve. El Administrador de controladores realiza las asignaciones necesarias cuando un ODBC 2. *x* aplicación está trabajando con un ODBC 3. *x* controlador o cuando un ODBC 3. *x* aplicación está trabajando con un ODBC 2. *x* conductor.  
  
 Cuando *ColumnNumber* es igual a 0 (para una columna de marcador), se devuelve SQL_BINARY en * \*DataTypePtr* para marcadores de longitud variable. (SQL_INTEGER se devuelve si un ODBC 3 utiliza marcadores. *x* aplicación que trabaja con un ODBC 2. *x* controlador o por un ODBC 2. *x* aplicación que trabaja con un ODBC 3. *x* controlador.)  
  
 Para obtener más información sobre estos tipos de datos, vea [Tipos de datos SQL](../../../odbc/reference/appendixes/sql-data-types.md) en Apéndice D: Tipos de datos. Para obtener información acerca de los tipos de datos SQL específicos del controlador, consulte la documentación del controlador.  
  
 *ColumnSizePtr*  
 [Salida] Puntero a un búfer en el que se va a devolver el tamaño (en caracteres) de la columna en el origen de datos. Si no se puede determinar el tamaño de columna, el controlador devuelve 0. Para obtener más información sobre el tamaño de columna, consulte Tamaño de [columna, Dígitos decimales, Transferir longitud de octeto y Tamaño](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) de visualización en apéndice D: tipos de datos.  
  
 *DecimalDigitsPtr*  
 [Salida] Puntero a un búfer en el que se va a devolver el número de dígitos decimales de la columna en el origen de datos. Si no se puede determinar el número de dígitos decimales o no es aplicable, el controlador devuelve 0. Para obtener más información sobre los dígitos decimales, consulte Tamaño de [columna, Dígitos decimales, Transferir longitud de octeto y Tamaño](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) de visualización en apéndice D: tipos de datos.  
  
 *NullablePtr*  
 [Salida] Puntero a un búfer en el que se va a devolver un valor que indica si la columna permite valores NULL. Este valor se lee en el campo SQL_DESC_NULLABLE del IRD. El valor puede ser:  
  
 SQL_NO_NULLS: la columna no permite valores NULL.  
  
 SQL_NULLABLE: la columna permite valores NULL.  
  
 SQL_NULLABLE_UNKNOWN: el controlador no puede determinar si la columna permite valores NULL.  
  
## <a name="returns"></a>Devuelve  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_STILL_EXECUTING, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnóstico  
 Cuando **SQLDescribeCol** devuelve SQL_ERROR o SQL_SUCCESS_WITH_INFO, se puede obtener un valor SQLSTATE asociado llamando a **SQLGetDiagRec** con un *HandleType* de SQL_HANDLE_STMT y un *control* *StatementHandle*. En la tabla siguiente se enumeran los valores SQLSTATE devueltos normalmente por **SQLDescribeCol** y se explica cada uno de ellos en el contexto de esta función; la notación "(DM)" precede a las descripciones de SQLSTATEs devueltas por el Administrador de controladores. El código de retorno asociado a cada valor SQLSTATE se SQL_ERROR, a menos que se indique lo contrario.  
  
|SQLSTATE|Error|Descripción|  
|--------------|-----------|-----------------|  
|01000|Advertencia general|Mensaje informativo específico del controlador. (La función devuelve SQL_SUCCESS_WITH_INFO.)|  
|01004|Datos de cadena truncados a la derecha|El \*búfer *ColumnName* no era lo suficientemente grande como para devolver el nombre de columna completo, por lo que el nombre de columna se truncó. La longitud del nombre de columna no truncado se devuelve en **NameLengthPtr*. (La función devuelve SQL_SUCCESS_WITH_INFO.)|  
|07005|Declaración preparada no una *especificación de cursor*|La instrucción asociada a *StatementHandle* no devolvió un conjunto de resultados. No había columnas que describir.|  
|07009|Indice de descriptor no válido|(DM) el valor especificado para el argumento *ColumnNumber* era igual a 0 y la opción de instrucción SQL_ATTR_USE_BOOKMARKS era SQL_UB_OFF.<br /><br /> El valor especificado para el argumento *ColumnNumber* era mayor que el número de columnas del conjunto de resultados.|  
|08S01|Fallo del enlace de comunicación|Error en el vínculo de comunicación entre el controlador y el origen de datos al que estaba conectado el controlador antes de que la función completara el procesamiento.|  
|HY000|Error general|Se ha producido un error para el que no se ha definido sqlSTATE específico y para el que no se ha definido sqlSTATE específico de la implementación. El mensaje de error devuelto por **SQLGetDiagRec** en el * \*messageText* búfer describe el error y su causa.|  
|HY001|Error de asignación de memoria|El controlador no pudo asignar la memoria necesaria para admitir la ejecución o finalización de la función.|  
|HY008|Operación cancelada|El procesamiento asincrónico se ha habilitado para *StatementHandle*. Se llamó a la función y antes de completar la ejecución, **SQLCancel** o **SQLCancelHandle** se llamó en el *StatementHandle*. A continuación, se volvió a llamar a la función en *StatementHandle*.<br /><br /> Se llamó a la función y antes de completar la ejecución, **SQLCancel** o **SQLCancelHandle** se llamó en el *StatementHandle* desde un subproceso diferente en una aplicación multiproceso.|  
|HY010|Error de secuencia de funciones|(DM) se llamó a una función de ejecución asincrónica para el identificador de conexión asociado a *StatementHandle*. Esta función asincrónica todavía se estaba ejecutando cuando **SQLDescribeCol** se llamó.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**o **SQLMoreResults** se llamó para el *StatementHandle* y devuelto SQL_PARAM_DATA_AVAILABLE. Se llamó a esta función antes de recuperar los datos para todos los parámetros transmitidos.<br /><br /> (DM) se llamó a una función de ejecución asincrónica (no esta) para el *StatementHandle* y todavía se estaba ejecutando cuando se llamó a esta función.<br /><br /> (DM) Se llamó a la función antes de llamar a **SQLPrepare**, **SQLExecute**o una función de catálogo en el identificador de instrucción.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, o **SQLSetPos** se llamó para el *StatementHandle* y devuelto SQL_NEED_DATA. Se llamó a esta función antes de que se enviaran datos para todos los parámetros o columnas de datos en ejecución.|  
|HY013|Error de administración de memoria|No se pudo procesar la llamada de función porque no se pudo tener acceso a los objetos de memoria subyacentes, posiblemente debido a condiciones de poca memoria.|  
|HY090|Cadena no válida o longitud de búfer|(DM) el valor especificado para el argumento *BufferLength* era menor que 0.|  
|HY117|La conexión se suspende debido al estado de transacción desconocido. Solo se permiten funciones de desconexión y de solo lectura.|(DM) Para obtener más información sobre el estado suspendido, vea [SqlEndTran (función).](../../../odbc/reference/syntax/sqlendtran-function.md)|  
|HYT01|Tiempo de espera de conexión expirado|El período de tiempo de espera de conexión expiró antes de que el origen de datos respondiera a la solicitud. El período de tiempo de espera de conexión se establece a través de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|El controlador no admite esta función|(DM) El controlador asociado con el *StatementHandle* no admite la función.|  
|IM017|El sondeo está deshabilitado en el modo de notificación asincrónica|Siempre que se utiliza el modelo de notificación, el sondeo está deshabilitado.|  
|IM018|**SQLCompleteAsync** no se ha llamado para completar la operación asincrónica anterior en este identificador.|Si la llamada de función anterior en el identificador devuelve SQL_STILL_EXECUTING y si el modo de notificación está habilitado, **sqlCompleteAsync** debe llamarse en el identificador para realizar el procesamiento posterior y completar la operación.|  
  
 **SQLDescribeCol** puede devolver cualquier SQLSTATE que **SQLPrepare** o **SQLExecute** pueden devolver cuando se llama después de **SQLPrepare** y antes de **SQLExecute**, dependiendo de cuándo el origen de datos evalúa la instrucción SQL asociada al identificador de instrucción.  
  
 Por motivos de rendimiento, una aplicación no debe llamar a **SQLDescribeCol** antes de ejecutar una instrucción.  
  
## <a name="comments"></a>Comentarios  
 Normalmente, una aplicación llama a **SQLDescribeCol** después de una llamada a **SQLPrepare** y antes o después de la llamada asociada a **SQLExecute**. Una aplicación también puede llamar a **SQLDescribeCol** después de una llamada a **SQLExecDirect**. Para obtener más información, consulte Metadatos del conjunto de [resultados](../../../odbc/reference/develop-app/result-set-metadata.md).  
  
 **SQLDescribeCol** recupera el nombre de columna, el tipo y la longitud generados por una instrucción **SELECT.** Si la columna es una expresión, **ColumnName* es una cadena vacía o un nombre definido por el controlador.  
  
> [!NOTE]  
>  ODBC admite SQL_NULLABLE_UNKNOWN como una extensión, aunque la especificación Open Group y SQL Access Group Call Level Interface no especifica la opción para **SQLDescribeCol**.  
  
## <a name="related-functions"></a>Funciones relacionadas  
  
|Para información acerca de|Vea|  
|---------------------------|---------|  
|Enlazar un búfer a una columna en un conjunto de resultados|[SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Cancelación del procesamiento de extractos|[SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Devolver información sobre una columna en un conjunto de resultados|[SQLColAttribute](../../../odbc/reference/syntax/sqlcolattribute-function.md)|  
|Obtención de varias filas de datos|[SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|Devolver el número de columnas del conjunto de resultados|[SQLNumResultCols](../../../odbc/reference/syntax/sqlnumresultcols-function.md)|  
|Preparación de una declaración para la ejecución|[SQLPrepare](../../../odbc/reference/syntax/sqlprepare-function.md)|  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de la API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Archivos de encabezado de ODBC](../../../odbc/reference/install/odbc-header-files.md)
