---
title: Función SQLAsyncNotificationCallback | Documentos de Microsoft
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
ms.assetid: c56aedc9-f7f7-4641-b605-f0f98ed4400c
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2dc584145ea87b34ecfa9417cc89135b1fbc98d4
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="sqlasyncnotificationcallback-function"></a>SQLAsyncNotificationCallback (función)
**Conformidad**  
 Versión incluyen: 3.8 de ODBC  
  
 Cumplimiento de normas: ninguno  
  
 **Resumen**  
 **SQLAsyncNotificationCallback** permite que el controlador para volver a llamar al administrador de controladores cuando no hay algunos progreso de la operación asincrónica actual después de que el controlador devuelve SQL_STILL_EXECUTING. **SQLAsyncNotificationCallback** puede solo llamado por el controlador.  
  
 No llame los controladores **SQLAsyncNotificationCallback** con el nombre de la función **SQLAsyncNotificationCallback**. En su lugar, el Administrador de controladores pasa un puntero a función a un controlador como el valor para el atributo SQL_ATTR_ASYNC_DBC_NOTIFICATION_CALLBACK o SQL_ATTR_ASYNC_STMT_NOTIFICATION_CALLBACK del identificador de conexión correspondiente o identificador de instrucción respectivamente. Es posible asignar valores de puntero de función diferentes identificadores diferentes. El tipo del puntero de función se define como SQL_ASYNC_NOTIFICATION_CALLBACK.  
  
 **SQLAsyncNotificationCallback** es segura para subprocesos. Un controlador puede optar por usar varios subprocesos que llaman a **SQLAsyncNotificationCallback** en diferentes controla simultáneamente.  
  
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
 Utiliza un controlador para indica que esta invocación de función de devolución de llamada es la última de ellas para la operación asincrónica actual. Cuando el Administrador de controladores llama a la función nuevo, el controlador devolverá un código de retorno distinto de SQL_STILL_EXECUTING. El Administrador de controladores puede utilizar esta información, por ejemplo, para informar a la aplicación de antemano que finalizará la operación asincrónica.  
  
 Si *controlar* no es un identificador válido del tipo especificado por *HandleType*, **SQLCancelHandle** devuelva SQL_INVALID_HANDLE.  
  
## <a name="returns"></a>Devuelve  
 SQL_SUCCESS o SQL_ERROR.  
  
## <a name="diagnostics"></a>Diagnósticos  
 **SQLAsyncNotificationCallback** puede devolver SQL_ERROR en las siguientes dos situaciones (éstas indican un problema de implementación en el controlador o el Administrador de controladores.  
  
|Error|Description|  
|-----------|-----------------|  
|Conexión o instrucción no ha solicitado la notificación.||  
|No válido *controlar*|El controlador pasa un identificador no válido, que no se pudo las pruebas de validación del Administrador de controladores interno.|  
  
## <a name="see-also"></a>Vea también  
 [Ejecución asincrónica (método de sondeo)](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md)
