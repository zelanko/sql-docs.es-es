---
title: Función SQLFetch ? Microsoft Docs
ms.custom: ''
ms.date: 07/18/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLFetch
apilocation:
- sqlsrv32.dll
- odbc32.dll
apitype: dllExport
f1_keywords:
- SQLFetch
helpviewer_keywords:
- SQLFetch function [ODBC]
ms.assetid: 6c6611d2-bc6a-4390-87c9-1c5dd9cfe07c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: bc7e2da6996d8d6b2ee66befdc90794efec5617b
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81285975"
---
# <a name="sqlfetch-function"></a>Función SQLFetch
**Conformidad**  
 Versión introducida: Cumplimiento de normas ODBC 1.0: ISO 92  
  
 **Resumen**  
 **SQLFetch** recupera el siguiente conjunto de filas de datos del conjunto de resultados y devuelve datos para todas las columnas enlazadas.  
  
## <a name="syntax"></a>Sintaxis  
  
```cpp  
  
SQLRETURN SQLFetch(  
     SQLHSTMT     StatementHandle);  
```  
  
## <a name="arguments"></a>Argumentos  
 *StatementHandle*  
 [Entrada] Identificador de instrucción.  
  
## <a name="returns"></a>Devuelve  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NO_DATA, SQL_STILL_EXECUTING, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnóstico  
 Cuando **SQLFetch** devuelve SQL_ERROR o SQL_SUCCESS_WITH_INFO, se puede obtener un valor SQLSTATE asociado llamando a [SQLGetDiagRec Function](../../../odbc/reference/syntax/sqlgetdiagrec-function.md) con un *HandleType* de SQL_HANDLE_STMT y un *Handle* of *StatementHandle*. En la tabla siguiente se enumeran los valores SQLSTATE normalmente devueltos por **SQLFetch** y se explica cada uno de ellos en el contexto de esta función; la notación "(DM)" precede a las descripciones de SQLSTATEs devueltas por el Administrador de controladores. El código de retorno asociado a cada valor SQLSTATE se SQL_ERROR, a menos que se indique lo contrario. Si se produce un error en una sola columna, [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md) se puede llamar con un *DiagIdentifier* de SQL_DIAG_COLUMN_NUMBER para determinar la columna en la que se produjo el error; y **SQLGetDiagField** se puede llamar con un *DiagIdentifier* de SQL_DIAG_ROW_NUMBER para determinar la fila que contiene esa columna.  
  
 Para todos aquellos SQLSTATEs que pueden devolver SQL_SUCCESS_WITH_INFO o SQL_ERROR (excepto 01xxx SQLSTATEs), se devuelve SQL_SUCCESS_WITH_INFO si se produce un error en una o más filas, pero no en todas, de una operación de varias filas y SQL_ERROR se devuelve si se produce un error en una operación de una sola fila.  
  
|SQLSTATE|Error|Descripción|  
|--------------|-----------|-----------------|  
|01000|Advertencia general|Mensaje informativo específico del controlador. (La función devuelve SQL_SUCCESS_WITH_INFO.)|  
|01004|Datos de cadena truncados a la derecha|Los datos de cadena o binarios devueltos para una columna dieron como resultado el truncamiento de caracteres no en blanco o datos binarios no NULL. Si era un valor de cadena, se truncaba a la derecha.|  
|01S01|Error en la fila|Se ha producido un error al capturar una o varias filas.<br /><br /> (Si se devuelve este SQLSTATE cuando una aplicación ODBC 3 *.x* está trabajando con un controlador ODBC 2 *.x,* se puede omitir.)|  
|01S07|Truncamiento fraccionario|Los datos devueltos para una columna se truncaron. Para los tipos de datos numéricos, la parte fraccionaria del número se truncó. Para los tipos de datos time, timestamp e interval que contienen un componente time, la parte fraccionaria del tiempo se truncó.<br /><br /> (La función devuelve SQL_SUCCESS_WITH_INFO.)|  
|07006|Infracción de atributo de tipo de datos restringido|El valor de datos de una columna del conjunto de resultados no se pudo convertir al tipo de datos especificado por *TargetType* en **SQLBindCol**.<br /><br /> La columna 0 se enlazaba con un tipo de datos de SQL_C_BOOKMARK y el atributo de instrucción SQL_ATTR_USE_BOOKMARKS se estableció en SQL_UB_VARIABLE.<br /><br /> La columna 0 se enlazaba con un tipo de datos de SQL_C_VARBOOKMARK y el atributo de instrucción SQL_ATTR_USE_BOOKMARKS no se estableció en SQL_UB_VARIABLE.|  
|07009|Indice de descriptor no válido|El controlador era un controlador ODBC 2 *.x* que no admite **SQLExtendedFetch**y un número de columna especificado en el enlace para una columna era 0.<br /><br /> La columna 0 estaba enlazada y el atributo de instrucción SQL_ATTR_USE_BOOKMARKS se estableció en SQL_UB_OFF.|  
|08S01|Fallo del enlace de comunicación|Error en el vínculo de comunicación entre el controlador y el origen de datos al que estaba conectado el controlador antes de que la función completara el procesamiento.|  
|22001|Datos de cadena truncados a la derecha|Se ha truncado un marcador de longitud variable devuelto para una columna.|  
|22002|Variable indicador requerida pero no suministrada|Los datos NULL se capturaron en una columna cuyo *StrLen_or_IndPtr* establecido por **SQLBindCol** (o SQL_DESC_INDICATOR_PTR establecido por **SQLSetDescField** o **SQLSetDescRec**) era un puntero nulo.|  
|22003|Valor numérico fuera del rango|Devolver el valor numérico como numérico o cadena para una o más columnas enlazadas habría provocado que se truncase la parte completa (en lugar de fraccionaria) del número.<br /><br /> Para obtener más información, vea [Convertir datos de SQL a tipos](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md) de datos C en apéndice D: tipos de datos.|  
|22007|Formato de fecha y hora no válido|Una columna de caracteres del conjunto de resultados estaba enlazada a una estructura C de fecha, hora o marca de tiempo, y un valor de la columna era, respectivamente, una fecha, hora o marca de tiempo no válidas.|  
|22012|División por cero|Se devolvió un valor de una expresión aritmética, lo que dio lugar a la división por cero.|  
|22015|Desbordamiento de campo de intervalo|La asignación de un tipo SQL numérico o de intervalo exacto a un tipo de intervalo C causó una pérdida de dígitos significativos en el campo inicial.<br /><br /> Al capturar datos en un tipo de intervalo C, no había ninguna representación del valor del tipo SQL en el tipo de intervalo C.|  
|22018|Valor de carácter no válido para la especificación de conversión|Una columna de caracteres del conjunto de resultados estaba enlazada a un búfer de caracteres C y la columna contenía un carácter para el que no había ninguna representación en el conjunto de caracteres del búfer.<br /><br /> El tipo C era un número exacto o aproximado, una fecha y hora o un tipo de datos de intervalo; el tipo SQL de la columna era un tipo de datos de carácter; y el valor de la columna no era un literal válido del tipo C enlazado.|  
|24000|Estado de cursor no válido|El *StatementHandle* estaba en un estado ejecutado, pero no se asoció ningún conjunto de resultados con *StatementHandle*.|  
|40001|Error de serialización|La transacción en la que se ejecutó la captura se ha terminado para evitar el interbloqueo.|  
|40003|Finalización de la declaración desconocida|Error en la conexión asociada durante la ejecución de esta función y no se puede determinar el estado de la transacción.|  
|HY000|Error general|Se ha producido un error para el que no se ha definido sqlSTATE específico y para el que no se ha definido sqlSTATE específico de la implementación. El mensaje de error devuelto por **SQLGetDiagRec** en el * \*messageText* búfer describe el error y su causa.|  
|HY001|Error de asignación de memoria|El controlador no pudo asignar la memoria necesaria para admitir la ejecución o finalización de la función.|  
|HY008|Operación cancelada|El procesamiento asincrónico se ha habilitado para *StatementHandle*. Se llamó a la función **SQLFetch** y antes de completar la ejecución, **SQLCancel** o **SQLCancelHandle** se llamó en el *StatementHandle*. A **continuación,** se volvió a llamar a la función SQLFetch en *StatementHandle*.<br /><br /> O bien, se llamó a la función **SQLFetch** y antes de completar la ejecución, **SQLCancel** o **SQLCancelHandle** se llamó en el *StatementHandle* desde un subproceso diferente en una aplicación multiproceso.|  
|HY010|Error de secuencia de funciones|(DM) se llamó a una función de ejecución asincrónica para el identificador de conexión asociado a *StatementHandle*. Esta función asincrónica todavía se estaba ejecutando cuando se llamó a la función **SQLFetch.**<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**o **SQLMoreResults** se llamó para el *StatementHandle* y devuelto SQL_PARAM_DATA_AVAILABLE. Se llamó a esta función antes de recuperar los datos para todos los parámetros transmitidos.<br /><br /> (DM) el *StatementHandle* especificado no estaba en un estado ejecutado. Se llamó a la función sin llamar primero a **SQLExecDirect**, **SQLExecute** o una función de catálogo.<br /><br /> (DM) se llamó a una función de ejecución asincrónica (no esta) para el *StatementHandle* y todavía se estaba ejecutando cuando se llamó a esta función.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, o **SQLSetPos** se llamó para el *StatementHandle* y devuelto SQL_NEED_DATA. Se llamó a esta función antes de que se enviaran datos para todos los parámetros o columnas de datos en ejecución.<br /><br /> (DM) **SQLFetch** se llamó para el *StatementHandle* después **de SQLExtendedFetch** se llamó y antes **de SQLFreeStmt** con el SQL_CLOSE opción se llamó.|  
|HY013|Error de administración de memoria|No se pudo procesar la llamada de función porque no se pudo tener acceso a los objetos de memoria subyacentes, posiblemente debido a condiciones de poca memoria.|  
|HY090|Cadena no válida o longitud de búfer|El atributo de instrucción SQL_ATTR_USE_BOOKMARK se estableció en SQL_UB_VARIABLE y la columna 0 se enlazaba a un búfer cuya longitud no era igual a la longitud máxima del marcador para este conjunto de resultados. (Esta longitud está disponible en el campo SQL_DESC_OCTET_LENGTH del IRD y se puede obtener llamando a **SQLDescribeCol**, **SQLColAttribute**o **SQLGetDescField**.)|  
|HY107|Valor de fila fuera del rango|El valor especificado con el atributo de instrucción SQL_ATTR_CURSOR_TYPE se SQL_CURSOR_KEYSET_DRIVEN, pero el valor especificado con el atributo de instrucción SQL_ATTR_KEYSET_SIZE fue mayor que 0 y menor que el valor especificado con el atributo de instrucción SQL_ATTR_ROW_ARRAY_SIZE.|  
|HY117|La conexión se suspende debido al estado de transacción desconocido. Solo se permiten funciones de desconexión y de solo lectura.|(DM) Para obtener más información sobre el estado suspendido, vea [SqlEndTran (función).](../../../odbc/reference/syntax/sqlendtran-function.md)|  
|HYC00|Característica opcional no implementada|El controlador o el origen de datos no admite la conversión especificada por la combinación de *TargetType* en **SQLBindCol** y el tipo de datos SQL de la columna correspondiente.|  
|HYT00|Tiempo de espera agotado|El período de tiempo de espera de la consulta expiró antes de que el origen de datos devolviera el conjunto de resultados solicitado. El período de tiempo de espera se establece a través de SQLSetStmtAttr, SQL_ATTR_QUERY_TIMEOUT.|  
|HYT01|Tiempo de espera de conexión expirado|El período de tiempo de espera de conexión expiró antes de que el origen de datos respondiera a la solicitud. El período de tiempo de espera de conexión se establece a través de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|El controlador no admite esta función|(DM) El controlador asociado con el *StatementHandle* no admite la función.|  
|IM017|El sondeo está deshabilitado en el modo de notificación asincrónica|Siempre que se utiliza el modelo de notificación, el sondeo está deshabilitado.|  
|IM018|**SQLCompleteAsync** no se ha llamado para completar la operación asincrónica anterior en este identificador.|Si la llamada de función anterior en el identificador devuelve SQL_STILL_EXECUTING y si el modo de notificación está habilitado, **sqlCompleteAsync** debe llamarse en el identificador para realizar el procesamiento posterior y completar la operación.|  
  
## <a name="comments"></a>Comentarios  
 **SQLFetch** devuelve el siguiente conjunto de filas del conjunto de resultados. Solo se puede llamar mientras existe un conjunto de resultados: es decir, después de una llamada que crea un conjunto de resultados y antes de que se cierre el cursor sobre ese conjunto de resultados. Si hay columnas enlazadas, devuelve los datos de esas columnas. Si la aplicación ha especificado un puntero a una matriz de estado de fila o un búfer en el que devolver el número de filas recuperadas, **SQLFetch** también devuelve esta información. Las llamadas a **SQLFetch** se pueden mezclar con llamadas a **SQLFetchScroll,** pero no se pueden mezclar con llamadas a **SQLExtendedFetch**. Para obtener más información, consulte [Obtención de una fila de datos](../../../odbc/reference/develop-app/fetching-a-row-of-data.md).  
  
 Si una aplicación ODBC 3 *.x* funciona con un controlador ODBC 2 *.x,* el Administrador de controladores asigna llamadas **SQLFetch** a **SQLExtendedFetch** para un controlador ODBC 2 *.x* que admite **SQLExtendedFetch**. Si el controlador ODBC 2 *.x* no admite **SQLExtendedFetch**, el Administrador de controladores asigna llamadas **SQLFetch** a **SQLFetch** en el controlador ODBC 2 *.x,* que solo puede capturar una sola fila.  
  
 Para obtener más información, consulte Cursores de [bloque, cursores desplazables y Compatibilidad con versiones](../../../odbc/reference/appendixes/block-cursors-scrollable-cursors-and-backward-compatibility.md) anteriores en apéndice G: directrices de controlador para la compatibilidad con versiones anteriores.  
  
## <a name="positioning-the-cursor"></a>Colocación del cursor  
 Cuando se crea el conjunto de resultados, el cursor se coloca antes del inicio del conjunto de resultados. **SQLFetch** recupera el siguiente conjunto de filas. Es equivalente a llamar a **SQLFetchScroll** con *FetchOrientation* establecido en SQL_FETCH_NEXT. Para obtener más información acerca de los cursores, vea [Cursores](../../../odbc/reference/develop-app/cursors.md) y [cursores](../../../odbc/reference/develop-app/block-cursors.md)de bloque .  
  
 El atributo de instrucción SQL_ATTR_ROW_ARRAY_SIZE especifica el número de filas del conjunto de filas. Si el conjunto de filas que está capturando **SQLFetch** se superpone al final del conjunto de resultados, **SQLFetch** devuelve un conjunto de filas parcial. Es decir, si S + R - 1 es mayor que L, donde S es la fila inicial del conjunto de filas que se va a capturar, R es el tamaño del conjunto de filas y L es la última fila del conjunto de resultados, solo son válidas las primeras filas L - S + 1 del conjunto de filas. Las filas restantes están vacías y tienen el estado de SQL_ROW_NOROW.  
  
 Después de **SQLFetch** devuelve, la fila actual es la primera fila del conjunto de filas.  
  
 Las reglas enumeradas en la tabla siguiente describen el posicionamiento del cursor después de una llamada a **SQLFetch**, en función de las condiciones enumeradas en la segunda tabla de esta sección.  
  
|Condición|Primera fila de nuevo conjunto de filas|  
|---------------|-----------------------------|  
|Antes de empezar|1|  
|*CurrRowsetStart* \< =  *LastResultRow - Rowsetsize*[1]|*CurrRowsetStart* + *RowsetSize*[2]|  
|*CurrRowsetStart* > *LastResultRow - Rowsetsize*[1]|Después del final|  
|Después del final|Después del final|  
  
 [1] Si el tamaño del conjunto de filas se cambia entre recuperaciones, este es el tamaño del conjunto de filas que se usó con la captura anterior.  
  
 [2] Si el tamaño del conjunto de filas se cambia entre fetches, este es el tamaño del conjunto de filas que se usó con la nueva captura.  
  
|Notación|Significado|  
|--------------|-------------|  
|Antes de empezar|El cursor de bloque se coloca antes del inicio del conjunto de resultados. Si la primera fila del nuevo conjunto de filas es antes del inicio del conjunto de resultados, **SQLFetch** devuelve SQL_NO_DATA.|  
|Después del final|El cursor de bloque se coloca después del final del conjunto de resultados. Si la primera fila del nuevo conjunto de filas es después del final del conjunto de resultados, **SQLFetch** devuelve SQL_NO_DATA.|  
|*CurrRowsetStart*|El número de la primera fila del conjunto de filas actual.|  
|*LastResultRow*|El número de la última fila del conjunto de resultados.|  
|*RowsetSize*|El tamaño del conjunto de filas.|  
  
 Por ejemplo, supongamos que un conjunto de resultados tiene 100 filas y el tamaño del conjunto de filas es 5. En la tabla siguiente se muestra el conjunto de filas y el código devuelto por **SQLFetch** para diferentes posiciones iniciales.  
  
|Conjunto de filas actual|Código de retorno|Nuevo conjunto de filas|N.o de filas capturadas|  
|--------------------|-----------------|----------------|------------------------|  
|Antes de empezar|SQL_SUCCESS|1 a 5|5|  
|1 a 5|SQL_SUCCESS|6 a 10|5|  
|52 a 56|SQL_SUCCESS|57 a 61|5|  
|91 a 95|SQL_SUCCESS|96 a 100|5|  
|93 a 97|SQL_SUCCESS|98 a 100. Las filas 4 y 5 de la matriz de estado de fila se establecen en SQL_ROW_NOROW.|3|  
|96 a 100|SQL_NO_DATA|Ninguno.|0|  
|99 a 100|SQL_NO_DATA|Ninguno.|0|  
|Después del final|SQL_NO_DATA|Ninguno.|0|  
  
## <a name="returning-data-in-bound-columns"></a>Devolución de datos en columnas enlazadas  
 Como **SQLFetch** devuelve cada fila, coloca los datos de cada columna enlazada en el búfer enlazado a esa columna. Si no hay columnas enlazadas, **SQLFetch** no devuelve ningún dato, pero mueve el cursor de bloque hacia delante. Los datos todavía se pueden recuperar mediante **SQLGetData**. Si el cursor es un cursor de varias filas (es decir, el SQL_ATTR_ROW_ARRAY_SIZE es mayor que 1), **SQLGetData** sólo se puede llamar si se devuelve SQL_GD_BLOCK cuando **SQLGetInfo** se llama con un *InfoType* de SQL_GETDATA_EXTENSIONS. (Para obtener más información, vea [SQLGetData](../../../odbc/reference/syntax/sqlgetdata-function.md).)  
  
 Para cada columna enlazada de una fila, **SQLFetch** hace lo siguiente:  
  
1.  Establece el búfer de longitud/indicador en SQL_NULL_DATA y procede a la siguiente columna si los datos son NULL. Si los datos son NULL y no se ha enlazado ningún búfer de longitud/indicador, **SQLFetch** devuelve SQLSTATE 22002 (variable de indicador requerida pero no proporcionada) para la fila y pasa a la fila siguiente. Para obtener información sobre cómo determinar la dirección del búfer de longitud/indicador, consulte "Direcciones de búfer" en [SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md).  
  
     Si los datos de la columna no son NULL, **SQLFetch** continúa con el paso 2.  
  
2.  Si el atributo de instrucción SQL_ATTR_MAX_LENGTH se establece en un valor distinto de cero y la columna contiene datos binarios o de caracteres, los datos se truncan en SQL_ATTR_MAX_LENGTH bytes.  
  
    > [!NOTE]  
    >  El atributo de instrucción SQL_ATTR_MAX_LENGTH está diseñado para reducir el tráfico de red. Generalmente lo implementa el origen de datos, que trunca los datos antes de devolverlos a través de la red. Los controladores y las fuentes de datos no son necesarios para admitirlo. Por lo tanto, para garantizar que los datos se truncan a un tamaño determinado, una aplicación debe asignar un búfer de ese tamaño y especificar el tamaño en el *argumento cbValueMax* en **SQLBindCol**.  
  
3.  Convierte los datos en el tipo especificado por *TargetType* en **SQLBindCol**.  
  
4.  Si los datos se convirtieron en un tipo de datos de longitud variable, como carácter o binario, **SQLFetch** comprueba si la longitud de los datos supera la longitud del búfer de datos. Si la longitud de los datos de caracteres (incluido el carácter de terminación null) supera la longitud del búfer de datos, **SQLFetch** trunca los datos a la longitud del búfer de datos menos la longitud de un carácter de terminación nula. A continuación, termina en null los datos. Si la longitud de los datos binarios supera la longitud del búfer de datos, **SQLFetch** lo trunca a la longitud del búfer de datos. La longitud del búfer de datos se especifica con *BufferLength* en **SQLBindCol**.  
  
     **SQLFetch** nunca trunca los datos convertidos a tipos de datos de longitud fija; siempre asume que la longitud del búfer de datos es el tamaño del tipo de datos.  
  
5.  Coloca los datos convertidos (y posiblemente truncados) en el búfer de datos. Para obtener información sobre cómo determinar la dirección del búfer de datos, vea "Direcciones de búfer" en [SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md).  
  
6.  Coloca la longitud de los datos en el búfer de longitud/indicador. Si el puntero del indicador y el puntero de longitud se establecieron en el mismo búfer (como hace una llamada a **SQLBindCol),** la longitud se escribe en el búfer para los datos válidos y SQL_NULL_DATA se escribe en el búfer para los datos NULL. Si no se ha enlazado ningún búfer de longitud/indicador, **SQLFetch** no devuelve la longitud.  
  
    -   Para los datos binarios o de caracteres, esta es la longitud de los datos después de la conversión y antes del truncamiento debido a que el búfer de datos es demasiado pequeño. Si el controlador no puede determinar la longitud de los datos después de la conversión, como a veces sucede con los datos largos, establece la longitud en SQL_NO_TOTAL. Si los datos se truncaron debido al atributo de instrucción SQL_ATTR_MAX_LENGTH, el valor de este atributo se coloca en el búfer de longitud/indicador en lugar de la longitud real. Esto se debe a que este atributo está diseñado para truncar los datos en el servidor antes de la conversión, de modo que el controlador no tiene forma de averiguar cuál es la longitud real.  
  
    -   Para todos los demás tipos de datos, esta es la longitud de los datos después de la conversión; es decir, es el tamaño del tipo al que se convirtieron los datos.  
  
     Para obtener información sobre cómo determinar la dirección del búfer de longitud/indicador, consulte "Direcciones de búfer" en [SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md).  
  
7.  Si los datos se truncan durante la conversión sin una pérdida de dígitos significativos (por ejemplo, el número real 1.234 se trunca al entero 1 cuando se convierte), **SQLFetch** devuelve SQLSTATE 01S07 (truncamiento fraccionario) y SQL_SUCCESS_WITH_INFO. Si los datos se truncan porque la longitud del búfer de datos es demasiado pequeña (por ejemplo, la cadena "abcdef" se coloca en un búfer de 4 bytes), **SQLFetch** devuelve SQLSTATE 01004 (datos truncados) y SQL_SUCCESS_WITH_INFO. Si los datos se truncan debido al atributo de instrucción SQL_ATTR_MAX_LENGTH, **SQLFetch** devuelve SQL_SUCCESS y no devuelve SQLSTATE 01S07 (truncamiento fraccionario) o SQLSTATE 01004 (datos truncados). Si los datos se truncan durante la conversión con una pérdida de dígitos significativos (por ejemplo, si un valor de SQL_INTEGER mayor que 100.000 se convirtió en un SQL_C_TINYINT), **SQLFetch** devuelve SQLSTATE 22003 (valor numérico fuera del intervalo) y SQL_ERROR (si el tamaño del conjunto de filas es 1) o SQL_SUCCESS_WITH_INFO (si el tamaño del conjunto de filas es mayor que 1).  
  
 El contenido del búfer de datos enlazado y el búfer de longitud/indicador son indefinidos si **SQLFetch** o **SQLFetchScroll** no devuelve SQL_SUCCESS o SQL_SUCCESS_WITH_INFO.  
  
## <a name="row-status-array"></a>Matriz de Estados de fila  
 La matriz de estado de fila se utiliza para devolver el estado de cada fila del conjunto de filas. La dirección de esta matriz se especifica con el atributo de instrucción SQL_ATTR_ROW_STATUS_PTR. La aplicación asigna la matriz y debe tener tantos elementos como se especifican en el atributo de instrucción SQL_ATTR_ROW_ARRAY_SIZE. Sus valores se establecen mediante **SQLFetch**, **SQLFetchScroll**y **SQLBulkOperations** o **SQLSetPos** (excepto cuando se han llamado después de que **SQLExtendedFetch**haya colocado el cursor). Si el valor del atributo de instrucción SQL_ATTR_ROW_STATUS_PTR es un puntero nulo, estas funciones no devuelven el estado de fila.  
  
 El contenido del búfer de matriz de estado de fila no está definido si **SQLFetch** o **SQLFetchScroll** no devuelve SQL_SUCCESS o SQL_SUCCESS_WITH_INFO.  
  
 Los siguientes valores se devuelven en la matriz de estado de fila.  
  
|Valor de la matriz de estado de fila|Descripción|  
|----------------------------|-----------------|  
|SQL_ROW_SUCCESS|La fila se ha capturado correctamente y no ha cambiado desde la última vez que se obtuvo de este conjunto de resultados.|  
|SQL_ROW_SUCCESS_WITH_INFO|La fila se ha capturado correctamente y no ha cambiado desde la última vez que se obtuvo de este conjunto de resultados. Sin embargo, se devolvió una advertencia sobre la fila.|  
|SQL_ROW_ERROR|Se ha producido un error al capturar la fila.|  
|SQL_ROW_UPDATED[1],[2] y [3]|La fila se ha capturado correctamente y ha cambiado desde la última vez que se obtuvo de este conjunto de resultados. Si la fila se recupera de nuevo desde este conjunto de resultados o **SQLSetPos**la actualiza, el estado se cambia al nuevo estado de la fila.|  
|SQL_ROW_DELETED[3]|La fila se ha eliminado desde la última vez que se obtuvo de este conjunto de resultados.|  
|SQL_ROW_ADDED[4]|LA fila se insertó mediante **SQLBulkOperations**. Si la fila se recupera de nuevo de este conjunto de resultados o **SQLSetPos**la actualiza, su estado se SQL_ROW_SUCCESS.|  
|SQL_ROW_NOROW|El conjunto de filas se superpuso al final del conjunto de resultados y no se devolvió ninguna fila que correspondiera a este elemento de la matriz de estado de fila.|  
  
 [1] Para los cursores de conjunto de claves, mixtos y dinámicos, si se actualiza un valor de clave, se considera que la fila de datos se ha eliminado y se ha añadido una nueva fila.  
  
 [2] Algunos controladores no pueden detectar actualizaciones de datos y, por lo tanto, no pueden devolver este valor. Para determinar si un controlador puede detectar actualizaciones de filas refetched, una aplicación llama a **SQLGetInfo** con la opción SQL_ROW_UPDATES.  
  
 [3] **SQLFetch** puede devolver este valor solo cuando se mezcla con llamadas a **SQLFetchScroll**. Esto se debe a que **SQLFetch** avanza a través del conjunto de resultados y, cuando se usa exclusivamente, no recupera ninguna fila. Dado que no hay filas refetched, **SQLFetch** no detecta los cambios realizados en las filas capturadas anteriormente. Sin embargo, si **SQLFetchScroll** coloca el cursor antes que las filas recuperadas anteriormente y **SQLFetch** se usa para capturar esas filas, **SQLFetch** puede detectar cualquier cambio en esas filas.  
  
 [4] Devuelto por SQLBulkOperations solamente. No establecido por **SQLFetch** o **SQLFetchScroll**.  
  
### <a name="rows-fetched-buffer"></a>Filas obtenidas Búfer  
 El búfer de filas capturado se utiliza para devolver el número de filas recuperadas, incluidas las filas para las que no se devolvió ningún dato porque se produjo un error mientras se estaban capturando. En otras palabras, es el número de filas para las que el valor de la matriz de estado de fila no se SQL_ROW_NOROW. La dirección de este búfer se especifica con el atributo de instrucción SQL_ATTR_ROWS_FETCHED_PTR. La aplicación asigna el búfer. Se establece mediante **SQLFetch** y **SQLFetchScroll**. Si el valor del atributo de instrucción SQL_ATTR_ROWS_FETCHED_PTR es un puntero nulo, estas funciones no devuelven el número de filas recuperadas. Para determinar el número de la fila actual en el conjunto de resultados, una aplicación puede llamar a **SQLGetStmtAttr** con el SQL_ATTR_ROW_NUMBER atributo.  
  
 El contenido del búfer de filas recuperadas no está definido si **SQLFetch** o **SQLFetchScroll** no devuelve SQL_SUCCESS o SQL_SUCCESS_WITH_INFO, excepto cuando se devuelve SQL_NO_DATA, en cuyo caso el valor del búfer de filas capturadose se establece en 0.  
  
### <a name="error-handling"></a>Tratamiento de errores  
 Los errores y advertencias se pueden aplicar a filas individuales o a toda la función. Para obtener más información acerca de los registros de diagnóstico, vea [Diagnóstico](../../../odbc/reference/develop-app/diagnostics.md) y [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md).  
  
#### <a name="errors-and-warnings-on-the-entire-function"></a>Errores y advertencias en toda la función  
 Si se aplica un error a toda la función, como SQLSTATE HYT00 (tiempo de espera caducado) o SQLSTATE 24000 (estado de cursor no válido), **SQLFetch** devuelve SQL_ERROR y el SQLSTATE aplicable. El contenido de los búferes del conjunto de filas es indefinido y la posición del cursor no cambia.  
  
 Si se aplica una advertencia a toda la función, **SQLFetch** devuelve SQL_SUCCESS_WITH_INFO y el SQLSTATE aplicable. Los registros de estado de las advertencias que se aplican a toda la función se devuelven antes de los registros de estado que se aplican a filas individuales.  
  
#### <a name="errors-and-warnings-in-individual-rows"></a>Errores y advertencias en filas individuales  
 Si un error (como SQLSTATE 22012 (División por cero)) o una advertencia (como SQLSTATE 01004 (Datos truncados)) se aplica a una sola fila, **SQLFetch**hace lo siguiente:  
  
-   Establece el elemento correspondiente de la matriz de estado de fila en SQL_ROW_ERROR para errores o SQL_ROW_SUCCESS_WITH_INFO para advertencias.  
  
-   Agrega cero o más registros de estado que contienen SQLSTATEs para el error o advertencia.  
  
-   Establece los campos de número de fila y columna en los registros de estado. Si **SQLFetch** no puede determinar un número de fila o columna, establece ese número en SQL_ROW_NUMBER_UNKNOWN o SQL_COLUMN_NUMBER_UNKNOWN, respectivamente. Si el registro de estado no se aplica a una columna determinada, **SQLFetch** establece el número de columna en SQL_NO_COLUMN_NUMBER.  
  
 **SQLFetch** continúa capturando filas hasta que ha capturado todas las filas del conjunto de filas. Devuelve SQL_SUCCESS_WITH_INFO a menos que se produzca un error en cada fila del conjunto de filas (sin incluir filas con el estado SQL_ROW_NOROW), en cuyo caso devuelve SQL_ERROR. En particular, si el tamaño del conjunto de filas es 1 y se produce un error en esa fila, **SQLFetch** devuelve SQL_ERROR.  
  
 **SQLFetch** devuelve los registros de estado en orden de número de fila. Es decir, devuelve todos los registros de estado de filas desconocidas (si los hay); a continuación, devuelve todos los registros de estado de la primera fila (si existe) y, a continuación, devuelve todos los registros de estado de la segunda fila (si los hay), y así sucesivamente. Los registros de estado para cada fila se ordenan de acuerdo con las reglas normales para ordenar registros de estado; Para obtener más información, vea "Secuencia de registros de estado" en [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md).  
  
### <a name="descriptors-and-sqlfetch"></a>Descriptores y SQLFetch  
 En las secciones siguientes se describe cómo **SQLFetch** interactúa con descriptores.  
  
#### <a name="argument-mappings"></a>Asignaciones de argumentos  
 El controlador no establece ningún campo descriptor basado en los argumentos de **SQLFetch**.  
  
#### <a name="other-descriptor-fields"></a>Otros campos descriptores  
 **SQLFetch**utiliza los siguientes campos descriptores.  
  
|Campo descriptor|Desc.|Campo en|Establecer a través de|  
|----------------------|-----------|--------------|-----------------|  
|SQL_DESC_ARRAY_SIZE|Ard|encabezado|SQL_ATTR_ROW_ARRAY_SIZE atributo de instrucción|  
|SQL_DESC_ARRAY_STATUS_PTR|Ird|encabezado|SQL_ATTR_ROW_STATUS_PTR atributo de instrucción|  
|SQL_DESC_BIND_OFFSET_PTR|Ard|encabezado|SQL_ATTR_ROW_BIND_OFFSET_PTR atributo de instrucción|  
|SQL_DESC_BIND_TYPE|Ard|encabezado|atributo de SQL_ATTR_ROW_BIND_TYPE instrucción|  
|SQL_DESC_COUNT|Ard|encabezado|*ColumnNumber* argumento de **SQLBindCol**|  
|SQL_DESC_DATA_PTR|Ard|records|*TargetValuePtr* argumento de **SQLBindCol**|  
|SQL_DESC_INDICATOR_PTR|Ard|records|*StrLen_or_IndPtr* argumento en **SQLBindCol**|  
|SQL_DESC_OCTET_LENGTH|Ard|records|*BufferLength* argumento en **SQLBindCol**|  
|SQL_DESC_OCTET_LENGTH_PTR|Ard|records|*StrLen_or_IndPtr* argumento en **SQLBindCol**|  
|SQL_DESC_ROWS_PROCESSED_PTR|Ird|encabezado|atributo de instrucción SQL_ATTR_ROWS_FETCHED_PTR|  
|SQL_DESC_TYPE|Ard|records|*TargetType* argumento en **SQLBindCol**|  
  
 Todos los campos descriptores también se pueden establecer a través de **SQLSetDescField**.  
  
#### <a name="separate-length-and-indicator-buffers"></a>Búferes separados de longitud e indicador  
 Las aplicaciones pueden enlazar un solo búfer o dos búferes independientes que se pueden utilizar para contener los valores de longitud e indicador. Cuando una aplicación llama a **SQLBindCol**, el controlador establece los campos SQL_DESC_OCTET_LENGTH_PTR y SQL_DESC_INDICATOR_PTR de la ARD en la misma dirección, que se pasa en el *argumento StrLen_or_IndPtr.* Cuando una aplicación llama a **SQLSetDescField** o **SQLSetDescRec**, puede establecer estos dos campos en direcciones diferentes.  
  
 **SQLFetch** determina si la aplicación ha especificado búferes de longitud e indicador independientes. En este caso, cuando los datos no son NULL, **SQLFetch** establece el búfer del indicador en 0 y devuelve la longitud en el búfer de longitud. Cuando los datos son NULL, **SQLFetch** establece el búfer del indicador en SQL_NULL_DATA y no modifica el búfer de longitud.  
  
### <a name="code-example"></a>Ejemplo de código  
 Vea [SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md), [SQLColumns](../../../odbc/reference/syntax/sqlcolumns-function.md), [SQLGetData](../../../odbc/reference/syntax/sqlgetdata-function.md)y [SQLProcedures](../../../odbc/reference/syntax/sqlprocedures-function.md).  
  
### <a name="related-functions"></a>Funciones relacionadas  
  
|Para información acerca de|Vea|  
|---------------------------|---------|  
|Enlazar un búfer a una columna en un conjunto de resultados|[SQLBindCol (función)](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Cancelación del procesamiento de extractos|[Función SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Devolver información sobre una columna en un conjunto de resultados|[SQLDescribeCol (función)](../../../odbc/reference/syntax/sqldescribecol-function.md)|  
|Ejecución de una instrucción SQL|[Función SQLExecDirect](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|Ejecución de una instrucción SQL preparada|[Función SQLExecute](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|Obtención de un bloque de datos o desplazamiento por un conjunto de resultados|[Función SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|Cerrar el cursor en la declaración|[Función SQLFreeStmt](../../../odbc/reference/syntax/sqlfreestmt-function.md)|  
|Obtención de parte o la totalidad de una columna de datos|[Función SQLGetData](../../../odbc/reference/syntax/sqlgetdata-function.md)|  
|Devolver el número de columnas del conjunto de resultados|[SQLNumResultCols (función)](../../../odbc/reference/syntax/sqlnumresultcols-function.md)|  
|Preparación de una declaración para la ejecución|[Función SQLPrepare](../../../odbc/reference/syntax/sqlprepare-function.md)|  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de la API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Archivos de encabezado de ODBC](../../../odbc/reference/install/odbc-header-files.md)
