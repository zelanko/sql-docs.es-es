---
title: Función SQLDisconnect | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLDisconnect
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLDisconnect
helpviewer_keywords:
- SQLDisconnect function [ODBC]
ms.assetid: 9e84a58e-db48-4821-a0cd-5c711fcbe36b
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 444e41699c1a61acb82acc419a2f23db6142f7bb
ms.sourcegitcommit: 7a3243c45830cb3f49a7fa71c2991a9454fd6f5a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/11/2019
ms.locfileid: "65537553"
---
# <a name="sqldisconnect-function"></a>Función SQLDisconnect
**Conformidad**  
 Versión de introducción: Cumplimiento de estándares 1.0 de ODBC: ISO 92  
  
 **Resumen**  
 **SQLDisconnect** cierra la conexión asociada con un identificador de conexión específico.  
  
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
  
## <a name="diagnostics"></a>Diagnósticos  
 Cuando **SQLDisconnect** devuelve SQL_ERROR o SQL_SUCCESS_WITH_INFO, un valor SQLSTATE asociado se puede obtener mediante una llamada a **SQLGetDiagRec** con un *HandleType* de SQL_ HANDLE_DBC y un *controlar* de *ConnectionHandle*. En la tabla siguiente se enumera los valores SQLSTATE devueltos normalmente por **SQLDisconnect** y se explica cada uno de ellos en el contexto de esta función; la notación "(DM)" precede a las descripciones de SQLSTATE devuelto por el Administrador de controladores. El código de retorno asociado a cada valor SQLSTATE es SQL_ERROR, a menos que se indique lo contrario.  
  
|SQLSTATE|Error|Descripción|  
|--------------|-----------|-----------------|  
|01000|Advertencia general|Específico del controlador de mensaje informativo. (La función devuelve SQL_SUCCESS_WITH_INFO).|  
|01002|Error de desconexión|Se produjo un error durante la desconexión. Sin embargo, la desconexión se realizó correctamente. (La función devuelve SQL_SUCCESS_WITH_INFO).|  
|08003|Conexión no abierta|(DM) la conexión especificada en el argumento *ConnectionHandle* no estaba abierto.|  
|25000|Estado de transacción no válido|Se ha producido una transacción en proceso en la conexión especificada por el argumento *ConnectionHandle*. La transacción permanece activa.|  
|HY000|Error general|Se produjo un error para que se ha producido ningún SQLSTATE específico y para los que se ha definido ningún SQLSTATE específicos de la implementación. El mensaje de error devuelto por **SQLGetDiagRec** en el  *\*MessageText* búfer describe el error y su causa.|  
|HY001|Error de asignación de memoria|El controlador no pudo asignar la memoria necesaria para admitir la ejecución o la finalización de la función.|  
|HY008|Operación cancelada|Procesamiento asincrónico se habilitó para la *ConnectionHandle*. Se llamó a la función, y antes de que ha terminado de ejecutar [función SQLCancelHandle](../../../odbc/reference/syntax/sqlcancelhandle-function.md) se ha llamado en el *ConnectionHandle*. A continuación, la función se llamó de nuevo en el *ConnectionHandle*.<br /><br /> Se llamó a la función, y antes de terminó de ejecutarse **SQLCancelHandle** se ha llamado en el *ConnectionHandle* desde un subproceso diferente en una aplicación multiproceso.|  
|HY010|Error de secuencia de función|(DM) se llamó a una función que se ejecuta de forma asincrónica para una *StatementHandle* asociado con el *ConnectionHandle* y aún se estaba ejecutando cuando **SQLDisconnect** era se llama.<br /><br /> (DM) se llamó a una función que se ejecuta asincrónicamente (no ésta) para el *ConnectionHandle* y aún se estaba ejecutando cuando se llamó a esta función.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, o **SQLSetPos** se llamó para un *StatementHandle*  asociado con el *ConnectionHandle* y devuelve SQL_NEED_DATA. Esta función se invoca antes de que se enviaron datos para todas las columnas o parámetros de datos en ejecución.|  
|HY013|Error de administración de memoria|No se pudo procesar la llamada de función porque los objetos de memoria subyacente no se podrían tener acceso, posiblemente debido a memoria insuficiente.|  
|HY117|Conexión está suspendida debido al estado de transacción desconocido. Solo se desconecte y se permiten funciones de solo lectura.|(DM) para obtener más información sobre el estado suspendido, consulte [función SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYT01|Tiempo de espera de conexión agotado|Ha expirado el período de tiempo de espera de conexión antes de que el origen de datos que respondió a la solicitud y la conexión todavía está activa. El período de tiempo de espera de conexión se establece a través de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Controlador no admite esta función|(DM) el controlador asociado con el *ConnectionHandle* no admite la función.|  
|IM017|Sondeo se deshabilita en modo de notificación asincrónica|Cada vez que se usa el modelo de notificación, se deshabilita el sondeo.|  
|IM018|**SQLCompleteAsync** no se ha llamado para completar la operación asincrónica anterior en este identificador.|Si la llamada de función anterior en el controlador devuelve SQL_STILL_EXECUTING y si está habilitado el modo de notificación, **SQLCompleteAsync** debe llamarse en el identificador para realizar el procesamiento posterior y completar la operación.|  
  
## <a name="comments"></a>Comentarios  
 Si una aplicación llama a **SQLDisconnect** después **SQLBrowseConnect** devuelve SQL_NEED_DATA y antes de devolver un código de retorno diferente, el controlador cancela el proceso de exploración de conexión y devuelve la conexión a un estado desconectado.  
  
 Si una aplicación llama a **SQLDisconnect** mientras hay una transacción incompleta asociada con el identificador de conexión, el controlador devuelve SQLSTATE 25000 (estado de transacción no válido), que indica que la transacción se ha modificado y la conexión está abierta. Una transacción incompleta es aquel que no se ha confirmado o revertido con **SQLEndTran**.  
  
 Si una aplicación llama a **SQLDisconnect** antes de que ha liberado todas las instrucciones asociadas con la conexión, el controlador, libera de después correctamente se desconecta del origen de datos, esas instrucciones y todos los descriptores que se han se asigna explícitamente en la conexión. Sin embargo, si una o varias de las instrucciones asociadas con la conexión se mantienen en ejecución de forma asincrónica, **SQLDisconnect** devuelve SQL_ERROR con un valor SQLSTATE HY010 (función de error de secuencia). Además, **SQLDisconnect** podrá dedicarse a todas las instrucciones y todos los descriptores que se han asignado explícitamente en la conexión, si la conexión está en estado suspendido o si **SQLDisconnect** era se canceló correctamente **SQLCancelHandle**.  
  
 Para obtener información sobre el uso de una aplicación **SQLDisconnect**, consulte [desconectarse de un origen de datos o un controlador](../../../odbc/reference/develop-app/disconnecting-from-a-data-source-or-driver.md).  
  
## <a name="disconnecting-from-a-pooled-connection"></a>Desconectarse de una conexión agrupada  
 Si está habilitada la agrupación de conexiones para un entorno compartido y una aplicación llama a **SQLDisconnect** en una conexión en ese entorno, la conexión se devuelve al grupo de conexiones y sigue estando disponible para otros componentes mediante el mismo entorno compartido.  
  
## <a name="code-example"></a>Ejemplo de código  
 Consulte [programa ODBC de ejemplo](../../../odbc/reference/sample-odbc-program.md), [función SQLBrowseConnect](../../../odbc/reference/syntax/sqlbrowseconnect-function.md), y [función SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md).  
  
## <a name="related-functions"></a>Funciones relacionadas  
  
|Para obtener información acerca de|Vea|  
|---------------------------|---------|  
|Asignar un identificador|[Función SQLAllocHandle](../../../odbc/reference/syntax/sqlallochandle-function.md)|  
|Conectar a un origen de datos|[Función SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)|  
|Conectarse a un origen de datos mediante un cuadro de diálogo o la cadena de conexión|[Función SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)|  
|Ejecutar una operación de confirmación o reversión|[Función SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md)|  
|Liberar un identificador de conexión|[Función SQLFreeConnect](../../../odbc/reference/syntax/sqlfreeconnect-function.md)|  
  
## <a name="see-also"></a>Vea también  
 [Referencia de la API de ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Archivos de encabezado de ODBC](../../../odbc/reference/install/odbc-header-files.md)
