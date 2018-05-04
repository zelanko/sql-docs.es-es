---
title: Función SQLDisconnect | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
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
caps.latest.revision: 31
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 658b6cdddf1cbf66d7216c7fcdaa1b011c134345
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="sqldisconnect-function"></a>SQLDisconnect, función
**Conformidad**  
 Versión introdujo: Cumplimiento de estándares 1.0 de ODBC: ISO 92  
  
 **Resumen**  
 **SQLDisconnect** cierra la conexión asociada a un identificador de conexión específico.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
SQLRETURN SQLDisconnect(  
     SQLHDBC     ConnectionHandle);  
```  
  
## <a name="arguments"></a>Argumentos  
 *IdentificadorConexión*  
 [Entrada] Identificador de conexión.  
  
## <a name="returns"></a>Devuelve  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR, SQL_INVALID_HANDLE o SQL_STILL_EXECUTING.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Cuando **SQLDisconnect** devuelve SQL_ERROR o SQL_SUCCESS_WITH_INFO, un valor SQLSTATE asociado se puede obtener mediante una llamada a **SQLGetDiagRec** con un *HandleType* de SQL_ HANDLE_DBC y un *controlar* de *IdentificadorConexión*. En la tabla siguiente se enumera los valores SQLSTATE devueltos normalmente por **SQLDisconnect** y se explica cada uno de ellos en el contexto de esta función; la notación "(DM)" precede a las descripciones de SQLSTATE devuelto por el Administrador de controladores. El código de retorno asociado a cada valor SQLSTATE es SQL_ERROR, a menos que se indique lo contrario.  
  
|SQLSTATE|Error|Description|  
|--------------|-----------|-----------------|  
|01000|Advertencia general|Mensaje informativo de específicas del controlador. (La función devuelve SQL_SUCCESS_WITH_INFO).|  
|01002|Error de desconexión|Se produjo un error durante la desconexión. Sin embargo, la desconexión se realizó correctamente. (La función devuelve SQL_SUCCESS_WITH_INFO).|  
|08003|Conexión no abierta|(DM) la conexión especificado en el argumento *IdentificadorConexión* no estaba abierto.|  
|25000|Estado de transacción no válido|Se produjo una transacción en proceso en la conexión especificada por el argumento *IdentificadorConexión*. La transacción permanece activa.|  
|HY000|Error general|Se produjo un error para que no hubo ninguna SQLSTATE específico y para el que se ha definido ningún SQLSTATE específico de la implementación. El mensaje de error devuelto por **SQLGetDiagRec** en el  *\*MessageText* búfer describe el error y su causa.|  
|HY001|Error de asignación de memoria|El controlador no pudo asignar la memoria necesaria para admitir la ejecución o la finalización de la función.|  
|HY008|Operación cancelada|Procesamiento asincrónico se habilitó para la *IdentificadorConexión*. Se llamó a la función, y antes de que se ejecuta acabó [SQLCancelHandle función](../../../odbc/reference/syntax/sqlcancelhandle-function.md) se llamó en la *IdentificadorConexión*. A continuación, se llama a la función nuevo en el *IdentificadorConexión*.<br /><br /> Se llamó a la función, y antes de terminó de ejecutarse **SQLCancelHandle** se llamó en la *IdentificadorConexión* desde un subproceso diferente en una aplicación multiproceso.|  
|HY010|Error de secuencia de función|(DM) se llamó a una función ejecuta de forma asincrónica para una *StatementHandle* asociados con el *IdentificadorConexión* y aún se estaba ejecutando cuando **SQLDisconnect** era se llama.<br /><br /> (DM) se llamó a una función ejecuta de forma asincrónica (no esta uno) para la *IdentificadorConexión* y aún se estaba ejecutando cuando se llamó a esta función.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, o **SQLSetPos** se piden un *StatementHandle*  asociados con el *IdentificadorConexión* y devuelve SQL_NEED_DATA. Esta función se invoca antes de que se enviaron los datos para todas las columnas o parámetros de datos en ejecución.|  
|HY013|Error de administración de memoria|No se pudo procesar la llamada de función porque los objetos subyacentes de la memoria no se pudieron tener acceso, posiblemente debido a condiciones de memoria insuficiente.|  
|HY117|Se suspende la conexión debido al estado de transacción desconocido. Solo se desconecte y se permiten las funciones de solo lectura.|(DM) para obtener más información sobre el estado suspendido, consulte [función SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYT01|Tiempo de espera de conexión expirado|El período de tiempo de espera de conexión finalizó antes de que el origen de datos se respondió a la solicitud y la conexión aún está activa. El período de tiempo de espera de conexión se establece a través de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Controlador no admite esta función|(DM) el controlador asociado a la *IdentificadorConexión* no admite la función.|  
|IM017|Sondeo está deshabilitado en el modo de notificación asincrónica|Cada vez que se utiliza el modelo de notificación, se deshabilita el sondeo.|  
|IM018|**SQLCompleteAsync** no se ha llamado para completar la operación asincrónica anterior en este identificador.|Si la llamada de función anterior en el controlador devuelve SQL_STILL_EXECUTING y si está habilitado el modo de notificación, **SQLCompleteAsync** se debe llamar en el identificador para realizar el procesamiento posterior a la y completar la operación.|  
  
## <a name="comments"></a>Comentarios  
 Si una aplicación llama **SQLDisconnect** después **SQLBrowseConnect** devuelve SQL_NEED_DATA y antes de devolver un código de retorno diferente, el controlador cancela la conexión en proceso de exploración y devuelve la conexión a un estado no conectada.  
  
 Si una aplicación llama **SQLDisconnect** mientras hay una transacción incompleta asociada con el identificador de conexión, el controlador devuelve SQLSTATE 25000 (estado de transacción no válido), que indica que la transacción es sin cambios y la conexión está abierta. Una transacción incompleta es aquel que no se ha confirmado o revertido con **SQLEndTran**.  
  
 Si una aplicación llama **SQLDisconnect** antes de libera todas las instrucciones asociadas a la conexión, el controlador, una vez correctamente se desconecta del origen de datos, libera los esas instrucciones y todos los descriptores que se han se asigna explícitamente en la conexión. Sin embargo, si una o varias de las instrucciones asociadas con la conexión son todavía está ejecutando de forma asincrónica, **SQLDisconnect** devuelve SQL_ERROR con un valor SQLSTATE HY010 (error de secuencia de función). Además, **SQLDisconnect** liberará instrucciones todos los asociados y los descriptores de todos los que se han asignado explícitamente en la conexión si la conexión está en un estado suspendido o si **SQLDisconnect** era se canceló correctamente por **SQLCancelHandle**.  
  
 Para obtener información acerca de cómo se usa una aplicación **SQLDisconnect**, consulte [desconectarse de un origen de datos o el controlador](../../../odbc/reference/develop-app/disconnecting-from-a-data-source-or-driver.md).  
  
## <a name="disconnecting-from-a-pooled-connection"></a>Desconectarse de una conexión agrupada  
 Si la agrupación de conexiones está habilitada para un entorno compartido y llama a una aplicación **SQLDisconnect** en una conexión en el entorno, la conexión se devuelve al grupo de conexiones y sigue estando disponible para otros componentes por medio el mismo entorno compartido.  
  
## <a name="code-example"></a>Ejemplo de código  
 Vea [ejemplo programa ODBC](../../../odbc/reference/sample-odbc-program.md), [función SQLBrowseConnect](../../../odbc/reference/syntax/sqlbrowseconnect-function.md), y [SQLConnect, función](../../../odbc/reference/syntax/sqlconnect-function.md).  
  
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
