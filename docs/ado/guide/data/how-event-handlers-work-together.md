---
title: "Cómo funcionan conjuntamente los controladores de eventos | Documentos de Microsoft"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- events [ADO], about event handlers
- unpaired event handlers [ADO]
- paired event handlers [ADO]
- single event handlers [ADO]
- event handlers [ADO]
- multiple object event handlers [ADO]
ms.assetid: a86c8a02-dd69-420d-8a47-0188b339858d
caps.latest.revision: "10"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 72ca437ae2d78395632abd06169feb2b41d4fc50
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="how-event-handlers-work-together"></a>Cómo funcionan conjuntamente los controladores de eventos
A menos que está programando en Visual Basic, todos los controladores de eventos para **conexión** y **Recordset** eventos deben estar implementados, independientemente de que procesen realmente todos los eventos. La cantidad de trabajo de implementación que tiene que hacer depende de su lenguaje de programación. Para obtener más información, consulte [creación de instancias de eventos de ADO según el lenguaje](../../../ado/guide/data/ado-event-instantiation-by-language.md).  
  
## <a name="paired-event-handlers"></a>Controladores de eventos emparejados  
 Cada controlador de eventos Will tiene asociado un **completar** controlador de eventos. Por ejemplo, cuando la aplicación cambia el valor de un campo, el **WillChangeField** se llama al controlador de eventos. Si el cambio es aceptable, la aplicación deja la **adStatus** parámetro sin modificar y se realiza la operación. Cuando se complete la operación, un **FieldChangeComplete** evento notifica a la aplicación que haya finalizado la operación. Si se ha completado correctamente, **adStatus** contiene **adStatusOK**; en caso contrario, **adStatus** contiene **adStatusErrorsOccurred** y debe comprobar la **Error** para determinar la causa del error.  
  
 Cuando **WillChangeField** es llama, podría determinar que no se debe realizar el cambio. En ese caso, establezca **adStatus** a **adStatusCancel.** Se cancela la operación y el **FieldChangeComplete** evento recibe un **adStatus** valo **adStatusErrorsOccurred**. El **Error** objeto contiene **adErrOperationCancelled** para que su **FieldChangeComplete** controlador sepa que se canceló la operación. Sin embargo, debe comprobar el valor de la **adStatus** parámetro antes de cambiarlo, dado que al establecer **adStatus** a **adStatusCancel** no tiene ningún efecto si se ha establecido el parámetro para **adStatusCantDeny** en la entrada al procedimiento.  
  
 A veces, una operación puede generar más de un evento. Por ejemplo, el **Recordset** objeto tiene eventos para emparejados **campo** cambios y **registro** cambios. Cuando la aplicación cambia el valor de un **campo**, **WillChangeField** se llama al controlador de eventos. Si se determina que la operación puede continuar, la **WillChangeRecord** también se genera el controlador de eventos. Si este controlador permite asimismo que continúe el evento, se realiza el cambio y la **FieldChangeComplete** y **RecordChangeComplete** se denominan controladores de eventos. No se define el orden en el que se llama a los controladores de eventos Will para una operación determinada, por lo que debe evitar escribir código que depende de una llamada a los controladores en un orden determinado.  
  
 En instancias cuando se producen varios eventos Will, uno de los eventos puede cancelar la operación pendiente. Por ejemplo, cuando la aplicación cambia el valor de un **campo**, ambos **WillChangeField** y **WillChangeRecord** normalmente se llamaría controladores de eventos. Sin embargo, si se cancela la operación en el primer controlador de eventos, sus asociado **completar** controlador se llama inmediatamente con **adStatusOperationCancelled**. Nunca se llama al controlador de segundo. Si, sin embargo, el primer controlador de eventos permite que continúe el evento, se llamará al otro controlador de eventos. Si, a continuación, cancela la operación, ambos **completar** eventos se les llama como en los ejemplos anteriores.  
  
## <a name="unpaired-event-handlers"></a>Controladores de eventos no emparejados  
 Siempre y cuando el estado pasado para el evento no es **adStatusCantDeny**, puede desactivar las notificaciones de eventos para cualquier evento devolviendo **adStatusUnwantedEvent** en el *estado*parámetro. Por ejemplo, cuando la **completar** controlador de eventos se llama por primera vez, puede devolver **adStatusUnwantedEvent**. Posteriormente, recibirá sólo **le** eventos. Sin embargo, algunos eventos pueden activarse por más de un motivo. En ese caso, el evento tendrá un *motivo* parámetro. Cuando vuelva **adStatusUnwantedEvent**, dejará de recibir notificaciones de ese evento sólo cuando se producen por ese motivo concreto. En otras palabras, potencialmente recibirá notificación para todas las posibles razones que podría activarse el evento.  
  
 Solo **le** controladores de eventos pueden ser útiles cuando desea examinar los parámetros que se utilizarán en una operación. Puede modificar esos parámetros de operación o cancelar la operación.  
  
 O bien, deje **completar** habilitada la notificación de eventos. Cuando se llame al primer controlador de eventos Will, devuelva **adStatusUnwantedEvent**. Posteriormente, recibirá sólo **completar** eventos.  
  
 Solo **completar** controladores de eventos pueden ser útiles para administrar las operaciones asincrónicas. Cada operación asincrónica tiene una adecuada **completar** eventos.  
  
 Por ejemplo, puede tardar mucho tiempo para rellenar una gran [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) objeto. Si la aplicación está escrita correctamente, puede iniciar un `Recordset.Open(...,adAsyncExecute)` operación y continuar con otros procesos. Finalmente estará le avisa cuando el **Recordset** se rellena con un **ExecuteComplete** eventos.  
  
## <a name="single-event-handlers-and-multiple-objects"></a>Controladores de eventos único y varios objetos  
 La flexibilidad de un lenguaje de programación como Microsoft Visual C++® le permite tener una eventos del proceso de controlador de eventos de varios objetos. Por ejemplo, podría tener una **desconexión** eventos del proceso de controlador de eventos desde varios **conexión** objetos. Si una de las conexiones finaliza, el **desconexión** se llamará al controlador de eventos. Puede indicar a qué conexión provocó el evento porque el parámetro de objeto de controlador de eventos se establecería en correspondiente **conexión** objeto.  
  
> [!NOTE]
>  Esta técnica no se puede usar en Visual Basic porque ese idioma puede poner en correlación sólo un objeto a un controlador de eventos.  
  
## <a name="see-also"></a>Vea también  
 [Resumen del controlador de eventos de ADO](../../../ado/guide/data/ado-event-handler-summary.md)   
 [Creación de instancias de eventos de ADO según el lenguaje](../../../ado/guide/data/ado-event-instantiation-by-language.md)   
 [Parámetros de eventos](../../../ado/guide/data/event-parameters.md)   
 [Tipos de eventos](../../../ado/guide/data/types-of-events.md)
