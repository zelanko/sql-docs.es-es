---
title: Función SQLExtendedFetch | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLExtendedFetch
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLExtendedFetch
helpviewer_keywords:
- SQLExtendedFetch function [ODBC]
ms.assetid: 940b5cf7-581c-4ede-8533-c67d5e9ef488
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f1896ec473caf1af8a3fa2bdaa4156ddca3c0a6b
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47697054"
---
# <a name="sqlextendedfetch-function"></a>Función SQLExtendedFetch
**Conformidad**  
 Versión introdujo: Cumplimiento de estándares 1.0 de ODBC: desusado  
  
 **Resumen**  
 **SQLExtendedFetch** recupera el conjunto especificado filas de datos del conjunto de resultados y devuelve datos para todas las columnas enlazadas. Los conjuntos de filas pueden especificarse en una posición absoluta o relativa, o por el marcador.  
  
> [!NOTE]  
>  En ODBC 3 *.x*, **SQLExtendedFetch** ha sido reemplazado por **SQLFetchScroll**. ODBC 3 *.x* aplicaciones no deben llamar a **SQLExtendedFetch**; en su lugar debe llamar a **SQLFetchScroll**. Asigna el Administrador de controladores **SQLFetchScroll** a **SQLExtendedFetch** cuando se trabaja con un ODBC 2 *.x* controlador. ODBC 3 *.x* controladores deben admitir **SQLExtendedFetch** si desean trabajar con ODBC 2 *.x* aplicaciones que llaman a él. Para obtener más información, vea "Comentarios" y [cursores de bloque, cursores desplazables y compatibilidad con versiones anteriores](../../../odbc/reference/appendixes/block-cursors-scrollable-cursors-and-backward-compatibility.md) en Apéndice G: directrices de controlador para la compatibilidad con versiones anteriores.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
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
 [Entrada] Tipo de captura. Esto equivale a *FetchOrientation* en **SQLFetchScroll**.  
  
 *FetchOffset*  
 [Entrada] Número de la fila que se va a capturar. Esto equivale a *FetchOffset* en **SQLFetchScroll**, con una excepción. Cuando *FetchOrientation* es SQL_FETCH_BOOKMARK, *FetchOffset* es un marcador de longitud fija, no un desplazamiento de un marcador. En otras palabras, **SQLExtendedFetch** recupera el marcador de este argumento, no el atributo de instrucción SQL_ATTR_FETCH_BOOKMARK_PTR. No admite marcadores de longitud variable y no se admite la obtención de un conjunto de filas con un desplazamiento (distinto de 0) de un marcador.  
  
 *RowCountPtr*  
 [Salida] Puntero a un búfer en el que se va a devolver el número de filas recuperadas realmente. Este búfer se utiliza en la misma manera que el búfer especificado por el atributo de instrucción SQL_ATTR_ROWS_FETCHED_PTR. Este búfer se utiliza únicamente por **SQLExtendedFetch**. No se usa por **SQLFetch** o **SQLFetchScroll**.  
  
 *RowStatusArray*  
 [Salida] Puntero a una matriz en la que se va a devolver el estado de cada fila. Esta matriz se usa en la misma manera que la matriz especificada por el atributo de instrucción SQL_ATTR_ROW_STATUS_PTR.  
  
 Sin embargo, la dirección de esta matriz no se almacena en el campo SQL_DESC_STATUS_ARRAY_PTR IRD. Además, esta matriz se usa únicamente por **SQLExtendedFetch** y **SQLBulkOperations** con un *operación* de SQL_ADD o **SQLSetPos**cuando se llama después de **SQLExtendedFetch**. No se usa por **SQLFetch** o **SQLFetchScroll**, y no se utiliza por **SQLBulkOperations** o **SQLSetPos** cuando se llama después de **SQLFetch** o **SQLFetchScroll**. También no es se utiliza cuando **SQLBulkOperations** con un *operación* de SQL_ADD se llama antes de llama a cualquier función de captura. En otras palabras, se utiliza exclusivamente en el estado de la instrucción S7. No se utiliza en los Estados de instrucción S5 o S6. Para obtener más información, consulte [transiciones de instrucción](../../../odbc/reference/appendixes/statement-transitions.md) en tablas de transición de estado de apéndice B: ODBC.  
  
 Las aplicaciones deben proporcionar un puntero válido en el *RowStatusArray* argumento; en caso contrario, el comportamiento de **SQLExtendedFetch** y el comportamiento de las llamadas a **SQLBulkOperations**o **SQLSetPos** después de un cursor posicionó **SQLExtendedFetch** son indefinidos.  
  
## <a name="returns"></a>Devuelve  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NO_DATA, SQL_STILL_EXECUTING, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Cuando **SQLExtendedFetch** devuelve SQL_ERROR o SQL_SUCCESS_WITH_INFO, un valor SQLSTATE asociado se puede obtener mediante una llamada a **SQLError**. En la tabla siguiente se enumera los valores SQLSTATE devueltos normalmente por **SQLExtendedFetch** y se explica cada uno de ellos en el contexto de esta función; la notación "(DM)" precede a las descripciones de SQLSTATE devuelto por el Administrador de controladores. El código de retorno asociado a cada valor SQLSTATE es SQL_ERROR, a menos que se indique lo contrario. Si se produce un error en una sola columna, **SQLGetDiagField** se puede llamar con un *DiagIdentifier* de SQL_DIAG_COLUMN_NUMBER para determinar la columna que se produjo el error; y  **SQLGetDiagField** se puede llamar con un *DiagIdentifier* de SQL_DIAG_ROW_NUMBER para determinar la fila que contiene la columna.  
  
|SQLSTATE|Error|Descripción|  
|--------------|-----------|-----------------|  
|01000|Advertencia general|Específico del controlador de mensaje informativo. (La función devuelve SQL_SUCCESS_WITH_INFO).|  
|01004|Datos de cadena derecha truncados|Cadena o datos binarios devueltos para una columna produjeron el truncamiento de carácter no en blanco o datos binarios que no son NULL. Si fuese un valor de cadena, era truncado a la derecha. Si fuese un valor numérico, se trunca la parte fraccionaria del número.  (La función devuelve SQL_SUCCESS_WITH_INFO).|  
|01S01|Error en la fila|Se produjo un error al capturar una o varias filas. (La función devuelve SQL_SUCCESS_WITH_INFO).|  
|01S06|Se intentó buscar antes de que el conjunto de resultados devuelve el primer conjunto de filas|El conjunto de filas solicitado superpuesta el inicio del resultado establecer cuando la posición actual está más allá de la primera fila y, o bien *FetchOrientation* era SQL_PRIOR o *FetchOrientation* fue SQL_RELATIVE con un negativo *FetchOffset* cuyo valor absoluto era menor o igual que el SQL_ROWSET_SIZE actual. (La función devuelve SQL_SUCCESS_WITH_INFO).|  
|01S07|Truncamiento fraccionario|Se truncaron los datos devueltos para una columna. Para los tipos de datos numéricos, se ha truncado la parte fraccionaria del número. De hora, marca de tiempo y los tipos de datos de intervalo que contiene un componente de tiempo, se trunca la parte fraccionaria del tiempo.<br /><br /> (La función devuelve SQL_SUCCESS_WITH_INFO).|  
|07006|Infracción del atributo de tipo de datos restringido|No se pudo convertir un valor de datos para el tipo de datos C especificado *TargetType* en **SQLBindCol**.|  
|07009|Índice de descriptor no válido|La columna 0 se enlazó con **SQLBindCol**, y se ha establecido el atributo de instrucción SQL_ATTR_USE_BOOKMARKS a SQL_UB_OFF.|  
|08S01|Error de vínculo de comunicación|Error en el vínculo de comunicación entre el controlador y el origen de datos a la que se ha conectado el controlador antes del procesamiento de la función se ha completado.|  
|22002|Variable de indicador necesaria pero no proporcionado|Datos nulos se capturan en una columna cuya propiedad *StrLen_or_IndPtr* establecido por **SQLBindCol** era un puntero nulo.<br /><br /> (La función devuelve SQL_SUCCESS_WITH_INFO).|  
|22003|Valor numérico fuera del intervalo|Devolver el valor numérico (como numérico o cadena) para una o varias columnas, habría causado la parte entera (en contraposición a fraccionarios) del número que se va a truncar.<br /><br /> (La función devuelve SQL_SUCCESS_WITH_INFO).<br /><br /> Para obtener más información, consulte [directrices para el intervalo y los tipos de datos numéricos](../../../odbc/reference/appendixes/guidelines-for-interval-and-numeric-data-types.md) en Apéndice D: tipos de datos.|  
|22007|Formato de datetime no válido|Una columna de caracteres del conjunto de resultados se enlazó con una fecha, hora o estructura de marca de tiempo C y un valor en la columna era, respectivamente, una fecha no válida, la hora o marca de tiempo.<br /><br /> (La función devuelve SQL_SUCCESS_WITH_INFO).|  
|22012|División por cero|Devolvió un valor de una expresión aritmética, lo que resultó en la división por cero.<br /><br /> (La función devuelve SQL_SUCCESS_WITH_INFO).|  
|22015|Desbordamiento de campo de intervalo|Asignación de un valor numérico exacto o el intervalo de tipo SQL a un tipo de intervalo C causó una pérdida de dígitos significativos en el campo inicial.<br /><br /> Al capturar datos para un tipo de intervalo de C, no hubo ninguna representación del valor del tipo SQL en el tipo de intervalo C.<br /><br /> (La función devuelve SQL_SUCCESS_WITH_INFO).|  
|22018|Valor de carácter no válido para especificación cast|El tipo C era un numérico exacto o aproximado, una fecha y hora o un tipo de datos del intervalo; el tipo SQL de la columna era un tipo de datos de caracteres; y el valor de la columna no es un literal válido de tipo C enlazado.<br /><br /> (La función devuelve SQL_SUCCESS_WITH_INFO).|  
|24000|Estado de cursor no válido|El *StatementHandle* estaba en un estado ejecutado, pero se ha asociado ningún conjunto de resultados la *StatementHandle*.|  
|HY000|Error general|Se produjo un error para que se ha producido ningún SQLSTATE específico y para los que se ha definido ningún SQLSTATE específicos de la implementación. El mensaje de error devuelto por **SQLError** en el  *\*MessageText* búfer describe el error y su causa.|  
|HY001|Error de asignación de memoria|El controlador no pudo asignar la memoria necesaria para admitir la ejecución o la finalización de la función.|  
|HY008|Operación cancelada|Procesamiento asincrónico se habilitó para la *StatementHandle*. Se llamó a la función, y antes que completó la ejecución, **SQLCancel** o **SQLCancelHandle** se ha llamado en el *StatementHandle*, y, a continuación, se llamó a la función nuevo en el *StatementHandle*.<br /><br /> Se llamó a la función, y antes que completó la ejecución, **SQLCancel** o **SQLCancelHandle** se ha llamado en el *StatementHandle* desde un subproceso diferente en un aplicaciones multiproceso.|  
|HY010|Error de secuencia de función|(DM) se llamó a una función que se ejecuta de forma asincrónica para el identificador de conexión que está asociado el *StatementHandle*. Aún estaba ejecutando esta función asincrónica cuando el **SQLExtendedFetch** se llamó a la función.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, o **SQLMoreResults** se llamó para el *StatementHandle* y devuelven SQL_PARAM_DATA_ ESTÁ DISPONIBLE. Esta función se invoca antes de que se recuperan los datos para todos los parámetros transmitidos.<br /><br /> (DM) especificado *StatementHandle* no estaba en un estado ejecutado. Se llamó a la función sin llamar primero a **SQLExecDirect**, **SQLExecute**, o una función de catálogo.<br /><br /> (DM) se llamó a una función que se ejecuta asincrónicamente (no ésta) para el *StatementHandle* y aún se estaba ejecutando cuando se llamó a esta función.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, o **SQLSetPos** se llamó para el  *StatementHandle* y devuelve SQL_NEED_DATA. Esta función se invoca antes de que se enviaron datos para todas las columnas o parámetros de datos en ejecución.<br /><br /> (DM) **SQLExtendedFetch** se llamó para el *StatementHandle* después **SQLFetch** o **SQLFetchScroll** llamó y antes de  **SQLFreeStmt** se llamó con la opción de SQL_CLOSE.<br /><br /> (DM) **SQLBulkOperations** se llamó para una instrucción antes de **SQLFetch**, **SQLFetchScroll**, o **SQLExtendedFetch** llamó, y a continuación, **SQLExtendedFetch** se llamó antes **SQLFreeStmt** se llamó con la opción de SQL_CLOSE.|  
|HY013|Error de administración de memoria|No se pudo procesar la llamada de función porque los objetos de memoria subyacente no se podrían tener acceso, posiblemente debido a memoria insuficiente.|  
|HY106|Tipo de captura fuera del intervalo|(DM) el valor especificado para el argumento *FetchOrientation* no era válido. (Vea "Comentarios".)<br /><br /> El argumento *FetchOrientation* era SQL_FETCH_BOOKMARK y se ha establecido el atributo de instrucción SQL_ATTR_USE_BOOKMARKS a SQL_UB_OFF.<br /><br /> El valor de la opción de instrucción SQL_CURSOR_TYPE era SQL_CURSOR_FORWARD_ONLY y el valor del argumento *FetchOrientation* no era SQL_FETCH_NEXT.<br /><br /> El argumento *FetchOrientation* era SQL_FETCH_RESUME.|  
|HY107|Valor de fila fuera del intervalo|El valor especificado con la opción de instrucción SQL_CURSOR_TYPE era SQL_CURSOR_KEYSET_DRIVEN, pero el valor especificado con el atributo de instrucción SQL_KEYSET_SIZE era mayor que 0 y menor que el valor especificado con el atributo de instrucción SQL_ROWSET_SIZE .|  
|HY111|Valor de marcador no válido|El argumento *FetchOrientation* era SQL_FETCH_BOOKMARK y el marcador especificado en el *FetchOffset* argumento no era válido.|  
|HY117|Conexión está suspendida debido al estado de transacción desconocido. Solo se desconecte y se permiten funciones de solo lectura.|(DM) para obtener más información sobre el estado suspendido, consulte [función SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Característica opcional no implementada|Controlador u origen de datos no admite el tipo de captura especificada.<br /><br /> El controlador u origen de datos no admite la conversión especificada por la combinación de la *TargetType* en **SQLBindCol** y el tipo de datos SQL de la columna correspondiente. Este error se aplica solo cuando el tipo de datos SQL de la columna se asignó a un tipo de datos SQL específicas del controlador.|  
|HYT00|Se agotó el tiempo de espera|Ha expirado el período de tiempo de espera de consulta antes de que el origen de datos devuelva el conjunto de resultados. El período de tiempo de espera se establece a través de **SQLSetStmtOption**, SQL_QUERY_TIMEOUT.|  
|HYT01|Tiempo de espera de conexión agotado|Ha expirado el período de tiempo de espera de conexión antes de que el origen de datos que respondió a la solicitud. El período de tiempo de espera de conexión se establece a través de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Controlador no admite esta función|(DM) el controlador asociado con el *StatementHandle* no admite la función.|  
  
## <a name="comments"></a>Comentarios  
 El comportamiento de **SQLExtendedFetch** es idéntico de **SQLFetchScroll**, con las siguientes excepciones:  
  
-   **SQLExtendedFetch** y **SQLFetchScroll** usar varios métodos para devolver el número de filas recuperadas. **SQLExtendedFetch** devuelve el número de filas recuperadas en  *\*RowCountPtr*; **SQLFetchScroll** devuelve el número de filas recuperadas directamente en el búfer señalado por SQL_ATTR_ROWS_FETCHED_PTR. Para obtener más información, consulte el *RowCountPtr* argumento.  
  
-   **SQLExtendedFetch** y **SQLFetchScroll** devuelven el estado de cada fila en matrices distintas. Para obtener más información, consulte el *RowStatusArray* argumento.  
  
-   **SQLExtendedFetch** y **SQLFetchScroll** usar varios métodos para recuperar el marcador cuando *FetchOrientation* es SQL_FETCH_BOOKMARK. **SQLExtendedFetch** no es compatible con marcadores de longitud variable o al recuperar conjuntos de filas con un desplazamiento distinto de 0 de un marcador. Para obtener más información, consulte el *FetchOffset* argumento.  
  
-   **SQLExtendedFetch** y **SQLFetchScroll** usar tamaños diferentes conjuntos de filas. **SQLExtendedFetch** usa el valor del atributo de instrucción SQL_ROWSET_SIZE, y **SQLFetchScroll** usa el valor del atributo de instrucción SQL_ATTR_ROW_ARRAY_SIZE.  
  
-   **SQLExtendedFetch** tiene una semántica de control de errores ligeramente diferentes **SQLFetchScroll**. Para obtener más información, vea "Control de errores" en la sección "Comentarios" de [SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md).  
  
-   **SQLExtendedFetch** no es compatible con los desplazamientos de enlace (el atributo de instrucción SQL_ATTR_ROW_BIND_OFFSET_PTR).  
  
-   Las llamadas a **SQLExtendedFetch** no se pueden mezclar con las llamadas a **SQLFetch** o **SQLFetchScroll**y si **SQLBulkOperations** se denomina antes de llama a cualquier función de captura, **SQLExtendedFetch** no se puede llamar hasta que se cierra y vuelve a abrir el cursor. Es decir, **SQLExtendedFetch** puede llamarse únicamente en el estado de la instrucción S7. Para obtener más información, consulte [transiciones de instrucción](../../../odbc/reference/appendixes/statement-transitions.md) en tablas de transición de estado de apéndice B: ODBC.  
  
 Cuando una aplicación llama **SQLFetchScroll** al usar una 2 de ODBC *.x* controlador, el Administrador de controladores asigna esta llamada a **SQLExtendedFetch**. Para obtener más información, vea "SQLFetchScroll y ODBC 2 *.x* controladores" en [SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md).  
  
 En ODBC 2 *.x*, **SQLExtendedFetch** se llamó para capturar varias filas y **SQLFetch** se llamó para capturar una sola fila. En ODBC 3 *.x*, por otro lado, **SQLFetch** se puede llamar para capturar varias filas.  
  
## <a name="related-functions"></a>Funciones relacionadas  
  
|Para obtener información acerca de|Vea|  
|---------------------------|---------|  
|Enlazar un búfer con una columna en un conjunto de resultados|[Función SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Realizar operaciones de eliminación, actualización o inserción masiva|[Función SQLBulkOperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md)|  
|Procesamiento de una instrucción de cancelación|[Función SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Devolver información acerca de una columna en un conjunto de resultados|[Función SQLDescribeCol](../../../odbc/reference/syntax/sqldescribecol-function.md)|  
|Ejecutar una instrucción SQL|[Función SQLExecDirect](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|Ejecutar una instrucción SQL preparada|[Función SQLExecute](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|Columnas del conjunto de devolver el número de resultados|[Función SQLNumResultCols](../../../odbc/reference/syntax/sqlnumresultcols-function.md)|  
|Sitúe el cursor, actualizar los datos en el conjunto de filas, o actualizar o eliminar datos en el conjunto de resultados|[Función SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md)|  
|Establecer un atributo de instrucción|[Función SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>Vea también  
 [Referencia de la API de ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Archivos de encabezado de ODBC](../../../odbc/reference/install/odbc-header-files.md)
