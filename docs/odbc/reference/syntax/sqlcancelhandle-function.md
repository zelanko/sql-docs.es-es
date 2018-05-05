---
title: Función SQLCancelHandle | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- SQLCancelHandle
helpviewer_keywords:
- SQLCancelHandle function [ODBC]
ms.assetid: 16049b5b-22a7-4640-9897-c25dd0f19d21
caps.latest.revision: 22
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 122e4dc49082e3bd6853ebee299e8b37d1a39596
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="sqlcancelhandle-function"></a>SQLCancelHandle (función)
**Conformidad**  
 Versión incluyen: 3.8 de ODBC  
  
 Cumplimiento de normas: ninguno  
  
 Se espera que la mayoría ODBC 3.8 (y versiones posteriores) de los controladores implementará esta función. Si un controlador no es así, una llamada a **SQLCancelHandle** con una conexión de controlar en el *controlar* parámetro devolverá SQL_ERROR con un mensaje y SQLSTATE de IM001 ' controlador no admite esta función '' una llamada para **SQLCancelHandle** con una instrucción tratar como el *controlar* parámetro se asignarán a una llamada a **SQLCancel** por el Administrador de controladores y puede procesarse si el controlador implementa **SQLCancel**. Una aplicación puede usar **SQLGetFunctions** para determinar si un controlador es compatible con **SQLCancelHandle**.  
  
 **Resumen**  
 **SQLCancelHandle** cancela el procesamiento en una conexión o instrucción. El Administrador de controladores se asigna una llamada a **SQLCancelHandle** a una llamada a **SQLCancel** cuando *HandleType* es SQL_HANDLE_STMT.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
SQLRETURN SQLCancelHandle(  
      SQLSMALLINT  HandleType,  
      SQLHANDLE    Handle);  
```  
  
## <a name="arguments"></a>Argumentos  
 *HandleType*  
 [Entrada] El tipo del identificador en el que el procesamiento de cacel. Los valores válidos son SQL_HANDLE_DBC o SQL_HANDLE_STMT.  
  
 *Handle*  
 [Entrada] El identificador en el que se va a cancelar el procesamiento.  
  
 Si *controlar* no es un identificador válido del tipo especificado por *HandleType*, **SQLCancelHandle** devuelva SQL_INVALID_HANDLE.  
  
## <a name="returns"></a>Devuelve  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Cuando **SQLCancelHandle** devuelve SQL_ERROR o SQL_SUCCESS_WITH_INFO, un valor SQLSTATE asociado se puede obtener mediante una llamada a **SQLGetDiagRec** con un *HandleType* de Controlan SQL_HANDLE_STMT y una instrucción *controlar* o un *HandleType* de SQL_HANDLE_DBC y un identificador de conexión *controlar*.  
  
 En la tabla siguiente se enumera los valores SQLSTATE devueltos normalmente por **SQLCancelHandle** y se explica cada uno de ellos en el contexto de esta función; la notación "(DM)" precede a las descripciones de SQLSTATE devuelto por el Administrador de controladores. El código de retorno asociado a cada valor SQLSTATE es SQL_ERROR, a menos que se indique lo contrario.  
  
|SQLSTATE|Error|Description|  
|--------------|-----------|-----------------|  
|01000|Advertencia general|Mensaje informativo de específicas del controlador. (La función devuelve SQL_SUCCESS_WITH_INFO).|  
|HY000|Error general|Se produjo un error para que no hubo ninguna SQLSTATE específico y para el que se ha definido ningún SQLSTATE específico de la implementación. El mensaje de error devuelto por [SQLGetDiagRec](../../../odbc/reference/syntax/sqlgetdiagrec-function.md) en el argumento  *\*MessageText* búfer describe el error y su causa.|  
|HY001|Error de asignación de memoria|El controlador no pudo asignar la memoria necesaria para admitir la ejecución o la finalización de la función.|  
|HY010|Error de secuencia de función|Se llamó a una función ejecuta de forma asincrónica, relacionado con la instrucción para uno de los identificadores de instrucción asociados a la *controlar*, y *HandleType* se ha establecido en SQL_HANDLE_DBC. La función asincrónica aún estaba ejecutando cuando **SQLCancelHandle** se llamó.<br /><br /> (DM) la *HandleType* argumento era SQL_HANDLE_STMT; se llamó a una función ejecuta de forma asincrónica en el identificador de conexión asociada; y la función aún se estaba ejecutando cuando se llamó a esta función.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, o **SQLMoreResults** se llama para uno de los identificadores de instrucción asociados a la *controlar* y *HandleType* se establece en SQL_HANDLE_DBC y se devolvió SQL_PARAM_DATA_AVAILABLE. Esta función se invoca antes de que se recuperan los datos para todos los parámetros transmitidos.<br /><br /> **SQLBrowseConnect** se llamó para *IdentificadorConexión*y devuelve SQL_NEED_DATA. Esta función se invoca antes de completar el proceso de exploración.|  
|HY013|Error de administración de memoria|No se pudo procesar la llamada de función porque los objetos subyacentes de la memoria no se pudieron tener acceso, posiblemente debido a condiciones de memoria insuficiente.|  
|HY092|Identificador de opción o atributo no válido|*HandleType* se estableció en SQL_HANDLE_ENV o SQL_HANDLE_DESC.|  
|HY117|Se suspende la conexión debido al estado de transacción desconocido. Solo se desconecte y se permiten las funciones de solo lectura.|(DM) para obtener más información sobre el estado suspendido, consulte [función SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYT01|Tiempo de espera de conexión expirado|El período de tiempo de espera de conexión finalizó antes de que el origen de datos se respondió a la solicitud. El período de tiempo de espera de conexión se establece a través de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Controlador no admite esta función|(DM) el controlador asociado a la *controlar* no admite la función.|  
  
 Si **SQLCancelHandle** se llama con *HandleType* establecido en SQL_HANDLE_STMT, puede devolver cualquier SQLSTATE, que puede ser devueltos por la función **SQLCancel**.  
  
## <a name="comments"></a>Comentarios  
 Esta función es similar a **SQLCancel** pero puede tardar una conexión o la instrucción identificador como un parámetro en lugar de un identificador de instrucción. El Administrador de controladores se asigna una llamada a **SQLCancelHandle** a una llamada a **SQLCancel** cuando *HandleType* es SQL_HANDLE_STMT. Esto permite que las aplicaciones usen **SQLCancelHandle** para cancelar la operación de instrucción incluso si el controlador no implementa **SQLCancelHandle**.  
  
 Para obtener más información acerca de cómo cancelar una operación de instrucción, consulte [SQLCancel, función](../../../odbc/reference/syntax/sqlcancel-function.md).  
  
 Si no hay ninguna operación en curso en *controlar* la llamada a **SQLCancelHandle** no tiene ningún efecto.  
  
 **SQLCancelHandle** en una conexión identificador puede cancelar los siguientes tipos de procesamiento:  
  
-   Una función que se ejecutan de forma asincrónica en la conexión.  
  
-   Una función que se ejecuta en el identificador de conexión en otro subproceso.  
  
 Cuando **SQLCancelHandle** se llama para cancelar una función que se ejecuta de forma asincrónica en una conexión, los registros de diagnóstico publicados por **SQLCancelHandle** se anexan a los devueltos por la operación que se va a cancelado; **SQLCancelHandle** no devuelve los registros de diagnóstico, sin embargo, al cancelar una función que se ejecuta en una conexión en otro subproceso.  
  
 Usar **SQLCancelHandle** cancelar **SQLEndTran** puede colocar la conexión en estado suspendido. Para obtener más información sobre el estado suspendido, consulte [función SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).  
  
> [!NOTE]  
>  Para obtener información sobre cómo usar **SQLCancelHandle** en una aplicación que se implementará en un sistema operativo de Windows anterior a Windows 7, consulte [la matriz de compatibilidad](../../../odbc/reference/develop-app/compatibility-matrix.md).  
  
#### <a name="canceling-connection-related-asynchronous-processing"></a>Cancelar el procesamiento asincrónico relacionado con la conexión  
 Si una función devuelve SQL_STILL_EXECUTING, una aplicación puede llamar a **SQLCancelHandle** para cancelar la operación. Si la solicitud de cancelación se realiza correctamente, **SQLCancelHandle** devuelve SQL_SUCCESS. Esto no significa que se ha cancelado la función original; indica que se procesó la solicitud de cancelación. El controlador y el origen de datos se determinan cuando o si se cancela la operación. La aplicación debe seguir llamar a la función original hasta que el código de retorno no se SQL_STILL_EXECUTING. Si se ha cancelado la función original, el código de retorno es SQL_ERROR y SQLSTATE HY008 (operación cancelada). Si la función original completa su procesamiento normal (no canceló), el código de retorno es SQL_SUCCESS o SQL_SUCCESS_WITH_INFO, o SQL_ERROR y un valor de SQLSTATE que no sea HY008 (operación cancelada), si produce un error de la función original.  
  
#### <a name="canceling-functions-executing-on-another-thread"></a>Cancelar las funciones que se ejecuta en otro subproceso  
 En una aplicación multiproceso, la aplicación puede cancelar una operación que se ejecuta en otro subproceso. Para cancelar la operación, la aplicación llama **SQLCancelHandle** con el identificador usado por la función, pero en un subproceso diferente. El controlador y el sistema operativo determinan cómo se cancela la operación. El **SQLCancelHandle** devolver código indica si el controlador procesa la solicitud, y devuelve SQL_SUCCESS o SQL_ERROR (no se devuelve ninguna información de diagnóstico). Si se cancela el procesamiento en la función original, la función original devuelve SQL_ERROR y SQLSTATE HY008 (operación cancelada).  
  
 Si se va una función se ejecuta cuando **SQLCancelHandle** se llama en otro subproceso para cancelar la función, es posible que la función sea correcta y devolver SQL_SUCCESS para que surta efecto la cancelación. Una llamada a **SQLCancelHandle** no tiene ningún efecto si la operación se completó antes de **SQLCancelHandle** pudo cancelar la operación.  
  
## <a name="related-functions"></a>Funciones relacionadas  
  
|Para obtener información acerca de|Vea|  
|---------------------------|---------|  
|Una función que se ejecuta de forma asincrónica en un identificador de instrucción, cancelar una función en una instrucción que necesita que los datos o cancelar una función que se ejecuta en una instrucción en otro subproceso se está cancelando.|[Función SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
  
## <a name="see-also"></a>Vea también  
 [Referencia de la API de ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Archivos de encabezado ODBC](../../../odbc/reference/install/odbc-header-files.md)   
 [Ejecución asincrónica (método de sondeo)](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md)
