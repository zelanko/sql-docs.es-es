---
title: Función SQLSetConnectAttr | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql-non-specified
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
- SQLSetConnectAttr
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLSetConnectAttr
helpviewer_keywords:
- SQLSetConnectAttr function [ODBC]
ms.assetid: 97fc7445-5a66-4eb9-8e77-10990b5fd685
caps.latest.revision: 83
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 806acdd35452ff22e922158ed071d41d8e45f031
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="sqlsetconnectattr-function"></a>Función SQLSetConnectAttr
**Conformidad**  
 Versión introdujo: ODBC 3.0 normativas: ISO 92  
  
 **Resumen**  
 **SQLSetConnectAttr** establece atributos que controlan aspectos de las conexiones.  
  
> [!NOTE]  
>  Para obtener más información sobre lo que el Administrador de controladores se asigna esta función cuando una aplicación ODBC 3*.x* aplicación está trabajando con una API ODBC 2*.x* controladores, consulte [asignación de funciones de reemplazo para hacia atrás Compatibilidad de las aplicaciones](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
SQLRETURN SQLSetConnectAttr(  
     SQLHDBC       ConnectionHandle,  
     SQLINTEGER    Attribute,  
     SQLPOINTER    ValuePtr,  
     SQLINTEGER    StringLength);  
```  
  
## <a name="arguments"></a>Argumentos  
 *IdentificadorConexión*  
 [Entrada] Identificador de conexión.  
  
 *Atributo*  
 [Entrada] Atributo que se establecerá, aparecen en "Comentarios".  
  
 *ValuePtr*  
 [Entrada] Puntero a la capacidad de asociarse *atributo*. Dependiendo del valor de *atributo*, *ValuePtr* será un valor entero sin signo o hará referencia a una cadena de caracteres terminada en null. Tenga en cuenta que el tipo de la integral de la *atributo* argumento puede no ser de longitud fija, vea la sección Comentarios para obtener información detallada.  
  
 *StringLength*  
 [Entrada] Si *atributo* es un atributo definido en ODBC y *ValuePtr* apunta a una cadena de caracteres o un búfer binario, este argumento debe ser la longitud de **ValuePtr*. Para los datos de cadena de caracteres, este argumento debe contener el número de bytes en la cadena.  
  
 Si *atributo* es un atributo definido en ODBC y *ValuePtr* es un entero, *StringLength* se omite.  
  
 Si *atributo* es un atributo definido por el controlador, la aplicación indica la naturaleza del atributo para el Administrador de controladores al establecer el *StringLength* argumento. *StringLength* puede tener los valores siguientes:  
  
-   Si *ValuePtr* es un puntero a una cadena de caracteres, a continuación, *StringLength* es la longitud de la cadena o SQL_NTS.  
  
-   Si *ValuePtr* es un puntero a un búfer binario, a continuación, la aplicación coloca el resultado de la SQL_LEN_BINARY_ATTR (*longitud*) macro en *StringLength*. Esto coloca un valor negativo en *StringLength*.  
  
-   Si *ValuePtr* es un puntero a un valor distinto de una cadena de caracteres o una cadena binaria, a continuación, *StringLength* debería tener el valor SQL_IS_POINTER.  
  
-   Si *ValuePtr* contiene un valor de longitud fija, a continuación, *StringLength* es SQL_IS_INTEGER o SQL_IS_UINTEGER, según corresponda.  
  
## <a name="returns"></a>Devuelve  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR, SQL_INVALID_HANDLE o SQL_STILL_EXECUTING.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Cuando **SQLSetConnectAttr** devuelve SQL_ERROR o SQL_SUCCESS_WITH_INFO, un valor SQLSTATE asociado se puede obtener mediante una llamada a **SQLGetDiagRec** con un *HandleType* de SQL_HANDLE_DBC y un *controlar* de *IdentificadorConexión*. En la tabla siguiente se enumera los valores SQLSTATE devueltos normalmente por **SQLSetConnectAttr** y se explica cada uno de ellos en el contexto de esta función; la notación "(DM)" precede a las descripciones de SQLSTATE devuelto por el Administrador de controladores. El código de retorno asociado a cada valor SQLSTATE es SQL_ERROR, a menos que se indique lo contrario.  
  
 El controlador puede devuelve SQL_SUCCESS_WITH_INFO para proporcionar información sobre el resultado de una opción de configuración.  
  
|SQLSTATE|Error|Description|  
|--------------|-----------|-----------------|  
|01000|Advertencia general|Mensaje informativo de específicas del controlador. (La función devuelve SQL_SUCCESS_WITH_INFO).|  
|01S02 DE SQLSTATE|Ha cambiado el valor de opción|El controlador no admitía el valor especificado en *ValuePtr* y sustituir un valor similar. (La función devuelve SQL_SUCCESS_WITH_INFO).|  
|08002|Nombre de la conexión en uso|El *atributo* argumento era SQL_ATTR_ODBC_CURSORS y el controlador ya estaba conectado al origen de datos.|  
|08003|Conexión no abierta|(DM) un *atributo* se especificó un valor que requiere una conexión abierta, pero la *IdentificadorConexión* no estaba en estado conectado.|  
|08S01|Error de vínculo de comunicación|El vínculo de comunicación entre el controlador y el origen de datos al que se conectó el controlador no pudo antes del procesamiento de la función se ha completado.|  
|24000|Estado de cursor no válido|El *atributo* argumento era SQL_ATTR_CURRENT_CATALOG y era de un conjunto de resultados pendiente.|  
|25000|Operación no válida en una transacción local|Una conexión se encontraba en una transacción local al intentar dar de alta en una conexión de transacciones distribuidas (DTC) estableciendo el atributo de conexión SQL_ATTR_ENLIST_IN_DTC.<br /><br /> Una conexión ya está dada de alta en un DTC.<br /><br /> Se ha dado de alta una conexión en una conexión de transacción distribuida y se inicia una transacción local estableciendo SQL_ATTR_AUTOCOMMIT como SQL_AUTOCOMMIT_OFF.|  
|3D000|Nombre de catálogo no válido|El *atributo* argumento era SQL_CURRENT_CATALOG y el nombre de catálogo especificado no era válido.|  
|HY000|Error general|Se produjo un error para que no hubo ninguna SQLSTATE específico y para el que se ha definido ningún SQLSTATE específico de la implementación. El mensaje de error devuelto por **SQLGetDiagRec** en el  *\*MessageText* búfer describe el error y su causa.|  
|HY001|Error de asignación de memoria|El controlador no pudo asignar la memoria necesaria para admitir la ejecución o la finalización de la función.|  
|HY008|Operación cancelada|Procesamiento asincrónico se habilitó para la *IdentificadorConexión*. El **SQLSetConnectAttr** se llamó a función y antes que completó la ejecución, el [SQLCancelHandle función](../../../odbc/reference/syntax/sqlcancelhandle-function.md) se llamó en la *IdentificadorConexión*y, a continuación, el **SQLSetConnectAttr** función llamó de nuevo en el *IdentificadorConexión*.<br /><br /> O bien, el **SQLSetConnectAttr** se llamó a función y antes que completó la ejecución, **SQLCancelHandle** se llamó en la *IdentificadorConexión* desde un subproceso diferente en una aplicación multiproceso.|  
|HY009|Uso no válido del puntero null|El *atributo* argumento identifica un atributo de conexión que requiere un valor de cadena, y el *ValuePtr* argumento era un puntero nulo.|  
|HY010|Error de secuencia de función|(DM) se llamó a una función ejecuta de forma asincrónica para una *StatementHandle* asociados con el *IdentificadorConexión* y aún se estaba ejecutando cuando **SQLSetConnectAttr**se llamó.<br /><br /> (DM) se llamó a una función ejecuta de forma asincrónica (no esta uno) para la *IdentificadorConexión* y aún se estaba ejecutando cuando se llamó a esta función.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, o **SQLMoreResults** se llama para uno de los identificadores de instrucción asociados a la *IdentificadorConexión* y devuelve SQL_PARAM_DATA_AVAILABLE. Esta función se invoca antes de que se recuperan los datos para todos los parámetros transmitidos.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, o **SQLSetPos** se piden un *StatementHandle*  asociados con el *IdentificadorConexión* y devuelve SQL_NEED_DATA. Esta función se invoca antes de que se enviaron los datos para todas las columnas o parámetros de datos en ejecución.<br /><br /> (DM) **SQLBrowseConnect** se llamó para el *IdentificadorConexión* y devuelve SQL_NEED_DATA. Esta función se invoca antes de **SQLBrowseConnect** devuelve SQL_SUCCESS_WITH_INFO o SQL_SUCCESS.|  
|HY011|Atributo no se puede establecer ahora|El *atributo* argumento era SQL_ATTR_TXN_ISOLATION y una transacción estaba abierta.|  
|HY013|Error de administración de memoria|No se pudo procesar la llamada de función porque los objetos subyacentes de la memoria no se pudieron tener acceso, posiblemente debido a condiciones de memoria insuficiente.|  
|HY024|Valor de atributo no válido|Dada la especificado *atributo* valor, que se especificó un valor no válido en *ValuePtr*. (El Administrador de controladores devuelve este valor de SQLSTATE solo para la conexión y los atributos de instrucción que aceptan un conjunto discreto de valores, como SQL_ATTR_ACCESS_MODE o SQL_ATTR_ASYNC_ENABLE. Para el resto de conexión y los atributos de instrucción, el controlador debe comprobar el valor especificado en *ValuePtr*.)<br /><br /> El *atributo* argumento era SQL_ATTR_TRACEFILE o SQL_ATTR_TRANSLATE_LIB, y *ValuePtr* era una cadena vacía.|  
|HY090|Longitud de búfer o cadena no válida|*(DM) \*ValuePtr* es una cadena de caracteres y la *StringLength* argumento era menor que 0 pero no SQL_NTS.|  
|HY092|Identificador de opción o atributo no válido|(DM) el valor especificado para el argumento *atributo* no era válido para la versión de ODBC compatible con el controlador.<br /><br /> (DM) el valor especificado para el argumento *atributo* era un atributo de sólo lectura.|  
|HY114|Controlador no admite la ejecución de la función de nivel de conexión asincrónica|(DM) una aplicación intentó habilitar la ejecución de la función asincrónica con SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE para un controlador que no admite operaciones de conexión asincrónica.|  
|HY117|Se suspende la conexión debido al estado de transacción desconocido. Solo se desconecte y se permiten las funciones de solo lectura.|(DM) para obtener más información sobre el estado suspendido, consulte [función SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HY121|Biblioteca de cursores y agrupación dependientes del controlador no se puede habilitar al mismo tiempo|Para obtener más información, consulte [agrupación de conexiones dependientes del controlador](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md).|  
|HYC00|Característica opcional no implementada|El valor especificado para el argumento *atributo* era una conexión ODBC válida o atributo de instrucción para la versión de ODBC compatibles con el controlador, pero no era compatible con el controlador.|  
|HYT01|Tiempo de espera de conexión expirado|El período de tiempo de espera de conexión finalizó antes de que el origen de datos se respondió a la solicitud. El período de tiempo de espera de conexión se establece a través de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Controlador no admite esta función|(DM) el controlador asociado a la *IdentificadorConexión* no admite la función.|  
|IM009|No se puede cargar el archivo DLL de traducción|El controlador no pudo cargar la DLL que se especificó para la conexión de traducción. Puede aparecer este error solo cuando *atributo* es SQL_ATTR_TRANSLATE_LIB.|  
|IM017|Sondeo está deshabilitado en el modo de notificación asincrónica|Cada vez que se utiliza el modelo de notificación, se deshabilita el sondeo.|  
|IM018|**SQLCompleteAsync** no se ha llamado para completar la operación asincrónica anterior en este identificador.|Si la llamada de función anterior en el controlador devuelve SQL_STILL_EXECUTING y si está habilitado el modo de notificación, **SQLCompleteAsync** se debe llamar en el identificador para realizar el procesamiento posterior a la y completar la operación.|  
|S1118|Controlador no admite la notificación asincrónica|Se estableció SQL_ATTR_ASYNC_DBC_EVENT (después de que se realizó la conexión) pero el controlador no admite la notificación asincrónica.|  
  
 Cuando *atributo* es un atributo de instrucción, **SQLSetConnectAttr** puede devolver cualquier SQLSTATE devuelto por **SQLSetStmtAttr**.  
  
## <a name="comments"></a>Comentarios  
 Para obtener información general acerca de los atributos de conexión, vea [atributos de conexión](../../../odbc/reference/develop-app/connection-attributes.md).  
  
 Se muestran los atributos definidos actualmente y la versión de ODBC en el que se introdujeron en la tabla más adelante en esta sección; se espera que se definirá más atributos para aprovechar las ventajas de diferentes orígenes de datos. Un intervalo de atributos está reservado por ODBC; los desarrolladores de controladores deben reservar los valores para su propio uso específicos del controlador de Open Group.  
  
> [!NOTE]  
>  Permite establecer atributos de instrucción en el nivel de conexión mediante una llamada a **SQLSetConnectAttr** está en desuso en ODBC 3*.x*. ODBC 3*.x* aplicaciones nunca deben establecer los atributos de instrucción en el nivel de conexión. ODBC 3*.x* atributos de instrucción no se puede establecer en el nivel de conexión, a excepción de los atributos SQL_ATTR_METADATA_ID y SQL_ATTR_ASYNC_ENABLE, que son atributos de conexión y los atributos de instrucción y se puede Establezca en el nivel de conexión o en el nivel de instrucción.  
>   
>  ODBC 3*.x* controladores sólo necesitan admitir esta funcionalidad si deben trabajar con ODBC 2*.x* aplicación que establezca ODBC 2*.x* opciones de la instrucción en el nivel de conexión. Para obtener más información, consulte [SQLSetConnectOption asignación](../../../odbc/reference/appendixes/sqlsetconnectoption-mapping.md) en Apéndice G: controlador directrices para la compatibilidad con versiones anteriores.  
  
 Una aplicación puede llamar a **SQLSetConnectAttr** en cualquier momento entre el momento en que se asignar y liberar la conexión. Todos los atributos de conexión e instrucción correctamente establecidos por la aplicación para la conexión se conservan hasta que **SQLFreeHandle** se llama en la conexión. Por ejemplo, si una aplicación llama **SQLSetConnectAttr** antes de conectarse a un origen de datos, el atributo persiste incluso si **SQLSetConnectAttr** produce un error en el controlador cuando la aplicación se conecta a la origen de datos; Si una aplicación establece un atributo específico del controlador, el atributo persiste incluso si la aplicación se conecta a un controlador diferente en la conexión.  
  
 Algunos atributos de conexión se pueden establecer sólo antes de que se ha realizado una conexión; otras se pueden establecer solo después de que se ha realizado una conexión. En la tabla siguiente indica los atributos de conexión que se deben establecer antes o después de que se ha realizado una conexión. *Cualquier* indica que se puede establecer el atributo antes o después de la conexión.  
  
|Attribute|¿Establecer antes o después de la conexión?|  
|---------------|-------------------------------------|  
|SQL_ATTR_ACCESS_MODE|[1]|  
|SQL_ATTR_ASYNC_DBC_EVENT|Antes o después|  
|SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE|Ambos [4]|  
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
  
 [1] SQL_ATTR_ACCESS_MODE y SQL_ATTR_CURRENT_CATALOG pueden establecerse antes o después de conectarse, según el controlador. Sin embargo, aplicaciones interoperables establecerlas antes de conectarse porque algunos controladores no admiten cambiar estos después de conectarse.  
  
 [2] SQL_ATTR_ASYNC_ENABLE debe establecerse antes de realizar una instrucción activa.  
  
 [3] SQL_ATTR_TXN_ISOLATION puede establecerse solo si no hay ninguna transacción abierta en la conexión. Algunos atributos de conexión admiten la sustitución de un valor similar si el origen de datos no es compatible con el valor especificado en \* *ValuePtr*. En tales casos, el controlador devuelve SQL_SUCCESS_WITH_INFO y SQLSTATE 01S02 de SQLState (valor de opción cambiado). Por ejemplo, si *atributo* es SQL_ATTR_PACKET_SIZE y \* *ValuePtr* supera el tamaño máximo de paquete, el controlador sustituye el tamaño máximo. Para determinar el valor sustituido, llama a una aplicación **SQLGetConnectAttr**.  
  
 [4] si SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE se establece antes de que una conexión está abierta, el Administrador de controladores establecerá el atributo del controlador cuando se carga el controlador durante una llamada a **SQLBrowseConnect**, **SQLConnect**, o **SQLDriverConnect**. Antes de llamar a **SQLBrowseConnect**, **SQLConnect**, o **SQLDriverConnect**, el Administrador de controladores no sabe qué controlador al que conectarse y no sabe si el controlador es compatible con las operaciones de conexión asincrónica. Por lo tanto, el Administrador de controladores siempre devuelve SQL_SUCCESS. Pero, en caso de que el controlador no admite operaciones de conexión asincrónica, la llamada a **SQLBrowseConnect**, **SQLConnect**, o **SQLDriverConnect** se producirá un error.  
  
 [5] cuando SQL_ATTR_AUTOCOMMIT se establece en FALSE, las aplicaciones deben llamar a SQLEndTran(SQL_ROLLBACK) si cualquier API devuelve SQL_ERROR para garantizar la coherencia transaccional.  
  
 El formato de información establecida en el \* *ValuePtr* búfer depende especificado *atributo*. **SQLSetConnectAttr** aceptará información de atributos en uno de dos formatos diferentes: una cadena de caracteres terminada en null o un valor entero. El formato de cada uno se indica en la descripción del atributo. Caracteres de cadenas que señala el *ValuePtr* argumento de **SQLSetConnectAttr** tienen una longitud de *StringLength* bytes.  
  
 El *StringLength* argumento se omite si la longitud está definida por el atributo, como es el caso de todos los atributos que se introdujo en ODBC 2*.x* o una versión anterior.  
  
|*Atributo*|*ValuePtr* contenido|  
|-----------------|-------------------------|  
|SQL_ATTR_ACCESS_MODE (ODBC 1.0)|Un valor SQLUINTEGER. El controlador o el origen de datos usa SQL_MODE_READ_ONLY como un indicador de que la conexión no es necesaria para admitir instrucciones SQL que se producen actualizaciones que se produzca. Este modo se puede utilizar para optimizar las estrategias de bloqueos, administración de transacciones u otras áreas según corresponda para el controlador u origen de datos. El controlador no es necesario para evitar tales instrucciones desde el que se envía al origen de datos. El comportamiento del controlador y el origen de datos cuando se le pregunte para procesar instrucciones SQL que no son de solo lectura durante una conexión de solo lectura es definido por la implementación. SQL_MODE_READ_WRITE es el valor predeterminado.|  
|SQL_ATTR_ASYNC_DBC_EVENT (ODBC 3.8)|Un valor SQLPOINTER es un identificador de evento.<br /><br /> Notificación de la finalización de funciones asincrónicas está habilitado mediante una llamada a **SQLSetConnectAttr** con el atributo SQL_ATTR_ASYNC_STMT_EVENT y especificar el controlador de eventos. **Nota:** el método de notificación no es compatible con la biblioteca de cursores. Una aplicación recibirá el mensaje de error si intenta habilitar la biblioteca de cursores a través de SQLSetConnectAttr, cuando el método de notificación está habilitado.|  
|SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE (ODBC 3.8)|Un valor SQLUINTEGER que habilita o deshabilita la ejecución asincrónica de las funciones seleccionadas en el identificador de conexión. Para obtener más información, consulte [ejecución asincrónica (método de sondeo)](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md).<br /><br /> SQL_ASYNC_DBC_ENABLE_ON = Enable en la operación asincrónica para funciones relacionadas con la conexión especificadas.<br /><br /> SQL_ASYNC_DBC_ENABLE_OFF = Disable (valor predeterminado) en la operación asincrónica para funciones relacionadas con la conexión especificadas.<br /><br /> Establecer SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE siempre es sincrónica (es decir, nunca devolverá SQL_STILL_EXECUTING).<br /><br /> Ejecución asincrónica de las operaciones de la instrucción se habilitan con SQL_ATTR_ASYNC_ENABLE.|  
|SQL_ATTR_ASYNC_DBC_PCALLBACK (ODBC 3.8)|Un valor SQLPOINTER que apunta a la estructura de contexto.<br /><br /> Solo el Administrador de controladores puede llamar a un controlador **SQLSetStmtAttr** función con este atributo.|  
|SQL_ATTR_ASYNC_DBC_PCONTEXT (ODBC 3.8)|Un valor SQLPOINTER que apunta a la estructura de contexto.<br /><br /> Solo el Administrador de controladores puede llamar a un controlador **SQLSetStmtAttr** función con este atributo.|  
|SQL_ATTR_ASYNC_ENABLE (ODBC 3.0)|Un valor SQLULEN que especifica si llama a una función con una instrucción en la conexión especificada se ejecuta de forma asincrónica:<br /><br /> SQL_ASYNC_ENABLE_OFF = Deshabilitar conexión nivel ejecución asincrónica la compatibilidad con operaciones de instrucción (valor predeterminado).<br /><br /> SQL_ASYNC_ENABLE_ON = habilitar el soporte de nivel de ejecución asincrónica de conexión para las operaciones de instrucción.<br /><br /> Este atributo se puede establecer si **SQLGetInfo** con la información de SQL_ASYNC_MODE tipo devuelve SQL_AM_CONNECTION o SQL_AM_STATEMENT.|  
|SQL_ATTR_AUTO_IPD (ODBC 3.0)|Un valor SQLUINTEGER de solo lectura que especifica si el rellenado automático de la IPD después de llamar a **SQLPrepare** se admite:<br /><br /> SQL_TRUE = el rellenado automático de la IPD después de llamar a **SQLPrepare** es compatible con el controlador.<br /><br /> SQL_FALSE = el rellenado automático de la IPD después de llamar a **SQLPrepare** no es compatible con el controlador. Servidores que no son compatibles con instrucciones preparadas no podrá rellenar automáticamente el IPD.<br /><br /> Si se devuelve SQL_TRUE para el atributo de conexión SQL_ATTR_AUTO_IPD, el atributo de instrucción SQL_ATTR_ENABLE_AUTO_IPD puede establecerse para activar o desactivar el rellenado automático de la IPD. Si SQL_ATTR_AUTO_IPD es SQL_FALSE, SQL_ATTR_ENABLE_AUTO_IPD no se puede establecer en SQL_TRUE. El valor predeterminado de SQL_ATTR_ENABLE_AUTO_IPD es igual que el valor de SQL_ATTR_AUTO_IPD.<br /><br /> Este atributo de conexión puede ser devueltos por **SQLGetConnectAttr** pero no se puede establecer **SQLSetConnectAttr**.|  
|SQL_ATTR_AUTOCOMMIT (ODBC 1.0)|Un valor SQLUINTEGER que especifica si se usa el modo de confirmación automática o manual:<br /><br /> SQL_AUTOCOMMIT_OFF = el controlador usa el modo de confirmación manual, y la aplicación debe confirmar o revertir las transacciones con explícitamente **SQLEndTran**.<br /><br /> SQL_AUTOCOMMIT_ON = controlador utiliza en el modo de confirmación automática. Cada instrucción se confirma inmediatamente después de que se ejecuta. Ésta es la opción predeterminada. Las transacciones abiertas en la conexión se confirman cuando SQL_ATTR_AUTOCOMMIT está establecido en SQL_AUTOCOMMIT_OFF para cambiar del modo de confirmación manual al modo de confirmación automática.<br /><br /> Para obtener más información, consulte [confirmar modo](../../../odbc/reference/develop-app/commit-mode.md). **Importante:** algunos orígenes de datos eliminar los planes de acceso y cerrar los cursores para todas las instrucciones en una conexión cada vez que una instrucción se confirma; modo de confirmación automática puede hacer que esto ocurre después de ejecutar cada instrucción nonquery o cuando el cursor está cerrado en una consulta. Para obtener más información, vea los tipos de información SQL_CURSOR_COMMIT_BEHAVIOR y SQL_CURSOR_ROLLBACK_BEHAVIOR en [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) y [efecto de las transacciones en los cursores y las instrucciones preparadas](../../../odbc/reference/develop-app/effect-of-transactions-on-cursors-and-prepared-statements.md). <br /><br /> Si un lote se ejecuta en modo de confirmación automática, son posibles las dos cosas. Todo el lote se puede tratar como una unidad autocommitable o cada instrucción en un lote se trata como una unidad de autocommitable. Algunos orígenes de datos pueden admitir ambos estos comportamientos y pueden proporcionar una manera de elegir uno u otro. Es definido por el controlador si un lote se trata como una unidad autocommitable o si cada instrucción individual dentro del lote es autocommitable.|  
|SQL_ATTR_CONNECTION_DEAD<br /><br /> (ODBC 3.5)|Un valor SQLUINTEGER de solo lectura que indica el estado de la conexión. Si SQL_CD_TRUE, la conexión se ha perdido. Si SQL_CD_FALSE, la conexión todavía está activa.|  
|SQL_ATTR_CONNECTION_TIMEOUT (ODBC 3.0)|Un valor SQLUINTEGER correspondiente al número de segundos de espera para cualquier solicitud en la conexión para completarse antes de devolver a la aplicación. El controlador debería devolver SQLSTATE HYT00 (tiempo de espera expirado) siempre que sea posible tiempo de espera en una situación no asociada con la ejecución de la consulta o el inicio de sesión.<br /><br /> Si *ValuePtr* es igual a 0 (valor predeterminado), no hay ningún tiempo de espera.|  
|SQL_ATTR_CURRENT_CATALOG (ODBC 2.0)|Una cadena de caracteres que contiene el nombre del catálogo que va a usar el origen de datos. Por ejemplo, en SQL Server, el catálogo es una base de datos, por lo que el controlador envía un **USE** *base de datos* instrucción al origen de datos, donde *base de datos* se especifica la base de datos en \* *ValuePtr*. Para un controlador de nivel único, el catálogo podría ser un directorio, por lo que el controlador cambia su directorio actual en el directorio especificado en **ValuePtr*.|  
|SQL_ATTR_DBC_INFO_TOKEN (ODBC 3.8|Un valor SQLPOINTER que se usa para establecer volver el símbolo (token) de información de conexión en el DBC controlar cuándo [SQLRateConnection](../../../odbc/reference/syntax/sqlrateconnection-function.md)del (\**pRating*) parámetro no es igual a 100.<br /><br /> SQL_ATTR_DBC_INFO_TOKEN es solo para establecer. No es posible utilizar **SQLGetConnectAttr** o **SQLGetConnectOption** para recuperar este valor. El Administrador de controladores **SQLSetConnectAttr** no aceptará SQL_ATTR_DBC_INFO_TOKEN, puesto que una aplicación no debe establecer este atributo.<br /><br /> Si un controlador devuelve SQL_ERROR después de establecer SQL_ATTR_DBC_INFO_TOKEN, se libera la conexión que solo se obtiene del grupo. El Administrador de controladores intentará obtener otra conexión del grupo. Vea [desarrollar conocimiento de la agrupación de conexiones en un controlador ODBC](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md) para obtener más información.|  
|SQL_ATTR_ENLIST_IN_DTC (ODBC 3.0)|Un valor SQLPOINTER que especifica si se usa el controlador ODBC en transacciones distribuidas coordinadas por servicios de componentes de Microsoft.<br /><br /> Pasar un DTC OLE objeto transaction que especifica la transacción para exportar a SQL Server o SQL_DTC_DONE para finalizar la asociación de conexión DTC.<br /><br /> El cliente llama al método de coordinador de transacciones distribuidas de Microsoft (MS DTC) OLE ITransactionDispenser:: BeginTransaction para iniciar una transacción de MS DTC y crear un objeto de transacción de MS DTC que representa la transacción. A continuación, la aplicación llama a SQLSetConnectAttr con la opción SQL_ATTR_ENLIST_IN_DTC para asociar el objeto de transacción con la conexión ODBC. Toda la actividad de base de datos relacionada se realizará bajo la protección de la transacción MS DTC. La aplicación llama SQLSetConnectAttr con SQL_DTC_DONE para finalizar la asociación de conexión DTC. Para obtener más información, consulte la documentación de MS DTC.|  
|SQL_ATTR_LOGIN_TIMEOUT (ODBC 1.0)|Un valor SQLUINTEGER correspondiente al número de segundos de espera para que una solicitud de inicio de sesión para completarse antes de devolver a la aplicación. El valor predeterminado depende del controlador. Si *ValuePtr* es 0, se deshabilita el tiempo de espera y un intento de conexión esperará indefinidamente.<br /><br /> Si el tiempo de espera especificado supera el tiempo de espera máximo de inicio de sesión en el origen de datos, el controlador sustituye ese valor y devuelve 01S02 SQLSTATE (valor de opción cambiado).|  
|SQL_ATTR_METADATA_ID (ODBC 3.0)|Un valor SQLUINTEGER que determina cómo se tratan los argumentos de cadena de funciones de catálogo.<br /><br /> Si SQL_TRUE, el argumento de cadena de funciones de catálogo se tratan como identificadores. El caso no es significativo. Para cadenas sin delimitar, el controlador quita los espacios finales y se dobla la cadena a mayúsculas. Para cadenas delimitadas, el controlador quita los espacios iniciales o finales y toma literalmente lo que es entre los delimitadores. Si se establece uno de estos argumentos a un puntero nulo, la función devuelve SQL_ERROR y SQLSTATE HY009 (uso no válido del puntero null).<br /><br /> Si SQL_FALSE, los argumentos de cadena de funciones de catálogo no se tratan como identificadores. El caso es significativo. O bien pueden contener un patrón de búsqueda de cadena o no, dependiendo del argumento.<br /><br /> El valor predeterminado es SQL_FALSE.<br /><br /> El *TableType* argumento de **SQLTables**, que toma una lista de valores, no se ve afectada por este atributo.<br /><br /> SQL_ATTR_METADATA_ID también puede establecerse en el nivel de instrucción. (Es el atributo de conexión único que también es un atributo de instrucción).<br /><br /> Para obtener más información, consulte [argumentos de las funciones de catálogo](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md).|  
|SQL_ATTR_ODBC_CURSORS (ODBC 2.0)|Un valor de SQLULEN especifica cómo el Administrador de controladores usa la biblioteca de cursores ODBC:<br /><br /> SQL_CUR_USE_IF_NEEDED = el Administrador de controladores utiliza la biblioteca de cursores ODBC si es necesario. Si el controlador admite la opción SQL_FETCH_PRIOR en **SQLFetchScroll**, el Administrador de controladores usa las capacidades de desplazamiento del controlador. En caso contrario, utiliza la biblioteca de cursores ODBC.<br /><br /> SQL_CUR_USE_ODBC = el Administrador de controladores utiliza la biblioteca de cursores ODBC.<br /><br /> SQL_CUR_USE_DRIVER = el Administrador de controladores usa las capacidades de desplazamiento del controlador. Esta es la configuración predeterminada.<br /><br /> Para obtener más información acerca de la biblioteca de cursores ODBC, vea [biblioteca de cursores ODBC Apéndice F:](../../../odbc/reference/appendixes/appendix-f-odbc-cursor-library.md). **Advertencia:** la biblioteca de cursores se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y piense en modificar las aplicaciones que actualmente utilizan esta característica. Microsoft recomienda usar la funcionalidad del controlador cursor.|  
|SQL_ATTR_PACKET_SIZE (ODBC 2.0)|Un valor SQLUINTEGER especifica el tamaño de paquete de red en bytes. **Nota:** muchos orígenes de datos no son compatibles con esta opción o sólo puede devuelto pero no se estableció el tamaño del paquete de red. <br /><br /> Si el tamaño especificado supera el tamaño máximo del paquete o es menor que el tamaño mínimo de paquete, el controlador sustituye ese valor y devuelve 01S02 SQLSTATE (valor de opción cambiado).<br /><br /> Si la aplicación establece el tamaño de paquete después de que ya se ha realizado una conexión, el controlador devolverá SQLSTATE HY011 (atributo no se puede establecer ahora).|  
|SQL_ATTR_QUIET_MODE (ODBC 2.0)|Un identificador de ventana (HWND).<br /><br /> Si el identificador de ventana es un puntero nulo, el controlador no muestra los cuadros de diálogo.<br /><br /> Si el identificador de ventana no es un puntero nulo, debe ser el identificador de la ventana principal de la aplicación. Ésta es la opción predeterminada. El controlador usa este identificador para mostrar cuadros de diálogo. **Nota:** el atributo de conexión SQL_ATTR_QUIET_MODE no se aplica a los cuadros de diálogo mostrados por **SQLDriverConnect**.|  
|SQL_ATTR_TRACE (ODBC 1.0)|Un valor SQLUINTEGER que indica si se debe realizar un seguimiento del Administrador de controladores:<br /><br /> SQL_OPT_TRACE_OFF = seguimiento off (valor predeterminado)<br /><br /> SQL_OPT_TRACE_ON = seguimiento en<br /><br /> Cuando el seguimiento está activado, el Administrador de controladores escribe cada llamada de función ODBC en el archivo de seguimiento. **Nota:** cuando el seguimiento está activado, el Administrador de controladores puede devolver SQLSTATE IM013 (error de archivo de seguimiento) de cualquier función. <br /><br /> Una aplicación especifica un archivo de seguimiento con la opción SQL_ATTR_TRACEFILE. Si el archivo ya existe, el Administrador de controladores se anexa al archivo. En caso contrario, crea el archivo. Si el seguimiento está activado y no se ha especificado ningún archivo de seguimiento, el Administrador de controladores se escribe en el archivo SQL. Inicie sesión en el directorio raíz.<br /><br /> Una aplicación puede establecer la variable **ODBCSharedTraceFlag** para habilitar el seguimiento de forma dinámica. Seguimiento está habilitado, a continuación, para todas las aplicaciones de ODBC que se está ejecutando actualmente. Si una aplicación desactiva el seguimiento, que se ha desactivado sólo para esa aplicación.<br /><br /> Si el **seguimiento** palabra clave en la información del sistema se establece en 1 cuando una aplicación llama **SQLAllocHandle** con un *HandleType* de SQL_HANDLE_ENV, el seguimiento está habilitado para todas las controla. Está habilitado solo para la aplicación que llama **SQLAllocHandle**.<br /><br /> Al llamar a **SQLSetConnectAttr** con una *atributo* de SQL_ATTR_TRACE no requiere que el *IdentificadorConexión* argumento sea válido y no devuelve SQL_ERROR si *IdentificadorConexión* es NULL. Este atributo se aplica a todas las conexiones.|  
|SQL_ATTR_TRACEFILE (ODBC 1.0)|Cadena de caracteres terminada en null que contiene el nombre del archivo de seguimiento.<br /><br /> El valor predeterminado del atributo SQL_ATTR_TRACEFILE se especifica con el **TraceFile** palabra clave en la información del sistema. Para obtener más información, consulte [subclave ODBC](../../../odbc/reference/install/odbc-subkey.md).<br /><br /> Al llamar a **SQLSetConnectAttr** con una *atributo* de SQL_ATTR_ TRACEFILE no requiere la *IdentificadorConexión* argumento sea válido y no devuelve SQL_ERROR si *IdentificadorConexión* no es válido. Este atributo se aplica a todas las conexiones.|  
|SQL_ATTR_TRANSLATE_LIB (ODBC 1.0)|Una cadena de caracteres terminada en null que contiene el nombre de una biblioteca que contiene las funciones **SQLDriverToDataSource** y **SQLDataSourceToDriver** que tiene acceso los controladores para llevar a cabo tareas como traducción del conjunto de caracteres. Esta opción puede ser especificado solo si el controlador ha conectado al origen de datos. El valor de este atributo se conservará en las conexiones. Para obtener más información acerca de cómo traducir datos, vea [archivos DLL de traducción](../../../odbc/reference/develop-app/translation-dlls.md) y [referencia de funciones de DLL de traducción](../../../odbc/reference/syntax/translation-dll-api-reference.md).|  
|SQL_ATTR_TRANSLATE_OPTION (ODBC 1.0)|Un valor de marca de 32 bits que se pasa a la DLL de traducción. Este atributo se puede especificar únicamente si el controlador ha conectado al origen de datos. Para obtener información acerca de cómo traducir datos, vea [archivos DLL de traducción](../../../odbc/reference/develop-app/translation-dlls.md).|  
|SQL_ATTR_TXN_ISOLATION (ODBC 1.0)|Una máscara de bits de 32 bits que establece el nivel de aislamiento de transacción para la conexión actual. Una aplicación debe llamar a **SQLEndTran** para confirmar o revertir todas las transacciones abiertas en una conexión antes de llamar a **SQLSetConnectAttr** con esta opción.<br /><br /> Los valores válidos para *ValuePtr* se puede determinar mediante una llamada a **SQLGetInfo** con *tipo de información* igual a SQL_TXN_ISOLATION_OPTIONS.<br /><br /> Para obtener una descripción de los niveles de aislamiento de transacción, vea la descripción del tipo de información SQL_DEFAULT_TXN_ISOLATION en [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) y [Transaction Isolation Levels](../../../odbc/reference/develop-app/transaction-isolation-levels.md).|  
  
 [1] estas funciones se pueden llamar de forma asincrónica solo si el descriptor es un descriptor de implementación, no un descriptor de la aplicación.  
  
## <a name="code-example"></a>Ejemplo de código  
 Vea [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md).  
  
## <a name="related-functions"></a>Funciones relacionadas  
  
|Para obtener información acerca de|Vea|  
|---------------------------|---------|  
|Asignar un identificador|[Función SQLAllocHandle](../../../odbc/reference/syntax/sqlallochandle-function.md)|  
|Devolver el valor de un atributo de conexión|[Función SQLGetConnectAttr](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|  
  
## <a name="see-also"></a>Vea también  
 [Referencia de la API de ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Archivos de encabezado de ODBC](../../../odbc/reference/install/odbc-header-files.md)
