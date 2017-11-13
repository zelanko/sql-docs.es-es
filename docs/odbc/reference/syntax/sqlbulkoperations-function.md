---
title: "Función SQLBulkOperations | Documentos de Microsoft"
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
- SQLBulkOperations
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLBulkOperations
helpviewer_keywords:
- SQLBulkOperations function [ODBC]
ms.assetid: 7029d0da-b0f2-44e6-9114-50bd96f47196
caps.latest.revision: 24
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: ea439a41a6a3d42c9266bbccfe53aace1c0f37f4
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="sqlbulkoperations-function"></a>Función SQLBulkOperations
**Conformidad**  
 Versión introdujo: ODBC 3.0 normativas: ODBC  
  
 **Resumen**  
 **SQLBulkOperations** realiza inserciones masivas y marcador de forma masiva las operaciones, incluida la actualización, eliminar y capturar por marcador.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
SQLRETURN SQLBulkOperations(  
     SQLHSTMT       StatementHandle,  
     SQLUSMALLINT   Operation);  
```  
  
## <a name="arguments"></a>Argumentos  
 *StatementHandle*  
 [Entrada] Identificador de instrucción.  
  
 *Operación*  
 [Entrada] Operación que se realiza:  
  
 SQL_ADD SQL_UPDATE_BY_BOOKMARK SQL_DELETE_BY_BOOKMARK SQL_FETCH_BY_BOOKMARK  
  
 Para obtener más información, vea "Comentarios".  
  
## <a name="returns"></a>Devuelve  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NEED_DATA, SQL_STILL_EXECUTING, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Cuando **SQLBulkOperations** devuelve SQL_ERROR o SQL_SUCCESS_WITH_INFO, un valor SQLSTATE asociado se puede obtener mediante una llamada a **SQLGetDiagRec** con un *HandleType* de SQL_HANDLE_STMT y un *controlar* de *StatementHandle*. En la tabla siguiente se enumera los valores SQLSTATE suelen ser devueltos por **SQLBulkOperations** y se explica cada uno de ellos en el contexto de esta función; la notación "(DM)" precede a las descripciones de SQLSTATE devuelto por el Administrador de controladores . El código de retorno asociado a cada valor SQLSTATE es SQL_ERROR, a menos que se indique lo contrario.  
  
 Para todas esa SQLSTATE que puede devolver SQL_SUCCESS_WITH_INFO o SQL_ERROR (excepto 01xxx SQLSTATEs), se devuelve SQL_SUCCESS_WITH_INFO, si se produce un error en uno o más, pero no todas las filas de una operación de inserción y se devuelve SQL_ERROR si se produce un error en un operación de varias filas.  
  
|SQLSTATE|Error|Description|  
|--------------|-----------|-----------------|  
|01000|Advertencia general|Mensaje informativo de específicas del controlador. (La función devuelve SQL_SUCCESS_WITH_INFO).|  
|01004|Cadena datos truncados por la derecha|El *operación* argumento era SQL_FETCH_BY_BOOKMARK y cadena o datos binarios devueltos para una o varias columnas con un tipo de datos SQL_C_CHAR o SQL_C_BINARY dio como resultado el truncamiento de carácter que no esté vacía o datos binarios no NULL.|  
|01S01|Error en la fila|El *operación* argumento era SQL_ADD y se produjo un error en una o varias filas al realizar la operación, pero se ha agregado correctamente al menos una fila. (La función devuelve SQL_SUCCESS_WITH_INFO).<br /><br /> (Este error se genera cuando una aplicación está trabajando con una API ODBC 2. *x* controlador.)|  
|01S07|Truncamiento fraccionario|El *operación* argumento era SQL_FETCH_BY_BOOKMARK, el tipo de datos del búfer de aplicación no era SQL_C_CHAR o SQL_C_BINARY y se truncaron los datos devueltos a los búferes de la aplicación para una o varias columnas. (Para los tipos de datos numéricos de C, se trunca la parte fraccionaria del número. De hora, marca de tiempo y los tipos de datos de intervalo C que contienen un componente de tiempo, la parte fraccionaria del tiempo se truncó).<br /><br /> (La función devuelve SQL_SUCCESS_WITH_INFO).|  
|07006|Infracción del atributo de tipo de datos restringido|El *operación* argumento era SQL_FETCH_BY_BOOKMARK y no se pudo convertir el valor de datos de una columna del conjunto de resultados para el tipo de datos especificado por la *TargetType* argumento en la llamada a **SQLBindCol**.<br /><br /> El *operación* argumento era SQL_UPDATE_BY_BOOKMARK o SQL_ADD y el valor de datos en los búferes de la aplicación no se pudo convertir al tipo de datos de una columna del conjunto de resultados.|  
|07009|Índice de descriptor no válido|El argumento *operación* era SQL_ADD y enlazar con un número de columna mayor que el número de columnas del conjunto de resultados.|  
|21S02|Grado de la tabla derivada no coincide con la lista de columnas|El argumento *operación* SQL_UPDATE_BY_BOOKMARK; y no hay columnas actualizables porque todas las columnas son independientes o de solo lectura, o el valor en el búfer de longitud/indicador enlazado era SQL_COLUMN_IGNORE.|  
|22001|Cadena datos truncados por la derecha|La asignación de un carácter o un valor binario a una columna del conjunto de resultados que se generó el truncamiento de no están en blanco (para los caracteres) o null (para el binario) caracteres o bytes.|  
|22003|Valor numérico fuera del intervalo|El *operación* argumento era SQL_ADD o SQL_UPDATE_BY_BOOKMARK y la asignación de un valor numérico a una columna del conjunto de resultados ocasiona la parte entera (en lugar de fracciones) del número se trunque.<br /><br /> El argumento *operación* era SQL_FETCH_BY_BOOKMARK y devolver el valor numérico de una o varias columnas enlazadas provocaría una pérdida de dígitos significativos.|  
|22007|Formato de datetime no válido|El *operación* argumento era SQL_ADD o SQL_UPDATE_BY_BOOKMARK y la asignación de un valor date o timestamp a una columna del conjunto de resultados que produjo el año, mes o día para estar fuera del intervalo.<br /><br /> El argumento *operación* era SQL_FETCH_BY_BOOKMARK y devolver el valor de fecha o marca de tiempo para una o varias columnas enlazadas habría provocado el año, mes o día para estar fuera del intervalo.|  
|22008|Desbordamiento del campo de fecha y hora|El *operación* argumento era SQL_ADD o SQL_UPDATE_BY_BOOKMARK y el rendimiento de fecha y hora aritmético en datos que se envían a una columna del conjunto de resultados que se generó en un campo de fecha y hora (el año, mes, día, hora, minuto o segundo campo) del resultado comprendidas fuera del intervalo válido de valores para el campo o no sea válido basándose en las reglas en natural para fechas y horas del calendario gregoriano.<br /><br /> El *operación* argumento era SQL_FETCH_BY_BOOKMARK y el rendimiento de fecha y hora aritmético en los datos recuperados del conjunto de resultados que se generó en un campo de fecha y hora (año, mes, día, hora, minuto o segundo campo) de la resultado comprendidas fuera del intervalo válido de valores para el campo o no es válido según reglas naturales del calendario gregoriano de fechas y horas.|  
|22015|Desbordamiento del campo de intervalo|El *operación* argumento era SQL_ADD o SQL_UPDATE_BY_BOOKMARK y la asignación de un valor numérico exacto o el tipo de intervalo C a un intervalo del tipo de datos SQL causó una pérdida de dígitos significativos.<br /><br /> El *operación* argumento era SQL_ADD o SQL_UPDATE_BY_BOOKMARK; cuando se asigna a un intervalo de tipo SQL, no había ninguna representación del valor del tipo de C en el intervalo de tipo SQL.<br /><br /> El *operación* argumento era SQL_FETCH_BY_BOOKMARK y asignación de un valor numérico exacto o el intervalo de tipo SQL a un tipo de intervalo C causó una pérdida de dígitos significativos en el campo inicial.<br /><br /> El *operación* argumento era SQL_FETCH_BY_BOOKMARK; cuando se asigna a un tipo de intervalo C, no había ninguna representación del valor del tipo de SQL en el tipo de intervalo C.|  
|22018|Valor de carácter no válido para especificación cast|El *operación* argumento era SQL_FETCH_BY_BOOKMARK; el tipo C era un numérico exacto o aproximado, una fecha y hora o un tipo de datos del intervalo; el tipo SQL de la columna era un tipo de datos character; y el valor de la columna no era válido literal de tipo C enlazado.<br /><br /> El argumento *operación* fue SQL_ADD o SQL_UPDATE_BY_BOOKMARK; el tipo SQL era un numérico exacto o aproximado, una fecha y hora o un tipo de datos del intervalo; el tipo C era SQL_C_CHAR; y el valor de la columna no es un literal válido de la enlazar el tipo SQL.|  
|23000|Infracción de restricción de integridad|El *operación* argumento era SQL_ADD, SQL_DELETE_BY_BOOKMARK o SQL_UPDATE_BY_BOOKMARK y se ha infringido una restricción de integridad.<br /><br /> El *operación* argumento era SQL_ADD y una columna que no se enlazó se define como no NULL y no tiene valor predeterminado.<br /><br /> El *operación* argumento era SQL_ADD, la longitud especificada en el límite *StrLen_or_IndPtr* búfer era SQL_COLUMN_IGNORE y la columna no tenía un valor predeterminado.|  
|24000|Estado de cursor no válido|El *StatementHandle* estaba en un estado ejecutado, pero ningún conjunto de resultados se asoció el *StatementHandle*.|  
|40001|Error de serialización.|La transacción se revirtió debido a un interbloqueo de recurso con otra transacción.|  
|40003|Finalización de instrucciones desconocida|Error en la conexión asociada durante la ejecución de esta función, y no se puede determinar el estado de la transacción.|  
|42000|Error de sintaxis, infracción de acceso|El controlador no pudo bloquear la fila según sea necesario para realizar la operación solicitada en el *operación* argumento.|  
|44000|Infracción de WITH CHECK OPTION|El *operación* argumento era SQL_ADD o SQL_UPDATE_BY_BOOKMARK y la inserción o actualización se realizó en una tabla vista (o una tabla derivada de la tabla mostrada) que se creó mediante la especificación de **WITH CHECK OPTION**, de tal manera que una o varias filas afectadas por la inserción o actualización ya no estará presente en la tabla mostrada.|  
|HY000|Error general|Se produjo un error para que no hubo ninguna SQLSTATE específico y para el que se ha definido ningún SQLSTATE específico de la implementación. El mensaje de error devuelto por **SQLGetDiagRec** en el  *\*MessageText* búfer describe el error y su causa.|  
|HY001|Error de asignación de memoria|El controlador no pudo asignar la memoria necesaria para admitir la ejecución o la finalización de la función.|  
|HY008|Operación cancelada|Procesamiento asincrónico se habilitó para la *StatementHandle*. Se llamó a la función y antes que completó la ejecución, **SQLCancel** o **SQLCancelHandle** se llamó en la *StatementHandle*. A continuación, se llama a la función nuevo en el *StatementHandle*.<br /><br /> Se llamó a la función y antes que completó la ejecución, **SQLCancel** o **SQLCancelHandle** se llamó en la *StatementHandle* desde un subproceso distinto en un aplicaciones multiproceso.|  
|HY010|Error de secuencia de función|(DM) se llamó a una función ejecuta de forma asincrónica para el identificador de conexión que está asociado el *StatementHandle*. Esta función asincrónica aún estaba ejecutando cuando el **SQLBulkOperations** se llamó la función.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, o **SQLMoreResults** se llamó para el *StatementHandle* devolvió SQL_PARAM_DATA_ ESTÁ DISPONIBLE. Esta función se invoca antes de que se recuperan los datos para todos los parámetros transmitidos.<br /><br /> (DM) especificado *StatementHandle* no estaba en un estado ejecutado. Se llamó a la función sin antes de llamar a **SQLExecDirect**, **SQLExecute**, o una función de catálogo.<br /><br /> (DM) se llamó a una función ejecuta de forma asincrónica (no esta uno) para la *StatementHandle* y aún se estaba ejecutando cuando se llamó a esta función.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, o **SQLSetPos** se llamó para el *StatementHandle* y devuelve SQL_NEED_DATA. Esta función se invoca antes de que se enviaron los datos para todas las columnas o parámetros de datos en ejecución.<br /><br /> (DM) el controlador fue un 2 de ODBC. *x* controlador, y **SQLBulkOperations** se piden un *StatementHandle* antes de **SQLFetchScroll** o **SQLFetch**  se llamó.<br /><br /> (DM) **SQLBulkOperations** se llama después de **SQLExtendedFetch** se llamó en la *StatementHandle*.|  
|HY011|Atributo no se puede establecer ahora|(DM) el controlador fue un 2 de ODBC. *x* controlador y el atributo de instrucción SQL_ATTR_ROW_STATUS_PTR se establecen entre las llamadas a **SQLFetch** o **SQLFetchScroll** y **SQLBulkOperations** .|  
|HY013|Error de administración de memoria|No se pudo procesar la llamada de función porque los objetos subyacentes de la memoria no se pudieron tener acceso, posiblemente debido a condiciones de memoria insuficiente.|  
|HY090|Longitud de búfer o cadena no válida|El *operación* argumento era SQL_ADD o SQL_UPDATE_BY_BOOKMARK; un valor de datos no era un puntero nulo; el tipo de datos de C se SQL_C_BINARY o SQL_C_CHAR; y el valor de longitud de columna era menor que 0, pero no es igual a SQL_DATA_AT_EXEC , SQL_COLUMN_IGNORE, SQL_NTS o SQL_NULL_DATA, o menor o igual que SQL_LEN_DATA_AT_EXEC_OFFSET.<br /><br /> El valor en un búfer de longitud/indicador era SQL_DATA_AT_EXEC; el tipo SQL era SQL_LONGVARCHAR, SQL_LONGVARBINARY o un tipo de datos específicos del origen de datos largos; y el tipo de información de SQL_NEED_LONG_DATA_LEN **SQLGetInfo** era "Y".<br /><br /> El *operación* argumento era SQL_ADD, el atributo de instrucción SQL_ATTR_USE_BOOKMARK se estableció en SQL_UB_VARIABLE y columna 0 se enlaza a un búfer cuya longitud no era igual a la longitud máxima de marcador para este conjunto de resultados. (Este valor de longitud está disponible en el campo SQL_DESC_OCTET_LENGTH de IRD y puede obtenerse mediante una llamada a **SQLDescribeCol**, **SQLColAttribute**, o **SQLGetDescField**.)|  
|HY092|Identificador de atributo no válido|(DM) el valor especificado para la *operación* argumento no era válido.<br /><br /> El *operación* argumento era SQL_ADD, SQL_UPDATE_BY_BOOKMARK o SQL_DELETE_BY_BOOKMARK y se estableció el atributo de instrucción SQL_ATTR_CONCURRENCY en SQL_CONCUR_READ_ONLY.<br /><br /> El *operación* argumento era SQL_DELETE_BY_BOOKMARK, SQL_FETCH_BY_BOOKMARK o SQL_UPDATE_BY_BOOKMARK y no se ha enlazado la columna de marcador o el atributo de instrucción SQL_ATTR_USE_BOOKMARKS se estableció en SQL_UB_OFF.|  
|HY117|Se suspende la conexión debido al estado de transacción desconocido. Solo se desconecte y se permiten las funciones de solo lectura.|(DM) para obtener más información sobre el estado suspendido, consulte [función SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Característica opcional no implementada|El controlador u origen de datos no admite la operación solicitada en el *operación* argumento.|  
|HYT00|Se agotó el tiempo de espera|El período de tiempo de espera de consulta finalizó antes de que el origen de datos devuelve el conjunto de resultados. El período de tiempo de espera se establece a través de **SQLSetStmtAttr** con una *atributo* argumento de SQL_ATTR_QUERY_TIMEOUT.|  
|HYT01|Tiempo de espera de conexión expirado|El período de tiempo de espera de conexión finalizó antes de que el origen de datos se respondió a la solicitud. El período de tiempo de espera de conexión se establece a través de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Controlador no admite esta función|(DM) el controlador asociado a la *StatementHandle* no admite la función.|  
|IM017|Sondeo está deshabilitado en el modo de notificación asincrónica|Cada vez que se utiliza el modelo de notificación, se deshabilita el sondeo.|  
|IM018|**SQLCompleteAsync** no se ha llamado para completar la operación asincrónica anterior en este identificador.|Si la llamada de función anterior en el controlador devuelve SQL_STILL_EXECUTING y si está habilitado el modo de notificación, **SQLCompleteAsync** se debe llamar en el identificador para realizar el procesamiento posterior a la y completar la operación.|  
  
## <a name="comments"></a>Comentarios  
  
> [!CAUTION]  
>  Para obtener información sobre qué instrucción indica **SQLBulkOperations** puede llamarse y lo que debe hacer para ofrecer compatibilidad con ODBC 2. *x* las aplicaciones, vea el [compatibilidad con versiones anteriores, los cursores desplazables y cursores de bloque](../../../odbc/reference/appendixes/block-cursors-scrollable-cursors-and-backward-compatibility.md) sección en Apéndice G: controlador directrices para la compatibilidad con versiones anteriores.  
  
 Una aplicación usa **SQLBulkOperations** para realizar las siguientes operaciones en la tabla base o vista que corresponde a la consulta actual:  
  
-   Agregar nuevas filas.  
  
-   Actualizar un conjunto de filas donde cada fila se identifica mediante un marcador.  
  
-   Eliminar un conjunto de filas donde cada fila se identifica mediante un marcador.  
  
-   Capturar un conjunto de filas donde cada fila se identifica mediante un marcador.  
  
 Después de llamar a **SQLBulkOperations**, la posición del cursor de bloque es indefinida. La aplicación tiene que llamar a **SQLFetchScroll** para establecer la posición del cursor. Una aplicación debe llamar a **SQLFetchScroll** sólo con una *FetchOrientation* argumento de SQL_FETCH_FIRST, SQL_FETCH_LAST, SQL_FETCH_ABSOLUTE o SQL_FETCH_BOOKMARK. La posición del cursor se define si la aplicación llama a **SQLFetch** o **SQLFetchScroll** con un *FetchOrientation* argumento de SQL_FETCH_PRIOR, SQL_FETCH_NEXT, o SQL_FETCH_RELATIVE.  
  
 Puede hacer caso omiso de una columna en operaciones masivas realizadas mediante una llamada a **SQLBulkOperations** estableciendo el búfer de longitud/indicador de columna especificado en la llamada a **SQLBindCol**, para SQL_COLUMN_IGNORE.  
  
 No es necesario para la aplicación establecer el atributo de instrucción SQL_ATTR_ROW_OPERATION_PTR cuando llama a **SQLBulkOperations** porque no se puede omitir filas al realizar operaciones masivas con esta función.  
  
 El búfer señalado por el atributo de instrucción SQL_ATTR_ROWS_FETCHED_PTR contiene el número de filas afectadas por una llamada a **SQLBulkOperations**.  
  
 Cuando el *operación* argumento es SQL_ADD o SQL_UPDATE_BY_BOOKMARK y la lista de selección de la especificación de consulta asociada con el cursor contiene más de una referencia a la misma columna, es definido por el controlador si un error se genera o el controlador pasa por alto las referencias duplicadas y realiza las operaciones solicitadas.  
  
 Para obtener más información sobre cómo usar **SQLBulkOperations**, consulte [actualizar los datos con SQLBulkOperations](../../../odbc/reference/develop-app/updating-data-with-sqlbulkoperations.md).  
  
## <a name="performing-bulk-inserts"></a>Ejecute inserciones masivas  
 Para insertar datos con **SQLBulkOperations**, una aplicación realiza la siguiente secuencia de pasos:  
  
1.  Ejecuta una consulta que devuelve un conjunto de resultados.  
  
2.  Establece el atributo de instrucción SQL_ATTR_ROW_ARRAY_SIZE en el número de filas que se va a insertar.  
  
3.  Llamadas **SQLBindCol** para enlazar los datos que se va a insertar. Los datos se enlazan a una matriz cuyo tamaño es igual que el valor de SQL_ATTR_ROW_ARRAY_SIZE.  
  
    > [!NOTE]  
    >  El tamaño de la matriz señalada por el atributo de instrucción de SQL_ATTR_ROW_STATUS_PTR debe ser igual a SQL_ATTR_ROW_ARRAY_SIZE o SQL_ATTR_ROW_STATUS_PTR debe ser un puntero nulo.  
  
4.  Llamadas **SQLBulkOperations**(*StatementHandle,* SQL_ADD) para realizar la inserción.  
  
5.  Si la aplicación ha establecido el atributo de instrucción de SQL_ATTR_ROW_STATUS_PTR, puede inspeccionar esta matriz para ver el resultado de la operación.  
  
 Si una aplicación enlaza la columna 0 antes de llamar a **SQLBulkOperations** con una *operación* argumento de SQL_ADD, el controlador actualizará los búferes de columna enlazada 0 con los valores de marcador para el recién fila insertada. Esto sucede, la aplicación debe estableciste el atributo de instrucción de SQL_ATTR_USE_BOOKMARKS a SQL_UB_VARIABLE antes de ejecutar la instrucción. (Esto no funciona con una API ODBC 2. *x* controlador.)  
  
 SQLBulkOperations, pueden agregar en elementos de datos de tipo Long mediante llamadas a SQLParamData y SQLPutData. Para obtener más información, vea "Proporcionar largo datos para Bulk Inserts y Updates" más adelante en esta referencia de función.  
  
 No es necesario para la aplicación llamar a **SQLFetch** o **SQLFetchScroll** antes de llamar a **SQLBulkOperations** (excepto cuando va en una API ODBC 2. *x* controlador; vea [compatibilidad con versiones anteriores y el cumplimiento de estándares](../../../odbc/reference/develop-app/backward-compatibility-and-standards-compliance.md)).  
  
 El comportamiento es definidos por el controlador si **SQLBulkOperations**, con un *operación* argumento de SQL_ADD, se llama en un cursor que contiene las columnas duplicadas. El controlador puede devolver un valor de SQLSTATE definidos por el controlador, agregue los datos a la primera columna que aparece en el resultado de establecer o realizan otros comportamientos definidos por el controlador.  
  
## <a name="performing-bulk-updates-by-using-bookmarks"></a>Realizar actualizaciones masivas mediante marcadores  
 Para realizar actualizaciones masivas mediante el uso de marcadores con **SQLBulkOperations**, una aplicación realiza los siguientes pasos de secuencia:  
  
1.  Establece el atributo de instrucción de SQL_ATTR_USE_BOOKMARKS a SQL_UB_VARIABLE.  
  
2.  Ejecuta una consulta que devuelve un conjunto de resultados.  
  
3.  Establece el atributo de instrucción SQL_ATTR_ROW_ARRAY_SIZE en el número de filas que se va a actualizar.  
  
4.  Llamadas **SQLBindCol** para enlazar los datos que se va a actualizar. Los datos se enlazan a una matriz cuyo tamaño es igual que el valor de SQL_ATTR_ROW_ARRAY_SIZE. También se llama **SQLBindCol** para enlazar la columna 0 (la columna de marcador).  
  
5.  Copias los marcadores para las filas que está interesado en la actualización en la matriz enlazado a la columna 0.  
  
6.  Actualiza los datos de los búferes de enlazado.  
  
    > [!NOTE]  
    >  El tamaño de la matriz señalada por el atributo de instrucción de SQL_ATTR_ROW_STATUS_PTR debe ser igual a SQL_ATTR_ROW_ARRAY_SIZE o SQL_ATTR_ROW_STATUS_PTR debe ser un puntero nulo.  
  
7.  Llamadas **SQLBulkOperations**(*StatementHandle,* SQL_UPDATE_BY_BOOKMARK).  
  
    > [!NOTE]  
    >  Si la aplicación ha establecido el atributo de instrucción de SQL_ATTR_ROW_STATUS_PTR, puede inspeccionar esta matriz para ver el resultado de la operación.  
  
8.  Opcionalmente, se llama **SQLBulkOperations**(*StatementHandle*, SQL_FETCH_BY_BOOKMARK) para capturar los datos en los búferes de aplicación enlazadas para comprobar que la actualización se ha producido.  
  
9. Si se han actualizado los datos, el controlador cambia el valor de la matriz de estado de fila para las filas correspondientes a SQL_ROW_UPDATED.  
  
 Las actualizaciones realizadas por forma masiva **SQLBulkOperations** puede incluir datos de tipo long mediante llamadas a **SQLParamData** y **SQLPutData**. Para obtener más información, vea "Proporcionar largo datos para Bulk Inserts y Updates" más adelante en esta referencia de función.  
  
 Si los marcadores son persistentes a través de los cursores, la aplicación no necesita llamar a **SQLFetch** o **SQLFetchScroll** antes de actualizar por marcadores. Puede usar los marcadores que haya almacenado de un cursor anterior. Si los marcadores no son persistentes en los cursores, la aplicación tiene que llamar a **SQLFetch** o **SQLFetchScroll** para recuperar los marcadores.  
  
 El comportamiento es definidos por el controlador si **SQLBulkOperations**, con un *operación* argumento de SQL_UPDATE_BY_BOOKMARK, se llama en un cursor que contiene las columnas duplicadas. El controlador puede devolver un valor de SQLSTATE definidos por el controlador, actualizar la primera columna que aparece en el conjunto de resultados o realizar otros comportamientos definidos por el controlador.  
  
## <a name="performing-bulk-fetches-using-bookmarks"></a>Realizar masiva captura mediante marcadores  
 Para realizar capturas de forma masiva mediante marcadores con **SQLBulkOperations**, una aplicación realiza los siguientes pasos de secuencia:  
  
1.  Establece el atributo de instrucción de SQL_ATTR_USE_BOOKMARKS a SQL_UB_VARIABLE.  
  
2.  Ejecuta una consulta que devuelve un conjunto de resultados.  
  
3.  Establece el atributo de instrucción SQL_ATTR_ROW_ARRAY_SIZE en el número de filas que se va a capturar.  
  
4.  Llamadas **SQLBindCol** para enlazar los datos que se va a capturar. Los datos se enlazan a una matriz cuyo tamaño es igual que el valor de SQL_ATTR_ROW_ARRAY_SIZE. También se llama **SQLBindCol** para enlazar la columna 0 (la columna de marcador).  
  
5.  Copias los marcadores para las filas que está interesado en Buscar en la matriz enlazado a la columna 0. (Esto supone que la aplicación ya ha obtenido los marcadores por separado).  
  
    > [!NOTE]  
    >  El tamaño de la matriz señalada por el atributo de instrucción de SQL_ATTR_ROW_STATUS_PTR debe ser igual a SQL_ATTR_ROW_ARRAY_SIZE o SQL_ATTR_ROW_STATUS_PTR debe ser un puntero nulo.  
  
6.  Llamadas **SQLBulkOperations**(*StatementHandle,* SQL_FETCH_BY_BOOKMARK).  
  
7.  Si la aplicación ha establecido el atributo de instrucción de SQL_ATTR_ROW_STATUS_PTR, puede inspeccionar esta matriz para ver el resultado de la operación.  
  
 Si los marcadores son persistentes a través de los cursores, la aplicación no necesita llamar a **SQLFetch** o **SQLFetchScroll** antes de capturar los marcadores. Puede usar los marcadores que haya almacenado de un cursor anterior. Si los marcadores no son persistentes en los cursores, la aplicación tiene que llamar a **SQLFetch** o **SQLFetchScroll** una vez para recuperar los marcadores.  
  
## <a name="performing-bulk-deletes-using-bookmarks"></a>Realizar masiva elimina mediante marcadores  
 Para cuando realice eliminaciones masivas mediante marcadores con **SQLBulkOperations**, una aplicación realiza los siguientes pasos de secuencia:  
  
1.  Establece el atributo de instrucción de SQL_ATTR_USE_BOOKMARKS a SQL_UB_VARIABLE.  
  
2.  Ejecuta una consulta que devuelve un conjunto de resultados.  
  
3.  Establece el atributo de instrucción SQL_ATTR_ROW_ARRAY_SIZE en el número de filas que se va a eliminar.  
  
4.  Llamadas **SQLBindCol** para enlazar la columna 0 (la columna de marcador).  
  
5.  Copias los marcadores para las filas que está interesado en Eliminar en la matriz enlazado a la columna 0.  
  
    > [!NOTE]  
    >  El tamaño de la matriz señalada por el atributo de instrucción de SQL_ATTR_ROW_STATUS_PTR debe ser igual a SQL_ATTR_ROW_ARRAY_SIZE o SQL_ATTR_ROW_STATUS_PTR debe ser un puntero nulo.  
  
6.  Llamadas **SQLBulkOperations**(*StatementHandle,* SQL_DELETE_BY_BOOKMARK).  
  
7.  Si la aplicación ha establecido el atributo de instrucción de SQL_ATTR_ROW_STATUS_PTR, puede inspeccionar esta matriz para ver el resultado de la operación.  
  
 Si los marcadores son persistentes a través de los cursores, la aplicación no deba llamar **SQLFetch** o **SQLFetchScroll** antes de eliminar por marcadores. Puede usar los marcadores que haya almacenado de un cursor anterior. Si los marcadores no son persistentes en los cursores, la aplicación tiene que llamar a **SQLFetch** o **SQLFetchScroll** una vez para recuperar los marcadores.  
  
## <a name="providing-long-data-for-bulk-inserts-and-updates"></a>Proporciona datos de tipo Long de actualizaciones e inserciones masivas  
 Pueden proporcionar datos de tipo Long para inserciones masivas y actualizaciones realizadas por las llamadas a **SQLBulkOperations**. Para insertar o actualizar datos largos, una aplicación realiza los pasos siguientes además de los pasos descritos en las secciones "Realizar masiva actualiza Using Bookmarks" y "Realizar inserción masiva" anteriormente en este tema.  
  
1.  Cuando enlazan los datos mediante **SQLBindCol**, la aplicación coloca un valor definido por la aplicación, como el número de columna, en la  *\*TargetValuePtr* búfer de datos en ejecución columnas. El valor se puede usar posteriormente para identificar la columna.  
  
     La aplicación coloca el resultado de la SQL_LEN_DATA_AT_EXEC (*longitud*) macro en el  *\*StrLen_or_IndPtr* búfer. Si el tipo de datos SQL de la columna es SQL_LONGVARBINARY, SQL_LONGVARCHAR o un tipo de datos específico del origen de datos de tipo long y el controlador devuelve "Y" para el tipo de información de SQL_NEED_LONG_DATA_LEN en **SQLGetInfo**, *longitud*  es el número de bytes de datos que se envía para el parámetro; en caso contrario, debe ser un valor no negativo y se omite.  
  
2.  Cuando **SQLBulkOperations** se llama, si hay columnas de datos en ejecución, la función devuelve SQL_NEED_DATA y continúa con el paso 3, que sigue. (Si no hay ninguna columna de datos en ejecución, el proceso es completo).  
  
3.  La aplicación llama **SQLParamData** para recuperar la dirección de la  *\*TargetValuePtr* búfer para la primera columna de datos en ejecución para procesarse. **SQLParamData** devuelve SQL_NEED_DATA. La aplicación recupera el valor definido por la aplicación desde el  *\*TargetValuePtr* búfer.  
  
    > [!NOTE]  
    >  Aunque los parámetros de datos en ejecución son similares a las columnas de datos en ejecución, el valor devuelto por **SQLParamData** es diferente para cada uno de ellos.  
  
     Columnas de datos en ejecución son columnas de un conjunto de filas para el que los datos se envían con **SQLPutData** cuando una fila se actualiza o inserta con **SQLBulkOperations**. Que están enlazados con **SQLBindCol**. El valor devuelto por **SQLParamData** es la dirección de la fila en el **TargetValuePtr* búfer que se está procesando.  
  
4.  La aplicación llama **SQLPutData** una o más veces para enviar datos de la columna. Se necesita más de una llamada si no se puede devolver el valor de datos en el  *\*TargetValuePtr* especificado en el búfer **SQLPutData**; varias llamadas a **SQLPutData** para la misma columna se permiten solo cuando se envían datos de carácter C a una columna con un tipo de datos de específico del origen de datos, binarios o caracteres o al enviar datos binarios de C a una columna con un carácter, binario, o de tipo de datos específico del origen de datos.  
  
5.  La aplicación llama **SQLParamData** nuevo para indicar que se han enviado todos los datos de la columna.  
  
    -   Si hay más columnas de datos en ejecución, **SQLParamData** devuelve SQL_NEED_DATA y la dirección de la *TargetValuePtr* búfer de la columna de datos en ejecución siguiente para procesarse. La aplicación repite los pasos 4 y 5.  
  
    -   Si no hay nada más columnas de datos en ejecución, el proceso es completando. Si la instrucción se ejecutó correctamente, **SQLParamData** devuelve SQL_SUCCESS o SQL_SUCCESS_WITH_INFO; si se produce un error en la ejecución, devuelve SQL_ERROR. En este momento, **SQLParamData** puede devolver cualquier SQLSTATE, que puede ser devueltos por **SQLBulkOperations**.  
  
 Si se cancela la operación o se produce un error en **SQLParamData** o **SQLPutData** después **SQLBulkOperations** devuelve SQL_NEED_DATA y antes de enviar datos para todas las columnas de datos en ejecución, la aplicación puede llamar a solo **SQLCancel**, **SQLGetDiagField**, **SQLGetDiagRec**, **SQLGetFunctions** , **SQLParamData**, o **SQLPutData** para la instrucción o la conexión asociada con la instrucción. Si cualquier otra función llama a la instrucción o la conexión asociada con la instrucción, la función devuelve SQL_ERROR y SQLSTATE HY010 (error de secuencia de función).  
  
 Si la aplicación llama **SQLCancel** mientras el controlador todavía necesita datos para las columnas de datos en ejecución, el controlador cancela la operación. A continuación, puede llamar la aplicación **SQLBulkOperations** nuevo; Cancelar no afecta el estado de cursor o la posición actual del cursor.  
  
## <a name="row-status-array"></a>Matriz de Estados de fila  
 La matriz de Estados de fila contiene valores de estado para cada fila de datos en el conjunto de filas después de llamar a **SQLBulkOperations**. El controlador establece los valores de estado de esta matriz después de llamar a **SQLFetch**, **SQLFetchScroll**, **SQLSetPos**, o **SQLBulkOperations** . Esta matriz se rellena inicialmente con una llamada a **SQLBulkOperations** si **SQLFetch** o **SQLFetchScroll** no se ha llamado antes de **SQLBulkOperations** . El atributo de instrucción SQL_ATTR_ROW_STATUS_PTR apunta a esta matriz. El número de elementos en las matrices de estado de fila debe igual al número de filas del conjunto de filas (tal y como se define por el atributo de instrucción SQL_ATTR_ROW_ARRAY_SIZE). Para obtener información acerca de esta matriz de estado de fila, vea [SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md).  
  
## <a name="code-example"></a>Ejemplo de código  
 En el ejemplo siguiente se obtiene 10 filas de datos a la vez de la tabla Customers. A continuación, pide al usuario una acción a realizar. Para reducir el tráfico de red, el búfer de ejemplo actualización, eliminación e inserta localmente en las matrices enlazadas, pero en los desplazamientos más allá de los datos del conjunto de filas. Cuando el usuario elige enviar las actualizaciones, eliminaciones y se inserta en el origen de datos, el código establece el enlace desplazamiento adecuadamente y llama a **SQLBulkOperations**. Para simplificar, el usuario no se puede almacenar en búfer más de 10 actualizaciones, eliminaciones o inserciones.  
  
```  
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
|Enlazar un búfer con una columna en un conjunto de resultados|[SQLBindCol (función)](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Cancelar el procesamiento de una instrucción|[SQLCancel, función](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Captura un bloque de datos o desplazarse a través de un resultado de conjunto|[SQLFetchScroll, función](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|Obtener un único campo de un descriptor de|[Sqlgetdescfield, función](../../../odbc/reference/syntax/sqlgetdescfield-function.md)|  
|Obtener varios campos de un descriptor de|[Sqlgetdescrec, función](../../../odbc/reference/syntax/sqlgetdescrec-function.md)|  
|Configuración de un único campo de un descriptor de|[Sqlsetdescfield, función](../../../odbc/reference/syntax/sqlsetdescfield-function.md)|  
|Configuración de varios campos de un descriptor de|[Sqlsetdescrec, función](../../../odbc/reference/syntax/sqlsetdescrec-function.md)|  
|Coloque el cursor, actualizar los datos en el conjunto de filas, o actualizar o eliminar datos en el conjunto de filas|[SQLSetPos, función](../../../odbc/reference/syntax/sqlsetpos-function.md)|  
|Establecer un atributo de instrucción|[SQLSetStmtAttr, función](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>Vea también  
 [Referencia de la API de ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Archivos de encabezado de ODBC](../../../odbc/reference/install/odbc-header-files.md)

