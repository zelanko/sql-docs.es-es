---
title: Notificación de finalización de la función asincrónica | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 336565da-4203-4745-bce2-4f011c08e357
author: MightyPen
ms.author: genemi
ms.openlocfilehash: de3496661f2ab329e5bf662a9cb8fa749cb81bfc
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68129320"
---
# <a name="notification-of-asynchronous-function-completion"></a>Notificación de finalización asincrónica (función)
En el SDK de Windows 8, ODBC agrega un mecanismo para notificar a las aplicaciones cuando se completa una operación asincrónica, lo que nos referiremos como "notificación de finalización". (Consulte [ejecución asincrónica (método de notificación)](../../../odbc/reference/develop-app/asynchronous-execution-notification-method.md) para obtener más información.) Este tema describen algunos de los problemas para los desarrolladores de controladores.  
  
## <a name="the-interface-between-the-driver-manager-and-driver"></a>La interfaz entre el Administrador de controladores y el controlador  
 Internamente, el Administrador de controladores proporciona una función de devolución de llamada [SQLAsyncNotificationCallback (función)](../../../odbc/reference/develop-driver/sqlasyncnotificationcallback-function.md). **SQLAsyncNotificationCallback** solo se puede llamar mediante el controlador de una aplicación no puede llamar directamente. El controlador llama a **SQLAsyncNotificationCallback** cada vez que se reciben nuevos datos desde el servidor después de la última SQL_STILL_EXECUTING devolver.  
  
 El Administrador de controladores proporciona un mecanismo de devolución de llamada para que un controlador puede notificar el Administrador de controladores cuando se ha realizado algún progreso en la ejecución de una operación asincrónica después de la función correspondiente devuelve SQL_STILL_EXECUTING  
  
 El Administrador de controladores se establece el atributo SQL_ATTR_ASYNC_DBC_NOTIFICATION_CALLBACK en un identificador de conexión de controlador con un puntero de función que no es NULL, que es de tipo SQL_ASYNC_NOTIFICATION_CALLBACK, para que funcione en modo de notificación para el controlador cualquier asincrónica operaciones en ese controlador. De forma similar, el Administrador de controladores establece el atributo SQL_ATTR_ASYNC_STMT_NOTIFICATION_CALLBACK en un identificador de instrucción del controlador con un puntero de función que no es NULL, que también es de tipo SQL_ASYNC_NOTIFICATION_CALLBACK, para que funcione en modo de notificación para el controlador las operaciones asincrónicas en ese identificador.  
  
 Si se realiza una operación asincrónica en un identificador de controlador, las funciones de controlador asincrónico deberían funcionar en un estilo que no sean de bloqueo. Si la operación no se puede completar inmediatamente, la función de controlador debe devolver SQL_STILL_EXECUTING. Este requisito es cierto para los modos de sondeo y notificación.  
  
 Si un controlador está en modo asincrónico de notificación, el controlador debe llamar a la función de devolución de llamada de notificación, cuya dirección es el valor del atributo SQL_ATTR_ASYNC_DBC_NOTIFICATION_CALLBACK o SQL_ATTR_ASYNC_STMT_NOTIFICATION_CALLBACK, una vez después de devolver SQL_STILL_EXECUTING. En otras palabras, SQL_STILL_EXECUTING devolver uno debe estar emparejado con una invocación de la función de devolución de llamada de notificación. El controlador debe usar el valor actual del atributo de identificador SQL_ATTR_ASYNC_DBC_NOTIFICATION_CONTEXT o SQL_ATTR_ASYNC_STMT_NOTIFICATION_CONTEXT como valor para el parámetro de función de devolución de llamada *pContext*.  
  
 El controlador debe no volver a llamar en el subproceso que llama a la función de controlador; No hay ninguna razón para notificar el progreso antes de que vuelva la función. El controlador debe usar su propio subproceso de devolución de llamada. El Administrador de controladores no usará el subproceso de devolución de llamada del controlador para ejecutar lógica de procesamientos exhaustivos.  
  
 El Administrador de controladores llamará a la función original de nuevo después de que el controlador llama de nuevo. El Administrador de controladores puede utilizar un subproceso que no es un subproceso de aplicación ni un subproceso del controlador. Si el controlador usa cierta información asociada al subproceso (por ejemplo, identificador de seguridad token o usuario), el controlador debe guardar la información necesaria en la llamada asincrónica inicial y usar el valor guardado antes de la operación completa asincrónica se completa. Por lo general, sólo **SQLDriverConnect**, **SQLConnect**, o **SQLBrowseConnect** debe usar ese tipo de información.  
  
## <a name="see-also"></a>Vea también  
 [Desarrollar un controlador ODBC](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)
