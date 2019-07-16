---
title: Función SQLSetConnectAttr | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLSetConnectAttr
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLSetConnectAttr
helpviewer_keywords:
- SQLSetConnectAttr function [ODBC]
ms.assetid: 97fc7445-5a66-4eb9-8e77-10990b5fd685
author: MightyPen
ms.author: genemi
ms.openlocfilehash: fd4acd7ce6a33665ce3d32e42328c906aaec3049
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67910385"
---
# <a name="sqlsetconnectattr-function"></a>Función SQLSetConnectAttr
**Conformidad**  
 Versión de introducción: Compatibilidad de ODBC 3.0 estándares: ISO 92  
  
 **Resumen**  
 **SQLSetConnectAttr** establece los atributos que controlan aspectos de las conexiones.  
  
> [!NOTE]
>  Para obtener más información sobre lo que el Administrador de controladores se asigna esta función cuando una aplicación ODBC 3 *.x* aplicación funciona con un ODBC 2 *.x* controladores, consulte [asignación de funciones de reemplazo para hacia atrás Compatibilidad de aplicaciones](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md).  
  
## <a name="syntax"></a>Sintaxis  
  
```cpp  
  
SQLRETURN SQLSetConnectAttr(  
     SQLHDBC       ConnectionHandle,  
     SQLINTEGER    Attribute,  
     SQLPOINTER    ValuePtr,  
     SQLINTEGER    StringLength);  
```  
  
## <a name="arguments"></a>Argumentos  
 *ConnectionHandle*  
 [Entrada] Identificador de conexión.  
  
 *Atributo*  
 [Entrada] Atributo para establecer, aparecen en "Comentarios".  
  
 *ValuePtr*  
 [Entrada] Puntero al valor que se asociará con *atributo*. Dependiendo del valor de *atributo*, *ValuePtr* será un valor entero sin signo o hará referencia a una cadena de caracteres terminada en null. Tenga en cuenta que el tipo del entero de la *atributo* argumento puede no tener una longitud fija, vea la sección Comentarios para obtener información detallada.  
  
 *StringLength*  
 [Entrada] Si *atributo* es un atributo definido por el ODBC y *ValuePtr* apunta a un búfer binario o una cadena de caracteres, este argumento debe ser la longitud de **ValuePtr*. Para los datos de cadena de caracteres, este argumento debe contener el número de bytes en la cadena.  
  
 Si *atributo* es un atributo definido por el ODBC y *ValuePtr* es un entero, *StringLength* se omite.  
  
 Si *atributo* es un atributo definido por el controlador, la aplicación indica la naturaleza del atributo para el Administrador de controladores al establecer el *StringLength* argumento. *StringLength* puede tener los siguientes valores:  
  
-   Si *ValuePtr* es un puntero a una cadena de caracteres, a continuación, *StringLength* es la longitud de la cadena o SQL_NTS.  
  
-   Si *ValuePtr* es un puntero a un búfer binario, a continuación, la aplicación, el resultado de la SQL_LEN_BINARY_ATTR (*longitud*) macro en *StringLength*. Esto coloca un valor negativo en *StringLength*.  
  
-   Si *ValuePtr* es un puntero a un valor distinto de una cadena de caracteres o una cadena binaria, a continuación, *StringLength* debe tener el valor SQL_IS_POINTER.  
  
-   Si *ValuePtr* contiene un valor de longitud fija, a continuación, *StringLength* es SQL_IS_INTEGER o SQL_IS_UINTEGER, según corresponda.  
  
## <a name="returns"></a>Devuelve  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR, SQL_INVALID_HANDLE o SQL_STILL_EXECUTING.  
  
## <a name="diagnostics"></a>Diagnóstico  
 Cuando **SQLSetConnectAttr** devuelve SQL_ERROR o SQL_SUCCESS_WITH_INFO, un valor SQLSTATE asociado se puede obtener mediante una llamada a **SQLGetDiagRec** con un *HandleType* de SQL_HANDLE_DBC y un *controlar* de *ConnectionHandle*. En la tabla siguiente se enumera los valores SQLSTATE devueltos normalmente por **SQLSetConnectAttr** y se explica cada uno de ellos en el contexto de esta función; la notación "(DM)" precede a las descripciones de SQLSTATE devuelto por el Administrador de controladores. El código de retorno asociado a cada valor SQLSTATE es SQL_ERROR, a menos que se indique lo contrario.  
  
 El controlador puede devuelve SQL_SUCCESS_WITH_INFO para proporcionar información sobre el resultado de establecer una opción.  
  
|SQLSTATE|Error|Descripción|  
|--------------|-----------|-----------------|  
|01000|Advertencia general|Específico del controlador de mensaje informativo. (La función devuelve SQL_SUCCESS_WITH_INFO).|  
|01S02|Valor de opción cambiado|El controlador no eran compatibles con el valor especificado en *ValuePtr* y sustituir un valor similar. (La función devuelve SQL_SUCCESS_WITH_INFO).|  
|08002|Nombre de la conexión en uso|El *atributo* argumento era SQL_ATTR_ODBC_CURSORS y el controlador ya se ha conectado al origen de datos.|  
|08003|Conexión no abierta|(DM) un *atributo* se especificó un valor que requiere una conexión abierta, pero la *ConnectionHandle* no estaba en estado conectado.|  
|08S01|Error de vínculo de comunicación|Error en el vínculo de comunicación entre el controlador y el origen de datos a la que se ha conectado el controlador antes del procesamiento de la función se ha completado.|  
|24000|Estado de cursor no válido|El *atributo* argumento era SQL_ATTR_CURRENT_CATALOG, y un conjunto de resultados quedó pendiente.|  
|25000|Operación no válida durante una transacción local|Una conexión no era una transacción local al intentar dar de alta una conexión de transacciones distribuidas (DTC) estableciendo el atributo SQL_ATTR_ENLIST_IN_DTC de conexión.<br /><br /> Una conexión ya está dada de alta en DTC.<br /><br /> Una conexión ha dado de alta en una conexión de transacción distribuida y se inicia una transacción local estableciendo SQL_ATTR_AUTOCOMMIT como SQL_AUTOCOMMIT_OFF.|  
|3D000|Nombre del catálogo no válido|El *atributo* argumento era SQL_CURRENT_CATALOG y el nombre de catálogo especificado no era válido.|  
|HY000|Error general|Se produjo un error para que se ha producido ningún SQLSTATE específico y para los que se ha definido ningún SQLSTATE específicos de la implementación. El mensaje de error devuelto por **SQLGetDiagRec** en el  *\*MessageText* búfer describe el error y su causa.|  
|HY001|Error de asignación de memoria|El controlador no pudo asignar la memoria necesaria para admitir la ejecución o la finalización de la función.|  
|HY008|Operación cancelada|Procesamiento asincrónico se habilitó para la *ConnectionHandle*. El **SQLSetConnectAttr** se llamó a la función, y antes que completó la ejecución, el [función SQLCancelHandle](../../../odbc/reference/syntax/sqlcancelhandle-function.md) se ha llamado en el *ConnectionHandle*y, a continuación, el **SQLSetConnectAttr** función se llamó de nuevo en el *ConnectionHandle*.<br /><br /> O bien, el **SQLSetConnectAttr** se llamó a la función, y antes que completó la ejecución, **SQLCancelHandle** se ha llamado en el *ConnectionHandle* desde un subproceso diferente en una aplicación multiproceso.|  
|HY009|Uso no válido del puntero nulo|El *atributo* argumento identifica un atributo de conexión que requiere un valor de cadena, y el *ValuePtr* argumento era un puntero nulo.|  
|HY010|Error de secuencia de función|(DM) se llamó a una función que se ejecuta de forma asincrónica para una *StatementHandle* asociado con el *ConnectionHandle* y aún se estaba ejecutando cuando **SQLSetConnectAttr**se llamó.<br /><br /> (DM) se llamó a una función que se ejecuta asincrónicamente (no ésta) para el *ConnectionHandle* y aún se estaba ejecutando cuando se llamó a esta función.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, o **SQLMoreResults** se llamó para uno de los identificadores de instrucción asociados con el *ConnectionHandle* y devuelve SQL_PARAM_DATA_AVAILABLE. Esta función se invoca antes de que se recuperan los datos para todos los parámetros transmitidos.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, o **SQLSetPos** se llamó para un *StatementHandle*  asociado con el *ConnectionHandle* y devuelve SQL_NEED_DATA. Esta función se invoca antes de que se enviaron datos para todas las columnas o parámetros de datos en ejecución.<br /><br /> (DM) **SQLBrowseConnect** se llamó para el *ConnectionHandle* y devuelve SQL_NEED_DATA. Se llamó a esta función antes de **SQLBrowseConnect** devuelve SQL_SUCCESS_WITH_INFO o SQL_SUCCESS.|  
|HY011|Atributo no se puede establecer ahora|El *atributo* argumento era SQL_ATTR_TXN_ISOLATION y una transacción estaba abierta.|  
|HY013|Error de administración de memoria|No se pudo procesar la llamada de función porque los objetos de memoria subyacente no se podrían tener acceso, posiblemente debido a memoria insuficiente.|  
|HY024|Valor de atributo no válido|Dada la especificado *atributo* valor, se especificó un valor no válido en *ValuePtr*. (El Administrador de controladores devuelve este SQLSTATE solo para la conexión y los atributos de instrucción que aceptan un conjunto discreto de valores, como SQL_ATTR_ACCESS_MODE o SQL_ATTR_ASYNC_ENABLE. Para el resto de conexión y los atributos de instrucción, el controlador debe comprobar el valor especificado en *ValuePtr*.)<br /><br /> El *atributo* argumento era SQL_ATTR_TRACEFILE o SQL_ATTR_TRANSLATE_LIB, y *ValuePtr* era una cadena vacía.|  
|HY090|Longitud de búfer o cadena no válida|*(DM) \*ValuePtr* es una cadena de caracteres y el *StringLength* argumento era menor que 0 pero no era SQL_NTS.|  
|HY092|Identificador de opción o atributo no válido|(DM) el valor especificado para el argumento *atributo* no era válido para la versión de ODBC compatible con el controlador.<br /><br /> (DM) el valor especificado para el argumento *atributo* era un atributo de sólo lectura.|  
|HY114|Controlador no admite la ejecución de la función de nivel de conexión asincrónica|(DM) ha intentado una aplicación habilitar la ejecución de la función asincrónica con SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE para un controlador que no es compatible con las operaciones de conexión asincrónica.|  
|HY117|Conexión está suspendida debido al estado de transacción desconocido. Solo se desconecte y se permiten funciones de solo lectura.|(DM) para obtener más información sobre el estado suspendido, consulte [función SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HY121|Biblioteca de cursores y la agrupación de dependientes del controlador no se puede habilitar al mismo tiempo|Para obtener más información, consulte [Driver-Aware Connection Pooling](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md).|  
|HYC00|Característica opcional no implementada|El valor especificado para el argumento *atributo* era una conexión ODBC válida o atributo de instrucción para la versión de ODBC compatibles con el controlador, pero no es compatible con el controlador.|  
|HYT01|Tiempo de espera de conexión agotado|Ha expirado el período de tiempo de espera de conexión antes de que el origen de datos que respondió a la solicitud. El período de tiempo de espera de conexión se establece a través de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Controlador no admite esta función|(DM) el controlador asociado con el *ConnectionHandle* no admite la función.|  
|IM009|No se puede cargar el archivo DLL de traducción|El controlador no pudo cargar la DLL que se especificó para la conexión de traducción. Este error puede devolverse solo cuando *atributo* es SQL_ATTR_TRANSLATE_LIB.|  
|IM017|Sondeo se deshabilita en modo de notificación asincrónica|Cada vez que se usa el modelo de notificación, se deshabilita el sondeo.|  
|IM018|**SQLCompleteAsync** no se ha llamado para completar la operación asincrónica anterior en este identificador.|Si la llamada de función anterior en el controlador devuelve SQL_STILL_EXECUTING y si está habilitado el modo de notificación, **SQLCompleteAsync** debe llamarse en el identificador para realizar el procesamiento posterior y completar la operación.|  
|S1118|Controlador no admite la notificación asincrónica|Se estableció SQL_ATTR_ASYNC_DBC_EVENT (después de que se realizó la conexión), pero la notificación asincrónica no es compatible con el controlador.|  
  
 Cuando *atributo* es un atributo de instrucción **SQLSetConnectAttr** puede devolver cualquier SQLSTATE devuelto por **SQLSetStmtAttr**.  
  
## <a name="comments"></a>Comentarios  
 Para obtener información general sobre los atributos de conexión, consulte [los atributos de conexión](../../../odbc/reference/develop-app/connection-attributes.md).  
  
 Se muestran los atributos definidos actualmente y la versión de ODBC en el que se presentaron en la tabla más adelante en esta sección. se espera que se definirá más atributos para aprovechar las ventajas de diferentes orígenes de datos. Un intervalo de atributos está reservado por ODBC; los desarrolladores de controladores deben reservar los valores para su propio uso específico del controlador de Open Group.  
  
> [!NOTE]
>  La capacidad de establecer los atributos de instrucción en el nivel de conexión mediante una llamada a **SQLSetConnectAttr** ha quedado obsoleto en ODBC 3 *.x*. ODBC 3 *.x* aplicaciones nunca deben establecer los atributos de instrucción en el nivel de conexión. ODBC 3 *.x* atributos de instrucción no se puede establecer en el nivel de conexión, a excepción de los atributos SQL_ATTR_METADATA_ID y SQL_ATTR_ASYNC_ENABLE, que son los atributos de conexión y los atributos de instrucción y pueden ser establecer en el nivel de conexión o el nivel de instrucción.  
> 
>  ODBC 3 *.x* controladores sólo necesitan admitir esta funcionalidad si trabajan con ODBC 2 *.x* aplicaciones que establezcan ODBC 2 *.x* opciones de la instrucción en el nivel de conexión. Para obtener más información, consulte [asignación de SQLSetConnectOption](../../../odbc/reference/appendixes/sqlsetconnectoption-mapping.md) en Apéndice G: Directrices de controlador para la compatibilidad con versiones anteriores.  
  
 Una aplicación puede llamar a **SQLSetConnectAttr** asigna y libera en cualquier momento entre el momento en que la conexión. Todos los atributos de conexión y la instrucción se estableció correctamente la aplicación para la conexión se conservan hasta que **SQLFreeHandle** se llama en la conexión. Por ejemplo, si una aplicación llama a **SQLSetConnectAttr** antes de conectarse a un origen de datos, el atributo persiste incluso si **SQLSetConnectAttr** produce un error en el controlador cuando la aplicación se conecta a la origen de datos; Si una aplicación establece un atributo específico del controlador, el atributo persiste incluso si la aplicación se conecta a un controlador diferente en la conexión.  
  
 Algunos atributos de conexión se pueden establecer sólo antes de que se ha realizado una conexión; otros se pueden establecer después de que se ha realizado una conexión. En la tabla siguiente indica los atributos de conexión que se deben establecer antes o después de que se ha realizado una conexión. *Cualquier* indica que se puede establecer el atributo antes o después de la conexión.  
  
|Atributo|¿Establecer antes o después de la conexión?|  
|---------------|-------------------------------------|  
|SQL_ATTR_ACCESS_MODE|[1]|  
|SQL_ATTR_ASYNC_DBC_EVENT|Antes o después|  
|SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE|Cualquier [4]|  
|SQL_ATTR_ASYNC_DBC_PCALLBACK|Antes o después|  
|SQL_ATTR_ASYNC_DBC_PCONTEXT|Antes o después|  
|SQL_ATTR_ASYNC_ENABLE|[2]|  
|SQL_ATTR_AUTO_IPD|Antes o después|  
|SQL_ATTR_AUTOCOMMIT|Ya sea [5]|  
|SQL_ATTR_CONNECTION_DEAD|Después|  
|SQL_ATTR_CONNECTION_TIMEOUT|Antes o después|  
|SQL_ATTR_CURRENT_CATALOG|[1]|  
|SQL_ATTR_DBC_INFO_TOKEN|Después|  
|SQL_ATTR_ENLIST_IN_DTC|Después|  
|SQL_ATTR_LOGIN_TIMEOUT|Antes del|  
|SQL_ATTR_METADATA_ID|Antes o después|  
|SQL_ATTR_ODBC_CURSORS|Antes del|  
|SQL_ATTR_PACKET_SIZE|Antes del|  
|SQL_ATTR_QUIET_MODE|Antes o después|  
|SQL_ATTR_TRACE|Antes o después|  
|SQL_ATTR_TRACEFILE|Antes o después|  
|SQL_ATTR_TRANSLATE_LIB|Después|  
|SQL_ATTR_TRANSLATE_OPTION|Después|  
|SQL_ATTR_TXN_ISOLATION|[3]|  
  
 [1] SQL_ATTR_ACCESS_MODE y SQL_ATTR_CURRENT_CATALOG se pueden establecer antes o después de conectarse, según el controlador. Sin embargo, las aplicaciones interoperables establecerlos antes de conectarse porque algunos controladores no admiten el cambio estos después de conectarse.  
  
 [2] SQL_ATTR_ASYNC_ENABLE debe establecerse antes de que hay una instrucción activa.  
  
 [3] SQL_ATTR_TXN_ISOLATION puede establecerse solo si hay no hay transacciones abiertas en la conexión. Algunos atributos de conexión admiten la sustitución de un valor similar si el origen de datos no es compatible con el valor especificado en \* *ValuePtr*. En tales casos, el controlador devuelve SQL_SUCCESS_WITH_INFO y SQLSTATE 01S02 de SQLState (valor de opción cambiado). Por ejemplo, si *atributo* es SQL_ATTR_PACKET_SIZE y \* *ValuePtr* supera el tamaño máximo del paquete, el controlador sustituye el tamaño máximo. Para determinar el valor sustituido, una aplicación llama a **SQLGetConnectAttr**.  
  
 [4] si SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE se establece antes de que una conexión está abierta, el Administrador de controladores establecerá el atributo del controlador cuando se carga el controlador durante una llamada a **SQLBrowseConnect**, **SQLConnect**, o **SQLDriverConnect**. Antes de llamar a **SQLBrowseConnect**, **SQLConnect**, o **SQLDriverConnect**, el Administrador de controladores no sabe qué controlador para conectarse a y no sabe si el controlador admite las operaciones de conexión asincrónica. Por lo tanto, el Administrador de controladores siempre devuelve SQL_SUCCESS. Pero, en caso de que el controlador no admite operaciones de conexión asincrónica, la llamada a **SQLBrowseConnect**, **SQLConnect**, o **SQLDriverConnect** se producirá un error.  
  
 [5] cuando SQL_ATTR_AUTOCOMMIT se establece en FALSE, las aplicaciones deben llamar SQLEndTran(SQL_ROLLBACK) si cualquier API devuelve SQL_ERROR para garantizar la coherencia transaccional.  
  
 El formato de información establecida el \* *ValuePtr* búfer depende especificado *atributo*. **SQLSetConnectAttr** aceptará la información de atributo en uno de los dos formatos diferentes: una cadena de caracteres terminada en null o un valor entero. El formato de cada uno se indica en la descripción del atributo. Caracteres de cadenas que apunta el *ValuePtr* argumento de **SQLSetConnectAttr** tener una longitud de *StringLength* bytes.  
  
 El *StringLength* argumento se omite si la longitud está definida por el atributo, como es el caso de todos los atributos que se introdujo en ODBC 2 *.x* o una versión anterior.  
  
|*Atributo*|*ValuePtr* contenido|  
|-----------------|-------------------------|  
|SQL_ATTR_ACCESS_MODE (ODBC 1.0)|Un valor SQLUINTEGER. El controlador o el origen de datos usa SQL_MODE_READ_ONLY como un indicador de que la conexión no es necesaria para admitir instrucciones SQL que provocan actualizaciones que se produzca. Este modo se puede usar para optimizar estrategias de bloqueo, administración de transacciones u otras áreas según sea apropiado para el controlador u origen de datos. El controlador no es necesario para evitar tales instrucciones desde el que se envía al origen de datos. El comportamiento del controlador y el origen de datos cuando se le pida para procesar instrucciones SQL que no son de solo lectura durante una conexión de solo lectura es definido por la implementación. SQL_MODE_READ_WRITE es el valor predeterminado.|  
|SQL_ATTR_ASYNC_DBC_EVENT (ODBC 3.8)|Un valor SQLPOINTER que es un identificador de evento.<br /><br /> Está habilitada la notificación de la finalización de las funciones asincrónicas mediante una llamada a **SQLSetConnectAttr** con el atributo SQL_ATTR_ASYNC_STMT_EVENT y especificando el identificador de evento. **Nota:**  El método de notificación no es compatible con la biblioteca de cursores. Una aplicación recibirá el mensaje de error si intenta habilitar la biblioteca de cursores a través de SQLSetConnectAttr, cuando el método de notificación está habilitado.|  
|SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE (ODBC 3.8)|Un valor SQLUINTEGER que habilita o deshabilita la ejecución asincrónica de las funciones seleccionadas en el identificador de conexión. Para obtener más información, consulte [ejecución asincrónica (método de sondeo)](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md).<br /><br /> SQL_ASYNC_DBC_ENABLE_ON = habilitar la operación asincrónica para funciones relacionadas con la conexión especificadas.<br /><br /> SQL_ASYNC_DBC_ENABLE_OFF = Disable (valor predeterminado) la operación asincrónica para funciones relacionadas con la conexión especificadas.<br /><br /> Establecer SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE es siempre sincrónico (es decir, que nunca devolverá SQL_STILL_EXECUTING).<br /><br /> Ejecución asincrónica de las operaciones de instrucción están habilitadas con SQL_ATTR_ASYNC_ENABLE.|  
|SQL_ATTR_ASYNC_DBC_PCALLBACK (ODBC 3.8)|Un valor SQLPOINTER que apunta a la estructura de contexto.<br /><br /> Solo el Administrador de controladores puede llamar a un controlador **SQLSetStmtAttr** función con este atributo.|  
|SQL_ATTR_ASYNC_DBC_PCONTEXT (ODBC 3.8)|Un valor SQLPOINTER que apunta a la estructura de contexto.<br /><br /> Solo el Administrador de controladores puede llamar a un controlador **SQLSetStmtAttr** función con este atributo.|  
|SQL_ATTR_ASYNC_ENABLE (ODBC 3.0)|Un valor SQLULEN que especifica si llama una función con una instrucción en la conexión especificada se ejecuta de forma asincrónica:<br /><br /> SQL_ASYNC_ENABLE_OFF = Disable soporte técnico de nivel de ejecución asincrónica de conexión para las operaciones de instrucción (predeterminado).<br /><br /> SQL_ASYNC_ENABLE_ON = Habilitar soporte técnico de nivel de ejecución asincrónica de conexión para las operaciones de la instrucción.<br /><br /> Este atributo se puede establecer si **SQLGetInfo** con la información de SQL_ASYNC_MODE tipo devuelve SQL_AM_CONNECTION o SQL_AM_STATEMENT.|  
|SQL_ATTR_AUTO_IPD (ODBC 3.0)|Un valor de solo lectura SQLUINTEGER que especifica si el rellenado automático de la IPD después de llamar a **SQLPrepare** es compatible con:<br /><br /> SQL_TRUE = rellenado automático de la IPD después de llamar a **SQLPrepare** es compatible con el controlador.<br /><br /> SQL_FALSE = rellenado automático de la IPD después de llamar a **SQLPrepare** no es compatible con el controlador. Los servidores que no admiten instrucciones preparadas no podrá rellenar automáticamente la IPD.<br /><br /> Si se devuelve SQL_TRUE para el atributo de conexión SQL_ATTR_AUTO_IPD, se puede establecer el atributo de instrucción SQL_ATTR_ENABLE_AUTO_IPD para activar o desactivar el rellenado automático de la IPD. Si SQL_ATTR_AUTO_IPD es SQL_FALSE, SQL_ATTR_ENABLE_AUTO_IPD no se puede establecer en SQL_TRUE. El valor predeterminado de SQL_ATTR_ENABLE_AUTO_IPD es igual al valor de SQL_ATTR_AUTO_IPD.<br /><br /> Este atributo de conexión puede ser devueltos por **SQLGetConnectAttr** pero no se puede establecer **SQLSetConnectAttr**.|  
|SQL_ATTR_AUTOCOMMIT (ODBC 1.0)|Un valor SQLUINTEGER que especifica si se debe usar el modo de confirmación automática o manual:<br /><br /> SQL_AUTOCOMMIT_OFF = el controlador utiliza el modo de confirmación manual y la aplicación debe confirmar o revertir las transacciones con explícitamente **SQLEndTran**.<br /><br /> SQL_AUTOCOMMIT_ON = controlador utiliza en el modo de confirmación automática. Cada instrucción se confirma inmediatamente después de se ejecuta. Ésta es la opción predeterminada. Las transacciones abiertas en la conexión se confirman cuando SQL_ATTR_AUTOCOMMIT está establecido en SQL_AUTOCOMMIT_OFF para cambiar de modo de confirmación manual a modo de confirmación automática.<br /><br /> Para obtener más información, consulte [el modo de confirmación](../../../odbc/reference/develop-app/commit-mode.md). **Importante:**  Eliminación los planes de acceso de algunos orígenes de datos y cerrar los cursores para todas las instrucciones en una conexión cada vez que una instrucción se confirma; modo de confirmación automática puede hacer que esto ocurra después de ejecutar cada instrucción nonquery o cuando se cierra el cursor para una consulta. Para obtener más información, vea los tipos de información SQL_CURSOR_COMMIT_BEHAVIOR y SQL_CURSOR_ROLLBACK_BEHAVIOR en [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) y [efecto de las transacciones en los cursores y las instrucciones preparadas](../../../odbc/reference/develop-app/effect-of-transactions-on-cursors-and-prepared-statements.md). <br /><br /> Cuando un lote se ejecuta en modo de confirmación automática, son posibles dos cosas. Todo el lote se puede tratar como una unidad autocommitable o cada instrucción en un lote se trata como una unidad autocommitable. Algunos orígenes de datos pueden admitir ambos de estos comportamientos y pueden proporcionar una manera de elegir uno u otro. Está definido por el controlador si se trata un lote como una unidad autocommitable o si cada instrucción individual dentro del lote es autocommitable.|  
|SQL_ATTR_CONNECTION_DEAD<br /><br /> (ODBC 3.5)|Un valor SQLUINTEGER de solo lectura que indica el estado de la conexión. Si se ha perdido SQL_CD_TRUE, la conexión. Si SQL_CD_FALSE, la conexión todavía está activa.|  
|SQL_ATTR_CONNECTION_TIMEOUT (ODBC 3.0)|Un valor SQLUINTEGER correspondiente al número de segundos de espera para cualquier solicitud en la conexión se complete antes de volver a la aplicación. El controlador debe devolver SQLSTATE HYT00 (tiempo de espera agotado) en cualquier momento que sea posible tiempo de espera en una situación no está asociada con la ejecución de la consulta o el inicio de sesión.<br /><br /> Si *ValuePtr* es igual a 0 (valor predeterminado), no hay ningún tiempo de espera.|  
|SQL_ATTR_CURRENT_CATALOG (ODBC 2.0)|Una cadena de caracteres que contiene el nombre del catálogo que va a usar el origen de datos. Por ejemplo, en SQL Server, el catálogo es una base de datos, por lo que el controlador envía un **USE** _base de datos_ instrucción para el origen de datos, donde *base de datos* se especifica la base de datos en \* *ValuePtr*. Para un controlador de nivel único, el catálogo podría ser un directorio, por lo que el controlador cambia el directorio actual en el directorio especificado en **ValuePtr*.|  
|SQL_ATTR_DBC_INFO_TOKEN (ODBC 3.8|Un valor SQLPOINTER utilizado para establecer volver el símbolo (token) de información de conexión en DBC controlar cuándo [SQLRateConnection](../../../odbc/reference/syntax/sqlrateconnection-function.md)del (\**pRating*) parámetro no es igual a 100.<br /><br /> SQL_ATTR_DBC_INFO_TOKEN es solo para establecer. No es posible usar **SQLGetConnectAttr** o **SQLGetConnectOption** para recuperar este valor. El Administrador de controladores **SQLSetConnectAttr** no aceptará SQL_ATTR_DBC_INFO_TOKEN, puesto que una aplicación no debe establecer este atributo.<br /><br /> Si un controlador devuelve SQL_ERROR después de establecer SQL_ATTR_DBC_INFO_TOKEN, se liberará la conexión que solo se obtiene del grupo. El Administrador de controladores intentará obtener otra conexión desde el grupo. Consulte [desarrollar el conocimiento de grupo de conexiones en un controlador ODBC](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md) para obtener más información.|  
|SQL_ATTR_ENLIST_IN_DTC (ODBC 3.0)|Un valor SQLPOINTER que especifica si se debe usar el controlador ODBC en las transacciones distribuidas coordinadas por servicios de componentes de Microsoft.<br /><br /> Pasar un DTC OLE objeto transaction que especifica la transacción para exportar a SQL Server o SQL_DTC_DONE para finalizar la asociación DTC de la conexión.<br /><br /> El cliente llama al método de Microsoft Distributed Transaction Coordinator (MS DTC) OLE ITransactionDispenser:: BeginTransaction para iniciar una transacción MS DTC y crear un objeto de transacción de MS DTC que representa la transacción. A continuación, la aplicación llama a SQLSetConnectAttr con la opción de SQL_ATTR_ENLIST_IN_DTC para asociar el objeto de transacción con la conexión de ODBC. Toda la actividad de base de datos relacionada se realizará bajo la protección de la transacción MS DTC. La aplicación llama a SQLSetConnectAttr con SQL_DTC_DONE para finalizar la asociación DTC de la conexión. Para obtener más información, consulte la documentación de MS DTC.|  
|SQL_ATTR_LOGIN_TIMEOUT (ODBC 1.0)|Un valor SQLUINTEGER corresponde al número de segundos de espera para que una solicitud de inicio de sesión para completar antes de volver a la aplicación. El valor predeterminado depende del controlador. Si *ValuePtr* es 0, el tiempo de espera está deshabilitado y un intento de conexión esperará indefinidamente.<br /><br /> Si el tiempo de espera especificado supera el tiempo de espera máximo de inicio de sesión en el origen de datos, el controlador sustituye ese valor y devuelve SQLSTATE 01S02 de SQLState (valor de opción cambiado).|  
|SQL_ATTR_METADATA_ID (ODBC 3.0)|Un valor SQLUINTEGER que determina cómo se tratan los argumentos de cadena de funciones de catálogo.<br /><br /> Si el valor SQL_TRUE, el argumento de cadena de funciones de catálogo se tratan como identificadores. El caso no es significativo. Para las cadenas sin delimitar, el controlador quita los espacios finales y se dobla la cadena a mayúsculas. Para cadenas delimitadas, el controlador quita los espacios iniciales o finales y toma literalmente cualquier cosa que esté entre los delimitadores. Si uno de estos argumentos se establece en un puntero nulo, la función devuelve SQL_ERROR y SQLSTATE HY009 (uso no válido del puntero nulo).<br /><br /> Si SQL_FALSE, los argumentos de cadena de funciones de catálogo no se tratan como identificadores. El caso es significativo. O bien pueden contener un patrón de búsqueda de cadena o no, dependiendo del argumento.<br /><br /> El valor predeterminado es SQL_FALSE.<br /><br /> El *TableType* argumento de **SQLTables**, que toma una lista de valores, no se ve afectada por este atributo.<br /><br /> SQL_ATTR_METADATA_ID también se puede establecer en el nivel de instrucción. (Es el atributo de conexión única que es también un atributo de instrucción).<br /><br /> Para obtener más información, consulte [argumentos en funciones de catálogo](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md).|  
|SQL_ATTR_ODBC_CURSORS (ODBC 2.0)|Un valor SQLULEN especifica cómo el Administrador de controladores utiliza la biblioteca de cursores ODBC:<br /><br /> SQL_CUR_USE_IF_NEEDED = usa el Administrador de controladores de la biblioteca de cursores ODBC solo si es necesario. Si el controlador admite la opción SQL_FETCH_PRIOR en **SQLFetchScroll**, el Administrador de controladores utiliza las capacidades de desplazamiento del controlador. En caso contrario, utiliza la biblioteca de cursores ODBC.<br /><br /> SQL_CUR_USE_ODBC = usa el Administrador de controladores en la biblioteca de cursores ODBC.<br /><br /> Al utilizar SQL_CUR_USE_DRIVER = el Administrador de controladores utiliza las capacidades de desplazamiento del controlador. Esta es la configuración predeterminada.<br /><br /> Para obtener más información acerca de la biblioteca de cursores ODBC, vea [Apéndice F: Biblioteca de cursores ODBC](../../../odbc/reference/appendixes/appendix-f-odbc-cursor-library.md). **Advertencia:**  La biblioteca de cursores se quitará en una versión futura de Windows. Evite usar esta característica en nuevos trabajos de desarrollo y piense en modificar las aplicaciones que actualmente utilizan esta característica. Microsoft recomienda usar la funcionalidad de cursor del controlador.|  
|SQL_ATTR_PACKET_SIZE (ODBC 2.0)|Un valor SQLUINTEGER especifica el tamaño del paquete de red en bytes. **Nota:**  Muchos orígenes de datos no son compatibles con esta opción o sólo devuelto pero no puede establecer el tamaño del paquete de red. <br /><br /> Si el tamaño especificado supera el tamaño máximo del paquete o es menor que el tamaño mínimo de paquete, el controlador sustituye ese valor y devuelve SQLSTATE 01S02 de SQLState (valor de opción cambiado).<br /><br /> Si la aplicación establece el tamaño de paquete después de que ya se ha realizado una conexión, el controlador devolverá SQLSTATE HY011 (atributo no se puede establecer ahora).|  
|SQL_ATTR_QUIET_MODE (ODBC 2.0)|Un identificador de ventana (HWND).<br /><br /> Si el identificador de ventana es un puntero nulo, el controlador no muestra los cuadros de diálogo.<br /><br /> Si el identificador de ventana no es un puntero nulo, debe ser el identificador de ventana principal de la aplicación. Ésta es la opción predeterminada. El controlador utiliza este identificador para mostrar cuadros de diálogo. **Nota:**  El atributo de conexión SQL_ATTR_QUIET_MODE no es aplicable a los cuadros de diálogo mostrados por **SQLDriverConnect**.|  
|SQL_ATTR_TRACE (ODBC 1.0)|Un valor SQLUINTEGER que indica si se debe realizar el seguimiento del Administrador de controladores:<br /><br /> SQL_OPT_TRACE_OFF = seguimiento off (valor predeterminado)<br /><br /> SQL_OPT_TRACE_ON = seguimiento en<br /><br /> Cuando el seguimiento está activado, el Administrador de controladores escribe cada llamada de función ODBC en el archivo de seguimiento. **Nota:**  Cuando el seguimiento está activado, el Administrador de controladores puede devolver IM013 SQLSTATE (error de archivo de seguimiento) desde cualquier función. <br /><br /> Una aplicación especifica un archivo de seguimiento con la opción SQL_ATTR_TRACEFILE. Si el archivo ya existe, el Administrador de controladores se anexa al archivo. En caso contrario, crea el archivo. Si el seguimiento está activado y no se ha especificado ningún archivo de seguimiento, el Administrador de controladores se escribe en el archivo SQL. Inicie sesión en el directorio raíz.<br /><br /> Una aplicación puede establecer la variable **ODBCSharedTraceFlag** para habilitar el seguimiento de forma dinámica. Seguimiento está habilitado, a continuación, para todas las aplicaciones ODBC que se está ejecutando actualmente. Si una aplicación desactiva el seguimiento, se ha desactivado para la aplicación.<br /><br /> Si el **seguimiento** palabra clave en la información del sistema se establece en 1 cuando una aplicación llama a **SQLAllocHandle** con un *HandleType* de SQL_HANDLE_ENV, el seguimiento está habilitado para todos controla. Está habilitada solo para la aplicación que llama **SQLAllocHandle**.<br /><br /> Una llamada a **SQLSetConnectAttr** con un *atributo* de SQL_ATTR_TRACE no requiere que el *ConnectionHandle* argumento sea válido y no devolverá SQL_ERROR si *ConnectionHandle* es NULL. Este atributo se aplica a todas las conexiones.|  
|SQL_ATTR_TRACEFILE (ODBC 1.0)|Cadena de caracteres terminada en null que contiene el nombre del archivo de seguimiento.<br /><br /> El valor predeterminado del atributo SQL_ATTR_TRACEFILE se especifica con el **TraceFile** palabra clave en la información del sistema. Para obtener más información, consulte [subclave ODBC](../../../odbc/reference/install/odbc-subkey.md).<br /><br /> Una llamada a **SQLSetConnectAttr** con un *atributo* de SQL_ATTR_ TRACEFILE no requiere la *ConnectionHandle* argumento sea válido y no devolverá SQL_ERROR si *ConnectionHandle* no es válido. Este atributo se aplica a todas las conexiones.|  
|SQL_ATTR_TRANSLATE_LIB (ODBC 1.0)|Una cadena de caracteres terminada en null que contiene el nombre de una biblioteca que contiene las funciones **SQLDriverToDataSource** y **SQLDataSourceToDriver** que el controlador tiene acceso para realizar tareas como traducción del juego de caracteres. Esta opción puede ser especificado sólo si el controlador se ha conectado al origen de datos. La configuración de este atributo se conservará en todas las conexiones. Para obtener más información acerca de la traducción de datos, vea [archivos DLL de traducción](../../../odbc/reference/develop-app/translation-dlls.md) y [referencia de funciones DLL de traducción](../../../odbc/reference/syntax/translation-dll-api-reference.md).|  
|SQL_ATTR_TRANSLATE_OPTION (ODBC 1.0)|Un valor de marca de 32 bits que se pasa a la DLL de traducción. Este atributo puede ser especificado sólo si el controlador se ha conectado al origen de datos. Para obtener información acerca de la traducción de datos, vea [archivos DLL de traducción](../../../odbc/reference/develop-app/translation-dlls.md).|  
|SQL_ATTR_TXN_ISOLATION (ODBC 1.0)|Una máscara de bits de 32 bits que establece el nivel de aislamiento de transacción para la conexión actual. Una aplicación debe llamar a **SQLEndTran** para confirmar o revertir todas las transacciones abiertas en una conexión antes de llamar a **SQLSetConnectAttr** con esta opción.<br /><br /> Los valores válidos para *ValuePtr* puede determinarse mediante una llamada a **SQLGetInfo** con *InfoType* igual a SQL_TXN_ISOLATION_OPTIONS.<br /><br /> Para obtener una descripción de los niveles de aislamiento de transacción, vea la descripción del tipo de información SQL_DEFAULT_TXN_ISOLATION en [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) y [Transaction Isolation Levels](../../../odbc/reference/develop-app/transaction-isolation-levels.md).|  
  
 [1] estas funciones se pueden llamar de forma asincrónica solo si el descriptor es un descriptor de implementación, no un descriptor de la aplicación.  
  
## <a name="code-example"></a>Ejemplo de código  
 Consulte [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md).  
  
## <a name="related-functions"></a>Funciones relacionadas  
  
|Para obtener información acerca de|Vea|  
|---------------------------|---------|  
|Asignar un identificador|[Función SQLAllocHandle](../../../odbc/reference/syntax/sqlallochandle-function.md)|  
|Devuelve el valor de un atributo de conexión|[Función SQLGetConnectAttr](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|  
  
## <a name="see-also"></a>Vea también  
 [Referencia de la API de ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Archivos de encabezado de ODBC](../../../odbc/reference/install/odbc-header-files.md)
