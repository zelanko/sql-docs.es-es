---
title: Función SQLGetData | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 70ee26274d101d1b18b00c83a89bd0c946da6742
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47855823"
---
# <a name="sqlgetdata-function"></a>Función SQLGetData
**Conformidad**  
 Versión introdujo: Cumplimiento de estándares 1.0 de ODBC: 92 ISO  
  
 **Resumen**  
 **SQLGetData** recupera datos de una sola columna del conjunto de resultados o para un único parámetro después **SQLParamData** devuelve SQL_PARAM_DATA_AVAILABLE. Se puede llamar varias veces para recuperar datos de longitud variable en partes.  
  
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
 [Entrada] Para recuperar datos de columna, es el número de la columna que se va a devolver los datos. Columnas del conjunto de resultados se numeran en orden creciente de columna que empieza por 1. La columna de marcador es el número de columna 0; Esto puede ser especificado sólo si están habilitados los marcadores.  
  
 Para recuperar los datos de parámetro, es el ordinal del parámetro, que comienza en 1.  
  
 *TargetType*  
 [Entrada] El identificador de tipo del tipo de datos C de la **TargetValuePtr* búfer. Para obtener una lista de tipos de datos válidos de C y los identificadores de tipo, consulte el [tipos de datos C](../../../odbc/reference/appendixes/c-data-types.md) sección en el apéndice D: tipos de datos.  
  
 Si *TargetType* es SQL_ARD_TYPE, lo controladores utiliza el identificador del tipo especificado en el campo SQL_DESC_CONCISE_TYPE del descartar. Si *TargetType* es SQL_APD_TYPE, **SQLGetData** usará el mismo tipo de datos de C que se especificó en **SQLBindParameter**. En caso contrario, se especifica el tipo de datos C en **SQLGetData** invalida especificado en el tipo de datos de C **SQLBindParameter**. Si es SQL_C_DEFAULT, el controlador selecciona el tipo de datos C predeterminado según el tipo de datos SQL del origen.  
  
 También puede especificar un tipo de datos C extendido. Para obtener más información, consulte [tipos de datos C en ODBC](../../../odbc/reference/develop-app/c-data-types-in-odbc.md).  
  
 *TargetValuePtr*  
 [Salida] Puntero al búfer en el que se va a devolver los datos.  
  
 *TargetValuePtr* no puede ser NULL.  
  
 *BufferLength*  
 [Entrada] Longitud de la **TargetValuePtr* búfer en bytes.  
  
 El controlador utiliza *BufferLength* para evitar escribir más allá del final de la \* *TargetValuePtr* al devolver datos de longitud variable, como datos binarios o de carácter del búfer. Tenga en cuenta que el controlador cuenta el carácter de terminación null cuando se devuelven los datos de caracteres a \* *TargetValuePtr*. **TargetValuePtr* debe contener por lo tanto espacio para el carácter de terminación null, o el controlador se truncarán los datos.  
  
 Cuando el controlador devuelve datos de longitud fija, como un entero o una estructura de fecha, el controlador omite *BufferLength* y asume que el búfer es suficientemente grande como para contener los datos. Por lo tanto, es importante para la aplicación asignar un búfer suficientemente grande como para los datos de longitud fija o escribirá el controlador más allá del final del búfer.  
  
 **SQLGetData** devuelve SQLSTATE HY090 (longitud de búfer o cadena no válida) cuando *BufferLength* es menor que 0 pero no cuando *BufferLength* es 0.  
  
 *StrLen_or_IndPtr*  
 [Salida] Puntero al búfer en el que se va a devolver el valor de longitud o indicador. Si se trata de un puntero nulo, no se devuelve ningún valor de longitud o indicador. Esto devuelve un error cuando los datos se capturan los están NULL.  
  
 **SQLGetData** puede devolver los valores siguientes en el búfer de longitud/indicador:  
  
-   La longitud de los datos disponibles para devolver  
  
-   SQL_NO_TOTAL  
  
-   SQL_NULL_DATA  
  
 Para obtener más información, consulte [con valores de longitud/indicador](../../../odbc/reference/develop-app/using-length-and-indicator-values.md) y "Comentarios" en este tema.  
  
## <a name="returns"></a>Devuelve  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NO_DATA, SQL_STILL_EXECUTING, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Cuando **SQLGetData** devuelve SQL_ERROR o SQL_SUCCESS_WITH_INFO, un valor SQLSTATE asociado se puede obtener mediante una llamada a **SQLGetDiagRec** con un *HandleType* de SQL_HANDLE_STMT y un *controlar* de *StatementHandle*. En la tabla siguiente se enumera los valores SQLSTATE devueltos normalmente por **SQLGetData** y se explica cada uno de ellos en el contexto de esta función; la notación "(DM)" precede a las descripciones de SQLSTATE devuelto por el Administrador de controladores. El código de retorno asociado a cada valor SQLSTATE es SQL_ERROR, a menos que se indique lo contrario.  
  
|SQLSTATE|Error|Descripción|  
|--------------|-----------|-----------------|  
|01000|Advertencia general|Específico del controlador de mensaje informativo. (La función devuelve SQL_SUCCESS_WITH_INFO).|  
|01004|Datos de cadena derecha truncados|No todos los datos de la columna especificada, *Col_or_Param_Num*, se recuperaron en una sola llamada a la función. SQL_NO_TOTAL o la longitud de los datos restantes de la columna especificada antes de la llamada actual a **SQLGetData** se devuelve en \* *StrLen_or_IndPtr*. (La función devuelve SQL_SUCCESS_WITH_INFO).<br /><br /> Para obtener más información sobre el uso de varias llamadas a **SQLGetData** para una sola columna, vea "Comentarios".|  
|01S07|Truncamiento fraccionario|Se truncaron los datos devueltos para una o varias columnas. Para los tipos de datos numéricos, se ha truncado la parte fraccionaria del número. De hora, marca de tiempo y los tipos de datos de intervalo que contiene un componente de tiempo, se trunca la parte fraccionaria del tiempo.<br /><br /> (La función devuelve SQL_SUCCESS_WITH_INFO).|  
|07006|Infracción del atributo de tipo de datos restringido|El valor de datos de una columna del conjunto de resultados no se puede convertir al tipo de datos C especificado por el argumento *TargetType*.|  
|07009|Índice de descriptor no válido|El valor especificado para el argumento *Col_or_Param_Num* era 0 y se ha establecido el atributo de instrucción SQL_ATTR_USE_BOOKMARKS a SQL_UB_OFF.<br /><br /> El valor especificado para el argumento *Col_or_Param_Num* era mayor que el número de columnas del conjunto de resultados.<br /><br /> El *Col_or_Param_Num* valor no era igual en el ordinal del parámetro que está disponible.<br /><br /> (DM) se ha enlazado la columna especificada. Esta descripción no es aplicable a los controladores que devuelven la máscara de bits SQL_GD_BOUND para la opción SQL_GETDATA_EXTENSIONS en **SQLGetInfo**.<br /><br /> (DM) el número de la columna especificada era menor o igual al número de la columna dependiente más alto. Esta descripción no es aplicable a los controladores que devuelven la máscara de bits SQL_GD_ANY_COLUMN para la opción SQL_GETDATA_EXTENSIONS en **SQLGetInfo**.<br /><br /> (DM) la aplicación ha llamado ya **SQLGetData** para la fila actual; el número de la columna especificada en la llamada actual es menor que el número de la columna especificada en la llamada anterior; y el controlador no devuelve el SQL_ Máscara de bits GD_ANY_ORDER para la opción SQL_GETDATA_EXTENSIONS en **SQLGetInfo**.<br /><br /> (DM) el *TargetType* argumento era SQL_ARD_TYPE y el *Col_or_Param_Num* error de registro del descriptor de la descartar la comprobación de coherencia.<br /><br /> (DM) el *TargetType* argumento era SQL_ARD_TYPE y el valor del campo SQL_DESC_COUNT de la descartar era menor que el *Col_or_Param_Num* argumento.|  
|08S01|Error de vínculo de comunicación|Error en el vínculo de comunicación entre el controlador y el origen de datos a la que se ha conectado el controlador antes del procesamiento de la función se ha completado.|  
|22002|Variable de indicador necesaria pero no proporcionado|*StrLen_or_IndPtr* era un puntero nulo y se recuperaron datos NULL.|  
|22003|Valor numérico fuera del intervalo|Devuelve el valor numérico (como numérico o cadena) para la columna habría causado la parte entera (en contraposición a fraccionarios) del número que se va a truncar.<br /><br /> Para obtener más información, consulte [apéndice D: tipos de datos](../../../odbc/reference/appendixes/appendix-d-data-types.md).|  
|22007|Formato de datetime no válido|La columna de caracteres del conjunto de resultados se enlazó a una fecha, hora o marca de tiempo estructura de C y el valor de la columna era una fecha no válida, la hora o marca de tiempo, respectivamente. Para obtener más información, consulte [apéndice D: tipos de datos](../../../odbc/reference/appendixes/appendix-d-data-types.md).|  
|22012|División por cero|Se devolvió un valor de una expresión aritmética que dan como resultado de división por cero.|  
|22015|Desbordamiento de campo de intervalo|Asignación de un valor numérico exacto o el intervalo de tipo SQL a un tipo de intervalo C causó una pérdida de dígitos significativos en el campo inicial.<br /><br /> Cuando se devuelven datos a un tipo de intervalo de C, no hubo ninguna representación del valor del tipo SQL en el tipo de intervalo C.|  
|22018|Valor de carácter no válido para especificación cast|Se devolvió una columna de caracteres del conjunto de resultados a un búfer de caracteres de C y la columna contiene un carácter para el que se ha producido ninguna representación en el juego de caracteres del búfer.<br /><br /> El tipo C era un numérico exacto o aproximado, una fecha y hora o un tipo de datos del intervalo; el tipo SQL de la columna era un tipo de datos de caracteres; y el valor de la columna no es un literal válido de tipo C enlazado.|  
|24000|Estado de cursor no válido|(DM) que se llamó la función sin llamar primero a **SQLFetch** o **SQLFetchScroll** para colocar el cursor en la fila de datos necesarios.<br /><br /> (DM) el *StatementHandle* estaba en un estado ejecutado, pero se ha asociado ningún conjunto de resultados la *StatementHandle*.<br /><br /> Un cursor estaba abierto en el *StatementHandle* y **SQLFetch** o **SQLFetchScroll** hubiera llamado, pero el cursor se coloca antes del inicio del conjunto de resultados o después de la fin del conjunto de resultados.|  
|HY000|Error general|Se produjo un error para que se ha producido ningún SQLSTATE específico y para los que se ha definido ningún SQLSTATE específicos de la implementación. El mensaje de error devuelto por **SQLGetDiagRec** en el *MessageText* búfer describe el error y su causa.|  
|HY001|Error de asignación de memoria|El controlador no pudo asignar la memoria necesaria para admitir la ejecución o la finalización de la función.|  
|HY003|Tipo de programa fuera del intervalo|(DM) el argumento *TargetType* no era un tipo de datos válido, SQL_C_DEFAULT, SQL_ARD_TYPE (en caso de recuperación de datos de columna) o SQL_APD_TYPE (en caso de recuperación de datos de parámetro).<br /><br /> (DM) el argumento *Col_or_Param_Num* era 0 y el argumento *TargetType* no era SQL_C_BOOKMARK para un marcador de longitud fija o SQL_C_VARBOOKMARK de un marcador de longitud variable.|  
|HY008|Operación cancelada|Procesamiento asincrónico se habilitó para la *StatementHandle*. Se llamó a la función, y antes que completó la ejecución, **SQLCancel** o **SQLCancelHandle** se ha llamado en el *StatementHandle*, y, a continuación, se llamó a la función nuevo en el *StatementHandle*.<br /><br /> Se llamó a la función, y antes que completó la ejecución, **SQLCancel** o **SQLCancelHandle** se ha llamado en el *StatementHandle* desde un subproceso diferente en un aplicación multiproceso y, a continuación, la función se llamó de nuevo en el *StatementHandle*.|  
|HY009|Uso no válido del puntero nulo|(DM) el argumento *TargetValuePtr* era un puntero nulo.|  
|HY010|Error de secuencia de función|(DM) especificado *StatementHandle* no estaba en un estado ejecutado. Se llamó a la función sin llamar primero a **SQLExecDirect**, **SQLExecute** o una función de catálogo.<br /><br /> (DM) se llamó a una función que se ejecuta de forma asincrónica para el identificador de conexión que está asociado el *StatementHandle*. Aún estaba ejecutando esta función asincrónica cuando el **SQLGetData** se llamó a la función.<br /><br /> (DM) se llamó a una función que se ejecuta asincrónicamente (no ésta) para el *StatementHandle* y aún se estaba ejecutando cuando se llamó a esta función.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, o **SQLSetPos** se llamó para el  *StatementHandle* y devuelve SQL_NEED_DATA. Esta función se invoca antes de que se enviaron datos para todas las columnas o parámetros de datos en ejecución.<br /><br /> (DM) el *StatementHandle* estaba en un estado ejecutado, pero se ha asociado ningún conjunto de resultados la *StatementHandle*.<br /><br /> Una llamada a **SQLExeceute**, **SQLExecDirect**, o **SQLMoreResults** devuelve SQL_PARAM_DATA_AVAILABLE, pero **SQLGetData** llamó , en lugar de **SQLParamData**.|  
|HY013|Error de administración de memoria|No se pudo procesar la llamada de función porque los objetos de memoria subyacente no se podrían tener acceso, posiblemente debido a memoria insuficiente.|  
|HY090|Longitud de búfer o cadena no válida|(DM) el valor especificado para el argumento *BufferLength* era menor que 0.<br /><br /> El valor especificado para el argumento *BufferLength* fue inferior a 4, el *Col_or_Param_Num* argumento se establece en 0 y el controlador fue un 2 de ODBC *.x* controlador.|  
|HY109|Posición del cursor no válido|Se coloca el cursor (por **SQLSetPos**, **SQLFetch**, **SQLFetchScroll**, o **SQLBulkOperations**) en una fila que se había eliminada o no se pudo obtener.<br /><br /> El cursor estaba un cursor de solo avance y el tamaño del conjunto de filas es mayor que uno.|  
|HY117|Conexión está suspendida debido al estado de transacción desconocido. Solo se desconecte y se permiten funciones de solo lectura.|(DM) para obtener más información sobre el estado suspendido, consulte [función SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Característica opcional no implementada|El controlador u origen de datos no admite el uso de **SQLGetData** con varias filas en **SQLFetchScroll**. Esta descripción no es aplicable a los controladores que devuelven la máscara de bits SQL_GD_BLOCK para la opción SQL_GETDATA_EXTENSIONS en **SQLGetInfo**.<br /><br /> El controlador u origen de datos no admite la conversión especificada por la combinación de la *TargetType* argumento y el tipo de datos SQL de la columna correspondiente. Este error se aplica solo cuando el tipo de datos SQL de la columna se asignó a un tipo de datos SQL específicas del controlador.<br /><br /> El controlador admite solo ODBC 2 *.x*y el argumento *TargetType* fue uno de los siguientes:<br /><br /> SQL_C_NUMERIC SQL_C_SBIGINT SQL_C_UBIGINT<br /><br /> y cualquiera de los tipos de datos C de intervalo que aparecen en [tipos de datos C](../../../odbc/reference/appendixes/c-data-types.md) en Apéndice D: tipos de datos.<br /><br /> El controlador sólo es compatible con versiones ODBC antes de 3,50 y el argumento *TargetType* era SQL_C_GUID.|  
|HYT01|Tiempo de espera de conexión agotado|Ha expirado el período de tiempo de espera de conexión antes de que el origen de datos que respondió a la solicitud. El período de tiempo de espera de conexión se establece a través de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Controlador no admite esta función|(DM) el controlador correspondiente a la *StatementHandle* no admite la función.|  
|IM017|Sondeo se deshabilita en modo de notificación asincrónica|Cada vez que se usa el modelo de notificación, se deshabilita el sondeo.|  
|IM018|**SQLCompleteAsync** no se ha llamado para completar la operación asincrónica anterior en este identificador.|Si la llamada de función anterior en el controlador devuelve SQL_STILL_EXECUTING y si está habilitado el modo de notificación, **SQLCompleteAsync** debe llamarse en el identificador para realizar el procesamiento posterior y completar la operación.|  
  
## <a name="comments"></a>Comentarios  
 **SQLGetData** devuelve los datos en una columna especificada. **SQLGetData** se puede llamar solo después de que se han capturado desde el conjunto de resultados por una o varias filas **SQLFetch**, **SQLFetchScroll**, o **SQLExtendedFetch**. Si los datos de longitud variable están demasiado grandes que se devolverán en una sola llamada a **SQLGetData** (debido a una limitación de la aplicación), **SQLGetData** puede recuperarlo en partes. Es posible enlazar algunas columnas de una fila y una llamada **SQLGetData** en otros casos, aunque esto está sujeto a algunas restricciones. Para obtener más información, consulte [obtención de datos Long](../../../odbc/reference/develop-app/getting-long-data.md).  
  
 Para obtener información sobre el uso de **SQLGetData** con parámetros de salida transmitidos, consulte [recuperar parámetros de salida mediante SQLGetData](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md).  
  
## <a name="using-sqlgetdata"></a>Mediante SQLGetData  
 Si el controlador no es compatible con las extensiones **SQLGetData**, la función puede devolver datos solo para las columnas sin enlazar con un número mayor que el de la última columna enlazada. Además, dentro de una fila de datos, el valor de la *Col_or_Param_Num* argumento en cada llamada a **SQLGetData** debe ser mayor o igual que el valor de *Col_or_Param_Num*en la llamada anterior; es decir, se deben recuperar los datos en orden de número de columna creciente. Por último, si no se admiten extensiones, **SQLGetData** no se puede llamar si el tamaño del conjunto de filas es mayor que 1.  
  
 Controladores pueden ser menos exigentes con alguna de estas restricciones. Para determinar qué restricciones relaja un controlador, una aplicación llama a **SQLGetInfo** con cualquiera de las siguientes opciones de SQL_GETDATA_EXTENSIONS:  
  
-   SQL_GD_OUTPUT_PARAMS = **SQLGetData** se puede llamar para devolver valores de parámetro de salida. Para obtener más información, consulte [recuperar parámetros de salida mediante SQLGetData](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md).  
  
-   SQL_GD_ANY_COLUMN. Si esta opción se devuelve, **SQLGetData** se puede llamar para cualquier columna sin enlazar, las incluidas antes de la última columna enlazada.  
  
-   SQL_GD_ANY_ORDER. Si esta opción se devuelve, **SQLGetData** se puede llamar a las columnas sin enlazar en cualquier orden.  
  
-   SQL_GD_BLOCK. Si esta opción es devuelto por **SQLGetInfo** para el tipo de información SQL_GETDATA_EXTENSIONS, el controlador admite las llamadas a **SQLGetData** cuando el tamaño del conjunto de filas es mayor que 1 y la aplicación puede llamar a **SQLSetPos** con la opción SQL_POSITION para colocar el cursor en la fila correcta antes de llamar a **SQLGetData.**  
  
-   SQL_GD_BOUND. Si esta opción se devuelve, **SQLGetData** se puede llamar a las columnas enlazadas, así como las columnas sin enlazar.  
  
 Existen dos excepciones a estas restricciones y capacidad de un controlador de ser menos exigentes con ellos. Primero, **SQLGetData** nunca debe llamarse para un cursor de avance y solo cuando el tamaño del conjunto de filas es mayor que 1. En segundo lugar, si un controlador es compatible con marcadores, siempre debe admitir la posibilidad de llamar a **SQLGetData** para la columna 0, incluso si no permite las aplicaciones llamen a **SQLGetData** para otras columnas antes de la última columna dependiente. (Cuando una aplicación se trabaja con un ODBC 2 *.x* controlador, **SQLGetData** devolverá correctamente un marcador cuando se llama con *Col_or_Param_Num* igual a 0 después de llamar a **SQLFetch**, porque **SQLFetch** son asignados por el ODBC 3 *.x* Administrador de controladores a **SQLExtendedFetch** con un  *FetchOrientation* de SQL_FETCH_NEXT, y **SQLGetData** con un *Col_or_Param_Num* 0 está asignada por el ODBC 3 *.x* Administrador de controladores para **SQLGetStmtOption** con un *fOption* de SQL_GET_BOOKMARK.)  
  
 **SQLGetData** no se puede usar para recuperar el marcador para una fila que acaba de insertar mediante una llamada a **SQLBulkOperations** con la opción SQL_ADD, porque no está situado el cursor en la fila. Una aplicación puede recuperar el marcador para dicha fila enlazando la columna 0 antes de llamar a **SQLBulkOperations** con SQL_ADD, en cuyo caso **SQLBulkOperations** devuelve el marcador en el búfer enlazado. **SQLFetchScroll** , a continuación, se puede llamar con SQL_FETCH_BOOKMARK para volver a colocar el cursor en esa fila.  
  
 Si el *TargetType* argumento es un tipo de datos de intervalo, la precisión inicial del intervalo de predeterminado (2) y la precisión de segundos de intervalo predeterminado (6), como se establece en los campos SQL_DESC_DATETIME_INTERVAL_PRECISION y SQL_DESC_PRECISION de el descartar, respectivamente, se usan para los datos. Si el *TargetType* argumento es un tipo de datos SQL_C_NUMERIC, la precisión predeterminada (definido por el controlador) y default escala (0), como se establece en los campos SQL_DESC_PRECISION y SQL_DESC_SCALE del descartar, se usan para los datos. Si cualquier valor predeterminado de precisión o escala no es adecuado, la aplicación debe establecer explícitamente el campo descriptor apropiado mediante una llamada a **SQLSetDescField** o **SQLSetDescRec**. Puede establecer el campo SQL_DESC_CONCISE_TYPE en SQL_C_NUMERIC y llame a **SQLGetData** con un *TargetType* argumento de SQL_ARD_TYPE, lo que hará que los valores de precisión y escala en los campos de descriptor que se usará.  
  
> [!NOTE]  
>  En ODBC 2 *.x*, las aplicaciones establecen *TargetType* SQL_C_DATE, SQL_C_TIME o SQL_C_TIMESTAMP para indicar que \* *TargetValuePtr* es una fecha, hora, o estructura de marca de tiempo. En ODBC 3 *.x*, las aplicaciones establecen *TargetType* SQL_C_TYPE_DATE, SQL_C_TYPE_TIME o SQL_C_TYPE_TIMESTAMP. El Administrador de controladores hace que asignaciones adecuadas si es necesario, en función de la versión de la aplicación y el controlador.  
  
## <a name="retrieving-variable-length-data-in-parts"></a>Recuperación de datos de longitud Variable en partes  
 **SQLGetData** puede usarse para recuperar datos de una columna que contiene datos de longitud variable en partes, es decir, cuando el identificador del tipo de datos SQL de la columna SQL_CHAR, SQL_VARCHAR, SQL_LONGVARCHAR, SQL_WCHAR, SQL_WVARCHAR, SQL_ WLONGVARCHAR, SQL_BINARY, SQL_VARBINARY, SQL_LONGVARBINARY o un identificador específico del controlador para un tipo de longitud variable.  
  
 Para recuperar datos de una columna de elementos, la aplicación llama a **SQLGetData** varias veces en una sucesión de la misma columna. En cada llamada, **SQLGetData** devuelve la siguiente parte de los datos. Es responsabilidad de la aplicación para volver a unir las piezas, teniendo cuidado de quitar el carácter de terminación null de los elementos intermedios de datos de caracteres. Si hay más datos para devolver o no se ha asignado suficiente búfer para el carácter de terminación, **SQLGetData** devuelve SQL_SUCCESS_WITH_INFO y SQLSTATE 01004 (datos truncados). Cuando se devuelve la última parte de los datos, **SQLGetData** devuelve SQL_SUCCESS. SQL_NO_TOTAL ni cero se puede devolver en la última llamada válida para recuperar datos de una columna, dado que la aplicación no dispondría de ninguna manera de saber qué cantidad de los datos en el búfer de aplicación es válido. Si **SQLGetData** se llama una vez hecho esto, devuelve SQL_NO_DATA. Para obtener más información, vea la sección siguiente, "Recuperar los datos con SQLGetData".  
  
 Marcadores de longitud variable pueden devolverse en partes de **SQLGetData**. Igual que con otros datos, una llamada a **SQLGetData** para devolver los marcadores de longitud variable en partes devolverá SQLSTATE 01004 (datos de cadena, truncados derecha) y SQL_SUCCESS_WITH_INFO cuando hay más datos que se va a devolver. Esto es diferente que en el caso cuando se trunca un marcador de longitud variable por una llamada a **SQLFetch** o **SQLFetchScroll**, que devuelve SQL_ERROR y SQLSTATE 22001 (datos de cadena, truncados derecha).  
  
 **SQLGetData** no se puede usar para devolver datos de longitud fija en partes. Si **SQLGetData** es llamado más de una vez en una fila para una columna que contiene datos de longitud fija, que devuelve SQL_NO_DATA para todas las llamadas después de la primera.  
  
## <a name="retrieving-streamed-output-parameters"></a>Recuperar parámetros de salida transmitidos  
 Si un controlador es compatible con los parámetros de salida transmitidos, una aplicación puede llamar a **SQLGetData** con una pequeña cantidad de veces para recuperar un valor de parámetro grande del búfer. Para obtener más información sobre el parámetro de salida transmitidos, consulte [recuperar parámetros de salida mediante SQLGetData](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md).  
  
## <a name="retrieving-data-with-sqlgetdata"></a>Recuperación de datos con SQLGetData  
 Para obtener datos de la columna especificada, **SQLGetData** realiza la siguiente secuencia de pasos:  
  
1.  Devuelve SQL_NO_DATA si ya ha devuelto todos los datos de la columna.  
  
2.  Conjuntos de \* *StrLen_or_IndPtr* en SQL_NULL_DATA si los datos son NULL. Si los datos son NULL y *StrLen_or_IndPtr* era un puntero nulo, **SQLGetData** devuelve SQLSTATE 22002 se necesita una (variable de indicador necesaria pero no se ha proporcionado).  
  
     Si los datos de la columna no están NULL, **SQLGetData** avanza al paso 3.  
  
3.  Si el atributo de instrucción SQL_ATTR_MAX_LENGTH se establece en un valor distinto de cero, si la columna contiene caracteres o datos binarios y **SQLGetData** no se ha llamado previamente para la columna, los datos se truncan en SQL_ATTR_MAX_LENGTH bytes.  
  
    > [!NOTE]  
    >  El atributo de instrucción SQL_ATTR_MAX_LENGTH está pensado para reducir el tráfico de red. Por lo general se implementa mediante el origen de datos que se trunca los datos antes de devolverlo a través de la red. Los controladores y orígenes de datos no tienen que lo admiten. Por lo tanto, para garantizar que los datos se truncan hasta un tamaño determinado, una aplicación debe asignar un búfer de ese tamaño y especifique el tamaño en el *BufferLength* argumento.  
  
4.  Convierte los datos en el tipo especificado en *TargetType*. Los datos se especifica la precisión y escala predeterminadas para ese tipo de datos. Si *TargetType* es SQL_ARD_TYPE, los datos se usa el tipo en el campo SQL_DESC_CONCISE_TYPE de la descartar. Si *TargetType* es SQL_ARD_TYPE, los datos se proporciona la precisión y escala en la SQL_DESC_DATETIME_INTERVAL_PRECISION, SQL_DESC_PRECISION, y escriba el SQL_DESC_CONCISE campos SQL_DESC_SCALE de descartar, dependiendo de los datos Campo _tipo. Si cualquier valor predeterminado de precisión o escala no es adecuado, la aplicación debe establecer explícitamente el campo descriptor apropiado mediante una llamada a **SQLSetDescField** o **SQLSetDescRec**.  
  
5.  Si los datos se convierten a un tipo de datos de longitud variable, como carácter o binario, **SQLGetData** comprueba si se supera la longitud de los datos *BufferLength*. Si supera la longitud de datos de caracteres (incluido el carácter de terminación null) *BufferLength*, **SQLGetData** trunca los datos a *BufferLength* menos la longitud de un carácter de terminación null. A continuación, null-finaliza los datos. Si la longitud de datos binarios supera la longitud del búfer de datos, **SQLGetData** trunca hasta *BufferLength* bytes.  
  
     Si el búfer de datos proporcionado es demasiado pequeño para contener el carácter de terminación null **SQLGetData** devuelve SQL_SUCCESS_WITH_INFO y SQLSTATE 01004.  
  
     **SQLGetData** nunca trunca los datos convierten en datos de longitud fija tipos; siempre se supone que la longitud de **TargetValuePtr* es el tamaño del tipo de datos.  
  
6.  Coloca los datos convertidos (y posiblemente truncados) en \* *TargetValuePtr*. Tenga en cuenta que **SQLGetData** no pueden devolver datos fuera de línea.  
  
7.  Coloca la longitud de los datos de \* *StrLen_or_IndPtr*. Si *StrLen_or_IndPtr* era un puntero nulo, **SQLGetData** no devuelve la longitud.  
  
    -   Para caracteres o datos binarios, esto es la longitud de los datos después de la conversión y antes del truncamiento debido a *BufferLength*. Si el controlador no puede determinar la longitud de los datos después de la conversión, como sucede en ocasiones con datos de tipo long, devuelve SQL_SUCCESS_WITH_INFO y establece la longitud en SQL_NO_TOTAL. (La última llamada a **SQLGetData** siempre debe devolver la longitud de los datos, no en cero o SQL_NO_TOTAL.) Si se truncaron los datos debido a la instrucción SQL_ATTR_MAX_LENGTH atributo, el valor de este atributo, en lugar de la longitud real, se coloca en \* *StrLen_or_IndPtr*. Esto es porque este atributo está diseñado para truncar los datos en el servidor antes de la conversión, por lo que el controlador no tiene ninguna manera de averiguar lo que la longitud real es. Cuando **SQLGetData** se llama varias veces seguidas de la misma columna, ésta es la longitud de los datos disponibles al principio de la llamada actual; es decir, reduce la longitud con cada llamada posterior.  
  
    -   Para los demás tipos de datos, esto es la longitud de los datos después de la conversión; es decir, es el tamaño del tipo al que se ha convertido los datos.  
  
8.  Si los datos se truncan sin pérdida de significado durante la conversión (por ejemplo, el número real 1,234 se trunca cuando se convierte en el entero 1) o porque *BufferLength* es demasiado pequeño (por ejemplo, la cadena "abcdef" se coloca en un búfer de 4 bytes), **SQLGetData** devuelve SQL_SUCCESS_WITH_INFO y SQLSTATE 01004 (datos truncados) el. Si los datos se truncan sin pérdida de significado porque el atributo de instrucción SQL_ATTR_MAX_LENGTH, **SQLGetData** devuelve SQL_SUCCESS y no devuelve SQLSTATE 01004 (datos truncados).  
  
 El contenido del búfer de datos dependiente (si **SQLGetData** se llama en una columna dependiente) y el búfer de longitud/indicador son indefinidos si **SQLGetData** no devuelve SQL_SUCCESS o SQL_SUCCESS_WITH_INFO.  
  
 Las llamadas sucesivas a **SQLGetData** recuperará los datos de la última columna solicitada; los desplazamientos anteriores dejan de ser válidos. Por ejemplo, cuando se realiza la siguiente secuencia:  
  
```  
SQLGetData(icol=n), SQLGetData(icol=m), SQLGetData(icol=n)  
```  
  
 la segunda llamada a SQLGetData(icol=n) recupera los datos desde el principio de la columna n. Cualquier posición de desplazamiento en los datos debido a las llamadas anteriores a **SQLGetData** para la columna ya no es válida.  
  
## <a name="descriptors-and-sqlgetdata"></a>Descriptores y SQLGetData  
 **SQLGetData** no interactúa directamente con los campos de descriptor.  
  
 Si *TargetType* es SQL_ARD_TYPE, los datos se usa el tipo en el campo SQL_DESC_CONCISE_TYPE de la descartar. Si *TargetType* es SQL_ARD_TYPE o SQL_C_DEFAULT, los datos se proporciona la precisión y escala en la SQL_DESC_DATETIME_INTERVAL_PRECISION, SQL_DESC_PRECISION, y campos SQL_DESC_SCALE de descartar, según los datos de tipo en el campo SQL_DESC_CONCISE_TYPE.  
  
## <a name="code-example"></a>Ejemplo de código  
 En el ejemplo siguiente, una aplicación ejecuta un **seleccione** instrucción para devolver un conjunto de resultados del cliente de identificadores, nombres y ordenados por nombre, el identificador y el número de teléfono de números de teléfono. Para cada fila de datos, llama a **SQLFetch** para colocar el cursor a la siguiente fila. Llama a **SQLGetData** para recuperar los datos capturados; los búferes de los datos y el número de bytes devuelto se especifican en la llamada a **SQLGetData**. Por último, se imprimen el nombre de cada empleado, Id. y número de teléfono.  
  
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
|Asignar almacenamiento para una columna en un conjunto de resultados|[SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Realizar operaciones masivas que no hacen referencia a la posición del cursor de bloque|[SQLBulkOperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md)|  
|Procesamiento de una instrucción de cancelación|[SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Ejecutar una instrucción SQL|[SQLExecDirect](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|Ejecutar una instrucción SQL preparada|[SQLExecute](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|Obtención de un bloque de datos o desplazarse a través de un resultado de conjunto|[SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|Obtención de una sola fila de datos o un bloque de datos en una dirección de solo avance|[SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|Envío de datos de parámetro en tiempo de ejecución|[SQLPutData](../../../odbc/reference/syntax/sqlputdata-function.md)|  
|Sitúe el cursor, actualizar los datos en el conjunto de filas, o actualizar o eliminar datos en el conjunto de filas|[SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md)|  
  
## <a name="see-also"></a>Vea también  
 [Referencia de la API de ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Archivos de encabezado ODBC](../../../odbc/reference/install/odbc-header-files.md)   
 [Recuperar parámetros de salida mediante SQLGetData](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)
