---
title: Función SQLExtendedFetch | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
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
caps.latest.revision: 26
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1a02b1c2e050b6fc7a0724286c7f023cb376e7bb
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="sqlextendedfetch-function"></a>Función SQLExtendedFetch
**Conformidad**  
 Versión introdujo: Cumplimiento de estándares 1.0 de ODBC: en desuso  
  
 **Resumen**  
 **SQLExtendedFetch** recupera el conjunto especificado de filas de datos del conjunto de resultados y devuelve datos para todas las columnas enlazadas. Conjuntos de filas se pueden especificar en una posición absoluta o relativa o marcador.  
  
> [!NOTE]  
>  En ODBC 3 *.x*, **SQLExtendedFetch** se ha reemplazado por **SQLFetchScroll**. ODBC 3 *.x* aplicaciones no deben llamar a **SQLExtendedFetch**; en su lugar, debe llamar a **SQLFetchScroll**. Asigna el Administrador de controladores **SQLFetchScroll** a **SQLExtendedFetch** cuando se trabaja con una API ODBC 2 *.x* controlador. ODBC 3 *.x* controladores deben admitir **SQLExtendedFetch** si desean trabajar con ODBC 2 *.x* aplicaciones que llamen a él. Para obtener más información, vea "Comentarios" y [compatibilidad con versiones anteriores, los cursores desplazables y cursores de bloque](../../../odbc/reference/appendixes/block-cursors-scrollable-cursors-and-backward-compatibility.md) en Apéndice G: controlador directrices para la compatibilidad con versiones anteriores.  
  
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
 [Entrada] Número de la fila que se va a capturar. Esto equivale a *FetchOffset* en **SQLFetchScroll**, con una excepción. Cuando *FetchOrientation* es SQL_FETCH_BOOKMARK, *FetchOffset* es un marcador de longitud fija, no un desplazamiento de un marcador. En otras palabras, **SQLExtendedFetch** recupera el marcador de este argumento, no el atributo de instrucción SQL_ATTR_FETCH_BOOKMARK_PTR. No es compatible con marcadores de longitud variable y no admite la obtención de un conjunto de filas en un desplazamiento (distinto de 0) de un marcador.  
  
 *RowCountPtr*  
 [Salida] Puntero a un búfer en el que se va a devolver el número de filas recuperadas realmente. Este búfer se utiliza en la misma manera que el búfer especificado por el atributo de instrucción SQL_ATTR_ROWS_FETCHED_PTR. Este búfer se utiliza únicamente por **SQLExtendedFetch**. No se utiliza por **SQLFetch** o **SQLFetchScroll**.  
  
 *RowStatusArray*  
 [Salida] Puntero a una matriz en la que se va a devolver el estado de cada fila. Esta matriz se usa en la misma manera que la matriz especificada por el atributo de instrucción SQL_ATTR_ROW_STATUS_PTR.  
  
 Sin embargo, la dirección de esta matriz no se almacena en el campo SQL_DESC_STATUS_ARRAY_PTR IRD. Además, esta matriz se utiliza únicamente por **SQLExtendedFetch** y **SQLBulkOperations** con una *operación* de SQL_ADD o **SQLSetPos**cuando se llama después de **SQLExtendedFetch**. No se utiliza por **SQLFetch** o **SQLFetchScroll**, y no lo está usando **SQLBulkOperations** o **SQLSetPos** cuando se llama después de **SQLFetch** o **SQLFetchScroll**. También no es utiliza cuando **SQLBulkOperations** con una *operación* de SQL_ADD se llama antes de llama a cualquier función de captura. En otras palabras, se utiliza exclusivamente en el estado de la instrucción S7. No se utiliza en Estados de instrucción S5 o S6. Para obtener más información, consulte [instrucción transiciones](../../../odbc/reference/appendixes/statement-transitions.md) en tablas de transición de estado de apéndice B: ODBC.  
  
 Las aplicaciones deben proporcionar un puntero válido en el *RowStatusArray* argumento; en caso contrario, el comportamiento de **SQLExtendedFetch** y el comportamiento de las llamadas a **SQLBulkOperations**o **SQLSetPos** después de que se ha colocado un cursor por **SQLExtendedFetch** son indefinidos.  
  
## <a name="returns"></a>Devuelve  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NO_DATA, SQL_STILL_EXECUTING, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Cuando **SQLExtendedFetch** devuelve SQL_ERROR o SQL_SUCCESS_WITH_INFO, un valor SQLSTATE asociado se puede obtener mediante una llamada a **SQLError**. En la tabla siguiente se enumera los valores SQLSTATE devueltos normalmente por **SQLExtendedFetch** y se explica cada uno de ellos en el contexto de esta función; la notación "(DM)" precede a las descripciones de SQLSTATE devuelto por el Administrador de controladores. El código de retorno asociado a cada valor SQLSTATE es SQL_ERROR, a menos que se indique lo contrario. Si se produce un error en una sola columna, **SQLGetDiagField** se puede llamar con un *DiagIdentifier* de SQL_DIAG_COLUMN_NUMBER para determinar la columna que se produjo el error; y  **SQLGetDiagField** se puede llamar con un *DiagIdentifier* de SQL_DIAG_ROW_NUMBER para determinar la fila que contiene la columna.  
  
|SQLSTATE|Error|Description|  
|--------------|-----------|-----------------|  
|01000|Advertencia general|Mensaje informativo de específicas del controlador. (La función devuelve SQL_SUCCESS_WITH_INFO).|  
|01004|Datos de cadena, delimitado truncados|Cadena o datos binarios devueltos para una columna generó el truncamiento de carácter que no esté vacía o datos binarios no NULL. Si ha realizado un valor de cadena, era truncado a la derecha. Si es un valor numérico, se trunca la parte fraccionaria del número.  (La función devuelve SQL_SUCCESS_WITH_INFO).|  
|01S01|Error en la fila|Se produjo un error al capturar una o varias filas. (La función devuelve SQL_SUCCESS_WITH_INFO).|  
|01S06|Intento de recuperación antes el conjunto de resultados devolviera el primer conjunto de filas|El conjunto de filas solicitado superpuesta el inicio del conjunto de resultados cuando la posición actual fue más allá de la primera fila y bien *FetchOrientation* era SQL_PRIOR o *FetchOrientation* era SQL_RELATIVE con un negativo *FetchOffset* cuyo valor absoluto era menor o igual que el SQL_ROWSET_SIZE actual. (La función devuelve SQL_SUCCESS_WITH_INFO).|  
|01S07|Truncamiento fraccionario|Se truncaron los datos devueltos para una columna. Para los tipos de datos numéricos, se trunca la parte fraccionaria del número. De hora, marca de tiempo y los tipos de datos interval que contiene un componente de tiempo, se trunca la parte fraccionaria del tiempo.<br /><br /> (La función devuelve SQL_SUCCESS_WITH_INFO).|  
|07006|Infracción del atributo de tipo de datos restringido|Un valor de datos no se pudo convertir al tipo de datos C especificado por *TargetType* en **SQLBindCol**.|  
|07009|Índice de descriptor no válido|La columna 0 se enlazó con **SQLBindCol**, y el atributo de instrucción SQL_ATTR_USE_BOOKMARKS estaba establecido como SQL_UB_OFF.|  
|08S01|Error de vínculo de comunicación|El vínculo de comunicación entre el controlador y el origen de datos al que se conectó el controlador no pudo antes del procesamiento de la función se ha completado.|  
|22002|Variable de indicador necesaria, pero no se ha suministrado|Datos nulos se capturan en una columna cuyo *StrLen_or_IndPtr* establecido por **SQLBindCol** era un puntero nulo.<br /><br /> (La función devuelve SQL_SUCCESS_WITH_INFO).|  
|22003|Valor numérico fuera del intervalo|Devolver el valor numérico (como numérico o cadena) para una o varias columnas, habría provocado la parte entera (en lugar de fracciones) del número se trunque.<br /><br /> (La función devuelve SQL_SUCCESS_WITH_INFO).<br /><br /> Para obtener más información, consulte [directrices para el intervalo y los tipos de datos numéricos](../../../odbc/reference/appendixes/guidelines-for-interval-and-numeric-data-types.md) en tipos de datos de apéndice D:.|  
|22007|Formato de datetime no válido|Una columna de caracteres del conjunto de resultados se enlazó a una fecha, hora o estructura de marca de tiempo C, y un valor en la columna era, respectivamente, una fecha no válida, una hora o una marca de tiempo.<br /><br /> (La función devuelve SQL_SUCCESS_WITH_INFO).|  
|22012|División por cero|Devolvió un valor de una expresión aritmética, lo que provocó de división por cero.<br /><br /> (La función devuelve SQL_SUCCESS_WITH_INFO).|  
|22015|Desbordamiento del campo de intervalo|Asignación de un valor numérico exacto o el intervalo de tipo SQL a un tipo de intervalo C causó una pérdida de dígitos significativos en el campo inicial.<br /><br /> Al capturar datos para un tipo de intervalo C, no había ninguna representación del valor del tipo de SQL en el tipo de intervalo C.<br /><br /> (La función devuelve SQL_SUCCESS_WITH_INFO).|  
|22018|Valor de carácter no válido para especificación cast|El tipo C era un numérico exacto o aproximado, una fecha y hora o un tipo de datos del intervalo; el tipo SQL de la columna era un tipo de datos character; y el valor de la columna no es un literal válido del tipo de C enlazado.<br /><br /> (La función devuelve SQL_SUCCESS_WITH_INFO).|  
|24000|Estado de cursor no válido|El *StatementHandle* estaba en un estado ejecutado, pero ningún conjunto de resultados se asoció el *StatementHandle*.|  
|HY000|Error general|Se produjo un error para que no hubo ninguna SQLSTATE específico y para el que se ha definido ningún SQLSTATE específico de la implementación. El mensaje de error devuelto por **SQLError** en el  *\*MessageText* búfer describe el error y su causa.|  
|HY001|Error de asignación de memoria|El controlador no pudo asignar la memoria necesaria para admitir la ejecución o la finalización de la función.|  
|HY008|Operación cancelada|Procesamiento asincrónico se habilitó para la *StatementHandle*. Se llamó a la función y antes que completó la ejecución, **SQLCancel** o **SQLCancelHandle** se llamó en la *StatementHandle*, y, a continuación, se llama a la función de nuevo en el *StatementHandle*.<br /><br /> Se llamó a la función y antes que completó la ejecución, **SQLCancel** o **SQLCancelHandle** se llamó en la *StatementHandle* desde un subproceso distinto en un aplicaciones multiproceso.|  
|HY010|Error de secuencia de función|(DM) se llamó a una función ejecuta de forma asincrónica para el identificador de conexión que está asociado el *StatementHandle*. Esta función asincrónica aún estaba ejecutando cuando el **SQLExtendedFetch** se llamó la función.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, o **SQLMoreResults** se llamó para el *StatementHandle* devolvió SQL_PARAM_DATA_ ESTÁ DISPONIBLE. Esta función se invoca antes de que se recuperan los datos para todos los parámetros transmitidos.<br /><br /> (DM) especificado *StatementHandle* no estaba en un estado ejecutado. Se llamó a la función sin antes de llamar a **SQLExecDirect**, **SQLExecute**, o una función de catálogo.<br /><br /> (DM) se llamó a una función ejecuta de forma asincrónica (no esta uno) para la *StatementHandle* y aún se estaba ejecutando cuando se llamó a esta función.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, o **SQLSetPos** se llamó para el  *StatementHandle* y devuelve SQL_NEED_DATA. Esta función se invoca antes de que se enviaron los datos para todas las columnas o parámetros de datos en ejecución.<br /><br /> (DM) **SQLExtendedFetch** se llamó para el *StatementHandle* después **SQLFetch** o **SQLFetchScroll** se llamó y antes de  **SQLFreeStmt** se llamó con la opción de SQL_CLOSE.<br /><br /> (DM) **SQLBulkOperations** se llamó para una instrucción antes de **SQLFetch**, **SQLFetchScroll**, o **SQLExtendedFetch** se llamó, y a continuación, **SQLExtendedFetch** se llamó antes de **SQLFreeStmt** se llamó con la opción de SQL_CLOSE.|  
|HY013|Error de administración de memoria|No se pudo procesar la llamada de función porque los objetos subyacentes de la memoria no se pudieron tener acceso, posiblemente debido a condiciones de memoria insuficiente.|  
|HY106|Tipo de captura fuera del intervalo|(DM) el valor especificado para el argumento *FetchOrientation* no era válido. (Vea "Comentarios".)<br /><br /> El argumento *FetchOrientation* era SQL_FETCH_BOOKMARK, y se estableció el atributo de instrucción de SQL_ATTR_USE_BOOKMARKS en SQL_UB_OFF.<br /><br /> El valor de la opción de instrucción SQL_CURSOR_TYPE era SQL_CURSOR_FORWARD_ONLY y el valor del argumento *FetchOrientation* no era SQL_FETCH_NEXT.<br /><br /> El argumento *FetchOrientation* era SQL_FETCH_RESUME.|  
|HY107|Valor de fila fuera del intervalo|El valor especificado con la opción de instrucción SQL_CURSOR_TYPE SQL_CURSOR_KEYSET_DRIVEN, pero el valor especificado con el atributo de instrucción de SQL_KEYSET_SIZE es mayor que 0 y menor que el valor especificado con el atributo de instrucción SQL_ROWSET_SIZE .|  
|HY111|Valor de marcador no válido|El argumento *FetchOrientation* era SQL_FETCH_BOOKMARK y el marcador especificado en el *FetchOffset* argumento no era válido.|  
|HY117|Se suspende la conexión debido al estado de transacción desconocido. Solo se desconecte y se permiten las funciones de solo lectura.|(DM) para obtener más información sobre el estado suspendido, consulte [función SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Característica opcional no implementada|Controlador u origen de datos no admite el tipo de captura especificado.<br /><br /> El controlador u origen de datos no admite la conversión especificada por la combinación de la *TargetType* en **SQLBindCol** y el tipo de datos SQL de la columna correspondiente. Este error se aplica sólo cuando el tipo de datos SQL de la columna se ha asignado a un tipo de datos SQL específico del controlador.|  
|HYT00|Se agotó el tiempo de espera|El período de tiempo de espera de consulta finalizó antes de que el origen de datos devuelve el conjunto de resultados. El período de tiempo de espera se establece a través de **SQLSetStmtOption**, SQL_QUERY_TIMEOUT.|  
|HYT01|Tiempo de espera de conexión expirado|El período de tiempo de espera de conexión finalizó antes de que el origen de datos se respondió a la solicitud. El período de tiempo de espera de conexión se establece a través de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Controlador no admite esta función|(DM) el controlador asociado a la *StatementHandle* no admite la función.|  
  
## <a name="comments"></a>Comentarios  
 El comportamiento de **SQLExtendedFetch** es idéntico de **SQLFetchScroll**, con las siguientes excepciones:  
  
-   **SQLExtendedFetch** y **SQLFetchScroll** utilizar métodos distintos para devolver el número de filas recuperadas. **SQLExtendedFetch** devuelve el número de filas recuperadas en  *\*RowCountPtr*; **SQLFetchScroll** devuelve el número de filas recuperadas directamente en el búfer señalado por SQL_ATTR_ROWS_FETCHED_PTR. Para obtener más información, consulte el *RowCountPtr* argumento.  
  
-   **SQLExtendedFetch** y **SQLFetchScroll** devolver el estado de cada fila en diferentes arreglos de discos. Para obtener más información, consulte el *RowStatusArray* argumento.  
  
-   **SQLExtendedFetch** y **SQLFetchScroll** usar varios métodos para recuperar el marcador cuando *FetchOrientation* es SQL_FETCH_BOOKMARK. **SQLExtendedFetch** no es compatible con marcadores de longitud variable o conjuntos de filas de captura en un desplazamiento distinto de 0 de un marcador. Para obtener más información, consulte el *FetchOffset* argumento.  
  
-   **SQLExtendedFetch** y **SQLFetchScroll** usar tamaños diferentes conjuntos de filas. **SQLExtendedFetch** utiliza el valor del atributo de instrucción SQL_ROWSET_SIZE, y **SQLFetchScroll** utiliza el valor del atributo de instrucción SQL_ATTR_ROW_ARRAY_SIZE.  
  
-   **SQLExtendedFetch** tiene una semántica de control de errores ligeramente diferente **SQLFetchScroll**. Para obtener más información, vea "Control de errores" en la sección "Comentarios" de [SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md).  
  
-   **SQLExtendedFetch** no es compatible con los desplazamientos de enlace (el atributo de instrucción de SQL_ATTR_ROW_BIND_OFFSET_PTR).  
  
-   Las llamadas a **SQLExtendedFetch** no se pueden mezclar con las llamadas a **SQLFetch** o **SQLFetchScroll**y si **SQLBulkOperations** se llama antes de llama a cualquier función de captura, **SQLExtendedFetch** no se puede llamar hasta que se cierra y se vuelve a abrir el cursor. Es decir, **SQLExtendedFetch** puede llamarse únicamente en el estado de la instrucción S7. Para obtener más información, consulte [instrucción transiciones](../../../odbc/reference/appendixes/statement-transitions.md) en tablas de transición de estado de apéndice B: ODBC.  
  
 Cuando una aplicación llama **SQLFetchScroll** durante el uso de una API ODBC 2 *.x* controlador, el Administrador de controladores asigna esta llamada a **SQLExtendedFetch**. Para obtener más información, vea "SQLFetchScroll y ODBC 2 *.x* controladores" en [SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md).  
  
 En ODBC 2 *.x*, **SQLExtendedFetch** se llamó para capturar varias filas y **SQLFetch** se llamó para capturar una sola fila. En ODBC 3 *.x*, por otro lado, **SQLFetch** puede llamarse para capturar varias filas.  
  
## <a name="related-functions"></a>Funciones relacionadas  
  
|Para obtener información acerca de|Vea|  
|---------------------------|---------|  
|Enlazar un búfer con una columna en un conjunto de resultados|[Función SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Realizar operación bulk insert, update o las operaciones de eliminación|[Función SQLBulkOperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md)|  
|Cancelar el procesamiento de una instrucción|[Función SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Devolver información acerca de una columna en un conjunto de resultados|[Función SQLDescribeCol](../../../odbc/reference/syntax/sqldescribecol-function.md)|  
|Ejecutar una instrucción SQL|[Función SQLExecDirect](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|Ejecutar una instrucción SQL preparada|[Función SQLExecute](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|Columnas del conjunto de devolver el número de resultados|[Función SQLNumResultCols](../../../odbc/reference/syntax/sqlnumresultcols-function.md)|  
|Coloque el cursor, actualizar los datos en el conjunto de filas, o actualizar o eliminar datos en el conjunto de resultados|[Función SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md)|  
|Establecer un atributo de instrucción|[Función SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>Vea también  
 [Referencia de la API de ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Archivos de encabezado de ODBC](../../../odbc/reference/install/odbc-header-files.md)
