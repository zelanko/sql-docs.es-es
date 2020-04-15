---
title: Función SQLExtendedFetch (SQLExtendedFetch) Microsoft Docs
ms.custom: ''
ms.date: 07/18/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLExtendedFetch
apilocation:
- sqlsrv32.dll
- odbc32.dll
apitype: dllExport
f1_keywords:
- SQLExtendedFetch
helpviewer_keywords:
- SQLExtendedFetch function [ODBC]
ms.assetid: 940b5cf7-581c-4ede-8533-c67d5e9ef488
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: dc832e5a20b1d3c0a1ad63b3e2a070563de2b46d
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81285985"
---
# <a name="sqlextendedfetch-function"></a>Función SQLExtendedFetch
**Conformidad**  
 Versión introducida: Cumplimiento de normas ODBC 1.0: en desuso  
  
 **Resumen**  
 **SQLExtendedFetch** recupera el conjunto de filas especificado de datos del conjunto de resultados y devuelve datos para todas las columnas enlazadas. Los conjuntos de filas se pueden especificar en una posición absoluta o relativa o por marcador.  
  
> [!NOTE]
>  En ODBC 3 *.x*, **SQLExtendedFetch** se ha reemplazado por **SQLFetchScroll**. Las aplicaciones ODBC 3 *.x* no deben llamar a **SQLExtendedFetch**; en su lugar, deben llamar a **SQLFetchScroll**. El Administrador de controladores asigna **SQLFetchScroll** a **SQLExtendedFetch** cuando se trabaja con un controlador ODBC 2 *.x.* Los controladores ODBC 3 *.x* deben admitir **SQLExtendedFetch** si desean trabajar con aplicaciones ODBC 2 *.x* que lo llamen. Para obtener más información, consulte "Comentarios" y cursores de [bloque, cursores desplazables y compatibilidad](../../../odbc/reference/appendixes/block-cursors-scrollable-cursors-and-backward-compatibility.md) con versiones anteriores en el Apéndice G: Directrices de controladores para la compatibilidad con versiones anteriores.  
  
## <a name="syntax"></a>Sintaxis  
  
```cpp  
  
SQLRETURN SQLExtendedFetch(  
      SQLHSTMT         StatementHandle,  
      SQLUSMALLINT     FetchOrientation,  
      SQLLEN           FetchOffset,  
      SQLULEN *        RowCountPtr,  
      SQLUSMALLINT *   RowStatusArray);  
```  
  
## <a name="arguments"></a>Argumentos  
 *StatementHandle*  
 [Entrada] Identificador de instrucción.  
  
 *FetchOrientation*  
 [Entrada] Tipo de captura. Esto es lo mismo que *FetchOrientation* en **SQLFetchScroll**.  
  
 *FetchOffset*  
 [Entrada] Número de la fila que se desea buscar. Esto es lo mismo que *FetchOffset* en **SQLFetchScroll**, con una excepción. Cuando *FetchOrientation* se SQL_FETCH_BOOKMARK, *FetchOffset* es un marcador de longitud fija, no un desplazamiento de un marcador. En otras palabras, **SQLExtendedFetch** recupera el marcador de este argumento, no el atributo de instrucción SQL_ATTR_FETCH_BOOKMARK_PTR. No admite marcadores de longitud variable y no admite la obtención de un conjunto de filas en un desplazamiento (distinto de 0) de un marcador.  
  
 *RowCountPtr*  
 [Salida] Puntero a un búfer en el que se va a devolver el número de filas realmente capturados. Este búfer se utiliza de la misma manera que el búfer especificado por el atributo de instrucción SQL_ATTR_ROWS_FETCHED_PTR. Este búfer solo lo utiliza **SQLExtendedFetch**. **SQLFetch** o **SQLFetchScroll**no lo utilizan.  
  
 *RowStatusArray*  
 [Salida] Puntero a una matriz en la que se va a devolver el estado de cada fila. Esta matriz se utiliza de la misma manera que la matriz especificada por el atributo de instrucción SQL_ATTR_ROW_STATUS_PTR.  
  
 Sin embargo, la dirección de esta matriz no se almacena en el campo SQL_DESC_STATUS_ARRAY_PTR del IRD. Además, esta matriz solo la utiliza **SQLExtendedFetch** y **SQLBulkOperations** con una *operación* de SQL_ADD o **SQLSetPos** cuando se llama después de **SQLExtendedFetch**. **SQLFetch** o **SQLFetchScroll**no lo utilizan y **SQLBulkOperations** o **SQLSetPos** no lo utilizan cuando se llaman después de **SQLFetch** o **SQLFetchScroll**. Tampoco se utiliza cuando **SQLBulkOperations** con una *operación* de SQL_ADD se llama antes de cualquier función de obtención se llama. En otras palabras, sólo se utiliza en el estado de instrucción S7. No se utiliza en los estados de instrucción S5 o S6. Para obtener más información, vea Transiciones de [instrucción](../../../odbc/reference/appendixes/statement-transitions.md) en el Apéndice B: Tablas de transición de estado ODBC.  
  
 Las aplicaciones deben proporcionar un puntero válido en el *RowStatusArray* argumento; Si no, el comportamiento de **SQLExtendedFetch** y el comportamiento de las llamadas a **SQLBulkOperations** o **SQLSetPos** después de que **SQLExtendedFetch** haya colocado un cursor son indefinidos.  
  
## <a name="returns"></a>Devuelve  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NO_DATA, SQL_STILL_EXECUTING, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnóstico  
 Cuando **SQLExtendedFetch** devuelve SQL_ERROR o SQL_SUCCESS_WITH_INFO, se puede obtener un valor SQLSTATE asociado llamando a **SQLError**. En la tabla siguiente se enumeran los valores SQLSTATE devueltos normalmente por **SQLExtendedFetch** y se explica cada uno de ellos en el contexto de esta función; la notación "(DM)" precede a las descripciones de SQLSTATEs devueltas por el Administrador de controladores. El código de retorno asociado a cada valor SQLSTATE se SQL_ERROR, a menos que se indique lo contrario. Si se produce un error en una sola columna, **SQLGetDiagField** se puede llamar con un *DiagIdentifier* de SQL_DIAG_COLUMN_NUMBER para determinar la columna en la que se produjo el error; y **SQLGetDiagField** se puede llamar con un *DiagIdentifier* de SQL_DIAG_ROW_NUMBER para determinar la fila que contiene esa columna.  
  
|SQLSTATE|Error|Descripción|  
|--------------|-----------|-----------------|  
|01000|Advertencia general|Mensaje informativo específico del controlador. (La función devuelve SQL_SUCCESS_WITH_INFO.)|  
|01004|Datos de cadena truncados a la derecha|Los datos de cadena o binarios devueltos para una columna dieron como resultado el truncamiento de caracteres no en blanco o datos binarios no NULL. Si era un valor de cadena, se truncaba a la derecha. Si era un valor numérico, la parte fraccionaria del número se truncó.  (La función devuelve SQL_SUCCESS_WITH_INFO.)|  
|01S01|Error en la fila|Se ha producido un error al capturar una o varias filas. (La función devuelve SQL_SUCCESS_WITH_INFO.)|  
|01S06|Intento de capturar antes de que el conjunto de resultados devolviera el primer conjunto de filas|El conjunto de filas solicitado superpuso el inicio del conjunto de resultados cuando la posición actual estaba más allá de la primera fila y *FetchOrientation* estaba SQL_PRIOR o *FetchOrientation* se SQL_RELATIVE con un *FetchOffset* negativo cuyo valor absoluto era menor o igual que el SQL_ROWSET_SIZE actual. (La función devuelve SQL_SUCCESS_WITH_INFO.)|  
|01S07|Truncamiento fraccionario|Los datos devueltos para una columna se truncaron. Para los tipos de datos numéricos, la parte fraccionaria del número se truncó. Para los tipos de datos time, timestamp e interval que contienen un componente de tiempo, la parte fraccionaria del tiempo se truncó.<br /><br /> (La función devuelve SQL_SUCCESS_WITH_INFO.)|  
|07006|Infracción de atributo de tipo de datos restringido|No se pudo convertir un valor de datos al tipo de datos c especificado por *TargetType* en **SQLBindCol**.|  
|07009|Indice de descriptor no válido|La columna 0 se enlazaba con **SQLBindCol**y el atributo de instrucción SQL_ATTR_USE_BOOKMARKS se estableció en SQL_UB_OFF.|  
|08S01|Fallo del enlace de comunicación|Error en el vínculo de comunicación entre el controlador y el origen de datos al que estaba conectado el controlador antes de que la función completara el procesamiento.|  
|22002|Variable indicador requerida pero no suministrada|Los datos NULL se capturaron en una columna cuyo *StrLen_or_IndPtr* establecido por **SQLBindCol** era un puntero nulo.<br /><br /> (La función devuelve SQL_SUCCESS_WITH_INFO.)|  
|22003|Valor numérico fuera del rango|Devolver el valor numérico (como numérico o cadena) para una o más columnas habría causado que se truncase la parte completa (en lugar de fraccionaria) del número.<br /><br /> (La función devuelve SQL_SUCCESS_WITH_INFO.)<br /><br /> Para obtener más información, consulte Directrices para tipos de [datos numéricos y](../../../odbc/reference/appendixes/guidelines-for-interval-and-numeric-data-types.md) de intervalo en apéndice D: tipos de datos.|  
|22007|Formato de fecha y hora no válido|Una columna de caracteres del conjunto de resultados estaba enlazada a una estructura C de fecha, hora o marca de tiempo, y un valor de la columna era, respectivamente, una fecha, hora o marca de tiempo no válidas.<br /><br /> (La función devuelve SQL_SUCCESS_WITH_INFO.)|  
|22012|División por cero|Se devolvió un valor de una expresión aritmética, lo que dio lugar a la división por cero.<br /><br /> (La función devuelve SQL_SUCCESS_WITH_INFO.)|  
|22015|Desbordamiento de campo de intervalo|La asignación de un tipo SQL numérico o de intervalo exacto a un tipo de intervalo C causó una pérdida de dígitos significativos en el campo inicial.<br /><br /> Al capturar datos en un tipo de intervalo C, no había ninguna representación del valor del tipo SQL en el tipo de intervalo C.<br /><br /> (La función devuelve SQL_SUCCESS_WITH_INFO.)|  
|22018|Valor de carácter no válido para la especificación de conversión|El tipo C era un número exacto o aproximado, una fecha y hora o un tipo de datos de intervalo; el tipo SQL de la columna era un tipo de datos de carácter; y el valor de la columna no era un literal válido del tipo C enlazado.<br /><br /> (La función devuelve SQL_SUCCESS_WITH_INFO.)|  
|24000|Estado de cursor no válido|El *StatementHandle* estaba en un estado ejecutado, pero no se asoció ningún conjunto de resultados con *StatementHandle*.|  
|HY000|Error general|Se ha producido un error para el que no se ha definido sqlSTATE específico y para el que no se ha definido sqlSTATE específico de la implementación. El mensaje de error devuelto por **SQLError** en el * \** búfer MessageText describe el error y su causa.|  
|HY001|Error de asignación de memoria|El controlador no pudo asignar la memoria necesaria para admitir la ejecución o finalización de la función.|  
|HY008|Operación cancelada|El procesamiento asincrónico se ha habilitado para *StatementHandle*. Se llamó a la función y antes de completar la ejecución, **sqlCancel** o **SQLCancelHandle** se llamó en el *StatementHandle*, y, a continuación, se llamó a la función de nuevo en el *StatementHandle*.<br /><br /> Se llamó a la función y antes de completar la ejecución, **SQLCancel** o **SQLCancelHandle** se llamó en el *StatementHandle* desde un subproceso diferente en una aplicación multiproceso.|  
|HY010|Error de secuencia de funciones|(DM) se llamó a una función de ejecución asincrónica para el identificador de conexión asociado a *StatementHandle*. Esta función asincrónica todavía se estaba ejecutando cuando se llamó a la función **SQLExtendedFetch** .<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**o **SQLMoreResults** se llamó para el *StatementHandle* y devuelto SQL_PARAM_DATA_AVAILABLE. Se llamó a esta función antes de recuperar los datos para todos los parámetros transmitidos.<br /><br /> (DM) el *StatementHandle* especificado no estaba en un estado ejecutado. Se llamó a la función sin llamar primero a **SQLExecDirect**, **SQLExecute**o una función de catálogo.<br /><br /> (DM) se llamó a una función de ejecución asincrónica (no esta) para el *StatementHandle* y todavía se estaba ejecutando cuando se llamó a esta función.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, o **SQLSetPos** se llamó para el *StatementHandle* y devuelto SQL_NEED_DATA. Se llamó a esta función antes de que se enviaran datos para todos los parámetros o columnas de datos en ejecución.<br /><br /> (DM) **SQLExtendedFetch** se llamó para el *StatementHandle* después **de SQLFetch** o **SQLFetchScroll** se llamó y antes **de SQLFreeStmt** se llamó con la SQL_CLOSE opción.<br /><br /> (DM) **SQLBulkOperations** se llamó para una instrucción antes de **SQLFetch**, **SQLFetchScroll**, o **SQLExtendedFetch** se llamó y, a continuación, **SQLExtendedFetch** se llamó antes **de SQLFreeStmt** se llamó con la opción SQL_CLOSE .|  
|HY013|Error de administración de memoria|No se pudo procesar la llamada de función porque no se pudo tener acceso a los objetos de memoria subyacentes, posiblemente debido a condiciones de poca memoria.|  
|HY106|Tipo de obtención fuera del rango|(DM) el valor especificado para el argumento *FetchOrientation* no era válido. (Véase "Comentarios.")<br /><br /> El argumento *FetchOrientation* se SQL_FETCH_BOOKMARK y el atributo de instrucción SQL_ATTR_USE_BOOKMARKS se estableció en SQL_UB_OFF.<br /><br /> El valor de la opción de instrucción SQL_CURSOR_TYPE se SQL_CURSOR_FORWARD_ONLY y el valor del argumento *FetchOrientation* no se SQL_FETCH_NEXT.<br /><br /> El argumento *FetchOrientation* se SQL_FETCH_RESUME.|  
|HY107|Valor de fila fuera del rango|El valor especificado con la opción de instrucción SQL_CURSOR_TYPE se SQL_CURSOR_KEYSET_DRIVEN, pero el valor especificado con el atributo de instrucción SQL_KEYSET_SIZE era mayor que 0 y menor que el valor especificado con el atributo de instrucción SQL_ROWSET_SIZE.|  
|HY111|Valor de marcador no válido|El argumento *FetchOrientation* se SQL_FETCH_BOOKMARK y el marcador especificado en el *FetchOffset* argumento no era válido.|  
|HY117|La conexión se suspende debido al estado de transacción desconocido. Solo se permiten funciones de desconexión y de solo lectura.|(DM) Para obtener más información sobre el estado suspendido, vea [SqlEndTran (función).](../../../odbc/reference/syntax/sqlendtran-function.md)|  
|HYC00|Característica opcional no implementada|El controlador o el origen de datos no admite el tipo de captura especificado.<br /><br /> El controlador o el origen de datos no admite la conversión especificada por la combinación de *TargetType* en **SQLBindCol** y el tipo de datos SQL de la columna correspondiente. Este error solo se aplica cuando el tipo de datos SQL de la columna se asignó a un tipo de datos SQL específico del controlador.|  
|HYT00|Tiempo de espera agotado|El período de tiempo de espera de la consulta expiró antes de que el origen de datos devolviera el conjunto de resultados. El período de tiempo de espera se establece a través de **SQLSetStmtOption**, SQL_QUERY_TIMEOUT.|  
|HYT01|Tiempo de espera de conexión expirado|El período de tiempo de espera de conexión expiró antes de que el origen de datos respondiera a la solicitud. El período de tiempo de espera de conexión se establece a través de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|El controlador no admite esta función|(DM) El controlador asociado con el *StatementHandle* no admite la función.|  
  
## <a name="comments"></a>Comentarios  
 El comportamiento de **SQLExtendedFetch** es idéntico al de **SQLFetchScroll**, con las siguientes excepciones:  
  
-   **SQLExtendedFetch** y **SQLFetchScroll** usan métodos diferentes para devolver el número de filas recuperadas. **SQLExtendedFetch** devuelve el número de filas recuperadas en * \*RowCountPtr*; **SQLFetchScroll** devuelve el número de filas obtenidas directamente en el búfer al que apunta SQL_ATTR_ROWS_FETCHED_PTR. Para obtener más información, vea el *RowCountPtr* argumento.  
  
-   **SQLExtendedFetch** y **SQLFetchScroll** devuelven el estado de cada fila en diferentes matrices. Para obtener más información, vea el *RowStatusArray* argumento.  
  
-   **SQLExtendedFetch** y **SQLFetchScroll** usan métodos diferentes para recuperar el marcador cuando *FetchOrientation* se SQL_FETCH_BOOKMARK. **SQLExtendedFetch** no admite marcadores de longitud variable ni la obtención de conjuntos de filas en un desplazamiento distinto de 0 de un marcador. Para obtener más información, vea el *FetchOffset* argumento.  
  
-   **SQLExtendedFetch** y **SQLFetchScroll** usan diferentes tamaños de conjunto de filas. **SQLExtendedFetch** utiliza el valor del atributo de instrucción SQL_ROWSET_SIZE y **SQLFetchScroll** utiliza el valor del atributo de instrucción SQL_ATTR_ROW_ARRAY_SIZE.  
  
-   **SQLExtendedFetch** tiene una semántica de control de errores ligeramente diferente que **SQLFetchScroll**. Para obtener más información, vea "Control de errores" en la sección "Comentarios" de [SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md).  
  
-   **SQLExtendedFetch** no admite desplazamientos de enlace (el atributo de instrucción SQL_ATTR_ROW_BIND_OFFSET_PTR).  
  
-   Las llamadas a **SQLExtendedFetch** no se pueden mezclar con llamadas a **SQLFetch** o **SQLFetchScroll**, y si se llama a **SQLBulkOperations** antes de llamar a cualquier función fetch, no se puede llamar a **SQLExtendedFetch** hasta que se cierre el cursor y se vuelva a abrir. Es decir, **SQLExtendedFetch** solo se puede llamar en el estado de instrucción S7. Para obtener más información, vea Transiciones de [instrucción](../../../odbc/reference/appendixes/statement-transitions.md) en el Apéndice B: Tablas de transición de estado ODBC.  
  
 Cuando una aplicación llama a **SQLFetchScroll** mientras se usa un controlador ODBC 2 *.x,* el Administrador de controladores asigna esta llamada a **SQLExtendedFetch**. Para obtener más información, vea "Controladores SQLFetchScroll y ODBC 2 *.x"* en [SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md).  
  
 En ODBC 2 *.x*, **SQLExtendedFetch** se llamó para capturar varias filas y **SQLFetch** se llamó para capturar una sola fila. En ODBC 3 *.x*, por otro lado, **SQLFetch** se puede llamar para capturar varias filas.  
  
## <a name="related-functions"></a>Funciones relacionadas  
  
|Para información acerca de|Vea|  
|---------------------------|---------|  
|Enlazar un búfer a una columna en un conjunto de resultados|[SQLBindCol (función)](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Realizar operaciones masivas de inserción, actualización o eliminación|[Función SQLBulkOperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md)|  
|Cancelación del procesamiento de extractos|[Función SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Devolver información sobre una columna en un conjunto de resultados|[SQLDescribeCol (función)](../../../odbc/reference/syntax/sqldescribecol-function.md)|  
|Ejecución de una instrucción SQL|[Función SQLExecDirect](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|Ejecución de una instrucción SQL preparada|[Función SQLExecute](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|Devolver el número de columnas del conjunto de resultados|[SQLNumResultCols (función)](../../../odbc/reference/syntax/sqlnumresultcols-function.md)|  
|Colocación del cursor, actualización de datos en el conjunto de filas o actualización o eliminación de datos en el conjunto de resultados|[Función SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md)|  
|Establecer un atributo de instrucción|[Función SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de la API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Archivos de encabezado de ODBC](../../../odbc/reference/install/odbc-header-files.md)
