---
title: "SQLFetch, función | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLFetch
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLFetch
helpviewer_keywords:
- SQLFetch function [ODBC]
ms.assetid: 6c6611d2-bc6a-4390-87c9-1c5dd9cfe07c
caps.latest.revision: 27
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 135ee130d56801c5da3abb47447a1372d29656a5
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="sqlfetch-function"></a>SQLFetch, función
**Conformidad**  
 Versión introdujo: Cumplimiento de estándares 1.0 de ODBC: ISO 92  
  
 **Resumen**  
 **SQLFetch** recupera el siguiente conjunto de filas de datos del conjunto de resultados y devuelve datos para todas las columnas enlazadas.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
SQLRETURN SQLFetch(  
     SQLHSTMT     StatementHandle);  
```  
  
## <a name="arguments"></a>Argumentos  
 *StatementHandle*  
 [Entrada] Identificador de instrucción.  
  
## <a name="returns"></a>Devuelve  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NO_DATA, SQL_STILL_EXECUTING, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Cuando **SQLFetch** devuelve SQL_ERROR o SQL_SUCCESS_WITH_INFO, un valor SQLSTATE asociado se puede obtener mediante una llamada a [SQLGetDiagRec, función](../../../odbc/reference/syntax/sqlgetdiagrec-function.md) con un *HandleType*de SQL_HANDLE_STMT y un *controlar* de *StatementHandle*. En la tabla siguiente se enumera los valores SQLSTATE suelen ser devueltos por **SQLFetch** y se explica cada uno de ellos en el contexto de esta función; la notación "(DM)" precede a las descripciones de SQLSTATE devuelto por el Administrador de controladores. El código de retorno asociado a cada valor SQLSTATE es SQL_ERROR, a menos que se indique lo contrario. Si se produce un error en una sola columna, [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md) se puede llamar con un *DiagIdentifier* de SQL_DIAG_COLUMN_NUMBER para determinar la columna que se produjo el error; y  **SQLGetDiagField** se puede llamar con un *DiagIdentifier* de SQL_DIAG_ROW_NUMBER para determinar la fila que contiene esa columna.  
  
 Para todas esa SQLSTATE que puede devolver SQL_SUCCESS_WITH_INFO o SQL_ERROR (excepto 01xxx SQLSTATEs), se devuelve SQL_SUCCESS_WITH_INFO, si se produce un error en uno o más, pero no todas las filas de una operación de inserción y se devuelve SQL_ERROR si se produce un error en un operación de varias filas.  
  
|SQLSTATE|Error|Description|  
|--------------|-----------|-----------------|  
|01000|Advertencia general|Mensaje informativo de específicas del controlador. (La función devuelve SQL_SUCCESS_WITH_INFO).|  
|01004|Datos de cadena, delimitado truncados|Cadena o datos binarios devueltos para una columna generó el truncamiento de carácter que no esté vacía o datos binarios no NULL. Si ha realizado un valor de cadena, era truncado a la derecha.|  
|01S01|Error en la fila|Se produjo un error al capturar una o varias filas.<br /><br /> (Si este SQLSTATE se devuelve cuando una aplicación ODBC 3*.x* aplicación está trabajando con una API ODBC 2*.x* controlador, puede hacer caso omiso.)|  
|01S07|Truncamiento fraccionario|Se truncaron los datos devueltos para una columna. Para los tipos de datos numéricos, se trunca la parte fraccionaria del número. De hora, marca de tiempo y los tipos de datos interval que contienen un componente de tiempo, se trunca la parte fraccionaria del tiempo.<br /><br /> (La función devuelve SQL_SUCCESS_WITH_INFO).|  
|07006|Infracción del atributo de tipo de datos restringido|No se pudo convertir el valor de datos de una columna del conjunto de resultados para el tipo de datos especificado por *TargetType* en **SQLBindCol**.<br /><br /> La columna 0 se enlazó con un tipo de datos de SQL_C_BOOKMARK y el atributo de instrucción SQL_ATTR_USE_BOOKMARKS se estableció en SQL_UB_VARIABLE.<br /><br /> La columna 0 se enlazó con un tipo de datos de SQL_C_VARBOOKMARK y no se estableció el atributo de instrucción de SQL_ATTR_USE_BOOKMARKS en SQL_UB_VARIABLE.|  
|07009|Índice de descriptor no válido|El controlador fue un ODBC 2*.x* controlador que no es compatible con **SQLExtendedFetch**, y un número de columna especificado en el enlace para una columna es 0.<br /><br /> Se ha enlazado la columna 0, y el atributo de instrucción SQL_ATTR_USE_BOOKMARKS estaba establecido como SQL_UB_OFF.|  
|08S01|Error de vínculo de comunicación|El vínculo de comunicación entre el controlador y el origen de datos al que se conectó el controlador no pudo antes del procesamiento de la función se ha completado.|  
|22001|Datos de cadena, delimitado truncados|Se ha truncado un marcador de longitud variable devuelto para una columna.|  
|22002|Variable de indicador necesaria, pero no se ha suministrado|Datos nulos se capturan en una columna cuyo *StrLen_or_IndPtr* establecido por **SQLBindCol** (o SQL_DESC_INDICATOR_PTR establecido por **SQLSetDescField** o  **SQLSetDescRec**) era un puntero nulo.|  
|22003|Valor numérico fuera del intervalo|Devolver el valor numérico como numérico o cadena de uno o más columnas enlazadas habría provocado la parte entera (en lugar de fracciones) del número se trunque.<br /><br /> Para obtener más información, consulte [convertir datos de SQL a tipos de datos C](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md) en tipos de datos de apéndice D:.|  
|22007|Formato de datetime no válido|Una columna de caracteres del conjunto de resultados se enlazó a una fecha, hora o estructura de marca de tiempo C, y un valor en la columna era, respectivamente, una fecha no válida, una hora o una marca de tiempo.|  
|22012|División por cero|Devolvió un valor de una expresión aritmética, lo que provocó de división por cero.|  
|22015|Desbordamiento del campo de intervalo|Asignación de un valor numérico exacto o el intervalo de tipo SQL a un tipo de intervalo C causó una pérdida de dígitos significativos en el campo inicial.<br /><br /> Al capturar datos para un tipo de intervalo C, no había ninguna representación del valor del tipo de SQL en el tipo de intervalo C.|  
|22018|Valor de carácter no válido para especificación cast|Una columna de caracteres del conjunto de resultados se enlazó a un búfer de caracteres de C y la columna contiene un carácter para el que se ha producido ninguna representación en el juego de caracteres del búfer.<br /><br /> El tipo C era un numérico exacto o aproximado, una fecha y hora o un tipo de datos del intervalo; el tipo SQL de la columna era un tipo de datos character; y el valor de la columna no es un literal válido del tipo de C enlazado.|  
|24000|Estado de cursor no válido|El *StatementHandle* estaba en un estado ejecutado pero ningún conjunto de resultados se asoció el *StatementHandle*.|  
|40001|Error de serialización.|Se finalizó la transacción en el que se ejecutó la operación de captura para evitar el interbloqueo.|  
|40003|Finalización de instrucciones desconocida|Error en la conexión asociada durante la ejecución de esta función, y no se puede determinar el estado de la transacción.|  
|HY000|Error general|Se produjo un error para que no hubo ninguna SQLSTATE específico y para el que se ha definido ningún SQLSTATE específico de la implementación. El mensaje de error devuelto por **SQLGetDiagRec** en el  *\*MessageText* búfer describe el error y su causa.|  
|HY001|Error de asignación de memoria|El controlador no pudo asignar memoria que es necesario para admitir la ejecución o la finalización de la función.|  
|HY008|Operación cancelada|Procesamiento asincrónico se habilitó para la *StatementHandle*. El **SQLFetch** se llamó a función y antes que completó la ejecución, **SQLCancel** o **SQLCancelHandle** se llamó en la *StatementHandle*. La **SQLFetch** función llamó de nuevo en el *StatementHandle*.<br /><br /> O bien, el **SQLFetch** se llamó a función y antes que completó la ejecución, **SQLCancel** o **SQLCancelHandle** se llamó en la *StatementHandle*  desde un subproceso diferente en una aplicación multiproceso.|  
|HY010|Error de secuencia de función|(DM) se llamó a una función ejecuta de forma asincrónica para el identificador de conexión que está asociado el *StatementHandle*. Esta función asincrónica aún estaba ejecutando cuando el **SQLFetch** se llamó la función.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, o **SQLMoreResults** se llamó para el *StatementHandle* devolvió SQL_PARAM_DATA_ ESTÁ DISPONIBLE. Esta función se invoca antes de que se recuperan los datos para todos los parámetros transmitidos.<br /><br /> (DM) especificado *StatementHandle* no estaba en un estado ejecutado. Se llamó a la función sin antes de llamar a **SQLExecDirect**, **SQLExecute** o una función de catálogo.<br /><br /> (DM) se llamó a una función ejecuta de forma asincrónica (no esta uno) para la *StatementHandle* y aún se estaba ejecutando cuando se llamó a esta función.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, o **SQLSetPos** se llamó para el  *StatementHandle* y devuelve SQL_NEED_DATA. Esta función se invoca antes de que se enviaron los datos para todas las columnas o parámetros de datos en ejecución.<br /><br /> (DM) **SQLFetch** se llamó para el *StatementHandle* después **SQLExtendedFetch** se llamó y antes de **SQLFreeStmt** con el SQL_ Se llamó a la opción de cierre.|  
|HY013|Error de administración de memoria|No se pudo procesar la llamada de función porque los objetos subyacentes de la memoria no se pudieron tener acceso, posiblemente debido a condiciones de memoria insuficiente.|  
|HY090|Longitud de búfer o cadena no válida|El atributo de instrucción SQL_ATTR_USE_BOOKMARK se estableció en SQL_UB_VARIABLE, y la columna 0 se enlazó a un búfer cuya longitud no era igual a la longitud máxima de marcador para este conjunto de resultados. (Este valor de longitud está disponible en el campo SQL_DESC_OCTET_LENGTH de IRD y puede obtenerse mediante una llamada a **SQLDescribeCol**, **SQLColAttribute**, o **SQLGetDescField**.)|  
|HY107|Valor de fila fuera del intervalo|El valor especificado con el atributo de instrucción SQL_ATTR_CURSOR_TYPE SQL_CURSOR_KEYSET_DRIVEN, pero el valor especificado con el atributo de instrucción de SQL_ATTR_KEYSET_SIZE es mayor que 0 y menor que el valor especificado con el SQL_ATTR_ROW_ARRAY_ Atributo de instrucción de tamaño.|  
|HY117|Se suspende la conexión debido al estado de transacción desconocido. Solo se desconecte y se permiten las funciones de solo lectura.|(DM) para obtener más información sobre el estado suspendido, consulte [función SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Característica opcional no implementada|El controlador u origen de datos no admite la conversión especificada por la combinación de la *TargetType* en **SQLBindCol** y el tipo de datos SQL de la columna correspondiente.|  
|HYT00|Se agotó el tiempo de espera|El período de tiempo de espera de consulta expirado antes el origen de datos que devuelve el conjunto de resultados solicitada. El período de tiempo de espera se establece a través de SQLSetStmtAttr, SQL_ATTR_QUERY_TIMEOUT.|  
|HYT01|Tiempo de espera de conexión expirado|El período de tiempo de espera de conexión finalizó antes de que el origen de datos se respondió a la solicitud. El período de tiempo de espera de conexión se establece a través de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Controlador no admite esta función|(DM) el controlador asociado a la *StatementHandle* no admite la función.|  
|IM017|Sondeo está deshabilitado en el modo de notificación asincrónica|Cada vez que se utiliza el modelo de notificación, se deshabilita el sondeo.|  
|IM018|**SQLCompleteAsync** no se ha llamado para completar la operación asincrónica anterior en este identificador.|Si la llamada de función anterior en el controlador devuelve SQL_STILL_EXECUTING y si está habilitado el modo de notificación, **SQLCompleteAsync** se debe llamar en el identificador para realizar el procesamiento posterior a la y completar la operación.|  
  
## <a name="comments"></a>Comentarios  
 **SQLFetch** devuelve el siguiente conjunto de filas del conjunto de resultados. Se puede llamar solo mientras existe un conjunto de resultados: es decir, después de una llamada que crea un conjunto de resultados y antes del cursor se cierra el disco que conjunto de resultados. Si no se enlaza ninguna columna, devuelve los datos en esas columnas. Si la aplicación especifica un puntero a una matriz de estado de fila o un búfer en el que se va a devolver el número de filas recuperadas, **SQLFetch** también devuelve esta información. Las llamadas a **SQLFetch** se puede combinar con llamadas a **SQLFetchScroll** pero no se pueden mezclar con las llamadas a **SQLExtendedFetch**. Para obtener más información, consulte [capturar una fila de datos](../../../odbc/reference/develop-app/fetching-a-row-of-data.md).  
  
 Si una aplicación ODBC 3*.x* aplicación funciona con una API ODBC 2*.x* controlador, el Administrador de controladores asigna **SQLFetch** llama a **SQLExtendedFetch** para un ODBC 2*.x* controlador que admita **SQLExtendedFetch**. Si la API ODBC 2*.x* controlador no admite **SQLExtendedFetch**, se asigna el Administrador de controladores **SQLFetch** llama a **SQLFetch** en la API ODBC 2 *.x* controlador, que se puede recuperar una única fila.  
  
 Para obtener más información, consulte [compatibilidad con versiones anteriores, los cursores desplazables y cursores de bloque](../../../odbc/reference/appendixes/block-cursors-scrollable-cursors-and-backward-compatibility.md) en Apéndice G: controlador directrices para la compatibilidad con versiones anteriores.  
  
## <a name="positioning-the-cursor"></a>Coloque el Cursor  
 Cuando se crea el conjunto de resultados, el cursor se coloca antes del inicio del conjunto de resultados. **SQLFetch** captura el siguiente conjunto de filas. Es equivalente a llamar a **SQLFetchScroll** con *FetchOrientation* establecido en SQL_FETCH_NEXT. Para obtener más información acerca de los cursores, vea [cursores](../../../odbc/reference/develop-app/cursors.md) y [cursores de bloque](../../../odbc/reference/develop-app/block-cursors.md).  
  
 El atributo de instrucción SQL_ATTR_ROW_ARRAY_SIZE especifica el número de filas del conjunto de filas. Si el conjunto de filas que se va a recuperar mediante **SQLFetch** se superpone al final del conjunto de resultados, **SQLFetch** devuelve un conjunto de filas parcial. Es decir, si S + R-1 es mayor que L, donde S es la fila inicial del conjunto de filas que se capturan, R es el tamaño de conjunto de filas y L es la última fila del conjunto de resultados, a continuación, solo el primer L – S + 1 filas del conjunto de filas son válidos. Las filas restantes están vacías y tienen un estado de SQL_ROW_NOROW.  
  
 Después de **SQLFetch** devuelve, la fila actual es la primera fila del conjunto de filas.  
  
 Las reglas que se muestran en la tabla siguiente describen los posicionamiento de cursor después de llamar a **SQLFetch**, en función de las condiciones enumeradas en la segunda tabla en esta sección.  
  
|Condición|Primera fila del conjunto de filas nuevas|  
|---------------|-----------------------------|  
|Antes de inicio|1|  
|*CurrRowsetStart* \< =  *LastResultRow: RowsetSize*[1]|*CurrRowsetStart* + *RowsetSize*[2]|  
|*CurrRowsetStart* > *LastResultRow: RowsetSize*[1]|Al finalizar|  
|Al finalizar|Al finalizar|  
  
 [1] si se cambia el tamaño de conjunto de filas entre capturas, es el tamaño de conjunto de filas que se usó con la captura anterior.  
  
 [2] si se cambia el tamaño de conjunto de filas entre capturas, es el tamaño de conjunto de filas que se usó con la nueva recopilación.  
  
|Notación|Significado|  
|--------------|-------------|  
|Antes de inicio|El cursor de bloque se coloca antes del inicio del conjunto de resultados. Si es la primera fila del conjunto de filas nuevas antes del inicio del conjunto de resultados, **SQLFetch** devuelve SQL_NO_DATA.|  
|Al finalizar|Después de establece el final del resultado, se coloca el cursor de bloque. Si la primera fila del conjunto de filas nuevas es posterior al final del conjunto de resultados, **SQLFetch** devuelve SQL_NO_DATA.|  
|*CurrRowsetStart*|El número de la primera fila del conjunto de filas actual.|  
|*LastResultRow*|El número de la última fila del conjunto de resultados.|  
|*RowsetSize*|El tamaño del conjunto de filas.|  
  
 Por ejemplo, suponga que tiene un conjunto de resultados 100 filas y el tamaño del conjunto de filas es 5. La siguiente tabla muestra el código de conjunto de filas y retorno devuelto por **SQLFetch** para distintas posiciones iniciales.  
  
|Conjunto de filas actual|Código de retorno|Nuevo conjunto de filas|número de filas recuperadas|  
|--------------------|-----------------|----------------|------------------------|  
|Antes de inicio|SQL_SUCCESS|1 a 5|5|  
|1 a 5|SQL_SUCCESS|6 y 10|5|  
|52 a 56|SQL_SUCCESS|57 a 61|5|  
|91 a 95|SQL_SUCCESS|96 a 100|5|  
|93 a 97|SQL_SUCCESS|98 a 100. Filas 4 y 5 de la matriz de Estados de fila se establecen en SQL_ROW_NOROW.|3|  
|96 a 100|SQL_NO_DATA|Ninguno.|0|  
|99 a 100|SQL_NO_DATA|Ninguno.|0|  
|Al finalizar|SQL_NO_DATA|Ninguno.|0|  
  
## <a name="returning-data-in-bound-columns"></a>Devolver datos de las columnas enlazadas  
 Como **SQLFetch** devuelve cada fila, y pone los datos para cada columna enlazada en el búfer enlazado a esa columna. Si no se enlaza ninguna columna, **SQLFetch** avanzar el cursor de bloque, pero no devuelve ningún dato. Todavía se pueden recuperar los datos mediante el uso de **SQLGetData**. Si el cursor es varias filas (es decir, el SQL_ATTR_ROW_ARRAY_SIZE es mayor que 1), **SQLGetData** se puede llamar solo si se devuelve SQL_GD_BLOCK cuando **SQLGetInfo** se llama con un  *Tipo de información* de SQL_GETDATA_EXTENSIONS. (Para obtener más información, consulte [SQLGetData](../../../odbc/reference/syntax/sqlgetdata-function.md).)  
  
 Para cada columna enlazada en una fila, **SQLFetch** hace lo siguiente:  
  
1.  Establece el búfer de longitud/indicador en SQL_NULL_DATA y avanza a la siguiente columna si los datos son NULL. Si los datos son NULL y no se enlaza ningún búfer de longitud/indicador, **SQLFetch** devuelve SQLSTATE 22002 (variable de indicador necesaria, pero no se ha suministrado) para la fila y avanza a la siguiente fila. Para obtener información acerca de cómo determinar la dirección del búfer de longitud/indicador, consulte "Direcciones de búfer" en [SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md).  
  
     Si los datos de la columna no son NULL, **SQLFetch** continúa con el paso 2.  
  
2.  Si el atributo de instrucción SQL_ATTR_MAX_LENGTH se establece en un valor distinto de cero y la columna contiene datos de caracteres o binarias, los datos se truncan a bytes SQL_ATTR_MAX_LENGTH.  
  
    > [!NOTE]  
    >  El atributo de instrucción SQL_ATTR_MAX_LENGTH está pensado para reducir el tráfico de red. Generalmente se implementa mediante el origen de datos, que trunca los datos antes de devolverlo a través de la red. No están necesario controladores y orígenes de datos para admitirla. Por lo tanto, para garantizar que los datos se truncan a un tamaño específico, una aplicación debe asignar un búfer de ese tamaño y especifique el tamaño en el *cbValueMax* argumento en **SQLBindCol**.  
  
3.  Convierte los datos en el tipo especificado por *TargetType* en **SQLBindCol**.  
  
4.  Si los datos se convierten a un tipo de datos de longitud variable, como carácter o binario, **SQLFetch** comprueba si la longitud de los datos supera la longitud del búfer de datos. Si la longitud de datos de caracteres (incluido el carácter de terminación null) supera la longitud del búfer de datos, **SQLFetch** trunca los datos a la longitud del búfer de datos menos la longitud de un carácter de terminación null. A continuación, termina en null los datos. Si la longitud de datos binarios supera la longitud del búfer de datos, **SQLFetch** trunca a la longitud del búfer de datos. La longitud del búfer de datos se especifica con *BufferLength* en **SQLBindCol**.  
  
     **SQLFetch** nunca trunca los datos convierten en datos de longitud fija tipos; siempre da por supuesto que la longitud del búfer de datos es el tamaño del tipo de datos.  
  
5.  Coloca los datos convertidos (y posiblemente truncados) en el búfer de datos. Para obtener información acerca de cómo determinar la dirección del búfer de datos, vea "Direcciones de búfer" en [SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md).  
  
6.  Coloca la longitud de los datos en el búfer de longitud/indicador. Si el puntero del indicador y el puntero de longitud se establecieron en el mismo búfer (como una llamada a **SQLBindCol** does), la longitud se escribe en el búfer de datos válidos y SQL_NULL_DATA se escribe en el búfer de datos de tipo NULL. Si no se enlazó ningún búfer de longitud/indicador, **SQLFetch** no devuelve la longitud.  
  
    -   Para caracteres o datos binarios, esto es la longitud de los datos después de la conversión y antes de truncamiento debido a que el búfer de datos es demasiado pequeño. Si el controlador no puede determinar la longitud de los datos después de la conversión, como sucede en ocasiones con datos de tipo long, Establece la longitud en SQL_NO_TOTAL. Si los datos se truncaron debido al atributo de instrucción de SQL_ATTR_MAX_LENGTH, el valor de este atributo se coloca en el búfer de longitud/indicador en lugar de la longitud real. Esto es porque este atributo está diseñado para truncar datos en el servidor antes de la conversión, por lo que el controlador no tiene ninguna manera de pensar en lo que es la longitud real.  
  
    -   Para todos los demás tipos de datos, esto es la longitud de los datos después de la conversión; es decir, es el tamaño del tipo al que se convierten los datos.  
  
     Para obtener información acerca de cómo determinar la dirección del búfer de longitud/indicador, consulte "Direcciones de búfer" en [SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md).  
  
7.  Si los datos se truncan durante la conversión sin una pérdida de dígitos significativos (por ejemplo, el número real 1,234 se trunca en un entero de 1 al convertir), **SQLFetch** devuelve SQLSTATE 01S07 (truncamiento fraccionario) y SQL_ SUCCESS_WITH_INFO. Si los datos se truncan porque la longitud del búfer de datos es demasiado pequeña (por ejemplo, la cadena "abcdef" se coloca en un búfer de 4 bytes), **SQLFetch** devuelve SQLSTATE 01004 (datos truncados) y SQL_SUCCESS_WITH_INFO. Si los datos se truncan debido al atributo de instrucción SQL_ATTR_MAX_LENGTH, **SQLFetch** devuelve SQL_SUCCESS y no devuelve SQLSTATE 01S07 (truncamiento fraccionario) o SQLSTATE 01004 (datos truncados). Si los datos se truncan durante la conversión con una pérdida de dígitos significativos (por ejemplo, si un valor SQL_INTEGER superior a 100 000 se han convertido a un SQL_C_TINYINT), **SQLFetch** devuelve SQLSTATE 22003 (valor numérico fuera del intervalo) y SQL_ERROR (si el tamaño del conjunto de filas es 1) o SQL_SUCCESS_WITH_INFO (si el tamaño del conjunto de filas es mayor que 1).  
  
 El contenido del búfer de datos enlazados y el búfer de longitud/indicador es indefinido si **SQLFetch** o **SQLFetchScroll** no devuelve SQL_SUCCESS o SQL_SUCCESS_WITH_INFO.  
  
## <a name="row-status-array"></a>Matriz de Estados de fila  
 La matriz de estado de fila se utiliza para devolver el estado de cada fila del conjunto de filas. La dirección de esta matriz se especifica con el atributo de instrucción SQL_ATTR_ROW_STATUS_PTR. La matriz asignada por la aplicación y debe tener tantos elementos como se especifican mediante el atributo de instrucción SQL_ATTR_ROW_ARRAY_SIZE. Sus valores son establecidos por **SQLFetch**, **SQLFetchScroll**, y **SQLBulkOperations** o **SQLSetPos** (excepto cuando ha llamado Después de que se ha colocado el cursor por **SQLExtendedFetch**). Si el valor del atributo de instrucción SQL_ATTR_ROW_STATUS_PTR es un puntero nulo, estas funciones no devuelven el estado de fila.  
  
 El contenido del búfer de la matriz de estado de la fila es indefinido si **SQLFetch** o **SQLFetchScroll** no devuelve SQL_SUCCESS o SQL_SUCCESS_WITH_INFO.  
  
 Los siguientes valores se devuelven en la matriz de Estados de fila.  
  
|Valor de matriz de estado de fila|Description|  
|----------------------------|-----------------|  
|SQL_ROW_SUCCESS|La fila se ha obtenido correctamente y no ha cambiado desde la última vez se recopiló desde este conjunto de resultados.|  
|SQL_ROW_SUCCESS_WITH_INFO|La fila se ha obtenido correctamente y no ha cambiado desde la última vez se recopiló desde este conjunto de resultados. Sin embargo, se devuelve una advertencia acerca de la fila.|  
|SQL_ROW_ERROR|Se produjo un error al capturar la fila.|  
|SQL_ROW_UPDATED [1], [2] y [3]|La fila se ha obtenido correctamente y ha cambiado desde la última vez se recopiló desde este conjunto de resultados. Si la fila se vuelve a recopilar desde este conjunto de resultados o se actualiza de forma **SQLSetPos**, el estado se cambia al estado de la fila nueva.|  
|SQL_ROW_DELETED [3]|Se ha eliminado la fila se capturó en último lugar de este conjunto de resultados.|  
|SQL_ROW_ADDED [4]|La fila se ha insertado por **SQLBulkOperations**. Si la fila se vuelve a recopilar desde este conjunto de resultados o se actualiza de forma **SQLSetPos**, su estado es SQL_ROW_SUCCESS.|  
|SQL_ROW_NOROW|El conjunto de filas había superpuesta al final del conjunto de resultados y se devuelve ninguna fila que correspondía a este elemento de la matriz de estado de fila.|  
  
 [1] para el conjunto de claves, mixtos y dinámicos cursores, si se actualiza un valor de clave, la fila de datos se considera que se haya eliminado y agrega una nueva fila.  
  
 [2] algunos controladores no pueden detectar las actualizaciones de datos y, por tanto, no pueden devolver este valor. Para determinar si un controlador puede detectar las actualizaciones para volver a capturar filas, llama a una aplicación **SQLGetInfo** con la opción SQL_ROW_UPDATES.  
  
 [3] **SQLFetch** puede devolver este valor solo cuando es entremezclado con llamadas a **SQLFetchScroll**. Esto es porque **SQLFetch** avanza a través del conjunto de resultados y cuando se utiliza exclusivamente, no volver a obtener todas las filas. Dado que ninguna fila se volver a capturar, **SQLFetch** no detecta los cambios realizados en filas capturadas anteriormente. Sin embargo, si **SQLFetchScroll** coloca el cursor antes de cualquier capturado previamente filas y **SQLFetch** se utiliza para capturar las filas, **SQLFetch** puede detectar los cambios realizados en las filas.  
  
 [4] devolviendo SQLBulkOperations solo. No establece **SQLFetch** o **SQLFetchScroll**.  
  
### <a name="rows-fetched-buffer"></a>Búfer de captura de filas  
 Las filas recuperadas búfer se utiliza para devolver el número de filas recuperadas, incluidas las filas para el que se recibió ningún dato porque se produjo un error mientras se estaban que se va a recuperar. En otras palabras, es el número de filas para el que el valor de la matriz de Estados de fila no es SQL_ROW_NOROW. La dirección de este búfer se especifica con el atributo de instrucción SQL_ATTR_ROWS_FETCHED_PTR. El búfer asignado por la aplicación. Está establecido de forma **SQLFetch** y **SQLFetchScroll**. Si el valor del atributo de instrucción SQL_ATTR_ROWS_FETCHED_PTR es un puntero nulo, estas funciones no devuelven el número de filas recuperadas. Para determinar el número de la fila actual del conjunto de resultados, una aplicación puede llamar a **SQLGetStmtAttr** con el atributo SQL_ATTR_ROW_NUMBER.  
  
 El contenido del búfer de filas recuperadas es indefinido si **SQLFetch** o **SQLFetchScroll** no devuelve SQL_SUCCESS o SQL_SUCCESS_WITH_INFO, excepto cuando se devuelve SQL_NO_DATA, en cuyo caso el valor en las filas del búfer de captura se establece en 0.  
  
### <a name="error-handling"></a>Tratamiento de errores  
 Errores y advertencias pueden aplicar a las filas individuales o a toda la función. Para obtener más información acerca de los registros de diagnóstico, vea [diagnósticos](../../../odbc/reference/develop-app/diagnostics.md) y [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md).  
  
#### <a name="errors-and-warnings-on-the-entire-function"></a>Errores y advertencias en toda la función  
 Si un error se aplica a toda la función, como SQLSTATE HYT00 (tiempo de espera expirado) o SQLSTATE 24000 (estado de cursor no válido), **SQLFetch** devuelve SQL_ERROR y el valor de SQLSTATE es aplicable. El contenido de los búferes de conjunto de filas no está definido y la posición del cursor se ha modificado.  
  
 Si una advertencia se aplica a toda la función **SQLFetch** devuelve SQL_SUCCESS_WITH_INFO y SQLSTATE es aplicable. Se devuelven los registros de estado para las advertencias que se aplican a toda la función antes de los registros de estado que se aplican a las filas individuales.  
  
#### <a name="errors-and-warnings-in-individual-rows"></a>Errores y advertencias en filas individuales  
 Si un error (por ejemplo, SQLSTATE 22012 (división por cero)) o una advertencia (por ejemplo, SQLSTATE 01004 (datos truncados)) se aplica a una sola fila, **SQLFetch**hace lo siguiente:  
  
-   Establece el elemento correspondiente de la matriz de Estados de fila en SQL_ROW_ERROR si hay errores o SQL_ROW_SUCCESS_WITH_INFO para las advertencias.  
  
-   Agrega cero o más registros de estado que contienen SqlState para el error o advertencia.  
  
-   Establece los campos de número de filas y columnas en los registros de estado. Si **SQLFetch** no se puede determinar el número de fila o columna, establece ese número en SQL_ROW_NUMBER_UNKNOWN o SQL_COLUMN_NUMBER_UNKNOWN, respectivamente. Si el registro de estado no se aplica a una columna concreta, **SQLFetch** establece el número de columna en SQL_NO_COLUMN_NUMBER.  
  
 **SQLFetch** continúa capturar las filas hasta que han capturado todas las filas del conjunto de filas. Devuelve SQL_SUCCESS_WITH_INFO, a menos que se produce un error en cada fila del conjunto de filas (sin incluir filas con el estado SQL_ROW_NOROW), en cuyo caso devuelve SQL_ERROR. En concreto, si el tamaño del conjunto de filas es 1 y se produce un error en esa fila, **SQLFetch** devuelve SQL_ERROR.  
  
 **SQLFetch** devuelve los registros de estado en el orden de número de fila. Es decir, devuelve todos los registros de estado para las filas desconocidos (si existe); a continuación devuelve todos los registros de estado para la primera fila (si existe) y, a continuación, devuelve todos los registros de estado para la segunda fila (si existe) y así sucesivamente. Los registros de estado para cada fila se ordenan según las reglas habituales para ordenar los registros de estado; Para obtener más información, vea "Secuencia de registros de estado" en [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md).  
  
### <a name="descriptors-and-sqlfetch"></a>Descriptores y SQLFetch  
 Las secciones siguientes describen cómo **SQLFetch** interactúa con descriptores.  
  
#### <a name="argument-mappings"></a>Asignaciones de argumento  
 El controlador no establece los campos de descriptor en función de los argumentos de **SQLFetch**.  
  
#### <a name="other-descriptor-fields"></a>Otros campos de Descriptor  
 Los siguientes campos de descriptor usan **SQLFetch**.  
  
|Campo descriptor|Desc.|Campo de|Establecer a través de|  
|----------------------|-----------|--------------|-----------------|  
|SQL_DESC_ARRAY_SIZE|DESCARTAR|Encabezado|Atributo de instrucción de SQL_ATTR_ROW_ARRAY_SIZE|  
|SQL_DESC_ARRAY_STATUS_PTR|IRD|Encabezado|Atributo de instrucción de SQL_ATTR_ROW_STATUS_PTR|  
|SQL_DESC_BIND_OFFSET_PTR|DESCARTAR|Encabezado|Atributo de instrucción de SQL_ATTR_ROW_BIND_OFFSET_PTR|  
|SQL_DESC_BIND_TYPE|DESCARTAR|Encabezado|Atributo de instrucción SQL_ATTR_ROW_BIND_TYPE|  
|SQL_DESC_COUNT|DESCARTAR|Encabezado|*ColumnNumber* argumento de **SQLBindCol**|  
|SQL_DESC_DATA_PTR|DESCARTAR|Registros|*TargetValuePtr* argumento de **SQLBindCol**|  
|SQL_DESC_INDICATOR_PTR|DESCARTAR|Registros|*StrLen_or_IndPtr* argumento en **SQLBindCol**|  
|SQL_DESC_OCTET_LENGTH|DESCARTAR|Registros|*BufferLength* argumento en **SQLBindCol**|  
|SQL_DESC_OCTET_LENGTH_PTR|DESCARTAR|Registros|*StrLen_or_IndPtr* argumento en **SQLBindCol**|  
|SQL_DESC_ROWS_PROCESSED_PTR|IRD|Encabezado|Atributo de instrucción de SQL_ATTR_ROWS_FETCHED_PTR|  
|SQL_DESC_TYPE|DESCARTAR|Registros|*TargetType* argumento en **SQLBindCol**|  
  
 También pueden establecerse a través de todos los campos de descriptor **SQLSetDescField**.  
  
#### <a name="separate-length-and-indicator-buffers"></a>Longitud independiente y búferes de indicador  
 Las aplicaciones pueden enlazar un único búfer o dos búferes independientes que pueden usarse para contener valores de longitud y el indicador. Cuando una aplicación llama **SQLBindCol**, el controlador establece los campos SQL_DESC_OCTET_LENGTH_PTR y SQL_DESC_INDICATOR_PTR de la descartar en la misma dirección, que se pasa en el *StrLen_or_IndPtr* argumento pasado. Cuando una aplicación llama **SQLSetDescField** o **SQLSetDescRec**, se pueden establecer estos dos campos en las diferentes direcciones.  
  
 **SQLFetch** determina si especifica la aplicación independiente de los búferes de longitud y el indicador. En este caso, cuando los datos que no son NULL, **SQLFetch** el búfer de indicador se establece en 0 y devuelve la longitud del búfer de longitud. Cuando los datos son NULL, **SQLFetch** establece el búfer de indicador en SQL_NULL_DATA y no la modifica el búfer de longitud.  
  
### <a name="code-example"></a>Ejemplo de código  
 Vea [SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md), [SQLColumns](../../../odbc/reference/syntax/sqlcolumns-function.md), [SQLGetData](../../../odbc/reference/syntax/sqlgetdata-function.md), y [SQLProcedures](../../../odbc/reference/syntax/sqlprocedures-function.md).  
  
### <a name="related-functions"></a>Funciones relacionadas  
  
|Para obtener información acerca de|Vea|  
|---------------------------|---------|  
|Enlazar un búfer con una columna en un conjunto de resultados|[SQLBindCol (función)](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Cancelar el procesamiento de una instrucción|[SQLCancel, función](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Devolver información acerca de una columna en un conjunto de resultados|[SQLDescribeCol (función)](../../../odbc/reference/syntax/sqldescribecol-function.md)|  
|Ejecutar una instrucción SQL|[SQLExecDirect, función](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|Ejecutar una instrucción SQL preparada|[SQLExecute, función](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|Captura un bloque de datos o desplazarse a través de un resultado de conjunto|[SQLFetchScroll, función](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|Cierre el cursor en la instrucción|[SQLFreeStmt, función](../../../odbc/reference/syntax/sqlfreestmt-function.md)|  
|Capturar parte o la totalidad de una columna de datos|[SQLGetData, función](../../../odbc/reference/syntax/sqlgetdata-function.md)|  
|Columnas del conjunto de devolver el número de resultados|[SQLNumResultCols (función)](../../../odbc/reference/syntax/sqlnumresultcols-function.md)|  
|Preparar una instrucción de ejecución|[Función SQLPrepare](../../../odbc/reference/syntax/sqlprepare-function.md)|  
  
## <a name="see-also"></a>Vea también  
 [Referencia de la API de ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Archivos de encabezado de ODBC](../../../odbc/reference/install/odbc-header-files.md)

