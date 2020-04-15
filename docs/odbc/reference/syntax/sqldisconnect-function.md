---
title: Función SQLDisconnect (FUNción sqlDisconnect) Microsoft Docs
ms.custom: ''
ms.date: 07/18/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLDisconnect
apilocation:
- sqlsrv32.dll
- odbc32.dll
apitype: dllExport
f1_keywords:
- SQLDisconnect
helpviewer_keywords:
- SQLDisconnect function [ODBC]
ms.assetid: 9e84a58e-db48-4821-a0cd-5c711fcbe36b
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a5ea73919fbe90719d881fb43108ab1934933708
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301155"
---
# <a name="sqldisconnect-function"></a>Función SQLDisconnect
**Conformidad**  
 Versión introducida: Cumplimiento de normas ODBC 1.0: ISO 92  
  
 **Resumen**  
 **SQLDisconnect** cierra la conexión asociada a un identificador de conexión específico.  
  
## <a name="syntax"></a>Sintaxis  
  
```cpp  
  
SQLRETURN SQLDisconnect(  
     SQLHDBC     ConnectionHandle);  
```  
  
## <a name="arguments"></a>Argumentos  
 *ConnectionHandle*  
 [Entrada] Identificador de conexión.  
  
## <a name="returns"></a>Devuelve  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR, SQL_INVALID_HANDLE o SQL_STILL_EXECUTING.  
  
## <a name="diagnostics"></a>Diagnóstico  
 Cuando **SQLDisconnect** devuelve SQL_ERROR o SQL_SUCCESS_WITH_INFO, se puede obtener un valor SQLSTATE asociado llamando a **SQLGetDiagRec** con un *HandleType* de SQL_HANDLE_DBC y un *control* de *ConnectionHandle*. En la tabla siguiente se enumeran los valores SQLSTATE devueltos normalmente por **SQLDisconnect** y se explica cada uno de ellos en el contexto de esta función; la notación "(DM)" precede a las descripciones de SQLSTATEs devueltas por el Administrador de controladores. El código de retorno asociado a cada valor SQLSTATE se SQL_ERROR, a menos que se indique lo contrario.  
  
|SQLSTATE|Error|Descripción|  
|--------------|-----------|-----------------|  
|01000|Advertencia general|Mensaje informativo específico del controlador. (La función devuelve SQL_SUCCESS_WITH_INFO.)|  
|01002|Error de desconexión|Se ha producido un error durante la desconexión. Sin embargo, la desconexión se realizó correctamente. (La función devuelve SQL_SUCCESS_WITH_INFO.)|  
|08003|Conexión no abierta|(DM) La conexión especificada en el argumento *ConnectionHandle* no estaba abierta.|  
|25000|Estado de transacción no válido|Se ha producido una transacción en proceso en la conexión especificada por el argumento *ConnectionHandle*. La transacción permanece activa.|  
|HY000|Error general|Se ha producido un error para el que no se ha definido sqlSTATE específico y para el que no se ha definido sqlSTATE específico de la implementación. El mensaje de error devuelto por **SQLGetDiagRec** en el * \*messageText* búfer describe el error y su causa.|  
|HY001|Error de asignación de memoria|El controlador no pudo asignar la memoria necesaria para admitir la ejecución o finalización de la función.|  
|HY008|Operación cancelada|El procesamiento asincrónico se ha habilitado para *ConnectionHandle*. Se llamó a la función y antes de que se finiera a ejecutar [SQLCancelHandle Function](../../../odbc/reference/syntax/sqlcancelhandle-function.md) se llamó en *ConnectionHandle*. A continuación, se volvió a llamar a la función en *ConnectionHandle*.<br /><br /> Se llamó a la función y antes de que terminara de ejecutar **SQLCancelHandle** se llamó en el *ConnectionHandle* desde un subproceso diferente en una aplicación multiproceso.|  
|HY010|Error de secuencia de funciones|(DM) se llamó a una función de ejecución asincrónica para un *StatementHandle* asociado con el *ConnectionHandle* y todavía se estaba ejecutando cuando **SQLDisconnect** se llamó.<br /><br /> (DM) se llamó a una función de ejecución asincrónica (no esta) para *ConnectionHandle* y todavía se estaba ejecutando cuando se llamó a esta función.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, o **SQLSetPos** se llamó para un *StatementHandle* asociado con el *ConnectionHandle* y devuelto SQL_NEED_DATA. Se llamó a esta función antes de que se enviaran datos para todos los parámetros o columnas de datos en ejecución.|  
|HY013|Error de administración de memoria|No se pudo procesar la llamada de función porque no se pudo tener acceso a los objetos de memoria subyacentes, posiblemente debido a condiciones de poca memoria.|  
|HY117|La conexión se suspende debido al estado de transacción desconocido. Solo se permiten funciones de desconexión y de solo lectura.|(DM) Para obtener más información sobre el estado suspendido, vea [SqlEndTran (función).](../../../odbc/reference/syntax/sqlendtran-function.md)|  
|HYT01|Tiempo de espera de conexión expirado|El período de tiempo de espera de conexión expiró antes de que el origen de datos respondiera a la solicitud y la conexión sigue activa. El período de tiempo de espera de conexión se establece a través de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|El controlador no admite esta función|(DM) El controlador asociado a *ConnectionHandle* no admite la función.|  
|IM017|El sondeo está deshabilitado en el modo de notificación asincrónica|Siempre que se utiliza el modelo de notificación, el sondeo está deshabilitado.|  
|IM018|**SQLCompleteAsync** no se ha llamado para completar la operación asincrónica anterior en este identificador.|Si la llamada de función anterior en el identificador devuelve SQL_STILL_EXECUTING y si el modo de notificación está habilitado, **sqlCompleteAsync** debe llamarse en el identificador para realizar el procesamiento posterior y completar la operación.|  
  
## <a name="comments"></a>Comentarios  
 Si una aplicación llama a **SQLDisconnect** después de **SQLBrowseConnect** devuelve SQL_NEED_DATA y antes de devolver un código de retorno diferente, el controlador cancela el proceso de exploración de la conexión y devuelve la conexión a un estado no conectado.  
  
 Si una aplicación llama a **SQLDisconnect** mientras hay una transacción incompleta asociada con el identificador de conexión, el controlador devuelve SQLSTATE 25000 (estado de transacción no válido), lo que indica que la transacción no cambia y la conexión está abierta. Una transacción incompleta es una transacción que no se ha confirmado ni revertido con **SQLEndTran**.  
  
 Si una aplicación llama a **SQLDisconnect** antes de liberar todas las instrucciones asociadas a la conexión, el controlador, después de desconectarse correctamente del origen de datos, libera esas instrucciones y todos los descriptores que se han asignado explícitamente en la conexión. Sin embargo, si una o varias de las instrucciones asociadas a la conexión siguen ejecutándose de forma asincrónica, **SQLDisconnect** devuelve SQL_ERROR con un valor SQLSTATE de HY010 (error de secuencia de funciones). Además, **SQLDisconnect** liberará todas las instrucciones asociadas y todos los descriptores que se han asignado explícitamente en la conexión, si la conexión está en un estado suspendido o si **SQLDisconnect** se canceló correctamente por **SQLCancelHandle**.  
  
 Para obtener información sobre cómo una aplicación usa **SQLDisconnect**, vea [Desconectarse de un origen](../../../odbc/reference/develop-app/disconnecting-from-a-data-source-or-driver.md)de datos o controlador .  
  
## <a name="disconnecting-from-a-pooled-connection"></a>Desconectarse de una conexión agrupada  
 Si la agrupación de conexiones está habilitada para un entorno compartido y una aplicación llama a **SQLDisconnect** en una conexión en ese entorno, la conexión se devuelve al grupo de conexiones y sigue estando disponible para otros componentes que utilizan el mismo entorno compartido.  
  
## <a name="code-example"></a>Ejemplo de código  
 Vea [Programa ODBC](../../../odbc/reference/sample-odbc-program.md)de ejemplo , [Función SQLBrowseConnect](../../../odbc/reference/syntax/sqlbrowseconnect-function.md)y [Función SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md).  
  
## <a name="related-functions"></a>Funciones relacionadas  
  
|Para información acerca de|Vea|  
|---------------------------|---------|  
|Asignación de un asa|[Función SQLAllocHandle](../../../odbc/reference/syntax/sqlallochandle-function.md)|  
|Conectar a un origen de datos|[Función SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)|  
|Conexión a un origen de datos mediante una cadena de conexión o un cuadro de diálogo|[Función SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)|  
|Ejecución de una operación de confirmación o reversión|[Función SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md)|  
|Liberar un asa de conexión|[Función SQLFreeConnect](../../../odbc/reference/syntax/sqlfreeconnect-function.md)|  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de la API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Archivos de encabezado de ODBC](../../../odbc/reference/install/odbc-header-files.md)
