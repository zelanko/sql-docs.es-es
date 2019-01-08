---
title: Función SQLFetch | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 001238b4e5d47b22ca991efcd8b4ee28971d7af7
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/11/2018
ms.locfileid: "53213094"
---
# <a name="sqlfetch-function"></a>Función SQLFetch
**Conformidad**  
 Versión de introducción: Cumplimiento de estándares 1.0 de ODBC: 92 ISO  
  
 **Resumen**  
 **SQLFetch** recupera el siguiente conjunto de filas de datos del conjunto de resultados y devuelve datos para todas las columnas enlazadas.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
SQLRETURN SQLFetch(  
     SQLHSTMT     StatementHandle);  
```  
  
## <a name="arguments"></a>Argumentos  
 *StatementHandle*  
 [Entrada] Identificador de instrucción.  
  
## <a name="returns"></a>Devuelve  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NO_DATA, SQL_STILL_EXECUTING, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Cuando **SQLFetch** devuelve SQL_ERROR o SQL_SUCCESS_WITH_INFO, un valor SQLSTATE asociado se puede obtener mediante una llamada a [función SQLGetDiagRec](../../../odbc/reference/syntax/sqlgetdiagrec-function.md) con un *HandleType*de SQL_HANDLE_STMT y un *controlar* de *StatementHandle*. En la tabla siguiente se enumera los valores SQLSTATE devueltos normalmente por **SQLFetch** y se explica cada uno de ellos en el contexto de esta función; la notación "(DM)" precede a las descripciones de SQLSTATE devuelto por el Administrador de controladores. El código de retorno asociado a cada valor SQLSTATE es SQL_ERROR, a menos que se indique lo contrario. Si se produce un error en una sola columna, [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md) se puede llamar con un *DiagIdentifier* de SQL_DIAG_COLUMN_NUMBER para determinar la columna que se produjo el error; y  **SQLGetDiagField** se puede llamar con un *DiagIdentifier* de SQL_DIAG_ROW_NUMBER para determinar la fila que contiene esa columna.  
  
 Para todas esas SQLSTATE que puede devolver SQL_SUCCESS_WITH_INFO o SQL_ERROR (excepto 01xxx SQLSTATEs), se devuelve SQL_SUCCESS_WITH_INFO, si se produce un error en uno o más, pero no todas las filas de una operación de varias filas, y se devuelve SQL_ERROR si se produce un error en un fila única operación.  
  
|SQLSTATE|Error|Descripción|  
|--------------|-----------|-----------------|  
|01000|Advertencia general|Específico del controlador de mensaje informativo. (La función devuelve SQL_SUCCESS_WITH_INFO).|  
|01004|Datos de cadena derecha truncados|Cadena o datos binarios devueltos para una columna produjeron el truncamiento de carácter no en blanco o datos binarios que no son NULL. Si fuese un valor de cadena, era truncado a la derecha.|  
|01S01|Error en la fila|Se produjo un error al capturar una o varias filas.<br /><br /> (Si este SQLSTATE se devuelve cuando una aplicación ODBC 3 *.x* aplicación funciona con un ODBC 2 *.x* controlador, se puede hacer caso omiso.)|  
|01S07|Truncamiento fraccionario|Se truncaron los datos devueltos para una columna. Para los tipos de datos numéricos, se ha truncado la parte fraccionaria del número. Para hora, marca de tiempo y los tipos de datos interval que contienen un componente de tiempo, se trunca la parte fraccionaria del tiempo.<br /><br /> (La función devuelve SQL_SUCCESS_WITH_INFO).|  
|07006|Infracción del atributo de tipo de datos restringido|No se pudo convertir el valor de datos de una columna del conjunto de resultados para el tipo de datos especificado por *TargetType* en **SQLBindCol**.<br /><br /> La columna 0 se enlazó con un tipo de datos de SQL_C_BOOKMARK y se ha establecido el atributo de instrucción SQL_ATTR_USE_BOOKMARKS a SQL_UB_VARIABLE.<br /><br /> La columna 0 se enlazó con un tipo de datos de SQL_C_VARBOOKMARK y el atributo de instrucción SQL_ATTR_USE_BOOKMARKS no se estableció en SQL_UB_VARIABLE.|  
|07009|Índice de descriptor no válido|El controlador fue un 2 de ODBC *.x* controlador que no es compatible con **SQLExtendedFetch**, y un número de columna especificado en el enlace para una columna era 0.<br /><br /> Se enlazó a la columna 0 y se ha establecido el atributo de instrucción SQL_ATTR_USE_BOOKMARKS a SQL_UB_OFF.|  
|08S01|Error de vínculo de comunicación|Error en el vínculo de comunicación entre el controlador y el origen de datos a la que se ha conectado el controlador antes del procesamiento de la función se ha completado.|  
|22001|Datos de cadena derecha truncados|Se ha truncado un marcador de longitud variable devuelto para una columna.|  
|22002|Variable de indicador necesaria pero no proporcionado|Datos nulos se capturan en una columna cuya propiedad *StrLen_or_IndPtr* establecido por **SQLBindCol** (o SQL_DESC_INDICATOR_PTR establecido por **SQLSetDescField** o  **SQLSetDescRec**) era un puntero nulo.|  
|22003|Valor numérico fuera del intervalo|Devuelve el valor numérico como numérico o cadena de uno o más columnas enlazadas habría causado la parte entera (en contraposición a fraccionarios) del número que se va a truncar.<br /><br /> Para obtener más información, consulte [convertir datos de SQL a tipos de datos C](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md) en el apéndice D: Tipos de datos.|  
|22007|Formato de datetime no válido|Una columna de caracteres del conjunto de resultados se enlazó con una fecha, hora o estructura de marca de tiempo C y un valor en la columna era, respectivamente, una fecha no válida, la hora o marca de tiempo.|  
|22012|División por cero|Devolvió un valor de una expresión aritmética, lo que resultó en la división por cero.|  
|22015|Desbordamiento de campo de intervalo|Asignación de un valor numérico exacto o el intervalo de tipo SQL a un tipo de intervalo C causó una pérdida de dígitos significativos en el campo inicial.<br /><br /> Al capturar datos para un tipo de intervalo de C, no hubo ninguna representación del valor del tipo SQL en el tipo de intervalo C.|  
|22018|Valor de carácter no válido para especificación cast|Una columna de caracteres del conjunto de resultados estaba enlazada a un búfer de caracteres de C y la columna contiene un carácter para el que se ha producido ninguna representación en el juego de caracteres del búfer.<br /><br /> El tipo C era un numérico exacto o aproximado, una fecha y hora o un tipo de datos del intervalo; el tipo SQL de la columna era un tipo de datos de caracteres; y el valor de la columna no es un literal válido de tipo C enlazado.|  
|24000|Estado de cursor no válido|El *StatementHandle* estaba en un estado ejecutado pero se ha asociado ningún conjunto de resultados la *StatementHandle*.|  
|40001|Error de serialización.|Se terminó la transacción en el que se ejecutó la operación de captura para evitar el interbloqueo.|  
|40003|Finalización de instrucción desconocida|Error en la conexión asociada durante la ejecución de esta función y no se puede determinar el estado de la transacción.|  
|HY000|Error general|Se produjo un error para que se ha producido ningún SQLSTATE específico y para los que se ha definido ningún SQLSTATE específicos de la implementación. El mensaje de error devuelto por **SQLGetDiagRec** en el  *\*MessageText* búfer describe el error y su causa.|  
|HY001|Error de asignación de memoria|El controlador no pudo asignar memoria que es necesario para admitir la ejecución o la finalización de la función.|  
|HY008|Operación cancelada|Procesamiento asincrónico se habilitó para la *StatementHandle*. El **SQLFetch** se llamó a la función, y antes que completó la ejecución, **SQLCancel** o **SQLCancelHandle** se ha llamado en el *StatementHandle*. El **SQLFetch** función se llamó de nuevo en el *StatementHandle*.<br /><br /> O bien, el **SQLFetch** se llamó a la función, y antes que completó la ejecución, **SQLCancel** o **SQLCancelHandle** se ha llamado en el *StatementHandle*  desde un subproceso diferente en una aplicación multiproceso.|  
|HY010|Error de secuencia de función|(DM) se llamó a una función que se ejecuta de forma asincrónica para el identificador de conexión que está asociado el *StatementHandle*. Aún estaba ejecutando esta función asincrónica cuando el **SQLFetch** se llamó a la función.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, o **SQLMoreResults** se llamó para el *StatementHandle* y devuelven SQL_PARAM_DATA_ ESTÁ DISPONIBLE. Esta función se invoca antes de que se recuperan los datos para todos los parámetros transmitidos.<br /><br /> (DM) especificado *StatementHandle* no estaba en un estado ejecutado. Se llamó a la función sin llamar primero a **SQLExecDirect**, **SQLExecute** o una función de catálogo.<br /><br /> (DM) se llamó a una función que se ejecuta asincrónicamente (no ésta) para el *StatementHandle* y aún se estaba ejecutando cuando se llamó a esta función.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, o **SQLSetPos** se llamó para el  *StatementHandle* y devuelve SQL_NEED_DATA. Esta función se invoca antes de que se enviaron datos para todas las columnas o parámetros de datos en ejecución.<br /><br /> (DM) **SQLFetch** se llamó para el *StatementHandle* después **SQLExtendedFetch** llamó y antes de **SQLFreeStmt** con el SQL_ Se llamó a la opción Cerrar.|  
|HY013|Error de administración de memoria|No se pudo procesar la llamada de función porque los objetos de memoria subyacente no se podrían tener acceso, posiblemente debido a memoria insuficiente.|  
|HY090|Longitud de búfer o cadena no válida|El atributo de instrucción SQL_ATTR_USE_BOOKMARK se estableció en SQL_UB_VARIABLE y la columna 0 estaba enlazada a un búfer cuya longitud no es igual a la longitud máxima para el marcador para este conjunto de resultados. (Esta longitud está disponible en el campo SQL_DESC_OCTET_LENGTH de IRD y se puede obtener mediante una llamada a **SQLDescribeCol**, **SQLColAttribute**, o **SQLGetDescField**.)|  
|HY107|Valor de fila fuera del intervalo|El valor especificado con el atributo de instrucción SQL_ATTR_CURSOR_TYPE era SQL_CURSOR_KEYSET_DRIVEN, pero el valor especificado con el atributo de instrucción SQL_ATTR_KEYSET_SIZE era mayor que 0 y menor que el valor especificado con el SQL_ATTR_ROW_ARRAY_ Atributo de instrucción de tamaño.|  
|HY117|Conexión está suspendida debido al estado de transacción desconocido. Solo se desconecte y se permiten funciones de solo lectura.|(DM) para obtener más información sobre el estado suspendido, consulte [función SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Característica opcional no implementada|El controlador u origen de datos no admite la conversión especificada por la combinación de la *TargetType* en **SQLBindCol** y el tipo de datos SQL de la columna correspondiente.|  
|HYT00|Se agotó el tiempo de espera|Ha expirado el período de tiempo de espera de consulta antes del origen de datos devuelve el conjunto de resultados solicitada. El período de tiempo de espera se establece a través de SQLSetStmtAttr, SQL_ATTR_QUERY_TIMEOUT.|  
|HYT01|Tiempo de espera de conexión agotado|Ha expirado el período de tiempo de espera de conexión antes de que el origen de datos que respondió a la solicitud. El período de tiempo de espera de conexión se establece a través de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Controlador no admite esta función|(DM) el controlador asociado con el *StatementHandle* no admite la función.|  
|IM017|Sondeo se deshabilita en modo de notificación asincrónica|Cada vez que se usa el modelo de notificación, se deshabilita el sondeo.|  
|IM018|**SQLCompleteAsync** no se ha llamado para completar la operación asincrónica anterior en este identificador.|Si la llamada de función anterior en el controlador devuelve SQL_STILL_EXECUTING y si está habilitado el modo de notificación, **SQLCompleteAsync** debe llamarse en el identificador para realizar el procesamiento posterior y completar la operación.|  
  
## <a name="comments"></a>Comentarios  
 **SQLFetch** devuelve el siguiente conjunto de filas del conjunto de resultados. Se puede llamar solo mientras existe un conjunto de resultados: es decir, después de una llamada que crea un conjunto de resultados y antes del cursor se cierra sobre que el conjunto de resultados. Si todas las columnas están enlazadas, devuelve los datos en esas columnas. Si la aplicación ha especificado un puntero a una matriz de Estados de fila o un búfer en el que se va a devolver el número de filas recuperadas, **SQLFetch** también devuelve esta información. Las llamadas a **SQLFetch** se pueden combinar con llamadas a **SQLFetchScroll** pero no se pueden mezclar con las llamadas a **SQLExtendedFetch**. Para obtener más información, consulte [capturar una fila de datos](../../../odbc/reference/develop-app/fetching-a-row-of-data.md).  
  
 Si una aplicación ODBC 3 *.x* aplicación trabaja con un ODBC 2 *.x* controlador, el Administrador de controladores asigna **SQLFetch** las llamadas a **SQLExtendedFetch** para un ODBC 2 *.x* controlador que admita **SQLExtendedFetch**. Si la API ODBC 2 *.x* controlador no es compatible con **SQLExtendedFetch**, asigna el Administrador de controladores **SQLFetch** las llamadas a **SQLFetch** en ODBC 2 *.x* controlador, que se puede recuperar una única fila.  
  
 Para obtener más información, consulte [cursores de bloque, cursores desplazables y compatibilidad con versiones anteriores](../../../odbc/reference/appendixes/block-cursors-scrollable-cursors-and-backward-compatibility.md) en Apéndice G: Directrices de controlador para la compatibilidad con versiones anteriores.  
  
## <a name="positioning-the-cursor"></a>Sitúe el Cursor  
 Cuando se crea el conjunto de resultados, el cursor se coloca antes del inicio del conjunto de resultados. **SQLFetch** Obtiene el siguiente conjunto de filas. Equivale a llamar a **SQLFetchScroll** con *FetchOrientation* establecido en SQL_FETCH_NEXT. Para obtener más información acerca de los cursores, vea [cursores](../../../odbc/reference/develop-app/cursors.md) y [cursores de bloque](../../../odbc/reference/develop-app/block-cursors.md).  
  
 El atributo de instrucción SQL_ATTR_ROW_ARRAY_SIZE especifica el número de filas del conjunto de filas. Si el conjunto de filas que se va a buscar por **SQLFetch** se superpone al final del conjunto de resultados, **SQLFetch** devuelve un conjunto de filas parcial. Es decir, si S + R - 1 es mayor que L, donde S es la fila inicial del conjunto de filas que se capturan, R es el tamaño del conjunto de filas y L es la última fila del conjunto de resultados, a continuación, solo el primer L - S + 1 filas del conjunto de filas son válidas. Las filas restantes están vacías y tienen un estado de SQL_ROW_NOROW.  
  
 Después de **SQLFetch** que devuelve la fila actual es la primera fila del conjunto de filas.  
  
 Las reglas enumeradas en la tabla siguiente describen la colocación de los cursores después de llamar a **SQLFetch**, según las condiciones enumeradas en la segunda tabla en esta sección.  
  
|Condición|Primera fila del conjunto de filas nuevas|  
|---------------|-----------------------------|  
|Antes de comenzar|1|  
|*CurrRowsetStart* \< =  *LastResultRow - RowsetSize*[1]|*CurrRowsetStart* + *RowsetSize*[2]|  
|*CurrRowsetStart* > *LastResultRow - RowsetSize*[1]|Después de finales|  
|Después de finales|Después de finales|  
  
 [1] si se cambia el tamaño del conjunto de filas entre capturas, esto es el tamaño del conjunto de filas que se usó con la captura anterior.  
  
 [2] si se cambia el tamaño del conjunto de filas entre capturas, esto es el tamaño del conjunto de filas que se usó con la nueva recopilación.  
  
|Notación|Significado|  
|--------------|-------------|  
|Antes de comenzar|El cursor de bloque se coloca antes del inicio del conjunto de resultados. Si es la primera fila del nuevo conjunto de filas antes del inicio del conjunto de resultados, **SQLFetch** devuelve SQL_NO_DATA.|  
|Después de finales|Después de establece el final del resultado, se coloca el cursor de bloque. Si es la primera fila del conjunto de filas nuevo después del final del conjunto de resultados, **SQLFetch** devuelve SQL_NO_DATA.|  
|*CurrRowsetStart*|El número de la primera fila del conjunto de filas actual.|  
|*LastResultRow*|El número de la última fila del conjunto de resultados.|  
|*RowsetSize*|El tamaño del conjunto de filas.|  
  
 Por ejemplo, supongamos que tiene un conjunto de resultados 100 filas y el tamaño del conjunto de filas es 5. En la tabla siguiente se muestra el código de conjunto de filas y de retorno devuelto por **SQLFetch** para distintas posiciones de inicio.  
  
|Conjunto de filas actual|Código de retorno|Nuevo conjunto de filas|número de filas recuperadas|  
|--------------------|-----------------|----------------|------------------------|  
|Antes de comenzar|SQL_SUCCESS|1 a 5|5|  
|1 a 5|SQL_SUCCESS|6 a 10|5|  
|52 a 56|SQL_SUCCESS|57 a 61|5|  
|91 a 95|SQL_SUCCESS|96 a 100|5|  
|93 a 97|SQL_SUCCESS|98 a 100. Las filas 4 y 5 de la matriz de Estados de fila se establecen en SQL_ROW_NOROW.|3|  
|96 a 100|SQL_NO_DATA|Ninguno.|0|  
|99 a 100|SQL_NO_DATA|Ninguno.|0|  
|Después de finales|SQL_NO_DATA|Ninguno.|0|  
  
## <a name="returning-data-in-bound-columns"></a>Devolver datos en las columnas enlazadas  
 Como **SQLFetch** devuelve cada fila, y pone los datos para cada columna enlazada en el búfer enlazado a esa columna. Si no hay columnas están enlazadas, **SQLFetch** avanzar el cursor de bloque, pero no devuelve ningún dato. Todavía se pueden recuperar los datos mediante el uso de **SQLGetData**. Si el cursor es acumulativo (es decir, el SQL_ATTR_ROW_ARRAY_SIZE es mayor que 1), **SQLGetData** se puede llamar solo si se devuelve SQL_GD_BLOCK cuando **SQLGetInfo** se denomina con un  *InfoType* de SQL_GETDATA_EXTENSIONS. (Para obtener más información, consulte [SQLGetData](../../../odbc/reference/syntax/sqlgetdata-function.md).)  
  
 Para cada columna enlazada en una fila, **SQLFetch** hace lo siguiente:  
  
1.  Establece el búfer de longitud/indicador en SQL_NULL_DATA y continúa con la siguiente columna, si los datos son NULL. Si los datos están NULL y no hay ningún búfer de longitud/indicador se enlazó, **SQLFetch** devuelve SQLSTATE 22002 se necesita una (variable de indicador necesaria pero no se proporciona) para la fila y avanza a la siguiente fila. Para obtener información acerca de cómo determinar la dirección del búfer de longitud/indicador, vea "Direcciones de búfer" en [SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md).  
  
     Si los datos de la columna no están NULL, **SQLFetch** avanza al paso 2.  
  
2.  Si el atributo de instrucción SQL_ATTR_MAX_LENGTH se establece en un valor distinto de cero y la columna contiene datos de caracteres o binarias, los datos se truncan a bytes SQL_ATTR_MAX_LENGTH.  
  
    > [!NOTE]  
    >  El atributo de instrucción SQL_ATTR_MAX_LENGTH está pensado para reducir el tráfico de red. Por lo general se implementa mediante el origen de datos que se trunca los datos antes de devolverlo a través de la red. Los controladores y orígenes de datos no tienen que lo admiten. Por lo tanto, para garantizar que los datos se truncan hasta un tamaño determinado, una aplicación debe asignar un búfer de ese tamaño y especifique el tamaño en el *cbValueMax* argumento en **SQLBindCol**.  
  
3.  Convierte los datos en el tipo especificado por *TargetType* en **SQLBindCol**.  
  
4.  Si los datos se convierten a un tipo de datos de longitud variable, como carácter o binario, **SQLFetch** comprueba si la longitud de los datos supera la longitud del búfer de datos. Si la longitud de datos de caracteres (incluido el carácter de terminación null) supera la longitud del búfer de datos, **SQLFetch** trunca los datos a la longitud del búfer de datos menos la longitud de un carácter de terminación null. A continuación, null-finaliza los datos. Si la longitud de datos binarios supera la longitud del búfer de datos, **SQLFetch** lo trunca a la longitud del búfer de datos. La longitud del búfer de datos se especifica con *BufferLength* en **SQLBindCol**.  
  
     **SQLFetch** nunca trunca los datos convierten en datos de longitud fija tipos; siempre se supone que la longitud del búfer de datos es el tamaño del tipo de datos.  
  
5.  Coloca los datos convertidos (y posiblemente truncados) en el búfer de datos. Para obtener información acerca de cómo determinar la dirección del búfer de datos, vea "Direcciones de búfer" en [SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md).  
  
6.  La longitud de los datos se coloca en el búfer de longitud/indicador. Si el puntero del indicador y el puntero de longitud se establecieron en el mismo búfer (como una llamada a **SQLBindCol** does), la longitud se escribe en el búfer de datos válidos y SQL_NULL_DATA se escribe en el búfer de datos de tipo NULL. Si no hay ningún búfer de longitud/indicador estaba enlazada, **SQLFetch** no devuelve la longitud.  
  
    -   Para caracteres o datos binarios, esto es la longitud de los datos después de la conversión y antes del truncamiento debido a que el búfer de datos es demasiado pequeño. Si el controlador no puede determinar la longitud de los datos después de la conversión, como sucede en ocasiones con datos de tipo long, Establece la longitud a SQL_NO_TOTAL. Si se truncaron los datos debido al atributo de instrucción SQL_ATTR_MAX_LENGTH, el valor de este atributo se coloca en el búfer de longitud/indicador en lugar de la longitud real. Esto es porque este atributo está diseñado para truncar los datos en el servidor antes de la conversión, para que el controlador no tiene ninguna manera de averiguar la longitud real es.  
  
    -   Para los demás tipos de datos, esto es la longitud de los datos después de la conversión; es decir, es el tamaño del tipo al que se ha convertido los datos.  
  
     Para obtener información acerca de cómo determinar la dirección del búfer de longitud/indicador, vea "Direcciones de búfer" en [SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md).  
  
7.  Si se truncan los datos durante la conversión sin pérdida de dígitos significativos (por ejemplo, se trunca el número real 1,234 al entero de 1 al convertir), **SQLFetch** devuelve SQLSTATE 01S07 (truncamiento fraccionario) y SQL_ SUCCESS_WITH_INFO. Si los datos se truncan porque la longitud del búfer de datos es demasiado pequeña (por ejemplo, la cadena "abcdef" se coloca en un búfer de 4 bytes), **SQLFetch** devuelve SQL_SUCCESS_WITH_INFO y SQLSTATE 01004 (datos truncados) el. Si los datos se truncan debido al atributo de instrucción SQL_ATTR_MAX_LENGTH, **SQLFetch** devuelve SQL_SUCCESS y no devuelve SQLSTATE 01S07 (truncamiento fraccionario) o SQLSTATE 01004 (datos truncados). Si los datos se truncan durante la conversión con una pérdida de dígitos significativos (por ejemplo, si un valor SQL_INTEGER superior a 100.000 se convirtieron en un SQL_C_TINYINT) **SQLFetch** devuelve SQLSTATE 22003 (valor numérico fuera del intervalo) y SQL_ERROR (si el tamaño del conjunto de filas es 1) o SQL_SUCCESS_WITH_INFO (si el tamaño del conjunto de filas es mayor que 1).  
  
 El contenido del búfer de datos enlazados y el búfer de longitud/indicador es indefinido si **SQLFetch** o **SQLFetchScroll** no devuelve SQL_SUCCESS o SQL_SUCCESS_WITH_INFO.  
  
## <a name="row-status-array"></a>Matriz de Estados de fila  
 La matriz de Estados de fila se utiliza para devolver el estado de cada fila del conjunto de filas. La dirección de esta matriz se especifica con el atributo de instrucción SQL_ATTR_ROW_STATUS_PTR. La matriz asignada por la aplicación y debe tener tantos elementos como se especifican mediante el atributo de instrucción SQL_ATTR_ROW_ARRAY_SIZE. Sus valores se establecen mediante **SQLFetch**, **SQLFetchScroll**, y **SQLBulkOperations** o **SQLSetPos** (excepto cuando ha llamado Después de que se ha colocado el cursor por **SQLExtendedFetch**). Si el valor del atributo de instrucción SQL_ATTR_ROW_STATUS_PTR es un puntero nulo, estas funciones no devuelven el estado de fila.  
  
 El contenido del búfer de matriz de estado de fila es indefinido si **SQLFetch** o **SQLFetchScroll** no devuelve SQL_SUCCESS o SQL_SUCCESS_WITH_INFO.  
  
 Los siguientes valores se devuelven en la matriz de Estados de fila.  
  
|Valor de matriz de estado de fila|Descripción|  
|----------------------------|-----------------|  
|SQL_ROW_SUCCESS|La fila se capturó correctamente y no ha cambiado desde que se capturó por última vez este conjunto de resultados.|  
|SQL_ROW_SUCCESS_WITH_INFO|La fila se capturó correctamente y no ha cambiado desde que se capturó por última vez este conjunto de resultados. Sin embargo, se devuelve una advertencia acerca de la fila.|  
|SQL_ROW_ERROR|Se produjo un error al capturar la fila.|  
|SQL_ROW_UPDATED [1], [2] y [3]|La fila se capturó correctamente y ha cambiado desde que se capturó por última vez este conjunto de resultados. Si la fila se vuelve a recopilar desde este conjunto de resultados o se actualiza de forma **SQLSetPos**, el estado cambia a estado de la fila nueva.|  
|SQL_ROW_DELETED [3]|La fila se ha eliminado desde que se capturó por última vez este conjunto de resultados.|  
|SQL_ROW_ADDED [4]|La fila se insertó por **SQLBulkOperations**. Si la fila se vuelve a recopilar desde este conjunto de resultados o se actualiza de forma **SQLSetPos**, su estado es SQL_ROW_SUCCESS.|  
|SQL_ROW_NOROW|El conjunto de filas había superpuesto al final del conjunto de resultados y no se devolvió ninguna fila que correspondía a este elemento de la matriz de Estados de fila.|  
  
 [1] para el conjunto de claves, mixtos y dinámicos cursores, si se actualiza un valor de clave, se considera que se haya eliminado la fila de datos y agrega una nueva fila.  
  
 [2] algunos controladores no pueden detectar las actualizaciones de datos y, por tanto, no pueden devolver este valor. Para determinar si un controlador puede detectar las actualizaciones para volver a capturar filas, una aplicación llama a **SQLGetInfo** con la opción SQL_ROW_UPDATES.  
  
 [3] **SQLFetch** puede devolver este valor sólo cuando es combinar con las llamadas a **SQLFetchScroll**. Esto es porque **SQLFetch** avanza por el conjunto de resultados y cuando se utiliza exclusivamente, no volver a obtener las filas. Dado que no es volver a capturar ninguna fila, **SQLFetch** no detecta los cambios realizados en las filas capturadas anteriormente. Sin embargo, si **SQLFetchScroll** coloca el cursor antes de cualquier capturado previamente las filas y **SQLFetch** se utiliza para capturar las filas, **SQLFetch** puede detectar los cambios realizados en las filas.  
  
 [4] devuelve SQLBulkOperations solo. No se establece **SQLFetch** o **SQLFetchScroll**.  
  
### <a name="rows-fetched-buffer"></a>Búfer de filas capturadas  
 Las filas al búfer de captura se utiliza para devolver el número de filas recuperado, incluidas las filas que no se devolvió ningún dato porque se produjo un error mientras se recuperan. En otras palabras, es el número de filas para el que el valor de la matriz de Estados de fila no es SQL_ROW_NOROW. La dirección de este búfer se especifica con el atributo de instrucción SQL_ATTR_ROWS_FETCHED_PTR. El búfer asignado por la aplicación. Se establece de forma **SQLFetch** y **SQLFetchScroll**. Si el valor del atributo SQL_ATTR_ROWS_FETCHED_PTR instrucción es un puntero nulo, estas funciones no devuelven el número de filas recuperadas. Para determinar el número de la fila actual del conjunto de resultados, puede llamar una aplicación **SQLGetStmtAttr** con el atributo SQL_ATTR_ROW_NUMBER.  
  
 El contenido del búfer de filas recuperadas es indefinido si **SQLFetch** o **SQLFetchScroll** no devuelve SQL_SUCCESS o SQL_SUCCESS_WITH_INFO, excepto cuando se devuelve SQL_NO_DATA, en cuyo caso el valor en las filas del búfer de captura se establece en 0.  
  
### <a name="error-handling"></a>Tratamiento de errores  
 Errores y advertencias pueden aplicar a filas individuales o a toda la función. Para obtener más información acerca de los registros de diagnóstico, consulte [diagnósticos](../../../odbc/reference/develop-app/diagnostics.md) y [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md).  
  
#### <a name="errors-and-warnings-on-the-entire-function"></a>Errores y advertencias en toda la función  
 Si un error se aplica a toda la función, como SQLSTATE HYT00 (tiempo de espera agotado) o SQLSTATE 24000 (estado de cursor no válido), **SQLFetch** devuelve SQL_ERROR y el valor de SQLSTATE aplicable. El contenido de los búferes del conjunto de filas no está definido y no se ha modificado la posición del cursor.  
  
 Si una advertencia que se aplica a toda la función **SQLFetch** devuelve SQL_SUCCESS_WITH_INFO y SQLSTATE aplicable. Se devuelven los registros de estado para las advertencias que se aplican a toda la función antes de los registros de estado que se aplican a las filas individuales.  
  
#### <a name="errors-and-warnings-in-individual-rows"></a>Errores y advertencias en filas individuales  
 Si un error (por ejemplo, SQLSTATE 22012 (división por cero)) o una advertencia (por ejemplo, SQLSTATE 01004 (datos truncados)) se aplica a una sola fila, **SQLFetch**hace lo siguiente:  
  
-   Establece el elemento correspondiente de la matriz de Estados de fila en SQL_ROW_ERROR SQL_ROW_SUCCESS_WITH_INFO posibles errores o advertencias.  
  
-   Agrega cero o más registros de estado que contienen el SqlState para el error o advertencia.  
  
-   Establece los campos de número de filas y columnas en los registros de estado. Si **SQLFetch** no se puede determinar el número de fila o columna, establece ese número en SQL_ROW_NUMBER_UNKNOWN o SQL_COLUMN_NUMBER_UNKNOWN, respectivamente. Si el registro de estado no es aplicable a una columna en particular, **SQLFetch** establece el número de columna en SQL_NO_COLUMN_NUMBER.  
  
 **SQLFetch** continúa capturar las filas hasta que captura todas las filas del conjunto de filas. Devuelve SQL_SUCCESS_WITH_INFO, a menos que se produce un error en todas las filas del conjunto de filas (sin incluir las filas con estado SQL_ROW_NOROW), en cuyo caso devuelve SQL_ERROR. En concreto, si el tamaño del conjunto de filas es 1 y se produce un error en esa fila, **SQLFetch** devuelve SQL_ERROR.  
  
 **SQLFetch** devuelve los registros de estado en el orden de número de fila. Es decir, devuelve todos los registros de estado de filas desconocidos (si existe); a continuación devuelve todos los registros de estado de la primera fila (si existe) y, a continuación, devuelve todos los registros de estado de la segunda fila (si existe) y así sucesivamente. Los registros de estado para cada fila se ordenan según las reglas normales para ordenar los registros de estado; Para obtener más información, vea "Secuencia de registros de estado" en [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md).  
  
### <a name="descriptors-and-sqlfetch"></a>Descriptores y SQLFetch  
 Las secciones siguientes describen cómo **SQLFetch** interactúa con los descriptores.  
  
#### <a name="argument-mappings"></a>Asignaciones de argumento  
 El controlador no establece los campos de descriptor en función de los argumentos de **SQLFetch**.  
  
#### <a name="other-descriptor-fields"></a>Otros campos de Descriptor  
 Los siguientes campos de descriptor que se usan por **SQLFetch**.  
  
|Campo descriptor|Desc.|Campo en|Establecer a través de|  
|----------------------|-----------|--------------|-----------------|  
|SQL_DESC_ARRAY_SIZE|DESCARTAR|Encabezado|Atributo de instrucción SQL_ATTR_ROW_ARRAY_SIZE|  
|SQL_DESC_ARRAY_STATUS_PTR|IRD|Encabezado|Atributo de instrucción SQL_ATTR_ROW_STATUS_PTR|  
|SQL_DESC_BIND_OFFSET_PTR|DESCARTAR|Encabezado|Atributo de instrucción SQL_ATTR_ROW_BIND_OFFSET_PTR|  
|SQL_DESC_BIND_TYPE|DESCARTAR|Encabezado|Atributo de instrucción SQL_ATTR_ROW_BIND_TYPE|  
|SQL_DESC_COUNT|DESCARTAR|Encabezado|*ColumnNumber* argumento de **SQLBindCol**|  
|SQL_DESC_DATA_PTR|DESCARTAR|Registros|*TargetValuePtr* argumento de **SQLBindCol**|  
|SQL_DESC_INDICATOR_PTR|DESCARTAR|Registros|*StrLen_or_IndPtr* argumento en **SQLBindCol**|  
|SQL_DESC_OCTET_LENGTH|DESCARTAR|Registros|*BufferLength* argumento en **SQLBindCol**|  
|SQL_DESC_OCTET_LENGTH_PTR|DESCARTAR|Registros|*StrLen_or_IndPtr* argumento en **SQLBindCol**|  
|SQL_DESC_ROWS_PROCESSED_PTR|IRD|Encabezado|Atributo de instrucción SQL_ATTR_ROWS_FETCHED_PTR|  
|SQL_DESC_TYPE|DESCARTAR|Registros|*TargetType* argumento en **SQLBindCol**|  
  
 También pueden establecerse a través de todos los campos de descriptor **SQLSetDescField**.  
  
#### <a name="separate-length-and-indicator-buffers"></a>Longitud independiente y búferes de indicador  
 Las aplicaciones pueden enlazar a un único búfer o dos búferes independientes que se pueden usar para contener valores de longitud y el indicador. Cuando una aplicación llama **SQLBindCol**, el controlador establece los campos SQL_DESC_OCTET_LENGTH_PTR y SQL_DESC_INDICATOR_PTR del descartar a la misma dirección, que se pasa en el *StrLen_or_IndPtr* argumento. Cuando una aplicación llama **SQLSetDescField** o **SQLSetDescRec**, se pueden establecer estos dos campos en diferentes direcciones.  
  
 **SQLFetch** determina si la aplicación ha especificado búferes independientes de longitud y el indicador. En este caso, cuando los datos que no son NULL, **SQLFetch** el búfer de indicador se establece en 0 y devuelve la longitud del búfer de longitud. Cuando los datos son NULL, **SQLFetch** establece el búfer de indicador en SQL_NULL_DATA y no modifica el búfer de longitud.  
  
### <a name="code-example"></a>Ejemplo de código  
 Consulte [SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md), [SQLColumns](../../../odbc/reference/syntax/sqlcolumns-function.md), [SQLGetData](../../../odbc/reference/syntax/sqlgetdata-function.md), y [SQLProcedures](../../../odbc/reference/syntax/sqlprocedures-function.md).  
  
### <a name="related-functions"></a>Funciones relacionadas  
  
|Para obtener información acerca de|Vea|  
|---------------------------|---------|  
|Enlazar un búfer con una columna en un conjunto de resultados|[Función SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Procesamiento de una instrucción de cancelación|[Función SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Devolver información acerca de una columna en un conjunto de resultados|[Función SQLDescribeCol](../../../odbc/reference/syntax/sqldescribecol-function.md)|  
|Ejecutar una instrucción SQL|[Función SQLExecDirect](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|Ejecutar una instrucción SQL preparada|[Función SQLExecute](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|Obtención de un bloque de datos o desplazarse a través de un resultado de conjunto|[Función SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|Cierre el cursor en la instrucción|[Función SQLFreeStmt](../../../odbc/reference/syntax/sqlfreestmt-function.md)|  
|Capturando la totalidad o parte de una columna de datos|[Función SQLGetData](../../../odbc/reference/syntax/sqlgetdata-function.md)|  
|Columnas del conjunto de devolver el número de resultados|[Función SQLNumResultCols](../../../odbc/reference/syntax/sqlnumresultcols-function.md)|  
|Preparar una instrucción de ejecución|[Función SQLPrepare](../../../odbc/reference/syntax/sqlprepare-function.md)|  
  
## <a name="see-also"></a>Vea también  
 [Referencia de la API de ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Archivos de encabezado de ODBC](../../../odbc/reference/install/odbc-header-files.md)
