---
title: Función SQLCancel ? Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLCancel
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLCancel
helpviewer_keywords:
- SQLCancel function [ODBC]
ms.assetid: ac0b5972-627f-4440-8c5a-0e8da728726d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: fcc2afce495a1481692ba1f20162a2df5d9a9458
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301315"
---
# <a name="sqlcancel-function"></a>Función SQLCancel
**Conformidad**  
 Versión introducida: Cumplimiento de normas ODBC 1.0: ISO 92  
  
 **Resumen**  
 **SQLCancel** cancela el procesamiento en una instrucción.  
  
 Para cancelar el procesamiento en una conexión o instrucción, utilice [SQLCancelHandle (función).](../../../odbc/reference/syntax/sqlcancelhandle-function.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```cpp  
  
SQLRETURN SQLCancel(  
     SQLHSTMT     StatementHandle);  
```  
  
## <a name="arguments"></a>Argumentos  
 *StatementHandle*  
 [Entrada] Identificador de instrucción.  
  
## <a name="returns"></a>Devuelve  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnóstico  
 Cuando **SQLCancel** devuelve SQL_ERROR o SQL_SUCCESS_WITH_INFO, se puede obtener un valor SQLSTATE asociado llamando a **SQLGetDiagRec** con un *HandleType* de SQL_HANDLE_STMT y un *Control* de *StatementHandle*. En la tabla siguiente se enumeran los valores SQLSTATE devueltos normalmente por **SQLCancel** y se explica cada uno de ellos en el contexto de esta función; la notación "(DM)" precede a las descripciones de SQLSTATEs devueltas por el Administrador de controladores. El código de retorno asociado a cada valor SQLSTATE se SQL_ERROR, a menos que se indique lo contrario.  
  
|SQLSTATE|Error|Descripción|  
|--------------|-----------|-----------------|  
|01000|Advertencia general|Mensaje informativo específico del controlador. (La función devuelve SQL_SUCCESS_WITH_INFO.)|  
|HY000|Error general|Se ha producido un error para el que no se ha definido sqlSTATE específico y para el que no se ha definido sqlSTATE específico de la implementación. El mensaje de error devuelto por [SQLGetDiagRec](../../../odbc/reference/syntax/sqlgetdiagrec-function.md) en el argumento * \*MessageText* buffer describe el error y su causa.|  
|HY001|Error de asignación de memoria|El controlador no pudo asignar la memoria necesaria para admitir la ejecución o finalización de la función.|  
|HY010|Error de secuencia de funciones|(DM) se llamó a una función de ejecución asincrónica para el identificador de conexión asociado a *StatementHandle*. Esta función asincrónica todavía se estaba ejecutando cuando se llamó a la función **SQLCancel.**<br /><br /> (DM) Error en la operación de cancelación porque una operación asincrónica está en curso en un identificador de conexión asociado a *StatementHandle*.|  
|HY013|Error de administración de memoria|No se pudo procesar la llamada de función porque no se pudo tener acceso a los objetos de memoria subyacentes, posiblemente debido a condiciones de poca memoria.|  
|HY018|Solicitud de cancelación rechazada por el servidor|El servidor rechazó la solicitud de cancelación.|  
|HY117|La conexión se suspende debido al estado de transacción desconocido. Solo se permiten funciones de desconexión y de solo lectura.|(DM) Para obtener más información sobre el estado suspendido, vea [SqlEndTran (función).](../../../odbc/reference/syntax/sqlendtran-function.md)|  
|HYT01|Tiempo de espera de conexión expirado|El período de tiempo de espera de conexión expiró antes de que el origen de datos respondiera a la solicitud. El período de tiempo de espera de conexión se establece a través de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|El controlador no admite esta función|(DM) El controlador asociado con el *StatementHandle* no admite la función.|  
  
## <a name="comments"></a>Comentarios  
 **SQLCancel** puede cancelar los siguientes tipos de procesamiento en una instrucción:  
  
-   Función que se ejecuta de forma asincrónica en la instrucción.  
  
-   Función de una instrucción que necesita datos.  
  
-   Función que se ejecuta en la instrucción en otro subproceso.  
  
 En ODBC 2. *x*, si una aplicación llama a **SQLCancel** cuando no se realiza ningún procesamiento en la instrucción, **SQLCancel** tiene el mismo efecto que **SQLFreeStmt** con la opción SQL_CLOSE; este comportamiento se define solo para la integridad y las aplicaciones deben llamar a **SQLFreeStmt** o **SQLCloseCursor** para cerrar los cursores.  
  
 Cuando **SQLCancel** se llama para cancelar una función que se ejecuta de forma asincrónica en una instrucción o una función en una instrucción que necesita datos, se borran los registros de diagnóstico registrados por la función que se cancela y **SQLCancel** publica sus propios registros de diagnóstico; Cuando **SQLCancel** se llama para cancelar una función que se ejecuta en una instrucción en otro subproceso, sin embargo, no borra los registros de diagnóstico de la función que se cancela y no registra sus propios registros de diagnóstico.  
  
## <a name="canceling-asynchronous-processing"></a>Cancelación del procesamiento asincrónico  
 Después de que una aplicación llama a una función de forma asincrónica, llama a la función repetidamente para determinar si ha terminado de procesarse. Si la función todavía se está procesando, devuelve SQL_STILL_EXECUTING. Si la función ha terminado de procesarse, devuelve un código diferente.  
  
 Después de cualquier llamada a la función que devuelve SQL_STILL_EXECUTING, una aplicación puede llamar a **SQLCancel** para cancelar la función. Si la solicitud de cancelación se realiza correctamente, el controlador devuelve SQL_SUCCESS. Este mensaje no indica que la función se haya cancelado realmente; indica que se ha procesado la solicitud de cancelación. Cuándo o si la función se cancela realmente depende del controlador y del origen de datos. La aplicación debe seguir llamando a la función original hasta que el código de retorno no se SQL_STILL_EXECUTING. Si la función se canceló correctamente, el código de retorno se SQL_ERROR y SQLSTATE HY008 (Operación cancelada). Si la función completó su procesamiento normal, el código de retorno se SQL_SUCCESS o SQL_SUCCESS_WITH_INFO si la función se realizó correctamente o SQL_ERROR y un SQLSTATE distinto de HY008 (Operación cancelada) si la función ha fallado.  
  
> [!NOTE]  
>  En ODBC 3.5, una llamada a **SQLCancel** cuando no se realiza ningún procesamiento en la instrucción no se trata como **SQLFreeStmt** con la opción SQL_CLOSE, pero no tiene ningún efecto en absoluto. Para cerrar un cursor, una aplicación debe llamar a **SQLCloseCursor**, no **SQLCancel**.  
  
 Para obtener más información sobre el procesamiento asincrónico, vea [Ejecución asincrónica](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md).  
  
## <a name="canceling-functions-that-need-data"></a>Cancelación de funciones que necesitan datos  
 Después de **SQLExecute** o **SQLExecDirect** devuelve SQL_NEED_DATA y antes de que se hayan enviado datos para todos los parámetros de datos en ejecución, una aplicación puede llamar a **SQLCancel** para cancelar la ejecución de la instrucción. Una vez cancelada la instrucción, la aplicación puede llamar a **SQLExecute** o **SQLExecDirect** de nuevo. Para obtener más información, vea [SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md).  
  
 Después de **SQLBulkOperations** o **SQLSetPos** devuelve SQL_NEED_DATA y antes de que se hayan enviado datos para todas las columnas de datos en ejecución, una aplicación puede llamar a **SQLCancel** para cancelar la operación. Una vez cancelada la operación, la aplicación puede llamar a **SQLBulkOperations** o **SQLSetPos** de nuevo; la cancelación no afecta al estado del cursor ni a la posición actual del cursor. Para obtener más información, vea [SQLBulkOperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md) o [SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md).  
  
## <a name="canceling-functions-executing-on-another-thread"></a>Cancelación de funciones que se ejecutan en otro subproceso  
 En una aplicación multiproceso, la aplicación puede cancelar una función que se ejecuta en otro subproceso. Para cancelar la función, la aplicación llama a **SQLCancel** con el mismo identificador de instrucción que el utilizado por la función de destino, pero en un subproceso diferente. La forma en que se cancela la función depende del controlador y del sistema operativo. Al igual que al cancelar una función que se ejecuta de forma asincrónica, el código de retorno de **SQLCancel** indica solo si el controlador procesó la solicitud correctamente. Solo se pueden devolver SQL_SUCCESS o SQL_ERROR; no se devuelve ninguna información de diagnóstico. Si se cancela la función original, devuelve SQL_ERROR y SQLSTATE HY008 (Operación cancelada).  
  
 Si se ejecuta una instrucción SQL cuando **sqlCancel** se llama en otro subproceso para cancelar la ejecución de la instrucción, es posible que la ejecución se realice correctamente y devuelva SQL_SUCCESS mientras la cancelación también se realiza correctamente. En este caso, el Administrador de controladores supone que el cursor abierto por la ejecución de la instrucción se cierra mediante la cancelación, por lo que la aplicación no podrá utilizar el cursor.  
  
 Para obtener más información sobre el subproceso, vea [Multithreading](../../../odbc/reference/develop-app/multithreading.md).  
  
## <a name="related-functions"></a>Funciones relacionadas  
  
|Para información acerca de|Vea|  
|---------------------------|---------|  
|Enlazar un búfer a un parámetro|[Función SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md)|  
|Realización de operaciones masivas de inserción o actualización|[Función SQLBulkOperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md)|  
|Cancela una función que se ejecuta de forma asincrónica en un identificador de conexión, además de la funcionalidad de **SQLCancel**.|[Función SQLCancelHandle](../../../odbc/reference/syntax/sqlcancelhandle-function.md)|  
|Ejecución de una instrucción SQL|[Función SQLExecDirect](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|Ejecución de una instrucción SQL preparada|[Función SQLExecute](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|Liberar un identificador de declaración|[SQLFreeStmt](../../../odbc/reference/syntax/sqlfreestmt-function.md)|  
|Obtención de un campo de un registro de diagnóstico o un campo de la cabecera de diagnóstico|[Función SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)|  
|Obtención de múltiples campos de una estructura de datos de diagnóstico|[Función SQLGetDiagRec](../../../odbc/reference/syntax/sqlgetdiagrec-function.md)|  
|Devolver el siguiente parámetro para enviar datos|[Función SQLParamData](../../../odbc/reference/syntax/sqlparamdata-function.md)|  
|Envío de datos de parámetros en tiempo de ejecución|[Función SQLPutData](../../../odbc/reference/syntax/sqlputdata-function.md)|  
|Colocar el cursor en un conjunto de filas, actualizar los datos del conjunto de filas o actualizar o eliminar datos en el conjunto de resultados|[Función SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md)|  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de la API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Archivos de encabezado de ODBC](../../../odbc/reference/install/odbc-header-files.md)
