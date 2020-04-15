---
title: Función SQLGetData ? Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ac11505b8e47dae8df53af27c64a7ee6372b3f28
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81285511"
---
# <a name="sqlgetdata-function"></a>Función SQLGetData
**Conformidad**  
 Versión introducida: Cumplimiento de normas ODBC 1.0: ISO 92  
  
 **Resumen**  
 **SQLGetData** recupera datos para una sola columna en el conjunto de resultados o para un único parámetro después **de SQLParamData** devuelve SQL_PARAM_DATA_AVAILABLE. Se puede llamar varias veces para recuperar datos de longitud variable en partes.  
  
## <a name="syntax"></a>Sintaxis  
  
```cpp  
  
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
 [Entrada] Para recuperar datos de columna, es el número de la columna para la que se devuelven datos. Las columnas del conjunto de resultados se numeran en orden de columna creciente a partir de 1. La columna de marcador es el número de columna 0; esto sólo se puede especificar si los marcadores están habilitados.  
  
 Para recuperar datos de parámetros, es el ordinal del parámetro, que comienza en 1.  
  
 *TargetType*  
 [Entrada] Identificador de tipo del tipo de datos C del búfer **TargetValuePtr.* Para obtener una lista de tipos de datos C válidos e identificadores de tipo, consulte la sección Tipos de [datos de C](../../../odbc/reference/appendixes/c-data-types.md) en Apéndice D: Tipos de datos.  
  
 Si *TargetType* es SQL_ARD_TYPE, el controlador utiliza el identificador de tipo especificado en el campo SQL_DESC_CONCISE_TYPE de la ARD. Si *TargetType* se SQL_APD_TYPE, **SQLGetData** usará el mismo tipo de datos C que se especificó en **SQLBindParameter**. De lo contrario, el tipo de datos de C especificado en **SQLGetData** reemplaza el tipo de datos de C especificado en **SQLBindParameter**. Si se SQL_C_DEFAULT, el controlador selecciona el tipo de datos C predeterminado en función del tipo de datos SQL del origen.  
  
 También puede especificar un tipo de datos C extendido. Para obtener más información, vea el tema sobre [tipos de datos C en ODBC](../../../odbc/reference/develop-app/c-data-types-in-odbc.md).  
  
 *TargetValuePtr*  
 [Salida] Puntero al búfer en el que se devolverán los datos.  
  
 *TargetValuePtr* no puede ser NULL.  
  
 *BufferLength*  
 [Entrada] Longitud del búfer **TargetValuePtr* en bytes.  
  
 El controlador utiliza *BufferLength* para evitar \*escribir más allá del final del búfer *TargetValuePtr* al devolver datos de longitud variable, como datos binarios o de caracteres. Tenga en cuenta que el controlador cuenta el \*carácter de terminación nula al devolver datos de caracteres a *TargetValuePtr*. *Por lo tanto, *TargetValuePtr* debe contener espacio para el carácter de terminación nula o el controlador truncará los datos.  
  
 Cuando el controlador devuelve datos de longitud fija, como un entero o una estructura de fecha, el controlador omite *BufferLength* y supone que el búfer es lo suficientemente grande como para contener los datos. Por lo tanto, es importante que la aplicación asigne un búfer lo suficientemente grande para los datos de longitud fija o el controlador escribirá más allá del final del búfer.  
  
 **SQLGetData** devuelve SQLSTATE HY090 (cadena no válida o longitud de búfer) cuando *BufferLength* es menor que 0 pero no cuando *BufferLength* es 0.  
  
 *StrLen_or_IndPtr*  
 [Salida] Puntero al búfer en el que se va a devolver la longitud o el valor del indicador. Si se trata de un puntero nulo, no se devuelve ningún valor de longitud o indicador. Esto devuelve un error cuando los datos que se capturan es NULL.  
  
 **SQLGetData** puede devolver los siguientes valores en el búfer de longitud/indicador:  
  
-   La longitud de los datos disponibles para devolver  
  
-   SQL_NO_TOTAL  
  
-   SQL_NULL_DATA  
  
 Para obtener más información, consulte Uso de valores de [longitud/indicador](../../../odbc/reference/develop-app/using-length-and-indicator-values.md) y "Comentarios" en este tema.  
  
## <a name="returns"></a>Devuelve  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NO_DATA, SQL_STILL_EXECUTING, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnóstico  
 Cuando **SQLGetData** devuelve SQL_ERROR o SQL_SUCCESS_WITH_INFO, se puede obtener un valor SQLSTATE asociado llamando a **SQLGetDiagRec** con un *HandleType* de SQL_HANDLE_STMT y un *control* de *StatementHandle*. En la tabla siguiente se enumeran los valores SQLSTATE devueltos normalmente por **SQLGetData** y se explica cada uno de ellos en el contexto de esta función; la notación "(DM)" precede a las descripciones de SQLSTATEs devueltas por el Administrador de controladores. El código de retorno asociado a cada valor SQLSTATE se SQL_ERROR, a menos que se indique lo contrario.  
  
|SQLSTATE|Error|Descripción|  
|--------------|-----------|-----------------|  
|01000|Advertencia general|Mensaje informativo específico del controlador. (La función devuelve SQL_SUCCESS_WITH_INFO.)|  
|01004|Datos de cadena truncados a la derecha|No todos los datos de la columna especificada, *Col_or_Param_Num*, se podrían recuperar en una sola llamada a la función. SQL_NO_TOTAL o la longitud de los datos restantes en la columna especificada antes \*de la llamada actual a **SQLGetData** se devuelve en *StrLen_or_IndPtr*. (La función devuelve SQL_SUCCESS_WITH_INFO.)<br /><br /> Para obtener más información sobre el uso de varias llamadas a **SQLGetData** para una sola columna, vea "Comentarios."|  
|01S07|Truncamiento fraccionario|Los datos devueltos para una o más columnas se truncaron. Para los tipos de datos numéricos, la parte fraccionaria del número se truncó. Para los tipos de datos time, timestamp e interval que contienen un componente de tiempo, la parte fraccionaria del tiempo se truncó.<br /><br /> (La función devuelve SQL_SUCCESS_WITH_INFO.)|  
|07006|Infracción de atributo de tipo de datos restringido|El valor de datos de una columna del conjunto de resultados no se puede convertir al tipo de datos de C especificado por el argumento *TargetType*.|  
|07009|Indice de descriptor no válido|El valor especificado para el *argumento Col_or_Param_Num* era 0 y el atributo de instrucción SQL_ATTR_USE_BOOKMARKS se estableció en SQL_UB_OFF.<br /><br /> El valor especificado para el argumento *Col_or_Param_Num* era mayor que el número de columnas del conjunto de resultados.<br /><br /> El valor *Col_or_Param_Num* no era igual al ordinal del parámetro que está disponible.<br /><br /> (DM) La columna especificada estaba enlazada. Esta descripción no se aplica a los controladores que devuelven la máscara de bits SQL_GD_BOUND para la opción SQL_GETDATA_EXTENSIONS en **SQLGetInfo**.<br /><br /> (DM) El número de la columna especificada era menor o igual que el número de la columna enlazada más alta. Esta descripción no se aplica a los controladores que devuelven la máscara de bits SQL_GD_ANY_COLUMN para la opción SQL_GETDATA_EXTENSIONS en **SQLGetInfo**.<br /><br /> (DM) la aplicación ya ha llamado **a SQLGetData** para la fila actual; el número de la columna especificada en la llamada actual era menor que el número de la columna especificada en la llamada anterior; y el controlador no devuelve la máscara de bits SQL_GD_ANY_ORDER para la opción SQL_GETDATA_EXTENSIONS en **SQLGetInfo**.<br /><br /> (DM) el argumento *TargetType* se SQL_ARD_TYPE y el registro descriptor *Col_or_Param_Num* de la ARD no pudo comprobar la coherencia.<br /><br /> (DM) el *TargetType* argumento era SQL_ARD_TYPE y el valor en el campo SQL_DESC_COUNT de la ARD era menor que el *Col_or_Param_Num* argumento.|  
|08S01|Fallo del enlace de comunicación|Error en el vínculo de comunicación entre el controlador y el origen de datos al que estaba conectado el controlador antes de que la función completara el procesamiento.|  
|22002|Variable indicador requerida pero no suministrada|*StrLen_or_IndPtr* era un puntero nulo y se recuperaron datos NULL.|  
|22003|Valor numérico fuera del rango|Devolver el valor numérico (como numérico o cadena) para la columna habría causado que se truncase la parte completa (en lugar de fraccionaria) del número.<br /><br /> Para obtener más información, consulte [Apéndice D: Tipos](../../../odbc/reference/appendixes/appendix-d-data-types.md)de datos .|  
|22007|Formato de fecha y hora no válido|La columna de caracteres del conjunto de resultados estaba enlazada a una estructura de fecha, hora o marca de tiempo de C, y el valor de la columna era una fecha, hora o marca de tiempo no válidas, respectivamente. Para obtener más información, consulte [Apéndice D: Tipos](../../../odbc/reference/appendixes/appendix-d-data-types.md)de datos .|  
|22012|División por cero|Se devolvió un valor de una expresión aritmética que dio lugar a la división por cero.|  
|22015|Desbordamiento de campo de intervalo|La asignación de un tipo SQL numérico o de intervalo exacto a un tipo de intervalo C causó una pérdida de dígitos significativos en el campo inicial.<br /><br /> Al devolver datos a un tipo de intervalo C, no había ninguna representación del valor del tipo SQL en el tipo de intervalo C.|  
|22018|Valor de carácter no válido para la especificación de conversión|Una columna de caracteres en el conjunto de resultados se devolvió a un búfer de caracteres C y la columna contenía un carácter para el que no había ninguna representación en el conjunto de caracteres del búfer.<br /><br /> El tipo C era un número exacto o aproximado, una fecha y hora o un tipo de datos de intervalo; el tipo SQL de la columna era un tipo de datos de carácter; y el valor de la columna no era un literal válido del tipo C enlazado.|  
|24000|Estado de cursor no válido|(DM) Se llamó a la función sin llamar primero a **SQLFetch** o **SQLFetchScroll** para colocar el cursor en la fila de datos necesaria.<br /><br /> (DM) *StatementHandle* estaba en un estado ejecutado, pero no se asoció ningún conjunto de resultados con *StatementHandle*.<br /><br /> Un cursor estaba abierto en el *StatementHandle* y **SQLFetch** o **SQLFetchScroll** se había llamado, pero el cursor se colocó antes del inicio del conjunto de resultados o después del final del conjunto de resultados.|  
|HY000|Error general|Se ha producido un error para el que no se ha definido sqlSTATE específico y para el que no se ha definido sqlSTATE específico de la implementación. El mensaje de error devuelto por **SQLGetDiagRec** en el *messageText* búfer describe el error y su causa.|  
|HY001|Error de asignación de memoria|El controlador no pudo asignar la memoria necesaria para admitir la ejecución o finalización de la función.|  
|HY003|Tipo de programa fuera de rango|(DM) el argumento *TargetType* no era un tipo de datos válido, SQL_C_DEFAULT, SQL_ARD_TYPE (en caso de recuperar datos de columna) o SQL_APD_TYPE (en caso de recuperar datos de parámetros).<br /><br /> (DM) el argumento *Col_or_Param_Num* era 0 y el argumento *TargetType* no se SQL_C_BOOKMARK para un marcador de longitud fija o SQL_C_VARBOOKMARK para un marcador de longitud variable.|  
|HY008|Operación cancelada|El procesamiento asincrónico se ha habilitado para *StatementHandle*. Se llamó a la función y antes de completar la ejecución, **sqlCancel** o **SQLCancelHandle** se llamó en el *StatementHandle*, y, a continuación, se llamó a la función de nuevo en el *StatementHandle*.<br /><br /> Se llamó a la función y, antes de completar la ejecución, **sqlCancel** o **SQLCancelHandle** se llamó en el *StatementHandle* desde un subproceso diferente en una aplicación multiproceso y, a continuación, se llamó a la función de nuevo en el *StatementHandle*.|  
|HY009|Uso no válido de puntero nulo|(DM) el argumento *TargetValuePtr* era un puntero nulo.|  
|HY010|Error de secuencia de funciones|(DM) el *StatementHandle* especificado no estaba en un estado ejecutado. Se llamó a la función sin llamar primero a **SQLExecDirect**, **SQLExecute** o una función de catálogo.<br /><br /> (DM) se llamó a una función de ejecución asincrónica para el identificador de conexión asociado a *StatementHandle*. Esta función asincrónica todavía se estaba ejecutando cuando se llamó a la función **SQLGetData** .<br /><br /> (DM) se llamó a una función de ejecución asincrónica (no esta) para el *StatementHandle* y todavía se estaba ejecutando cuando se llamó a esta función.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, o **SQLSetPos** se llamó para el *StatementHandle* y devuelto SQL_NEED_DATA. Se llamó a esta función antes de que se enviaran datos para todos los parámetros o columnas de datos en ejecución.<br /><br /> (DM) *StatementHandle* estaba en un estado ejecutado, pero no se asoció ningún conjunto de resultados con *StatementHandle*.<br /><br /> Una llamada a **SQLExeceute**, **SQLExecDirect**o **SQLMoreResults** devuelto SQL_PARAM_DATA_AVAILABLE, pero **SQLGetData** se llamó, en lugar de **SQLParamData**.|  
|HY013|Error de administración de memoria|No se pudo procesar la llamada de función porque no se pudo tener acceso a los objetos de memoria subyacentes, posiblemente debido a condiciones de poca memoria.|  
|HY090|Cadena no válida o longitud de búfer|(DM) el valor especificado para el argumento *BufferLength* era menor que 0.<br /><br /> El valor especificado para el argumento *BufferLength* era menor que 4, el argumento *Col_or_Param_Num* se estableció en 0 y el controlador era un controlador ODBC 2 *.x.*|  
|HY109|Posición del cursor no válida|El cursor se colocó (por **SQLSetPos**, **SQLFetch**, **SQLFetchScroll**o **SQLBulkOperations**) en una fila que se había eliminado o no se pudo recuperar.<br /><br /> El cursor era un cursor de solo avance y el tamaño del conjunto de filas era mayor que uno.|  
|HY117|La conexión se suspende debido al estado de transacción desconocido. Solo se permiten funciones de desconexión y de solo lectura.|(DM) Para obtener más información sobre el estado suspendido, vea [SqlEndTran (función).](../../../odbc/reference/syntax/sqlendtran-function.md)|  
|HYC00|Característica opcional no implementada|El controlador o el origen de datos no admite el uso de **SQLGetData** con varias filas en **SQLFetchScroll**. Esta descripción no se aplica a los controladores que devuelven la máscara de bits SQL_GD_BLOCK para la opción SQL_GETDATA_EXTENSIONS en **SQLGetInfo**.<br /><br /> El controlador o el origen de datos no admite la conversión especificada por la combinación del argumento *TargetType* y el tipo de datos SQL de la columna correspondiente. Este error solo se aplica cuando el tipo de datos SQL de la columna se asignó a un tipo de datos SQL específico del controlador.<br /><br /> El controlador solo admite ODBC 2 *.x*y el argumento *TargetType* era uno de los siguientes:<br /><br /> SQL_C_NUMERIC SQL_C_SBIGINT SQL_C_UBIGINT<br /><br /> y cualquiera de los tipos de datos de intervalo C enumerados en [C Tipos](../../../odbc/reference/appendixes/c-data-types.md) de datos en el Apéndice D: Tipos de datos.<br /><br /> El controlador solo admite versiones ODBC anteriores a 3.50 y el argumento *TargetType* se SQL_C_GUID.|  
|HYT01|Tiempo de espera de conexión expirado|El período de tiempo de espera de conexión expiró antes de que el origen de datos respondiera a la solicitud. El período de tiempo de espera de conexión se establece a través de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|El controlador no admite esta función|(DM) El controlador correspondiente a *StatementHandle* no admite la función.|  
|IM017|El sondeo está deshabilitado en el modo de notificación asincrónica|Siempre que se utiliza el modelo de notificación, el sondeo está deshabilitado.|  
|IM018|**SQLCompleteAsync** no se ha llamado para completar la operación asincrónica anterior en este identificador.|Si la llamada de función anterior en el identificador devuelve SQL_STILL_EXECUTING y si el modo de notificación está habilitado, **sqlCompleteAsync** debe llamarse en el identificador para realizar el procesamiento posterior y completar la operación.|  
  
## <a name="comments"></a>Comentarios  
 **SQLGetData** devuelve los datos de una columna especificada. SOLO se puede llamar a **SQLGetData** después de que **SQLFetch**, **SQLFetchScroll**o **SQLExtendedFetch**hayan obtenido una o varias filas del conjunto de resultados. Si los datos de longitud variable son demasiado grandes para devolverse en una sola llamada a **SQLGetData** (debido a una limitación en la aplicación), **SQLGetData** puede recuperarlos en partes. Es posible enlazar algunas columnas de una fila y llamar a **SQLGetData** para otros, aunque esto está sujeto a algunas restricciones. Para obtener más información, consulte [Obtención de datos largos](../../../odbc/reference/develop-app/getting-long-data.md).  
  
 Para obtener información sobre el uso de **SQLGetData** con parámetros de salida transmitidos, vea Recuperar parámetros de [salida mediante SQLGetData](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md).  
  
## <a name="using-sqlgetdata"></a>Uso de SQLGetData  
 Si el controlador no admite extensiones para **SQLGetData**, la función solo puede devolver datos para columnas sin enlazar con un número mayor que el de la última columna enlazada. Además, dentro de una fila de datos, el valor del *Col_or_Param_Num* argumento en cada llamada a **SQLGetData** debe ser mayor o igual que el valor de *Col_or_Param_Num* en la llamada anterior; es decir, los datos deben recuperarse en el orden creciente del número de columna. Por último, si no se admite ninguna extensión, no se puede llamar a **SQLGetData** si el tamaño del conjunto de filas es mayor que 1.  
  
 Los conductores pueden relajarse cualquiera de estas restricciones. Para determinar qué restricciones relaja un controlador, una aplicación llama a **SQLGetInfo** con cualquiera de las siguientes opciones de SQL_GETDATA_EXTENSIONS:  
  
-   SQL_GD_OUTPUT_PARAMS se puede llamar a **SQLGetData** para devolver valores de parámetro de salida. Para obtener más información, vea el tema que trata sobre [recuperar parámetros de salida mediante SQLGetData](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md).  
  
-   SQL_GD_ANY_COLUMN. Si se devuelve esta opción, **SQLGetData** se puede llamar para cualquier columna sin enlazar, incluidas las anteriores a la última columna enlazada.  
  
-   SQL_GD_ANY_ORDER. Si se devuelve esta opción, **SQLGetData** se puede llamar para las columnas sin enlazar en cualquier orden.  
  
-   SQL_GD_BLOCK. Si **SQLGetInfo** devuelve esta opción para el SQL_GETDATA_EXTENSIONS InfoType, el controlador admite llamadas a **SQLGetData** cuando el tamaño del conjunto de filas es mayor que 1 y la aplicación puede llamar a **SQLSetPos** con la opción SQL_POSITION para colocar el cursor en la fila correcta antes de llamar a **SQLGetData.**  
  
-   SQL_GD_BOUND. Si se devuelve esta opción, **SQLGetData** se puede llamar para las columnas enlazadas, así como las columnas sin enlazar.  
  
 Hay dos excepciones a estas restricciones y la capacidad de un conductor para relajarlas. En primer lugar, **SQLGetData** nunca debe llamarse para un cursor de solo avance cuando el tamaño del conjunto de filas es mayor que 1. En segundo lugar, si un controlador admite marcadores, siempre debe admitir la capacidad de llamar a **SQLGetData** para la columna 0, incluso si no permite que las aplicaciones llamen a **SQLGetData** para otras columnas antes de la última columna enlazada. (Cuando una aplicación está trabajando con un controlador ODBC 2 *.x,* **SQLGetData** devolverá correctamente un marcador cuando se llama con *Col_or_Param_Num* igual a 0 después de una llamada a **SQLFetch**, porque **SQLFetch** se asigna mediante el Administrador de controladores ODBC 3 *.x* a **SQLExtendedFetch** con un *FetchOrientation* de SQL_FETCH_NEXT y **SQLGetData** con un *Col_or_Param_Num* de 0 se asigna mediante el Administrador de controladores ODBC 3 *.x* a **SQLGetStmtOption** con un *fOption* de SQL_GET_BOOKMARK.)  
  
 **SQLGetData** no se puede usar para recuperar el marcador de una fila insertada mediante una llamada a **SQLBulkOperations** con la opción SQL_ADD, porque el cursor no se coloca en la fila. Una aplicación puede recuperar el marcador para una fila de este tipo mediante el enlace de la columna 0 antes de llamar a **SQLBulkOperations** con SQL_ADD, en cuyo caso **SQLBulkOperations** devuelve el marcador en el búfer enlazado. **SQLFetchScroll,** a continuación, se puede llamar con SQL_FETCH_BOOKMARK para cambiar la posición del cursor en esa fila.  
  
 Si el argumento *TargetType* es un tipo de datos de intervalo, se utilizan para los datos la precisión inicial del intervalo predeterminado (2) y la precisión de segundos de intervalo predeterminada (6), tal como se establece en los campos SQL_DESC_DATETIME_INTERVAL_PRECISION y SQL_DESC_PRECISION de la ARD, respectivamente. Si el *TargetType* argumento es un tipo de datos SQL_C_NUMERIC, la precisión predeterminada (definido por el controlador) y la escala predeterminada (0), como se establece en el SQL_DESC_PRECISION y SQL_DESC_SCALE campos de la ARD, se utilizan para los datos. Si alguna precisión o escala predeterminada no es adecuada, la aplicación debe establecer explícitamente el campo descriptor adecuado mediante una llamada a **SQLSetDescField** o **SQLSetDescRec**. Puede establecer el campo SQL_DESC_CONCISE_TYPE para SQL_C_NUMERIC y llamar a **SQLGetData** con un *TargetType* argumento de SQL_ARD_TYPE, lo que hará que se usen los valores de precisión y escala en los campos descriptores.  
  
> [!NOTE]
>  En ODBC 2 *.x*, las aplicaciones establecen *TargetType* en SQL_C_DATE, SQL_C_TIME o SQL_C_TIMESTAMP para indicar que \* *TargetValuePtr* es una estructura de fecha, hora o marca de tiempo. En ODBC 3 *.x*, las aplicaciones establecen *TargetType* en SQL_C_TYPE_DATE, SQL_C_TYPE_TIME o SQL_C_TYPE_TIMESTAMP. El Administrador de controladores realiza las asignaciones adecuadas si es necesario, en función de la aplicación y la versión del controlador.  
  
## <a name="retrieving-variable-length-data-in-parts"></a>Recuperación de datos de longitud variable en piezas  
 **SQLGetData** se puede usar para recuperar datos de una columna que contiene datos de longitud variable en partes, es decir, cuando el identificador del tipo de datos SQL de la columna está SQL_CHAR, SQL_VARCHAR, SQL_LONGVARCHAR, SQL_WCHAR, SQL_WVARCHAR, SQL_WLONGVARCHAR, SQL_BINARY, SQL_VARBINARY, SQL_LONGVARBINARY o un identificador específico del controlador para un tipo de longitud variable.  
  
 Para recuperar datos de una columna en partes, la aplicación llama a **SQLGetData** varias veces consecutivas para la misma columna. En cada llamada, **SQLGetData** devuelve la siguiente parte de los datos. Depende de la aplicación volver a ensamblar las partes, teniendo cuidado de quitar el carácter de terminación nula de las partes intermedias de los datos de caracteres. Si hay más datos que devolver o no se asignó suficiente búfer para el carácter de terminación, **SQLGetData** devuelve SQL_SUCCESS_WITH_INFO y SQLSTATE 01004 (datos truncados). Cuando devuelve la última parte de los datos, **SQLGetData** devuelve SQL_SUCCESS. Ni SQL_NO_TOTAL ni cero se pueden devolver en la última llamada válida para recuperar datos de una columna, porque la aplicación no tendría forma de saber cuánto de los datos en el búfer de la aplicación es válido. Si **SQLGetData** se llama después de esto, devuelve SQL_NO_DATA. Para obtener más información, vea la sección siguiente, "Recuperar datos con SQLGetData."  
  
 **SQLGetData**puede devolver marcadores de longitud variable en partes. Al igual que con otros datos, una llamada a **SQLGetData** para devolver marcadores de longitud variable en partes devolverá SQLSTATE 01004 (datos de cadena, truncados a la derecha) y SQL_SUCCESS_WITH_INFO cuando haya más datos que devolver. Esto es diferente del caso cuando un marcador de longitud variable se trunca mediante una llamada a **SQLFetch** o **SQLFetchScroll**, que devuelve SQL_ERROR y SQLSTATE 22001 (datos de cadena, truncados a la derecha).  
  
 **SQLGetData** no se puede usar para devolver datos de longitud fija en partes. Si **SQLGetData** se llama más de una vez en una fila para una columna que contiene datos de longitud fija, devuelve SQL_NO_DATA para todas las llamadas después de la primera.  
  
## <a name="retrieving-streamed-output-parameters"></a>Recuperación de parámetros de salida transmitidos  
 Si un controlador admite parámetros de salida transmitidos, una aplicación puede llamar a **SQLGetData** con un búfer pequeño muchas veces para recuperar un valor de parámetro grande. Para obtener más información acerca del parámetro de salida transmitido, vea Recuperar parámetros de [salida mediante SQLGetData](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md).  
  
## <a name="retrieving-data-with-sqlgetdata"></a>Recuperación de datos con SQLGetData  
 Para devolver datos para la columna especificada, **SQLGetData** realiza la siguiente secuencia de pasos:  
  
1.  Devuelve SQL_NO_DATA si ya ha devuelto todos los datos de la columna.  
  
2.  Establece \* *StrLen_or_IndPtr* en SQL_NULL_DATA si los datos son NULL. Si los datos son NULL y *StrLen_or_IndPtr* era un puntero nulo, **SQLGetData** devuelve SQLSTATE 22002 (variable de indicador necesaria pero no proporcionada).  
  
     Si los datos de la columna no son NULL, **SQLGetData** continúa con el paso 3.  
  
3.  Si el atributo de instrucción SQL_ATTR_MAX_LENGTH se establece en un valor distinto de cero, si la columna contiene datos binarios o de caracteres y si **SQLGetData** no se ha llamado previamente para la columna, los datos se truncan en SQL_ATTR_MAX_LENGTH bytes.  
  
    > [!NOTE]  
    >  El atributo de instrucción SQL_ATTR_MAX_LENGTH está diseñado para reducir el tráfico de red. Generalmente lo implementa el origen de datos, que trunca los datos antes de devolverlos a través de la red. Los controladores y las fuentes de datos no son necesarios para admitirlo. Por lo tanto, para garantizar que los datos se truncan a un tamaño determinado, una aplicación debe asignar un búfer de ese tamaño y especificar el tamaño en el *BufferLength* argumento.  
  
4.  Convierte los datos al tipo especificado en *TargetType*. Los datos reciben la precisión y la escala predeterminadas para ese tipo de datos. Si *TargetType* es SQL_ARD_TYPE, se utiliza el tipo de datos en el campo SQL_DESC_CONCISE_TYPE de la ARD. Si *TargetType* se SQL_ARD_TYPE, los datos reciben la precisión y la escala en los campos SQL_DESC_DATETIME_INTERVAL_PRECISION, SQL_DESC_PRECISION y SQL_DESC_SCALE del ARD, según el tipo de datos del campo SQL_DESC_CONCISE_TYPE. Si alguna precisión o escala predeterminada no es adecuada, la aplicación debe establecer explícitamente el campo descriptor adecuado mediante una llamada a **SQLSetDescField** o **SQLSetDescRec**.  
  
5.  Si los datos se han convertido en un tipo de datos de longitud variable, como carácter o binario, **SQLGetData** comprueba si la longitud de los datos supera *BufferLength*. Si la longitud de los datos de caracteres (incluido el carácter de terminación null) supera *BufferLength*, **SQLGetData** trunca los datos a *BufferLength* menos la longitud de un carácter de terminación nula. A continuación, termina en null los datos. Si la longitud de los datos binarios supera la longitud del búfer de datos, **SQLGetData** lo trunca a bytes *BufferLength.*  
  
     Si el búfer de datos proporcionado es demasiado pequeño para contener el carácter de terminación nula, **SQLGetData** devuelve SQL_SUCCESS_WITH_INFO y SQLSTATE 01004.  
  
     **SQLGetData** nunca trunca los datos convertidos en tipos de datos de longitud fija; siempre asume que la longitud de **TargetValuePtr* es el tamaño del tipo de datos.  
  
6.  Coloca los datos convertidos (y \*posiblemente truncados) en *TargetValuePtr*. Tenga en cuenta que **SQLGetData** no puede devolver datos fuera de línea.  
  
7.  Coloca la longitud de \*los datos en *StrLen_or_IndPtr*. Si *StrLen_or_IndPtr* era un puntero nulo, **SQLGetData** no devuelve la longitud.  
  
    -   Para datos binarios o de caracteres, esta es la longitud de los datos después de la conversión y antes del truncamiento debido a *BufferLength*. Si el controlador no puede determinar la longitud de los datos después de la conversión, como suele ser el caso de los datos largos, devuelve SQL_SUCCESS_WITH_INFO y establece la longitud en SQL_NO_TOTAL. (La última llamada a **SQLGetData** siempre debe devolver la longitud de los datos, no cero o SQL_NO_TOTAL.) Si los datos se truncaron debido al atributo de instrucción SQL_ATTR_MAX_LENGTH, el valor \*de este atributo, a diferencia de la longitud real, se coloca en *StrLen_or_IndPtr*. Esto se debe a que este atributo está diseñado para truncar los datos en el servidor antes de la conversión, por lo que el controlador no tiene forma de averiguar cuál es la longitud real. Cuando **SQLGetData** se llama varias veces consecutivas para la misma columna, esta es la longitud de los datos disponibles al principio de la llamada actual; es decir, la longitud disminuye con cada llamada posterior.  
  
    -   Para todos los demás tipos de datos, esta es la longitud de los datos después de la conversión; es decir, es el tamaño del tipo al que se convirtieron los datos.  
  
8.  Si los datos se truncan sin pérdida de importancia durante la conversión (por ejemplo, el número real 1.234 se trunca cuando se convierte en el entero 1) o porque *BufferLength* es demasiado pequeño (por ejemplo, la cadena "abcdef" se coloca en un búfer de 4 bytes), **SQLGetData** devuelve SQLSTATE 01004 (Data truncated) y SQL_SUCCESS_WITH_INFO. Si los datos se truncan sin pérdida de importancia debido al atributo de instrucción SQL_ATTR_MAX_LENGTH, **SQLGetData** devuelve SQL_SUCCESS y no devuelve SQLSTATE 01004 (datos truncados).  
  
 El contenido del búfer de datos enlazado (si **SQLGetData** se llama en una columna enlazada) y el búfer de longitud/indicador son indefinidos si **SQLGetData** no devuelve SQL_SUCCESS o SQL_SUCCESS_WITH_INFO.  
  
 Las llamadas sucesivas a **SQLGetData** recuperarán los datos de la última columna solicitada; los desplazamientos anteriores se vuelven inválidos. Por ejemplo, cuando se realiza la siguiente secuencia:  
  
```cpp  
SQLGetData(icol=n), SQLGetData(icol=m), SQLGetData(icol=n)  
```  
  
 la segunda llamada a SQLGetData(icol-n) recupera datos desde el inicio de la columna n. Cualquier desplazamiento en los datos debido a llamadas anteriores a **SQLGetData** para la columna ya no es válido.  
  
## <a name="descriptors-and-sqlgetdata"></a>Descriptores y SQLGetData  
 **SQLGetData** no interactúa directamente con ningún campo descriptor.  
  
 Si *TargetType* es SQL_ARD_TYPE, se utiliza el tipo de datos en el campo SQL_DESC_CONCISE_TYPE de la ARD. Si *TargetType* es SQL_ARD_TYPE o SQL_C_DEFAULT, los datos reciben la precisión y la escala en los campos SQL_DESC_DATETIME_INTERVAL_PRECISION, SQL_DESC_PRECISION y SQL_DESC_SCALE del ARD, según el tipo de datos del campo SQL_DESC_CONCISE_TYPE.  
  
## <a name="code-example"></a>Ejemplo de código  
 En el ejemplo siguiente, una aplicación ejecuta una instrucción **SELECT** para devolver un conjunto de resultados de los identificadores de cliente, los nombres y los números de teléfono ordenados por nombre, identificador y número de teléfono. Para cada fila de datos, llama a **SQLFetch** para colocar el cursor en la fila siguiente. Llama a **SQLGetData** para recuperar los datos capturados; los búferes de los datos y el número devuelto de bytes se especifican en la llamada a **SQLGetData**. Por último, imprime el nombre, el ID y el número de teléfono de cada empleado.  
  
```cpp  
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
  
|Para información acerca de|Vea|  
|---------------------------|---------|  
|Asignación de almacenamiento para una columna en un conjunto de resultados|[SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Realizar operaciones masivas que no se relacionan con la posición del cursor de bloque|[SQLBulkOperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md)|  
|Cancelación del procesamiento de extractos|[SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Ejecución de una instrucción SQL|[SQLExecDirect](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|Ejecución de una instrucción SQL preparada|[SQLExecute](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|Obtención de un bloque de datos o desplazamiento por un conjunto de resultados|[SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|Obtención de una sola fila de datos o un bloque de datos en una dirección de solo avance|[SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|Envío de datos de parámetros en tiempo de ejecución|[SQLPutData](../../../odbc/reference/syntax/sqlputdata-function.md)|  
|Colocación del cursor, actualización de datos en el conjunto de filas o actualización o eliminación de datos en el conjunto de filas|[SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md)|  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de la API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Archivos de encabezado ODBC](../../../odbc/reference/install/odbc-header-files.md)   
 [Recuperar parámetros de salida mediante SQLGetData](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)
