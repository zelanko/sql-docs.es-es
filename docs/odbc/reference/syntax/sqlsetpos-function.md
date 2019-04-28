---
title: Función SQLSetPos | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLSetPos
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLSetPos
helpviewer_keywords:
- SQLSetPos function [ODBC]
ms.assetid: 80190ee7-ae3b-45e5-92a9-693eb558f322
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e769949c8c57bbec56055c58c9002494fc6d37be
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62982395"
---
# <a name="sqlsetpos-function"></a>Función SQLSetPos
**Conformidad**  
 Versión de introducción: Cumplimiento de estándares 1.0 de ODBC: ODBC  
  
 **Resumen**  
 **SQLSetPos** establece la posición del cursor en un conjunto de filas y permite que una aplicación para actualizar los datos del conjunto de filas o actualizar o eliminar datos en el conjunto de resultados.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
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
 [Entrada] Posición de la fila del conjunto de filas en el que se va a realizar la operación especificada con el *operación* argumento. Si *RowNumber* es 0, la operación se aplica a todas las filas del conjunto de filas.  
  
 Para obtener más información, vea "Comentarios".  
  
 *Operación*  
 [Entrada] Para realizar la operación:  
  
 SQL_POSITION SQL_REFRESH SQL_UPDATE SQL_DELETE  
  
> [!NOTE]
>  El valor SQL_ADD para el *operación* argumento ha quedado en desuso en ODBC 3 *.x*. ODBC 3. *x* controladores deberá ser compatible con SQL_ADD para compatibilidad con versiones anteriores. Esta funcionalidad se ha reemplazado por una llamada a **SQLBulkOperations** con un *operación* de SQL_ADD. Cuando un ODBC 3. *x* aplicación trabaja con un ODBC 2. *x* controlador, el Administrador de controladores asigna una llamada a **SQLBulkOperations** con un *operación* de SQL_ADD a **SQLSetPos** con un  *Operación* de SQL_ADD.  
  
 Para obtener más información, vea "Comentarios".  
  
 *LockType*  
 [Entrada] Especifica la forma de bloquear la fila después de realizar la operación especificada en el *operación* argumento.  
  
 SQL_LOCK_NO_CHANGE SQL_LOCK_EXCLUSIVE SQL_LOCK_UNLOCK  
  
 Para obtener más información, vea "Comentarios".  
  
 **Devuelve**  
  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NEED_DATA, SQL_STILL_EXECUTING, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Cuando **SQLSetPos** devuelve SQL_ERROR o SQL_SUCCESS_WITH_INFO, un valor SQLSTATE asociado se puede obtener mediante una llamada a **SQLGetDiagRec** con un *HandleType* de SQL_ HANDLE_STMT y un *controlar* de *StatementHandle*. En la tabla siguiente se enumera los valores SQLSTATE devueltos normalmente por **SQLSetPos** y se explica cada uno de ellos en el contexto de esta función; la notación "(DM)" precede a las descripciones de SQLSTATE devuelto por el Administrador de controladores. El código de retorno asociado a cada valor SQLSTATE es SQL_ERROR, a menos que se indique lo contrario.  
  
 Para todas esas SQLSTATE que puede devolver SQL_SUCCESS_WITH_INFO o SQL_ERROR (excepto 01xxx SQLSTATEs), se devuelve SQL_SUCCESS_WITH_INFO, si se produce un error en uno o más, pero no todas las filas de una operación de varias filas, y se devuelve SQL_ERROR si se produce un error en un fila única operación.  
  
|SQLSTATE|Error|Descripción|  
|--------------|-----------|-----------------|  
|01000|Advertencia general|Específico del controlador de mensaje informativo. (La función devuelve SQL_SUCCESS_WITH_INFO).|  
|01001|Conflicto de operación de cursor|El *operación* argumento era SQL_DELETE o SQL_UPDATE, y no hay filas o más de una fila se eliminó o actualizó. (Para obtener más información acerca de las actualizaciones a más de una fila, vea la descripción de la SQL_ATTR_SIMULATE_CURSOR *atributo* en **SQLSetStmtAttr**.) (La función devuelve SQL_SUCCESS_WITH_INFO).<br /><br /> El *operación* argumento era SQL_DELETE o SQL_UPDATE y error en la operación debido a la simultaneidad optimista. (La función devuelve SQL_SUCCESS_WITH_INFO).|  
|01004|Truncamiento de datos derecho de cadena|El *operación* argumento era SQL_REFRESH y cadena o datos binarios devueltos para una o varias columnas con un tipo de datos SQL_C_CHAR o SQL_C_BINARY dieron como resultado el truncamiento de carácter no en blanco o datos binarios que no son NULL.|  
|01S01|Error en la fila|El *RowNumber* argumento era 0 y se produjo un error en una o varias filas al realizar la operación especificada con el *operación* argumento.<br /><br /> (Se devuelve SQL_SUCCESS_WITH_INFO si se produce un error en uno o más, pero no todas las filas de una operación de varias filas, y se devuelve SQL_ERROR si se produce un error en una operación única fila).<br /><br /> (Este SQLSTATE se devuelve solo cuando **SQLSetPos** se llama después de **SQLExtendedFetch**, si el controlador es un ODBC 2. *x* no se utiliza el controlador y la biblioteca de cursores.)|  
|01S07|Truncamiento fraccionario|El *operación* argumento era SQL_REFRESH, el tipo de datos del búfer de aplicación no era SQL_C_CHAR o SQL_C_BINARY y se truncaron los datos devueltos a los búferes de la aplicación para una o varias columnas. Para los tipos de datos numéricos, se ha truncado la parte fraccionaria del número. De hora, marca de tiempo y los tipos de datos de intervalo que contiene un componente de tiempo, se trunca la parte fraccionaria del tiempo.<br /><br /> (La función devuelve SQL_SUCCESS_WITH_INFO).|  
|07006|Infracción del atributo de tipo de datos restringido|No se pudo convertir el valor de datos de una columna del conjunto de resultados para el tipo de datos especificado por *TargetType* en la llamada a **SQLBindCol**.|  
|07009|Índice de descriptor no válido|El argumento *operación* fue SQL_REFRESH o SQL_UPDATE, y se enlaza una columna con un número de columna mayor que el número de columnas del conjunto de resultados.|  
|21S02|Grado de la tabla derivada no coincide con la lista de columnas|El argumento *operación* era SQL_UPDATE y no hay columnas eran actualizables porque todas las columnas se puede ser independiente, de solo lectura o el valor en el búfer de longitud/indicador enlazado era SQL_COLUMN_IGNORE.|  
|22001|Cadena de datos, truncamiento por la derecha|El *operación* argumento era SQL_UPDATE, y tuvo como resultado de la asignación de un carácter o un valor binario a una columna en el truncamiento de no están en blanco (para los caracteres) o distinto de null (para el binario) caracteres o bytes.|  
|22003|Valor numérico fuera del intervalo|El argumento *operación* estaba SQL_UPDATE y la asignación de un valor numérico a una columna del conjunto de resultados provocó la parte entera (en contraposición a fraccionarios) del número que se va a truncar.<br /><br /> El argumento *operación* era SQL_REFRESH y devolver el valor numérico para una o varias columnas enlazadas, habría provocado una pérdida de dígitos significativos.|  
|22007|Formato de datetime no válido|El argumento *operación* estaba SQL_UPDATE y la asignación de un valor date o timestamp a una columna del conjunto de resultados que provocó el año, mes o campo día para estar fuera del intervalo.<br /><br /> El argumento *operación* era SQL_REFRESH y devolver el valor de fecha o la marca de tiempo para uno o más columnas enlazadas habría provocado el año, mes o campo día para estar fuera del intervalo.|  
|22008|Desbordamiento del campo de fecha y hora|El *operación* argumento era SQL_UPDATE y el rendimiento de fecha y hora aritmética en datos que se envían a una columna del conjunto de resultados dieron lugar a un campo de fecha y hora (año, mes, día, hora, minuto o segundo campo) de los resultados fuera del intervalo válido de valores para el campo o no sea válido según las reglas en natural para fechas y horas del calendario gregoriano.<br /><br /> El *operación* argumento era SQL_REFRESH y el rendimiento de fecha y hora aritmética en los datos recuperados del conjunto de resultados dieron lugar a un campo de fecha y hora (año, mes, día, hora, minuto o segundo campo) de los resultados fuera del intervalo válido de valores para el campo o no sea válido según las reglas en natural para fechas y horas del calendario gregoriano.|  
|22015|Desbordamiento de campo de intervalo|El *operación* argumento era SQL_UPDATE y la asignación de un valor numérico exacto o el tipo de intervalo C a un tipo de datos SQL de intervalo causó una pérdida de dígitos significativos.<br /><br /> El *operación* argumento era SQL_UPDATE; cuando se asigna a un intervalo de tipo SQL, no había ninguna representación del valor del tipo C en el intervalo de tipo SQL.<br /><br /> El *operación* argumento era SQL_REFRESH y asignación de un valor numérico exacto o el intervalo de tipo SQL a un tipo de intervalo C causó una pérdida de dígitos significativos en el campo inicial.<br /><br /> El *operación* argumento era SQL_ actualizar; cuando se asigna a un tipo de intervalo de C, no había ninguna representación del valor del tipo SQL en el tipo de intervalo C.|  
|22018|Valor de carácter no válido para especificación cast|El *operación* argumento era SQL_REFRESH; el tipo C era un numérico exacto o aproximado, una fecha y hora o un tipo de datos de intervalo; el tipo SQL de la columna era un tipo de datos de caracteres; y el valor de la columna no es un literal válido de la tipo de C enlazado.<br /><br /> El argumento *operación* era SQL_UPDATE; el tipo SQL era un numérico exacto o aproximado, una fecha y hora o un tipo de datos de intervalo; el tipo de C era SQL_C_CHAR; y el valor de la columna no es un literal válido del tipo SQL enlazado.|  
|23000|Infracción de restricción de integridad|El argumento *operación* fue SQL_DELETE o SQL_UPDATE, y se ha infringido una restricción de integridad.|  
|24000|Estado de cursor no válido|El *StatementHandle* estaba en un estado ejecutado, pero se ha asociado ningún conjunto de resultados la *StatementHandle*.<br /><br /> (DM) un cursor estaba abierto en el *StatementHandle*, pero **SQLFetch** o **SQLFetchScroll** no se había llamado.<br /><br /> Un cursor estaba abierto en el *StatementHandle*, y **SQLFetch** o **SQLFetchScroll** hubiera llamado, pero el cursor se coloca antes del inicio del conjunto de resultados o después de final del conjunto de resultados.<br /><br /> El argumento *operación* fue SQL_DELETE, SQL_REFRESH o SQL_UPDATE, y el cursor se coloca antes del inicio del conjunto de resultados o después del final del conjunto de resultados.|  
|40001|Error de serialización.|Debido a un interbloqueo de recurso con otra transacción se revirtió la transacción.|  
|40003|Finalización de instrucción desconocida|Error en la conexión asociada durante la ejecución de esta función y no se puede determinar el estado de la transacción.|  
|42000|Error de sintaxis, infracción de acceso|El controlador no pudo bloquear la fila según sea necesario para realizar la operación solicitada en el argumento *operación*.<br /><br /> El controlador no pudo bloquear la fila cuando se le solicite en el argumento *LockType*.|  
|44000|Infracción de WITH CHECK OPTION|El *operación* argumento era SQL_UPDATE y la actualización se realizó en una tabla vista o una tabla derivada de la tabla mostrada en la que se creó mediante la especificación de **WITH CHECK OPTION**, de modo que una o varias filas afectado por la actualización ya no estará presente en la tabla mostrada.|  
|HY000|Error general|Se produjo un error para que se ha producido ningún SQLSTATE específico y para los que se ha definido ningún SQLSTATE específicos de la implementación. El mensaje de error devuelto por **SQLGetDiagRec** en el  *\*MessageText* búfer describe el error y su causa.|  
|HY001|Error de asignación de memoria|El controlador no pudo asignar la memoria necesaria para admitir la ejecución o la finalización de la función.|  
|HY008|Operación cancelada|Procesamiento asincrónico se habilitó para la *StatementHandle*. Se llamó a la función, y antes que completó la ejecución, **SQLCancel** o **SQLCancelHandle** se ha llamado en el *StatementHandle*, y, a continuación, se llamó a la función nuevo en el *StatementHandle*.<br /><br /> Se llamó a la función, y antes que completó la ejecución, **SQLCancel** o **SQLCancelHandle** se ha llamado en el *StatementHandle* desde un subproceso diferente en un aplicaciones multiproceso.|  
|HY010|Error de secuencia de función|(DM) se llamó a una función que se ejecuta de forma asincrónica para el identificador de conexión que está asociado el *StatementHandle*. Esta función asincrónica todavía se estaba ejecutando cuando se llamó a la función SQLSetPos.<br /><br /> (DM) especificado *StatementHandle* no estaba en un estado ejecutado. Se llamó a la función sin llamar primero a **SQLExecDirect**, **SQLExecute**, o una función de catálogo.<br /><br /> (DM) se llamó a una función que se ejecuta asincrónicamente (no ésta) para el *StatementHandle* y aún se estaba ejecutando cuando se llamó a esta función.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, o **SQLSetPos** se llamó para el  *StatementHandle* y devuelve SQL_NEED_DATA. Esta función se invoca antes de que se enviaron datos para todas las columnas o parámetros de datos en ejecución.<br /><br /> (DM) el controlador fue un 2 de ODBC. *x* controlador, y **SQLSetPos** se llamó para un *StatementHandle* después **SQLFetch** llamó.|  
|HY011|Atributo no se puede establecer ahora|(DM) el controlador fue un 2 de ODBC. *x* controlador; el SQL_ATTR_ROW_STATUS_PTR se estableció el atributo de instrucción; a continuación, **SQLSetPos** se llamó antes **SQLFetch**, **SQLFetchScroll**, o **SQLExtendedFetch** llamó.|  
|HY013|Error de administración de memoria|No se pudo procesar la llamada de función porque los objetos de memoria subyacente no se podrían tener acceso, posiblemente debido a memoria insuficiente.|  
|HY090|Longitud de búfer o cadena no válida|El *operación* argumento era SQL_UPDATE, un valor de datos era un puntero nulo y el valor de longitud de columna no era 0, SQL_DATA_AT_EXEC, SQL_COLUMN_IGNORE, SQL_NULL_DATA, o menor o igual que SQL_LEN_DATA_AT_EXEC_OFFSET.<br /><br /> El *operación* argumento era SQL_UPDATE; un valor de datos no era un puntero nulo; el tipo de datos C era SQL_C_BINARY o SQL_C_CHAR; y el valor de longitud de columna era menor que 0 pero no es igual a SQL_DATA_AT_EXEC, SQL_COLUMN_IGNORE , SQL_NTS o SQL_NULL_DATA, o menor o igual que SQL_LEN_DATA_AT_EXEC_OFFSET.<br /><br /> El valor en un búfer de longitud/indicador era SQL_DATA_AT_EXEC; el tipo SQL era SQL_LONGVARCHAR, SQL_LONGVARBINARY o un tipo de datos específicos del origen de datos long; y el tipo de información SQL_NEED_LONG_DATA_LEN **SQLGetInfo** era "S".|  
|HY092|Identificador de atributo no válido|(DM) el valor especificado para el *operación* argumento no era válido.<br /><br /> (DM) el valor especificado para el *LockType* argumento no era válido.<br /><br /> El *operación* argumento era SQL_UPDATE o SQL_DELETE y el atributo de instrucción SQL_ATTR_CONCURRENCY era SQL_ATTR_CONCUR_READ_ONLY.|  
|HY107|Valor de fila fuera del intervalo|El valor especificado para el argumento *RowNumber* era mayor que el número de filas del conjunto de filas.|  
|HY109|Posición del cursor no válido|El cursor asociado con el *StatementHandle* se definió como de solo avance, por lo que no se podría colocar el cursor dentro del conjunto de filas. Vea la descripción para el atributo SQL_ATTR_CURSOR_TYPE en **SQLSetStmtAttr**.<br /><br /> El *operación* argumento era SQL_UPDATE, SQL_DELETE o SQL_REFRESH y la fila identificada por el *RowNumber* argumento se había eliminado o no se ha tenido capturado.<br /><br /> (DM) el *RowNumber* argumento era 0 y el *operación* argumento era SQL_POSITION.<br /><br /> **SQLSetPos** llamó después **SQLBulkOperations** llamó y antes de **SQLFetchScroll** o **SQLFetch** llamó.|  
|HY117|Conexión está suspendida debido al estado de transacción desconocido. Solo se desconecte y se permiten funciones de solo lectura.|(DM) para obtener más información sobre el estado suspendido, consulte [función SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Característica opcional no implementada|El controlador u origen de datos no admite la operación solicitada en el *operación* argumento o la *LockType* argumento.|  
|HYT00|Se agotó el tiempo de espera|Ha expirado el período de tiempo de espera de consulta antes de que el origen de datos devuelva el conjunto de resultados. El período de tiempo de espera se establece a través de **SQLSetStmtAttr** con un *atributo* de SQL_ATTR_QUERY_TIMEOUT.|  
|HYT01|Tiempo de espera de conexión agotado|Ha expirado el período de tiempo de espera de conexión antes de que el origen de datos que respondió a la solicitud. El período de tiempo de espera de conexión se establece a través de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Controlador no admite esta función|(DM) el controlador asociado con el *StatementHandle* no admite la función.|  
|IM017|Sondeo se deshabilita en modo de notificación asincrónica|Cada vez que se usa el modelo de notificación, se deshabilita el sondeo.|  
|IM018|**SQLCompleteAsync** no se ha llamado para completar la operación asincrónica anterior en este identificador.|Si la llamada de función anterior en el controlador devuelve SQL_STILL_EXECUTING y si está habilitado el modo de notificación, **SQLCompleteAsync** debe llamarse en el identificador para realizar el procesamiento posterior y completar la operación.|  
  
## <a name="comments"></a>Comentarios  
  
> [!CAUTION]
>  Para obtener información acerca de la instrucción indica que **SQLSetPos** puede llamarse y lo que necesita hacer para ofrecer compatibilidad con ODBC 2 *.x* las aplicaciones, vea [cursores de bloque, cursores desplazables, y Compatibilidad con versiones anteriores](../../../odbc/reference/appendixes/block-cursors-scrollable-cursors-and-backward-compatibility.md).  
  
## <a name="rownumber-argument"></a>Argumento RowNumber  
 El *RowNumber* argumento especifica el número de la fila del conjunto de filas en el que se va a realizar la operación especificada por el *operación* argumento. Si *RowNumber* es 0, la operación se aplica a todas las filas del conjunto de filas. *RowNumber* debe ser un valor entre 0 y el número de filas del conjunto de filas.  
  
> [!NOTE]  
>  En el lenguaje C, las matrices son basado en 0 y el *RowNumber* argumento está basado en 1. Por ejemplo, para actualizar la quinta fila del conjunto de filas, una aplicación modifica los búferes de conjunto de filas en el índice de matriz 4 pero especifica un *RowNumber* de 5.  
  
 Todas las operaciones de colocar el cursor en la fila especificada por *RowNumber*. Las siguientes operaciones requieren una posición del cursor:  
  
-   Coloca la actualización y eliminación de instrucciones.  
  
-   Las llamadas a **SQLGetData**.  
  
-   Las llamadas a **SQLSetPos** con las opciones SQL_DELETE, SQL_REFRESH y SQL_UPDATE.  
  
 Por ejemplo, si *RowNumber* es 2 para llamar a **SQLSetPos** con un *operación* de SQL_DELETE, el cursor se coloca en la segunda fila del conjunto de filas y se elimina esa fila. La entrada en la implementación fila matriz de Estados (indicada por el atributo de instrucción SQL_ATTR_ROW_STATUS_PTR) para la segunda fila se cambia a SQL_ROW_DELETED.  
  
 Una aplicación puede especificar una posición del cursor cuando llama a **SQLSetPos**. Por lo general, llama a **SQLSetPos** con la operación SQL_POSITION o SQL_REFRESH para colocar el cursor antes de ejecutar un posicionadas update o delete, instrucción o una llamada a **SQLGetData**.  
  
## <a name="operation-argument"></a>Argumento de operación  
 El *operación* argumento admite las siguientes operaciones. Para determinar qué opciones son compatibles con un origen de datos, una aplicación llama a **SQLGetInfo** con SQL_DYNAMIC_CURSOR_ATTRIBUTES1, SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1, SQL_KEYSET_CURSOR_ATTRIBUTES1 o SQL_STATIC_ Tipo de información CURSOR_ATTRIBUTES1 (según el tipo del cursor).  
  
|*Operación*<br /><br /> argumento|Operación|  
|------------------------------|---------------|  
|SQL_POSITION|El controlador coloca el cursor en la fila especificada por *RowNumber*.<br /><br /> El contenido de la matriz de Estados de fila que apunta el atributo de instrucción SQL_ATTR_ROW_OPERATION_PTR se omite para las SQL_POSITION *operación*.|  
|SQL_REFRESH|El controlador coloca el cursor en la fila especificada por *RowNumber* y actualiza los datos en los búferes del conjunto de filas de esa fila. Para obtener más información acerca de cómo el controlador devuelve datos en los búferes de conjunto de filas, vea las descripciones de modo de fila y el enlace en **SQLBindCol**.<br /><br /> **SQLSetPos** con un *operación* de SQL_REFRESH actualiza el estado y el contenido de las filas dentro del conjunto de filas capturada actual. Esto incluye la actualización de los marcadores. Dado que los datos en los búferes se actualiza pero no volver a capturar, la pertenencia en el conjunto de filas se ha corregido. Esto es diferente de la actualización se realiza mediante una llamada a **SQLFetchScroll** con un *FetchOrientation* de SQL_FETCH_RELATIVE y un *RowNumber* igual a 0, que vuelve a obtener el conjunto de filas del conjunto de resultados para que pueda mostrar datos agregados y quitar los datos eliminados si esas operaciones son compatibles con el controlador y el cursor.<br /><br /> Una actualización correcta con **SQLSetPos** no cambiará el estado de una fila de SQL_ROW_DELETED. Las filas eliminadas del conjunto de filas se seguirán se marca como eliminada hasta la próxima recopilación. Las filas desaparecerá en la siguiente captura si el cursor admite el empaquetado (en el que un posteriores **SQLFetch** o **SQLFetchScroll** no devuelve las filas eliminadas).<br /><br /> Agrega filas no aparecen cuando una actualización con **SQLSetPos** se lleva a cabo. Este comportamiento es diferente de **SQLFetchScroll** con un *FetchType* de SQL_FETCH_RELATIVE y un *RowNumber* igual a 0, lo que también actualiza el conjunto de filas actual, pero que se Mostrar los registros agregados o módulo de registros eliminados si estas operaciones son compatibles con el cursor.<br /><br /> Una actualización correcta con **SQLSetPos** cambiará el estado de una fila de SQL_ROW_ADDED a SQL_ROW_SUCCESS (si existe la matriz de Estados de fila).<br /><br /> Una actualización correcta con **SQLSetPos** cambiará el estado de una fila de SQL_ROW_UPDATED al código de estado de la fila nueva (si existe la matriz de Estados de fila).<br /><br /> Si se produce un error en un **SQLSetPos** operación en una fila, el estado de fila se establece en SQL_ROW_ERROR (si existe la matriz de Estados de fila).<br /><br /> Para un cursor abierto con un atributo de instrucción SQL_ATTR_CONCURRENCY de SQL_CONCUR_ROWVER o SQL_CONCUR_VALUES, una actualización con **SQLSetPos** podría actualizar los valores de la simultaneidad optimista utilizados por el origen de datos para detectar que el fila ha cambiado. Si esto ocurre, las versiones de fila o los valores que se utiliza para garantizar la simultaneidad de cursor se actualizan cada vez que se actualizan los búferes de conjunto de filas desde el servidor. Esto se produce para cada fila que se actualiza.<br /><br /> El contenido de la matriz de Estados de fila que apunta el atributo de instrucción SQL_ATTR_ROW_OPERATION_PTR se omite para las SQL_REFRESH *operación*.|  
|SQL_UPDATE|El controlador coloca el cursor en la fila especificada por *RowNumber* y actualiza la fila de datos subyacente con los valores de los búferes de conjunto de filas (el *TargetValuePtr* argumento en  **SQLBindCol**). Recupera las longitudes de los datos de los búferes de longitud/indicador (el *StrLen_or_IndPtr* argumento en **SQLBindCol**). Si la longitud de cualquier columna es SQL_COLUMN_IGNORE, no se actualiza la columna. Después de actualizar la fila, el controlador cambia el elemento correspondiente de la matriz de Estados de fila a SQL_ROW_UPDATED o SQL_ROW_SUCCESS_WITH_INFO (si existe la matriz de Estados de fila).<br /><br /> Es definido por el controlador lo que es el comportamiento si **SQLSetPos** con un *operación* argumento de SQL_UPDATE se llama en un cursor que contiene las columnas duplicadas. El controlador puede devolver un valor de SQLSTATE definidos por el controlador, puede actualizar la primera columna que aparece en el conjunto de resultados o realizar otros comportamientos definidos por el controlador.<br /><br /> La matriz de operación de fila que apunta el atributo de instrucción SQL_ATTR_ROW_OPERATION_PTR puede utilizarse para indicar que una fila en el conjunto de filas actual se debe omitir durante una actualización masiva. Para obtener más información, vea "Matrices de estado y de operación" más adelante en esta referencia de función.|  
|SQL_DELETE|El controlador coloca el cursor en la fila especificada por *RowNumber* y elimina la fila de datos subyacente. Cambia el elemento correspondiente de la matriz de Estados de fila a SQL_ROW_DELETED. Después de que se ha eliminado la fila, los siguientes no son válidos para la fila: coloca la actualización y eliminación de instrucciones, las llamadas a **SQLGetData**y las llamadas a **SQLSetPos** con *operación* establece en cualquier valor excepto SQL_POSITION. Para los controladores compatibles con el empaquetado, se elimina la fila del cursor cuando se recuperan datos nuevos del origen de datos.<br /><br /> Si la fila permanece visible depende del tipo de cursor. Por ejemplo, las filas eliminadas son visibles para los cursores estáticos y controlados por pero invisibles para los cursores dinámicos.<br /><br /> La matriz de operación de fila que apunta el atributo de instrucción SQL_ATTR_ROW_OPERATION_PTR puede utilizarse para indicar que una fila en el conjunto de filas actual se debe omitir durante una eliminación masiva. Para obtener más información, vea "Matrices de estado y de operación" más adelante en esta referencia de función.|  
  
## <a name="locktype-argument"></a>Argumento LockType  
 El *LockType* argumento proporciona una manera para las aplicaciones controlar la simultaneidad. En la mayoría de los casos, los orígenes de datos que admiten los niveles de simultaneidad y las transacciones admitirá solo el valor SQL_LOCK_NO_CHANGE de la *LockType* argumento. El *LockType* argumento generalmente se usa solo para soporte técnico basado en archivos.  
  
 El *LockType* argumento especifica el estado de bloqueo de la fila después de **SQLSetPos** se ha ejecutado. Si el controlador no se puede bloquear la fila para realizar la operación solicitada o para satisfacer la *LockType* argumento, devuelve SQL_ERROR y SQLSTATE 42000 (sintaxis o infracción de acceso).  
  
 Aunque el *LockType* se especifica el argumento para una única instrucción, el bloqueo dará los mismos privilegios a todas las instrucciones de la conexión. En concreto, puede desbloquear un bloqueo que se adquiere una instrucción en una conexión con una instrucción diferente en la misma conexión.  
  
 Bloquea una fila a través de **SQLSetPos** permanece bloqueado hasta que la aplicación llama a **SQLSetPos** para la fila con *LockType* establecido en SQL_LOCK_UNLOCK, o hasta que la aplicación las llamadas **SQLFreeHandle** para la instrucción o **SQLFreeStmt** con la opción de SQL_CLOSE. Para un controlador que admite transacciones, se bloquea una fila a través de **SQLSetPos** se desbloquea cuando la aplicación llama **SQLEndTran** para confirmar o revertir una transacción en la conexión (si se cierra un cursor Cuando una transacción se confirma o revierte, tal y como indica los tipos de información SQL_CURSOR_COMMIT_BEHAVIOR y SQL_CURSOR_ROLLBACK_BEHAVIOR devueltos por **SQLGetInfo**).  
  
 El *LockType* argumento admite los siguientes tipos de bloqueos. Para determinar los bloqueos que son compatibles con un origen de datos, una aplicación llama a **SQLGetInfo** con SQL_DYNAMIC_CURSOR_ATTRIBUTES1, SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1, SQL_KEYSET_CURSOR_ATTRIBUTES1 o SQL_STATIC_ Tipo de información CURSOR_ATTRIBUTES1 (según el tipo del cursor).  
  
|*LockType* argumento|Tipo de bloqueo|  
|-------------------------|---------------|  
|SQL_LOCK_NO_CHANGE|El controlador u origen de datos garantiza que la fila en el mismo estado bloqueado o desbloqueado que estaba antes **SQLSetPos** llamó. Este valor de *LockType* permite a los orígenes de datos que no admiten bloqueos de nivel de fila explícitos para usar cualquier bloqueo es necesaria por los niveles de aislamiento de transacciones y simultaneidad actuales.|  
|SQL_LOCK_EXCLUSIVE|El controlador u origen de datos bloquea exclusivamente la fila. No se puede usar una instrucción en una conexión diferente o en una aplicación diferente para adquirir los bloqueos de la fila.|  
|SQL_LOCK_UNLOCK|El controlador u origen de datos desbloquea la fila.|  
  
 Si un controlador es compatible con SQL_LOCK_EXCLUSIVE pero no admite SQL_LOCK_UNLOCK, una fila que está bloqueada permanecerá bloqueada hasta que se produzca una de las llamadas de función que se describe en el párrafo anterior.  
  
 Si un controlador es compatible con SQL_LOCK_EXCLUSIVE pero no admite SQL_LOCK_UNLOCK, una fila que está bloqueada permanecerá bloqueada hasta que la aplicación llama a **SQLFreeHandle** para la instrucción o **SQLFreeStmt** con la opción SQL_CLOSE. Si el controlador admite las transacciones y se cierra el cursor al confirmar o revertir la transacción, la aplicación llama a **SQLEndTran**.  
  
 Para las operaciones update y delete en **SQLSetPos**, la aplicación usa el *LockType* argumento tal como sigue:  
  
-   Para garantizar que una fila no cambia después de haberlos recuperado, una aplicación llama a **SQLSetPos** con *operación* establecido en SQL_REFRESH y *LockType* establecido en SQL_LOCK_ EXCLUSIVO.  
  
-   Si la aplicación establece *LockType* a SQL_LOCK_NO_CHANGE, el controlador garantiza que una operación update o delete se realizará correctamente solo si la aplicación especifica SQL_CONCUR_LOCK para el atributo de instrucción SQL_ATTR_CONCURRENCY.  
  
-   Si la aplicación especifica SQL_CONCUR_ROWVER o SQL_CONCUR_VALUES para el atributo de instrucción SQL_ATTR_CONCURRENCY, el controlador compara las versiones de fila o los valores y rechaza la operación si la fila ha cambiado desde la aplicación había capturado la fila.  
  
-   Si la aplicación especifica SQL_CONCUR_READ_ONLY para el atributo de instrucción SQL_ATTR_CONCURRENCY, el controlador rechaza cualquier actualización o la operación de eliminación.  
  
 Para obtener más información sobre el atributo de instrucción SQL_ATTR_CONCURRENCY, consulte [SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md).  
  
## <a name="status-and-operation-arrays"></a>Estado y las matrices de operación  
 Las siguientes matrices de estado y la operación se usan al llamar a **SQLSetPos**:  
  
-   La matriz de Estados de fila (como la que apunta el campo SQL_DESC_ARRAY_STATUS_PTR IRD y el atributo de instrucción SQL_ATTR_ROW_STATUS_ARRAY) contiene los valores de estado para cada fila de datos en el conjunto de filas. El controlador establece los valores de estado de esta matriz después de llamar a **SQLFetch**, **SQLFetchScroll**, **SQLBulkOperations**, o **SQLSetPos** . El atributo de instrucción SQL_ATTR_ROW_STATUS_PTR apunta a esta matriz.  
  
-   La matriz de operación de fila (como la que apunta el campo SQL_DESC_ARRAY_STATUS_PTR el descartar y el atributo de instrucción SQL_ATTR_ROW_OPERATION_ARRAY) contiene un valor para cada fila del conjunto de filas que indica si una llamada a **SQLSetPos**para se omite o se realiza una operación masiva. Cada elemento de la matriz se establece en SQL_ROW_PROCEED (valor predeterminado) o SQL_ROW_IGNORE. El atributo de instrucción SQL_ATTR_ROW_OPERATION_PTR apunta a esta matriz.  
  
 El número de elementos de las matrices de estado y la operación debe ser igual el número de filas del conjunto de filas (tal y como se define por el atributo de instrucción SQL_ATTR_ROW_ARRAY_SIZE).  
  
 Para obtener información acerca de la matriz de Estados de fila, vea [SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md). Para obtener información acerca de la matriz de operación de fila, vea "Omitiendo una fila en una operación masiva," más adelante en esta sección.  
  
## <a name="using-sqlsetpos"></a>Uso de SQLSetPos  
 Antes de que una aplicación llama a **SQLSetPos**, debe realizar la siguiente secuencia de pasos:  
  
1.  Si la aplicación llamará **SQLSetPos** con *operación* establecido en SQL_UPDATE, llamada **SQLBindCol** (o **SQLSetDescRec**) para cada uno columna para especificar su tipo de datos y enlazar los búferes de datos y la longitud de la columna.  
  
2.  Si la aplicación llamará **SQLSetPos** con *operación* establecido en SQL_DELETE o SQL_UPDATE, llamada **SQLColAttribute** para asegurarse de que las columnas que se eliminó o actualizó son actualizables.  
  
3.  Llame a **SQLExecDirect**, **SQLExecute**, o una función de catálogo para crear un conjunto de resultados.  
  
4.  Llame a **SQLFetch** o **SQLFetchScroll** para recuperar los datos.  
  
 Para obtener más información sobre el uso de **SQLSetPos**, consulte [actualizar los datos con SQLSetPos](../../../odbc/reference/develop-app/updating-data-with-sqlsetpos.md).  
  
## <a name="deleting-data-using-sqlsetpos"></a>Eliminar datos con SQLSetPos  
 Para eliminar datos con **SQLSetPos**, una aplicación llama a **SQLSetPos** con *RowNumber* establecido en el número de la fila para eliminar y *operación*establecido en SQL_DELETE.  
  
 Después de que se han eliminado los datos, el controlador cambia el valor de la matriz de estado de fila de implementación para la fila correspondiente a SQL_ROW_DELETED (o SQL_ROW_ERROR).  
  
## <a name="updating-data-using-sqlsetpos"></a>Actualizar datos con SQLSetPos  
 Una aplicación puede pasar el valor de una columna en el búfer de datos enlazados o con uno o más llamadas a **SQLPutData**. Las columnas cuyos datos se pasan con **SQLPutData** se conocen como *datos en ejecución* *columnas*. Estos se usan normalmente para enviar datos de las columnas SQL_LONGVARBINARY y SQL_LONGVARCHAR y se pueden mezclar con otras columnas.  
  
#### <a name="to-update-data-with-sqlsetpos-an-application"></a>Para actualizar datos con SQLSetPos, una aplicación:  
  
1.  Los valores de los lugares en los búferes de datos y de longitud/indicador enlazan con **SQLBindCol**:  
  
    -   Para las columnas normales, la aplicación coloca el nuevo valor de columna en la  *\*TargetValuePtr* búfer y la longitud de ese valor en el  *\*StrLen_or_IndPtr* búfer. Si no se debe actualizar la fila, la aplicación coloca SQL_ROW_IGNORE en elemento de la fila de la matriz de operación de la fila.  
  
    -   Para las columnas de datos en ejecución, la aplicación coloca un valor definido por la aplicación, como el número de columna, en el  *\*TargetValuePtr* búfer. El valor se puede usar posteriormente para identificar la columna.  
  
         La aplicación coloca el resultado de la SQL_LEN_DATA_AT_EXEC (*longitud*) macro en el **StrLen_or_IndPtr* búfer. Si el tipo de datos SQL de la columna es SQL_LONGVARBINARY, SQL_LONGVARCHAR o un tipo de datos específicos del origen de datos de tipo long y el controlador devuelve "Y" para el tipo de información SQL_NEED_LONG_DATA_LEN en **SQLGetInfo**, *longitud*  es el número de bytes de datos que se enviarán para el parámetro; en caso contrario, debe ser un valor no negativo y se omite.  
  
2.  Las llamadas **SQLSetPos** con el *operación* establecido en SQL_UPDATE para actualizar la fila de datos.  
  
    -   Si no hay ninguna columna de datos en ejecución, el proceso está completado.  
  
    -   Si hay columnas de datos en ejecución, la función devuelve SQL_NEED_DATA y continúa con el paso 3.  
  
3.  Las llamadas **SQLParamData** para recuperar la dirección de la  *\*TargetValuePtr* búfer para la primera columna de datos en ejecución para procesarse. **SQLParamData** devuelve SQL_NEED_DATA. La aplicación recupera el valor definido por la aplicación desde el  *\*TargetValuePtr* búfer.  
  
    > [!NOTE]  
    >  Aunque los parámetros de datos en ejecución son similares a las columnas de datos en ejecución, el valor devuelto por **SQLParamData** es diferente para cada uno.  
  
    > [!NOTE]  
    >  Parámetros de datos en ejecución son parámetros en una instrucción SQL para el que se enviarán los datos con **SQLPutData** cuando se ejecuta la instrucción con **SQLExecDirect** o **SQLExecute**. Se enlazan con **SQLBindParameter** o estableciendo descriptores con **SQLSetDescRec**. El valor devuelto por **SQLParamData** es un valor de 32 bits que se pasa a **SQLBindParameter** en el *ParameterValuePtr* argumento.  
  
    > [!NOTE]  
    >  Columnas de datos en ejecución son columnas de un conjunto de filas para el que se enviarán los datos con **SQLPutData** cuando se actualiza una fila con **SQLSetPos**. Se enlazan con **SQLBindCol**. El valor devuelto por **SQLParamData** es la dirección de la fila en el **TargetValuePtr* búfer que se está procesando.  
  
4.  Las llamadas **SQLPutData** uno o más veces para enviar datos de la columna. Se necesita más de una llamada si no se puede devolver todos los valores de datos en el  *\*TargetValuePtr* especificado en el búfer **SQLPutData**; varias llamadas a **SQLPutData** para la misma columna se permiten solo al enviar datos de carácter C a una columna con un tipo de carácter, binario o datos específicos del origen de datos o al enviar datos binarios de C a una columna con un carácter, binario, o el tipo de datos específico del origen de datos.  
  
5.  Las llamadas **SQLParamData** nuevo para indicar que se han enviado todos los datos de la columna.  
  
    -   Si hay más columnas de datos en ejecución, **SQLParamData** devuelve SQL_NEED_DATA y la dirección de la *TargetValuePtr* búfer para la siguiente columna de datos en ejecución para procesarse. La aplicación repite los pasos 4 y 5.  
  
    -   Si no hay nada más columnas de datos en ejecución, el proceso está completado. Si se ha ejecutado correctamente, la instrucción **SQLParamData** devuelve SQL_SUCCESS o SQL_SUCCESS_WITH_INFO; si se produjo un error en la ejecución, devuelve SQL_ERROR. En este momento, **SQLParamData** puede devolver cualquier SQLSTATE, que puede devolver **SQLSetPos**.  
  
 Si se han actualizado los datos, el controlador cambia el valor de la matriz de estado de fila de implementación para la fila correspondiente a SQL_ROW_UPDATED.  
  
 Si se cancela la operación o se produce un error en **SQLParamData** o **SQLPutData**, después **SQLSetPos** devuelve SQL_NEED_DATA y antes de enviar los datos para todos columnas de datos en ejecución, la aplicación puede llamar solo **SQLCancel**, **SQLGetDiagField**, **SQLGetDiagRec**, **SQLGetFunctions** , **SQLParamData**, o **SQLPutData** para la instrucción o la conexión asociada con la instrucción. Si llama a cualquier otra función para la instrucción o la conexión asociada con la instrucción, la función devuelve SQL_ERROR y SQLSTATE HY010 (función de error de secuencia).  
  
 Si la aplicación llama a **SQLCancel** mientras el controlador sigue necesitando los datos para las columnas de datos en ejecución, el controlador cancela la operación. A continuación, puede llamar la aplicación **SQLSetPos** nuevo; Cancelar no afecta el estado del cursor o la posición actual del cursor.  
  
 Cuando la lista de selección de la especificación de consulta asociada con el cursor contiene más de una referencia a la misma columna, si se genera un error o el controlador omite las referencias duplicadas y realiza las operaciones solicitadas es definido por el controlador.  
  
## <a name="performing-bulk-operations"></a>Realización de operaciones masivas  
 Si el *RowNumber* argumento es 0, el controlador realiza la operación especificada en el *operación* argumento para cada fila del conjunto de filas que tiene un valor de SQL_ROW_PROCEED en su campo en la operación de fila matriz señalada por el atributo de instrucción SQL_ATTR_ROW_OPERATION_PTR. Este es un valor válido de la *RowNumber* argumento para un *operación* argumento de SQL_DELETE, SQL_REFRESH, o SQL_UPDATE, pero no SQL_POSITION. **SQLSetPos** con un *operación* de SQL_POSITION y un *RowNumber* es igual a 0 devolverá SQLSTATE HY109 (posición del cursor no válido).  
  
 Si produce un error que se aplica a todo el conjunto de filas, como SQLSTATE HYT00 (tiempo de espera expirado), el controlador devuelve SQL_ERROR y el SQLSTATE correspondiente. El contenido de los búferes del conjunto de filas no está definido, y la posición del cursor se ha modificado.  
  
 Si produce un error pertenece a una sola fila, el controlador:  
  
-   Establece el elemento de la fila de la matriz de Estados de fila que apunta el atributo de instrucción SQL_ATTR_ROW_STATUS_PTR para SQL_ROW_ERROR.  
  
-   Envía una o varias SQLSTATEs adicionales para el error en la cola de errores y establece el campo SQL_DIAG_ROW_NUMBER en la estructura de datos de diagnóstico.  
  
 Una vez procesado el error o advertencia, si el controlador completa la operación de las filas restantes del conjunto de filas, devuelve SQL_SUCCESS_WITH_INFO. Por lo tanto, para cada fila que devolvió un error, la cola de errores contiene cero o más SQLSTATEs adicionales. Si el controlador detiene la operación una vez procesado el error o advertencia, devuelve SQL_ERROR.  
  
 Si el controlador devuelve las advertencias, como SQLSTATE 01004 (datos truncados), devuelve las advertencias que se aplican a todo el conjunto de filas o filas desconocidas en el conjunto de filas antes de devolver la información de error que se aplica a filas específicas. Devuelve las advertencias para las filas específicas junto con cualquier otra información de error acerca de las filas.  
  
 Si *RowNumber* es igual a 0 y *operación* es SQL_UPDATE, SQL_REFRESH o SQL_DELETE, el número de filas que **SQLSetPos** opera en apunta a la y Atributo de instrucción _FETCHED_PTR.  
  
 Si *RowNumber* es igual a 0 y *operación* es SQL_DELETE, SQL_REFRESH o SQL_UPDATE, la fila actual después de la operación es igual que la fila actual antes de la operación.  
  
## <a name="ignoring-a-row-in-a-bulk-operation"></a>Se omitirá una fila en una operación masiva  
 La matriz de operación de la fila se puede usar para indicar que una fila en el conjunto de filas actual se debe omitir durante una operación masiva mediante **SQLSetPos**. Para indicar que el controlador para pasar por alto una o varias filas durante una operación masiva, una aplicación debe realizar los pasos siguientes:  
  
1.  Llame a **SQLSetStmtAttr** para establecer el atributo de instrucción SQL_ATTR_ROW_OPERATION_PTR para que apunte a una matriz de SQLUSMALLINTs. Este campo también se puede establecer mediante una llamada a **SQLSetDescField** para establecer el campo de encabezado SQL_DESC_ARRAY_STATUS_PTR del descartar, lo que requiere que una aplicación obtiene el identificador de descriptor.  
  
2.  Cada elemento de la matriz de operación de la fila se establece en uno de dos valores:  
  
    -   SQL_ROW_IGNORE, para indicar que la fila se ha excluido de la operación masiva.  
  
    -   SQL_ROW_PROCEED, para indicar que la fila se incluye en la operación masiva. (Esto es el valor predeterminado).  
  
3.  Llame a **SQLSetPos** para realizar la operación masiva.  
  
 Las siguientes reglas se aplican a la matriz de operación de fila:  
  
-   SQL_ROW_IGNORE y SQL_ROW_PROCEED afectan a solo las operaciones masivas utilizando **SQLSetPos** con un *operación* de SQL_DELETE o SQL_UPDATE. No afectan a las llamadas a **SQLSetPos** con un *operación* de SQL_REFRESH o SQL_POSITION.  
  
-   El puntero se establece en null de forma predeterminada.  
  
-   Si el puntero es null, se actualizan todas las filas como si todos los elementos se han establecido en SQL_ROW_PROCEED.  
  
-   Establecimiento de un elemento a SQL_ROW_PROCEED no garantiza que la operación se producirá en esa fila determinada. Por ejemplo, si una determinada fila del conjunto de filas tiene el estado SQL_ROW_ERROR, el controlador puede no ser capaz de actualizar esa fila, independientemente de si la aplicación especificó SQL_ROW_PROCEED. Una aplicación debe comprobar siempre la matriz de Estados de fila para ver si la operación fue correcta.  
  
-   SQL_ROW_PROCEED se define como 0 en el archivo de encabezado. Una aplicación puede inicializar la matriz de operación de la fila en 0 con el fin de procesar todas las filas.  
  
-   Si el número de elemento "n" en la matriz de operación de la fila se establece en SQL_ROW_IGNORE y **SQLSetPos** se llama para realizar una actualización masiva o la enésima fila en el conjunto de filas que se modifica después de llamar a la operación de eliminación **SQLSetPos**.  
  
-   Una aplicación debe establecer automáticamente una columna de sólo lectura a SQL_ROW_IGNORE.  
  
## <a name="ignoring-a-column-in-a-bulk-operation"></a>Omitir una columna en una operación masiva  
 Para evitar los diagnósticos de procesamiento innecesario generados por intentadas actualizaciones a una o varias columnas de solo lectura, una aplicación puede establecer el valor en el búfer de longitud/indicador enlazado a SQL_COLUMN_IGNORE. Para obtener más información, consulte [SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md).  
  
## <a name="code-example"></a>Ejemplo de código  
 En el ejemplo siguiente, una aplicación permite al usuario examinar la tabla ORDERS y actualizar el estado del pedido. El cursor es dinámico con un tamaño de conjunto de filas de 20 y usa el control de simultaneidad optimista comparar versiones de fila. Después de que se captura cada conjunto de filas, la aplicación lo imprime y permite al usuario seleccionar y actualizar el estado de un pedido. La aplicación usa **SQLSetPos** para colocar el cursor en la fila seleccionada y realiza una actualización por posición de la fila. (Control de errores se omite para mayor claridad).  
  
```  
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
  
 Para obtener más ejemplos, vea [coloca actualizar y eliminar instrucciones](../../../odbc/reference/develop-app/positioned-update-and-delete-statements.md) y [actualizar filas en el conjunto de filas con SQLSetPos](../../../odbc/reference/develop-app/updating-rows-in-the-rowset-with-sqlsetpos.md).  
  
## <a name="related-functions"></a>Funciones relacionadas  
  
|Para obtener información acerca de|Vea|  
|---------------------------|---------|  
|Enlazar un búfer con una columna en un conjunto de resultados|[Función SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Realizar operaciones masivas que no hacen referencia a la posición del cursor de bloque|[Función SQLBulkOperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md)|  
|Procesamiento de una instrucción de cancelación|[Función SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Obtención de un bloque de datos o desplazarse a través de un resultado de conjunto|[Función SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|Obtención de un único campo de un descriptor|[Función SQLGetDescField](../../../odbc/reference/syntax/sqlgetdescfield-function.md)|  
|Introducción a varios campos de descriptor|[Función SQLGetDescRec](../../../odbc/reference/syntax/sqlgetdescrec-function.md)|  
|Configuración de un único campo de un descriptor|[Función SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)|  
|Configuración de varios campos de descriptor|[Función SQLSetDescRec](../../../odbc/reference/syntax/sqlsetdescrec-function.md)|  
|Establecer un atributo de instrucción|[Función SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>Vea también  
 [Referencia de la API de ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Archivos de encabezado de ODBC](../../../odbc/reference/install/odbc-header-files.md)
