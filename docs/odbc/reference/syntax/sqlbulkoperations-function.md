---
title: Función SQLBulkOperations (SQLBulkOperations) Microsoft Docs
ms.custom: ''
ms.date: 07/18/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLBulkOperations
apilocation:
- sqlsrv32.dll
- odbc32.dll
apitype: dllExport
f1_keywords:
- SQLBulkOperations
helpviewer_keywords:
- SQLBulkOperations function [ODBC]
ms.assetid: 7029d0da-b0f2-44e6-9114-50bd96f47196
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 61f4f294a6d84856bc3065b599a370bb5658e3ca
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301335"
---
# <a name="sqlbulkoperations-function"></a>Función SQLBulkOperations
**Conformidad**  
 Versión introducida: Cumplimiento de estándares ODBC 3.0: ODBC  
  
 **Resumen**  
 **SQLBulkOperations** realiza inserciones masivas y operaciones de marcadores masivos, incluidas la actualización, eliminación y obtención por marcador.  
  
## <a name="syntax"></a>Sintaxis  
  
```cpp  
  
SQLRETURN SQLBulkOperations(  
     SQLHSTMT       StatementHandle,  
     SQLUSMALLINT   Operation);  
```  
  
## <a name="arguments"></a>Argumentos  
 *StatementHandle*  
 [Entrada] Identificador de instrucción.  
  
 *Operación*  
 [Entrada] Operación para realizar:  
  
 SQL_ADD SQL_UPDATE_BY_BOOKMARK SQL_DELETE_BY_BOOKMARK SQL_FETCH_BY_BOOKMARK  
  
 Para obtener más información, consulte "Comentarios."  
  
## <a name="returns"></a>Devuelve  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NEED_DATA, SQL_STILL_EXECUTING, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnóstico  
 Cuando **SQLBulkOperations** devuelve SQL_ERROR o SQL_SUCCESS_WITH_INFO, se puede obtener un valor SQLSTATE asociado llamando a **SQLGetDiagRec** con un *HandleType* de SQL_HANDLE_STMT y un *control* de *StatementHandle*. En la tabla siguiente se enumeran los valores SQLSTATE normalmente devueltos por **SQLBulkOperations** y se explica cada uno de ellos en el contexto de esta función; la notación "(DM)" precede a las descripciones de SQLSTATEs devueltas por el Administrador de controladores. El código de retorno asociado a cada valor SQLSTATE se SQL_ERROR, a menos que se indique lo contrario.  
  
 Para todos aquellos SQLSTATEs que pueden devolver SQL_SUCCESS_WITH_INFO o SQL_ERROR (excepto 01xxx SQLSTATEs), se devuelve SQL_SUCCESS_WITH_INFO si se produce un error en una o más filas, pero no en todas, de una operación de varias filas y SQL_ERROR se devuelve si se produce un error en una operación de una sola fila.  
  
|SQLSTATE|Error|Descripción|  
|--------------|-----------|-----------------|  
|01000|Advertencia general|Mensaje informativo específico del controlador. (La función devuelve SQL_SUCCESS_WITH_INFO.)|  
|01004|Truncamiento de la derecha de datos de cadena|El *Operación* argumento era SQL_FETCH_BY_BOOKMARK y datos de cadena o binarios devueltos para una columna o columnas con un tipo de datos de SQL_C_CHAR o SQL_C_BINARY dio lugar al truncamiento de caracteres no en blanco o datos binarios no NULL.|  
|01S01|Error en la fila|El *operación* argumento se SQL_ADD y se produjo un error en una o más filas al realizar la operación, pero al menos una fila se agregó correctamente. (La función devuelve SQL_SUCCESS_WITH_INFO.)<br /><br /> (Este error solo se produce cuando una aplicación está trabajando con un ODBC 2. *x* controlador.)|  
|01S07|Truncamiento fraccionario|El *operación* argumento era SQL_FETCH_BY_BOOKMARK, el tipo de datos del búfer de aplicación no era SQL_C_CHAR o SQL_C_BINARY y los datos devueltos a los búferes de aplicación para una o más columnas se truncaron. (Para los tipos de datos numéricos C, la parte fraccionaria del número se truncó. Para los tipos de datos time, timestamp e interval C que contienen un componente time, la parte fraccionaria del tiempo se truncó.)<br /><br /> (La función devuelve SQL_SUCCESS_WITH_INFO.)|  
|07006|Infracción de atributo de tipo de datos restringido|El *Operación* argumento se SQL_FETCH_BY_BOOKMARK y el valor de datos de una columna en el conjunto de resultados no se pudo convertir al tipo de datos especificado por el *TargetType* argumento en la llamada a **SQLBindCol**.<br /><br /> El *operación* argumento era SQL_UPDATE_BY_BOOKMARK o SQL_ADD y el valor de datos en los búferes de aplicación no se pudo convertir al tipo de datos de una columna en el conjunto de resultados.|  
|07009|Indice de descriptor no válido|El argumento *Operation* se SQL_ADD y una columna se enlazacon con un número de columna mayor que el número de columnas del conjunto de resultados.|  
|21S02|El grado de la tabla derivada no coincide con la lista de columnas|El argumento *Operación* fue SQL_UPDATE_BY_BOOKMARK; y ninguna columna era actualizable porque todas las columnas estaban sin enlazar o de solo lectura, o el valor del búfer de longitud/indicador enlazado estaba SQL_COLUMN_IGNORE.|  
|22001|Truncamiento de la derecha de datos de cadena|La asignación de un carácter o valor binario a una columna del conjunto de resultados dio lugar al truncamiento de caracteres o bytes no en blanco (para caracteres) o no nulos (para caracteres binarios).|  
|22003|Valor numérico fuera del rango|El *operación* argumento era SQL_ADD o SQL_UPDATE_BY_BOOKMARK y la asignación de un valor numérico a una columna en el conjunto de resultados hizo que se truncar la parte completa (en lugar de fraccionaria) del número.<br /><br /> El argumento *Operation* se SQL_FETCH_BY_BOOKMARK y devolver el valor numérico de una o más columnas enlazadas habría causado una pérdida de dígitos significativos.|  
|22007|Formato de fecha y hora no válido|El *operación* argumento se SQL_ADD o SQL_UPDATE_BY_BOOKMARK y la asignación de un valor de fecha o marca de tiempo a una columna en el conjunto de resultados hizo que el año, mes o día campo a estar fuera del intervalo.<br /><br /> El argumento *Operation* se SQL_FETCH_BY_BOOKMARK y devolver el valor de fecha o marca de tiempo para una o más columnas enlazadas habría provocado que el campo de año, mes o día estuviera fuera del intervalo.|  
|22008|Desbordamiento del campo de fecha y hora|El argumento *Operation* se SQL_ADD o SQL_UPDATE_BY_BOOKMARK, y el rendimiento de la aritmética de fecha y hora en los datos que se envían a una columna del conjunto de resultados dio como resultado un campo datetime (el campo year, month, day, hour, minute o second) del resultado que quedando fuera del rango permitido de valores para el campo o siendo inválidos en función de las reglas naturales del calendario gregoriano para datetimes.<br /><br /> El argumento *Operation* se SQL_FETCH_BY_BOOKMARK, y el rendimiento de la aritmética datetime en los datos que se recuperan del conjunto de resultados dio como resultado un campo datetime (el campo year, month, day, hour, minute o second) del resultado que quedó fuera del intervalo permitido de valores para el campo o no es válido en función de las reglas naturales del calendario gregoriano para datetimes.|  
|22015|Desbordamiento de campo de intervalo|El *operación* argumento se SQL_ADD o SQL_UPDATE_BY_BOOKMARK y la asignación de un tipo numérico exacto o de intervalo C a un intervalo de tipo de datos SQL causó una pérdida de dígitos significativos.<br /><br /> El *argumento Operation* era SQL_ADD o SQL_UPDATE_BY_BOOKMARK; al asignar a un tipo SQL de intervalo, no había ninguna representación del valor del tipo C en el tipo SQL de intervalo.<br /><br /> El *operación* argumento se SQL_FETCH_BY_BOOKMARK, y la asignación de un tipo SQL numérico o de intervalo exacto a un tipo de intervalo C causó una pérdida de dígitos significativos en el campo inicial.<br /><br /> El argumento *Operation* fue SQL_FETCH_BY_BOOKMARK; al asignar a un tipo de intervalo C, no había ninguna representación del valor del tipo SQL en el tipo de intervalo C.|  
|22018|Valor de carácter no válido para la especificación de conversión|El argumento *Operation* fue SQL_FETCH_BY_BOOKMARK; el tipo C era un número exacto o aproximado, una fecha y hora o un tipo de datos de intervalo; el tipo SQL de la columna era un tipo de datos de carácter; y el valor de la columna no era un literal válido del tipo C enlazado.<br /><br /> El argumento *Operación* era SQL_ADD o SQL_UPDATE_BY_BOOKMARK; el tipo SQL era un número exacto o aproximado, una fecha y hora o un tipo de datos de intervalo; el tipo C se SQL_C_CHAR; y el valor de la columna no era un literal válido del tipo SQL enlazado.|  
|23000|Violación de la restricción de integridad|El argumento *Operation* era SQL_ADD, SQL_DELETE_BY_BOOKMARK o SQL_UPDATE_BY_BOOKMARK, y se infringió una restricción de integridad.<br /><br /> El *Operación* argumento se SQL_ADD y una columna que no estaba enlazada se define como NOT NULL y no tiene ningún valor predeterminado.<br /><br /> El *Operación* argumento era SQL_ADD, la longitud especificada en el búfer *de StrLen_or_IndPtr* enlazado era SQL_COLUMN_IGNORE y la columna no tenía un valor predeterminado.|  
|24000|Estado de cursor no válido|El *StatementHandle* estaba en un estado ejecutado, pero no se asoció ningún conjunto de resultados con *StatementHandle*.|  
|40001|Error de serialización|La transacción se revirtió debido a un interbloqueo de recursos con otra transacción.|  
|40003|Finalización de la declaración desconocida|Error en la conexión asociada durante la ejecución de esta función y no se puede determinar el estado de la transacción.|  
|42000|Error de sintaxis o violación de acceso|El controlador no pudo bloquear la fila según sea necesario para realizar la operación solicitada en el *operación* argumento.|  
|44000|Infracción de WITH CHECK OPTION|El *operación* argumento se SQL_ADD o SQL_UPDATE_BY_BOOKMARK y la inserción o actualización se realizó en una tabla vista (o una tabla derivada de la tabla vista) que se creó especificando **WITH CHECK OPTION**, de forma que una o varias filas afectadas por la inserción o actualización ya no estarán presentes en la tabla vista.|  
|HY000|Error general|Se ha producido un error para el que no se ha definido sqlSTATE específico y para el que no se ha definido sqlSTATE específico de la implementación. El mensaje de error devuelto por **SQLGetDiagRec** en el * \*messageText* búfer describe el error y su causa.|  
|HY001|Error de asignación de memoria|El controlador no pudo asignar la memoria necesaria para admitir la ejecución o finalización de la función.|  
|HY008|Operación cancelada|El procesamiento asincrónico se ha habilitado para *StatementHandle*. Se llamó a la función y antes de completar la ejecución, **SQLCancel** o **SQLCancelHandle** se llamó en el *StatementHandle*. A continuación, se volvió a llamar a la función en *StatementHandle*.<br /><br /> Se llamó a la función y antes de completar la ejecución, **SQLCancel** o **SQLCancelHandle** se llamó en el *StatementHandle* desde un subproceso diferente en una aplicación multiproceso.|  
|HY010|Error de secuencia de funciones|(DM) se llamó a una función de ejecución asincrónica para el identificador de conexión asociado a *StatementHandle*. Esta función asincrónica todavía se estaba ejecutando cuando se llamó a la función **SQLBulkOperations.**<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**o **SQLMoreResults** se llamó para el *StatementHandle* y devuelto SQL_PARAM_DATA_AVAILABLE. Se llamó a esta función antes de recuperar los datos para todos los parámetros transmitidos.<br /><br /> (DM) el *StatementHandle* especificado no estaba en un estado ejecutado. Se llamó a la función sin llamar primero a **SQLExecDirect**, **SQLExecute**o una función de catálogo.<br /><br /> (DM) se llamó a una función de ejecución asincrónica (no esta) para el *StatementHandle* y todavía se estaba ejecutando cuando se llamó a esta función.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**o **SQLSetPos** se llamó para el *StatementHandle* y devuelto SQL_NEED_DATA. Se llamó a esta función antes de que se enviaran datos para todos los parámetros o columnas de datos en ejecución.<br /><br /> (DM) El controlador era un ODBC 2. *x* controlador y **SQLBulkOperations** se llamó para un *StatementHandle* antes **de SQLFetchScroll** o **SQLFetch** se llamó.<br /><br /> (DM) **SQLBulkOperations** se llamó después de **SQLExtendedFetch** se llamó en el *StatementHandle*.|  
|HY011|Atributo no se puede establecer ahora|(DM) El controlador era un ODBC 2. *x* driver y el atributo de instrucción SQL_ATTR_ROW_STATUS_PTR se estableció entre llamadas a **SQLFetch** o **SQLFetchScroll** y **SQLBulkOperations**.|  
|HY013|Error de administración de memoria|No se pudo procesar la llamada de función porque no se pudo tener acceso a los objetos de memoria subyacentes, posiblemente debido a condiciones de poca memoria.|  
|HY090|Cadena no válida o longitud de búfer|El *argumento Operation* era SQL_ADD o SQL_UPDATE_BY_BOOKMARK; un valor de datos no era un puntero nulo; el tipo de datos C era SQL_C_BINARY o SQL_C_CHAR; y el valor de longitud de columna era menor que 0, pero no igual a SQL_DATA_AT_EXEC, SQL_COLUMN_IGNORE, SQL_NTS o SQL_NULL_DATA, o menor o igual que SQL_LEN_DATA_AT_EXEC_OFFSET.<br /><br /> El valor de un búfer de longitud/indicador se SQL_DATA_AT_EXEC; el tipo SQL era SQL_LONGVARCHAR, SQL_LONGVARBINARY o un tipo de datos específico del origen de datos largo; y el tipo de información SQL_NEED_LONG_DATA_LEN en **SQLGetInfo** era "Y".<br /><br /> El *Operación* argumento se SQL_ADD, el atributo de instrucción SQL_ATTR_USE_BOOKMARK se estableció en SQL_UB_VARIABLE y la columna 0 se enlazaa a un búfer cuya longitud no era igual a la longitud máxima para el marcador para este conjunto de resultados. (Esta longitud está disponible en el campo SQL_DESC_OCTET_LENGTH del IRD y se puede obtener llamando a **SQLDescribeCol**, **SQLColAttribute**o **SQLGetDescField**.)|  
|HY092|Identificador de atributo no válido|(DM) el valor especificado para el *operación* argumento no era válido.<br /><br /> El *operación* argumento era SQL_ADD, SQL_UPDATE_BY_BOOKMARK o SQL_DELETE_BY_BOOKMARK y el atributo de instrucción SQL_ATTR_CONCURRENCY se estableció en SQL_CONCUR_READ_ONLY.<br /><br /> El *operación* argumento se SQL_DELETE_BY_BOOKMARK, SQL_FETCH_BY_BOOKMARK o SQL_UPDATE_BY_BOOKMARK y la columna de marcador no estaba enlazada o el atributo de instrucción SQL_ATTR_USE_BOOKMARKS se estableció en SQL_UB_OFF.|  
|HY117|La conexión se suspende debido al estado de transacción desconocido. Solo se permiten funciones de desconexión y de solo lectura.|(DM) Para obtener más información sobre el estado suspendido, vea [SqlEndTran (función).](../../../odbc/reference/syntax/sqlendtran-function.md)|  
|HYC00|Característica opcional no implementada|El controlador o el origen de datos no admite la operación solicitada en el *operación* argumento.|  
|HYT00|Tiempo de espera agotado|El período de tiempo de espera de la consulta expiró antes de que el origen de datos devolviera el conjunto de resultados. El período de tiempo de espera se establece a través de **SQLSetStmtAttr** con un *atributo* argumento de SQL_ATTR_QUERY_TIMEOUT.|  
|HYT01|Tiempo de espera de conexión expirado|El período de tiempo de espera de conexión expiró antes de que el origen de datos respondiera a la solicitud. El período de tiempo de espera de conexión se establece a través de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|El controlador no admite esta función|(DM) El controlador asociado con el *StatementHandle* no admite la función.|  
|IM017|El sondeo está deshabilitado en el modo de notificación asincrónica|Siempre que se utiliza el modelo de notificación, el sondeo está deshabilitado.|  
|IM018|**SQLCompleteAsync** no se ha llamado para completar la operación asincrónica anterior en este identificador.|Si la llamada de función anterior en el identificador devuelve SQL_STILL_EXECUTING y si el modo de notificación está habilitado, **sqlCompleteAsync** debe llamarse en el identificador para realizar el procesamiento posterior y completar la operación.|  
  
## <a name="comments"></a>Comentarios  
  
> [!CAUTION]  
>  Para obtener información acerca de qué estados de instrucción **SQLBulkOperations** se puede llamar y lo que debe hacer para la compatibilidad con ODBC 2. *x* aplicaciones, consulte la sección Cursores de [bloque, cursores desplazables y compatibilidad con](../../../odbc/reference/appendixes/block-cursors-scrollable-cursors-and-backward-compatibility.md) versiones anteriores en el Apéndice G: Directrices del controlador para la compatibilidad con versiones anteriores.  
  
 Una aplicación utiliza **SQLBulkOperations** para realizar las siguientes operaciones en la tabla o vista base que corresponde a la consulta actual:  
  
-   Agregue nuevas filas.  
  
-   Actualice un conjunto de filas donde cada fila se identifica mediante un marcador.  
  
-   Elimine un conjunto de filas donde cada fila se identifica mediante un marcador.  
  
-   Obtenga un conjunto de filas donde cada fila se identifica mediante un marcador.  
  
 Después de una llamada a **SQLBulkOperations**, la posición del cursor de bloque es indefinida. La aplicación tiene que llamar a **SQLFetchScroll** para establecer la posición del cursor. Una aplicación debe llamar a **SQLFetchScroll** solo con un *FetchOrientation* argumento de SQL_FETCH_FIRST, SQL_FETCH_LAST, SQL_FETCH_ABSOLUTE o SQL_FETCH_BOOKMARK. La posición del cursor no está definida si la aplicación llama a **SQLFetch** o **SQLFetchScroll** con un *FetchOrientation* argumento de SQL_FETCH_PRIOR, SQL_FETCH_NEXT o SQL_FETCH_RELATIVE.  
  
 Una columna se puede omitir en las operaciones masivas realizadas por una llamada a **SQLBulkOperations** estableciendo la longitud de columna/búfer de indicador especificado en la llamada a **SQLBindCol**, en SQL_COLUMN_IGNORE.  
  
 No es necesario que la aplicación establezca el atributo de instrucción SQL_ATTR_ROW_OPERATION_PTR cuando llama a **SQLBulkOperations** porque las filas no se pueden omitir al realizar operaciones masivas con esta función.  
  
 El búfer al que apunta el atributo de instrucción SQL_ATTR_ROWS_FETCHED_PTR contiene el número de filas afectadas por una llamada a **SQLBulkOperations**.  
  
 Cuando el *Operación* argumento es SQL_ADD o SQL_UPDATE_BY_BOOKMARK y la lista de selección de la especificación de consulta asociada con el cursor contiene más de una referencia a la misma columna, se define por controlador si se genera un error o el controlador omite las referencias duplicadas y realiza las operaciones solicitadas.  
  
 Para obtener más información acerca de cómo utilizar **SQLBulkOperations**, vea [Actualización de datos con SQLBulkOperations](../../../odbc/reference/develop-app/updating-data-with-sqlbulkoperations.md).  
  
## <a name="performing-bulk-inserts"></a>Realización de inserciones masivas  
 Para insertar datos con **SQLBulkOperations**, una aplicación realiza la siguiente secuencia de pasos:  
  
1.  Ejecuta una consulta que devuelve un conjunto de resultados.  
  
2.  Establece el atributo de instrucción SQL_ATTR_ROW_ARRAY_SIZE en el número de filas que desea insertar.  
  
3.  Llama a **SQLBindCol** para enlazar los datos que desea insertar. Los datos se enlazan a una matriz con un tamaño igual al valor de SQL_ATTR_ROW_ARRAY_SIZE.  
  
    > [!NOTE]  
    >  El tamaño de la matriz señalada por el atributo de instrucción SQL_ATTR_ROW_STATUS_PTR debe ser igual a SQL_ATTR_ROW_ARRAY_SIZE o SQL_ATTR_ROW_STATUS_PTR debe ser un puntero nulo.  
  
4.  Llama a **SQLBulkOperations**(*StatementHandle,* SQL_ADD) para realizar la inserción.  
  
5.  Si la aplicación ha establecido el atributo de instrucción SQL_ATTR_ROW_STATUS_PTR, puede inspeccionar esta matriz para ver el resultado de la operación.  
  
 Si una aplicación enlaza la columna 0 antes de llamar a **SQLBulkOperations** con un *operación* argumento de SQL_ADD, el controlador actualizará los búferes de columna 0 enlazados con los valores de marcador para la fila recién insertada. Para que esto ocurra, la aplicación debe haber establecido el atributo de instrucción SQL_ATTR_USE_BOOKMARKS en SQL_UB_VARIABLE antes de ejecutar la instrucción. (Esto no funciona con un ODBC 2. *x* controlador.)  
  
 SQLBulkOperations puede agregar datos largos en partes mediante llamadas a SQLParamData y SQLPutData. Para obtener más información, consulte "Proporcionar datos largos para inserciones y actualizaciones masivas" más adelante en esta referencia de función.  
  
 No es necesario que la aplicación llame a **SQLFetch** o **SQLFetchScroll** antes de llamar a **SQLBulkOperations** (excepto cuando se va a un ODBC 2.* x* controlador; consulte [Compatibilidad con versiones anteriores y Cumplimiento](../../../odbc/reference/develop-app/backward-compatibility-and-standards-compliance.md)de normas ).  
  
 El comportamiento está definido por el controlador si **SQLBulkOperations**, con un *operación* argumento de SQL_ADD, se llama en un cursor que contiene columnas duplicadas. El controlador puede devolver un SQLSTATE definido por el controlador, agregar los datos a la primera columna que aparece en el conjunto de resultados o realizar otro comportamiento definido por el controlador.  
  
## <a name="performing-bulk-updates-by-using-bookmarks"></a>Realización de actualizaciones masivas mediante marcadores  
 Para realizar actualizaciones masivas mediante marcadores con **SQLBulkOperations**, una aplicación realiza los pasos siguientes en secuencia:  
  
1.  Establece el atributo de instrucción SQL_ATTR_USE_BOOKMARKS en SQL_UB_VARIABLE.  
  
2.  Ejecuta una consulta que devuelve un conjunto de resultados.  
  
3.  Establece el atributo de instrucción SQL_ATTR_ROW_ARRAY_SIZE en el número de filas que desea actualizar.  
  
4.  Llama a **SQLBindCol** para enlazar los datos que desea actualizar. Los datos se enlazan a una matriz con un tamaño igual al valor de SQL_ATTR_ROW_ARRAY_SIZE. También llama a **SQLBindCol** para enlazar la columna 0 (la columna de marcador).  
  
5.  Copia los marcadores de las filas que le interesa actualizar en la matriz enlazada a la columna 0.  
  
6.  Actualiza los datos en los búferes enlazados.  
  
    > [!NOTE]  
    >  El tamaño de la matriz señalada por el atributo de instrucción SQL_ATTR_ROW_STATUS_PTR debe ser igual a SQL_ATTR_ROW_ARRAY_SIZE o SQL_ATTR_ROW_STATUS_PTR debe ser un puntero nulo.  
  
7.  Llama a **SQLBulkOperations**(*StatementHandle,* SQL_UPDATE_BY_BOOKMARK).  
  
    > [!NOTE]  
    >  Si la aplicación ha establecido el atributo de instrucción SQL_ATTR_ROW_STATUS_PTR, puede inspeccionar esta matriz para ver el resultado de la operación.  
  
8.  Opcionalmente, llama a **SQLBulkOperations**(*StatementHandle*, SQL_FETCH_BY_BOOKMARK) para capturar datos en los búferes de aplicación enlazados para comprobar que se ha producido la actualización.  
  
9. Si se han actualizado los datos, el controlador cambia el valor de la matriz de estado de fila para las filas adecuadas a SQL_ROW_UPDATED.  
  
 Las actualizaciones masivas realizadas por **SQLBulkOperations** pueden incluir datos largos mediante llamadas a **SQLParamData** y **SQLPutData**. Para obtener más información, consulte "Proporcionar datos largos para inserciones y actualizaciones masivas" más adelante en esta referencia de función.  
  
 Si los marcadores persisten entre cursores, la aplicación no necesita llamar a **SQLFetch** o **SQLFetchScroll** antes de actualizar por marcadores. Puede utilizar marcadores que ha almacenado desde un cursor anterior. Si los marcadores no persisten entre cursores, la aplicación tiene que llamar a **SQLFetch** o **SQLFetchScroll** para recuperar los marcadores.  
  
 El comportamiento está definido por el controlador si **SQLBulkOperations**, con un *Operación* argumento de SQL_UPDATE_BY_BOOKMARK, se llama en un cursor que contiene columnas duplicadas. El controlador puede devolver un SQLSTATE definido por el controlador, actualizar la primera columna que aparece en el conjunto de resultados o realizar otro comportamiento definido por el controlador.  
  
## <a name="performing-bulk-fetches-using-bookmarks"></a>Realización de capturas masivas mediante marcadores  
 Para realizar capturas masivas mediante marcadores con **SQLBulkOperations**, una aplicación realiza los pasos siguientes en secuencia:  
  
1.  Establece el atributo de instrucción SQL_ATTR_USE_BOOKMARKS en SQL_UB_VARIABLE.  
  
2.  Ejecuta una consulta que devuelve un conjunto de resultados.  
  
3.  Establece el atributo de instrucción SQL_ATTR_ROW_ARRAY_SIZE en el número de filas que desea capturar.  
  
4.  Llama a **SQLBindCol** para enlazar los datos que desea capturar. Los datos se enlazan a una matriz con un tamaño igual al valor de SQL_ATTR_ROW_ARRAY_SIZE. También llama a **SQLBindCol** para enlazar la columna 0 (la columna de marcador).  
  
5.  Copia los marcadores de las filas que le interesa capturar en la matriz enlazada a la columna 0. (Esto supone que la aplicación ya ha obtenido los marcadores por separado.)  
  
    > [!NOTE]  
    >  El tamaño de la matriz señalada por el atributo de instrucción SQL_ATTR_ROW_STATUS_PTR debe ser igual a SQL_ATTR_ROW_ARRAY_SIZE o SQL_ATTR_ROW_STATUS_PTR debe ser un puntero nulo.  
  
6.  Llama a **SQLBulkOperations**(*StatementHandle,* SQL_FETCH_BY_BOOKMARK).  
  
7.  Si la aplicación ha establecido el atributo de instrucción SQL_ATTR_ROW_STATUS_PTR, puede inspeccionar esta matriz para ver el resultado de la operación.  
  
 Si los marcadores persisten entre cursores, la aplicación no necesita llamar a **SQLFetch** o **SQLFetchScroll** antes de capturar por marcadores. Puede utilizar marcadores que ha almacenado desde un cursor anterior. Si los marcadores no persisten entre cursores, la aplicación tiene que llamar a **SQLFetch** o **SQLFetchScroll** una vez para recuperar los marcadores.  
  
## <a name="performing-bulk-deletes-using-bookmarks"></a>Realización de eliminaciones masivas mediante marcadores  
 Para realizar eliminaciones masivas mediante marcadores con **SQLBulkOperations**, una aplicación realiza los pasos siguientes en secuencia:  
  
1.  Establece el atributo de instrucción SQL_ATTR_USE_BOOKMARKS en SQL_UB_VARIABLE.  
  
2.  Ejecuta una consulta que devuelve un conjunto de resultados.  
  
3.  Establece el atributo de instrucción SQL_ATTR_ROW_ARRAY_SIZE en el número de filas que desea eliminar.  
  
4.  Llama a **SQLBindCol** para enlazar la columna 0 (la columna de marcador).  
  
5.  Copia los marcadores de las filas que le interesa eliminar en la matriz enlazada a la columna 0.  
  
    > [!NOTE]  
    >  El tamaño de la matriz señalada por el atributo de instrucción SQL_ATTR_ROW_STATUS_PTR debe ser igual a SQL_ATTR_ROW_ARRAY_SIZE o SQL_ATTR_ROW_STATUS_PTR debe ser un puntero nulo.  
  
6.  Llama a **SQLBulkOperations**(*StatementHandle,* SQL_DELETE_BY_BOOKMARK).  
  
7.  Si la aplicación ha establecido el atributo de instrucción SQL_ATTR_ROW_STATUS_PTR, puede inspeccionar esta matriz para ver el resultado de la operación.  
  
 Si los marcadores persisten entre cursores, la aplicación no tiene que llamar a **SQLFetch** o **SQLFetchScroll** antes de eliminar por marcadores. Puede utilizar marcadores que ha almacenado desde un cursor anterior. Si los marcadores no persisten entre cursores, la aplicación tiene que llamar a **SQLFetch** o **SQLFetchScroll** una vez para recuperar los marcadores.  
  
## <a name="providing-long-data-for-bulk-inserts-and-updates"></a>Proporcionar datos largos para inserciones y actualizaciones masivas  
 Se pueden proporcionar datos largos para inserciones masivas y actualizaciones realizadas por llamadas a **SQLBulkOperations**. Para insertar o actualizar datos largos, una aplicación realiza los pasos siguientes además de los pasos descritos en las secciones "Realizar inserciones masivas" y "Realizar actualizaciones masivas mediante marcadores" anteriormente en este tema.  
  
1.  Cuando enlaza los datos mediante **SQLBindCol**, la aplicación coloca un valor definido por la aplicación, como el número de columna, en el * \*búfer TargetValuePtr* para las columnas de datos en ejecución. El valor se puede utilizar más adelante para identificar la columna.  
  
     La aplicación coloca el resultado de la macro SQL_LEN_DATA_AT_EXEC(*length*) en el * \*búfer de StrLen_or_IndPtr.* Si el tipo de datos SQL de la columna es SQL_LONGVARBINARY, SQL_LONGVARCHAR o un tipo de datos específico del origen de datos largo y el controlador devuelve "Y" para el tipo de información SQL_NEED_LONG_DATA_LEN en **SQLGetInfo**, *longitud* es el número de bytes de datos que se enviarán para el parámetro; de lo contrario, debe ser un valor no negativo y se ignora.  
  
2.  Cuando **SQLBulkOperations** se llama, si hay columnas de datos en ejecución, la función devuelve SQL_NEED_DATA y procede al paso 3, que sigue. (Si no hay columnas de datos en ejecución, el proceso se ha completado.)  
  
3.  La aplicación llama a **SQLParamData** para recuperar la dirección del * \*búfer TargetValuePtr* para la primera columna de datos en ejecución que se va a procesar. **SQLParamData** devuelve SQL_NEED_DATA. La aplicación recupera el valor definido por la aplicación del * \*búfer TargetValuePtr.*  
  
    > [!NOTE]  
    >  Aunque los parámetros de datos en ejecución se asemejan a las columnas de datos en ejecución, el valor devuelto por **SQLParamData** es diferente para cada una.  
  
     Las columnas de datos en ejecución son columnas de un conjunto de filas para el que se enviarán datos con **SQLPutData** cuando se actualice o inserte una fila con **SQLBulkOperations**. Están enlazados con **SQLBindCol**. El valor devuelto por **SQLParamData** es la dirección de la fila en el **TargetValuePtr* búfer que se está procesando.  
  
4.  La aplicación llama a **SQLPutData** una o varias veces para enviar datos para la columna. Se necesita más de una llamada si no * \** se puede devolver todo el valor de datos en el búfer TargetValuePtr especificado en **SQLPutData**; Solo se permiten varias llamadas a **SQLPutData** para la misma columna al enviar datos de caracteres C a una columna con un tipo de datos específico de carácter, binario o origen de datos o al enviar datos c binarios a una columna con un tipo de datos de carácter, binario o específico del origen de datos.  
  
5.  La aplicación llama a **SQLParamData** de nuevo para indicar que se han enviado todos los datos para la columna.  
  
    -   Si hay más columnas de datos en ejecución, **SQLParamData** devuelve SQL_NEED_DATA y la dirección del búfer *TargetValuePtr* para la siguiente columna de datos en ejecución que se va a procesar. La aplicación repite los pasos 4 y 5.  
  
    -   Si no hay más columnas de datos en ejecución, el proceso se ha completado. Si la instrucción se ejecutó correctamente, **SQLParamData** devuelve SQL_SUCCESS o SQL_SUCCESS_WITH_INFO; si se produce un error en la ejecución, devuelve SQL_ERROR. En este punto, **SQLParamData** puede devolver cualquier SQLSTATE que **SQLBulkOperations**pueda devolver .  
  
 Si se cancela la operación o se produce un error en **SQLParamData** o **SQLPutData** después de **SQLBulkOperations** devuelve SQL_NEED_DATA y antes de que se envíen datos para todas las columnas de datos en ejecución, la aplicación solo puede llamar a **SQLCancel**, **SQLGetDiagField**, **SQLGetDiagRec**, **SQLGetFunctions**, **SQLParamData**o **SQLPutData** para la instrucción o la conexión asociada a la instrucción. Si llama a cualquier otra función para la instrucción o la conexión asociada a la instrucción, la función devuelve SQL_ERROR y SQLSTATE HY010 (error de secuencia de funciones).  
  
 Si la aplicación llama a **SQLCancel** mientras el controlador todavía necesita datos para las columnas de datos en ejecución, el controlador cancela la operación. A continuación, la aplicación puede llamar a **SQLBulkOperations** de nuevo; la cancelación no afecta al estado del cursor ni a la posición actual del cursor.  
  
## <a name="row-status-array"></a>Matriz de Estados de fila  
 La matriz de estado de fila contiene valores de estado para cada fila de datos del conjunto de filas después de una llamada a **SQLBulkOperations**. El controlador establece los valores de estado de esta matriz después de una llamada a **SQLFetch**, **SQLFetchScroll**, **SQLSetPos**o **SQLBulkOperations**. Esta matriz se rellena inicialmente con una llamada a **SQLBulkOperations** si **SQLFetch** o **SQLFetchScroll** no se ha llamado antes de **SQLBulkOperations**. El atributo de instrucción SQL_ATTR_ROW_STATUS_PTR señala esta matriz. El número de elementos de las matrices de estado de fila debe ser igual al número de filas del conjunto de filas (según lo definido por el atributo de instrucción SQL_ATTR_ROW_ARRAY_SIZE). Para obtener información acerca de esta matriz de estado de fila, vea [SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md).  
  
## <a name="code-example"></a>Ejemplo de código  
 En el ejemplo siguiente se capturan 10 filas de datos a la vez de la tabla Customers. A continuación, solicita al usuario que realice una acción. Para reducir el tráfico de red, el búfer de ejemplo se actualiza, elimina e inserta localmente en las matrices enlazadas, pero en desplazamientos más allá de los datos del conjunto de filas. Cuando el usuario decide enviar actualizaciones, eliminaciones e inserciones en el origen de datos, el código establece el desplazamiento de enlace correctamente y llama a **SQLBulkOperations**. Para simplificar, el usuario no puede almacenar en búfer más de 10 actualizaciones, eliminaciones o inserciones.  
  
```cpp  
// SQLBulkOperations_Function.cpp  
// compile with: ODBC32.lib  
#include <windows.h>  
#include <sqlext.h>  
#include "stdio.h"  
  
#define UPDATE_ROW 100  
#define DELETE_ROW 101  
#define ADD_ROW 102  
#define SEND_TO_DATA_SOURCE 103  
#define UPDATE_OFFSET 10  
#define INSERT_OFFSET 20  
#define DELETE_OFFSET 30  
  
// Define structure for customer data (assume 10 byte maximum bookmark size).  
typedef struct tagCustStruct {  
   SQLCHAR Bookmark[10];  
   SQLINTEGER BookmarkLen;  
   SQLUINTEGER CustomerID;  
   SQLINTEGER CustIDInd;  
   SQLCHAR CompanyName[51];  
   SQLINTEGER NameLenOrInd;  
   SQLCHAR Address[51];  
   SQLINTEGER AddressLenOrInd;  
   SQLCHAR Phone[11];  
   SQLINTEGER PhoneLenOrInd;  
} CustStruct;  
  
// Allocate 40 of these structures. Elements 0-9 are for the current rowset,  
// elements 10-19 are for the buffered updates, elements 20-29 are for  
// the buffered inserts, and elements 30-39 are for the buffered deletes.  
CustStruct CustArray[40];  
SQLUSMALLINT RowStatusArray[10], Action, RowNum, NumUpdates = 0, NumInserts = 0,  
NumDeletes = 0;  
SQLLEN BindOffset = 0;  
SQLRETURN retcode;  
SQLHENV henv = NULL;  
SQLHDBC hdbc = NULL;  
SQLHSTMT hstmt = NULL;  
  
int main() {  
   retcode = SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, &henv);  
   retcode = SQLSetEnvAttr(henv, SQL_ATTR_ODBC_VERSION, (SQLPOINTER*)SQL_OV_ODBC3, 0);   
  
   retcode = SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc);   
   retcode = SQLSetConnectAttr(hdbc, SQL_LOGIN_TIMEOUT, (SQLPOINTER)5, 0);  
  
   retcode = SQLConnect(hdbc, (SQLCHAR*) "Northwind", SQL_NTS, (SQLCHAR*) NULL, 0, NULL, 0);  
   retcode = SQLAllocHandle(SQL_HANDLE_STMT, hdbc, &hstmt);  
  
   // Set the following statement attributes:  
   // SQL_ATTR_CURSOR_TYPE:           Keyset-driven  
   // SQL_ATTR_ROW_BIND_TYPE:         Row-wise  
   // SQL_ATTR_ROW_ARRAY_SIZE:        10  
   // SQL_ATTR_USE_BOOKMARKS:         Use variable-length bookmarks  
   // SQL_ATTR_ROW_STATUS_PTR:        Points to RowStatusArray  
   // SQL_ATTR_ROW_BIND_OFFSET_PTR:   Points to BindOffset  
   retcode = SQLSetStmtAttr(hstmt, SQL_ATTR_CURSOR_TYPE, (SQLPOINTER)SQL_CURSOR_KEYSET_DRIVEN, 0);  
   retcode = SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_BIND_TYPE, (SQLPOINTER)sizeof(CustStruct), 0);  
   retcode = SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_ARRAY_SIZE, (SQLPOINTER)10, 0);  
   retcode = SQLSetStmtAttr(hstmt, SQL_ATTR_USE_BOOKMARKS, (SQLPOINTER)SQL_UB_VARIABLE, 0);  
   retcode = SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_STATUS_PTR, RowStatusArray, 0);  
   retcode = SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_BIND_OFFSET_PTR, &BindOffset, 0);  
  
   // Bind arrays to the bookmark, CustomerID, CompanyName, Address, and Phone columns.  
   retcode = SQLBindCol(hstmt, 0, SQL_C_VARBOOKMARK, CustArray[0].Bookmark, sizeof(CustArray[0].Bookmark), &CustArray[0].BookmarkLen);  
   retcode = SQLBindCol(hstmt, 1, SQL_C_ULONG, &CustArray[0].CustomerID, 0, &CustArray[0].CustIDInd);  
   retcode = SQLBindCol(hstmt, 2, SQL_C_CHAR, CustArray[0].CompanyName, sizeof(CustArray[0].CompanyName), &CustArray[0].NameLenOrInd);  
   retcode = SQLBindCol(hstmt, 3, SQL_C_CHAR, CustArray[0].Address, sizeof(CustArray[0].Address), &CustArray[0].AddressLenOrInd);  
   retcode = SQLBindCol(hstmt, 4, SQL_C_CHAR, CustArray[0].Phone, sizeof(CustArray[0].Phone), &CustArray[0].PhoneLenOrInd);  
  
   // Execute a statement to retrieve rows from the Customers table.  
   retcode = SQLExecDirect(hstmt, (SQLCHAR*)"SELECT CustomerID, CompanyName, Address, Phone FROM Customers", SQL_NTS);  
  
   // Fetch and display the first 10 rows.  
   retcode = SQLFetchScroll(hstmt, SQL_FETCH_NEXT, 0);  
   // DisplayCustData(CustArray, 10);  
  
   // Call GetAction to get an action and a row number from the user.  
   // while (GetAction(&Action, &RowNum)) {  
   Action = SQL_FETCH_NEXT;  
   RowNum = 2;  
   switch (Action) {  
      case SQL_FETCH_NEXT:  
      case SQL_FETCH_PRIOR:  
      case SQL_FETCH_FIRST:  
      case SQL_FETCH_LAST:  
      case SQL_FETCH_ABSOLUTE:  
      case SQL_FETCH_RELATIVE:  
         // Fetch and display the requested data.  
         SQLFetchScroll(hstmt, Action, RowNum);  
         // DisplayCustData(CustArray, 10);  
         break;  
  
      case UPDATE_ROW:  
         // Check if we have reached the maximum number of buffered updates.  
         if (NumUpdates < 10) {  
            // Get the new customer data and place it in the next available element of  
            // the buffered updates section of CustArray, copy the bookmark of the row  
            // being updated to the same element, and increment the update counter.  
            // Checking to see we have not already buffered an update for this  
            // row not shown.  
            // GetNewCustData(CustArray, UPDATE_OFFSET + NumUpdates);  
            memcpy(CustArray[UPDATE_OFFSET + NumUpdates].Bookmark,  
               CustArray[RowNum - 1].Bookmark,  
               CustArray[RowNum - 1].BookmarkLen);  
            CustArray[UPDATE_OFFSET + NumUpdates].BookmarkLen =  
               CustArray[RowNum - 1].BookmarkLen;  
            NumUpdates++;  
         } else {  
            printf("Buffers full. Send buffered changes to the data source.");  
         }  
         break;  
      case DELETE_ROW:  
         // Check if we have reached the maximum number of buffered deletes.  
         if (NumDeletes < 10) {  
            // Copy the bookmark of the row being deleted to the next available element  
            // of the buffered deletes section of CustArray and increment the delete  
            // counter. Checking to see we have not already buffered an update for  
            // this row not shown.  
            memcpy(CustArray[DELETE_OFFSET + NumDeletes].Bookmark,  
               CustArray[RowNum - 1].Bookmark,  
               CustArray[RowNum - 1].BookmarkLen);  
  
            CustArray[DELETE_OFFSET + NumDeletes].BookmarkLen =  
               CustArray[RowNum - 1].BookmarkLen;  
  
            NumDeletes++;  
         } else  
            printf("Buffers full. Send buffered changes to the data source.");  
         break;  
  
      case ADD_ROW:  
         // reached maximum number of buffered inserts?  
         if (NumInserts < 10) {  
            // Get the new customer data and place it in the next available element of  
            // the buffered inserts section of CustArray and increment insert counter.  
            // GetNewCustData(CustArray, INSERT_OFFSET + NumInserts);  
            NumInserts++;  
         } else  
            printf("Buffers full. Send buffered changes to the data source.");  
         break;  
  
      case SEND_TO_DATA_SOURCE:  
         // If there are any buffered updates, inserts, or deletes, set the array size  
         // to that number, set the binding offset to use the data in the buffered  
         // update, insert, or delete part of CustArray, and call SQLBulkOperations to  
         // do the updates, inserts, or deletes. Because we will never have more than  
         // 10 updates, inserts, or deletes, we can use the same row status array.  
         if (NumUpdates) {  
            SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_ARRAY_SIZE, (SQLPOINTER)NumUpdates, 0);  
            BindOffset = UPDATE_OFFSET * sizeof(CustStruct);  
            SQLBulkOperations(hstmt, SQL_UPDATE_BY_BOOKMARK);  
            NumUpdates = 0;  
         }  
  
         if (NumInserts) {  
            SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_ARRAY_SIZE, (SQLPOINTER)NumInserts, 0);  
            BindOffset = INSERT_OFFSET * sizeof(CustStruct);  
            SQLBulkOperations(hstmt, SQL_ADD);  
            NumInserts = 0;  
         }  
  
         if (NumDeletes) {  
            SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_ARRAY_SIZE, (SQLPOINTER)NumDeletes, 0);  
            BindOffset = DELETE_OFFSET * sizeof(CustStruct);  
            SQLBulkOperations(hstmt, SQL_DELETE_BY_BOOKMARK);  
            NumDeletes = 0;  
         }  
  
         // If there were any updates, inserts, or deletes, reset the binding offset  
         // and array size to their original values.  
         if (NumUpdates || NumInserts || NumDeletes) {  
            SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_ARRAY_SIZE, (SQLPOINTER)10, 0);  
            BindOffset = 0;  
         }  
         break;  
   }  
   // }  
  
   // Close the cursor.  
   SQLFreeStmt(hstmt, SQL_CLOSE);  
}  
```  
  
## <a name="related-functions"></a>Funciones relacionadas  
  
|Para información acerca de|Vea|  
|---------------------------|---------|  
|Enlazar un búfer a una columna en un conjunto de resultados|[SQLBindCol (función)](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Cancelación del procesamiento de extractos|[Función SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Obtención de un bloque de datos o desplazamiento por un conjunto de resultados|[Función SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|Obtener un único campo de un descriptor|[Función SQLGetDescField](../../../odbc/reference/syntax/sqlgetdescfield-function.md)|  
|Obtención de varios campos de un descriptor|[Función SQLGetDescRec](../../../odbc/reference/syntax/sqlgetdescrec-function.md)|  
|Establecer un único campo de un descriptor|[Función SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)|  
|Establecer varios campos de un descriptor|[Función SQLSetDescRec](../../../odbc/reference/syntax/sqlsetdescrec-function.md)|  
|Colocación del cursor, actualización de datos en el conjunto de filas o actualización o eliminación de datos en el conjunto de filas|[Función SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md)|  
|Establecer un atributo de instrucción|[Función SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de la API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Archivos de encabezado de ODBC](../../../odbc/reference/install/odbc-header-files.md)
