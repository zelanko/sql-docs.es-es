---
title: Función SQLGetData | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
apiname:
- SQLGetData
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLGetData
helpviewer_keywords:
- SQLGetData function [ODBC]
ms.assetid: e3c1356a-5db7-4186-85fd-8b74633317e8
caps.latest.revision: 46
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: bd10d34093e7aa1bcbe901555c6b23ffc6368fbb
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="sqlgetdata-function"></a>Función SQLGetData
**Conformidad**  
 Versión introdujo: Cumplimiento de estándares 1.0 de ODBC: ISO 92  
  
 **Resumen**  
 **SQLGetData** recupera datos de una sola columna del conjunto de resultados o para un único parámetro después de **SQLParamData** devuelve SQL_PARAM_DATA_AVAILABLE. Se puede llamar varias veces para recuperar datos de longitud variable en partes.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
SQLRETURN SQLGetData(  
      SQLHSTMT       StatementHandle,  
      SQLUSMALLINT   Col_or_Param_Num,  
      SQLSMALLINT    TargetType,  
      SQLPOINTER     TargetValuePtr,  
      SQLLEN         BufferLength,  
      SQLLEN *       StrLen_or_IndPtr);  
```  
  
## <a name="arguments"></a>Argumentos  
 *StatementHandle*  
 [Entrada] Identificador de instrucción.  
  
 *Col_or_Param_Num*  
 [Entrada] Para recuperar datos de columna, es el número de la columna para la que se va a devolver datos. Columnas del conjunto de resultados se numeran en orden creciente de las columnas a partir de 1. La columna de marcador es el número de columna 0; Esto se puede especificar únicamente si se habilitan los marcadores.  
  
 Para recuperar datos de parámetro, es el ordinal del parámetro, que comienza en 1.  
  
 *TargetType*  
 [Entrada] El identificador de tipo del tipo de datos C de la **TargetValuePtr* búfer. Para obtener una lista de tipos de datos válidos de C y los identificadores de tipo, consulte el [tipos de datos C](../../../odbc/reference/appendixes/c-data-types.md) sección en tipos de datos de apéndice D:.  
  
 Si *TargetType* es SQL_ARD_TYPE, lo controladores utiliza el identificador del tipo especificado en el campo SQL_DESC_CONCISE_TYPE de la descartar. Si *TargetType* es SQL_APD_TYPE, **SQLGetData** va a usar el mismo tipo de datos de C que se especificó en **SQLBindParameter**. En caso contrario, se especifica el tipo de datos de C en **SQLGetData** invalida especificado en el tipo de datos de C **SQLBindParameter**. Si es SQL_C_DEFAULT, el controlador selecciona el tipo de datos C predeterminado según el tipo de datos SQL del origen.  
  
 También puede especificar un tipo de datos C extendido. Para obtener más información, consulte [tipos de datos C en ODBC](../../../odbc/reference/develop-app/c-data-types-in-odbc.md).  
  
 *TargetValuePtr*  
 [Salida] Puntero al búfer en el que se va a devolver los datos.  
  
 *TargetValuePtr* no puede ser NULL.  
  
 *BufferLength*  
 [Entrada] Longitud de la **TargetValuePtr* búfer en bytes.  
  
 El controlador utiliza *BufferLength* para evitar escribir más allá del final de la \* *TargetValuePtr* almacenar en búfer cuando se devuelven los datos de longitud variable, como datos de caracteres o binarios. Tenga en cuenta que el controlador cuenta el carácter de terminación null cuando se devuelven los datos de caracteres a \* *TargetValuePtr*. **TargetValuePtr* , por tanto, debe contener un espacio para el carácter de terminación null, o el controlador, se truncará los datos.  
  
 Cuando el controlador devuelve datos de longitud fija, como un entero o una estructura de fecha, el controlador omite *BufferLength* y se supone que el búfer es lo suficientemente grande como para contener los datos. Por lo tanto, es importante para la aplicación asignar un búfer lo suficientemente grande como para datos de longitud fija o el controlador escribirá más allá del final del búfer.  
  
 **SQLGetData** devuelve SQLSTATE HY090 (longitud de búfer o cadena no válida) al *BufferLength* es menor que 0 pero no cuando *BufferLength* es 0.  
  
 *StrLen_or_IndPtr*  
 [Salida] Puntero al búfer en el que se va a devolver el valor de longitud o indicador. Si se trata de un puntero nulo, no se devuelve ningún valor de longitud o indicador. Esto devuelve un error cuando los datos que se capturan están NULL.  
  
 **SQLGetData** puede devolver los valores siguientes en el búfer de longitud/indicador:  
  
-   La longitud de los datos disponibles para devolver  
  
-   SQL_NO_TOTAL  
  
-   SQL_NULL_DATA  
  
 Para obtener más información, consulte [con valores de longitud/indicador](../../../odbc/reference/develop-app/using-length-and-indicator-values.md) y "Comentarios" en este tema.  
  
## <a name="returns"></a>Devuelve  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NO_DATA, SQL_STILL_EXECUTING, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Cuando **SQLGetData** devuelve SQL_ERROR o SQL_SUCCESS_WITH_INFO, un valor SQLSTATE asociado se puede obtener mediante una llamada a **SQLGetDiagRec** con un *HandleType* de SQL_HANDLE_STMT y un *controlar* de *StatementHandle*. En la tabla siguiente se enumera los valores SQLSTATE devueltos normalmente por **SQLGetData** y se explica cada uno de ellos en el contexto de esta función; la notación "(DM)" precede a las descripciones de SQLSTATE devuelto por el Administrador de controladores. El código de retorno asociado a cada valor SQLSTATE es SQL_ERROR, a menos que se indique lo contrario.  
  
|SQLSTATE|Error|Description|  
|--------------|-----------|-----------------|  
|01000|Advertencia general|Mensaje informativo de específicas del controlador. (La función devuelve SQL_SUCCESS_WITH_INFO).|  
|01004|Datos de cadena, delimitado truncados|No todos los datos para la columna especificada, *Col_or_Param_Num*, se pudo recuperar en una sola llamada a la función. SQL_NO_TOTAL o la longitud de los datos restantes de la columna especificada antes de la llamada actual a **SQLGetData** se devuelve en \* *StrLen_or_IndPtr*. (La función devuelve SQL_SUCCESS_WITH_INFO).<br /><br /> Para obtener más información sobre el uso de varias llamadas a **SQLGetData** para una sola columna, vea "Comentarios".|  
|01S07|Truncamiento fraccionario|Se truncaron los datos devueltos de una o más columnas. Para los tipos de datos numéricos, se trunca la parte fraccionaria del número. De hora, marca de tiempo y los tipos de datos interval que contiene un componente de tiempo, se trunca la parte fraccionaria del tiempo.<br /><br /> (La función devuelve SQL_SUCCESS_WITH_INFO).|  
|07006|Infracción del atributo de tipo de datos restringido|El valor de datos de una columna del conjunto de resultados no se puede convertir al tipo de datos C especificado por el argumento *TargetType*.|  
|07009|Índice de descriptor no válido|El valor especificado para el argumento *Col_or_Param_Num* es 0 y el atributo de instrucción SQL_ATTR_USE_BOOKMARKS estaba establecido como SQL_UB_OFF.<br /><br /> El valor especificado para el argumento *Col_or_Param_Num* era mayor que el número de columnas del conjunto de resultados.<br /><br /> El *Col_or_Param_Num* valor no es igual que el ordinal del parámetro que está disponible.<br /><br /> (DM) se enlazó a la columna especificada. Esta descripción no se aplica a los controladores que devuelven la máscara de bits SQL_GD_BOUND la opción SQL_GETDATA_EXTENSIONS en **SQLGetInfo**.<br /><br /> (DM) el número de la columna especificada es menor o igual al número de la columna dependiente más alto. Esta descripción no se aplica a los controladores que devuelven la máscara de bits SQL_GD_ANY_COLUMN la opción SQL_GETDATA_EXTENSIONS en **SQLGetInfo**.<br /><br /> (DM) la aplicación ya ha llamado **SQLGetData** para la fila actual; el número de la columna especificada en la llamada actual era menor que el número de la columna especificada en la llamada anterior; y el controlador no devuelve el SQL_ GD_ANY_ORDER máscara de bits para la opción SQL_GETDATA_EXTENSIONS en **SQLGetInfo**.<br /><br /> (DM) la *TargetType* argumento era SQL_ARD_TYPE y el *Col_or_Param_Num* error de registro del descriptor de la descartar la comprobación de coherencia.<br /><br /> (DM) la *TargetType* argumento era SQL_ARD_TYPE y el valor del campo SQL_DESC_COUNT de la descartar era menor que el *Col_or_Param_Num* argumento.|  
|08S01|Error de vínculo de comunicación|El vínculo de comunicación entre el controlador y el origen de datos al que se conectó el controlador no pudo antes del procesamiento de la función se ha completado.|  
|22002|Variable de indicador necesaria, pero no se ha suministrado|*StrLen_or_IndPtr* era un puntero nulo y se recuperan datos de tipo NULL.|  
|22003|Valor numérico fuera del intervalo|Devolver el valor numérico (como numérico o cadena) para la columna habría provocado la parte entera (en lugar de fracciones) del número se trunque.<br /><br /> Para obtener más información, consulte [tipos de datos de apéndice D:](../../../odbc/reference/appendixes/appendix-d-data-types.md).|  
|22007|Formato de datetime no válido|La columna de caracteres del conjunto de resultados se enlazó a una fecha, hora o estructura de marca de tiempo de C, y el valor de la columna era una fecha no válida, una hora o una marca de tiempo, respectivamente. Para obtener más información, consulte [tipos de datos de apéndice D:](../../../odbc/reference/appendixes/appendix-d-data-types.md).|  
|22012|División por cero|Se devolvió un valor de una expresión aritmética que dan como resultado de división por cero.|  
|22015|Desbordamiento del campo de intervalo|Asignación de un valor numérico exacto o el intervalo de tipo SQL a un tipo de intervalo C causó una pérdida de dígitos significativos en el campo inicial.<br /><br /> Cuando se devuelven datos a un tipo de intervalo C, no había ninguna representación del valor del tipo de SQL en el tipo de intervalo C.|  
|22018|Valor de carácter no válido para especificación cast|Una columna de caracteres del conjunto de resultados se devuelve a un búfer de caracteres de C y la columna contiene un carácter para el que se ha producido ninguna representación en el juego de caracteres del búfer.<br /><br /> El tipo C era un numérico exacto o aproximado, una fecha y hora o un tipo de datos del intervalo; el tipo SQL de la columna era un tipo de datos character; y el valor de la columna no es un literal válido del tipo de C enlazado.|  
|24000|Estado de cursor no válido|(DM) se llama a la función sin antes de llamar a **SQLFetch** o **SQLFetchScroll** para colocar el cursor en la fila de datos necesarios.<br /><br /> (DM) la *StatementHandle* estaba en un estado ejecutado, pero ningún conjunto de resultados se asoció el *StatementHandle*.<br /><br /> Un cursor estaba abierto en el *StatementHandle* y **SQLFetch** o **SQLFetchScroll** si se hubiese llamado, pero el cursor se coloca antes del inicio del conjunto de resultados o después de la final del conjunto de resultados.|  
|HY000|Error general|Se produjo un error para que no hubo ninguna SQLSTATE específico y para el que se ha definido ningún SQLSTATE específico de la implementación. El mensaje de error devuelto por **SQLGetDiagRec** en el *MessageText* búfer describe el error y su causa.|  
|HY001|Error de asignación de memoria|El controlador no pudo asignar la memoria necesaria para admitir la ejecución o la finalización de la función.|  
|HY003|Tipo de programa fuera del intervalo|(DM) el argumento *TargetType* no era un tipo de datos válido, SQL_C_DEFAULT, SQL_ARD_TYPE (en caso de recuperación de datos de columna) o SQL_APD_TYPE (en caso de recuperación de datos de parámetro).<br /><br /> (DM) el argumento *Col_or_Param_Num* era 0 y el argumento *TargetType* no era SQL_C_BOOKMARK para un marcador de longitud fija o SQL_C_VARBOOKMARK por un marcador de longitud variable.|  
|HY008|Operación cancelada|Procesamiento asincrónico se habilitó para la *StatementHandle*. Se llamó a la función y antes que completó la ejecución, **SQLCancel** o **SQLCancelHandle** se llamó en la *StatementHandle*, y, a continuación, se llama a la función de nuevo en el *StatementHandle*.<br /><br /> Se llamó a la función y antes que completó la ejecución, **SQLCancel** o **SQLCancelHandle** se llamó en la *StatementHandle* desde un subproceso distinto en un aplicaciones multiproceso y, a continuación, la función se llama de nuevo en el *StatementHandle*.|  
|HY009|Uso no válido del puntero null|(DM) el argumento *TargetValuePtr* era un puntero nulo.|  
|HY010|Error de secuencia de función|(DM) especificado *StatementHandle* no estaba en un estado ejecutado. Se llamó a la función sin antes de llamar a **SQLExecDirect**, **SQLExecute** o una función de catálogo.<br /><br /> (DM) se llamó a una función ejecuta de forma asincrónica para el identificador de conexión que está asociado el *StatementHandle*. Esta función asincrónica aún estaba ejecutando cuando el **SQLGetData** se llamó la función.<br /><br /> (DM) se llamó a una función ejecuta de forma asincrónica (no esta uno) para la *StatementHandle* y aún se estaba ejecutando cuando se llamó a esta función.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, o **SQLSetPos** se llamó para el  *StatementHandle* y devuelve SQL_NEED_DATA. Esta función se invoca antes de que se enviaron los datos para todas las columnas o parámetros de datos en ejecución.<br /><br /> (DM) la *StatementHandle* estaba en un estado ejecutado, pero ningún conjunto de resultados se asoció el *StatementHandle*.<br /><br /> Una llamada a **SQLExeceute**, **SQLExecDirect**, o **SQLMoreResults** devuelve SQL_PARAM_DATA_AVAILABLE, pero **SQLGetData** se llamó , en lugar de **SQLParamData**.|  
|HY013|Error de administración de memoria|No se pudo procesar la llamada de función porque los objetos subyacentes de la memoria no se pudieron tener acceso, posiblemente debido a condiciones de memoria insuficiente.|  
|HY090|Longitud de búfer o cadena no válida|(DM) el valor especificado para el argumento *BufferLength* era menor que 0.<br /><br /> El valor especificado para el argumento *BufferLength* fue inferior a 4, la *Col_or_Param_Num* argumento se establece en 0 y el controlador fue un ODBC 2*.x* controlador.|  
|HY109|Posición del cursor no válido|El cursor se coloca (por **SQLSetPos**, **SQLFetch**, **SQLFetchScroll**, o **SQLBulkOperations**) en una fila que se había eliminada o no se pudo obtener.<br /><br /> El cursor estaba un cursor de solo avance y el tamaño del conjunto de filas es mayor que uno.|  
|HY117|Se suspende la conexión debido al estado de transacción desconocido. Solo se desconecte y se permiten las funciones de solo lectura.|(DM) para obtener más información sobre el estado suspendido, consulte [función SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Característica opcional no implementada|El controlador u origen de datos no admite el uso de **SQLGetData** con varias filas en **SQLFetchScroll**. Esta descripción no se aplica a los controladores que devuelven la máscara de bits SQL_GD_BLOCK la opción SQL_GETDATA_EXTENSIONS en **SQLGetInfo**.<br /><br /> El controlador u origen de datos no admite la conversión especificada por la combinación de la *TargetType* argumento y el tipo de datos SQL de la columna correspondiente. Este error se aplica sólo cuando el tipo de datos SQL de la columna se ha asignado a un tipo de datos SQL específico del controlador.<br /><br /> El controlador admite solo ODBC 2*.x*y el argumento *TargetType* era una de las siguientes acciones:<br /><br /> SQL_C_NUMERIC SQL_C_SBIGINT SQL_C_UBIGINT<br /><br /> y cualquiera de los tipos de datos C de intervalo que aparecen en [tipos de datos C](../../../odbc/reference/appendixes/c-data-types.md) en tipos de datos de apéndice D:.<br /><br /> El controlador solo es compatible con las versiones ODBC anteriores 3.50 y el argumento *TargetType* era SQL_C_GUID.|  
|HYT01|Tiempo de espera de conexión expirado|El período de tiempo de espera de conexión finalizó antes de que el origen de datos se respondió a la solicitud. El período de tiempo de espera de conexión se establece a través de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Controlador no admite esta función|(DM) el controlador correspondiente a la *StatementHandle* no admite la función.|  
|IM017|Sondeo está deshabilitado en el modo de notificación asincrónica|Cada vez que se utiliza el modelo de notificación, se deshabilita el sondeo.|  
|IM018|**SQLCompleteAsync** no se ha llamado para completar la operación asincrónica anterior en este identificador.|Si la llamada de función anterior en el controlador devuelve SQL_STILL_EXECUTING y si está habilitado el modo de notificación, **SQLCompleteAsync** se debe llamar en el identificador para realizar el procesamiento posterior a la y completar la operación.|  
  
## <a name="comments"></a>Comentarios  
 **SQLGetData** devuelve los datos en una columna especificada. **SQLGetData** puede llamar solo después de que una o más filas se han capturado el conjunto de resultados **SQLFetch**, **SQLFetchScroll**, o **SQLExtendedFetch**. Si los datos de longitud variable están demasiado largo para devolverse en una sola llamada a **SQLGetData** (debido a una limitación en la aplicación), **SQLGetData** pueda recuperarlos en partes. Es posible enlazar algunas columnas de una fila y una llamada **SQLGetData** en otros casos, aunque esto está sujeto a algunas restricciones. Para obtener más información, consulte [obtener datos Long](../../../odbc/reference/develop-app/getting-long-data.md).  
  
 Para obtener información sobre el uso de **SQLGetData** con parámetros de salida transmitidos, consulte [recuperar parámetros de salida mediante SQLGetData](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md).  
  
## <a name="using-sqlgetdata"></a>Mediante SQLGetData  
 Si el controlador no admite extensiones de **SQLGetData**, la función puede devolver datos solamente para las columnas sin enlazar con un número mayor que el de la última columna enlazada. Además, dentro de una fila de datos, el valor de la *Col_or_Param_Num* argumento en cada llamada a **SQLGetData** debe ser mayor o igual que el valor de *Col_or_Param_Num*en la llamada anterior; es decir, los datos se deben recuperar de forma ascendente, orden de número de columna. Por último, si no se admiten extensiones, **SQLGetData** no se puede llamar si el tamaño del conjunto de filas es mayor que 1.  
  
 Los controladores pueden ser menos exigentes alguna de estas restricciones. Para determinar qué restricciones relaja un controlador, una aplicación llama **SQLGetInfo** con cualquiera de las siguientes opciones de SQL_GETDATA_EXTENSIONS:  
  
-   SQL_GD_OUTPUT_PARAMS = **SQLGetData** puede llamarse para devolver valores de parámetro de salida. Para obtener más información, consulte [recuperar parámetros de salida mediante SQLGetData](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md).  
  
-   SQL_GD_ANY_COLUMN. Si esta opción se devuelve, **SQLGetData** puede llamarse para cualquier columna sin enlazar, las incluidas antes de la última columna enlazada.  
  
-   SQL_GD_ANY_ORDER. Si esta opción se devuelve, **SQLGetData** puede llamarse para columnas sin enlazar en cualquier orden.  
  
-   SQL_GD_BLOCK. Si esta opción es devuelto por **SQLGetInfo** para el tipo de información SQL_GETDATA_EXTENSIONS, el controlador admite llamadas a **SQLGetData** cuando el tamaño del conjunto de filas es mayor que 1 y la aplicación puede llamar a **SQLSetPos** con la opción SQL_POSITION para colocar el cursor en la fila correcta antes de llamar a **SQLGetData.**  
  
-   SQL_GD_BOUND. Si esta opción se devuelve, **SQLGetData** puede llamarse para las columnas enlazadas, así como las columnas que no enlazados.  
  
 Hay dos excepciones a estas restricciones y capacidad del controlador de ser menos exigentes con ellos. En primer lugar, **SQLGetData** nunca se debería llamar para un cursor de avance y solo cuando el tamaño del conjunto de filas es mayor que 1. En segundo lugar, si un controlador es compatible con marcadores, siempre debe admitir la capacidad de llamar a **SQLGetData** para la columna 0, incluso si no permite a las aplicaciones llamen a **SQLGetData** de otras columnas antes de la última columna enlazada. (Cuando una aplicación se trabaja con una API ODBC 2*.x* controlador, **SQLGetData** devolverá correctamente un marcador cuando se llama con *Col_or_Param_Num* igual a 0 después de llamar a **SQLFetch**, porque **SQLFetch** ha sido asignada por ODBC 3*.x* el Administrador de controladores a **SQLExtendedFetch** con un  *FetchOrientation* de SQL_FETCH_NEXT, y **SQLGetData** con un *Col_or_Param_Num* 0 ha sido asignada por ODBC 3*.x* para el Administrador de controladores **SQLGetStmtOption** con una *fOption* de SQL_GET_BOOKMARK.)  
  
 **SQLGetData** no se puede usar para recuperar el marcador de una fila recién insertado mediante una llamada a **SQLBulkOperations** con la opción SQL_ADD, porque no está colocado el cursor en la fila. Una aplicación puede recuperar el marcador de dicha fila enlazando la columna 0 antes de llamar a **SQLBulkOperations** con SQL_ADD, en cuyo caso **SQLBulkOperations** devuelve el marcador en el búfer de enlazado. **SQLFetchScroll** , a continuación, se puede llamar con SQL_FETCH_BOOKMARK para volver a colocar el cursor en esa fila.  
  
 Si el *TargetType* argumento es un tipo de datos de intervalo, la precisión iniciales de intervalo (2) y la precisión de segundos de intervalo predeterminado (6), como se establece en los campos SQL_DESC_DATETIME_INTERVAL_PRECISION y SQL_DESC_PRECISION de Descartar, respectivamente, se usan para los datos. Si el *TargetType* argumento es un tipo de datos SQL_C_NUMERIC, la precisión predeterminada (definida por el controlador) y predeterminado escala (0), como se establece en los campos SQL_DESC_PRECISION y SQL_DESC_SCALE de la descartar, se usan para los datos. Si cualquier valor predeterminado de precisión o escala no es adecuada, la aplicación debe establecer explícitamente el campo descriptor adecuado mediante una llamada a **SQLSetDescField** o **SQLSetDescRec**. Puede establecer el campo SQL_DESC_CONCISE_TYPE en SQL_C_NUMERIC y llame al método **SQLGetData** con un *TargetType* argumento de SQL_ARD_TYPE, lo que hará que los valores de precisión y escala en los campos de descriptor para su uso.  
  
> [!NOTE]  
>  En ODBC 2*.x*, conjunto de aplicaciones *TargetType* SQL_C_DATE, SQL_C_TIME o SQL_C_TIMESTAMP para indicar que \* *TargetValuePtr* es una fecha, hora, o estructura de marca de tiempo. En ODBC 3*.x*, conjunto de aplicaciones *TargetType* SQL_C_TYPE_DATE, SQL_C_TYPE_TIME o SQL_C_TYPE_TIMESTAMP. El Administrador de controladores hace asignaciones adecuadas si es necesario, en función de la versión del controlador y la aplicación.  
  
## <a name="retrieving-variable-length-data-in-parts"></a>Recuperar datos de longitud Variable en partes  
 **SQLGetData** puede usarse para recuperar datos de una columna que contiene los datos de longitud variable en partes, es decir, cuando el identificador del tipo de datos SQL de la columna SQL_CHAR, SQL_VARCHAR, SQL_LONGVARCHAR, SQL_WCHAR, SQL_WVARCHAR, SQL_ WLONGVARCHAR, SQL_BINARY, SQL_VARBINARY, SQL_LONGVARBINARY o un identificador específico del controlador para un tipo de longitud variable.  
  
 Para recuperar datos de una columna en partes, la aplicación llama a **SQLGetData** varias veces en sucesión para la misma columna. En cada llamada, **SQLGetData** devuelve la parte siguiente de los datos. Depende de la aplicación para volver a ensamblar las partes, teniendo cuidado para quitar el carácter de terminación null de los elementos intermedios de datos de caracteres. Si hay más datos para devolver o no se asignó suficiente búfer para el carácter de terminación, **SQLGetData** devuelve SQL_SUCCESS_WITH_INFO y SQLSTATE 01004 (datos truncados). Cuando devuelve la última parte de los datos, **SQLGetData** devuelve SQL_SUCCESS. SQL_NO_TOTAL ni cero se puede devolver en la última llamada válida para recuperar datos de una columna, ya que la aplicación, a continuación, no tendría ninguna manera de saber la cantidad de los datos en el búfer de aplicación es válido. Si **SQLGetData** se llama después de esto, devuelve SQL_NO_DATA. Para obtener más información, vea la sección siguiente, "Recuperar los datos con SQLGetData".  
  
 Marcadores de longitud variable pueden devolverse en partes por **SQLGetData**. Al igual que con otros datos, una llamada a **SQLGetData** para devolver los marcadores de longitud variable en partes devolverá SQLSTATE 01004 (datos de cadena, truncados por la derecha) y SQL_SUCCESS_WITH_INFO cuando hay más datos que se va a devolver. Esto es diferente que el caso cuando un marcador de longitud variable se trunca mediante una llamada a **SQLFetch** o **SQLFetchScroll**, que devuelve SQL_ERROR y SQLSTATE 22001 (datos de cadena, truncados por la derecha).  
  
 **SQLGetData** no se puede usar para devolver datos de longitud fija en partes. Si **SQLGetData** es llama más de una vez en una fila para una columna que contiene datos de longitud fija, que devuelve SQL_NO_DATA para todas las llamadas después del primero.  
  
## <a name="retrieving-streamed-output-parameters"></a>Recuperar parámetros de salida transmitidos  
 Si un controlador es compatible con parámetros de salida transmitidos, una aplicación puede llamar a **SQLGetData** con una pequeña búfer muchas veces para recuperar un valor de parámetro grande. Para obtener más información sobre el parámetro de salida de transmisión por secuencias, vea [recuperar parámetros de salida mediante SQLGetData](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md).  
  
## <a name="retrieving-data-with-sqlgetdata"></a>Recuperar datos con SQLGetData  
 Para obtener datos de la columna especificada, **SQLGetData** realiza la siguiente secuencia de pasos:  
  
1.  Devuelve SQL_NO_DATA si ya ha devuelto todos los datos de la columna.  
  
2.  Conjuntos de \* *StrLen_or_IndPtr* en SQL_NULL_DATA si los datos son NULL. Si los datos son NULL y *StrLen_or_IndPtr* era un puntero nulo, **SQLGetData** devuelve SQLSTATE 22002 (variable de indicador necesaria pero no se ha proporcionado).  
  
     Si los datos de la columna no son NULL, **SQLGetData** continúa con el paso 3.  
  
3.  Si el atributo de instrucción SQL_ATTR_MAX_LENGTH se establece en un valor distinto de cero si la columna contiene datos de caracteres o binarios y si **SQLGetData** no se ha llamado anteriormente para la columna, los datos se truncan en SQL_ATTR_MAX_LENGTH bytes.  
  
    > [!NOTE]  
    >  El atributo de instrucción SQL_ATTR_MAX_LENGTH está pensado para reducir el tráfico de red. Generalmente se implementa mediante el origen de datos, que trunca los datos antes de devolverlo a través de la red. No están necesario controladores y orígenes de datos para admitirla. Por lo tanto, para garantizar que los datos se truncan a un tamaño específico, una aplicación debe asignar un búfer de ese tamaño y especifique el tamaño en el *BufferLength* argumento.  
  
4.  Convierte los datos en el tipo especificado en *TargetType*. Los datos se proporciona la precisión y escala predeterminadas para ese tipo de datos. Si *TargetType* es SQL_ARD_TYPE, los datos se utiliza el tipo en el campo SQL_DESC_CONCISE_TYPE de la descartar. Si *TargetType* es SQL_ARD_TYPE, los datos se proporcionan la precisión y escala en el SQL_DESC_DATETIME_INTERVAL_PRECISION, SQL_DESC_PRECISION, y escriba la SQL_DESC_CONCISE campos SQL_DESC_SCALE de descartar, dependiendo de los datos Campo e_scriba. Si cualquier valor predeterminado de precisión o escala no es adecuada, la aplicación debe establecer explícitamente el campo descriptor adecuado mediante una llamada a **SQLSetDescField** o **SQLSetDescRec**.  
  
5.  Si los datos se convierten a un tipo de datos de longitud variable, como carácter o binario, **SQLGetData** comprueba si se supera la longitud de los datos *BufferLength*. Si supera la longitud de datos de caracteres (incluido el carácter de terminación null) *BufferLength*, **SQLGetData** trunca los datos a *BufferLength* menos la longitud de un carácter de terminación null. A continuación, termina en null los datos. Si la longitud de datos binarios supera la longitud del búfer de datos, **SQLGetData** lo trunca a *BufferLength* bytes.  
  
     Si el búfer de datos proporcionado es demasiado pequeño para contener el carácter de terminación null, **SQLGetData** devuelve SQL_SUCCESS_WITH_INFO y SQLSTATE 01004.  
  
     **SQLGetData** nunca trunca los datos convierten en datos de longitud fija tipos; siempre se supone que la longitud de **TargetValuePtr* es el tamaño del tipo de datos.  
  
6.  Coloca los datos convertidos (y posiblemente truncados) en \* *TargetValuePtr*. Tenga en cuenta que **SQLGetData** no puede devolver datos fuera de línea.  
  
7.  Coloca la longitud de los datos de \* *StrLen_or_IndPtr*. Si *StrLen_or_IndPtr* era un puntero nulo, **SQLGetData** no devuelve la longitud.  
  
    -   Para caracteres o datos binarios, esto es la longitud de los datos después de la conversión y antes de truncamiento debido a *BufferLength*. Si el controlador no puede determinar la longitud de los datos después de la conversión, como sucede en ocasiones con datos de tipo long, se devuelve SQL_SUCCESS_WITH_INFO y establece la longitud en SQL_NO_TOTAL. (La última llamada a **SQLGetData** siempre debe devolver la longitud de los datos, no en cero o SQL_NO_TOTAL.) Si los datos se truncaron debido a la instrucción SQL_ATTR_MAX_LENGTH atributo, el valor de este atributo, en lugar de la longitud real, se coloca en \* *StrLen_or_IndPtr*. Esto es porque este atributo está diseñado para truncar los datos en el servidor antes de la conversión, por lo que el controlador no tiene ninguna manera de saber es qué la longitud real. Cuando **SQLGetData** se llama varias veces seguidas de la misma columna, ésta es la longitud de los datos disponibles al principio de la llamada actual; es decir, la longitud disminuye con cada llamada posterior.  
  
    -   Para todos los demás tipos de datos, esto es la longitud de los datos después de la conversión; es decir, es el tamaño del tipo al que se convierten los datos.  
  
8.  Si los datos se truncan sin pérdida de significado durante la conversión (por ejemplo, el número real 1,234 se trunca cuando se convierte en un entero de 1) o porque *BufferLength* es demasiado pequeño (por ejemplo, la cadena "abcdef" se coloca en un búfer de 4 bytes), **SQLGetData** devuelve SQLSTATE 01004 (datos truncados) y SQL_SUCCESS_WITH_INFO. Si los datos se truncan sin pérdida de significado debido a que el atributo de instrucción SQL_ATTR_MAX_LENGTH **SQLGetData** devuelve SQL_SUCCESS y no devuelve SQLSTATE 01004 (datos truncados).  
  
 El contenido del búfer de datos enlazados (si **SQLGetData** se llama en una columna dependiente) y el búfer de longitud/indicador son indefinidos si **SQLGetData** no devuelve SQL_SUCCESS o SQL_SUCCESS_WITH_INFO.  
  
 Las llamadas sucesivas a **SQLGetData** recuperará los datos de la última columna solicitada; desplazamientos anteriores dejan de ser válidos. Por ejemplo, cuando se realiza la siguiente secuencia:  
  
```  
SQLGetData(icol=n), SQLGetData(icol=m), SQLGetData(icol=n)  
```  
  
 la segunda llamada a SQLGetData(icol=n) recupera los datos desde el principio de la columna n. Cualquier posición de desplazamiento en los datos debido a las llamadas anteriores a **SQLGetData** para la columna ya no es válida.  
  
## <a name="descriptors-and-sqlgetdata"></a>Descriptores y SQLGetData  
 **SQLGetData** no interactúa directamente con los campos de descriptor.  
  
 Si *TargetType* es SQL_ARD_TYPE, los datos se utiliza el tipo en el campo SQL_DESC_CONCISE_TYPE de la descartar. Si *TargetType* es SQL_ARD_TYPE o SQL_C_DEFAULT, los datos se proporcionan la precisión y escala en el SQL_DESC_DATETIME_INTERVAL_PRECISION, SQL_DESC_PRECISION, y campos SQL_DESC_SCALE de descartar, según los datos de tipo en el campo SQL_DESC_CONCISE_TYPE.  
  
## <a name="code-example"></a>Ejemplo de código  
 En el ejemplo siguiente, se ejecuta una aplicación un **seleccione** instrucción para devolver un conjunto de resultados del cliente identificadores, nombres y ordenados por nombre, identificador y número de teléfono de números de teléfono. Para cada fila de datos, llama a **SQLFetch** para colocar el cursor a la fila siguiente. Llama **SQLGetData** para recuperar los datos capturados; los búferes de los datos y el número de bytes devuelto se especifican en la llamada a **SQLGetData**. Por último, se imprimen el número de teléfono, Id. y nombre de cada empleado.  
  
```  
#define NAME_LEN 50  
#define PHONE_LEN 50  
  
SQLCHAR      szName[NAME_LEN], szPhone[PHONE_LEN];  
SQLINTEGER   sCustID, cbName, cbAge, cbBirthday;  
SQLRETURN    retcode;  
SQLHSTMT     hstmt;  
  
retcode = SQLExecDirect(hstmt,  
   "SELECT CUSTID, NAME, PHONE FROM CUSTOMERS ORDER BY 2, 1, 3",  
   SQL_NTS);  
  
if (retcode == SQL_SUCCESS) {  
   while (TRUE) {  
      retcode = SQLFetch(hstmt);  
      if (retcode == SQL_ERROR || retcode == SQL_SUCCESS_WITH_INFO) {  
         show_error();  
      }  
      if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO){  
  
         /* Get data for columns 1, 2, and 3 */  
  
         SQLGetData(hstmt, 1, SQL_C_ULONG, &sCustID, 0, &cbCustID);  
         SQLGetData(hstmt, 2, SQL_C_CHAR, szName, NAME_LEN, &cbName);  
         SQLGetData(hstmt, 3, SQL_C_CHAR, szPhone, PHONE_LEN,  
            &cbPhone);  
  
         /* Print the row of data */  
  
         fprintf(out, "%-5d %-*s %*s", sCustID, NAME_LEN-1, szName,   
            PHONE_LEN-1, szPhone);  
      } else {  
         break;  
      }  
   }  
}  
```  
  
## <a name="related-functions"></a>Funciones relacionadas  
  
|Para obtener información acerca de|Vea|  
|---------------------------|---------|  
|Asignación de almacenamiento para una columna de un conjunto de resultados|[SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Realizar operaciones masivas que no hacen referencia a la posición del cursor de bloque|[SQLBulkOperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md)|  
|Cancelar el procesamiento de una instrucción|[SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Ejecutar una instrucción SQL|[SQLExecDirect](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|Ejecutar una instrucción SQL preparada|[SQLExecute](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|Captura un bloque de datos o desplazarse a través de un resultado de conjunto|[SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|Capturar una sola fila de datos o un bloque de datos en una dirección de solo avance|[SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|Envío de datos de parámetro en tiempo de ejecución|[SQLPutData](../../../odbc/reference/syntax/sqlputdata-function.md)|  
|Coloque el cursor, actualizar los datos en el conjunto de filas, o actualizar o eliminar datos en el conjunto de filas|[SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md)|  
  
## <a name="see-also"></a>Vea también  
 [Referencia de la API de ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Archivos de encabezado ODBC](../../../odbc/reference/install/odbc-header-files.md)   
 [Recuperar parámetros de salida mediante SQLGetData](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)
