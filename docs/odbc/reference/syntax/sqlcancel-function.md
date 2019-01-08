---
title: Función SQLCancel | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b9d0c756db7f84e6bcec46a61ef805f885f39d28
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/11/2018
ms.locfileid: "53214656"
---
# <a name="sqlcancel-function"></a>Función SQLCancel
**Conformidad**  
 Versión de introducción: Cumplimiento de estándares 1.0 de ODBC: 92 ISO  
  
 **Resumen**  
 **SQLCancel** cancela el procesamiento en una instrucción.  
  
 Para cancelar el procesamiento en una conexión o instrucción, utilice [función SQLCancelHandle](../../../odbc/reference/syntax/sqlcancelhandle-function.md).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
SQLRETURN SQLCancel(  
     SQLHSTMT     StatementHandle);  
```  
  
## <a name="arguments"></a>Argumentos  
 *StatementHandle*  
 [Entrada] Identificador de instrucción.  
  
## <a name="returns"></a>Devuelve  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Cuando **SQLCancel** devuelve SQL_ERROR o SQL_SUCCESS_WITH_INFO, un valor SQLSTATE asociado se puede obtener mediante una llamada a **SQLGetDiagRec** con un *HandleType* de SQL_ HANDLE_STMT y un *controlar* de *StatementHandle*. En la tabla siguiente se enumera los valores SQLSTATE devueltos normalmente por **SQLCancel** y se explica cada uno de ellos en el contexto de esta función; la notación "(DM)" precede a las descripciones de SQLSTATE devuelto por el Administrador de controladores. El código de retorno asociado a cada valor SQLSTATE es SQL_ERROR, a menos que se indique lo contrario.  
  
|SQLSTATE|Error|Descripción|  
|--------------|-----------|-----------------|  
|01000|Advertencia general|Específico del controlador de mensaje informativo. (La función devuelve SQL_SUCCESS_WITH_INFO).|  
|HY000|Error general|Se produjo un error para que se ha producido ningún SQLSTATE específico y para los que se ha definido ningún SQLSTATE específicos de la implementación. El mensaje de error devuelto por [SQLGetDiagRec](../../../odbc/reference/syntax/sqlgetdiagrec-function.md) en el argumento  *\*MessageText* búfer describe el error y su causa.|  
|HY001|Error de asignación de memoria|El controlador no pudo asignar la memoria necesaria para admitir la ejecución o la finalización de la función.|  
|HY010|Error de secuencia de función|(DM) se llamó a una función que se ejecuta de forma asincrónica para el identificador de conexión que está asociado el *StatementHandle*. Aún estaba ejecutando esta función asincrónica cuando el **SQLCancel** se llamó a la función.<br /><br /> (DM) cancelar la operación porque no es una operación asincrónica en curso en un identificador de conexión que está asociado con *StatementHandle*.|  
|HY013|Error de administración de memoria|No se pudo procesar la llamada de función porque los objetos de memoria subyacente no se podrían tener acceso, posiblemente debido a memoria insuficiente.|  
|HY018|El servidor rechazada la solicitud de cancelación|El servidor rechazó la solicitud de cancelación.|  
|HY117|Conexión está suspendida debido al estado de transacción desconocido. Solo se desconecte y se permiten funciones de solo lectura.|(DM) para obtener más información sobre el estado suspendido, consulte [función SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYT01|Tiempo de espera de conexión agotado|Ha expirado el período de tiempo de espera de conexión antes de que el origen de datos que respondió a la solicitud. El período de tiempo de espera de conexión se establece a través de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Controlador no admite esta función|(DM) el controlador asociado con el *StatementHandle* no admite la función.|  
  
## <a name="comments"></a>Comentarios  
 **SQLCancel** puede cancelar los siguientes tipos de procesamiento en una instrucción:  
  
-   Una función que se ejecutan asincrónicamente en la instrucción.  
  
-   Una función en una instrucción que necesita que los datos.  
  
-   Una función que se ejecuta en la instrucción en otro subproceso.  
  
 En ODBC 2. *x*, si una aplicación llama a **SQLCancel** cuando no se realiza ningún procesamiento en la instrucción, **SQLCancel** tiene el mismo efecto que **SQLFreeStmt** con la opción SQL_CLOSE; Este comportamiento se define únicamente por integridad y las aplicaciones deben llamar a **SQLFreeStmt** o **SQLCloseCursor** para cerrar los cursores.  
  
 Cuando **SQLCancel** se llama para cancelar una función que se ejecutan asincrónicamente en una instrucción o una función en una instrucción que se borran las necesidades de datos, los registros de diagnóstico enviados por la función que se va a cancelar, y **SQLCancel**  registra sus propios registros de diagnóstico; cuando **SQLCancel** se llama para cancelar una función que se ejecuta en una instrucción en otro subproceso, sin embargo, no borra el diagnóstico de los registros de la que canceló función y no no registrar sus propios registros de diagnóstico.  
  
## <a name="canceling-asynchronous-processing"></a>Cancelación del procesamiento asincrónico  
 Después de una aplicación llama a una función de forma asincrónica, llama a la función varias veces para determinar si ha finalizado el procesamiento. Si la función todavía está procesando, devuelve SQL_STILL_EXECUTING. Si la función ha finalizado el procesamiento, devuelve un código diferente.  
  
 Después de llamar a la función que devuelve SQL_STILL_EXECUTING, una aplicación puede llamar a **SQLCancel** para cancelar la función. Si la solicitud de cancelación se realiza correctamente, el controlador devuelve SQL_SUCCESS. Este mensaje no indica que la función se ha cancelado realmente; indica que se procesó la solicitud de cancelación. Cuándo o si la función se cancelará realmente es dependiente del controlador y depende del origen de datos. La aplicación debe seguir llamar a la función original hasta que el código de retorno no es SQL_STILL_EXECUTING. Si la función se canceló correctamente, el código de retorno es SQL_ERROR y SQLSTATE HY008 (operación cancelada). Si la función de completa su procesamiento normal, el código de retorno es SQL_SUCCESS o SQL_SUCCESS_WITH_INFO si la función se realizó correctamente o SQL_ERROR y un valor de SQLSTATE que no sea HY008 (operación cancelada) si la función produjo un error.  
  
> [!NOTE]  
>  ODBC 3.5, una llamada a **SQLCancel** cuando no se realiza ningún procesamiento en la instrucción no se trata como **SQLFreeStmt** con la opción SQL_CLOSE, pero tiene no es en absoluto ningún efecto. Para cerrar un cursor, una aplicación debe llamar a **SQLCloseCursor**, no **SQLCancel**.  
  
 Para obtener más información sobre el procesamiento asincrónico, vea [ejecución asincrónica](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md).  
  
## <a name="canceling-functions-that-need-data"></a>Cancelación de las funciones que necesitan los datos  
 Después de **SQLExecute** o **SQLExecDirect** devuelve SQL_NEED_DATA y antes de que se han enviado datos para todos los parámetros de datos en ejecución, puede llamar una aplicación **SQLCancel** Para cancelar la ejecución de la instrucción. Después de que se ha cancelado la instrucción, la aplicación puede llamar a **SQLExecute** o **SQLExecDirect** nuevo. Para obtener más información, consulte [SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md).  
  
 Después de **SQLBulkOperations** o **SQLSetPos** devuelve SQL_NEED_DATA y antes de que se han enviado datos para todas las columnas de datos en ejecución, puede llamar una aplicación **SQLCancel** Para cancelar la operación. Después de que se ha cancelado la operación, la aplicación puede llamar a **SQLBulkOperations** o **SQLSetPos** nuevo; Cancelar no afecta el estado del cursor o la posición actual del cursor. Para obtener más información, consulte [SQLBulkOperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md) o [SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md).  
  
## <a name="canceling-functions-executing-on-another-thread"></a>Cancelación de funciones que se ejecutan en otro subproceso  
 En una aplicación multiproceso, la aplicación puede cancelar una función que se está ejecutando en otro subproceso. Para cancelar la función, la aplicación llama a **SQLCancel** con el mismo identificador de instrucción que se utiliza la función de destino, pero en un subproceso diferente. Cómo se cancela la función depende del controlador y el sistema operativo. Al igual que en la cancelación de una función que se ejecuta de forma asincrónica, el código de retorno de la **SQLCancel** sólo indica si el controlador procesa la solicitud correctamente. Se puede devolver sólo SQL_SUCCESS o SQL_ERROR; no se devuelve ninguna información de diagnóstico. Si se cancela la función original, devuelve SQL_ERROR y SQLSTATE HY008 (operación cancelada).  
  
 Si una instrucción SQL se va a ejecutar cuando **SQLCancel** es llamado desde otro subproceso para cancelar la ejecución de instrucciones, es posible que la ejecución se realice correctamente y SQL_SUCCESS devuelto durante la cancelación también es correcta. En este caso, el Administrador de controladores se da por supuesto que la cancelación, cierra el cursor abierto mediante la ejecución de instrucciones para que la aplicación no podrá usar el cursor.  
  
 Para obtener más información acerca de los subprocesos, vea [Multithreading](../../../odbc/reference/develop-app/multithreading.md).  
  
## <a name="related-functions"></a>Funciones relacionadas  
  
|Para obtener información acerca de|Vea|  
|---------------------------|---------|  
|Enlazar un búfer con un parámetro|[Función SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md)|  
|Rendimiento masiva insertar o actualizar operaciones|[Función SQLBulkOperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md)|  
|Cancela una función que se ejecuta asincrónicamente en un identificador de conexión, además la funcionalidad de **SQLCancel**.|[Función SQLCancelHandle](../../../odbc/reference/syntax/sqlcancelhandle-function.md)|  
|Ejecutar una instrucción SQL|[Función SQLExecDirect](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|Ejecutar una instrucción SQL preparada|[Función SQLExecute](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|Liberar un identificador de instrucción|[SQLFreeStmt](../../../odbc/reference/syntax/sqlfreestmt-function.md)|  
|Obtención de un campo de un registro de diagnóstico o un campo del encabezado de diagnóstico|[Función SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)|  
|Obtención de varios campos de una estructura de datos de diagnóstico|[Función SQLGetDiagRec](../../../odbc/reference/syntax/sqlgetdiagrec-function.md)|  
|Devuelve el siguiente parámetro para enviar datos|[Función SQLParamData](../../../odbc/reference/syntax/sqlparamdata-function.md)|  
|Envío de datos de parámetro en tiempo de ejecución|[Función SQLPutData](../../../odbc/reference/syntax/sqlputdata-function.md)|  
|Sitúe el cursor en un conjunto de filas, actualizar los datos en el conjunto de filas, o actualizar o eliminar datos en el conjunto de resultados|[Función SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md)|  
  
## <a name="see-also"></a>Vea también  
 [Referencia de la API de ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Archivos de encabezado de ODBC](../../../odbc/reference/install/odbc-header-files.md)
