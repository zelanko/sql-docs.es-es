---
title: Notificación de la finalización de la función asíncrona ? Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 336565da-4203-4745-bce2-4f011c08e357
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a453967f2ffdda4af2a44429737f700f4a994cf8
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81287825"
---
# <a name="notification-of-asynchronous-function-completion"></a>Notificación de finalización asincrónica (función)
En el SDK de Windows 8, ODBC agregó un mecanismo para notificar a las aplicaciones cuando se completa una operación asincrónica, a la que nos referiremos como "notificación al finalizar". (Consulte Ejecución asincrónica (método de [notificación)](../../../odbc/reference/develop-app/asynchronous-execution-notification-method.md) para obtener más información.) En este tema se describen algunos de los problemas para los desarrolladores de controladores.  
  
## <a name="the-interface-between-the-driver-manager-and-driver"></a>La interfaz entre el administrador de controladores y el controlador  
 El Administrador de controladores proporciona internamente una función de devolución de [llamada SQLAsyncNotificationCallback (función).](../../../odbc/reference/develop-driver/sqlasyncnotificationcallback-function.md) **SQLAsyncNotificationCallback** solo puede ser llamado por el controlador: una aplicación no puede llamarlo directamente. El controlador llama a **SQLAsyncNotificationCallback** cada vez que se reciben nuevos datos del servidor después de devolver SQL_STILL_EXECUTING por última vez.  
  
 El Administrador de controladores proporciona un mecanismo de devolución de llamada para que un controlador pueda notificar al Administrador de controladores cuando se ha realizado algún progreso en la ejecución de una operación asincrónica después de que la función correspondiente devuelve SQL_STILL_EXECUTING  
  
 El Administrador de controladores establece el atributo SQL_ATTR_ASYNC_DBC_NOTIFICATION_CALLBACK en un identificador de conexión de controlador con un puntero de función no NULL, que es de tipo SQL_ASYNC_NOTIFICATION_CALLBACK, para que el controlador funcione en modo de notificación para cualquier operación asincrónica en ese identificador. De forma similar, el Administrador de controladores establece el atributo SQL_ATTR_ASYNC_STMT_NOTIFICATION_CALLBACK en un identificador de instrucción de controlador con un puntero de función no NULL, que también es de tipo SQL_ASYNC_NOTIFICATION_CALLBACK, para que el controlador funcione en modo de notificación para cualquier operación asincrónica en ese identificador.  
  
 Si se realiza una operación asincrónica en un identificador de controlador, las funciones de controlador asincrónico deben funcionar en un estilo sin bloqueo. Si la operación no se puede completar inmediatamente, la función de controlador debe devolver SQL_STILL_EXECUTING. Este requisito es cierto para el modo de sondeo y el modo de notificación.  
  
 Si un identificador está en modo asincrónico de notificación, el controlador debe llamar a la función de devolución de notificación, cuya dirección es el valor del atributo SQL_ATTR_ASYNC_DBC_NOTIFICATION_CALLBACK o SQL_ATTR_ASYNC_STMT_NOTIFICATION_CALLBACK, una vez después de devolver SQL_STILL_EXECUTING. En otras palabras, un SQL_STILL_EXECUTING que devuelve debe estar emparejado con una invocación de la función de devolución de llamada de notificación. El controlador debe utilizar el valor actual del atributo SQL_ATTR_ASYNC_DBC_NOTIFICATION_CONTEXT o SQL_ATTR_ASYNC_STMT_NOTIFICATION_CONTEXT handle como valor para el parámetro de función de devolución de llamada *pContext*.  
  
 El controlador no debe volver a llamar en el subproceso que llama a la función de controlador; no hay ninguna razón para notificar el progreso antes de que la función regrese. El controlador debe usar su propio subproceso para la devolución de llamada. El Administrador de controladores no usará el subproceso de devolución de llamada del controlador para ejecutar una lógica de procesamiento extensa.  
  
 El Administrador de controladores volverá a llamar a la función original después de que el controlador vuelva a llamar. El Administrador de controladores puede usar un subproceso que no es ni un subproceso de aplicación ni un subproceso de controlador. Si el controlador utiliza cierta información asociada con el subproceso (por ejemplo, token de seguridad o identificador de usuario), el controlador debe guardar la información necesaria en la llamada asincrónica inicial y usar el valor guardado antes de que se complete toda la operación asincrónica. Normalmente, solo **SQLDriverConnect**, **SQLConnect**o **SQLBrowseConnect** necesitan usar ese tipo de información.  
  
## <a name="see-also"></a>Consulte también  
 [Desarrollar un controlador ODBC](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)
