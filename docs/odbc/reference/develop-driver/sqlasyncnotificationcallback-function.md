---
title: FUNción SQLAsyncNotificationCallback ( SQLAsyncNotificationCallback) Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: c56aedc9-f7f7-4641-b605-f0f98ed4400c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e6c182c48b8e5ddb70204ddd3a94d9651f97595d
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81294542"
---
# <a name="sqlasyncnotificationcallback-function"></a>SQLAsyncNotificationCallback (función)
**Conformidad**  
 Versión introducida: ODBC 3.8  
  
 Cumplimiento de normas: Ninguno  
  
 **Resumen**  
 **SQLAsyncNotificationCallback** permite que un controlador vuelva a llamar al Administrador de controladores cuando hay algún progreso para la operación asincrónica actual después de que el controlador devuelve SQL_STILL_EXECUTING. **SQLAsyncNotificationCallback** solo puede llamar lo del controlador.  
  
 Los controladores no llaman a **SQLAsyncNotificationCallback** con el nombre de función **SQLAsyncNotificationCallback**. En su lugar, el Administrador de controladores pasa un puntero de función a un controlador como el valor del atributo SQL_ATTR_ASYNC_DBC_NOTIFICATION_CALLBACK o SQL_ATTR_ASYNC_STMT_NOTIFICATION_CALLBACK del identificador de conexión o identificador de instrucción correspondiente, respectivamente. A los diferentes identificadores se les pueden asignar diferentes valores de puntero de función. El tipo del puntero de función se define como SQL_ASYNC_NOTIFICATION_CALLBACK.  
  
 **SQLAsyncNotificationCallback** es seguro para subprocesos. Un controlador puede elegir usar varios subprocesos que llamen a **SQLAsyncNotificationCallback** en identificadores diferentes simultáneamente.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
typedef SQLRETURN (SQL_API *SQL_ASYNC_NOTIFICATION_CALLBACK)(  
   SQLPOINTER pContex,   
   BOOL fLast);  
```  
  
## <a name="arguments"></a>Argumentos  
 *pContex*  
 Puntero a una estructura de datos definida por el Administrador de controladores. El valor se pasa al controlador a través de SQLSetConnectAttr(SQL_ATTR_ASYNC_DBC_NOTIFICATION_CONTEXT) o SQLSetStmtAttr(SQL_ATTR_ASYNC_STMT_NOTIFICATION_CONTEXT).  El controlador no tiene acceso al valor.  
  
 *fLast*  
 Utilizado por un controlador para indicar que esta invocación de función de devolución de llamada es la última para la operación asincrónica actual. El controlador devolverá un código de retorno distinto de SQL_STILL_EXECUTING cuando el Administrador de controladores vuelve a llamar a la función. El Administrador de controladores puede utilizar esta información, por ejemplo, para informar a la aplicación con antelación de que se completará la operación asincrónica.  
  
 Si *Handle* no es un identificador válido del tipo especificado por *HandleType*, **SQLCancelHandle** devuelve SQL_INVALID_HANDLE.  
  
## <a name="returns"></a>Devuelve  
 SQL_SUCCESS o SQL_ERROR.  
  
## <a name="diagnostics"></a>Diagnóstico  
 **SQLAsyncNotificationCallback** puede devolver SQL_ERROR para las dos situaciones siguientes (indican un problema de implementación en el controlador o el Administrador de controladores.  
  
|Error|Descripción|  
|-----------|-----------------|  
|La conexión o la instrucción no solicitaron notificación.||  
|*Mango no válido*|El controlador pasó un identificador no válido, que no superó las pruebas de validación internas del Administrador de controladores.|  
  
## <a name="see-also"></a>Consulte también  
 [Ejecución asincrónica (método de sondeo)](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md)
