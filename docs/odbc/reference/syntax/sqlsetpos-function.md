---
title: Función SQLSetPos ???????????? Microsoft Docs
ms.custom: ''
ms.date: 07/18/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLSetPos
apilocation:
- sqlsrv32.dll
- odbc32.dll
apitype: dllExport
f1_keywords:
- SQLSetPos
helpviewer_keywords:
- SQLSetPos function [ODBC]
ms.assetid: 80190ee7-ae3b-45e5-92a9-693eb558f322
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7a8839f1ae540ac9e5f29e144f7f57fb754e50ff
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81287335"
---
# <a name="sqlsetpos-function"></a>Función SQLSetPos
**Conformidad**  
 Versión introducida: Cumplimiento de estándares ODBC 1.0: ODBC  
  
 **Resumen**  
 **SQLSetPos** establece la posición del cursor en un conjunto de filas y permite a una aplicación actualizar datos en el conjunto de filas o actualizar o eliminar datos en el conjunto de resultados.  
  
## <a name="syntax"></a>Sintaxis  
  
```cpp  
  
SQLRETURN SQLSetPos(  
      SQLHSTMT        StatementHandle,  
      SQLSETPOSIROW   RowNumber,  
      SQLUSMALLINT    Operation,  
      SQLUSMALLINT    LockType);  
```  
  
## <a name="arguments"></a>Argumentos  
 *StatementHandle*  
 [Entrada] Identificador de instrucción.  
  
 *RowNumber*  
 [Entrada] Posición de la fila en el conjunto de filas en el que se realizará la operación especificada con el *operación* argumento. Si *RowNumber* es 0, la operación se aplica a todas las filas del conjunto de filas.  
  
 Para obtener información adicional, consulte "Comentarios."  
  
 *Operación*  
 [Entrada] Operación para realizar:  
  
 SQL_POSITION SQL_REFRESH SQL_UPDATE SQL_DELETE  
  
> [!NOTE]
>  El valor SQL_ADD del argumento *Operation* ha quedado en desuso para ODBC *3.x*. Los controladores ODBC *3.x* necesitarán admitir SQL_ADD para la compatibilidad con versiones anteriores. Esta funcionalidad se ha reemplazado por una llamada a **SQLBulkOperations** con una *operación* de SQL_ADD. Cuando una aplicación ODBC *3.x* funciona con un controlador ODBC *2.x,* el Administrador de controladores asigna una llamada a **SQLBulkOperations** con una *operación* de SQL_ADD a **SQLSetPos** con una *operación* de SQL_ADD.  
  
 Para obtener más información, consulte "Comentarios."  
  
 *LockType*  
 [Entrada] Especifica cómo bloquear la fila después de realizar la operación especificada en el *operación* argumento.  
  
 SQL_LOCK_NO_CHANGE SQL_LOCK_EXCLUSIVE SQL_LOCK_UNLOCK  
  
 Para obtener más información, consulte "Comentarios."  
  
 **Devuelve**  
  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NEED_DATA, SQL_STILL_EXECUTING, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnóstico  
 Cuando **SQLSetPos** devuelve SQL_ERROR o SQL_SUCCESS_WITH_INFO, se puede obtener un valor SQLSTATE asociado llamando a **SQLGetDiagRec** con un *HandleType* de SQL_HANDLE_STMT y un *Control* de *StatementHandle*. En la tabla siguiente se enumeran los valores SQLSTATE devueltos normalmente por **SQLSetPos** y se explica cada uno de ellos en el contexto de esta función; la notación "(DM)" precede a las descripciones de SQLSTATEs devueltas por el Administrador de controladores. El código de retorno asociado a cada valor SQLSTATE se SQL_ERROR, a menos que se indique lo contrario.  
  
 Para todos aquellos SQLSTATEs que pueden devolver SQL_SUCCESS_WITH_INFO o SQL_ERROR (excepto 01xxx SQLSTATEs), se devuelve SQL_SUCCESS_WITH_INFO si se produce un error en una o más filas, pero no en todas, de una operación de varias filas y SQL_ERROR se devuelve si se produce un error en una operación de una sola fila.  
  
|SQLSTATE|Error|Descripción|  
|--------------|-----------|-----------------|  
|01000|Advertencia general|Mensaje informativo específico del controlador. (La función devuelve SQL_SUCCESS_WITH_INFO.)|  
|01001|Conflicto de operación del cursor|El *operación* argumento era SQL_DELETE o SQL_UPDATE y no se eliminó o actualizó ninguna fila o más de una fila. (Para obtener más información acerca de las actualizaciones de más de una fila, vea la descripción del *atributo* SQL_ATTR_SIMULATE_CURSOR en **SQLSetStmtAttr**.) (La función devuelve SQL_SUCCESS_WITH_INFO.)<br /><br /> El *operación* argumento era SQL_DELETE o SQL_UPDATE y la operación falló debido a la simultaneidad optimista. (La función devuelve SQL_SUCCESS_WITH_INFO.)|  
|01004|Truncamiento de la derecha de datos de cadena|El *Operación* argumento era SQL_REFRESH y datos de cadena o binarios devueltos para una columna o columnas con un tipo de datos de SQL_C_CHAR o SQL_C_BINARY dio lugar al truncamiento de caracteres no en blanco o datos binarios no NULL.|  
|01S01|Error en la fila|El *RowNumber* argumento era 0, y se produjo un error en una o más filas al realizar la operación especificada con el *Operation* argumento.<br /><br /> (SQL_SUCCESS_WITH_INFO se devuelve si se produce un error en una o varias filas, pero no en todas, filas de una operación de varias filas y se devuelve SQL_ERROR si se produce un error en una operación de una sola fila.)<br /><br /> (Este SQLSTATE se devuelve solo cuando **SQLSetPos** se llama después de **SQLExtendedFetch**, si el controlador es un controlador ODBC *2.x* y no se utiliza la biblioteca de cursores.)|  
|01S07|Truncamiento fraccionario|El *Operación* argumento era SQL_REFRESH, el tipo de datos del búfer de aplicación no era SQL_C_CHAR ni SQL_C_BINARY y los datos devueltos a los búferes de aplicación para una o varias columnas se truncaron. Para los tipos de datos numéricos, la parte fraccionaria del número se truncó. Para los tipos de datos time, timestamp e interval que contienen un componente de tiempo, la parte fraccionaria del tiempo se truncó.<br /><br /> (La función devuelve SQL_SUCCESS_WITH_INFO.)|  
|07006|Infracción de atributo de tipo de datos restringido|El valor de datos de una columna del conjunto de resultados no se pudo convertir al tipo de datos especificado por *TargetType* en la llamada a **SQLBindCol**.|  
|07009|Indice de descriptor no válido|El argumento *Operation* se SQL_REFRESH o SQL_UPDATE y una columna se enlazaba con un número de columna mayor que el número de columnas del conjunto de resultados.|  
|21S02|El grado de la tabla derivada no coincide con la lista de columnas|El argumento *Operation* se SQL_UPDATE y no se puede cambiar ninguna columna porque todas las columnas estaban sin enlazar, de solo lectura o el valor del búfer de longitud/indicador enlazado estaba SQL_COLUMN_IGNORE.|  
|22001|Datos de cadena, truncamiento a la derecha|El *Operación* argumento se SQL_UPDATE y la asignación de un carácter o valor binario a una columna dio lugar a la truncación de caracteres no en blanco (para caracteres) o no nulos (para caracteres binarios) o bytes.|  
|22003|Valor numérico fuera del rango|El argumento *Operation* se SQL_UPDATE y la asignación de un valor numérico a una columna del conjunto de resultados hizo truncar la parte completa (en lugar de fraccionaria) del número.<br /><br /> El argumento *Operation* se SQL_REFRESH y devolver el valor numérico de una o más columnas enlazadas habría causado una pérdida de dígitos significativos.|  
|22007|Formato de fecha y hora no válido|El argumento *Operación* se SQL_UPDATE y la asignación de un valor de fecha o marca de tiempo a una columna del conjunto de resultados hizo que el campo de año, mes o día estuviera fuera del intervalo.<br /><br /> El argumento *Operation* se SQL_REFRESH y devolver el valor de fecha o marca de tiempo para una o más columnas enlazadas habría provocado que el campo de año, mes o día estuviera fuera del intervalo.|  
|22008|Desbordamiento del campo de fecha y hora|El argumento *Operation* se SQL_UPDATE y el rendimiento de la aritmética datetime en los datos que se envían a una columna del conjunto de resultados dio como resultado un campo datetime (el campo year, month, day, hour, minute o second) del resultado que está fuera del intervalo de valores permitido para el campo o no es válido en función de las reglas naturales del calendario gregoriano para las fechas y horas.<br /><br /> El argumento *Operation* se SQL_REFRESH, y el rendimiento de la aritmética datetime en los datos que se recuperan del conjunto de resultados dio como resultado un campo datetime (el campo year, month, day, hour, minute o second) del resultado fuera del intervalo de valores permitido para el campo o no es válido en función de las reglas naturales del calendario gregoriano para datetimes.|  
|22015|Desbordamiento de campo de intervalo|El *operación* argumento se SQL_UPDATE y la asignación de un tipo numérico exacto o de intervalo C a un intervalo DE tipo de datos SQL causó una pérdida de dígitos significativos.<br /><br /> El argumento *Operation* era SQL_UPDATE; al asignar a un tipo SQL de intervalo, no había ninguna representación del valor del tipo C en el tipo SQL de intervalo.<br /><br /> El *operación* argumento se SQL_REFRESH y la asignación de un tipo SQL numérico o de intervalo exacto a un tipo de intervalo C causó una pérdida de dígitos significativos en el campo inicial.<br /><br /> El *operación* argumento era SQL_ REFRESH; al asignar a un tipo de intervalo C, no había ninguna representación del valor del tipo SQL en el tipo de intervalo C.|  
|22018|Valor de carácter no válido para la especificación de conversión|El argumento *Operation* fue SQL_REFRESH; el tipo C era un número exacto o aproximado, una fecha y hora o un tipo de datos de intervalo; el tipo SQL de la columna era un tipo de datos de carácter; y el valor de la columna no era un literal válido del tipo C enlazado.<br /><br /> El argumento *Operación* fue SQL_UPDATE; el tipo SQL era un número exacto o aproximado, una fecha y hora o un tipo de datos de intervalo; el tipo C se SQL_C_CHAR; y el valor de la columna no era un literal válido del tipo SQL enlazado.|  
|23000|Violación de la restricción de integridad|El argumento *Operation* fue SQL_DELETE o SQL_UPDATE y se ha infringido una restricción de integridad.|  
|24000|Estado de cursor no válido|El *StatementHandle* estaba en un estado ejecutado, pero no se asoció ningún conjunto de resultados con *StatementHandle*.<br /><br /> (DM) un cursor estaba abierto en el *StatementHandle*, pero **SQLFetch** o **SQLFetchScroll** no se había llamado.<br /><br /> Un cursor estaba abierto en el *StatementHandle*, y **SQLFetch** o **SQLFetchScroll** se había llamado, pero el cursor se colocó antes del inicio del conjunto de resultados o después del final del conjunto de resultados.<br /><br /> El argumento *Operation* se SQL_DELETE, SQL_REFRESH o SQL_UPDATE y el cursor se colocó antes del inicio del conjunto de resultados o después del final del conjunto de resultados.|  
|40001|Error de serialización|La transacción se revirtió debido a un interbloqueo de recursos con otra transacción.|  
|40003|Finalización de la declaración desconocida|Error en la conexión asociada durante la ejecución de esta función y no se puede determinar el estado de la transacción.|  
|42000|Error de sintaxis o violación de acceso|El controlador no pudo bloquear la fila según sea necesario para realizar la operación solicitada en el argumento *Operation*.<br /><br /> El controlador no pudo bloquear la fila como se solicitó en el argumento *LockType*.|  
|44000|Infracción de WITH CHECK OPTION|El *operación* argumento se SQL_UPDATE y la actualización se realizó en una tabla vista o una tabla derivada de la tabla vista que se creó especificando **WITH CHECK OPTION**, de modo que una o varias filas afectadas por la actualización ya no estarán presentes en la tabla vista.|  
|HY000|Error general|Se ha producido un error para el que no se ha definido sqlSTATE específico y para el que no se ha definido sqlSTATE específico de la implementación. El mensaje de error devuelto por **SQLGetDiagRec** en el * \*messageText* búfer describe el error y su causa.|  
|HY001|Error de asignación de memoria|El controlador no pudo asignar la memoria necesaria para admitir la ejecución o finalización de la función.|  
|HY008|Operación cancelada|El procesamiento asincrónico se ha habilitado para *StatementHandle*. Se llamó a la función y antes de completar la ejecución, **sqlCancel** o **SQLCancelHandle** se llamó en el *StatementHandle*, y, a continuación, se llamó a la función de nuevo en el *StatementHandle*.<br /><br /> Se llamó a la función y antes de completar la ejecución, **SQLCancel** o **SQLCancelHandle** se llamó en el *StatementHandle* desde un subproceso diferente en una aplicación multiproceso.|  
|HY010|Error de secuencia de funciones|(DM) se llamó a una función de ejecución asincrónica para el identificador de conexión asociado a *StatementHandle*. Esta función asincrónica todavía se estaba ejecutando cuando se llamó a la función SQLSetPos.<br /><br /> (DM) el *StatementHandle* especificado no estaba en un estado ejecutado. Se llamó a la función sin llamar primero a **SQLExecDirect**, **SQLExecute**o una función de catálogo.<br /><br /> (DM) se llamó a una función de ejecución asincrónica (no esta) para el *StatementHandle* y todavía se estaba ejecutando cuando se llamó a esta función.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, o **SQLSetPos** se llamó para el *StatementHandle* y devuelto SQL_NEED_DATA. Se llamó a esta función antes de que se enviaran datos para todos los parámetros o columnas de datos en ejecución.<br /><br /> (DM) el controlador era un controlador ODBC *2.x* y **SQLSetPos** se llamó para un *StatementHandle* después de **SQLFetch** se llamó.|  
|HY011|Atributo no se puede establecer ahora|(DM) El controlador era un controlador ODBC *2.x;* se estableció el atributo de instrucción SQL_ATTR_ROW_STATUS_PTR; a continuación, **sqlSetPos** se llamó antes **de SQLFetch**, **SQLFetchScroll**, o **SQLExtendedFetch** se llamó.|  
|HY013|Error de administración de memoria|No se pudo procesar la llamada de función porque no se pudo tener acceso a los objetos de memoria subyacentes, posiblemente debido a condiciones de poca memoria.|  
|HY090|Cadena no válida o longitud de búfer|El *Operación* argumento era SQL_UPDATE, un valor de datos era un puntero nulo y el valor de longitud de columna no era 0, SQL_DATA_AT_EXEC, SQL_COLUMN_IGNORE, SQL_NULL_DATA o menor o igual que SQL_LEN_DATA_AT_EXEC_OFFSET.<br /><br /> El argumento *Operation* era SQL_UPDATE; un valor de datos no era un puntero nulo; el tipo de datos C era SQL_C_BINARY o SQL_C_CHAR; y el valor de longitud de columna era menor que 0 pero no igual que SQL_DATA_AT_EXEC, SQL_COLUMN_IGNORE, SQL_NTS o SQL_NULL_DATA, o menor o igual que SQL_LEN_DATA_AT_EXEC_OFFSET.<br /><br /> El valor de un búfer de longitud/indicador se SQL_DATA_AT_EXEC; el tipo SQL era SQL_LONGVARCHAR, SQL_LONGVARBINARY o un tipo de datos específico del origen de datos largo; y el tipo de información SQL_NEED_LONG_DATA_LEN en **SQLGetInfo** era "Y".|  
|HY092|Identificador de atributo no válido|(DM) el valor especificado para el *operación* argumento no era válido.<br /><br /> (DM) el valor especificado para el *LockType* argumento no era válido.<br /><br /> El *operación* argumento era SQL_UPDATE o SQL_DELETE y el atributo de instrucción SQL_ATTR_CONCURRENCY se SQL_ATTR_CONCUR_READ_ONLY.|  
|HY107|Valor de fila fuera del rango|El valor especificado para el argumento *RowNumber* era mayor que el número de filas del conjunto de filas.|  
|HY109|Posición del cursor no válida|El cursor asociado con el *StatementHandle* se definió como de solo avance, por lo que el cursor no se pudo colocar dentro del conjunto de filas. Vea la descripción del atributo SQL_ATTR_CURSOR_TYPE en **SQLSetStmtAttr**.<br /><br /> El *operación* argumento era SQL_UPDATE, SQL_DELETE o SQL_REFRESH, y la fila identificada por el *RowNumber* argumento se había eliminado o no se había capturado.<br /><br /> (DM) El *RowNumber* argumento era 0, y el *Operation* argumento fue SQL_POSITION.<br /><br /> **SQLSetPos** se llamó después **de SQLBulkOperations** se llamó y antes **de SQLFetchScroll** o **SQLFetch** se llamó.|  
|HY117|La conexión se suspende debido al estado de transacción desconocido. Solo se permiten funciones de desconexión y de solo lectura.|(DM) Para obtener más información sobre el estado suspendido, vea [SqlEndTran (función).](../../../odbc/reference/syntax/sqlendtran-function.md)|  
|HYC00|Característica opcional no implementada|El controlador o el origen de datos no admite la operación solicitada en el *operación* argumento o el *LockType* argumento.|  
|HYT00|Tiempo de espera agotado|El período de tiempo de espera de la consulta expiró antes de que el origen de datos devolviera el conjunto de resultados. El período de tiempo de espera se establece a través de **SQLSetStmtAttr** con un *atributo* de SQL_ATTR_QUERY_TIMEOUT.|  
|HYT01|Tiempo de espera de conexión expirado|El período de tiempo de espera de conexión expiró antes de que el origen de datos respondiera a la solicitud. El período de tiempo de espera de conexión se establece a través de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|El controlador no admite esta función|(DM) El controlador asociado con el *StatementHandle* no admite la función.|  
|IM017|El sondeo está deshabilitado en el modo de notificación asincrónica|Siempre que se utiliza el modelo de notificación, el sondeo está deshabilitado.|  
|IM018|**SQLCompleteAsync** no se ha llamado para completar la operación asincrónica anterior en este identificador.|Si la llamada de función anterior en el identificador devuelve SQL_STILL_EXECUTING y si el modo de notificación está habilitado, **sqlCompleteAsync** debe llamarse en el identificador para realizar el procesamiento posterior y completar la operación.|  
  
## <a name="comments"></a>Comentarios  
  
> [!CAUTION]
>  Para obtener información sobre los estados de instrucción que se pueden llamar a **SQLSetPos** y lo que debe hacer para la compatibilidad con aplicaciones ODBC *2.x,* vea cursores de [bloque, cursores desplazables y compatibilidad con versiones anteriores](../../../odbc/reference/appendixes/block-cursors-scrollable-cursors-and-backward-compatibility.md).  
  
## <a name="rownumber-argument"></a>Argumento RowNumber  
 El *RowNumber* argumento especifica el número de la fila en el conjunto de filas en el que se va a realizar la operación especificada por el *Operation* argumento. Si *RowNumber* es 0, la operación se aplica a todas las filas del conjunto de filas. *RowNumber* debe ser un valor de 0 al número de filas del conjunto de filas.  
  
> [!NOTE]  
>  En el lenguaje C, las matrices se basan en 0 y el argumento *RowNumber* se basa en 1. Por ejemplo, para actualizar la quinta fila del conjunto de filas, una aplicación modifica los búferes del conjunto de filas en el índice de matriz 4, pero especifica un *RowNumber* de 5.  
  
 Todas las operaciones colocan el cursor en la fila especificada por *RowNumber*. Las siguientes operaciones requieren una posición del cursor:  
  
-   Instrucciones de actualización y eliminación posicionadas.  
  
-   Llamadas a **SQLGetData**.  
  
-   Llamadas a **SQLSetPos** con las opciones SQL_DELETE, SQL_REFRESH y SQL_UPDATE.  
  
 Por ejemplo, si *RowNumber* es 2 para una llamada a **SQLSetPos** con una *operación* de SQL_DELETE, el cursor se coloca en la segunda fila del conjunto de filas y se elimina esa fila. La entrada de la matriz de estado de fila de implementación (señalada por el atributo de instrucción SQL_ATTR_ROW_STATUS_PTR) para la segunda fila se cambia a SQL_ROW_DELETED.  
  
 Una aplicación puede especificar una posición de cursor cuando llama a **SQLSetPos**. Por lo general, llama a **SQLSetPos** con la operación SQL_POSITION o SQL_REFRESH para colocar el cursor antes de ejecutar una instrucción de actualización o eliminación posicionada o llamar a **SQLGetData**.  
  
## <a name="operation-argument"></a>Argumento de la operación  
 El *operación* argumento admite las siguientes operaciones. Para determinar qué opciones admite un origen de datos, una aplicación llama a **SQLGetInfo** con el tipo de información SQL_DYNAMIC_CURSOR_ATTRIBUTES1, SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1, SQL_KEYSET_CURSOR_ATTRIBUTES1 o SQL_STATIC_CURSOR_ATTRIBUTES1 (según el tipo del cursor).  
  
|*Operación*<br /><br /> Argumento|Operación|  
|------------------------------|---------------|  
|SQL_POSITION|El controlador coloca el cursor en la fila especificada por *RowNumber*.<br /><br /> El contenido de la matriz de estado de fila a la que apunta el atributo de instrucción SQL_ATTR_ROW_OPERATION_PTR se omite para el SQL_POSITION *Operation*.|  
|SQL_REFRESH|El controlador coloca el cursor en la fila especificada por *RowNumber* y actualiza los datos en los búferes del conjunto de filas para esa fila. Para obtener más información acerca de cómo el controlador devuelve datos en los búferes de conjunto de filas, vea las descripciones de enlace de fila y columna en **SQLBindCol**.<br /><br /> **SQLSetPos** con una *operación* de SQL_REFRESH actualiza el estado y el contenido de las filas dentro del conjunto de filas capturado actual. Esto incluye la actualización de los marcadores. Dado que los datos de los búferes se actualizan pero no se vuelven a grabar, la pertenencia al conjunto de filas es fija. Esto es diferente de la actualización realizada por una llamada a **SQLFetchScroll** con un *FetchOrientation* de SQL_FETCH_RELATIVE y un *RowNumber* igual a 0, que recupera el conjunto de filas del conjunto de resultados para que pueda mostrar los datos agregados y quitar los datos eliminados si esas operaciones son compatibles con el controlador y el cursor.<br /><br /> Una actualización correcta con **SQLSetPos** no cambiará el estado de una fila de SQL_ROW_DELETED. Las filas eliminadas dentro del conjunto de filas seguirán marcando como eliminadas hasta la siguiente captura. Las filas desaparecerán en la siguiente captura si el cursor admite el empaquetado (en el que un **SQLFetch** posterior o **SQLFetchScroll** no devuelve filas eliminadas).<br /><br /> Las filas agregadas no aparecen cuando se realiza una actualización con **SQLSetPos.** Este comportamiento es diferente de **SQLFetchScroll** con un *FetchType* de SQL_FETCH_RELATIVE y un *RowNumber* igual a 0, que también actualiza el conjunto de filas actual, pero mostrará registros agregados o empaquetar registros eliminados si estas operaciones son compatibles con el cursor.<br /><br /> Una actualización correcta con **SQLSetPos** cambiará el estado de una fila de SQL_ROW_ADDED a SQL_ROW_SUCCESS (si existe la matriz de estado de fila).<br /><br /> Una actualización correcta con **SQLSetPos** cambiará el estado de una fila de SQL_ROW_UPDATED al nuevo estado de la fila (si existe la matriz de estado de fila).<br /><br /> Si se produce un error en una operación **SQLSetPos** en una fila, el estado de la fila se establece en SQL_ROW_ERROR (si existe la matriz de estado de fila).<br /><br /> Para un cursor abierto con un atributo de instrucción SQL_ATTR_CONCURRENCY de SQL_CONCUR_ROWVER o SQL_CONCUR_VALUES, una actualización con **SQLSetPos** podría actualizar los valores de simultaneidad optimista utilizados por el origen de datos para detectar que la fila ha cambiado. Si esto ocurre, las versiones de fila o los valores utilizados para garantizar que la simultaneidad del cursor se actualizan cada vez que se actualizan los búferes del conjunto de filas desde el servidor. Esto ocurre para cada fila que se actualiza.<br /><br /> El contenido de la matriz de estado de fila a la que apunta el atributo de instrucción SQL_ATTR_ROW_OPERATION_PTR se omite para el SQL_REFRESH *Operation*.|  
|SQL_UPDATE|El controlador coloca el cursor en la fila especificada por *RowNumber* y actualiza la fila subyacente de datos con los valores de los búferes del conjunto de filas (el *argumento TargetValuePtr* en **SQLBindCol**). Recupera las longitudes de los datos de los búferes de longitud/indicador (el argumento *StrLen_or_IndPtr* en **SQLBindCol**). Si la longitud de cualquier columna es SQL_COLUMN_IGNORE, la columna no se actualiza. Después de actualizar la fila, el controlador cambia el elemento correspondiente de la matriz de estado de fila a SQL_ROW_UPDATED o SQL_ROW_SUCCESS_WITH_INFO (si existe la matriz de estado de fila).<br /><br /> Está definido por el controlador cuál es el comportamiento si **SQLSetPos** con un *Operación* argumento de SQL_UPDATE se llama en un cursor que contiene columnas duplicadas. El controlador puede devolver un SQLSTATE definido por el controlador, puede actualizar la primera columna que aparece en el conjunto de resultados o realizar otro comportamiento definido por el controlador.<br /><br /> La matriz de operaciones de fila a la que apunta el atributo de instrucción SQL_ATTR_ROW_OPERATION_PTR se puede utilizar para indicar que se debe omitir una fila del conjunto de filas actual durante una actualización masiva. Para obtener más información, consulte "Status and Operation Arrays" más adelante en esta referencia de función.|  
|SQL_DELETE|El controlador coloca el cursor en la fila especificada por *RowNumber* y elimina la fila subyacente de datos. Cambia el elemento correspondiente de la matriz de estado de fila a SQL_ROW_DELETED. Una vez eliminada la fila, no son válidos para la fila las instrucciones de actualización y eliminación posicionadas, las llamadas a **SQLGetData**y las llamadas a **SQLSetPos** con *Operation* establecida en cualquier cosa excepto SQL_POSITION. Para los controladores que admiten el empaquetado, la fila se elimina del cursor cuando se recuperan nuevos datos del origen de datos.<br /><br /> Si la fila permanece visible depende del tipo de cursor. Por ejemplo, las filas eliminadas son visibles para cursores estáticos y controlados por conjuntos de claves, pero invisibles para los cursores dinámicos.<br /><br /> La matriz de operaciones de fila a la que apunta el atributo de instrucción SQL_ATTR_ROW_OPERATION_PTR se puede utilizar para indicar que se debe omitir una fila del conjunto de filas actual durante una eliminación masiva. Para obtener más información, consulte "Status and Operation Arrays" más adelante en esta referencia de función.|  
  
## <a name="locktype-argument"></a>Argumento LockType  
 El *LockType* argumento proporciona una manera para que las aplicaciones para controlar la simultaneidad. En la mayoría de los casos, los orígenes de datos que admiten transacciones y niveles de simultaneidad solo admitirán el valor SQL_LOCK_NO_CHANGE del argumento *LockType.* El *LockType* argumento se utiliza generalmente solo para la compatibilidad basada en archivos.  
  
 El *argumento LockType* especifica el estado de bloqueo de la fila después de ejecutar **SQLSetPos.** Si el controlador no puede bloquear la fila para realizar la operación solicitada o para satisfacer el argumento *LockType,* devuelve SQL_ERROR y SQLSTATE 42000 (error de sintaxis o infracción de acceso).  
  
 Aunque el *LockType* argumento se especifica para una sola instrucción, el bloqueo concede los mismos privilegios a todas las instrucciones de la conexión. En particular, un bloqueo adquirido por una instrucción en una conexión se puede desbloquear mediante una instrucción diferente en la misma conexión.  
  
 Una fila bloqueada a través de **SQLSetPos** permanece bloqueada hasta que la aplicación llama a **SQLSetPos** para la fila con *LockType* establecido en SQL_LOCK_UNLOCK, o hasta que la aplicación llama **sqlFreeHandle** para la instrucción o **SQLFreeStmt** con la opción SQL_CLOSE. Para un controlador que admite transacciones, una fila bloqueada a través de **SQLSetPos** se desbloquea cuando la aplicación llama a **SQLEndTran** para confirmar o revertir una transacción en la conexión (si se cierra un cursor cuando se confirma o revierte una transacción, como se indica en los tipos de información SQL_CURSOR_COMMIT_BEHAVIOR y SQL_CURSOR_ROLLBACK_BEHAVIOR devueltos por **SQLGetInfo**).  
  
 El *LockType* argumento admite los siguientes tipos de bloqueos. Para determinar qué bloqueos son compatibles con un origen de datos, una aplicación llama a **SQLGetInfo** con el tipo de información SQL_DYNAMIC_CURSOR_ATTRIBUTES1, SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1, SQL_KEYSET_CURSOR_ATTRIBUTES1 o SQL_STATIC_CURSOR_ATTRIBUTES1 (según el tipo del cursor).  
  
|*Argumento LockType*|Tipo de bloqueo|  
|-------------------------|---------------|  
|SQL_LOCK_NO_CHANGE|El controlador o el origen de datos garantiza que la fila está en el mismo estado bloqueado o desbloqueado que antes de **SQLSetPos** se llamó. Este valor de *LockType* permite que los orígenes de datos que no admiten el bloqueo explícito de nivel de fila usen cualquier bloqueo que requieran los niveles de aislamiento de transacciones y simultaneidad actuales.|  
|SQL_LOCK_EXCLUSIVE|El controlador o el origen de datos bloquea la fila exclusivamente. No se puede usar una instrucción en una conexión diferente o en una aplicación diferente para adquirir bloqueos en la fila.|  
|SQL_LOCK_UNLOCK|El controlador o el origen de datos desbloquea la fila.|  
  
 Si un controlador admite SQL_LOCK_EXCLUSIVE pero no admite SQL_LOCK_UNLOCK, una fila que está bloqueada permanecerá bloqueada hasta que se produzca una de las llamadas de función descritas en el párrafo anterior.  
  
 Si un controlador admite SQL_LOCK_EXCLUSIVE pero no admite SQL_LOCK_UNLOCK, una fila que está bloqueada permanecerá bloqueada hasta que la aplicación llame a **SQLFreeHandle** para la instrucción o **SQLFreeStmt** con la opción SQL_CLOSE. Si el controlador admite transacciones y cierra el cursor al confirmar o revertir la transacción, la aplicación llama a **SQLEndTran**.  
  
 Para las operaciones de actualización y eliminación en **SQLSetPos**, la aplicación utiliza el argumento *LockType* de la siguiente manera:  
  
-   Para garantizar que una fila no cambia después de recuperarla, una aplicación llama a **SQLSetPos** con *Operation* establecida en SQL_REFRESH y *LockType* establecido en SQL_LOCK_EXCLUSIVE.  
  
-   Si la aplicación establece *LockType* en SQL_LOCK_NO_CHANGE, el controlador garantiza que una operación de actualización o eliminación se realizará correctamente solo si la aplicación especificada SQL_CONCUR_LOCK para el atributo de instrucción SQL_ATTR_CONCURRENCY.  
  
-   Si la aplicación especifica SQL_CONCUR_ROWVER o SQL_CONCUR_VALUES para el atributo de instrucción SQL_ATTR_CONCURRENCY, el controlador compara las versiones o los valores de fila y rechaza la operación si la fila ha cambiado desde que la aplicación ha capturado la fila.  
  
-   Si la aplicación especifica SQL_CONCUR_READ_ONLY para el atributo de instrucción SQL_ATTR_CONCURRENCY, el controlador rechaza cualquier operación de actualización o eliminación.  
  
 Para obtener más información sobre el atributo de instrucción SQL_ATTR_CONCURRENCY, vea [SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md).  
  
## <a name="status-and-operation-arrays"></a>Matriz de estado y operación  
 Las siguientes matrices de estado y operación se utilizan al llamar a **SQLSetPos:**  
  
-   La matriz de estado de fila (como apunta el campo SQL_DESC_ARRAY_STATUS_PTR del IRD y el atributo de instrucción SQL_ATTR_ROW_STATUS_ARRAY) contiene valores de estado para cada fila de datos del conjunto de filas. El controlador establece los valores de estado de esta matriz después de una llamada a **SQLFetch**, **SQLFetchScroll**, **SQLBulkOperations**o **SQLSetPos**. El atributo de instrucción SQL_ATTR_ROW_STATUS_PTR señala esta matriz.  
  
-   La matriz de operaciones de fila (como apunta el campo SQL_DESC_ARRAY_STATUS_PTR en el atributo ARD y la instrucción SQL_ATTR_ROW_OPERATION_ARRAY) contiene un valor para cada fila del conjunto de filas que indica si se omite o se realiza una llamada a **SQLSetPos** para una operación masiva. Cada elemento de la matriz se establece en SQL_ROW_PROCEED (valor predeterminado) o SQL_ROW_IGNORE. El atributo de instrucción SQL_ATTR_ROW_OPERATION_PTR señala esta matriz.  
  
 El número de elementos de las matrices status y operation debe ser igual al número de filas del conjunto de filas (según lo definido por el atributo de instrucción SQL_ATTR_ROW_ARRAY_SIZE).  
  
 Para obtener información acerca de la matriz de estado de fila, vea [SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md). Para obtener información acerca de la matriz de operaciones de fila, vea "Ignorar una fila en una operación masiva", más adelante en esta sección.  
  
## <a name="using-sqlsetpos"></a>Uso de SQLSetPos  
 Antes de que una aplicación llame a **SQLSetPos**, debe realizar la siguiente secuencia de pasos:  
  
1.  Si la aplicación llamará a **SQLSetPos** con *Operation* establecido en SQL_UPDATE, llame a **SQLBindCol** (o **SQLSetDescRec**) para cada columna para especificar su tipo de datos y enlazar búferes para los datos y la longitud de la columna.  
  
2.  Si la aplicación llamará a **SQLSetPos** con *Operation* establecido en SQL_DELETE o SQL_UPDATE, llame a **SQLColAttribute** para asegurarse de que las columnas que se van a eliminar o actualizar son actualizables.  
  
3.  Llame a **SQLExecDirect**, **SQLExecute**o a una función de catálogo para crear un conjunto de resultados.  
  
4.  Llame a **SQLFetch** o **SQLFetchScroll** para recuperar los datos.  
  
 Para obtener más información sobre el uso de **SQLSetPos**, vea [Actualización de datos con SQLSetPos](../../../odbc/reference/develop-app/updating-data-with-sqlsetpos.md).  
  
## <a name="deleting-data-using-sqlsetpos"></a>Eliminación de datos mediante SQLSetPos  
 Para eliminar datos con **SQLSetPos**, una aplicación llama a **SQLSetPos** con *RowNumber* establecido en el número de la fila que se desea eliminar y *Operation* establecido en SQL_DELETE.  
  
 Una vez eliminados los datos, el controlador cambia el valor de la matriz de estado de la fila de implementación para la fila adecuada a SQL_ROW_DELETED (o SQL_ROW_ERROR).  
  
## <a name="updating-data-using-sqlsetpos"></a>Actualización de datos mediante SQLSetPos  
 Una aplicación puede pasar el valor de una columna en el búfer de datos enlazado o con una o varias llamadas a **SQLPutData**. Las columnas cuyos datos se pasan con **SQLPutData** se conocen como *columnas* *de datos en ejecución.* Estos se utilizan comúnmente para enviar datos para SQL_LONGVARBINARY y SQL_LONGVARCHAR columnas y se pueden mezclar con otras columnas.  
  
#### <a name="to-update-data-with-sqlsetpos-an-application"></a>Para actualizar datos con SQLSetPos, una aplicación:  
  
1.  Coloca valores en los búferes de datos y longitud/indicador enlazados con **SQLBindCol:**  
  
    -   Para las columnas normales, la aplicación coloca el nuevo valor de columna en el * \*TargetValuePtr* búfer y la longitud de ese valor en el * \*búfer de StrLen_or_IndPtr.* Si no se debe actualizar la fila, la aplicación coloca SQL_ROW_IGNORE en el elemento de esa fila de la matriz de operaciones de fila.  
  
    -   Para las columnas de datos en ejecución, la aplicación coloca un valor definido por la aplicación, como el número de columna, en el * \*búfer TargetValuePtr.* El valor se puede utilizar más adelante para identificar la columna.  
  
         La aplicación coloca el resultado de la macro SQL_LEN_DATA_AT_EXEC(*length*) en el búfer de*StrLen_or_IndPtr* *. Si el tipo de datos SQL de la columna es SQL_LONGVARBINARY, SQL_LONGVARCHAR o un tipo de datos específico del origen de datos largo y el controlador devuelve "Y" para el tipo de información SQL_NEED_LONG_DATA_LEN en **SQLGetInfo**, *longitud* es el número de bytes de datos que se enviarán para el parámetro; de lo contrario, debe ser un valor no negativo y se ignora.  
  
2.  Llama a **SQLSetPos** con el *operación* argumento establecido en SQL_UPDATE para actualizar la fila de datos.  
  
    -   Si no hay columnas de datos en ejecución, el proceso se ha completado.  
  
    -   Si hay columnas de datos en ejecución, la función devuelve SQL_NEED_DATA y continúa con el paso 3.  
  
3.  Llama a **SQLParamData** para recuperar la dirección del * \*búfer TargetValuePtr* para la primera columna de datos en ejecución que se va a procesar. **SQLParamData** devuelve SQL_NEED_DATA. La aplicación recupera el valor definido por la aplicación del * \*búfer TargetValuePtr.*  
  
    > [!NOTE]  
    >  Aunque los parámetros de datos en ejecución son similares a las columnas de datos en ejecución, el valor devuelto por **SQLParamData** es diferente para cada uno.  
  
    > [!NOTE]  
    >  Los parámetros de datos en ejecución son parámetros de una instrucción SQL para la que se enviarán datos con **SQLPutData** cuando la instrucción se ejecute con **SQLExecDirect** o **SQLExecute**. Están enlazados con **SQLBindParameter** o estableciendo descriptores con **SQLSetDescRec**. El valor devuelto por **SQLParamData** es un valor de 32 bits pasado a **SQLBindParameter** en el *ParameterValuePtr* argumento.  
  
    > [!NOTE]  
    >  Las columnas de datos en ejecución son columnas de un conjunto de filas para el que se enviarán datos con **SQLPutData** cuando se actualice una fila con **SQLSetPos**. Están enlazados con **SQLBindCol**. El valor devuelto por **SQLParamData** es la dirección de la fila en el **TargetValuePtr* búfer que se está procesando.  
  
4.  Llama a **SQLPutData** una o varias veces para enviar datos para la columna. Se necesita más de una llamada si no * \** se pueden devolver todos los valores de datos en el búfer TargetValuePtr especificado en **SQLPutData**; Solo se permiten varias llamadas a **SQLPutData** para la misma columna al enviar datos de caracteres C a una columna con un tipo de datos específico de carácter, binario o origen de datos o al enviar datos c binarios a una columna con un tipo de datos de carácter, binario o específico del origen de datos.  
  
5.  Llama a **SQLParamData** de nuevo para indicar que se han enviado todos los datos para la columna.  
  
    -   Si hay más columnas de datos en ejecución, **SQLParamData** devuelve SQL_NEED_DATA y la dirección del búfer *TargetValuePtr* para la siguiente columna de datos en ejecución que se va a procesar. La aplicación repite los pasos 4 y 5.  
  
    -   Si no hay más columnas de datos en ejecución, el proceso se ha completado. Si la instrucción se ejecutó correctamente, **SQLParamData** devuelve SQL_SUCCESS o SQL_SUCCESS_WITH_INFO; si se produce un error en la ejecución, devuelve SQL_ERROR. En este momento, **SQLParamData** puede devolver cualquier SQLSTATE que **SQLSetPos**pueda devolver .  
  
 Si se han actualizado los datos, el controlador cambia el valor de la matriz de estado de la fila de implementación para la fila adecuada para SQL_ROW_UPDATED.  
  
 Si se cancela la operación o se produce un error en **SQLParamData** o **SQLPutData**, después de **sqlSetPos** devuelve SQL_NEED_DATA y antes de que se envíen datos para todas las columnas de datos en ejecución, la aplicación solo puede llamar a **SQLCancel**, **SQLGetDiagField**, **SQLGetDiagRec**, **SQLGetFunctions**, **SQLParamData**o **SQLPutData** para la instrucción o la conexión asociada a la instrucción. Si llama a cualquier otra función para la instrucción o la conexión asociada a la instrucción, la función devuelve SQL_ERROR y SQLSTATE HY010 (error de secuencia de funciones).  
  
 Si la aplicación llama a **SQLCancel** mientras el controlador todavía necesita datos para las columnas de datos en ejecución, el controlador cancela la operación. A continuación, la aplicación puede llamar a **SQLSetPos** de nuevo; la cancelación no afecta al estado del cursor ni a la posición actual del cursor.  
  
 Cuando la lista SELECT de la especificación de consulta asociada al cursor contiene más de una referencia a la misma columna, si se genera un error o el controlador omite las referencias duplicadas y realiza las operaciones solicitadas está definido por el controlador.  
  
## <a name="performing-bulk-operations"></a>Realización de operaciones a granel  
 Si el *RowNumber* argumento es 0, el controlador realiza la operación especificada en el *Operación* argumento para cada fila en el conjunto de filas que tiene un valor de SQL_ROW_PROCEED en su campo en la matriz de operaciones de fila señalada por SQL_ATTR_ROW_OPERATION_PTR atributo de instrucción. Se trata de un valor válido del argumento *RowNumber* para un argumento *Operation* de SQL_DELETE, SQL_REFRESH o SQL_UPDATE, pero no SQL_POSITION. **SQLSetPos** con una *operación* de SQL_POSITION y un *RowNumber* igual a 0 devolverá SQLSTATE HY109 (posición de cursor no válida).  
  
 Si se produce un error que pertenece a todo el conjunto de filas, como SQLSTATE HYT00 (tiempo de espera caducado), el controlador devuelve SQL_ERROR y el SQLSTATE adecuado. El contenido de los búferes del conjunto de filas no está definido y la posición del cursor no cambia.  
  
 Si se produce un error que pertenece a una sola fila, el controlador:  
  
-   Establece el elemento de la fila de la matriz de estado de fila a la que apunta el atributo de instrucción SQL_ATTR_ROW_STATUS_PTR en SQL_ROW_ERROR.  
  
-   Registra uno o más SQLSTATEs adicionales para el error en la cola de errores y establece el campo SQL_DIAG_ROW_NUMBER en la estructura de datos de diagnóstico.  
  
 Después de procesar el error o la advertencia, si el controlador completa la operación para las filas restantes del conjunto de filas, devuelve SQL_SUCCESS_WITH_INFO. Por lo tanto, para cada fila que devuelve un error, la cola de errores contiene cero o más SQLSTATEs adicionales. Si el controlador detiene la operación después de que haya procesado el error o la advertencia, devuelve SQL_ERROR.  
  
 Si el controlador devuelve advertencias, como SQLSTATE 01004 (datos truncados), devuelve advertencias que se aplican a todo el conjunto de filas o a filas desconocidas del conjunto de filas antes de devolver la información de error que se aplica a filas específicas. Devuelve advertencias para filas específicas junto con cualquier otra información de error sobre esas filas.  
  
 Si *RowNumber* es igual a 0 y *Operation* es SQL_UPDATE, SQL_REFRESH o SQL_DELETE, el número de filas en las que **SQLSetPos** opera apunta al atributo de instrucción SQL_ATTR_ROWS_FETCHED_PTR.  
  
 Si *RowNumber* es igual a 0 y *Operation* es SQL_DELETE, SQL_REFRESH o SQL_UPDATE, la fila actual después de la operación es la misma que la fila actual antes de la operación.  
  
## <a name="ignoring-a-row-in-a-bulk-operation"></a>Ignorar una fila en una operación a granel  
 La matriz de operaciones de fila se puede utilizar para indicar que se debe omitir una fila del conjunto de filas actual durante una operación masiva mediante **SQLSetPos**. Para hacer que el controlador ignore una o más filas durante una operación masiva, una aplicación debe realizar los pasos siguientes:  
  
1.  Llame a **SQLSetStmtAttr** para establecer el atributo de instrucción SQL_ATTR_ROW_OPERATION_PTR para que apunte a una matriz de SQLUSMALLINTs. Este campo también se puede establecer llamando a **SQLSetDescField** para establecer el SQL_DESC_ARRAY_STATUS_PTR campo de encabezado de la ARD, que requiere que una aplicación obtenga el identificador de descriptor.  
  
2.  Establezca cada elemento de la matriz de operaciones de fila en uno de los dos valores:  
  
    -   SQL_ROW_IGNORE, para indicar que la fila se excluye para la operación masiva.  
  
    -   SQL_ROW_PROCEED, para indicar que la fila se incluye en la operación masiva. Este es el valor predeterminado.  
  
3.  Llame a **SQLSetPos** para realizar la operación masiva.  
  
 Las siguientes reglas se aplican a la matriz de operaciones de fila:  
  
-   SQL_ROW_IGNORE y SQL_ROW_PROCEED solo afectan a las operaciones masivas mediante **SQLSetPos** con una *operación* de SQL_DELETE o SQL_UPDATE. No afectan a las llamadas a **SQLSetPos** con una *operación* de SQL_REFRESH o SQL_POSITION.  
  
-   El puntero se establece en null de forma predeterminada.  
  
-   Si el puntero es null, todas las filas se actualizan como si todos los elementos estuvieran establecidos en SQL_ROW_PROCEED.  
  
-   Establecer un elemento en SQL_ROW_PROCEED no garantiza que la operación se producirá en esa fila concreta. Por ejemplo, si una fila determinada del conjunto de filas tiene el estado SQL_ROW_ERROR, es posible que el controlador no pueda actualizar esa fila independientemente de si la aplicación especificó SQL_ROW_PROCEED. Una aplicación siempre debe comprobar la matriz de estado de fila para ver si la operación se realizó correctamente.  
  
-   SQL_ROW_PROCEED se define como 0 en el archivo de encabezado. Una aplicación puede inicializar la matriz de operaciones de fila en 0 para procesar todas las filas.  
  
-   Si el número de elemento "n" en la matriz de operaciones de fila se establece en SQL_ROW_IGNORE y **SQLSetPos** se llama para realizar una operación de actualización o eliminación masiva, la enésima fila del conjunto de filas permanece sin cambios después de la llamada a **SQLSetPos**.  
  
-   Una aplicación debe establecer automáticamente una columna de solo lectura en SQL_ROW_IGNORE.  
  
## <a name="ignoring-a-column-in-a-bulk-operation"></a>Ignorar una columna en una operación masiva  
 Para evitar diagnósticos de procesamiento innecesarios generados por intentos de actualizaciones en una o más columnas de solo lectura, una aplicación puede establecer el valor del búfer de longitud/indicador enlazado en SQL_COLUMN_IGNORE. Para obtener más información, vea [SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md).  
  
## <a name="code-example"></a>Ejemplo de código  
 En el ejemplo siguiente, una aplicación permite a un usuario examinar la tabla ORDERS y actualizar el estado del pedido. El cursor está controlado por conjuntos de claves con un tamaño de conjunto de filas de 20 y usa un control de simultaneidad optimista que compara las versiones de fila. Después de capturar cada conjunto de filas, la aplicación lo imprime y permite al usuario seleccionar y actualizar el estado de un pedido. La aplicación utiliza **SQLSetPos** para colocar el cursor en la fila seleccionada y realiza una actualización posicionada de la fila. (Se omite el control de errores para mayor claridad.)  
  
```cpp  
#define ROWS 20  
#define STATUS_LEN 6  
  
SQLCHAR        szStatus[ROWS][STATUS_LEN], szReply[3];  
SQLINTEGER     cbStatus[ROWS], cbOrderID;  
SQLUSMALLINT   rgfRowStatus[ROWS];  
SQLUINTEGER    sOrderID, crow = ROWS, irow;  
SQLHSTMT       hstmtS, hstmtU;  
  
SQLSetStmtAttr(hstmtS, SQL_ATTR_CONCURRENCY, (SQLPOINTER) SQL_CONCUR_ROWVER, 0);  
SQLSetStmtAttr(hstmtS, SQL_ATTR_CURSOR_TYPE, (SQLPOINTER) SQL_CURSOR_KEYSET_DRIVEN, 0);  
SQLSetStmtAttr(hstmtS, SQL_ATTR_ROW_ARRAY_SIZE, (SQLPOINTER) ROWS, 0);  
SQLSetStmtAttr(hstmtS, SQL_ATTR_ROW_STATUS_PTR, (SQLPOINTER) rgfRowStatus, 0);  
SQLSetCursorName(hstmtS, "C1", SQL_NTS);  
SQLExecDirect(hstmtS, "SELECT ORDERID, STATUS FROM ORDERS ", SQL_NTS);  
  
SQLBindCol(hstmtS, 1, SQL_C_ULONG, &sOrderID, 0, &cbOrderID);  
SQLBindCol(hstmtS, 2, SQL_C_CHAR, szStatus, STATUS_LEN, &cbStatus);  
  
while ((retcode == SQLFetchScroll(hstmtS, SQL_FETCH_NEXT, 0)) != SQL_ERROR) {  
   if (retcode == SQL_NO_DATA_FOUND)  
      break;  
   for (irow = 0; irow < crow; irow++) {  
      if (rgfRowStatus[irow] != SQL_ROW_DELETED)  
         printf("%2d %5d %*s\n", irow+1, sOrderID, NAME_LEN-1, szStatus[irow]);  
   }  
   while (TRUE) {  
      printf("\nRow number to update?");  
      gets_s(szReply, 3);  
      irow = atoi(szReply);  
      if (irow > 0 && irow <= crow) {  
         printf("\nNew status?");  
         gets_s(szStatus[irow-1], (ROWS * STATUS_LEN));  
         SQLSetPos(hstmtS, irow, SQL_POSITION, SQL_LOCK_NO_CHANGE);  
         SQLPrepare(hstmtU,  
          "UPDATE ORDERS SET STATUS=? WHERE CURRENT OF C1", SQL_NTS);  
         SQLBindParameter(hstmtU, 1, SQL_PARAM_INPUT,  
            SQL_C_CHAR, SQL_CHAR,  
            STATUS_LEN, 0, szStatus[irow], 0, NULL);  
         SQLExecute(hstmtU);  
      } else if (irow == 0) {  
         break;  
      }  
   }  
}  
```  
  
 Para obtener más ejemplos, vea [Instrucciones de actualización y eliminación posicionadas](../../../odbc/reference/develop-app/positioned-update-and-delete-statements.md) y Actualización de filas en el conjunto de filas con [SQLSetPos](../../../odbc/reference/develop-app/updating-rows-in-the-rowset-with-sqlsetpos.md).  
  
## <a name="related-functions"></a>Funciones relacionadas  
  
|Para información acerca de|Vea|  
|---------------------------|---------|  
|Enlazar un búfer a una columna en un conjunto de resultados|[SQLBindCol (función)](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Realizar operaciones masivas que no se relacionan con la posición del cursor de bloque|[Función SQLBulkOperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md)|  
|Cancelación del procesamiento de extractos|[Función SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Obtención de un bloque de datos o desplazamiento por un conjunto de resultados|[Función SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|Obtener un único campo de un descriptor|[Función SQLGetDescField](../../../odbc/reference/syntax/sqlgetdescfield-function.md)|  
|Obtención de varios campos de un descriptor|[Función SQLGetDescRec](../../../odbc/reference/syntax/sqlgetdescrec-function.md)|  
|Establecer un único campo de un descriptor|[Función SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)|  
|Establecer varios campos de un descriptor|[Función SQLSetDescRec](../../../odbc/reference/syntax/sqlsetdescrec-function.md)|  
|Establecer un atributo de instrucción|[Función SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de la API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Archivos de encabezado de ODBC](../../../odbc/reference/install/odbc-header-files.md)
