---
title: Control de eventos de ADO | Documentos de Microsoft
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- events [ADO]
- ADO, events
- event handlers [ADO]
ms.assetid: e9003457-0762-48b3-942f-0820266b158f
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b84df66d25c4e1ccda2330ccb1b0d02ff89dc20c
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="handling-ado-events"></a>Control de eventos de ADO
El modelo de eventos de ADO admite operaciones ciertas operaciones sincrónicas y asincrónicas de ADO que emiten *eventos*, o notificaciones, antes de iniciar la operación o después de que se complete. Un evento es realmente una llamada a una rutina de controlador de eventos que define en la aplicación.  
  
 Si proporciona procedimientos o funciones de controlador para el grupo de eventos que se producen antes de iniciar la operación, puede examinar o modificar los parámetros que se pasaron a la operación. Porque no se ha ejecutado todavía, puede cancelar la operación o permitir que se complete.  
  
 Los eventos que se producen cuando se complete una operación están especialmente importantes si utiliza ADO asincrónicamente. Por ejemplo, una aplicación que inicia una asincrónica [Recordset.Open](../../../ado/reference/ado-api/open-method-ado-recordset.md) operación recibe una notificación por un evento de finalización de ejecución cuando finaliza la operación.  
  
 Uso del modelo de eventos de ADO agrega cierta sobrecarga a la aplicación, pero proporciona mucha más flexibilidad que otros métodos de trabajar con operaciones asincrónicas, como la supervisión del [estado](../../../ado/reference/ado-api/state-property-ado.md) propiedad de un objeto con un bucle.  
  
> [!NOTE]
>  Para controlar eventos, ADO debe tener una bomba de mensaje o pueden utilizar en un modelo de contenedor uniproceso (STA). Eventos de ADO internamente se controlan mediante la creación de una ventana oculta. ADO envía mensajes a esta ventana cuando necesitan eventos que se deben activar. Esto se hace para asegurarse de que los eventos se envían al subproceso que llamó a **IConnectionPoint:: Advise** en el punto de conexión. Esta arquitectura puede causar problemas cuando el subproceso que debe recibir las notificaciones no extrae los mensajes de ventana. Posibles problemas incluyen eventos de ADO no se entregan a los subprocesos y las difusiones tiempo de espera agotado y posiblemente ralentizar todo el sistema, porque las ventanas ocultas no procesan los mensajes de ventana global. Los subprocesos STA tienen normalmente una bomba de mensaje que se ejecuta para que este problema no manifestarse en subprocesos STA. Subprocesos MTA, sin embargo, no tiene normalmente una bomba de mensaje para que el problema normalmente se manifestará en subprocesos MTA.  
  
 Esta sección contiene los temas siguientes.  
  
-   [Conexión ADO y los eventos de conjunto de registros](../../../ado/guide/data/ado-event-handler-summary.md)  
  
-   [Tipos de eventos](../../../ado/guide/data/types-of-events.md)  
  
-   [Parámetros de eventos](../../../ado/guide/data/event-parameters.md)  
  
-   [Cómo funcionan conjuntamente los controladores de eventos](../../../ado/guide/data/how-event-handlers-work-together.md)  
  
-   [Creación de instancias de eventos de ADO según el lenguaje](../../../ado/guide/data/ado-event-instantiation-by-language.md)  
  
## <a name="see-also"></a>Vea también  
 [Resumen del controlador de eventos de ADO](../../../ado/guide/data/ado-event-handler-summary.md)   
 [Creación de instancias de eventos de ADO según el lenguaje](../../../ado/guide/data/ado-event-instantiation-by-language.md)   
 [Eventos de ADO](../../../ado/reference/ado-api/ado-events.md)   
 [Parámetros de eventos](../../../ado/guide/data/event-parameters.md)   
 [Tipos de eventos](../../../ado/guide/data/types-of-events.md)
