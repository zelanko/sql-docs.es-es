---
title: Función SQLDescribeCol | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 63982d87f0dbbe0c8ab1a540185e298d9943f630
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68104790"
---
# <a name="sqldescribecol-function"></a>SQLDescribeCol (función)
**Conformidad**  
 Versión de introducción: Cumplimiento de estándares 1.0 de ODBC: ISO 92  
  
 **Resumen**  
 **SQLDescribeCol** devuelve el descriptor de resultado - nombre de columna, tipo, tamaño de la columna, dígitos decimales y nulabilidad - para una columna del conjunto de resultados. Esta información también está disponible en los campos de IRD.  
  
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
 [Entrada] Número de columna de datos de resultados, ordenados secuencialmente en orden creciente de columna, comenzando en 1. El *ColumnNumber* argumento también se puede establecer en 0 para describir la columna de marcador.  
  
 *ColumnName*  
 [Salida] Puntero a un búfer terminado en null en la que se va a devolver el nombre de columna. Este valor se lee desde el campo SQL_DESC_NAME de IRD. Si la columna no tiene nombre o no se puede determinar el nombre de columna, el controlador devuelve una cadena vacía.  
  
 Si *ColumnName* es NULL, *NameLengthPtr* devolverá el número total de caracteres (excepto el carácter de terminación null para los datos de caracteres) disponibles para devolver en el búfer señalado por *ColumnName*.  
  
 *BufferLength*  
 [Entrada] Longitud de la **ColumnName* búfer en caracteres.  
  
 *NameLengthPtr*  
 [Salida] Puntero a un búfer en el que se va a devolver el número total de caracteres (excepto la terminación null) disponibles para devolver en \* *ColumnName*. Si el número de caracteres disponibles para devolver es mayor o igual a *BufferLength*, el nombre de columna \* *ColumnName* se trunca a *BufferLength*menos la longitud de un carácter de terminación null.  
  
 *DataTypePtr*  
 [Salida] Puntero a un búfer en el que se va a devolver el tipo de datos SQL de la columna. Este valor se lee desde el campo SQL_DESC_CONCISE_TYPE de IRD. Se trata de uno de los valores de [tipos de datos SQL](../../../odbc/reference/appendixes/sql-data-types.md), o un tipo de datos SQL específicas del controlador. Si no se puede determinar el tipo de datos, el controlador devuelve SQL_UNKNOWN_TYPE.  
  
 En ODBC 3. *x*, SQL_TYPE_DATE, SQL_TYPE_TIME y SQL_TYPE_TIMESTAMP se devuelve en  *\*DataTypePtr* para fecha, hora o datos de marca de tiempo, respectivamente; en ODBC 2. *x*, SQL_DATE, SQL_TIME o SQL_TIMESTAMP se devuelve. El Administrador de controladores realiza las asignaciones necesarias cuando un ODBC 2. *x* aplicación funciona con una aplicación ODBC 3. *x* controlador o cuando una aplicación ODBC 3. *x* aplicación funciona con un ODBC 2. *x* controlador.  
  
 Cuando *ColumnNumber* es igual a 0 (para una columna de marcador), se devuelve SQL_BINARY en  *\*DataTypePtr* los marcadores de longitud variable. (SQL_INTEGER se devuelve si se utilizan marcadores por una aplicación ODBC 3. *x* la aplicación funciona con un ODBC 2. *x* controlador o por un ODBC 2. *x* la aplicación funciona con una aplicación ODBC 3. *x* controlador.)  
  
 Para obtener más información sobre estos tipos de datos, vea [tipos de datos SQL](../../../odbc/reference/appendixes/sql-data-types.md) en el apéndice D: Tipos de datos. Para obtener información acerca de los tipos de datos SQL específicas del controlador, consulte la documentación del controlador.  
  
 *ColumnSizePtr*  
 [Salida] Puntero a un búfer en el que se va a devolver el tamaño (en caracteres) de la columna del origen de datos. Si no se puede determinar el tamaño de columna, el controlador devuelve 0. Para obtener más información sobre el tamaño de la columna, vea [tamaño de la columna, dígitos decimales, transferir la longitud en octetos y tamaño de presentación](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) en el apéndice D: Tipos de datos.  
  
 *DecimalDigitsPtr*  
 [Salida] Puntero a un búfer en el que se va a devolver el número de dígitos decimales de la columna del origen de datos. Si no se puede determinar el número de dígitos decimales o no aplicable, el controlador devuelve 0. Para obtener más información sobre los dígitos decimales, consulte [tamaño de la columna, dígitos decimales, transferir la longitud en octetos y tamaño de presentación](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) en el apéndice D: Tipos de datos.  
  
 *NullablePtr*  
 [Salida] Puntero a un búfer en el que se va a devolver un valor que indica si la columna permite valores NULL. Este valor se lee desde el campo SQL_DESC_NULLABLE de IRD. El valor puede ser:  
  
 SQL_NO_NULLS: La columna no permite valores NULL.  
  
 SQL_NULLABLE: La columna permite valores NULL.  
  
 SQL_NULLABLE_UNKNOWN: El controlador no puede determinar si la columna permite valores NULL.  
  
## <a name="returns"></a>Devuelve  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_STILL_EXECUTING, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnóstico  
 Cuando **SQLDescribeCol** devuelve SQL_ERROR o SQL_SUCCESS_WITH_INFO, un valor SQLSTATE asociado se puede obtener mediante una llamada a **SQLGetDiagRec** con un *HandleType*de SQL_HANDLE_STMT y un *controlar* de *StatementHandle*. En la tabla siguiente se enumera los valores SQLSTATE devueltos normalmente por **SQLDescribeCol** y se explica cada uno de ellos en el contexto de esta función; la notación "(DM)" precede a las descripciones de SQLSTATE devuelto por el Administrador de controladores. El código de retorno asociado a cada valor SQLSTATE es SQL_ERROR, a menos que se indique lo contrario.  
  
|SQLSTATE|Error|Descripción|  
|--------------|-----------|-----------------|  
|01000|Advertencia general|Específico del controlador de mensaje informativo. (La función devuelve SQL_SUCCESS_WITH_INFO).|  
|01004|Datos de cadena derecha truncados|El búfer \* *ColumnName* no era lo suficientemente grande como para devolver el nombre de columna completa, por lo que el nombre de columna se ha truncado. Se devuelve la longitud del nombre de columna sin truncar en **NameLengthPtr*. (La función devuelve SQL_SUCCESS_WITH_INFO).|  
|07005|Instrucción preparada no un *especificación de cursor*|La instrucción asociada con el *StatementHandle* no devolvió un conjunto de resultados. No hay ninguna columna para describir.|  
|07009|Índice de descriptor no válido|(DM) el valor especificado para el argumento *ColumnNumber* era igual a 0, y la opción de instrucción SQL_ATTR_USE_BOOKMARKS era SQL_UB_OFF.<br /><br /> El valor especificado para el argumento *ColumnNumber* era mayor que el número de columnas del conjunto de resultados.|  
|08S01|Error de vínculo de comunicación|Error en el vínculo de comunicación entre el controlador y el origen de datos a la que se ha conectado el controlador antes del procesamiento de la función se ha completado.|  
|HY000|Error general|Se produjo un error para que se ha producido ningún SQLSTATE específico y para los que se ha definido ningún SQLSTATE específicos de la implementación. El mensaje de error devuelto por **SQLGetDiagRec** en el  *\*MessageText* búfer describe el error y su causa.|  
|HY001|Error de asignación de memoria|El controlador no pudo asignar la memoria necesaria para admitir la ejecución o la finalización de la función.|  
|HY008|Operación cancelada|Procesamiento asincrónico se habilitó para la *StatementHandle*. Se llamó a la función, y antes que completó la ejecución, **SQLCancel** o **SQLCancelHandle** se ha llamado en el *StatementHandle*. A continuación, la función se llamó de nuevo en el *StatementHandle*.<br /><br /> Se llamó a la función, y antes que completó la ejecución, **SQLCancel** o **SQLCancelHandle** se ha llamado en el *StatementHandle* desde un subproceso diferente en un aplicaciones multiproceso.|  
|HY010|Error de secuencia de función|(DM) se llamó a una función que se ejecuta de forma asincrónica para el identificador de conexión que está asociado el *StatementHandle*. Esta función asincrónica aún estaba ejecutando cuando **SQLDescribeCol** llamó.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, o **SQLMoreResults** se llamó para el *StatementHandle* y devuelven SQL_PARAM_DATA_ ESTÁ DISPONIBLE. Esta función se invoca antes de que se recuperan los datos para todos los parámetros transmitidos.<br /><br /> (DM) se llamó a una función que se ejecuta asincrónicamente (no ésta) para el *StatementHandle* y aún se estaba ejecutando cuando se llamó a esta función.<br /><br /> (DM) que se llamó la función antes de llamar a **SQLPrepare**, **SQLExecute**, o una función de catálogo en el identificador de instrucción.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, o **SQLSetPos** se llamó para el  *StatementHandle* y devuelve SQL_NEED_DATA. Esta función se invoca antes de que se enviaron datos para todas las columnas o parámetros de datos en ejecución.|  
|HY013|Error de administración de memoria|No se pudo procesar la llamada de función porque los objetos de memoria subyacente no se podrían tener acceso, posiblemente debido a memoria insuficiente.|  
|HY090|Longitud de búfer o cadena no válida|(DM) el valor especificado para el argumento *BufferLength* era menor que 0.|  
|HY117|Conexión está suspendida debido al estado de transacción desconocido. Solo se desconecte y se permiten funciones de solo lectura.|(DM) para obtener más información sobre el estado suspendido, consulte [función SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYT01|Tiempo de espera de conexión agotado|Ha expirado el período de tiempo de espera de conexión antes de que el origen de datos que respondió a la solicitud. El período de tiempo de espera de conexión se establece a través de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Controlador no admite esta función|(DM) el controlador asociado con el *StatementHandle* no admite la función.|  
|IM017|Sondeo se deshabilita en modo de notificación asincrónica|Cada vez que se usa el modelo de notificación, se deshabilita el sondeo.|  
|IM018|**SQLCompleteAsync** no se ha llamado para completar la operación asincrónica anterior en este identificador.|Si la llamada de función anterior en el controlador devuelve SQL_STILL_EXECUTING y si está habilitado el modo de notificación, **SQLCompleteAsync** debe llamarse en el identificador para realizar el procesamiento posterior y completar la operación.|  
  
 **SQLDescribeCol** puede devolver cualquier SQLSTATE, que puede devolver **SQLPrepare** o **SQLExecute** cuando se llama después **SQLPrepare** y antes de **SQLExecute**, dependiendo de si el origen de datos se evalúa como la instrucción SQL asociada con el identificador de instrucción.  
  
 Por motivos de rendimiento, una aplicación no debe llamar a **SQLDescribeCol** antes de ejecutar una instrucción.  
  
## <a name="comments"></a>Comentarios  
 Normalmente, se llama una aplicación **SQLDescribeCol** después de llamar a **SQLPrepare** y antes o después de la llamada asociada a **SQLExecute**. También puede llamar una aplicación **SQLDescribeCol** después de llamar a **SQLExecDirect**. Para obtener más información, consulte [metadatos del conjunto de resultados](../../../odbc/reference/develop-app/result-set-metadata.md).  
  
 **SQLDescribeCol** recupera el nombre de columna, tipo y longitud generados por un **seleccione** instrucción. Si la columna es una expresión, **ColumnName* es una cadena vacía o un nombre definido por el controlador.  
  
> [!NOTE]  
>  ODBC admite SQL_NULLABLE_UNKNOWN como una extensión, aunque la especificación Open Group y el grupo de acceso SQL llamar a nivel de interfaz no especifica la opción para **SQLDescribeCol**.  
  
## <a name="related-functions"></a>Funciones relacionadas  
  
|Para obtener información acerca de|Vea|  
|---------------------------|---------|  
|Enlazar un búfer con una columna en un conjunto de resultados|[SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Procesamiento de una instrucción de cancelación|[SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Devolver información acerca de una columna en un conjunto de resultados|[SQLColAttribute](../../../odbc/reference/syntax/sqlcolattribute-function.md)|  
|Recopilación de varias filas de datos|[SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|Columnas del conjunto de devolver el número de resultados|[SQLNumResultCols](../../../odbc/reference/syntax/sqlnumresultcols-function.md)|  
|Preparar una instrucción de ejecución|[SQLPrepare](../../../odbc/reference/syntax/sqlprepare-function.md)|  
  
## <a name="see-also"></a>Vea también  
 [Referencia de la API de ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Archivos de encabezado de ODBC](../../../odbc/reference/install/odbc-header-files.md)
