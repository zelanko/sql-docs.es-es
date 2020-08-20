---
description: Notificación de finalización asincrónica (función)
title: Notificación de finalización de la función asincrónica | Microsoft Docs
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
ms.openlocfilehash: d6e762e6b144e6a713f22429dccf43e1d27d8b24
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476264"
---
# <a name="notification-of-asynchronous-function-completion"></a>Notificación de finalización asincrónica (función)
En el SDK de Windows 8, ODBC agregó un mecanismo para notificar a las aplicaciones cuando se completa una operación asincrónica, a la que nos referiremos como "notificación al finalizar". (Consulte [ejecución asincrónica (método de notificación)](../../../odbc/reference/develop-app/asynchronous-execution-notification-method.md) para obtener más información). En este tema se describen algunos de los problemas de los desarrolladores de controladores.  
  
## <a name="the-interface-between-the-driver-manager-and-driver"></a>La interfaz entre el administrador de controladores y el controlador  
 El administrador de controladores proporciona internamente una función de devolución de llamada [SQLAsyncNotificationCallback](../../../odbc/reference/develop-driver/sqlasyncnotificationcallback-function.md). El controlador solo puede llamar a **SQLAsyncNotificationCallback** : una aplicación no puede llamarlo directamente. El controlador llama a **SQLAsyncNotificationCallback** cada vez que se reciben nuevos datos desde el servidor después de la última devolución de SQL_STILL_EXECUTING.  
  
 El administrador de controladores proporciona un mecanismo de devolución de llamada para que un controlador pueda notificar al administrador de controladores cuando se ha realizado algún progreso en la ejecución de una operación asincrónica después de que la función correspondiente devuelva SQL_STILL_EXECUTING  
  
 El administrador de controladores establece el atributo de SQL_ATTR_ASYNC_DBC_NOTIFICATION_CALLBACK en un identificador de conexión de controlador con un puntero de función que no es NULL, que es de tipo SQL_ASYNC_NOTIFICATION_CALLBACK, para que el controlador funcione en modo de notificación para las operaciones asincrónicas en ese controlador. Del mismo modo, el administrador de controladores establece el atributo de SQL_ATTR_ASYNC_STMT_NOTIFICATION_CALLBACK en un identificador de instrucción de controlador con un puntero de función que no es NULL, que es también de tipo SQL_ASYNC_NOTIFICATION_CALLBACK, para que el controlador funcione en modo de notificación para las operaciones asincrónicas en ese controlador.  
  
 Si se realiza una operación asincrónica en un identificador de controlador, las funciones del controlador asincrónico deben funcionar en un estilo que no sea de bloqueo. Si la operación no se puede completar inmediatamente, la función de controlador debe devolver SQL_STILL_EXECUTING. Este requisito se cumple para el modo de sondeo y el modo de notificación.  
  
 Si un identificador está en modo asincrónico de notificación, el controlador debe llamar a la función de devolución de llamada de notificación, cuya dirección es el valor del atributo SQL_ATTR_ASYNC_DBC_NOTIFICATION_CALLBACK o SQL_ATTR_ASYNC_STMT_NOTIFICATION_CALLBACK, una vez que se devuelve SQL_STILL_EXECUTING. En otras palabras, una SQL_STILL_EXECUTING devuelta debe emparejarse con una invocación de la función de devolución de llamada de notificación. El controlador debe usar el valor actual del atributo de identificador SQL_ATTR_ASYNC_DBC_NOTIFICATION_CONTEXT o SQL_ATTR_ASYNC_STMT_NOTIFICATION_CONTEXT como valor del parámetro de función de devolución de llamada *pContext*.  
  
 El controlador no debe devolver una llamada en el subproceso que llama a la función de controlador. no hay ninguna razón para notificar el progreso antes de que se devuelva la función. El controlador debe usar su propio subproceso para la devolución de llamada. El administrador de controladores no usará el subproceso de devolución de llamada del controlador para ejecutar una lógica de procesamiento extensa.  
  
 El administrador de controladores llamará de nuevo a la función original después de volver a llamar al controlador. El administrador de controladores puede usar un subproceso que no sea ni un subproceso de aplicación ni un subproceso de controlador. Si el controlador utiliza alguna información asociada con el subproceso (por ejemplo, un token de seguridad o un identificador de usuario), el controlador debe guardar la información necesaria en la llamada asincrónica inicial y usar el valor guardado antes de que se complete la operación asincrónica completa. Normalmente, solo **SQLDriverConnect**, **SQLConnect**o **SQLBrowseConnect** necesitan usar ese tipo de información.  
  
## <a name="see-also"></a>Consulte también  
 [Desarrollar un controlador ODBC](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)
