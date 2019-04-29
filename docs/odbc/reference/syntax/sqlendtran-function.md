---
title: Función SQLEndTran | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLEndTran
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLEndTran
helpviewer_keywords:
- SQLEndTran function [ODBC]
ms.assetid: ff375ce1-eb50-4693-b1e6-70181a6dbf9f
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: fa1b2afec38116bef3ae90d75607d21c9a92cd80
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63062263"
---
# <a name="sqlendtran-function"></a>Función SQLEndTran
**Conformidad**  
 Versión de introducción: Compatibilidad de ODBC 3.0 estándares: ISO 92  
  
 **Resumen**  
 **SQLEndTran** solicita una operación de confirmación o reversión para todas las operaciones activas en todas las instrucciones asociadas con una conexión. **SQLEndTran** también puede solicitar que se realiza una operación de confirmación o reversión para todas las conexiones asociadas con un entorno.  
  
> [!NOTE]  
>  Para obtener más información sobre lo que el Administrador de controladores asigna esta función cuando una aplicación ODBC 3. *x* aplicación funciona con un ODBC 2. *x* controladores, consulte [asignación de funciones de reemplazo para compatibilidad con versiones anteriores de aplicaciones](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
SQLRETURN SQLEndTran(  
     SQLSMALLINT   HandleType,  
     SQLHANDLE     Handle,  
     SQLSMALLINT   CompletionType);  
```  
  
## <a name="arguments"></a>Argumentos  
 *HandleType*  
 [Entrada] Identificador de tipo de identificador. Contiene cualquier SQL_HANDLE_ENV (si *controlar* es un identificador de entorno) o SQL_HANDLE_DBC (si *controlar* es un identificador de conexión).  
  
 *Handle*  
 [Entrada] El identificador del tipo indicado por *HandleType*, que indica el ámbito de la transacción. Para obtener más información, vea "Comentarios".  
  
 *CompletionType*  
 [Entrada] Uno de los dos valores siguientes:  
  
 SQL_COMMIT SQL_ROLLBACK  
  
## <a name="returns"></a>Devuelve  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR, SQL_INVALID_HANDLE o SQL_STILL_EXECUTING.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Cuando **SQLEndTran** devuelve SQL_ERROR o SQL_SUCCESS_WITH_INFO, un valor SQLSTATE asociado se puede obtener mediante una llamada a **SQLGetDiagRec** con los valores adecuados *HandleType*y *controlar*. En la tabla siguiente se enumera los valores SQLSTATE devueltos normalmente por **SQLEndTran** y se explica cada uno de ellos en el contexto de esta función; la notación "(DM)" precede a las descripciones de SQLSTATE devuelto por el Administrador de controladores. El código de retorno asociado a cada valor SQLSTATE es SQL_ERROR, a menos que se indique lo contrario.  
  
|SQLSTATE|Error|Descripción|  
|--------------|-----------|-----------------|  
|01000|Advertencia general|Específico del controlador de mensaje informativo. (La función devuelve SQL_SUCCESS_WITH_INFO).|  
|08003|Conexión no abierta|(DM) el *HandleType* era SQL_HANDLE_DBC y el *controlar* no estaba en estado conectado.|  
|08007|Error de conexión durante la transacción|El *HandleType* era SQL_HANDLE_DBC y la conexión asociada con el *controlar* error durante la ejecución de la función y no se puede determinar si solicitado  **Confirmar** o **reversión** se ha producido antes del error.|  
|25S01|Estado de transacción desconocido|Una o varias de las conexiones en *controlar* no se pudo completar la transacción con el resultado especificado y se desconoce el resultado.|  
|25S02|Transacción todavía está activa|El controlador no pudo garantizar que todo el trabajo de la transacción global podría realizarse de forma atómica y la transacción todavía está activa.|  
|25S03|Se revierte la transacción|El controlador no pudo garantizar que todo el trabajo de la transacción global podría realizarse de forma atómica y todo el trabajo de la transacción activa en *controlar* se revirtió.|  
|40001|Error de serialización.|Debido a un interbloqueo de recurso con otra transacción se revirtió la transacción.|  
|40002|Infracción de restricción de integridad|El *Sql_commit* estaba SQL_COMMIT y el compromiso de cambios provocó la infracción de restricción de integridad. Como resultado, se revirtió la transacción.|  
|HY000|Error general|Se produjo un error para que se ha producido ningún SQLSTATE específico y para los que se ha definido ningún SQLSTATE específicos de la implementación. El mensaje de error devuelto por **SQLGetDiagRec** en el  *\*szMessageText* búfer describe el error y su causa.|  
|HY001|Error de asignación de memoria|El controlador no pudo asignar la memoria necesaria para admitir la ejecución o la finalización de la función.|  
|HY008|Operación cancelada|Procesamiento asincrónico se habilitó para la *ConnectionHandle*. Se llamó a la función, y antes de terminó de ejecutarse [función SQLCancelHandle](../../../odbc/reference/syntax/sqlcancelhandle-function.md) se ha llamado en el *ConnectionHandle*. A continuación, la función se llamó de nuevo en el *ConnectionHandle*.<br /><br /> Se llamó a la función, y antes de terminó de ejecutarse **SQLCancelHandle** se ha llamado en el *ConnectionHandle* desde un subproceso diferente en una aplicación multiproceso.|  
|HY010|Error de secuencia de función|(DM) se llamó a una función que se ejecuta de forma asincrónica para un identificador de instrucción asociado con el *ConnectionHandle* y aún se estaba ejecutando cuando **SQLEndTran** llamó.<br /><br /> (DM) se llamó a una función que se ejecuta asincrónicamente (no ésta) para el *ConnectionHandle* y aún se estaba ejecutando cuando se llamó a esta función.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, o **SQLSetPos** llamó para un identificador de instrucción asociado con el *ConnectionHandle* y devuelve SQL_NEED_DATA. Esta función se invoca antes de que se enviaron datos para todas las columnas o parámetros de datos en ejecución.<br /><br /> (DM) se llamó a una función que se ejecuta asincrónicamente (no ésta) para el *controlar* con *HandleType* establecido en SQL_HANDLE_DBC y aún se estaba ejecutando cuando se llamó a esta función.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, o **SQLMoreResults** se llamó para uno de los identificadores de instrucción asociados *controlar* y SQL_PARAM_DATA_AVAILABLE devuelta. Esta función se invoca antes de que se recuperan los datos para todos los parámetros transmitidos.|  
|HY012|Código de operación de transacción no válido|(DM) el valor especificado para el argumento *Sql_commit* era ni SQL_COMMIT ni SQL_ROLLBACK.|  
|HY013|Error de administración de memoria|No se pudo procesar la llamada de función porque los objetos de memoria subyacente no se podrían tener acceso, posiblemente debido a memoria insuficiente.|  
|HY092|Identificador de opción o atributo no válido|(DM) el valor especificado para el argumento *HandleType* era SQL_HANDLE_ENV ni SQL_HANDLE_DBC.|  
|HY115|SQLEndTran no se permite para un entorno que contenga una conexión con la ejecución de la función asincrónica habilitada|(DM) *HandleType* no puede establecerse en SQL_HANDLE_ENV si la ejecución asincrónica de las funciones de la conexión está habilitada para una conexión en el entorno.|  
|HY117|Conexión está suspendida debido al estado de transacción desconocido. Solo se desconecte y se permiten funciones de solo lectura.|(DM) para obtener más información sobre el estado suspendido, consulte la sección Comentarios de este tema.|  
|HYC00|Característica opcional no implementada|El controlador u origen de datos no admite la **reversión** operación.|  
|HYT01|Tiempo de espera de conexión agotado|Ha expirado el período de tiempo de espera de conexión antes de que el origen de datos que respondió a la solicitud. El período de tiempo de espera de conexión se establece a través de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Controlador no admite esta función|(DM) el controlador asociado con el *ConnectionHandle* no admite la función.|  
|IM017|Sondeo se deshabilita en modo de notificación asincrónica|Cada vez que se usa el modelo de notificación, se deshabilita el sondeo.|  
|IM018|**SQLCompleteAsync** no se ha llamado para completar la operación asincrónica anterior en este identificador.|Si la llamada de función anterior en el controlador devuelve SQL_STILL_EXECUTING y si está habilitado el modo de notificación, **SQLCompleteAsync** debe llamarse en el identificador para realizar el procesamiento posterior y completar la operación.|  
  
## <a name="comments"></a>Comentarios  
 Para un ODBC 3. *x* controlador, si *HandleType* es SQL_HANDLE_ENV y *controlar* es un identificador de entorno válido, a continuación, el Administrador de controladores llamará **SQLEndTran**en cada controlador asociado con el entorno. El *controlar* argumento de la llamada a un controlador será el identificador de entorno del controlador. Para un ODBC 2. *x* controlador, si *HandleType* es SQL_HANDLE_ENV y *controlar* es un identificador de entorno válido, y hay varias conexiones en un estado conectado en ese entorno, a continuación, el Administrador de controladores llamará **SQLTransact** en el controlador de una vez para cada conexión en estado conectado en ese entorno. El *controlar* argumento en cada llamada será el identificador de la conexión. En cualquier caso, el controlador intentará confirmar o revertir las transacciones, según el valor de *Sql_commit*, en todas las conexiones que se encuentran en estado conectado en ese entorno. Las conexiones que no están activas no afectan a la transacción.  
  
> [!NOTE]  
>  **SQLEndTran** no se puede usar para confirmar o revertir las transacciones en un entorno compartido. SQLSTATE HY092 (identificador de opción o atributo no válido), se devolverá si **SQLEndTran** se llama con *controlar* establecido en cualquier identificador de un entorno compartido o el identificador de una conexión en un compartido entorno.  
  
 El Administrador de controladores devuelve SQL_SUCCESS solo si no recibe SQL_SUCCESS para cada conexión. Si el Administrador de controladores recibe SQL_ERROR en una o más conexiones, devuelve SQL_ERROR a la aplicación y la información de diagnóstico se coloca en la estructura de datos de diagnóstico del entorno. Para determinar qué conexión o las conexiones no se pudo durante la operación de confirmación o reversión, la aplicación puede llamar a **SQLGetDiagRec** para cada conexión.  
  
> [!NOTE]  
>  El Administrador de controladores no simula una transacción global en todas las conexiones y, por tanto, no utiliza protocolos de confirmación en dos fases.  
  
 Si *Sql_commit* es SQL_COMMIT, **SQLEndTran** emite una solicitud de confirmación para todas las operaciones activas en cualquier instrucción asociada con una conexión afectada. Si *Sql_commit* es SQL_ROLLBACK, **SQLEndTran** emite una solicitud de reversión para todas las operaciones activas en cualquier instrucción asociada con una conexión afectada. Si no hay transacciones activas, **SQLEndTran** devuelve SQL_SUCCESS no tiene ningún efecto en los orígenes de datos. Para obtener más información, consulte [comprometer y revertir transacciones](../../../odbc/reference/develop-app/committing-and-rolling-back-transactions.md).  
  
 Si el controlador está en modo de confirmación manual (mediante una llamada a **SQLSetConnectAttr** con el SQL_ATTR_AUTOCOMMIT atributo establecido en SQL_AUTOCOMMIT_OFF), una nueva transacción se inicia implícitamente cuando una instrucción SQL que puede incluirse dentro de un transacción se ejecuta en el origen de datos actual. Para obtener más información, consulte [el modo de confirmación](../../../odbc/reference/develop-app/commit-mode.md).  
  
 Para determinar cómo afectan las operaciones de transacción a los cursores, una aplicación llama a **SQLGetInfo** con las opciones SQL_CURSOR_ROLLBACK_BEHAVIOR y SQL_CURSOR_COMMIT_BEHAVIOR. Para obtener más información, consulte los siguientes párrafos así como [efecto de las transacciones en los cursores y las instrucciones preparadas](../../../odbc/reference/develop-app/effect-of-transactions-on-cursors-and-prepared-statements.md).  
  
 Si el valor SQL_CURSOR_ROLLBACK_BEHAVIOR o SQL_CURSOR_COMMIT_BEHAVIOR es igual a SQL_CB_DELETE, **SQLEndTran** cierra y elimina todos los cursores abiertos en todas las instrucciones asociadas con la conexión y descarta todos los resultados pendientes. **SQLEndTran** deja cualquier instrucción presente en un estado de asignación (cancelado); la aplicación puede volver a usarlos para las solicitudes posteriores de SQL o puede llamar a **SQLFreeStmt** o **SQLFreeHandle** con un *HandleType* de SQL_HANDLE_STMT para desasignar ellos.  
  
 Si el valor SQL_CURSOR_ROLLBACK_BEHAVIOR o SQL_CURSOR_COMMIT_BEHAVIOR es igual a SQL_CB_CLOSE, **SQLEndTran** cierra todos los cursores abiertos en todas las instrucciones asociadas con la conexión. **SQLEndTran** deja cualquier instrucción presente en un estado preparado; la aplicación puede llamar a **SQLExecute** para una instrucción asociada con la conexión sin llamar primero a **SQLPrepare**.  
  
 Si el valor SQL_CURSOR_ROLLBACK_BEHAVIOR o SQL_CURSOR_COMMIT_BEHAVIOR es igual a SQL_CB_PRESERVE, **SQLEndTran** no afecta a los cursores abiertos asociados con la conexión. Los cursores permanecen en la fila que apunta a antes de llamar a **SQLEndTran**.  
  
 Para los controladores y orígenes de datos que admiten transacciones, una llamada a **SQLEndTran** con SQL_COMMIT o SQL_ROLLBACK cuando no hay ninguna transacción está activa devuelve SQL_SUCCESS (lo que indica que no hay ningún trabajo que se confirma o revierte) y no tiene ningún efecto en el origen de datos.  
  
 Cuando un controlador está en modo de confirmación automática, el Administrador de controladores no llama a **SQLEndTran** en el controlador. **SQLEndTran** siempre devuelve SQL_SUCCESS, independientemente de si se llama con un *Sql_commit* de SQL_COMMIT o SQL_ROLLBACK.  
  
 Los controladores u orígenes de datos que no admiten transacciones (**SQLGetInfo** *opción* SQL_TXN_CAPABLE es SQL_TC_NONE) eficazmente siempre están en modo de confirmación automática y, por tanto, siempre devuelve SQL_SUCCESS para **SQLEndTran** o no que se llaman con un *Sql_commit* de SQL_COMMIT o SQL_ROLLBACK. Controladores y orígenes de datos no realmente revertir las transacciones cuando lo solicita.  
  
## <a name="suspended-state"></a>Estado suspendido  
 En administradores de controlador que se publicaron antes de Windows 7, una transacción estaba activa si **SQLEndTran** devuelve SQL_ERROR desde el controlador. Sin embargo, era posible que la transacción se ha tenido confirmada correctamente en el servidor, pero no se había notificó el controlador en el cliente (por ejemplo, porque se produjo un error de red). Esto podría dejar la conexión en mal estado. A partir de Windows 7, cuando **SQLEndTran** devuelve SQL_ERROR, la conexión puede estar en un estado suspendido. En un estado suspendido, es posible llamar a funciones de solo lectura. Finalmente, la aplicación debe llamar a **SQLDisconnect** en una conexión suspendida para liberar los recursos.  
  
 Si todas las condiciones siguientes son verdaderas, la conexión se coloca en un estado suspendido:  
  
-   El controlador devuelve SQL_ERROR desde **SQLEndTran**.  
  
-   El controlador es la versión 3.8 o versiones posterior de ODBC.  
  
-   La versión de la aplicación es la 3.8 o versiones posteriores; o la aplicación recompilada de ODBC 2.x o 3.x correctamente cancela la **SQLEndTran** funcionar a través del **SQLCancelHandle**.  
  
-   El controlador no ha devuelto uno de los mensajes siguientes, que confirmación que no se completó la transacción:  
  
    -   25S03: Se revierte la transacción  
  
    -   40001: Error de serialización.  
  
    -   40002: restricción de integridad  
  
    -   HYC00: Característica opcional no implementada  
  
 Si **SQLEndTran** se llamó en un entorno de controlador y uno de sus conexiones cumplen las condiciones anteriores, todas las conexiones de conectar con el mismo controlador se coloca en el estado suspendido.  
  
 Después de una aplicación llama a **SQLDisconnect** en una conexión de suspensión, la conexión se puede usar para volver a conectarse a otro origen de datos o el mismo origen de datos.  
  
## <a name="related-functions"></a>Funciones relacionadas  
  
|Para obtener información acerca de|Vea|  
|---------------------------|---------|  
|Cancelación de una función que se ejecuta de forma asincrónica en un identificador de conexión.|[Función SQLCancelHandle](../../../odbc/reference/syntax/sqlcancelhandle-function.md)|  
|Devolver información acerca de un controlador o un origen de datos|[Función SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)|  
|Liberar un identificador|[Función SQLFreeHandle](../../../odbc/reference/syntax/sqlfreehandle-function.md)|  
|Liberar un identificador de instrucción|[Función SQLFreeStmt](../../../odbc/reference/syntax/sqlfreestmt-function.md)|  
  
## <a name="see-also"></a>Vea también  
 [Referencia de la API de ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Archivos de encabezado ODBC](../../../odbc/reference/install/odbc-header-files.md)   
 [Ejecución asincrónica (método de sondeo)](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md)
