---
title: Función SQLBulkOperations | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLBulkOperations
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLBulkOperations
helpviewer_keywords:
- SQLBulkOperations function [ODBC]
ms.assetid: 7029d0da-b0f2-44e6-9114-50bd96f47196
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 14e51f1d04012e22c198b7ed5f70d9b508933c5d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "65538035"
---
# <a name="sqlbulkoperations-function"></a>Función SQLBulkOperations
**Conformidad**  
 Versión de introducción: Compatibilidad de ODBC 3.0 estándares: ODBC  
  
 **Resumen**  
 **SQLBulkOperations** realiza inserciones masivas y marcador de forma masiva las operaciones, incluida la actualización, eliminar y recuperar por marcador.  
  
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
 [Entrada] Para realizar la operación:  
  
 SQL_ADD SQL_UPDATE_BY_BOOKMARK SQL_DELETE_BY_BOOKMARK SQL_FETCH_BY_BOOKMARK  
  
 Para obtener más información, vea "Comentarios".  
  
## <a name="returns"></a>Devuelve  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NEED_DATA, SQL_STILL_EXECUTING, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Cuando **SQLBulkOperations** devuelve SQL_ERROR o SQL_SUCCESS_WITH_INFO, un valor SQLSTATE asociado se puede obtener mediante una llamada a **SQLGetDiagRec** con un *HandleType* de SQL_HANDLE_STMT y un *controlar* de *StatementHandle*. En la tabla siguiente se enumera los valores SQLSTATE devueltos normalmente por **SQLBulkOperations** y se explica cada uno de ellos en el contexto de esta función; la notación "(DM)" precede a las descripciones de SQLSTATE devuelto por el Administrador de controladores . El código de retorno asociado a cada valor SQLSTATE es SQL_ERROR, a menos que se indique lo contrario.  
  
 Para todas esas SQLSTATE que puede devolver SQL_SUCCESS_WITH_INFO o SQL_ERROR (excepto 01xxx SQLSTATEs), se devuelve SQL_SUCCESS_WITH_INFO, si se produce un error en uno o más, pero no todas las filas de una operación de varias filas, y se devuelve SQL_ERROR si se produce un error en un fila única operación.  
  
|SQLSTATE|Error|Descripción|  
|--------------|-----------|-----------------|  
|01000|Advertencia general|Específico del controlador de mensaje informativo. (La función devuelve SQL_SUCCESS_WITH_INFO).|  
|01004|Truncamiento de datos derecho de cadena|El *operación* argumento era SQL_FETCH_BY_BOOKMARK y cadena o datos binarios devueltos para una o varias columnas con un tipo de datos SQL_C_CHAR o SQL_C_BINARY dieron como resultado el truncamiento de carácter no en blanco o datos binarios que no son NULL.|  
|01S01|Error en la fila|El *operación* argumento era SQL_ADD y se produjo un error en una o varias filas al realizar la operación, pero se ha agregado correctamente al menos una fila. (La función devuelve SQL_SUCCESS_WITH_INFO).<br /><br /> (Este error se genera solo cuando una aplicación está trabajando con un ODBC 2. *x* controlador.)|  
|01S07|Truncamiento fraccionario|El *operación* argumento era SQL_FETCH_BY_BOOKMARK, el tipo de datos del búfer de aplicación no era SQL_C_CHAR o SQL_C_BINARY y se truncaron los datos devueltos a los búferes de la aplicación para una o varias columnas. (Para los tipos de datos numéricos de C, se trunca la parte fraccionaria del número. Para el tiempo, marca de tiempo y los tipos de datos de intervalo de C que contienen un componente de tiempo, la parte fraccionaria del tiempo se truncaron.)<br /><br /> (La función devuelve SQL_SUCCESS_WITH_INFO).|  
|07006|Infracción del atributo de tipo de datos restringido|El *operación* argumento era SQL_FETCH_BY_BOOKMARK y no se pudo convertir el valor de datos de una columna del conjunto de resultados para el tipo de datos especificado por el *TargetType* argumento en la llamada a **SQLBindCol**.<br /><br /> El *operación* argumento era SQL_UPDATE_BY_BOOKMARK o SQL_ADD y el valor de datos en los búferes de la aplicación no se pudo convertir al tipo de datos de una columna del conjunto de resultados.|  
|07009|Índice de descriptor no válido|El argumento *operación* era SQL_ADD y se enlaza una columna con un número de columna mayor que el número de columnas del conjunto de resultados.|  
|21S02|Grado de la tabla derivada no coincide con la lista de columnas|El argumento *operación* era SQL_UPDATE_BY_BOOKMARK; y no hay columnas eran actualizables porque todas las columnas eran independientes o de solo lectura o el valor en el búfer de longitud/indicador enlazado era SQL_COLUMN_IGNORE.|  
|22001|Truncamiento de datos derecho de cadena|La asignación de un carácter o un valor binario a una columna del conjunto de resultados producía el truncamiento de no están en blanco (para los caracteres) o distinto de null (para el binario) caracteres o bytes.|  
|22003|Valor numérico fuera del intervalo|El *operación* argumento estaba SQL_ADD o SQL_UPDATE_BY_BOOKMARK y la asignación de un valor numérico a una columna del conjunto de resultados provocó la parte entera (en contraposición a fraccionarios) del número que se va a truncar.<br /><br /> El argumento *operación* era SQL_FETCH_BY_BOOKMARK y devolver el valor numérico para una o varias columnas enlazadas, habría provocado una pérdida de dígitos significativos.|  
|22007|Formato de datetime no válido|El *operación* argumento estaba SQL_ADD o SQL_UPDATE_BY_BOOKMARK y la asignación de un valor date o timestamp a una columna del conjunto de resultados que provocó el año, mes o campo día para estar fuera del intervalo.<br /><br /> El argumento *operación* era SQL_FETCH_BY_BOOKMARK y devolver el valor de fecha o la marca de tiempo para uno o más columnas enlazadas habría provocado el año, mes o campo día para estar fuera del intervalo.|  
|22008|Desbordamiento del campo de fecha y hora|El *operación* argumento era SQL_ADD o SQL_UPDATE_BY_BOOKMARK y el rendimiento de fecha y hora aritmética en datos que se envían a una columna del conjunto de resultados dieron lugar a un campo de fecha y hora (el año, mes, día, hora, minuto o segundo campo) del resultado queda fuera del intervalo válido de valores para el campo o no sea válido según las reglas en natural para fechas y horas del calendario gregoriano.<br /><br /> El *operación* argumento era SQL_FETCH_BY_BOOKMARK y el rendimiento de fecha y hora aritmética en los datos recuperados del conjunto de resultados dieron lugar a un campo de fecha y hora (año, mes, día, hora, minuto o segundo campo) de la resultado queda fuera del intervalo válido de valores para el campo o no sea válido según las reglas en natural para fechas y horas del calendario gregoriano.|  
|22015|Desbordamiento de campo de intervalo|El *operación* argumento era SQL_ADD o SQL_UPDATE_BY_BOOKMARK y la asignación de un valor numérico exacto o el tipo de intervalo C a un tipo de datos SQL de intervalo causó una pérdida de dígitos significativos.<br /><br /> El *operación* argumento era SQL_ADD o SQL_UPDATE_BY_BOOKMARK; cuando se asigna a un intervalo de tipo SQL, no había ninguna representación del valor del tipo C en el intervalo de tipo SQL.<br /><br /> El *operación* argumento era SQL_FETCH_BY_BOOKMARK y asignación de un valor numérico exacto o el intervalo de tipo SQL a un tipo de intervalo C causó una pérdida de dígitos significativos en el campo inicial.<br /><br /> El *operación* argumento era SQL_FETCH_BY_BOOKMARK; cuando se asigna a un tipo de intervalo de C, no había ninguna representación del valor del tipo SQL en el tipo de intervalo C.|  
|22018|Valor de carácter no válido para especificación cast|El *operación* argumento era SQL_FETCH_BY_BOOKMARK; el tipo C era un numérico exacto o aproximado, una fecha y hora o un tipo de datos de intervalo; el tipo SQL de la columna era un tipo de datos de caracteres; y el valor de la columna no era válido literal de tipo C enlazado.<br /><br /> El argumento *operación* era SQL_ADD o SQL_UPDATE_BY_BOOKMARK; el tipo SQL era un numérico exacto o aproximado, una fecha y hora o un tipo de datos de intervalo; el tipo de C era SQL_C_CHAR; y el valor de la columna no es un literal válido de la tipo SQL de enlazado.|  
|23000|Infracción de restricción de integridad|El *operación* argumento era SQL_ADD, SQL_DELETE_BY_BOOKMARK o SQL_UPDATE_BY_BOOKMARK y se ha infringido una restricción de integridad.<br /><br /> El *operación* argumento era SQL_ADD y una columna que no estaba enlazada se define como no NULL y no tiene valor predeterminado.<br /><br /> El *operación* argumento era SQL_ADD, la longitud especificada en el límite *StrLen_or_IndPtr* búfer era SQL_COLUMN_IGNORE y la columna no tenía un valor predeterminado.|  
|24000|Estado de cursor no válido|El *StatementHandle* estaba en un estado ejecutado, pero se ha asociado ningún conjunto de resultados la *StatementHandle*.|  
|40001|Error de serialización.|Debido a un interbloqueo de recurso con otra transacción se revirtió la transacción.|  
|40003|Finalización de instrucción desconocida|Error en la conexión asociada durante la ejecución de esta función y no se puede determinar el estado de la transacción.|  
|42000|Error de sintaxis, infracción de acceso|El controlador no pudo bloquear la fila según sea necesario para realizar la operación solicitada en el *operación* argumento.|  
|44000|Infracción de WITH CHECK OPTION|El *operación* argumento era SQL_ADD o SQL_UPDATE_BY_BOOKMARK y la inserción o actualización realizada en una tabla vista (o una tabla derivada de la tabla mostrada) que se creó mediante la especificación de **WITH CHECK OPTION**, de tal forma que una o varias filas afectadas por la inserción o actualización ya no estará presente en la tabla mostrada.|  
|HY000|Error general|Se produjo un error para que se ha producido ningún SQLSTATE específico y para los que se ha definido ningún SQLSTATE específicos de la implementación. El mensaje de error devuelto por **SQLGetDiagRec** en el  *\*MessageText* búfer describe el error y su causa.|  
|HY001|Error de asignación de memoria|El controlador no pudo asignar la memoria necesaria para admitir la ejecución o la finalización de la función.|  
|HY008|Operación cancelada|Procesamiento asincrónico se habilitó para la *StatementHandle*. Se llamó a la función, y antes que completó la ejecución, **SQLCancel** o **SQLCancelHandle** se ha llamado en el *StatementHandle*. A continuación, la función se llamó de nuevo en el *StatementHandle*.<br /><br /> Se llamó a la función, y antes que completó la ejecución, **SQLCancel** o **SQLCancelHandle** se ha llamado en el *StatementHandle* desde un subproceso diferente en un aplicaciones multiproceso.|  
|HY010|Error de secuencia de función|(DM) se llamó a una función que se ejecuta de forma asincrónica para el identificador de conexión que está asociado el *StatementHandle*. Aún estaba ejecutando esta función asincrónica cuando el **SQLBulkOperations** se llamó a la función.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, o **SQLMoreResults** se llamó para el *StatementHandle* y devuelven SQL_PARAM_DATA_ ESTÁ DISPONIBLE. Esta función se invoca antes de que se recuperan los datos para todos los parámetros transmitidos.<br /><br /> (DM) especificado *StatementHandle* no estaba en un estado ejecutado. Se llamó a la función sin llamar primero a **SQLExecDirect**, **SQLExecute**, o una función de catálogo.<br /><br /> (DM) se llamó a una función que se ejecuta asincrónicamente (no ésta) para el *StatementHandle* y aún se estaba ejecutando cuando se llamó a esta función.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, o **SQLSetPos** se llamó para el *StatementHandle* y devuelve SQL_NEED_DATA. Esta función se invoca antes de que se enviaron datos para todas las columnas o parámetros de datos en ejecución.<br /><br /> (DM) el controlador fue un 2 de ODBC. *x* controlador, y **SQLBulkOperations** se llamó para un *StatementHandle* antes **SQLFetchScroll** o **SQLFetch**  se llamó.<br /><br /> (DM) **SQLBulkOperations** llamó después **SQLExtendedFetch** se ha llamado en el *StatementHandle*.|  
|HY011|Atributo no se puede establecer ahora|(DM) el controlador fue un 2 de ODBC. *x* se estableció el controlador y el atributo de instrucción SQL_ATTR_ROW_STATUS_PTR entre las llamadas a **SQLFetch** o **SQLFetchScroll** y **SQLBulkOperations** .|  
|HY013|Error de administración de memoria|No se pudo procesar la llamada de función porque los objetos de memoria subyacente no se podrían tener acceso, posiblemente debido a memoria insuficiente.|  
|HY090|Longitud de búfer o cadena no válida|El *operación* argumento era SQL_ADD o SQL_UPDATE_BY_BOOKMARK; un valor de datos no era un puntero nulo; el tipo de datos C era SQL_C_BINARY o SQL_C_CHAR; y el valor de longitud de columna era menor que 0, pero no es igual a SQL_DATA_AT_EXEC , SQL_COLUMN_IGNORE, SQL_NTS o SQL_NULL_DATA, o menor o igual que SQL_LEN_DATA_AT_EXEC_OFFSET.<br /><br /> El valor en un búfer de longitud/indicador era SQL_DATA_AT_EXEC; el tipo SQL era SQL_LONGVARCHAR, SQL_LONGVARBINARY o un tipo de datos específicos del origen de datos long; y el tipo de información SQL_NEED_LONG_DATA_LEN **SQLGetInfo** era "S".<br /><br /> El *operación* argumento era SQL_ADD, el atributo de instrucción SQL_ATTR_USE_BOOKMARK se estableció en SQL_UB_VARIABLE y la columna 0 estaba enlazada a un búfer cuya longitud no es igual a la longitud máxima para el marcador para este conjunto de resultados. (Esta longitud está disponible en el campo SQL_DESC_OCTET_LENGTH de IRD y se puede obtener mediante una llamada a **SQLDescribeCol**, **SQLColAttribute**, o **SQLGetDescField**.)|  
|HY092|Identificador de atributo no válido|(DM) el valor especificado para el *operación* argumento no era válido.<br /><br /> El *operación* argumento era SQL_ADD, SQL_UPDATE_BY_BOOKMARK o SQL_DELETE_BY_BOOKMARK y se estableció el atributo de instrucción SQL_ATTR_CONCURRENCY en SQL_CONCUR_READ_ONLY.<br /><br /> El *operación* argumento era SQL_DELETE_BY_BOOKMARK, SQL_FETCH_BY_BOOKMARK o SQL_UPDATE_BY_BOOKMARK y no se ha enlazado la columna de marcador o el atributo de instrucción SQL_ATTR_USE_BOOKMARKS se estableció en SQL_UB_OFF.|  
|HY117|Conexión está suspendida debido al estado de transacción desconocido. Solo se desconecte y se permiten funciones de solo lectura.|(DM) para obtener más información sobre el estado suspendido, consulte [función SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Característica opcional no implementada|El controlador u origen de datos no admite la operación solicitada en el *operación* argumento.|  
|HYT00|Se agotó el tiempo de espera|Ha expirado el período de tiempo de espera de consulta antes de que el origen de datos devuelva el conjunto de resultados. El período de tiempo de espera se establece a través de **SQLSetStmtAttr** con un *atributo* argumento de SQL_ATTR_QUERY_TIMEOUT.|  
|HYT01|Tiempo de espera de conexión agotado|Ha expirado el período de tiempo de espera de conexión antes de que el origen de datos que respondió a la solicitud. El período de tiempo de espera de conexión se establece a través de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Controlador no admite esta función|(DM) el controlador asociado con el *StatementHandle* no admite la función.|  
|IM017|Sondeo se deshabilita en modo de notificación asincrónica|Cada vez que se usa el modelo de notificación, se deshabilita el sondeo.|  
|IM018|**SQLCompleteAsync** no se ha llamado para completar la operación asincrónica anterior en este identificador.|Si la llamada de función anterior en el controlador devuelve SQL_STILL_EXECUTING y si está habilitado el modo de notificación, **SQLCompleteAsync** debe llamarse en el identificador para realizar el procesamiento posterior y completar la operación.|  
  
## <a name="comments"></a>Comentarios  
  
> [!CAUTION]  
>  Para obtener información acerca de qué instrucción indica **SQLBulkOperations** puede llamarse y lo que debe hacer para ofrecer compatibilidad con ODBC 2. *x* las aplicaciones, vea el [cursores de bloque, cursores desplazables y compatibilidad con versiones anteriores](../../../odbc/reference/appendixes/block-cursors-scrollable-cursors-and-backward-compatibility.md) sección en el apéndice G: Directrices de controlador para la compatibilidad con versiones anteriores.  
  
 Una aplicación usa **SQLBulkOperations** para realizar las siguientes operaciones en la tabla base o vista que corresponde a la consulta actual:  
  
-   Agregar nuevas filas.  
  
-   Actualizar un conjunto de filas, donde cada fila se identifica mediante un marcador.  
  
-   Eliminar un conjunto de filas, donde cada fila se identifica mediante un marcador.  
  
-   Capturar un conjunto de filas, donde cada fila se identifica mediante un marcador.  
  
 Después de llamar a **SQLBulkOperations**, la posición del cursor de bloque es indefinida. La aplicación tiene que llamar a **SQLFetchScroll** para establecer la posición del cursor. Una aplicación debe llamar a **SQLFetchScroll** solo con un *FetchOrientation* argumento de SQL_FETCH_FIRST, SQL_FETCH_LAST, SQL_FETCH_ABSOLUTE o SQL_FETCH_BOOKMARK. La posición del cursor es indefinida si la aplicación llama a **SQLFetch** o **SQLFetchScroll** con un *FetchOrientation* argumento de SQL_FETCH_PRIOR, SQL_FETCH_NEXT, o SQL_FETCH_RELATIVE.  
  
 Puede omitir una columna en operaciones masivas realizadas mediante una llamada a **SQLBulkOperations** estableciendo el búfer de longitud/indicador de columna especificado en la llamada a **SQLBindCol**, para SQL_COLUMN_IGNORE.  
  
 No es necesario para la aplicación para establecer el atributo de instrucción SQL_ATTR_ROW_OPERATION_PTR cuando llama a **SQLBulkOperations** porque no se pueden omitir las filas al realizar operaciones masivas con esta función.  
  
 El búfer señalado por el atributo SQL_ATTR_ROWS_FETCHED_PTR la instrucción contiene el número de filas afectadas por una llamada a **SQLBulkOperations**.  
  
 Cuando el *operación* argumento es SQL_ADD o SQL_UPDATE_BY_BOOKMARK y la lista de selección de la especificación de consulta asociada con el cursor contiene más de una referencia a la misma columna, es definido por el controlador si un error se genera o el controlador omite las referencias duplicadas y realiza las operaciones solicitadas.  
  
 Para obtener más información sobre cómo usar **SQLBulkOperations**, consulte [actualizar los datos con SQLBulkOperations](../../../odbc/reference/develop-app/updating-data-with-sqlbulkoperations.md).  
  
## <a name="performing-bulk-inserts"></a>Ejecute inserciones masivas  
 Para insertar datos con **SQLBulkOperations**, una aplicación realiza la siguiente secuencia de pasos:  
  
1.  Ejecuta una consulta que devuelve un conjunto de resultados.  
  
2.  Establece el atributo de instrucción SQL_ATTR_ROW_ARRAY_SIZE en el número de filas que se va a insertar.  
  
3.  Las llamadas **SQLBindCol** para enlazar los datos que se va a insertar. Los datos se enlazan a una matriz con un tamaño igual al valor de SQL_ATTR_ROW_ARRAY_SIZE.  
  
    > [!NOTE]  
    >  El tamaño de la matriz señalada por el atributo de instrucción SQL_ATTR_ROW_STATUS_PTR debe ser igual a SQL_ATTR_ROW_ARRAY_SIZE o SQL_ATTR_ROW_STATUS_PTR debe ser un puntero nulo.  
  
4.  Las llamadas **SQLBulkOperations**(*StatementHandle,* SQL_ADD) para realizar la inserción.  
  
5.  Si la aplicación ha establecido el atributo de instrucción SQL_ATTR_ROW_STATUS_PTR, puede inspeccionar esta matriz para ver el resultado de la operación.  
  
 Si una aplicación enlaza la columna 0 antes de llamar a **SQLBulkOperations** con un *operación* argumento de SQL_ADD, el controlador actualizará los búferes de columna enlazada 0 con los valores de marcador para el recién fila insertada. Para que esto, la aplicación debe haber establecer el atributo de instrucción SQL_ATTR_USE_BOOKMARKS a SQL_UB_VARIABLE antes de ejecutar la instrucción. (Esto no funciona con una API ODBC 2. *x* controlador.)  
  
 SQLBulkOperations, pueden agregar en elementos de datos de tipo Long mediante llamadas a SQLParamData y SQLPutData. Para obtener más información, vea "Proporcionar largo datos para la masiva Inserts y Updates" más adelante en esta referencia de función.  
  
 No es necesario para la aplicación llamar a **SQLFetch** o **SQLFetchScroll** antes de llamar a **SQLBulkOperations** (excepto cuando va contra un ODBC 2. *x* controlador; vea [compatibilidad con versiones anteriores y el cumplimiento de estándares](../../../odbc/reference/develop-app/backward-compatibility-and-standards-compliance.md)).  
  
 El comportamiento está definido por el controlador si **SQLBulkOperations**, con un *operación* argumento de SQL_ADD, se llama en un cursor que contiene las columnas duplicadas. El controlador puede devolver un valor de SQLSTATE definidos por el controlador, agregue los datos a la primera columna que aparece en el resultado de establecer o realizan otros comportamientos definidos por el controlador.  
  
## <a name="performing-bulk-updates-by-using-bookmarks"></a>Realizar actualizaciones masivas mediante el uso de marcadores  
 Para realizar actualizaciones masivas mediante el uso de marcadores con **SQLBulkOperations**, una aplicación realiza los siguientes pasos en secuencia:  
  
1.  Define el atributo de instrucción SQL_ATTR_USE_BOOKMARKS SQL_UB_VARIABLE.  
  
2.  Ejecuta una consulta que devuelve un conjunto de resultados.  
  
3.  Establece el atributo de instrucción SQL_ATTR_ROW_ARRAY_SIZE en el número de filas que desea actualizar.  
  
4.  Las llamadas **SQLBindCol** para enlazar los datos que desea actualizar. Los datos se enlazan a una matriz con un tamaño igual al valor de SQL_ATTR_ROW_ARRAY_SIZE. También llama a **SQLBindCol** para enlazar la columna 0 (la columna de marcador).  
  
5.  Copias los marcadores para las filas que está interesada en la actualización en la matriz se enlaza a la columna 0.  
  
6.  Actualiza los datos en los búferes de enlazado.  
  
    > [!NOTE]  
    >  El tamaño de la matriz señalada por el atributo de instrucción SQL_ATTR_ROW_STATUS_PTR debe ser igual a SQL_ATTR_ROW_ARRAY_SIZE o SQL_ATTR_ROW_STATUS_PTR debe ser un puntero nulo.  
  
7.  Las llamadas **SQLBulkOperations**(*StatementHandle,* SQL_UPDATE_BY_BOOKMARK).  
  
    > [!NOTE]  
    >  Si la aplicación ha establecido el atributo de instrucción SQL_ATTR_ROW_STATUS_PTR, puede inspeccionar esta matriz para ver el resultado de la operación.  
  
8.  Opcionalmente, llama a **SQLBulkOperations**(*StatementHandle*, SQL_FETCH_BY_BOOKMARK) para capturar los datos en los búferes de la aplicación dependiente para comprobar que la actualización se ha producido.  
  
9. Si se han actualizado los datos, el controlador cambia el valor de la matriz de estado de fila para las filas correspondientes a SQL_ROW_UPDATED.  
  
 Actualizaciones realizadas por masivas **SQLBulkOperations** puede incluir datos de tipo long mediante llamadas a **SQLParamData** y **SQLPutData**. Para obtener más información, vea "Proporcionar largo datos para la masiva Inserts y Updates" más adelante en esta referencia de función.  
  
 Si los marcadores son persistentes entre los cursores, la aplicación no es necesario llamar a **SQLFetch** o **SQLFetchScroll** antes de actualizar por marcadores. Puede utilizar marcadores que tiene almacenado de un cursor anterior. Si no los marcadores son persistentes entre los cursores, la aplicación tiene que llamar a **SQLFetch** o **SQLFetchScroll** para recuperar los marcadores.  
  
 El comportamiento está definido por el controlador si **SQLBulkOperations**, con un *operación* argumento de SQL_UPDATE_BY_BOOKMARK, se llama en un cursor que contiene las columnas duplicadas. El controlador puede devolver un valor de SQLSTATE definidos por el controlador, actualizar la primera columna que aparece en el conjunto de resultados o realizar otros comportamientos definidos por el controlador.  
  
## <a name="performing-bulk-fetches-using-bookmarks"></a>Realización de forma masiva captura mediante marcadores  
 Para realizar capturas de forma masiva mediante marcadores con **SQLBulkOperations**, una aplicación realiza los siguientes pasos en secuencia:  
  
1.  Define el atributo de instrucción SQL_ATTR_USE_BOOKMARKS SQL_UB_VARIABLE.  
  
2.  Ejecuta una consulta que devuelve un conjunto de resultados.  
  
3.  Establece el atributo de instrucción SQL_ATTR_ROW_ARRAY_SIZE en el número de filas que desea capturar.  
  
4.  Las llamadas **SQLBindCol** para enlazar los datos que desea capturar. Los datos se enlazan a una matriz con un tamaño igual al valor de SQL_ATTR_ROW_ARRAY_SIZE. También llama a **SQLBindCol** para enlazar la columna 0 (la columna de marcador).  
  
5.  Copias los marcadores para las filas que está interesada en la captura en la matriz se enlaza a la columna 0. (Esto supone que la aplicación ya ha obtenido los marcadores por separado).  
  
    > [!NOTE]  
    >  El tamaño de la matriz señalada por el atributo de instrucción SQL_ATTR_ROW_STATUS_PTR debe ser igual a SQL_ATTR_ROW_ARRAY_SIZE o SQL_ATTR_ROW_STATUS_PTR debe ser un puntero nulo.  
  
6.  Las llamadas **SQLBulkOperations**(*StatementHandle,* SQL_FETCH_BY_BOOKMARK).  
  
7.  Si la aplicación ha establecido el atributo de instrucción SQL_ATTR_ROW_STATUS_PTR, puede inspeccionar esta matriz para ver el resultado de la operación.  
  
 Si los marcadores son persistentes entre los cursores, la aplicación no es necesario llamar a **SQLFetch** o **SQLFetchScroll** antes de capturar por marcadores. Puede utilizar marcadores que tiene almacenado de un cursor anterior. Si no los marcadores son persistentes entre los cursores, la aplicación tiene que llamar a **SQLFetch** o **SQLFetchScroll** una vez para recuperar los marcadores.  
  
## <a name="performing-bulk-deletes-using-bookmarks"></a>Realización de forma masiva elimina mediante marcadores  
 Para realizar eliminaciones masivas utilizando marcadores con **SQLBulkOperations**, una aplicación realiza los siguientes pasos en secuencia:  
  
1.  Define el atributo de instrucción SQL_ATTR_USE_BOOKMARKS SQL_UB_VARIABLE.  
  
2.  Ejecuta una consulta que devuelve un conjunto de resultados.  
  
3.  Establece el atributo de instrucción SQL_ATTR_ROW_ARRAY_SIZE en el número de filas que desea eliminar.  
  
4.  Las llamadas **SQLBindCol** para enlazar la columna 0 (la columna de marcador).  
  
5.  Copias los marcadores para las filas que está interesado en Eliminar en la matriz se enlaza a la columna 0.  
  
    > [!NOTE]  
    >  El tamaño de la matriz señalada por el atributo de instrucción SQL_ATTR_ROW_STATUS_PTR debe ser igual a SQL_ATTR_ROW_ARRAY_SIZE o SQL_ATTR_ROW_STATUS_PTR debe ser un puntero nulo.  
  
6.  Las llamadas **SQLBulkOperations**(*StatementHandle,* SQL_DELETE_BY_BOOKMARK).  
  
7.  Si la aplicación ha establecido el atributo de instrucción SQL_ATTR_ROW_STATUS_PTR, puede inspeccionar esta matriz para ver el resultado de la operación.  
  
 Si los marcadores son persistentes entre los cursores, no tiene la aplicación llamar a **SQLFetch** o **SQLFetchScroll** antes de la eliminación de marcadores. Puede utilizar marcadores que tiene almacenado de un cursor anterior. Si no los marcadores son persistentes entre los cursores, la aplicación tiene que llamar a **SQLFetch** o **SQLFetchScroll** una vez para recuperar los marcadores.  
  
## <a name="providing-long-data-for-bulk-inserts-and-updates"></a>Proporcionar datos largos de las actualizaciones e inserciones masivas  
 Se pueden proporcionar datos de tipo Long para inserciones masivas y actualizaciones realizadas por las llamadas a **SQLBulkOperations**. Para insertar o actualizar datos largos, una aplicación realiza los pasos siguientes, además de los pasos descritos en las secciones "Realizar inserciones masivas" y "Realizar masiva actualiza utilizar marcadores" anteriormente en este tema.  
  
1.  Cuando enlaza los datos mediante el uso de **SQLBindCol**, la aplicación coloca un valor definido por la aplicación, como el número de columna, en el  *\*TargetValuePtr* búfer de datos en ejecución columnas. El valor se puede usar posteriormente para identificar la columna.  
  
     La aplicación coloca el resultado de la SQL_LEN_DATA_AT_EXEC (*longitud*) macro en el  *\*StrLen_or_IndPtr* búfer. Si el tipo de datos SQL de la columna es SQL_LONGVARBINARY, SQL_LONGVARCHAR o un tipo de datos específicos del origen de datos de tipo long y el controlador devuelve "Y" para el tipo de información SQL_NEED_LONG_DATA_LEN en **SQLGetInfo**, *longitud*  es el número de bytes de datos que se enviarán para el parámetro; en caso contrario, debe ser un valor no negativo y se omite.  
  
2.  Cuando **SQLBulkOperations** se llama, si hay columnas de datos en ejecución, la función devuelve SQL_NEED_DATA y continúa con el paso 3, que sigue. (Si no hay ninguna columna de datos en ejecución, el proceso de es completo).  
  
3.  La aplicación llama a **SQLParamData** para recuperar la dirección de la  *\*TargetValuePtr* búfer para la primera columna de datos en ejecución para procesarse. **SQLParamData** devuelve SQL_NEED_DATA. La aplicación recupera el valor definido por la aplicación desde el  *\*TargetValuePtr* búfer.  
  
    > [!NOTE]  
    >  Aunque los parámetros de datos en ejecución son similares a las columnas de datos en ejecución, el valor devuelto por **SQLParamData** es diferente para cada uno.  
  
     Columnas de datos en ejecución son columnas de un conjunto de filas para el que se enviarán los datos con **SQLPutData** cuando una fila se actualiza o inserta con **SQLBulkOperations**. Se enlazan con **SQLBindCol**. El valor devuelto por **SQLParamData** es la dirección de la fila en el **TargetValuePtr* búfer que se está procesando.  
  
4.  La aplicación llama a **SQLPutData** uno o más veces para enviar datos de la columna. Se necesita más de una llamada si no se puede devolver todos los valores de datos en el  *\*TargetValuePtr* especificado en el búfer **SQLPutData**; varias llamadas a **SQLPutData** para la misma columna se permiten solo al enviar datos de carácter C a una columna con un tipo de carácter, binario o datos específicos del origen de datos o al enviar datos binarios de C a una columna con un carácter, binario, o el tipo de datos específico del origen de datos.  
  
5.  La aplicación llama a **SQLParamData** nuevo para indicar que se han enviado todos los datos de la columna.  
  
    -   Si hay más columnas de datos en ejecución, **SQLParamData** devuelve SQL_NEED_DATA y la dirección de la *TargetValuePtr* búfer para la siguiente columna de datos en ejecución para procesarse. La aplicación repite los pasos 4 y 5.  
  
    -   Si no hay nada más columnas de datos en ejecución, el proceso está completado. Si se ha ejecutado correctamente, la instrucción **SQLParamData** devuelve SQL_SUCCESS o SQL_SUCCESS_WITH_INFO; si se produjo un error en la ejecución, devuelve SQL_ERROR. En este momento, **SQLParamData** puede devolver cualquier SQLSTATE, que puede devolver **SQLBulkOperations**.  
  
 Si se cancela la operación o se produce un error en **SQLParamData** o **SQLPutData** después **SQLBulkOperations** devuelve SQL_NEED_DATA y antes de enviar los datos para todos columnas de datos en ejecución, la aplicación puede llamar solo **SQLCancel**, **SQLGetDiagField**, **SQLGetDiagRec**, **SQLGetFunctions** , **SQLParamData**, o **SQLPutData** para la instrucción o la conexión asociada con la instrucción. Si llama a cualquier otra función para la instrucción o la conexión asociada con la instrucción, la función devuelve SQL_ERROR y SQLSTATE HY010 (función de error de secuencia).  
  
 Si la aplicación llama a **SQLCancel** mientras el controlador sigue necesitando los datos para las columnas de datos en ejecución, el controlador cancela la operación. A continuación, puede llamar la aplicación **SQLBulkOperations** nuevo; Cancelar no afecta el estado del cursor o la posición actual del cursor.  
  
## <a name="row-status-array"></a>Matriz de Estados de fila  
 La matriz de Estados de fila contiene valores de estado para cada fila de datos en el conjunto de filas después de llamar a **SQLBulkOperations**. El controlador establece los valores de estado de esta matriz después de llamar a **SQLFetch**, **SQLFetchScroll**, **SQLSetPos**, o **SQLBulkOperations** . Esta matriz inicialmente se rellena mediante una llamada a **SQLBulkOperations** si **SQLFetch** o **SQLFetchScroll** no se ha llamado antes de **SQLBulkOperations** . El atributo de instrucción SQL_ATTR_ROW_STATUS_PTR apunta a esta matriz. El número de elementos de las matrices de estado de fila debe ser igual el número de filas del conjunto de filas (tal y como se define por el atributo de instrucción SQL_ATTR_ROW_ARRAY_SIZE). Para obtener información acerca de esta matriz de estado de fila, vea [SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md).  
  
## <a name="code-example"></a>Ejemplo de código  
 En el ejemplo siguiente se recupera 10 filas de datos en un momento de la tabla Customers. A continuación, se pide al usuario tomar una acción. Para reducir el tráfico de red, el búfer en el ejemplo actualiza, elimina e inserta localmente en las matrices enlazadas, pero en los desplazamientos más allá de los datos del conjunto de filas. Cuando el usuario elige enviar las actualizaciones, eliminaciones y se inserta en el origen de datos, el código establece el enlace de desplazamiento de forma adecuada y llama a **SQLBulkOperations**. Por motivos de simplicidad, el usuario no se puede almacenar en búfer más de 10 actualizaciones, eliminaciones o inserciones.  
  
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
  
|Para obtener información acerca de|Vea|  
|---------------------------|---------|  
|Enlazar un búfer con una columna en un conjunto de resultados|[Función SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Procesamiento de una instrucción de cancelación|[Función SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Obtención de un bloque de datos o desplazarse a través de un resultado de conjunto|[Función SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|Obtención de un único campo de un descriptor|[Función SQLGetDescField](../../../odbc/reference/syntax/sqlgetdescfield-function.md)|  
|Introducción a varios campos de descriptor|[Función SQLGetDescRec](../../../odbc/reference/syntax/sqlgetdescrec-function.md)|  
|Configuración de un único campo de un descriptor|[Función SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)|  
|Configuración de varios campos de descriptor|[Función SQLSetDescRec](../../../odbc/reference/syntax/sqlsetdescrec-function.md)|  
|Sitúe el cursor, actualizar los datos en el conjunto de filas, o actualizar o eliminar datos en el conjunto de filas|[Función SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md)|  
|Establecer un atributo de instrucción|[Función SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>Vea también  
 [Referencia de la API de ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Archivos de encabezado de ODBC](../../../odbc/reference/install/odbc-header-files.md)
