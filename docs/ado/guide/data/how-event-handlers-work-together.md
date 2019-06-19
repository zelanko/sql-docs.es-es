---
title: Cómo funcionan conjuntamente los controladores de eventos | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- events [ADO], about event handlers
- unpaired event handlers [ADO]
- paired event handlers [ADO]
- single event handlers [ADO]
- event handlers [ADO]
- multiple object event handlers [ADO]
ms.assetid: a86c8a02-dd69-420d-8a47-0188b339858d
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: cb02a96e6ee3d28c67e21996677c02b58fc97c07
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66718389"
---
# <a name="how-event-handlers-work-together"></a>Cómo funcionan conjuntamente los controladores de eventos
A menos que se está programando en Visual Basic, todos los controladores de eventos para **conexión** y **Recordset** deben implementarse los eventos, independientemente de procese realmente todos los eventos. La cantidad de trabajo de implementación que debe hacer depende del lenguaje de programación. Para obtener más información, consulte [creación de instancias de eventos de ADO por lenguaje](../../../ado/guide/data/ado-event-instantiation-by-language.md).  
  
## <a name="paired-event-handlers"></a>Controladores de eventos emparejados  
 Cada controlador de eventos Will tiene asociado un **completar** controlador de eventos. Por ejemplo, cuando la aplicación cambia el valor de un campo, el **WillChangeField** se llama al controlador de eventos. Si el cambio es aceptable, la aplicación deja el **adStatus** parámetro sin modificar y se realiza la operación. Cuando se complete la operación, un **FieldChangeComplete** evento notifica a la aplicación que ha finalizado la operación. Si se ha completado correctamente, **adStatus** contiene **adStatusOK**; en caso contrario, **adStatus** contiene **adStatusErrorsOccurred** y debe comprobar la **Error** para determinar la causa del error.  
  
 Cuando **WillChangeField** es llamado, puede determinar que no se debe realizar el cambio. En ese caso, establezca **adStatus** a **adStatusCancel.** Se cancela la operación y el **FieldChangeComplete** evento recibe un **adStatus** valor **adStatusErrorsOccurred**. El **Error** contiene el objeto **adErrOperationCancelled** para que su **FieldChangeComplete** controlador sabe que se ha cancelado la operación. Sin embargo, deberá comprobar el valor de la **adStatus** parámetro antes de cambiarlo, porque si se establece **adStatus** a **adStatusCancel** no tiene ningún efecto si se ha establecido el parámetro para **adStatusCantDeny** en la entrada al procedimiento.  
  
 A veces, una operación puede generar más de un evento. Por ejemplo, el **Recordset** objeto tiene eventos para emparejados **campo** cambios y **registro** cambios. Cuando la aplicación cambia el valor de un **campo**, **WillChangeField** se llama al controlador de eventos. Si determina que la operación pueda continuar, el **WillChangeRecord** también se genera el controlador de eventos. Si este controlador también permite que continúe el evento, se realiza el cambio y la **FieldChangeComplete** y **RecordChangeComplete** se denominan controladores de eventos. No se define el orden en el que se llama a los controladores de eventos Will para una operación determinada, por lo que debe evitar escribir código que depende de una llamada a los controladores en una secuencia determinada.  
  
 En las instancias cuando se producen varios eventos Will, uno de los eventos puede cancelar la operación pendiente. Por ejemplo, cuando la aplicación cambia el valor de un **campo**, ambos **WillChangeField** y **WillChangeRecord** controladores de eventos normalmente se llama. Sin embargo, si se cancela la operación en el primer controlador de eventos, su asociado **completar** controlador se llama inmediatamente con **adStatusOperationCancelled**. Nunca se llama al controlador de segundo. Si, sin embargo, el primer controlador de eventos permite que continúe el evento, se llamará el otro controlador de eventos. Si cancela la operación, ambos **completar** se llamará a eventos como en los ejemplos anteriores.  
  
## <a name="unpaired-event-handlers"></a>Controladores de eventos no emparejados  
 Siempre y cuando el estado correcto para el evento no es **adStatusCantDeny**, puede desactivar las notificaciones de eventos para cualquier evento devolviendo **adStatusUnwantedEvent** en el *estado*parámetro. Por ejemplo, cuando su **completar** controlador de eventos se llama a la primera vez, puede devolver **adStatusUnwantedEvent**. Posteriormente, recibirá solo **le** eventos. Sin embargo, algunos eventos pueden desencadenarse por más de un motivo. En ese caso, el evento tendrá un *motivo* parámetro. Cuando vuelva **adStatusUnwantedEvent**, dejará de recibir notificaciones de ese evento sólo cuando se producen por ese motivo concreto. En otras palabras, potencialmente recibirá notificación para todas las posibles razones que podría activarse el evento.  
  
 Solo **le** controladores de eventos pueden ser útiles cuando desea examinar los parámetros que se usará en una operación. Puede modificar los parámetros de operación o cancelar la operación.  
  
 Como alternativa, dejar **completar** habilitada la notificación de eventos. Cuando se llama al primer controlador de eventos Will, devolver **adStatusUnwantedEvent**. Posteriormente, recibirá solo **completar** eventos.  
  
 Solo **completar** controladores de eventos pueden ser útiles para administrar las operaciones asincrónicas. Cada operación asincrónica tiene un adecuado **completar** eventos.  
  
 Por ejemplo, puede tardar mucho tiempo en rellenar un gran [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) objeto. Si la aplicación está escrita correctamente, puede iniciar un `Recordset.Open(...,adAsyncExecute)` operación y continuar con otros procesamientos. Finalmente estará le avisa cuando el **Recordset** se rellena con un **ExecuteComplete** eventos.  
  
## <a name="single-event-handlers-and-multiple-objects"></a>Controladores de eventos único y varios objetos  
 La flexibilidad de un lenguaje de programación como Microsoft Visual C++® permite que un evento controlador procesar los eventos de varios objetos. Por ejemplo, podría tener **desconexión** procesar eventos de controlador de eventos desde varios **conexión** objetos. Si una de las conexiones ha finalizado, el **desconexión** se llamará al controlador de eventos. Puede indicar a qué conexión provocó el evento porque el parámetro de objeto de controlador de eventos se establecería en el correspondiente **conexión** objeto.  
  
> [!NOTE]
>  Esta técnica no se puede usar en Visual Basic porque ese idioma puede poner en correlación un solo objeto a un controlador de eventos.  
  
## <a name="see-also"></a>Vea también  
 [Resumen del controlador de eventos de ADO](../../../ado/guide/data/ado-event-handler-summary.md)   
 [Creación de instancias de eventos de ADO por idioma](../../../ado/guide/data/ado-event-instantiation-by-language.md)   
 [Parámetros de evento](../../../ado/guide/data/event-parameters.md)   
 [Tipos de eventos](../../../ado/guide/data/types-of-events.md)
