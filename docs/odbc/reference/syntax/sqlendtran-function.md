---
title: "Función SQLEndTran | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
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
caps.latest.revision: 29
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: fcae4699f6effbc0e6605701560dad11acff5281
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="sqlendtran-function"></a>Función SQLEndTran
**Conformidad**  
 Versión introdujo: ODBC 3.0 normativas: ISO 92  
  
 **Resumen**  
 **SQLEndTran** solicita una operación de confirmación o reversión para todas las operaciones activas en todas las instrucciones asociadas a una conexión. **SQLEndTran** también puede solicitar que se realiza una operación de confirmación o reversión para todas las conexiones asociadas a un entorno.  
  
> [!NOTE]  
>  Para obtener más información acerca de qué el Administrador de controladores asigna esta función cuando una aplicación ODBC 3. *x* aplicación está trabajando con una API ODBC 2. *x* controladores, consulte [asignación de funciones de reemplazo para compatibilidad con versiones anteriores de aplicaciones](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md).  
  
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
  
 *Sql_commit*  
 [Entrada] Uno de los dos valores siguientes:  
  
 SQL_COMMIT SQL_ROLLBACK  
  
## <a name="returns"></a>Devuelve  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR, SQL_INVALID_HANDLE o SQL_STILL_EXECUTING.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Cuando **SQLEndTran** devuelve SQL_ERROR o SQL_SUCCESS_WITH_INFO, un valor SQLSTATE asociado se puede obtener mediante una llamada a **SQLGetDiagRec** con el adecuado *HandleType*y *controlar*. En la tabla siguiente se enumera los valores SQLSTATE devueltos normalmente por **SQLEndTran** y se explica cada uno de ellos en el contexto de esta función; la notación "(DM)" precede a las descripciones de SQLSTATE devuelto por el Administrador de controladores. El código de retorno asociado a cada valor SQLSTATE es SQL_ERROR, a menos que se indique lo contrario.  
  
|SQLSTATE|Error|Description|  
|--------------|-----------|-----------------|  
|01000|Advertencia general|Mensaje informativo de específicas del controlador. (La función devuelve SQL_SUCCESS_WITH_INFO).|  
|08003|Conexión no abierta|(DM) la *HandleType* era SQL_HANDLE_DBC y el *controlar* no estaba en estado conectado.|  
|08007|Error de conexión durante la transacción|El *HandleType* era SQL_HANDLE_DBC y la conexión asociada la *controlar* error durante la ejecución de la función y no se puede determinar si solicitado  **Confirmar** o **reversión** se produjo antes del error.|  
|25S01|Estado de transacción desconocido|Una o varias de las conexiones en *controlar* no se pudo completar la transacción con el resultado especificado y el resultado es desconocido.|  
|25S02|Transacción aún está activa|El controlador no pudo garantiza que todo el trabajo de la transacción global se pudo completar de forma automática y la transacción aún está activa.|  
|25S03|Se revierte la transacción|El controlador no pudo garantiza que todo el trabajo de la transacción global se pudo completar de forma atómica, y todo el trabajo en la transacción activa en *controlar* se revirtió.|  
|40001|Error de serialización.|La transacción se revirtió debido a un interbloqueo de recurso con otra transacción.|  
|40002|Infracción de restricción de integridad|El *Sql_commit* era SQL_COMMIT y el compromiso de cambios produjo la infracción de restricción de integridad. Como resultado, se revierte la transacción.|  
|HY000|Error general|Se produjo un error para que no hubo ninguna SQLSTATE específico y para el que se ha definido ningún SQLSTATE específico de la implementación. El mensaje de error devuelto por **SQLGetDiagRec** en el  *\*szMessageText* búfer describe el error y su causa.|  
|HY001|Error de asignación de memoria|El controlador no pudo asignar la memoria necesaria para admitir la ejecución o la finalización de la función.|  
|HY008|Operación cancelada|Procesamiento asincrónico se habilitó para la *IdentificadorConexión*. Se llamó a la función, y antes de terminó de ejecutarse [SQLCancelHandle función](../../../odbc/reference/syntax/sqlcancelhandle-function.md) se llamó en la *IdentificadorConexión*. A continuación, se llama a la función nuevo en el *IdentificadorConexión*.<br /><br /> Se llamó a la función, y antes de terminó de ejecutarse **SQLCancelHandle** se llamó en la *IdentificadorConexión* desde un subproceso diferente en una aplicación multiproceso.|  
|HY010|Error de secuencia de función|(DM) se llamó a una función ejecuta de forma asincrónica para un identificador de instrucción asociado a la *IdentificadorConexión* y aún se estaba ejecutando cuando **SQLEndTran** se llamó.<br /><br /> (DM) se llamó a una función ejecuta de forma asincrónica (no esta uno) para la *IdentificadorConexión* y aún se estaba ejecutando cuando se llamó a esta función.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, o **SQLSetPos** se llamó con un identificador de instrucción asociados a la *IdentificadorConexión* y devuelve SQL_NEED_DATA. Esta función se invoca antes de que se enviaron los datos para todas las columnas o parámetros de datos en ejecución.<br /><br /> (DM) se llamó a una función ejecuta de forma asincrónica (no esta uno) para la *controlar* con *HandleType* establecido en SQL_HANDLE_DBC y aún se estaba ejecutando cuando se llamó a esta función.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, o **SQLMoreResults** se llama para uno de los identificadores de instrucción asociados a *controlar* y SQL_PARAM_DATA_AVAILABLE devuelto. Esta función se invoca antes de que se recuperan los datos para todos los parámetros transmitidos.|  
|HY012|Código de operación de transacción no válido|(DM) el valor especificado para el argumento *Sql_commit* era SQL_COMMIT ni SQL_ROLLBACK.|  
|HY013|Error de administración de memoria|No se pudo procesar la llamada de función porque los objetos subyacentes de la memoria no se pudieron tener acceso, posiblemente debido a condiciones de memoria insuficiente.|  
|HY092|Identificador de opción o atributo no válido|(DM) el valor especificado para el argumento *HandleType* era SQL_HANDLE_ENV ni SQL_HANDLE_DBC.|  
|HY115|SQLEndTran no está permitida para un entorno que contiene una conexión con la ejecución de una función asincrónica habilitada|(DM) *HandleType* no puede establecerse en SQL_HANDLE_ENV si la ejecución asincrónica de las funciones de conexión está habilitada para una conexión en el entorno.|  
|HY117|Se suspende la conexión debido al estado de transacción desconocido. Solo se desconecte y se permiten las funciones de solo lectura.|(DM) para obtener más información sobre el estado suspendido, consulte la sección Comentarios de este tema.|  
|HYC00|Característica opcional no implementada|El controlador u origen de datos no admite la **reversión** operación.|  
|HYT01|Tiempo de espera de conexión expirado|El período de tiempo de espera de conexión finalizó antes de que el origen de datos se respondió a la solicitud. El período de tiempo de espera de conexión se establece a través de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Controlador no admite esta función|(DM) el controlador asociado a la *IdentificadorConexión* no admite la función.|  
|IM017|Sondeo está deshabilitado en el modo de notificación asincrónica|Cada vez que se utiliza el modelo de notificación, se deshabilita el sondeo.|  
|IM018|**SQLCompleteAsync** no se ha llamado para completar la operación asincrónica anterior en este identificador.|Si la llamada de función anterior en el controlador devuelve SQL_STILL_EXECUTING y si está habilitado el modo de notificación, **SQLCompleteAsync** se debe llamar en el identificador para realizar el procesamiento posterior a la y completar la operación.|  
  
## <a name="comments"></a>Comentarios  
 Para un ODBC 3. *x* controlador, si *HandleType* es SQL_HANDLE_ENV y *controlar* es un identificador de entorno válido, el Administrador de controladores llamará **SQLEndTran**en cada controlador asociado con el entorno. El *controlar* argumento de la llamada a un controlador será el identificador de entorno del controlador. Para un ODBC 2. *x* controlador, si *HandleType* es SQL_HANDLE_ENV y *controlar* es un identificador válido de entorno y hay varias conexiones en un estado conectado en el entorno, a continuación, el Administrador de controladores llamará **SQLTransact** en el controlador de una vez para cada conexión en un estado conectado en ese entorno. El *controlar* argumento en cada llamada será el identificador de la conexión. En cualquier caso, el controlador intentará confirmar o revertir las transacciones, dependiendo del valor de *Sql_commit*, en todas las conexiones que se encuentran en un estado conectado en ese entorno. Las conexiones que no están activas no afectan a la transacción.  
  
> [!NOTE]  
>  **SQLEndTran** no se puede usar para confirmar o revertir las transacciones en un entorno compartido. SQLSTATE HY092 (identificador de atributo u opción no válido) se devolverá si **SQLEndTran** se llama con *controlar* establecido en cualquier el identificador de un entorno compartido o el identificador de una conexión en un compartido entorno.  
  
 El Administrador de controladores devuelve SQL_SUCCESS solo si recibe SQL_SUCCESS para cada conexión. Si el Administrador de controladores que recibe SQL_ERROR en una o más conexiones, devuelve SQL_ERROR a la aplicación y la información de diagnóstico se coloca en la estructura de datos de diagnóstico del entorno. Para determinar qué conexión o conexiones de error durante la operación de confirmación o reversión, la aplicación puede llamar a **SQLGetDiagRec** para cada conexión.  
  
> [!NOTE]  
>  El Administrador de controladores no simula una transacción global en todas las conexiones y, por tanto, no utiliza protocolos de confirmación en dos fases.  
  
 Si *Sql_commit* es SQL_COMMIT, **SQLEndTran** emite una solicitud de confirmación para todas las operaciones activas en cualquier instrucción asociada a una conexión afectada. Si *Sql_commit* es SQL_ROLLBACK, **SQLEndTran** emite una solicitud rollback para todas las operaciones activas en cualquier instrucción asociada a una conexión afectada. Si no hay transacciones activas, **SQLEndTran** devuelve SQL_SUCCESS con ningún efecto en los orígenes de datos. Para obtener más información, consulte [comprometer y revertir transacciones](../../../odbc/reference/develop-app/committing-and-rolling-back-transactions.md).  
  
 Si el controlador está en modo de confirmación manual (mediante una llamada a **SQLSetConnectAttr** con el SQL_ATTR_AUTOCOMMIT atributo establecido en SQL_AUTOCOMMIT_OFF), implícitamente se inicia una nueva transacción cuando una instrucción SQL que puede incluirse en un transacción se ejecuta en el origen de datos actual. Para obtener más información, consulte [confirmar modo](../../../odbc/reference/develop-app/commit-mode.md).  
  
 Para determinar cómo afectan las operaciones de transacción a los cursores, llama a una aplicación **SQLGetInfo** con las opciones SQL_CURSOR_ROLLBACK_BEHAVIOR y SQL_CURSOR_COMMIT_BEHAVIOR. Para obtener más información, consulte los siguientes párrafos así como [efecto de las transacciones en los cursores y las instrucciones preparadas](../../../odbc/reference/develop-app/effect-of-transactions-on-cursors-and-prepared-statements.md).  
  
 Si el valor SQL_CURSOR_ROLLBACK_BEHAVIOR o SQL_CURSOR_COMMIT_BEHAVIOR es igual a SQL_CB_DELETE, **SQLEndTran** cierra y elimina todos los cursores abiertos en todas las instrucciones asociadas con la conexión y descarta todos los resultados pendientes. **SQLEndTran** deja cualquier instrucción que se encuentra en un estado de asignación (sin haberse preparado); la aplicación puede volver a usarlos para las solicitudes posteriores de SQL o puede llamar a **SQLFreeStmt** o **SQLFreeHandle** con un *HandleType* de SQL_HANDLE_STMT para cancelar la asignación de ellos.  
  
 Si el valor SQL_CURSOR_ROLLBACK_BEHAVIOR o SQL_CURSOR_COMMIT_BEHAVIOR es igual a SQL_CB_CLOSE, **SQLEndTran** cierra todos los cursores abiertos en todas las instrucciones asociadas con la conexión. **SQLEndTran** deja cualquier instrucción que se encuentra en un estado preparado; la aplicación puede llamar a **SQLExecute** para una instrucción asociada a la conexión sin antes de llamar a **SQLPrepare** .  
  
 Si el valor SQL_CURSOR_ROLLBACK_BEHAVIOR o SQL_CURSOR_COMMIT_BEHAVIOR es igual a SQL_CB_PRESERVE, **SQLEndTran** no afecta a los cursores abiertos asociados con la conexión. Los cursores permanecen en la fila que apunta a antes de la llamada a **SQLEndTran**.  
  
 Para controladores y orígenes de datos que admiten transacciones, al llamar a **SQLEndTran** con SQL_COMMIT o SQL_ROLLBACK cuando no hay ninguna transacción está activa devuelve SQL_SUCCESS (lo que indica que no hay ningún trabajo que se haya confirmado o revertido) y no tiene ningún efecto en el origen de datos.  
  
 Cuando un controlador está en modo de confirmación automática, el Administrador de controladores no llama a **SQLEndTran** en el controlador. **SQLEndTran** siempre devuelve SQL_SUCCESS, independientemente de si se llama con un *Sql_commit* de SQL_COMMIT o SQL_ROLLBACK.  
  
 Controladores u orígenes de datos que no se admiten transacciones (**SQLGetInfo** *opción* SQL_TXN_CAPABLE es SQL_TC_NONE) eficazmente siempre están en modo de confirmación automática y, por tanto, siempre devuelve SQL_SUCCESS para **SQLEndTran** si no se llama con un *Sql_commit* de SQL_COMMIT o SQL_ROLLBACK. Estos controladores y orígenes de datos no realmente revierten las transacciones cuando lo solicita.  
  
## <a name="suspended-state"></a>Estado de suspensión  
 En administradores de controladores que se hayan publicado antes de Windows 7, una transacción estaba activa si **SQLEndTran** devuelve SQL_ERROR desde el controlador. Sin embargo, es posible que la transacción se hubiera confirmado correctamente en el servidor, pero no se había notificó el controlador en el cliente (por ejemplo, porque se produjo un error de red). Esto daría lugar a la conexión en mal estado. A partir de Windows 7, cuando **SQLEndTran** devuelve SQL_ERROR, la conexión puede estar en un estado suspendido. En un estado suspendido, es posible llamar a funciones de sólo lectura. Finalmente, la aplicación debe llamar a **SQLDisconnect** en una conexión suspendida para liberar recursos.  
  
 Si todas las condiciones siguientes son verdaderas, la conexión se colocará en un estado suspendido:  
  
-   El controlador devuelve SQL_ERROR de **SQLEndTran**.  
  
-   El controlador es ODBC versión 3.8 o una versión posterior.  
  
-   La versión de la aplicación es 3.8 o versiones posteriores; o la aplicación de 2.x o 3.x ODBC ha vuelto a compilar correctamente cancela la **SQLEndTran** funcione a través de **SQLCancelHandle**.  
  
-   El controlador no devolvió uno de los siguientes mensajes, que confirmación que no se completó la transacción:  
  
    -   25S03: se revierte la transacción  
  
    -   40001: error de serialización.  
  
    -   40002: restricción de integridad  
  
    -   HYC00: Característica opcional no implementada  
  
 Si **SQLEndTran** se llamó en un entorno de controlador y uno de sus conexiones cumplen las condiciones anteriores, todas las conexiones de conectar con el mismo controlador se colocarán en el estado suspendido.  
  
 Después de que una aplicación llama **SQLDisconnect** en una conexión suspendida, la conexión se puede usar para volver a conectarse a otro origen de datos o el mismo origen de datos.  
  
## <a name="related-functions"></a>Funciones relacionadas  
  
|Para obtener información acerca de|Vea|  
|---------------------------|---------|  
|Cancelar una función que se ejecuta de forma asincrónica en un identificador de conexión.|[SQLCancelHandle (función)](../../../odbc/reference/syntax/sqlcancelhandle-function.md)|  
|Devolver información acerca de un controlador o un origen de datos|[Función SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)|  
|Liberar un identificador|[SQLFreeHandle, función](../../../odbc/reference/syntax/sqlfreehandle-function.md)|  
|Liberar un identificador de instrucción|[SQLFreeStmt, función](../../../odbc/reference/syntax/sqlfreestmt-function.md)|  
  
## <a name="see-also"></a>Vea también  
 [Referencia de la API de ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Archivos de encabezado ODBC](../../../odbc/reference/install/odbc-header-files.md)   
 [Ejecución asincrónica (método de sondeo)](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md)

