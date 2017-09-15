---
title: "Notificación de finalización de la función asincrónica | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 336565da-4203-4745-bce2-4f011c08e357
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 91c63c55a3d36e1b0c788361a8ae13a01ece9a38
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="notification-of-asynchronous-function-completion"></a>Notificación de finalización asincrónica (función)
En el SDK de Windows 8, ODBC agrega un mecanismo para notificar a las aplicaciones cuando se completa una operación asincrónica, lo que nos referiremos a como "notificación de finalización". (Consulte [ejecución asincrónica (método de notificación)](../../../odbc/reference/develop-app/asynchronous-execution-notification-method.md) para obtener más información.) En este tema se trata algunos de los problemas para los desarrolladores de controladores.  
  
## <a name="the-interface-between-the-driver-manager-and-driver"></a>La interfaz entre el controlador y el Administrador de controladores  
 Internamente, el Administrador de controladores proporciona una función de devolución de llamada [SQLAsyncNotificationCallback función](../../../odbc/reference/develop-driver/sqlasyncnotificationcallback-function.md). **SQLAsyncNotificationCallback** sólo puede ser llamado por el controlador: una aplicación no puede llamar directamente a él. El controlador llama **SQLAsyncNotificationCallback** siempre nuevos datos recibieron del servidor después de la última SQL_STILL_EXECUTING devolver.  
  
 El Administrador de controladores proporciona un mecanismo de devolución de llamada para que un controlador puede notificar el Administrador de controladores cuando se ha realizado algún progreso en la ejecución de una operación asincrónica después de que la función correspondiente devuelva SQL_STILL_EXECUTING  
  
 El Administrador de controladores se establece el atributo SQL_ATTR_ASYNC_DBC_NOTIFICATION_CALLBACK en un identificador de conexión de controlador con un puntero de función no es NULL, que es de tipo SQL_ASYNC_NOTIFICATION_CALLBACK, para que funcione en modo de notificación para el controlador cualquier asincrónica operaciones con ese identificador. De igual forma, el Administrador de controladores establece el atributo SQL_ATTR_ASYNC_STMT_NOTIFICATION_CALLBACK en un identificador de instrucción de controlador con un puntero de función no es NULL, que también es de tipo SQL_ASYNC_NOTIFICATION_CALLBACK, para que funcione en modo de notificación para el controlador todas las operaciones asincrónicas en ese identificador.  
  
 Si se realiza una operación asincrónica en un identificador de controlador, las funciones de controlador asincrónico deberían funcionar en un estilo de no bloqueo. Si la operación no se puede completar inmediatamente, la función de controlador debe devolver SQL_STILL_EXECUTING. Este requisito es true para los modos de sondeo y notificación.  
  
 Si un controlador está en modo asincrónico de notificación, el controlador debe llamar a la función de devolución de llamada de notificación, cuya dirección es el valor para el atributo SQL_ATTR_ASYNC_DBC_NOTIFICATION_CALLBACK o SQL_ATTR_ASYNC_STMT_NOTIFICATION_CALLBACK, una vez después de devolver SQL_STILL_EXECUTING. En otras palabras, un SQL_STILL_EXECUTING devolver deben estar emparejadas con una invocación de la función de devolución de llamada de notificación. El controlador debe usar el valor actual del atributo de identificador SQL_ATTR_ASYNC_DBC_NOTIFICATION_CONTEXT o SQL_ATTR_ASYNC_STMT_NOTIFICATION_CONTEXT como el valor para el parámetro de función de respuesta de llamada *pContext*.  
  
 El controlador no debe devolver llamada en el subproceso que llama a la función de controlador; No hay ninguna razón para notificar el progreso antes de que la función devuelve. El controlador debe utilizar su propio subproceso de devolución de llamada. El Administrador de controladores no usará el subproceso de devolución de llamada del controlador para ejecutar lógica de procesamientos exhaustivos.  
  
 El Administrador de controladores llamará a la función original de nuevo después de que el controlador llama de nuevo. El Administrador de controladores puede utilizar un subproceso que no es un subproceso de aplicación ni un subproceso de controlador. Si el controlador utiliza cierta información asociada al subproceso (por ejemplo, identificador de seguridad token o usuario), el controlador debe guardar la información necesaria en la llamada asincrónica inicial y usar el valor guardado antes de la operación completa asincrónica completa. Por lo general, sólo **SQLDriverConnect**, **SQLConnect**, o **SQLBrowseConnect** necesite utilizar ese tipo de información.  
  
## <a name="see-also"></a>Vea también  
 [Desarrollar un controlador ODBC](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)
