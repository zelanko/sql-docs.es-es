---
title: Función SQLFetchScroll ( SQLFetchScroll Function) Microsoft Docs
ms.custom: ''
ms.date: 07/18/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLFetchScroll
apilocation:
- sqlsrv32.dll
- odbc32.dll
apitype: dllExport
f1_keywords:
- SQLFetchScroll
helpviewer_keywords:
- SQLFetchScroll function [ODBC]
ms.assetid: c0243667-428c-4dda-ae91-3c307616a1ac
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b6c65ef71f5c2cb9202ab788cac5e00357674f4a
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81285885"
---
# <a name="sqlfetchscroll-function"></a>Función SQLFetchScroll
**Conformidad**  
 Versión introducida: Cumplimiento de normas ODBC 3.0: ISO 92  
  
 **Resumen**  
 **SQLFetchScroll** recupera el conjunto de filas especificado de datos del conjunto de resultados y devuelve datos para todas las columnas enlazadas. Los conjuntos de filas se pueden especificar en una posición absoluta o relativa o por marcador.  
  
 Cuando se trabaja con un controlador ODBC 2.x, el Administrador de controladores asigna esta función a **SQLExtendedFetch**. Para obtener más información, consulte Asignación de [funciones de reemplazo para la compatibilidad con versiones anteriores de aplicaciones](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md).  
  
## <a name="syntax"></a>Sintaxis  
  
```cpp  
  
SQLRETURN SQLFetchScroll(  
      SQLHSTMT      StatementHandle,  
      SQLSMALLINT   FetchOrientation,  
      SQLLEN        FetchOffset);  
```  
  
## <a name="arguments"></a>Argumentos  
 *StatementHandle*  
 [Entrada] Identificador de instrucción.  
  
 *FetchOrientation*  
 [Entrada]  
  
 Tipo de captura:  
  
 SQL_FETCH_NEXT  
  
 SQL_FETCH_PRIOR  
  
 SQL_FETCH_FIRST  
  
 SQL_FETCH_LAST  
  
 SQL_FETCH_ABSOLUTE  
  
 SQL_FETCH_RELATIVE  
  
 SQL_FETCH_BOOKMARK  
  
 Para obtener más información, consulte "Posición del cursor" en la sección "Comentarios".  
  
 *FetchOffset*  
 [Entrada]  
  
 Número de la fila que se desea buscar. La interpretación de este argumento depende del valor de la *FetchOrientation* argumento. Para obtener más información, consulte "Posición del cursor" en la sección "Comentarios".  
  
## <a name="returns"></a>Devuelve  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NO_DATA, SQL_STILL_EXECUTING, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnóstico  
 Cuando **SQLFetchScroll** devuelve SQL_ERROR o SQL_SUCCESS_WITH_INFO, se puede obtener un valor SQLSTATE asociado llamando a **SQLGetDiagRec** con un HandleType de SQL_HANDLE_STMT y un handle of StatementHandle. En la tabla siguiente se enumeran los valores SQLSTATE devueltos normalmente por **SQLFetchScroll** y se explica cada uno de ellos en el contexto de esta función; la notación "(DM)" precede a las descripciones de SQLSTATEs devueltas por el Administrador de controladores. El código de retorno asociado a cada valor SQLSTATE se SQL_ERROR, a menos que se indique lo contrario. Si se produce un error en una sola columna, **SQLGetDiagField** se puede llamar con un DiagIdentifier de SQL_DIAG_COLUMN_NUMBER para determinar la columna en la que se produjo el error; y **SQLGetDiagField** se puede llamar con un DiagIdentifier de SQL_DIAG_ROW_NUMBER para determinar la fila que contiene esa columna.  
  
 Para todos aquellos SQLSTATEs que pueden devolver SQL_SUCCESS_WITH_INFO o SQL_ERROR (excepto 01xxx SQLSTATEs), se devuelve SQL_SUCCESS_WITH_INFO si se produce un error en una o más filas, pero no en todas, de una operación de varias filas y SQL_ERROR se devuelve si se produce un error en una operación de una sola fila.  
  
|SQLSTATE|Error|Descripción|  
|--------------|-----------|-----------------|  
|01000|Advertencia general|Mensaje informativo específico del controlador. (La función devuelve SQL_SUCCESS_WITH_INFO.)|  
|01004|Datos de cadena truncados a la derecha|Los datos de cadena o binarios devueltos para una columna dieron como resultado el truncamiento de caracteres no en blanco o datos binarios no NULL. Si era un valor de cadena, se truncaba a la derecha.|  
|01S01|Error en la fila|Se ha producido un error al capturar una o varias filas.<br /><br /> (Si se devuelve este SQLSTATE cuando una aplicación ODBC 3 *.x* está trabajando con un controlador ODBC 2 *.x,* se puede omitir.)|  
|01S06|Intento de capturar antes de que el conjunto de resultados devolviera el primer conjunto de filas|El conjunto de filas solicitado superpuso el inicio del conjunto de resultados cuando FetchOrientation se SQL_FETCH_PRIOR, la posición actual estaba más allá de la primera fila y el número de la fila actual es menor o igual que el tamaño del conjunto de filas.<br /><br /> El conjunto de filas solicitado superpuso el inicio del conjunto de resultados cuando FetchOrientation se SQL_FETCH_PRIOR, la posición actual estaba más allá del final del conjunto de resultados y el tamaño del conjunto de filas era mayor que el tamaño del conjunto de resultados.<br /><br /> El conjunto de filas solicitado superpuso el inicio del conjunto de resultados cuando FetchOrientation se SQL_FETCH_RELATIVE, FetchOffset era negativo y el valor absoluto de FetchOffset era menor o igual que el tamaño del conjunto de filas.<br /><br /> El conjunto de filas solicitado superpuso el inicio del conjunto de resultados cuando FetchOrientation se SQL_FETCH_ABSOLUTE, FetchOffset era negativo y el valor absoluto de FetchOffset era mayor que el tamaño del conjunto de resultados, pero menor o igual que el tamaño del conjunto de filas.<br /><br /> (La función devuelve SQL_SUCCESS_WITH_INFO.)|  
|01S07|Truncamiento fraccionario|Los datos devueltos para una columna se truncaron. Para los tipos de datos numéricos, la parte fraccionaria del número se truncó. Para los tipos de datos time, timestamp e interval que contienen un componente de tiempo, la parte fraccionaria del tiempo se truncó.<br /><br /> (La función devuelve SQL_SUCCESS_WITH_INFO.)|  
|07006|Infracción de atributo de tipo de datos restringido|El valor de datos de una columna del conjunto de resultados no se pudo convertir al tipo de datos especificado por *TargetType* en **SQLBindCol**.<br /><br /> La columna 0 se enlazaba con un tipo de datos de SQL_C_BOOKMARK y el atributo de instrucción SQL_ATTR_USE_BOOKMARKS se estableció en SQL_UB_VARIABLE.<br /><br /> La columna 0 se enlazaba con un tipo de datos de SQL_C_VARBOOKMARK y el atributo de instrucción SQL_ATTR_USE_BOOKMARKS no se estableció en SQL_UB_VARIABLE.|  
|07009|Indice de descriptor no válido|El controlador era un controlador ODBC 2 *.x* que no admite **SQLExtendedFetch**y un número de columna especificado en el enlace para una columna era 0.<br /><br /> La columna 0 estaba enlazada y el atributo de instrucción SQL_ATTR_USE_BOOKMARKS se estableció en SQL_UB_OFF.|  
|08S01|Fallo del enlace de comunicación|Error en el vínculo de comunicación entre el controlador y el origen de datos al que estaba conectado el controlador antes de que la función completara el procesamiento.|  
|22001|Datos de cadena truncados a la derecha|Se ha truncado un marcador de longitud variable devuelto para una columna.|  
|22002|Variable indicador requerida pero no suministrada|Los datos NULL se capturaron en una columna cuyo *StrLen_or_IndPtr* establecido por **SQLBindCol** (o SQL_DESC_INDICATOR_PTR establecido por **SQLSetDescField** o **SQLSetDescRec**) era un puntero nulo.|  
|22003|Valor numérico fuera del rango|Devolver el valor numérico (como numérico o cadena) para una o más columnas enlazadas habría causado que se truncase la parte completa (en lugar de fraccionaria) del número.<br /><br /> Para obtener más información, vea [Convertir datos de SQL a tipos](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md) de datos C en Apéndice [D: Tipos](../../../odbc/reference/appendixes/appendix-d-data-types.md)de datos .|  
|22007|Formato de fecha y hora no válido|Una columna de caracteres del conjunto de resultados estaba enlazada a una estructura C de fecha, hora o marca de tiempo, y un valor de la columna era, respectivamente, una fecha, hora o marca de tiempo no válidas.|  
|22012|División por cero|Se devolvió un valor de una expresión aritmética, lo que dio lugar a la división por cero.|  
|22015|Desbordamiento de campo de intervalo|La asignación de un tipo SQL numérico o de intervalo exacto a un tipo de intervalo C causó una pérdida de dígitos significativos en el campo inicial.<br /><br /> Al capturar datos en un tipo de intervalo C, no había ninguna representación del valor del tipo SQL en el tipo de intervalo C.|  
|22018|Valor de carácter no válido para la especificación de conversión|Una columna de caracteres del conjunto de resultados estaba enlazada a un búfer de caracteres C y la columna contenía un carácter para el que no había ninguna representación en el conjunto de caracteres del búfer.<br /><br /> El tipo C era un número exacto o aproximado, una fecha y hora o un tipo de datos de intervalo; el tipo SQL de la columna era un tipo de datos de carácter; y el valor de la columna no era un literal válido del tipo C enlazado.|  
|24000|Estado de cursor no válido|El *StatementHandle* estaba en un estado ejecutado, pero no se asoció ningún conjunto de resultados con *StatementHandle*.|  
|40001|Error de serialización|La transacción en la que se ejecutó la captura se ha terminado para evitar el interbloqueo.|  
|40003|Finalización de la declaración desconocida|Error en la conexión asociada durante la ejecución de esta función y no se puede determinar el estado de la transacción.|  
|HY000|Error general|Se ha producido un error para el que no se ha definido sqlSTATE específico y para el que no se ha definido sqlSTATE específico de la implementación. El mensaje de error devuelto por **SQLGetDiagRec** en el * \*messageText* búfer describe el error y su causa.|  
|HY001|Error de asignación de memoria|El controlador no pudo asignar la memoria necesaria para admitir la ejecución o finalización de la función.|  
|HY008|Operación cancelada|El procesamiento asincrónico se ha habilitado para *StatementHandle*. Se llamó a la función y antes de completar la ejecución, **SQLCancel** o **SQLCancelHandle** se llamó en el *StatementHandle*. A continuación, se volvió a llamar a la función en *StatementHandle*.<br /><br /> Se llamó a la función y antes de completar la ejecución, **SQLCancel** o **SQLCancelHandle** se llamó en el *StatementHandle* desde un subproceso diferente en una aplicación multiproceso.|  
|HY010|Error de secuencia de funciones|(DM) se llamó a una función de ejecución asincrónica para el identificador de conexión asociado a *StatementHandle*. Esta función asincrónica todavía se estaba ejecutando cuando se llamó a la función **SQLFetchScroll** .<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**o **SQLMoreResults** se llamó para el *StatementHandle* y devuelto SQL_PARAM_DATA_AVAILABLE. Se llamó a esta función antes de recuperar los datos para todos los parámetros transmitidos.<br /><br /> (DM) el *StatementHandle* especificado no estaba en un estado ejecutado. Se llamó a la función sin llamar primero a **SQLExecDirect**, **SQLExecute** o una función de catálogo.<br /><br /> (DM) se llamó a una función de ejecución asincrónica (no esta) para el *StatementHandle* y todavía se estaba ejecutando cuando se llamó a esta función.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, o **SQLSetPos** se llamó para el *StatementHandle* y devuelto SQL_NEED_DATA. Se llamó a esta función antes de que se enviaran datos para todos los parámetros o columnas de datos en ejecución.<br /><br /> (DM) **SQLFetch** se llamó para el *StatementHandle* después **de SQLExtendedFetch** se llamó y antes **de SQLFreeStmt** con el SQL_CLOSE opción se llamó.|  
|HY013|Error de administración de memoria|No se pudo procesar la llamada de función porque no se pudo tener acceso a los objetos de memoria subyacentes, posiblemente debido a condiciones de poca memoria.|  
|HY090|Cadena no válida o longitud de búfer|El atributo de instrucción SQL_ATTR_USE_BOOKMARK se estableció en SQL_UB_VARIABLE y la columna 0 se enlazaba a un búfer cuya longitud no era igual a la longitud máxima del marcador para este conjunto de resultados. (Esta longitud está disponible en el campo SQL_DESC_OCTET_LENGTH del IRD y se puede obtener llamando a **SQLDescribeCol**, **SQLColAttribute**o **SQLGetDescField**.)|  
|HY106|Tipo de obtención fuera del rango|DM) el valor especificado para el argumento FetchOrientation no era válido.<br /><br /> (DM) el argumento FetchOrientation se SQL_FETCH_BOOKMARK y el atributo de instrucción SQL_ATTR_USE_BOOKMARKS se estableció en SQL_UB_OFF.<br /><br /> El valor del atributo de instrucción SQL_ATTR_CURSOR_TYPE se SQL_CURSOR_FORWARD_ONLY y el valor del argumento FetchOrientation no se SQL_FETCH_NEXT.<br /><br /> El valor del atributo de instrucción SQL_ATTR_CURSOR_SCROLLABLE se SQL_NONSCROLLABLE y el valor del argumento FetchOrientation no se SQL_FETCH_NEXT.|  
|HY107|Valor de fila fuera del rango|El valor especificado con el atributo de instrucción SQL_ATTR_CURSOR_TYPE se SQL_CURSOR_KEYSET_DRIVEN, pero el valor especificado con el atributo de instrucción SQL_ATTR_KEYSET_SIZE fue mayor que 0 y menor que el valor especificado con el atributo de instrucción SQL_ATTR_ROW_ARRAY_SIZE.|  
|HY111|Valor de marcador no válido|El argumento FetchOrientation se SQL_FETCH_BOOKMARK y el marcador al que apunta el valor del atributo de instrucción SQL_ATTR_FETCH_BOOKMARK_PTR no era válido o era un puntero nulo.|  
|HY117|La conexión se suspende debido al estado de transacción desconocido. Solo se permiten funciones de desconexión y de solo lectura.|(DM) Para obtener más información sobre el estado suspendido, vea [SqlEndTran (función).](../../../odbc/reference/syntax/sqlendtran-function.md)|  
|HYC00|Característica opcional no implementada|El controlador o el origen de datos no admite la conversión especificada por la combinación de *TargetType* en **SQLBindCol** y el tipo de datos SQL de la columna correspondiente.|  
|HYT00|Tiempo de espera agotado|El período de tiempo de espera de la consulta expiró antes de que el origen de datos devolviera el conjunto de resultados solicitado. El período de tiempo de espera se establece a través de SQLSetStmtAttr, SQL_ATTR_QUERY_TIMEOUT.|  
|HYT01|Tiempo de espera de conexión expirado|El período de tiempo de espera de conexión expiró antes de que el origen de datos respondiera a la solicitud. El período de tiempo de espera de conexión se establece a través de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|El controlador no admite esta función|(DM) El controlador asociado con el *StatementHandle* no admite la función.|  
|IM017|El sondeo está deshabilitado en el modo de notificación asincrónica|Siempre que se utiliza el modelo de notificación, el sondeo está deshabilitado.|  
|IM018|**SQLCompleteAsync** no se ha llamado para completar la operación asincrónica anterior en este identificador.|Si la llamada de función anterior en el identificador devuelve SQL_STILL_EXECUTING y si el modo de notificación está habilitado, **sqlCompleteAsync** debe llamarse en el identificador para realizar el procesamiento posterior y completar la operación.|  
  
## <a name="comments"></a>Comentarios  
 **SQLFetchScroll** devuelve un conjunto de filas especificado del conjunto de resultados. Los conjuntos de filas se pueden especificar por posición absoluta o relativa o por marcador. **SQLFetchScroll** sólo se puede llamar mientras existe un conjunto de resultados, es decir, después de una llamada que crea un conjunto de resultados y antes de que se cierre el cursor sobre ese conjunto de resultados. Si hay columnas enlazadas, devuelve los datos de esas columnas. Si la aplicación ha especificado un puntero a una matriz de estado de fila o un búfer en el que devolver el número de filas recuperadas, **SQLFetchScroll** devuelve también esta información. Las llamadas a **SQLFetchScroll** se pueden mezclar con llamadas a **SQLFetch,** pero no se pueden mezclar con llamadas a **SQLExtendedFetch**.  
  
 Para obtener más información, consulte Uso de [cursores](../../../odbc/reference/develop-app/using-block-cursors.md) de bloque y Uso de [cursores desplazables](../../../odbc/reference/develop-app/using-scrollable-cursors.md).  
  
## <a name="positioning-the-cursor"></a>Colocación del cursor  
 Cuando se crea el conjunto de resultados, el cursor se coloca antes del inicio del conjunto de resultados. **SQLFetchScroll** coloca el cursor de bloque en función de los valores de la *FetchOrientation* y *FetchOffset* argumentos como se muestra en la tabla siguiente. Las reglas exactas para determinar el inicio del nuevo conjunto de filas se muestran en la sección siguiente.  
  
|FetchOrientation|Significado|  
|----------------------|-------------|  
|SQL_FETCH_NEXT|Devuelve el siguiente conjunto de filas. Esto equivale a llamar a **SQLFetch**.<br /><br /> **SQLFetchScroll** omite el valor de *FetchOffset*.|  
|SQL_FETCH_PRIOR|Devuelve el conjunto de filas anterior.<br /><br /> **SQLFetchScroll** omite el valor de *FetchOffset*.|  
|SQL_FETCH_RELATIVE|Devuelve el conjunto de filas *FetchOffset* desde el inicio del conjunto de filas actual.|  
|SQL_FETCH_ABSOLUTE|Devuelve el conjunto de filas a partir de la fila *FetchOffset*.|  
|SQL_FETCH_FIRST|Devuelve el primer conjunto de filas del conjunto de resultados.<br /><br /> **SQLFetchScroll** omite el valor de *FetchOffset*.|  
|SQL_FETCH_LAST|Devuelve el último conjunto de filas completo del conjunto de resultados.<br /><br /> **SQLFetchScroll** omite el valor de *FetchOffset*.|  
|SQL_FETCH_BOOKMARK|Devuelve el conjunto de filas FetchOffset del marcador especificado por el atributo de instrucción SQL_ATTR_FETCH_BOOKMARK_PTR.|  
  
 Los controladores no son necesarios para admitir todas las orientaciones de captura; una aplicación llama a **SQLGetInfo** con un tipo de información de SQL_DYNAMIC_CURSOR_ATTRIBUTES1, SQL_KEYSET_CURSOR_ATTRIBUTES1 o SQL_STATIC_CURSOR_ATTRIBUTES1 (dependiendo del tipo del cursor) para determinar qué orientaciones de captura admite el controlador. La aplicación debe examinar las máscaras de bits SQL_CA1_NEXT, SQL_CA1_RELATIVE, SQL_CA1_ABSOLUTE y WQL_CA1_BOOKMARK en estos tipos de información. Además, si el cursor es de solo avance y FetchOrientation no está SQL_FETCH_NEXT, **SQLFetchScroll** devuelve SQLSTATE HY106 (tipo Fetch fuera del intervalo).  
  
 El atributo de instrucción SQL_ATTR_ROW_ARRAY_SIZE especifica el número de filas del conjunto de filas. Si el conjunto de filas que está capturando **SQLFetchScroll** se superpone al final del conjunto de resultados, **SQLFetchScroll** devuelve un conjunto de filas parcial. Es decir, si S + R - 1 es mayor que L, donde S es la fila inicial del conjunto de filas que se va a capturar, R es el tamaño del conjunto de filas y L es la última fila del conjunto de resultados, solo son válidas las primeras filas L - S + 1 del conjunto de filas. Las filas restantes están vacías y tienen el estado de SQL_ROW_NOROW.  
  
 Después **de SQLFetchScroll** devuelve, la fila actual es la primera fila del conjunto de filas.  
  
## <a name="cursor-positioning-rules"></a>Reglas de posicionamiento del cursor  
 En las secciones siguientes se describen las reglas exactas para cada valor de FetchOrientation. Estas reglas utilizan la siguiente notación.  
  
|Notación|Significado|  
|--------------|-------------|  
|*Antes de empezar*|El cursor de bloque se coloca antes del inicio del conjunto de resultados. Si la primera fila del nuevo conjunto de filas es antes del inicio del conjunto de resultados, **SQLFetchScroll** devuelve SQL_NO_DATA.|  
|*Después del final*|El cursor de bloque se coloca después del final del conjunto de resultados. Si la primera fila del nuevo conjunto de filas es después del final del conjunto de resultados, **SQLFetchScroll** devuelve SQL_NO_DATA.|  
|*CurrRowsetStart*|El número de la primera fila del conjunto de filas actual.|  
|*LastResultRow*|El número de la última fila del conjunto de resultados.|  
|*RowsetSize*|El tamaño del conjunto de filas.|  
|*FetchOffset*|El valor de la *FetchOffset* argumento.|  
|*BookmarkRow*|La fila correspondiente al marcador especificado por el atributo de instrucción SQL_ATTR_FETCH_BOOKMARK_PTR.|  
  
## <a name="sql_fetch_next"></a>SQL_FETCH_NEXT  
 Se aplican las siguientes reglas.  
  
|Condición|Primera fila de nuevo conjunto de filas|  
|---------------|-----------------------------|  
|*Antes de empezar*|1|  
|*CurrRowsetStart + RowsetSize*[1] * \<á LastResultRow*|*CurrRowsetStart + RowsetSize*[1]|  
|*CurrRowsetStart + RowsetSize*[1]*> LastResultRow*|*Después del final*|  
|*Después del final*|*Después del final*|  
  
 [1] Si se ha cambiado el tamaño del conjunto de filas desde la llamada anterior para capturar filas, este es el tamaño del conjunto de filas que se usó con la llamada anterior.  
  
## <a name="sql_fetch_prior"></a>SQL_FETCH_PRIOR  
 Se aplican las siguientes reglas.  
  
|Condición|Primera fila de nuevo conjunto de filas|  
|---------------|-----------------------------|  
|*Antes de empezar*|*Antes de empezar*|  
|*CurrRowsetStart n.o 1*|*Antes de empezar*|  
|*1 < CurrRowsetStart <- RowsetSize* <sup>[2]</sup>|*1* <sup>[1]</sup>|  
|*RowsetStart > RowsetSize* <sup>[2]</sup>|*CurrRowsetStart - Rowsetsize* <sup>[2]</sup>|  
|*After end AND LastResultRow < RowsetSize* <sup>[2]</sup>|*1* <sup>[1]</sup>|  
|*After end AND LastResultRow >á RowsetSize* <sup>[2]</sup>|*LastResultRow - RowsetSize + 1* <sup>[2]</sup>|  
  
 [1] **SQLFetchScroll** devuelve SQLSTATE 01S06 (Intento de capturar antes de que el conjunto de resultados devolviera el primer conjunto de filas) y SQL_SUCCESS_WITH_INFO.  
  
 [2] Si se ha cambiado el tamaño del conjunto de filas desde la llamada anterior para capturar filas, este es el nuevo tamaño del conjunto de filas.  
  
## <a name="sql_fetch_relative"></a>SQL_FETCH_RELATIVE  
 Se aplican las siguientes reglas.  
  
|Condición|Primera fila de nuevo conjunto de filas|  
|---------------|-----------------------------|  
|*(Antes de iniciar y FetchOffset > 0) OR (Después del final Y FetchOffset < 0)*|*--*<sup>[1]</sup>|  
|*BeforeStart AND FetchOffset <0*|*Antes de empezar*|  
|*CurrRowsetStart 1 Y FetchOffset < 0*|*Antes de empezar*|  
|*CurrRowsetStart > 1 AND CurrRowsetStart + FetchOffset < 1 AND &#124; FetchOffset &#124; > RowsetSize* <sup>[3]</sup>|*Antes de empezar*|  
|*CurrRowsetStart > 1 AND CurrRowsetStart + FetchOffset < 1 AND &#124; FetchOffset &#124; <á RowsetSize* <sup>[3]</sup>|*1* <sup>[2]</sup>|  
|*1 <de la lista \<de datos de la clase de la clase de la clase de la fila de la clase de la clase de la clase de la clase de la clase de la clase de la clase de*|*CurrRowsetStart + FetchOffset*|  
|*CurrRowsetStart + FetchOffset > LastResultRow*|*Después del final*|  
|*Después del final Y FetchOffset >0*|*Después del final*|  
  
 [1] ***SQLFetchScroll*** devuelve el mismo conjunto de filas como si se llamara con FetchOrientation establecido en SQL_FETCH_ABSOLUTE. Para obtener más información, consulte la sección "SQL_FETCH_ABSOLUTE".  
  
 [2] **SQLFetchScroll** devuelve SQLSTATE 01S06 (Intento de capturar antes de que el conjunto de resultados devolviera el primer conjunto de filas) y SQL_SUCCESS_WITH_INFO.  
  
 [3] Si se ha cambiado el tamaño del conjunto de filas desde la llamada anterior para capturar filas, este es el nuevo tamaño del conjunto de filas.  
  
## <a name="sql_fetch_absolute"></a>SQL_FETCH_ABSOLUTE  
 Se aplican las siguientes reglas.  
  
|Condición|Primera fila de nuevo conjunto de filas|  
|---------------|-----------------------------|  
|*FetchOffset < 0 AND &#124; FetchOffset &#124; <á LastResultRow*|*LastResultRow + FetchOffset + 1*|  
|*FetchOffset < 0 AND &#124; FetchOffset &#124; > LastResultRow AND &#124; FetchOffset &#124; > RowsetSize* <sup>[2]</sup>|*Antes de empezar*|  
|*FetchOffset < 0 AND &#124; FetchOffset &#124; > LastResultRow And &#124; FetchOffset &#124; <- RowsetSize* <sup>[2]</sup>|*1* <sup>[1]</sup>|  
|*FetchOffset - 0*|*Antes de empezar*|  
|*1 <- \<FetchOffset - LastResultRow*|*FetchOffset*|  
|*FetchOffset > LastResultRow*|*Después del final*|  
  
 [1] **SQLFetchScroll** devuelve SQLSTATE 01S06 (Intento de capturar antes de que el conjunto de resultados devolviera el primer conjunto de filas) y SQL_SUCCESS_WITH_INFO.  
  
 [2] Si se ha cambiado el tamaño del conjunto de filas desde la llamada anterior para capturar filas, este es el nuevo tamaño del conjunto de filas.  
  
 Una captura absoluta realizada en un cursor dinámico no puede proporcionar el resultado necesario porque las posiciones de fila en un cursor dinámico son indeterminadas. Tal operación es equivalente a una captura primero seguida de un pariente de captura; no es una operación atómica, como es una captura absoluta en un cursor estático.  
  
## <a name="sql_fetch_first"></a>SQL_FETCH_FIRST  
 Se aplican las siguientes reglas.  
  
|Condición|Primera fila de nuevo conjunto de filas|  
|---------------|-----------------------------|  
|*Cualquiera*|*1*|  
  
## <a name="sql_fetch_last"></a>SQL_FETCH_LAST  
 Se aplican las siguientes reglas.  
  
|Condición|Primera fila de nuevo conjunto de filas|  
|---------------|-----------------------------|  
|*RowsetSize* <sup>[1]</sup> <á LastResultRow|*LastResultRow - RowsetSize + 1* <sup>[1]</sup>|  
|*RowsetSize* <sup>[1]</sup> > LastResultRow|*1*|  
  
 [1] Si se ha cambiado el tamaño del conjunto de filas desde la llamada anterior para capturar filas, este es el nuevo tamaño del conjunto de filas.  
  
## <a name="sql_fetch_bookmark"></a>SQL_FETCH_BOOKMARK  
 Se aplican las siguientes reglas.  
  
|Condición|Primera fila de nuevo conjunto de filas|  
|---------------|-----------------------------|  
|*BookmarkRow + FetchOffset < 1*|*Antes de empezar*|  
|*1 <de la \<página de la <de la fila BookmarkRow + FetchOffset - LastResultRow*|*BookmarkRow + FetchOffset*|  
|*BookmarkRow + FetchOffset > LastResultRow*|*Después del final*|  
  
 Para obtener información acerca de los marcadores, vea [Marcadores (ODBC)](../../../odbc/reference/develop-app/bookmarks-odbc.md).  
  
## <a name="effect-of-deleted-added-and-error-rows-on-cursor-movement"></a>Efecto de las filas eliminadas, agregadas y de error en el movimiento del cursor  
 Los cursores estáticos y controlados por conjuntos de claves a veces detectan filas agregadas al conjunto de resultados y quitan filas eliminadas del conjunto de resultados. Al llamar a **SQLGetInfo** con las opciones SQL_STATIC_CURSOR_ATTRIBUTES2 y SQL_KEYSET_CURSOR_ATTRIBUTES2 y examinar las máscaras de bits SQL_CA2_SENSITIVITY_ADDITIONS, SQL_CA2_SENSITIVITY_DELETIONS y SQL_CA2_SENSITIVITY_UPDATES, una aplicación determina si los cursores implementados por un controlador determinado hacen esto. Para los controladores que pueden detectar filas eliminadas y quitarlas, los párrafos siguientes describen los efectos de este comportamiento. Para los controladores que pueden detectar filas eliminadas pero no pueden eliminarlas, las eliminaciones no tienen ningún efecto en los movimientos del cursor y no se aplican los párrafos siguientes.  
  
 Si el cursor detecta filas agregadas al conjunto de resultados o quita las filas eliminadas del conjunto de resultados, aparece como si detecta estos cambios solo cuando recupera datos. Esto incluye el caso cuando **SQLFetchScroll** se llama con FetchOrientation establecido en SQL_FETCH_RELATIVE y FetchOffset establecido en 0 para volver a capturar el mismo conjunto de filas, pero no incluye el caso cuando SQLSetPos se llama con fOption establecido en SQL_REFRESH. En este último caso, los datos de los búferes del conjunto de filas se actualizan, pero no se vuelven a grabar, y las filas eliminadas no se quitan del conjunto de resultados. Por lo tanto, cuando se elimina una fila o se inserta en el conjunto de filas actual, el cursor no modifica los búferes del conjunto de filas. En su lugar, detecta el cambio cuando recupera cualquier conjunto de filas que anteriormente incluye la fila eliminada o ahora incluye la fila insertada.  
  
 Por ejemplo:  
  
```cpp  
// Fetch the next rowset.  
SQLFetchScroll(hstmt, SQL_FETCH_NEXT, 0);  
// Delete third row of the rowset. Does not modify the rowset buffers.  
SQLSetPos(hstmt, 3, SQL_DELETE, SQL_LOCK_NO_CHANGE);  
// The third row has a status of SQL_ROW_DELETED after this call.  
SQLSetPos(hstmt, 3, SQL_REFRESH, SQL_LOCK_NO_CHANGE);  
// Refetch the same rowset. The third row is removed, replaced by what  
// was previously the fourth row.  
SQLFetchScroll(hstmt, SQL_FETCH_RELATIVE, 0);  
```  
  
 Cuando **SQLFetchScroll** devuelve un nuevo conjunto de filas que tiene una posición relativa al conjunto de filas actual, es decir, FetchOrientation es SQL_FETCH_NEXT, SQL_FETCH_PRIOR o SQL_FETCH_RELATIVE- no incluye cambios en el conjunto de filas actual al calcular la posición inicial del nuevo conjunto de filas. Sin embargo, incluye cambios fuera del conjunto de filas actual si es capaz de detectarlos. Además, cuando **SQLFetchScroll** devuelve un nuevo conjunto de filas que tiene una posición independiente del conjunto de filas actual - es decir, FetchOrientation es SQL_FETCH_FIRST, SQL_FETCH_LAST, SQL_FETCH_ABSOLUTE o SQL_FETCH_BOOKMARK - incluye todos los cambios que es capaz de detectar, incluso si están en el conjunto de filas actual.  
  
 Al determinar si las filas recién agregadas están dentro o fuera del conjunto de filas actual, se considera que un conjunto de filas parcial termina en la última fila válida; es decir, la última fila para la que el estado de la fila no es SQL_ROW_NOROW. Por ejemplo, supongamos que el cursor es capaz de detectar filas recién agregadas, el conjunto de filas actual es un conjunto de filas parcial, la aplicación agrega nuevas filas y el cursor agrega estas filas al final del conjunto de resultados. Si la aplicación llama a **SQLFetchScroll** con FetchOrientation establecido en SQL_FETCH_NEXT, **SQLFetchScroll** devuelve el conjunto de filas a partir de la primera fila recién agregada.  
  
 Por ejemplo, supongamos que el conjunto de filas actual comprende las filas 21 a 30, el tamaño del conjunto de filas es 10, el cursor quita las filas eliminadas del conjunto de resultados y el cursor detecta las filas agregadas al conjunto de resultados. En la tabla siguiente se muestran las filas **QUE SQLFetchScroll** devuelve en varias situaciones.  
  
|Change|Tipo de captura|FetchOffset|Nuevo conjunto de filas[1]|  
|------------|----------------|-----------------|---------------------|  
|Eliminar fila 21|NEXT|0|De 31 a 40|  
|Eliminar fila 31|NEXT|0|De 32 a 41|  
|Insertar fila entre las filas 21 y 22|NEXT|0|De 31 a 40|  
|Insertar fila entre las filas 30 y 31|NEXT|0|Fila insertada, 31 a 39|  
|Eliminar fila 21|PRIOR|0|11 a 20|  
|Eliminar fila 20|PRIOR|0|10 a 19|  
|Insertar fila entre las filas 21 y 22|PRIOR|0|11 a 20|  
|Insertar fila entre las filas 20 y 21|PRIOR|0|12 a 20, fila insertada|  
|Eliminar fila 21|RELATIVE|0|22 a 31<sup>[2]</sup>|  
|Eliminar fila 21|RELATIVE|1|22 a 31|  
|Insertar fila entre las filas 21 y 22|RELATIVE|0|21, fila insertada, 22 a 29|  
|Insertar fila entre las filas 21 y 22|RELATIVE|1|22 a 31|  
|Eliminar fila 21|ABSOLUTE|21|22 a 31<sup>[2]</sup>|  
|Eliminar fila 22|ABSOLUTE|21|21, 23 a 31|  
|Insertar fila entre las filas 21 y 22|ABSOLUTE|22|Fila insertada, 22 a 29|  
  
 [1] Esta columna utiliza los números de fila antes de insertar o eliminar las filas.  
  
 [2] En este caso, el cursor intenta devolver filas a partir de la fila 21. Dado que se ha eliminado la fila 21, la primera fila que devuelve es la fila 22.  
  
 Las filas de error (es decir, las filas con el estado de SQL_ROW_ERROR) no afectan al movimiento del cursor. Por ejemplo, si el conjunto de filas actual comienza con la fila 11 y el estado de la fila 11 es SQL_ROW_ERROR, llamar a **SQLFetchScroll** con FetchOrientation establecido en SQL_FETCH_RELATIVE y FetchOffset establecido en 5 devuelve el conjunto de filas a partir de la fila 16, tal como lo haría si el estado de la fila 11 fuera SQL_SUCCESS.  
  
## <a name="returning-data-in-bound-columns"></a>Devolución de datos en columnas enlazadas  
 **SQLFetchScroll** devuelve datos en columnas enlazadas de la misma manera que **SQLFetch**. Para obtener más información, vea "Devolver datos en columnas enlazadas" en [SQLFetch (función).](../../../odbc/reference/syntax/sqlfetch-function.md)  
  
 Si no hay columnas enlazadas, **SQLFetchScroll** no devuelve datos, pero mueve el cursor de bloque a la posición especificada. Si los datos se pueden recuperar de columnas sin enlazar de un cursor de bloque con **SQLGetData** depende del controlador. Esta funcionalidad se admite si una llamada a **SQLGetInfo** devuelve el bit SQL_GD_BLOCK para el tipo de información SQL_GETDATA_EXTENSIONS.  
  
## <a name="buffer-addresses"></a>Direcciones de búfer  
 **SQLFetchScroll** utiliza la misma fórmula para determinar la dirección de los datos y los búferes de longitud/indicador como **SQLFetch**. Para obtener más información, vea "Buffer Addresses" en [SQLBindCol Function](../../../odbc/reference/syntax/sqlbindcol-function.md).  
  
## <a name="row-status-array"></a>Matriz de Estados de fila  
 **SQLFetchScroll** establece valores en la matriz de estado de fila de la misma manera que SQLFetch. Para obtener más información, vea "Row Status Array" en [SQLFetch (Función)](../../../odbc/reference/syntax/sqlfetch-function.md).  
  
## <a name="rows-fetched-buffer"></a>Filas obtenidas Búfer  
 **SQLFetchScroll** devuelve el número de filas recuperadas en el búfer de filas recuperadas de la misma manera que **SQLFetch**. Para obtener más información, vea "Rows Fetched Buffer" en [SQLFetch (función)](../../../odbc/reference/syntax/sqlfetch-function.md).  
  
## <a name="error-handling"></a>Tratamiento de errores  
 Cuando una aplicación llama a **SQLFetchScroll** en un controlador ODBC 3.x, el Administrador de controladores llama a **SQLFetchScroll** en el controlador. Cuando una aplicación llama a **SQLFetchScroll** en un controlador ODBC 2.x, el Administrador de controladores llama a SQLExtendedFetch en el controlador. Dado que **SQLFetchScroll** y SQLExtendedFetch controlan los errores de una manera ligeramente diferente, la aplicación ve un comportamiento de error ligeramente diferente cuando llama a **SQLFetchScroll** en controladores ODBC 2.x y ODBC 3.x.  
  
 **SQLFetchScroll** devuelve errores y advertencias de la misma manera que **SQLFetch**; Para obtener más información, vea "Control de errores" en **SQLFetch**. **SQLExtendedFetch** devuelve errores de la misma manera que **SQLFetch**, con las siguientes excepciones:  
  
 Cuando se produce una advertencia que se aplica a una fila determinada del conjunto de filas, SQLExtendedFetch establece la entrada correspondiente en la matriz de estado de fila en SQL_ROW_SUCCESS, no SQL_ROW_SUCCESS_WITH_INFO.  
  
 Si se producen errores en cada fila del conjunto de filas, SQLExtendedFetch devuelve SQL_SUCCESS_WITH_INFO, no SQL_ERROR.  
  
 En cada grupo de registros de estado que se aplica a una fila individual, el primer registro de estado devuelto por SQLExtendedFetch debe contener SQLSTATE 01S01 (Error en la fila); **SQLFetchScroll** no devuelve este SQLSTATE. Si SQLExtendedFetch no puede devolver SQLSTATEs adicionales, debe devolver este SQLSTATE.  
  
## <a name="sqlfetchscroll-and-optimistic-concurrency"></a>SQLFetchScroll y simultaneidad optimista  
 Si un cursor utiliza simultaneidad optimista, es decir, el atributo de instrucción SQL_ATTR_CONCURRENCY tiene un valor de SQL_CONCUR_VALUES o SQL_CONCUR_ROWVER- **SQLFetchScroll** actualiza los valores de simultaneidad optimista utilizados por el origen de datos para detectar si una fila ha cambiado. Esto sucede siempre que **SQLFetchScroll** recupera un nuevo conjunto de filas, incluso cuando vuelve a capturar el conjunto de filas actual. (Se llama con FetchOrientation establecido en SQL_FETCH_RELATIVE y FetchOffset establecido en 0.)  
  
## <a name="sqlfetchscroll-and-odbc-2x-drivers"></a>Controladores SQLFetchScroll y ODBC 2.x  
 Cuando una aplicación llama a **SQLFetchScroll** en un controlador ODBC 2.x, el Administrador de controladores asigna esta llamada a **SQLExtendedFetch**. Pasa los siguientes valores para los argumentos de **SQLExtendedFetch**.  
  
|Argumento SQLExtendedFetch|Value|  
|-------------------------------|-----------|  
|StatementHandle|StatementHandle en **SQLFetchScroll**.|  
|FetchOrientation|FetchOrientation en **SQLFetchScroll**.|  
|FetchOffset|Si FetchOrientation no se SQL_FETCH_BOOKMARK, se utiliza el valor del argumento FetchOffset en **SQLFetchScroll.**<br /><br /> Si FetchOrientation se SQL_FETCH_BOOKMARK, se utiliza el valor almacenado en la dirección especificada por el atributo de instrucción SQL_ATTR_FETCH_BOOKMARK_PTR.|  
|RowCountPtr|La dirección especificada por el atributo de instrucción SQL_ATTR_ROWS_FETCHED_PTR.|  
|RowStatusArray|La dirección especificada por el atributo de instrucción SQL_ATTR_ROW_STATUS_PTR.|  
  
 Para obtener más información, consulte Cursores de [bloque, cursores desplazables y Compatibilidad con versiones](../../../odbc/reference/appendixes/block-cursors-scrollable-cursors-and-backward-compatibility.md) anteriores en apéndice G: directrices de controlador para la compatibilidad con versiones anteriores.  
  
## <a name="descriptors-and-sqlfetchscroll"></a>Descriptores y SQLFetchScroll  
 **SQLFetchScroll** interactúa con descriptores de la misma manera que **SQLFetch**. Para obtener más información, vea la sección "Descriptores y SQLFetchScroll" en [SQLFetch (función)](../../../odbc/reference/syntax/sqlfetch-function.md).  
  
## <a name="code-example"></a>Ejemplo de código  
 Consulte Enlace de [columna- wise](../../../odbc/reference/develop-app/column-wise-binding.md), [Enlace de fila- varias](../../../odbc/reference/develop-app/row-wise-binding.md)filas , Actualizar y eliminar instrucciones [posicionadas](../../../odbc/reference/develop-app/positioned-update-and-delete-statements.md)y Actualizar filas en el conjunto de [filas con SQLSetPos](../../../odbc/reference/develop-app/updating-rows-in-the-rowset-with-sqlsetpos.md).  
  
## <a name="related-functions"></a>Funciones relacionadas  
  
|Para información acerca de|Vea|  
|---------------------------|---------|  
|Enlazar un búfer a una columna en un conjunto de resultados|[SQLBindCol (función)](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Realizar operaciones masivas de inserción, actualización o eliminación|[Función SQLBulkOperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md)|  
|Cancelación del procesamiento de extractos|[Función SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Devolver información sobre una columna en un conjunto de resultados|[SQLDescribeCol (función)](../../../odbc/reference/syntax/sqldescribecol-function.md)|  
|Ejecución de una instrucción SQL|[Función SQLExecDirect](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|Ejecución de una instrucción SQL preparada|[Función SQLExecute](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|Obtención de una sola fila o un bloque de datos en una dirección de solo avance|[Función SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|Cerrar el cursor en la declaración|[Función SQLFreeStmt](../../../odbc/reference/syntax/sqlfreestmt-function.md)|  
|Devolver el número de columnas del conjunto de resultados|[SQLNumResultCols (función)](../../../odbc/reference/syntax/sqlnumresultcols-function.md)|  
|Colocación del cursor, actualización de datos en el conjunto de filas o actualización o eliminación de datos en el conjunto de resultados|[Función SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md)|  
|Establecer un atributo de instrucción|[Función SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de la API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Archivos de encabezado de ODBC](../../../odbc/reference/install/odbc-header-files.md)
