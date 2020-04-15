---
title: Función SQLSetConnectAttr (SQLSetConnectAttr) Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8424462ddde4f99196e26d633fddfa5bb2ed6ee9
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301941"
---
# <a name="sqlsetconnectattr-function"></a>Función SQLSetConnectAttr
**Conformidad**  
 Versión introducida: Cumplimiento de normas ODBC 3.0: ISO 92  
  
 **Resumen**  
 **SQLSetConnectAttr** establece atributos que rigen aspectos de las conexiones.  
  
> [!NOTE]
>  Para obtener más información acerca de a qué asigna el Administrador de controladores esta función cuando una aplicación ODBC 3 *.x* está trabajando con un controlador ODBC 2 *.x,* vea Asignación de funciones de [reemplazo para la compatibilidad con versiones anteriores de aplicaciones](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md).  
  
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
 [Entrada] Atributo a establecer, que aparece en "Comentarios."  
  
 *ValuePtr*  
 [Entrada] Puntero al valor que se va a asociar a *Attribute*. Dependiendo del valor de *Attribute*, *ValuePtr* será un valor entero sin signo o apuntará a una cadena de caracteres terminada en null. Tenga en cuenta que el tipo entero de la *Attribute* argumento puede no ser de longitud fija, consulte el comentarios sección para obtener más detalles.  
  
 *StringLength*  
 [Entrada] Si *Attribute* es un atributo definido por ODBC y *ValuePtr* apunta a una cadena de caracteres o un búfer binario, este argumento debe ser la longitud de **ValuePtr*. Para los datos de cadena de caracteres, este argumento debe contener el número de bytes de la cadena.  
  
 Si *Attribute* es un atributo definido por ODBC y *ValuePtr* es un entero, *StringLength* se omite.  
  
 Si *Attribute* es un atributo definido por el controlador, la aplicación indica la naturaleza del atributo para el Administrador de controladores estableciendo el *StringLength* argumento. *StringLength* puede tener los siguientes valores:  
  
-   Si *ValuePtr* es un puntero a una cadena de caracteres, *StringLength* es la longitud de la cadena o SQL_NTS.  
  
-   Si *ValuePtr* es un puntero a un búfer binario, la aplicación coloca el resultado de la macro SQL_LEN_BINARY_ATTR(*length*) en *StringLength*. Esto coloca un valor negativo en *StringLength*.  
  
-   Si *ValuePtr* es un puntero a un valor distinto de una cadena de caracteres o una cadena binaria, *StringLength* debe tener el valor SQL_IS_POINTER.  
  
-   Si *ValuePtr* contiene un valor de longitud fija, *StringLength* es SQL_IS_INTEGER o SQL_IS_UINTEGER, según corresponda.  
  
## <a name="returns"></a>Devuelve  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR, SQL_INVALID_HANDLE o SQL_STILL_EXECUTING.  
  
## <a name="diagnostics"></a>Diagnóstico  
 Cuando **SQLSetConnectAttr** devuelve SQL_ERROR o SQL_SUCCESS_WITH_INFO, se puede obtener un valor SQLSTATE asociado llamando a **SQLGetDiagRec** con un *HandleType* de SQL_HANDLE_DBC y un *identificador* de *ConnectionHandle*. En la tabla siguiente se enumeran los valores SQLSTATE devueltos normalmente por **SQLSetConnectAttr** y se explica cada uno de ellos en el contexto de esta función; la notación "(DM)" precede a las descripciones de SQLSTATEs devueltas por el Administrador de controladores. El código de retorno asociado a cada valor SQLSTATE se SQL_ERROR, a menos que se indique lo contrario.  
  
 El controlador puede devolver SQL_SUCCESS_WITH_INFO para proporcionar información sobre el resultado de establecer una opción.  
  
|SQLSTATE|Error|Descripción|  
|--------------|-----------|-----------------|  
|01000|Advertencia general|Mensaje informativo específico del controlador. (La función devuelve SQL_SUCCESS_WITH_INFO.)|  
|01S02|Valor de opción cambiado|El controlador no admitió el valor especificado en *ValuePtr* y sustituyó un valor similar. (La función devuelve SQL_SUCCESS_WITH_INFO.)|  
|08002|Nombre de conexión en uso|El *argumento Attribute* se SQL_ATTR_ODBC_CURSORS y el controlador ya estaba conectado al origen de datos.|  
|08003|Conexión no abierta|(DM) se especificó un valor *de atributo* que requería una conexión abierta, pero *ConnectionHandle* no estaba en un estado conectado.|  
|08S01|Fallo del enlace de comunicación|Error en el vínculo de comunicación entre el controlador y el origen de datos al que estaba conectado el controlador antes de que la función completara el procesamiento.|  
|24000|Estado de cursor no válido|El *argumento Attribute* se SQL_ATTR_CURRENT_CATALOG y un conjunto de resultados estaba pendiente.|  
|25000|Operación ilegal en una transacción local|Una conexión estaba en una transacción local al intentar dar de alta en una conexión de transacción distribuida (DTC) estableciendo el atributo de conexión SQL_ATTR_ENLIST_IN_DTC.<br /><br /> Una conexión ya está inscrita en un DTC.<br /><br /> Se ha dado de alta una conexión en una conexión de transacción distribuida y se ha iniciado una transacción local estableciendo SQL_ATTR_AUTOCOMMIT en SQL_AUTOCOMMIT_OFF.|  
|3D000|Nombre de catálogo no válido|El *argumento Attribute* se SQL_CURRENT_CATALOG y el nombre de catálogo especificado no era válido.|  
|HY000|Error general|Se ha producido un error para el que no se ha definido sqlSTATE específico y para el que no se ha definido sqlSTATE específico de la implementación. El mensaje de error devuelto por **SQLGetDiagRec** en el * \*messageText* búfer describe el error y su causa.|  
|HY001|Error de asignación de memoria|El controlador no pudo asignar la memoria necesaria para admitir la ejecución o finalización de la función.|  
|HY008|Operación cancelada|El procesamiento asincrónico se ha habilitado para *ConnectionHandle*. Se llamó a la función **SQLSetConnectAttr** y, antes de completar la ejecución, se llamó a la [función SQLCancelHandle](../../../odbc/reference/syntax/sqlcancelhandle-function.md) en *ConnectionHandle*y, a continuación, se llamó de nuevo a la función **SQLSetConnectAttr** en *ConnectionHandle*.<br /><br /> O bien, se llamó a la función **SQLSetConnectAttr** y, antes de completar la ejecución, **sqlCancelHandle** se llamó en el *ConnectionHandle* desde un subproceso diferente en una aplicación multiproceso.|  
|HY009|Uso no válido de puntero nulo|El *atributo Attribute* argumento identificó un atributo de conexión que requería un valor de cadena y el *ValuePtr* argumento era un puntero nulo.|  
|HY010|Error de secuencia de funciones|(DM) se llamó a una función de ejecución asincrónica para un *StatementHandle* asociado con el *ConnectionHandle* y todavía se estaba ejecutando cuando **SQLSetConnectAttr** se llamó.<br /><br /> (DM) se llamó a una función de ejecución asincrónica (no esta) para *ConnectionHandle* y todavía se estaba ejecutando cuando se llamó a esta función.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**o **SQLMoreResults** se llamó para uno de los identificadores de instrucción asociados con el *ConnectionHandle* y devuelto SQL_PARAM_DATA_AVAILABLE. Se llamó a esta función antes de recuperar los datos para todos los parámetros transmitidos.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, o **SQLSetPos** se llamó para un *StatementHandle* asociado con el *ConnectionHandle* y devuelto SQL_NEED_DATA. Se llamó a esta función antes de que se enviaran datos para todos los parámetros o columnas de datos en ejecución.<br /><br /> (DM) **SQLBrowseConnect** se llamó para el *ConnectionHandle* y devuelto SQL_NEED_DATA. Esta función se llamó antes de **SQLBrowseConnect** devuelto SQL_SUCCESS_WITH_INFO o SQL_SUCCESS.|  
|HY011|Atributo no se puede establecer ahora|El *argumento Attribute* se SQL_ATTR_TXN_ISOLATION y una transacción estaba abierta.|  
|HY013|Error de administración de memoria|No se pudo procesar la llamada de función porque no se pudo tener acceso a los objetos de memoria subyacentes, posiblemente debido a condiciones de poca memoria.|  
|HY024|Valor de atributo no válido|Dado el valor *Attribute* especificado, se especificó un valor no válido en *ValuePtr*. (El Administrador de controladores devuelve este SQLSTATE solo para los atributos de conexión e instrucción que aceptan un conjunto discreto de valores, como SQL_ATTR_ACCESS_MODE o SQL_ATTR_ASYNC_ENABLE. Para todos los demás atributos de conexión e instrucción, el controlador debe comprobar el valor especificado en *ValuePtr*.)<br /><br /> El *attribute* argumento se SQL_ATTR_TRACEFILE o SQL_ATTR_TRANSLATE_LIB y *ValuePtr* era una cadena vacía.|  
|HY090|Cadena no válida o longitud de búfer|*(DM) \*ValuePtr* es una cadena de caracteres y el *StringLength* argumento era menor que 0 pero no se SQL_NTS.|  
|HY092|Identificador de atributo/opción no válido|(DM) el valor especificado para el argumento *Attribute* no era válido para la versión de ODBC admitida por el controlador.<br /><br /> (DM) el valor especificado para el argumento *Attribute* era un atributo de solo lectura.|  
|HY114|El controlador no admite la ejecución de funciones asincrónicas a nivel de conexión|(DM) Una aplicación intentó habilitar la ejecución de funciones asincrónicas con SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE para un controlador que no admite operaciones de conexión asincrónicas.|  
|HY117|La conexión se suspende debido al estado de transacción desconocido. Solo se permiten funciones de desconexión y de solo lectura.|(DM) Para obtener más información sobre el estado suspendido, vea [Función SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HY121|La biblioteca de cursores y la agrupación compatible con el controlador no se pueden habilitar al mismo tiempo|Para obtener más información, consulte Agrupación de [conexiones compatible con controladores](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md).|  
|HYC00|Característica opcional no implementada|El valor especificado para el argumento *Attribute* era una conexión ODBC válida o un atributo de instrucción para la versión de ODBC admitida por el controlador, pero no era compatible con el controlador.|  
|HYT01|Tiempo de espera de conexión expirado|El período de tiempo de espera de conexión expiró antes de que el origen de datos respondiera a la solicitud. El período de tiempo de espera de conexión se establece a través de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|El controlador no admite esta función|(DM) El controlador asociado a *ConnectionHandle* no admite la función.|  
|IM009|No se puede cargar DLL de traducción|El controlador no pudo cargar el archivo DLL de traducción que se especificó para la conexión. Este error solo se puede devolver cuando se SQL_ATTR_TRANSLATE_LIB *Attribute.*|  
|IM017|El sondeo está deshabilitado en el modo de notificación asincrónica|Siempre que se utiliza el modelo de notificación, el sondeo está deshabilitado.|  
|IM018|**SQLCompleteAsync** no se ha llamado para completar la operación asincrónica anterior en este identificador.|Si la llamada de función anterior en el identificador devuelve SQL_STILL_EXECUTING y si el modo de notificación está habilitado, **sqlCompleteAsync** debe llamarse en el identificador para realizar el procesamiento posterior y completar la operación.|  
|S1118|El controlador no admite la notificación asincrónica|SQL_ATTR_ASYNC_DBC_EVENT se estableció (después de realizar la conexión) pero el controlador no admite la notificación asincrónica.|  
  
 Cuando *Attribute* es un atributo de instrucción, **SQLSetConnectAttr** puede devolver cualquier SQLSTATEs devuelto por **SQLSetStmtAttr**.  
  
## <a name="comments"></a>Comentarios  
 Para obtener información general sobre los atributos de conexión, consulte [Atributos](../../../odbc/reference/develop-app/connection-attributes.md)de conexión .  
  
 Los atributos definidos actualmente y la versión de ODBC en la que se introdujeron se muestran en la tabla más adelante en esta sección; se espera que se definan más atributos para aprovechar los diferentes orígenes de datos. ODBC reserva un intervalo de atributos; los desarrolladores de controladores deben reservar valores para su propio uso específico del controlador de Open Group.  
  
> [!NOTE]
>  La capacidad de establecer atributos de instrucción en el nivel de conexión mediante una llamada a **SQLSetConnectAttr** ha quedado en desuso en ODBC 3 *.x*. Las aplicaciones ODBC 3 *.x* nunca deben establecer atributos de instrucción en el nivel de conexión. Los atributos de instrucción ODBC 3 *.x* no se pueden establecer en el nivel de conexión, con la excepción de los atributos SQL_ATTR_METADATA_ID y SQL_ATTR_ASYNC_ENABLE, que son atributos de conexión y atributos de instrucción y se pueden establecer en el nivel de conexión o en el nivel de instrucción.  
> 
>  Los controladores ODBC 3 *.x* solo necesitan admitir esta funcionalidad si deben trabajar con aplicaciones ODBC 2 *.x* que establezcan opciones de instrucción ODBC 2 *.x* en el nivel de conexión. Para obtener más información, vea [Asignación de SQLSetConnectOption](../../../odbc/reference/appendixes/sqlsetconnectoption-mapping.md) en Apéndice G: Directrices de controlador para la compatibilidad con versiones anteriores.  
  
 Una aplicación puede llamar a **SQLSetConnectAttr** en cualquier momento entre el momento en que se asigna y libera la conexión. Todos los atributos de conexión e instrucción establecidos correctamente por la aplicación para la conexión persisten hasta **sqlFreeHandle** se llama en la conexión. Por ejemplo, si una aplicación llama a **SQLSetConnectAttr** antes de conectarse a un origen de datos, el atributo persiste incluso si **SQLSetConnectAttr** produce un error en el controlador cuando la aplicación se conecta al origen de datos; si una aplicación establece un atributo específico del controlador, el atributo persiste incluso si la aplicación se conecta a un controlador diferente en la conexión.  
  
 Algunos atributos de conexión solo se pueden establecer antes de que se haya realizado una conexión; otros se pueden establecer sólo después de que se haya realizado una conexión. En la tabla siguiente se indican los atributos de conexión que se deben establecer antes o después de que se haya realizado una conexión. *Indica* que el atributo se puede establecer antes o después de la conexión.  
  
|Atributo|¿Establecer antes o después de la conexión?|  
|---------------|-------------------------------------|  
|SQL_ATTR_ACCESS_MODE|Ya sea[1]|  
|SQL_ATTR_ASYNC_DBC_EVENT|Es posible usar el|  
|SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE|Ya sea[4]|  
|SQL_ATTR_ASYNC_DBC_PCALLBACK|Es posible usar el|  
|SQL_ATTR_ASYNC_DBC_PCONTEXT|Es posible usar el|  
|SQL_ATTR_ASYNC_ENABLE|Ya sea[2]|  
|SQL_ATTR_AUTO_IPD|Es posible usar el|  
|SQL_ATTR_AUTOCOMMIT|Ya sea[5]|  
|SQL_ATTR_CONNECTION_DEAD|Después|  
|SQL_ATTR_CONNECTION_TIMEOUT|Es posible usar el|  
|SQL_ATTR_CURRENT_CATALOG|Ya sea[1]|  
|SQL_ATTR_DBC_INFO_TOKEN|Después|  
|SQL_ATTR_ENLIST_IN_DTC|Después|  
|SQL_ATTR_LOGIN_TIMEOUT|Antes del|  
|SQL_ATTR_METADATA_ID|Es posible usar el|  
|SQL_ATTR_ODBC_CURSORS|Antes del|  
|SQL_ATTR_PACKET_SIZE|Antes del|  
|SQL_ATTR_QUIET_MODE|Es posible usar el|  
|SQL_ATTR_TRACE|Es posible usar el|  
|SQL_ATTR_TRACEFILE|Es posible usar el|  
|SQL_ATTR_TRANSLATE_LIB|Después|  
|SQL_ATTR_TRANSLATE_OPTION|Después|  
|SQL_ATTR_TXN_ISOLATION|Ya sea[3]|  
  
 [1] SQL_ATTR_ACCESS_MODE y SQL_ATTR_CURRENT_CATALOG se pueden ajustar antes o después de la conexión, dependiendo del controlador. Sin embargo, las aplicaciones interoperables las establecen antes de conectarse porque algunos controladores no admiten cambiarlos después de la conexión.  
  
 [2] SQL_ATTR_ASYNC_ENABLE debe establecerse antes de que haya una declaración activa.  
  
 [3] SQL_ATTR_TXN_ISOLATION solo se puede establecer si no hay transacciones abiertas en la conexión. Algunos atributos de conexión admiten la sustitución de un \*valor similar si el origen de datos no admite el valor especificado en *ValuePtr*. En tales casos, el controlador devuelve SQL_SUCCESS_WITH_INFO y SQLSTATE 01S02 (valor de opción cambiado). Por ejemplo, *Attribute* si Attribute \*es SQL_ATTR_PACKET_SIZE y *ValuePtr* supera el tamaño máximo de paquete, el controlador sustituye el tamaño máximo. Para determinar el valor sustituido, una aplicación llama a **SQLGetConnectAttr**.  
  
 [4] Si se establece SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE antes de que se abra una conexión, el Administrador de controladores establecerá el atributo del controlador cuando se cargue el controlador durante una llamada a **SQLBrowseConnect**, **SQLConnect**o **SQLDriverConnect**. Antes de una llamada a **SQLBrowseConnect**, **SQLConnect**o **SQLDriverConnect**, el Administrador de controladores no sabe a qué controlador conectarse y no sabe si el controlador admite operaciones de conexión asincrónicas. Por lo tanto, el Administrador de controladores siempre devuelve SQL_SUCCESS. Pero, en caso de que el controlador no admita operaciones de conexión asincrónicas, se producirá un error en la llamada a **SQLBrowseConnect**, **SQLConnect**o **SQLDriverConnect.**  
  
 [5] Cuando SQL_ATTR_AUTOCOMMIT se establece en FALSE, las aplicaciones deben llamar a SQLEndTran(SQL_ROLLBACK) si alguna API devuelve SQL_ERROR para garantizar la coherencia transaccional.  
  
 El formato de la \*información establecida en el búfer *ValuePtr* depende del *atributo*especificado . **SQLSetConnectAttr** aceptará información de atributo en uno de los dos formatos diferentes: una cadena de caracteres terminada en null o un valor entero. El formato de cada uno se indica en la descripción del atributo. Las cadenas de caracteres señaladas por el *ValuePtr* argumento de **SQLSetConnectAttr** tienen una longitud de *StringLength* bytes.  
  
 El *StringLength* argumento se omite si la longitud se define por el atributo, como es el caso para todos los atributos introducidos en ODBC 2 *.x* o anterior.  
  
|*Atributo*|*Contenido valuePtr*|  
|-----------------|-------------------------|  
|SQL_ATTR_ACCESS_MODE (ODBC 1.0)|Un valor SQLUINTEGER. SQL_MODE_READ_ONLY es utilizado por el controlador o el origen de datos como un indicador de que la conexión no es necesaria para admitir instrucciones SQL que hacen que se produzcan actualizaciones. Este modo se puede utilizar para optimizar las estrategias de bloqueo, la administración de transacciones u otras áreas según corresponda al controlador o al origen de datos. El controlador no es necesario para evitar que dichas instrucciones se envíen al origen de datos. El comportamiento del controlador y el origen de datos cuando se le pide que procese instrucciones SQL que no son de solo lectura durante una conexión de solo lectura está definido por la implementación. SQL_MODE_READ_WRITE es el valor predeterminado.|  
|SQL_ATTR_ASYNC_DBC_EVENT (ODBC 3.8)|Un valor SQLPOINTER que es un identificador de evento.<br /><br /> La notificación de la finalización de funciones asincrónicas se habilita llamando a **SQLSetConnectAttr** con el atributo SQL_ATTR_ASYNC_STMT_EVENT y especificando el identificador de evento. **Nota:**  El método de notificación no es compatible con la biblioteca de cursores. Una aplicación recibirá un mensaje de error si intenta habilitar la biblioteca de cursores a través de SQLSetConnectAttr, cuando el método de notificación está habilitado.|  
|SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE (ODBC 3.8)|Un valor SQLUINTEGER que habilita o deshabilita la ejecución asincrónica de las funciones seleccionadas en el identificador de conexión. Para obtener más información, vea [Ejecución asincrónica (método de sondeo).](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md)<br /><br /> SQL_ASYNC_DBC_ENABLE_ON: habilite la operación asincrónica para las funciones relacionadas con la conexión especificadas.<br /><br /> SQL_ASYNC_DBC_ENABLE_OFF (predeterminado) Deshabilitar la operación asincrónica para las funciones relacionadas con la conexión especificadas.<br /><br /> Establecer SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE siempre es sincrónico (es decir, nunca volverá SQL_STILL_EXECUTING).<br /><br /> La ejecución asincrónica de operaciones de instrucción se habilita con SQL_ATTR_ASYNC_ENABLE.|  
|SQL_ATTR_ASYNC_DBC_PCALLBACK (ODBC 3.8)|Valor SQLPOINTER que apunta a la estructura de contexto.<br /><br /> Solo el Administrador de controladores puede llamar a la función **SQLSetStmtAttr** de un controlador con este atributo.|  
|SQL_ATTR_ASYNC_DBC_PCONTEXT (ODBC 3.8)|Valor SQLPOINTER que apunta a la estructura de contexto.<br /><br /> Solo el Administrador de controladores puede llamar a la función **SQLSetStmtAttr** de un controlador con este atributo.|  
|SQL_ATTR_ASYNC_ENABLE (ODBC 3.0)|Un valor SQLULEN que especifica si una función a la que se llama con una instrucción en la conexión especificada se ejecuta de forma asincrónica:<br /><br /> SQL_ASYNC_ENABLE_OFF: deshabilitar la compatibilidad de ejecución asincrónica de nivel de conexión para operaciones de instrucción (valor predeterminado).<br /><br /> SQL_ASYNC_ENABLE_ON: Habilitar la compatibilidad de ejecución asincrónica de nivel de conexión para operaciones de instrucción.<br /><br /> Este atributo se puede establecer si **SQLGetInfo** con el tipo de información SQL_ASYNC_MODE devuelve SQL_AM_CONNECTION o SQL_AM_STATEMENT.|  
|SQL_ATTR_AUTO_IPD (ODBC 3.0)|Un valor SQLUINTEGER de solo lectura que especifica si se admite el rellenado automático de la IPD después de una llamada a **SQLPrepare:**<br /><br /> SQL_TRUE: el controlador admite la población automática de la IPD después de una llamada a **SQLPrepare.**<br /><br /> SQL_FALSE: el controlador no admite la población automática de la IPD después de una llamada a **SQLPrepare.** Los servidores que no admiten instrucciones preparadas no podrán rellenar el IPD automáticamente.<br /><br /> Si se devuelve SQL_TRUE para el atributo de conexión SQL_ATTR_AUTO_IPD, el atributo de instrucción SQL_ATTR_ENABLE_AUTO_IPD se puede establecer para activar o desactivar el rellenado automático de la IPD. Si SQL_ATTR_AUTO_IPD es SQL_FALSE, no se puede establecer SQL_ATTR_ENABLE_AUTO_IPD en SQL_TRUE. El valor predeterminado de SQL_ATTR_ENABLE_AUTO_IPD es igual al valor de SQL_ATTR_AUTO_IPD.<br /><br /> **SQLGetConnectAttr** puede devolver este atributo de conexión, pero **SQLSetConnectAttr**no puede establecerlo.|  
|SQL_ATTR_AUTOCOMMIT (ODBC 1.0)|Un valor SQLUINTEGER que especifica si se debe utilizar el modo de confirmación automática o de confirmación manual:<br /><br /> SQL_AUTOCOMMIT_OFF: el controlador utiliza el modo de confirmación manual y la aplicación debe confirmar o revertir explícitamente las transacciones con **SQLEndTran**.<br /><br /> SQL_AUTOCOMMIT_ON: el controlador utiliza el modo de confirmación automática. Cada instrucción se confirma inmediatamente después de ejecutarla. Este es el valor predeterminado. Las transacciones abiertas en la conexión se confirman cuando SQL_ATTR_AUTOCOMMIT se establece en SQL_AUTOCOMMIT_ON cambiar del modo de confirmación manual al modo de confirmación automática.<br /><br /> Para obtener más información, consulte [Modo de confirmación](../../../odbc/reference/develop-app/commit-mode.md). **Importante:**  Algunos orígenes de datos eliminan los planes de acceso y cierran los cursores de todas las instrucciones de una conexión cada vez que se confirma una instrucción; El modo de confirmación automática puede hacer que esto suceda después de ejecutar cada instrucción que no sea de consulta o cuando se cierra el cursor para una consulta. Para obtener más información, vea los tipos de información SQL_CURSOR_COMMIT_BEHAVIOR y SQL_CURSOR_ROLLBACK_BEHAVIOR en [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) y [Efecto de las transacciones en cursores e instrucciones preparadas](../../../odbc/reference/develop-app/effect-of-transactions-on-cursors-and-prepared-statements.md). <br /><br /> Cuando un lote se ejecuta en modo de confirmación automática, son posibles dos cosas. El lote completo se puede tratar como una unidad autocommitable, o cada instrucción de un lote se trata como una unidad autocommitable. Ciertos orígenes de datos pueden admitir ambos comportamientos y pueden proporcionar una manera de elegir uno u otro. Se define por el controlador si un lote se trata como una unidad autocommitable o si cada instrucción individual dentro del lote es autocommitable.|  
|SQL_ATTR_CONNECTION_DEAD<br /><br /> (ODBC 3.5)|Un valor SQLUINTEGER de solo lectura que indica el estado de la conexión. Si SQL_CD_TRUE, se ha perdido la conexión. Si SQL_CD_FALSE, la conexión sigue activa.|  
|SQL_ATTR_CONNECTION_TIMEOUT (ODBC 3.0)|Un valor SQLUINTEGER correspondiente al número de segundos para esperar a que se complete cualquier solicitud en la conexión antes de volver a la aplicación. El controlador debe devolver SQLSTATE HYT00 (tiempo de espera expirado) en cualquier momento que sea posible agotar el tiempo de espera en una situación no asociada con la ejecución de consultas o el inicio de sesión.<br /><br /> Si *ValuePtr* es igual a 0 (valor predeterminado), no hay tiempo de espera.|  
|SQL_ATTR_CURRENT_CATALOG (ODBC 2.0)|Cadena de caracteres que contiene el nombre del catálogo que utilizará el origen de datos. Por ejemplo, en SQL ServerSQL Server, el catálogo es una base de datos, por lo \*que el controlador envía una instrucción **USE** _database_ al origen de datos, donde *database* es la base de datos especificada en *ValuePtr*. Para un controlador de un solo nivel, el catálogo podría ser un directorio, por lo que el controlador cambia su directorio actual al directorio especificado en **ValuePtr*.|  
|SQL_ATTR_DBC_INFO_TOKEN (ODBC 3.8|Un valor SQLPOINTER utilizado para establecer el token de información de conexión\*en el identificador DBC cuando [SQLRateConnection](../../../odbc/reference/syntax/sqlrateconnection-function.md)'s (*pRating*) parámetro no es igual a 100.<br /><br /> SQL_ATTR_DBC_INFO_TOKEN es solo establecido. No es posible usar **SQLGetConnectAttr** o **SQLGetConnectOption** para recuperar este valor. **SQLSetConnectAttr** del Administrador de controladores no aceptará SQL_ATTR_DBC_INFO_TOKEN, ya que una aplicación no debe establecer este atributo.<br /><br /> Si un controlador devuelve SQL_ERROR después de establecer SQL_ATTR_DBC_INFO_TOKEN, la conexión que acaba de obtener del grupo se liberará. El Administrador de controladores intentará obtener otra conexión del grupo. Consulte Desarrollo de la conciencia [del grupo de conexiones en un controlador ODBC](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md) para obtener más información.|  
|SQL_ATTR_ENLIST_IN_DTC (ODBC 3.0)|Un valor SQLPOINTER que especifica si se debe usar el controlador ODBC en transacciones distribuidas coordinadas por Servicios de componentes de Microsoft.<br /><br /> Pase un objeto de transacción OLE DTC que especifique la transacción que se va a exportar a SQL ServerSQL Server o SQL_DTC_DONE finalizar la asociación DTC de la conexión.<br /><br /> El cliente llama al método OLE ITransactionDispenser::BeginTransaction del Coordinador de transacciones distribuidas de Microsoft (MS DTC) para iniciar una transacción de MS DTC y crear un objeto de transacción de MS DTC que represente la transacción. A continuación, la aplicación llama a SQLSetConnectAttr con la opción SQL_ATTR_ENLIST_IN_DTC para asociar el objeto de transacción con la conexión ODBC. Toda la actividad de base de datos relacionada se realizará bajo la protección de la transacción MS DTC. La aplicación llama a SQLSetConnectAttr con SQL_DTC_DONE para finalizar la asociación DTC de la conexión. Para obtener más información, consulte la documentación de MS DTC.|  
|SQL_ATTR_LOGIN_TIMEOUT (ODBC 1.0)|Un valor SQLUINTEGER correspondiente al número de segundos que se debe esperar a que se complete una solicitud de inicio de sesión antes de volver a la aplicación. El valor predeterminado depende del controlador. Si *ValuePtr* es 0, el tiempo de espera está deshabilitado y un intento de conexión esperará indefinidamente.<br /><br /> Si el tiempo de espera especificado supera el tiempo de espera de inicio de sesión máximo en el origen de datos, el controlador sustituye ese valor y devuelve SQLSTATE 01S02 (valor de opción cambiado).|  
|SQL_ATTR_METADATA_ID (ODBC 3.0)|Un valor SQLUINTEGER que determina cómo se tratan los argumentos de cadena de las funciones de catálogo.<br /><br /> Si SQL_TRUE, el argumento de cadena de las funciones de catálogo se tratan como identificadores. El caso no es significativo. Para las cadenas no delimitadas, el controlador quita los espacios finales y la cadena se pliega en mayúsculas. Para las cadenas delimitadas, el controlador quita los espacios iniciales o finales y toma literalmente lo que hay entre los delimitadores. Si uno de estos argumentos se establece en un puntero nulo, la función devuelve SQL_ERROR y SQLSTATE HY009 (uso no válido del puntero nulo).<br /><br /> Si SQL_FALSE, los argumentos de cadena de las funciones de catálogo no se tratan como identificadores. El caso es significativo. Pueden contener un patrón de búsqueda de cadena o no, dependiendo del argumento.<br /><br /> El valor predeterminado es SQL_FALSE.<br /><br /> El argumento *TableType* de **SQLTables**, que toma una lista de valores, no se ve afectado por este atributo.<br /><br /> SQL_ATTR_METADATA_ID también se pueden establecer en el nivel de instrucción. (Es el único atributo de conexión que también es un atributo de instrucción.)<br /><br /> Para obtener más información, vea [Argumentos en funciones](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md)de catálogo .|  
|SQL_ATTR_ODBC_CURSORS (ODBC 2.0)|Un valor SQLULEN que especifica cómo el Administrador de controladores utiliza la biblioteca de cursores ODBC:<br /><br /> SQL_CUR_USE_IF_NEEDED: el Administrador de controladores utiliza la biblioteca de cursores ODBC solo si es necesario. Si el controlador admite la opción SQL_FETCH_PRIOR en **SQLFetchScroll**, el Administrador de controladores usa las capacidades de desplazamiento del controlador. De lo contrario, utiliza la biblioteca de cursores ODBC.<br /><br /> SQL_CUR_USE_ODBC: el Administrador de controladores utiliza la biblioteca de cursores ODBC.<br /><br /> SQL_CUR_USE_DRIVER: el Administrador de controladores utiliza las capacidades de desplazamiento del controlador. Esta es la configuración predeterminada.<br /><br /> Para obtener más información acerca de la biblioteca de cursores ODBC, vea [Apéndice F: Biblioteca](../../../odbc/reference/appendixes/appendix-f-odbc-cursor-library.md)de cursores ODBC . **Advertencia:**  La biblioteca de cursores se eliminará en una versión futura de Windows. Evite usar esta característica en el nuevo trabajo de desarrollo y planee modificar las aplicaciones que actualmente utilizan esta característica. Microsoft recomienda usar la funcionalidad del cursor del controlador.|  
|SQL_ATTR_PACKET_SIZE (ODBC 2.0)|Un valor SQLUINTEGER que especifica el tamaño del paquete de red en bytes. **Nota:**  Muchas fuentes de datos no admiten esta opción o solo pueden devolver pero no establecer el tamaño del paquete de red. <br /><br /> Si el tamaño especificado supera el tamaño máximo del paquete o es menor que el tamaño mínimo del paquete, el controlador sustituye ese valor y devuelve SQLSTATE 01S02 (valor de opción cambiado).<br /><br /> Si la aplicación establece el tamaño del paquete después de que ya se ha realizado una conexión, el controlador devolverá SQLSTATE HY011 (el atributo no se puede establecer ahora).|  
|SQL_ATTR_QUIET_MODE (ODBC 2.0)|Un identificador de ventana (HWND).<br /><br /> Si el identificador de ventana es un puntero nulo, el controlador no muestra ningún cuadro de diálogo.<br /><br /> Si el identificador de ventana no es un puntero nulo, debe ser el identificador de ventana principal de la aplicación. Este es el valor predeterminado. El controlador utiliza este identificador para mostrar cuadros de diálogo. **Nota:**  El atributo de conexión SQL_ATTR_QUIET_MODE no se aplica a los cuadros de diálogo mostrados por **SQLDriverConnect**.|  
|SQL_ATTR_TRACE (ODBC 1.0)|Un valor SQLUINTEGER que indica al Administrador de controladores si desea realizar el seguimiento:<br /><br /> SQL_OPT_TRACE_OFF - Seguimiento desactivado (valor predeterminado)<br /><br /> SQL_OPT_TRACE_ON - Seguimiento en<br /><br /> Cuando el seguimiento está activado, el Administrador de controladores escribe cada llamada de función ODBC en el archivo de seguimiento. **Nota:**  Cuando el seguimiento está activado, el Administrador de controladores puede devolver SQLSTATE IM013 (error de archivo de seguimiento) desde cualquier función. <br /><br /> Una aplicación especifica un archivo de seguimiento con la opción SQL_ATTR_TRACEFILE. Si el archivo ya existe, el Administrador de controladores se anexa al archivo. De lo contrario, crea el archivo. Si el seguimiento está activado y no se ha especificado ningún archivo de seguimiento, el Administrador de controladores escribe en el archivo SQL. LOG en el directorio raíz.<br /><br /> Una aplicación puede establecer la variable **ODBCSharedTraceFlag** para habilitar el seguimiento dinámicamente. A continuación, se habilita el seguimiento para todas las aplicaciones ODBC que se ejecutan actualmente. Si una aplicación desactiva el seguimiento, se desactiva solo para esa aplicación.<br /><br /> Si la palabra clave **Trace** de la información del sistema se establece en 1 cuando una aplicación llama a **SQLAllocHandle** con un *HandleType* de SQL_HANDLE_ENV, el seguimiento está habilitado para todos los identificadores. Solo está habilitado para la aplicación que llamó a **SQLAllocHandle**.<br /><br /> Llamar a **SQLSetConnectAttr** con un *atributo* de SQL_ATTR_TRACE no requiere que el *ConnectionHandle* argumento sea válido y no devolverá SQL_ERROR si *ConnectionHandle* es NULL. Este atributo se aplica a todas las conexiones.|  
|SQL_ATTR_TRACEFILE (ODBC 1.0)|Cadena de caracteres terminada en null que contiene el nombre del archivo de seguimiento.<br /><br /> El valor predeterminado del atributo SQL_ATTR_TRACEFILE se especifica con la palabra clave **TraceFile** en la información del sistema. Para obtener más información, vea [Subclave ODBC](../../../odbc/reference/install/odbc-subkey.md).<br /><br /> Llamar a **SQLSetConnectAttr** con un *atributo* de SQL_ATTR_ TRACEFILE no requiere el *ConnectionHandle* argumento sea válido y no devolverá SQL_ERROR si *ConnectionHandle* no es válido. Este atributo se aplica a todas las conexiones.|  
|SQL_ATTR_TRANSLATE_LIB (ODBC 1.0)|Cadena de caracteres terminada en null que contiene el nombre de una biblioteca que contiene las funciones **SQLDriverToDataSource** y **SQLDataSourceToDriver** a las que el controlador tiene acceso para realizar tareas como la traducción de conjuntos de caracteres. Esta opción solo se puede especificar si el controlador se ha conectado al origen de datos. La configuración de este atributo persistirá en las conexiones. Para obtener más información sobre la traducción de datos, vea Referencia de [funciones](../../../odbc/reference/develop-app/translation-dlls.md) DLL de traducción [y](../../../odbc/reference/syntax/translation-dll-api-reference.md)DLL de traducción .|  
|SQL_ATTR_TRANSLATE_OPTION (ODBC 1.0)|Un valor de indicador de 32 bits que se pasa al archivo DLL de traducción. Este atributo solo se puede especificar si el controlador se ha conectado al origen de datos. Para obtener información sobre la traducción de datos, consulte [DLL de traducción](../../../odbc/reference/develop-app/translation-dlls.md).|  
|SQL_ATTR_TXN_ISOLATION (ODBC 1.0)|Una máscara de bits de 32 bits que establece el nivel de aislamiento de transacción para la conexión actual. Una aplicación debe llamar a **SQLEndTran** para confirmar o revertir todas las transacciones abiertas en una conexión, antes de llamar a **SQLSetConnectAttr** con esta opción.<br /><br /> Los valores válidos para *ValuePtr* se pueden determinar llamando a **SQLGetInfo** con *InfoType* igual a SQL_TXN_ISOLATION_OPTIONS.<br /><br /> Para obtener una descripción de los niveles de aislamiento de transacción, vea la descripción del tipo de información SQL_DEFAULT_TXN_ISOLATION en [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) y niveles de aislamiento de [transacción](../../../odbc/reference/develop-app/transaction-isolation-levels.md).|  
  
 [1] Estas funciones se pueden llamar de forma asincrónica solo si el descriptor es un descriptor de implementación, no un descriptor de aplicación.  
  
## <a name="code-example"></a>Ejemplo de código  
 Consulte [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md).  
  
## <a name="related-functions"></a>Funciones relacionadas  
  
|Para información acerca de|Vea|  
|---------------------------|---------|  
|Asignación de un asa|[Función SQLAllocHandle](../../../odbc/reference/syntax/sqlallochandle-function.md)|  
|Devolver la configuración de un atributo de conexión|[Función SQLGetConnectAttr](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de la API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Archivos de encabezado de ODBC](../../../odbc/reference/install/odbc-header-files.md)
