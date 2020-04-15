---
title: Función SQLCancelHandle ? Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
f1_keywords:
- SQLCancelHandle
helpviewer_keywords:
- SQLCancelHandle function [ODBC]
ms.assetid: 16049b5b-22a7-4640-9897-c25dd0f19d21
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 059ed283032feb96ca5e6b12520682ccb034752a
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299670"
---
# <a name="sqlcancelhandle-function"></a>Función SQLCancelHandle
**Conformidad**  
 Versión introducida: ODBC 3.8  
  
 Cumplimiento de normas: Ninguno  
  
 Se espera que la mayoría de los controladores ODBC 3.8 (y posteriores) implementarán esta función. Si un controlador no lo hace, una llamada a **SQLCancelHandle** con un identificador de conexión en *el* Handle parámetro devolverá SQL_ERROR con un SQLSTATE de IM001 y mensaje 'Driver no admite esta función'' Una llamada a **SQLCancelHandle** con un identificador de instrucción como el *Handle* parámetro se asignará a una llamada a **SQLCancel** por el Administrador de controladores y se puede procesar si el controlador implementa **SQLCancel**. Una aplicación puede usar **SQLGetFunctions** para determinar si un controlador admite **SQLCancelHandle**.  
  
 **Resumen**  
 **SQLCancelHandle** cancela el procesamiento en una conexión o instrucción. El Administrador de controladores asigna una llamada a **SQLCancelHandle** a una llamada a **SQLCancel** cuando *HandleType* es SQL_HANDLE_STMT.  
  
## <a name="syntax"></a>Sintaxis  
  
```cpp  
  
SQLRETURN SQLCancelHandle(  
      SQLSMALLINT  HandleType,  
      SQLHANDLE    Handle);  
```  
  
## <a name="arguments"></a>Argumentos  
 *HandleType*  
 [Entrada] El tipo de asa en la que se debe hacer el procesamiento de cacareos. Los valores válidos son SQL_HANDLE_DBC o SQL_HANDLE_STMT.  
  
 *Handle*  
 [Entrada] El identificador en el que se cancela el procesamiento.  
  
 Si *Handle* no es un identificador válido del tipo especificado por *HandleType*, **SQLCancelHandle** devuelve SQL_INVALID_HANDLE.  
  
## <a name="returns"></a>Devuelve  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnóstico  
 Cuando **SQLCancelHandle** devuelve SQL_ERROR o SQL_SUCCESS_WITH_INFO, se puede obtener un valor SQLSTATE asociado llamando a **SQLGetDiagRec** con un *HandleType* de SQL_HANDLE_STMT y un *identificador* de instrucción o un *HandleType* de SQL_HANDLE_DBC y un *identificador*de conexión .  
  
 En la tabla siguiente se enumeran los valores SQLSTATE devueltos normalmente por **SQLCancelHandle** y se explica cada uno de ellos en el contexto de esta función; la notación "(DM)" precede a las descripciones de SQLSTATEs devueltas por el Administrador de controladores. El código de retorno asociado a cada valor SQLSTATE se SQL_ERROR, a menos que se indique lo contrario.  
  
|SQLSTATE|Error|Descripción|  
|--------------|-----------|-----------------|  
|01000|Advertencia general|Mensaje informativo específico del controlador. (La función devuelve SQL_SUCCESS_WITH_INFO.)|  
|HY000|Error general|Se ha producido un error para el que no se ha definido sqlSTATE específico y para el que no se ha definido sqlSTATE específico de la implementación. El mensaje de error devuelto por [SQLGetDiagRec](../../../odbc/reference/syntax/sqlgetdiagrec-function.md) en el argumento * \*MessageText* buffer describe el error y su causa.|  
|HY001|Error de asignación de memoria|El controlador no pudo asignar la memoria necesaria para admitir la ejecución o finalización de la función.|  
|HY010|Error de secuencia de funciones|Se llamó a una función relacionada con instrucciones que se ejecuta de forma asincrónica para uno de los identificadores de instrucción asociados con *Handle*y *HandleType* se estableció en SQL_HANDLE_DBC. La función asincrónica todavía se estaba ejecutando cuando **SQLCancelHandle** se llamó.<br /><br /> (DM) El *HandleType* argumento se SQL_HANDLE_STMT; se llamó a una función de ejecución asincrónica en el identificador de conexión asociado; y la función todavía se estaba ejecutando cuando se llamó a esta función.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**o **SQLMoreResults** se llamó para uno de los identificadores de instrucción asociados con el *Handle* y *HandleType* se estableció en SQL_HANDLE_DBC y devolvió SQL_PARAM_DATA_AVAILABLE. Se llamó a esta función antes de recuperar los datos para todos los parámetros transmitidos.<br /><br /> **SQLBrowseConnect** se llamó para *ConnectionHandle*y SQL_NEED_DATA devuelto. Esta función se llamó antes de que se completara el proceso de exploración.|  
|HY013|Error de administración de memoria|No se pudo procesar la llamada de función porque no se pudo tener acceso a los objetos de memoria subyacentes, posiblemente debido a condiciones de poca memoria.|  
|HY092|Identificador de atributo/opción no válido|*HandleType* se estableció en SQL_HANDLE_ENV o SQL_HANDLE_DESC.|  
|HY117|La conexión se suspende debido al estado de transacción desconocido. Solo se permiten funciones de desconexión y de solo lectura.|(DM) Para obtener más información sobre el estado suspendido, vea [SqlEndTran (función).](../../../odbc/reference/syntax/sqlendtran-function.md)|  
|HYT01|Tiempo de espera de conexión expirado|El período de tiempo de espera de conexión expiró antes de que el origen de datos respondiera a la solicitud. El período de tiempo de espera de conexión se establece a través de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|El controlador no admite esta función|(DM) El controlador asociado con el *controlador* no admite la función.|  
  
 Si **SQLCancelHandle** se llama con *HandleType* establecido en SQL_HANDLE_STMT, puede devolver cualquier SQLSTATE que pueda devolver la función **SQLCancel**.  
  
## <a name="comments"></a>Comentarios  
 Esta función es similar a **SQLCancel,** pero puede tomar una conexión o un identificador de instrucción como parámetro en lugar de solo un identificador de instrucción. El Administrador de controladores asigna una llamada a **SQLCancelHandle** a una llamada a **SQLCancel** cuando *HandleType* es SQL_HANDLE_STMT. Esto permite a las aplicaciones usar **SQLCancelHandle** para cancelar operaciones de instrucción incluso si el controlador no implementa **SQLCancelHandle**.  
  
 Para obtener más información acerca de cómo cancelar una operación de instrucción, vea [SQLCancel (función)](../../../odbc/reference/syntax/sqlcancel-function.md).  
  
 Si no hay ninguna operación en curso en *Controlar* la llamada a **SQLCancelHandle** no tiene ningún efecto.  
  
 **SQLCancelHandle** en un identificador de conexión puede cancelar los siguientes tipos de procesamiento:  
  
-   Función que se ejecuta de forma asincrónica en la conexión.  
  
-   Función que se ejecuta en el identificador de conexión en otro subproceso.  
  
 Cuando **SQLCancelHandle** se llama para cancelar una función que se ejecuta de forma asincrónica en una conexión, los registros de diagnóstico publicados por **SQLCancelHandle** se anexan a los devueltos por la operación que se cancela; **SQLCancelHandle** no devuelve registros de diagnóstico, sin embargo, al cancelar una función que se ejecuta en una conexión en otro subproceso.  
  
 El uso de **SQLCancelHandle** para cancelar **SQLEndTran** puede poner la conexión en estado suspendido. Para obtener más información sobre el estado suspendido, vea [SqlEndTran (función).](../../../odbc/reference/syntax/sqlendtran-function.md)  
  
> [!NOTE]  
>  Para obtener información acerca de cómo usar **SQLCancelHandle** en una aplicación que se implementará en un sistema operativo Windows anterior a Windows 7, vea Matriz de [compatibilidad](../../../odbc/reference/develop-app/compatibility-matrix.md).  
  
#### <a name="canceling-connection-related-asynchronous-processing"></a>Cancelación del procesamiento asincrónico relacionado con la conexión  
 Si una función devuelve SQL_STILL_EXECUTING, una aplicación puede llamar a **SQLCancelHandle** para cancelar la operación. Si la solicitud de cancelación se realiza correctamente, **SQLCancelHandle** devuelve SQL_SUCCESS. Esto no significa que la función original se canceló; indica que se ha procesado la solicitud de cancelación. El controlador y el origen de datos determinan cuándo o si se cancela la operación. La aplicación debe seguir llamando a la función original hasta que el código de retorno no se SQL_STILL_EXECUTING. Si se canceló la función original, el código de retorno se SQL_ERROR y SQLSTATE HY008 (Operación cancelada). Si la función original completó su procesamiento normal (no se canceló), el código de retorno se SQL_SUCCESS o SQL_SUCCESS_WITH_INFO, o SQL_ERROR y un SQLSTATE distinto de HY008 (Operación cancelada), si la función original falla.  
  
#### <a name="canceling-functions-executing-on-another-thread"></a>Cancelación de funciones que se ejecutan en otro subproceso  
 En una aplicación multiproceso, la aplicación puede cancelar una operación que se ejecuta en otro subproceso. Para cancelar la operación, la aplicación llama a **SQLCancelHandle** con el identificador utilizado por la función, pero en un subproceso diferente. El controlador y el sistema operativo determinan cómo se cancela la operación. El código de retorno **SQLCancelHandle** indica si el controlador procesó la solicitud, devolviendo SQL_SUCCESS o SQL_ERROR (no se devuelve ninguna información de diagnóstico). Si se cancela el procesamiento de la función original, la función original devuelve SQL_ERROR y SQLSTATE HY008 (Operación cancelada).  
  
 Si se ejecuta una función cuando **SQLCancelHandle** se llama en otro subproceso para cancelar la función, es posible que la función se realice correctamente y devuelva SQL_SUCCESS antes de que la cancelación pueda surtir efecto. Una llamada a **SQLCancelHandle** no tiene ningún efecto si la operación completada antes de **SQLCancelHandle** pudo cancelar la operación.  
  
## <a name="related-functions"></a>Funciones relacionadas  
  
|Para información acerca de|Vea|  
|---------------------------|---------|  
|Cancelar una función que se ejecuta de forma asincrónica en un identificador de instrucción, cancelar una función en una instrucción que necesita datos o cancelar una función que se ejecuta en una instrucción en otro subproceso.|[Función SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de la API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Archivos de encabezado ODBC](../../../odbc/reference/install/odbc-header-files.md)   
 [Ejecución asincrónica (método de sondeo)](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md)
