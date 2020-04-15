---
title: Función SQLEndTran ? Microsoft Docs
ms.custom: ''
ms.date: 07/18/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLEndTran
apilocation:
- sqlsrv32.dll
- odbc32.dll
apitype: dllExport
f1_keywords:
- SQLEndTran
helpviewer_keywords:
- SQLEndTran function [ODBC]
ms.assetid: ff375ce1-eb50-4693-b1e6-70181a6dbf9f
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: cce7792e52fce4984f3da41e11d79c34b6b79e53
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302746"
---
# <a name="sqlendtran-function"></a>Función SQLEndTran
**Conformidad**  
 Versión introducida: Cumplimiento de normas ODBC 3.0: ISO 92  
  
 **Resumen**  
 **SQLEndTran** solicita una operación de confirmación o reversión para todas las operaciones activas en todas las instrucciones asociadas a una conexión. **SQLEndTran** también puede solicitar que se realice una operación de confirmación o reversión para todas las conexiones asociadas a un entorno.  
  
> [!NOTE]  
>  Para obtener más información acerca de lo que el Administrador de controladores asigna esta función a cuando un ODBC 3. *x* aplicación está trabajando con un ODBC 2. *x* driver, consulte Asignación de [funciones de reemplazo para compatibilidad con versiones anteriores de aplicaciones](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md).  
  
## <a name="syntax"></a>Sintaxis  
  
```cpp  
  
SQLRETURN SQLEndTran(  
     SQLSMALLINT   HandleType,  
     SQLHANDLE     Handle,  
     SQLSMALLINT   CompletionType);  
```  
  
## <a name="arguments"></a>Argumentos  
 *HandleType*  
 [Entrada] Identificador de tipo de identificador de identificador de identificador. Contiene SQL_HANDLE_ENV (si *Handle* es un identificador de entorno) o SQL_HANDLE_DBC (si *Handle* es un identificador de conexión).  
  
 *Handle*  
 [Entrada] Identificador, del tipo indicado por *HandleType*, que indica el ámbito de la transacción. Consulte "Comentarios" para obtener más información.  
  
 *CompletionType*  
 [Entrada] Uno de los dos valores siguientes:  
  
 SQL_COMMIT SQL_ROLLBACK  
  
## <a name="returns"></a>Devuelve  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR, SQL_INVALID_HANDLE o SQL_STILL_EXECUTING.  
  
## <a name="diagnostics"></a>Diagnóstico  
 Cuando **SQLEndTran** devuelve SQL_ERROR o SQL_SUCCESS_WITH_INFO, se puede obtener un valor SQLSTATE asociado llamando a **SQLGetDiagRec** con el *HandleType* y *Handle*adecuados . En la tabla siguiente se enumeran los valores SQLSTATE devueltos normalmente por **SQLEndTran** y se explica cada uno de ellos en el contexto de esta función; la notación "(DM)" precede a las descripciones de SQLSTATEs devueltas por el Administrador de controladores. El código de retorno asociado a cada valor SQLSTATE se SQL_ERROR, a menos que se indique lo contrario.  
  
|SQLSTATE|Error|Descripción|  
|--------------|-----------|-----------------|  
|01000|Advertencia general|Mensaje informativo específico del controlador. (La función devuelve SQL_SUCCESS_WITH_INFO.)|  
|08003|Conexión no abierta|(DM) el *HandleType* se SQL_HANDLE_DBC y el *handle* no estaba en un estado conectado.|  
|08007|Error de conexión durante la transacción|El *HandleType* se SQL_HANDLE_DBC y la conexión asociada con el *control* falló durante la ejecución de la función y no se puede determinar si el **COMMIT** o **ROLLBACK** solicitado se produjo antes del error.|  
|25S01|Estado de la transacción desconocido|Una o varias de las conexiones de *Handle* no pudieron completar la transacción con el resultado especificado y se desconoce el resultado.|  
|25S02|La transacción sigue activa|El controlador no pudo garantizar que todo el trabajo en la transacción global se pudiera completar atómicamente y la transacción sigue activa.|  
|25S03|La transacción se revierte|El controlador no pudo garantizar que todo el trabajo en la transacción global se pudiera completar atómicamente, y todo el trabajo en la transacción activa en *Handle* se revirtió.|  
|40001|Error de serialización|La transacción se revirtió debido a un interbloqueo de recursos con otra transacción.|  
|40002|Violación de la restricción de integridad|El *CompletionType* se SQL_COMMIT y el compromiso de los cambios causó infracción de restricción de integridad. Como resultado, la transacción se revirtió.|  
|HY000|Error general|Se ha producido un error para el que no se ha definido sqlSTATE específico y para el que no se ha definido sqlSTATE específico de la implementación. El mensaje de error devuelto por **SQLGetDiagRec** en el * \*búfer szMessageText* describe el error y su causa.|  
|HY001|Error de asignación de memoria|El controlador no pudo asignar la memoria necesaria para admitir la ejecución o finalización de la función.|  
|HY008|Operación cancelada|El procesamiento asincrónico se ha habilitado para *ConnectionHandle*. Se llamó a la función y antes de que terminara de ejecutar [SQLCancelHandle Function](../../../odbc/reference/syntax/sqlcancelhandle-function.md) se llamó en *ConnectionHandle*. A continuación, se volvió a llamar a la función en *ConnectionHandle*.<br /><br /> Se llamó a la función y antes de que terminara de ejecutar **SQLCancelHandle** se llamó en el *ConnectionHandle* desde un subproceso diferente en una aplicación multiproceso.|  
|HY010|Error de secuencia de funciones|(DM) se llamó a una función de ejecución asincrónica para un identificador de instrucción asociado con el *ConnectionHandle* y todavía se estaba ejecutando cuando **SQLEndTran** se llamó.<br /><br /> (DM) se llamó a una función de ejecución asincrónica (no esta) para *ConnectionHandle* y todavía se estaba ejecutando cuando se llamó a esta función.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, o **SQLSetPos** se llamó para un identificador de instrucción asociado con el *ConnectionHandle* y devuelto SQL_NEED_DATA. Se llamó a esta función antes de que se enviaran datos para todos los parámetros o columnas de datos en ejecución.<br /><br /> (DM) se llamó a una función de ejecución asincrónica (no esta) para el *Handle* con *HandleType* establecido en SQL_HANDLE_DBC y todavía se estaba ejecutando cuando se llamó a esta función.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**o **SQLMoreResults** se llamó para uno de los identificadores de instrucción asociados con *Handle* y devuelto SQL_PARAM_DATA_AVAILABLE. Se llamó a esta función antes de recuperar los datos para todos los parámetros transmitidos.|  
|HY012|Código de operación de transacción no válido|(DM) el valor especificado para el argumento *CompletionType* no era SQL_COMMIT ni SQL_ROLLBACK.|  
|HY013|Error de administración de memoria|No se pudo procesar la llamada de función porque no se pudo tener acceso a los objetos de memoria subyacentes, posiblemente debido a condiciones de poca memoria.|  
|HY092|Identificador de atributo/opción no válido|(DM) el valor especificado para el argumento *HandleType* no era SQL_HANDLE_ENV ni SQL_HANDLE_DBC.|  
|HY115|SQLEndTran no está permitido para un entorno que contiene una conexión con la ejecución de funciones asincrónicas habilitadas|(DM) *HandleType* no se puede establecer en SQL_HANDLE_ENV si la ejecución asincrónica de funciones de conexión está habilitada para una conexión en el entorno.|  
|HY117|La conexión se suspende debido al estado de transacción desconocido. Solo se permiten funciones de desconexión y de solo lectura.|(DM) Para obtener más información sobre el estado suspendido, consulte la sección Comentarios de este tema.|  
|HYC00|Característica opcional no implementada|El controlador o el origen de datos no admite la operación **ROLLBACK.**|  
|HYT01|Tiempo de espera de conexión expirado|El período de tiempo de espera de conexión expiró antes de que el origen de datos respondiera a la solicitud. El período de tiempo de espera de conexión se establece a través de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|El controlador no admite esta función|(DM) El controlador asociado a *ConnectionHandle* no admite la función.|  
|IM017|El sondeo está deshabilitado en el modo de notificación asincrónica|Siempre que se utiliza el modelo de notificación, el sondeo está deshabilitado.|  
|IM018|**SQLCompleteAsync** no se ha llamado para completar la operación asincrónica anterior en este identificador.|Si la llamada de función anterior en el identificador devuelve SQL_STILL_EXECUTING y si el modo de notificación está habilitado, **sqlCompleteAsync** debe llamarse en el identificador para realizar el procesamiento posterior y completar la operación.|  
  
## <a name="comments"></a>Comentarios  
 Para un ODBC 3. *x* controlador, si *HandleType* es SQL_HANDLE_ENV y *Handle* es un identificador de entorno válido, el Administrador de controladores llamará a **SQLEndTran** en cada controlador asociado con el entorno. El *Handle* argumento para la llamada a un controlador será el identificador de entorno del controlador. Para un ODBC 2. *x* controlador, si *HandleType* es SQL_HANDLE_ENV y *Handle* es un identificador de entorno válido y hay varias conexiones en un estado conectado en ese entorno, el Administrador de controladores llamará a **SQLTransact** en el controlador una vez para cada conexión en un estado conectado en ese entorno. El *Handle* argumento en cada llamada será el identificador de la conexión. En cualquier caso, el controlador intentará confirmar o revertir transacciones, dependiendo del valor de *CompletionType*, en todas las conexiones que se encuentran en un estado conectado en ese entorno. Las conexiones que no están activas no afectan a la transacción.  
  
> [!NOTE]  
>  **SQLEndTran** no se puede usar para confirmar o revertir transacciones en un entorno compartido. SQLSTATE HY092 (identificador de atributo/opción no válido) se devolverá si **SQLEndTran** se llama con *Handle* establecido en el identificador de un entorno compartido o el identificador de una conexión en un entorno compartido.  
  
 El Administrador de controladores devolverá SQL_SUCCESS solo si recibe SQL_SUCCESS para cada conexión. Si el Administrador de controladores recibe SQL_ERROR en una o varias conexiones, devuelve SQL_ERROR a la aplicación y la información de diagnóstico se coloca en la estructura de datos de diagnóstico del entorno. Para determinar qué conexión o conexiones fallaron durante la operación de confirmación o reversión, la aplicación puede llamar a **SQLGetDiagRec** para cada conexión.  
  
> [!NOTE]  
>  El Administrador de controladores no simula una transacción global en todas las conexiones y, por lo tanto, no utiliza protocolos de confirmación de dos fases.  
  
 Si *CompletionType* se SQL_COMMIT, **SQLEndTran** emite una solicitud de confirmación para todas las operaciones activas en cualquier instrucción asociada a una conexión afectada. Si *CompletionType* se SQL_ROLLBACK, **SQLEndTran** emite una solicitud de reversión para todas las operaciones activas en cualquier instrucción asociada a una conexión afectada. Si no hay transacciones activas, **SQLEndTran** devuelve SQL_SUCCESS sin ningún efecto en ningún origen de datos. Para obtener más información, consulte [Confirmación y reversión](../../../odbc/reference/develop-app/committing-and-rolling-back-transactions.md)de transacciones .  
  
 Si el controlador está en modo de confirmación manual (mediante una llamada a **SQLSetConnectAttr** con el atributo SQL_ATTR_AUTOCOMMIT establecido en SQL_AUTOCOMMIT_OFF), se inicia implícitamente una nueva transacción cuando se ejecuta una instrucción SQL que se puede incluir dentro de una transacción en el origen de datos actual. Para obtener más información, consulte [Modo de confirmación](../../../odbc/reference/develop-app/commit-mode.md).  
  
 Para determinar cómo afectan las operaciones de transacción a los cursores, una aplicación llama a **SQLGetInfo** con las opciones SQL_CURSOR_ROLLBACK_BEHAVIOR y SQL_CURSOR_COMMIT_BEHAVIOR. Para obtener más información, consulte los párrafos siguientes y también vea [Efecto de las transacciones en cursores e instrucciones preparadas](../../../odbc/reference/develop-app/effect-of-transactions-on-cursors-and-prepared-statements.md).  
  
 Si el valor SQL_CURSOR_ROLLBACK_BEHAVIOR o SQL_CURSOR_COMMIT_BEHAVIOR es igual a SQL_CB_DELETE, **SQLEndTran** cierra y elimina todos los cursores abiertos en todas las instrucciones asociadas a la conexión y descarta todos los resultados pendientes. **SQLEndTran** deja cualquier instrucción presente en un estado asignado (no preparado); la aplicación puede reutilizarlos para solicitudes SQL posteriores o puede llamar a **SQLFreeStmt** o **SQLFreeHandle** con un *HandleType* de SQL_HANDLE_STMT para desasignarlas.  
  
 Si el valor SQL_CURSOR_ROLLBACK_BEHAVIOR o SQL_CURSOR_COMMIT_BEHAVIOR es igual a SQL_CB_CLOSE, **SQLEndTran** cierra todos los cursores abiertos en todas las instrucciones asociadas a la conexión. **SQLEndTran** deja cualquier instrucción presente en un estado preparado; la aplicación puede llamar a **SQLExecute** para una instrucción asociada a la conexión sin llamar primero a **SQLPrepare**.  
  
 Si el valor SQL_CURSOR_ROLLBACK_BEHAVIOR o SQL_CURSOR_COMMIT_BEHAVIOR es igual a SQL_CB_PRESERVE, **SQLEndTran** no afecta a los cursores abiertos asociados a la conexión. Los cursores permanecen en la fila a la que apuntaban antes de la llamada a **SQLEndTran**.  
  
 Para los controladores y orígenes de datos que admiten transacciones, llamar a **SQLEndTran** con SQL_COMMIT o SQL_ROLLBACK cuando no hay ninguna transacción activa devuelve SQL_SUCCESS (lo que indica que no hay trabajo que confirmar o revertir) y no tiene ningún efecto en el origen de datos.  
  
 Cuando un controlador está en modo de confirmación automática, el Administrador de controladores no llama a **SQLEndTran** en el controlador. **SQLEndTran** siempre devuelve SQL_SUCCESS independientemente de si se llama con un *CompletionType* de SQL_COMMIT o SQL_ROLLBACK.  
  
 Los controladores o orígenes de datos que no admiten transacciones ( la *opción* **SQLGetInfo** SQL_TXN_CAPABLE es SQL_TC_NONE) siempre están en modo de confirmación automática y, por lo tanto, siempre devuelven SQL_SUCCESS para **SQLEndTran** si se llaman con un *CompletionType* de SQL_COMMIT o SQL_ROLLBACK. Estos controladores y orígenes de datos no revierten realmente las transacciones cuando se le solicita que lo haga.  
  
## <a name="suspended-state"></a>Estado suspendido  
 En los administradores de controladores que se publicaron antes de Windows 7, una transacción estaba activa si **SQLEndTran devolvía** SQL_ERROR desde el controlador. Sin embargo, es posible que la transacción se haya confirmado correctamente en el servidor, pero no se ha notificado al controlador del cliente (por ejemplo, porque se ha producido un error de red). Esto dejaría la conexión en mal estado. A partir de Windows 7, cuando **SQLEndTran** devuelve SQL_ERROR, la conexión puede estar en un estado suspendido. En un estado suspendido, es posible llamar a funciones de solo lectura. Finalmente, la aplicación debe llamar a **SQLDisconnect** en una conexión suspendida para liberar recursos.  
  
 Si se cumplen todas las condiciones siguientes, la conexión se pondrá en un estado suspendido:  
  
-   El controlador devuelve SQL_ERROR de **SQLEndTran**.  
  
-   El controlador es ODBC versión 3.8 o posterior.  
  
-   La versión de la aplicación es 3.8 o posterior; o la aplicación ODBC 2.x o 3.x recompilada cancela correctamente la función **SQLEndTran** a través de **SQLCancelHandle**.  
  
-   El controlador no devolvió uno de los siguientes mensajes, que confirman que la transacción no se completó:  
  
    -   25S03: La transacción se revierte  
  
    -   40001: Error de serialización  
  
    -   40002: Restricción de integridad  
  
    -   HYC00: Característica opcional no implementada  
  
 Si **sqlEndTran** se llamó en un identificador de entorno y una de sus conexiones cumple las condiciones anteriores, todas las conexiones que se conectan al mismo controlador se pondrán en estado suspendido.  
  
 Después de que una aplicación llama a **SQLDisconnect** en una conexión suspendida, la conexión se puede usar para volver a conectarse a otro origen de datos o al mismo origen de datos.  
  
## <a name="related-functions"></a>Funciones relacionadas  
  
|Para información acerca de|Vea|  
|---------------------------|---------|  
|Cancelar una función que se ejecuta de forma asincrónica en un identificador de conexión.|[Función SQLCancelHandle](../../../odbc/reference/syntax/sqlcancelhandle-function.md)|  
|Devolver información sobre un controlador o una fuente de datos|[Función SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)|  
|Liberar un mango|[Función SQLFreeHandle](../../../odbc/reference/syntax/sqlfreehandle-function.md)|  
|Liberar un identificador de declaración|[Función SQLFreeStmt](../../../odbc/reference/syntax/sqlfreestmt-function.md)|  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de la API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Archivos de encabezado ODBC](../../../odbc/reference/install/odbc-header-files.md)   
 [Ejecución asincrónica (método de sondeo)](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md)
