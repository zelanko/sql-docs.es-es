---
title: Control de eventos de ADO | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- events [ADO]
- ADO, events
- event handlers [ADO]
ms.assetid: e9003457-0762-48b3-942f-0820266b158f
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 162cac52920b076e4388a74a251cd347137f49cd
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/05/2019
ms.locfileid: "66702005"
---
# <a name="handling-ado-events"></a>Control de eventos de ADO
El modelo de eventos de ADO admite determinadas operaciones sincrónicas y asincrónicas de ADO que emiten *eventos*, o notificaciones, antes de iniciar la operación o después de que se complete. Un evento es realmente una llamada a una rutina de controlador de eventos que define en la aplicación.  
  
 Si proporciona procedimientos o funciones de controlador para el grupo de eventos que se producen antes de iniciar la operación, puede examinar o modificar los parámetros que se pasaron a la operación. Dado que no se ha ejecutado todavía, puede cancelar la operación o permitir que se complete.  
  
 Los eventos que se producen después de que se completa una operación están especialmente importantes si utiliza ADO asincrónicamente. Por ejemplo, una aplicación que inicia asincrónico [Recordset.Open](../../../ado/reference/ado-api/open-method-ado-recordset.md) operación se le notifica mediante un evento de finalización de ejecución cuando finaliza la operación.  
  
 Uso del modelo de eventos de ADO agrega cierta sobrecarga a la aplicación, pero proporciona mucha más flexibilidad que otros métodos para trabajar con operaciones asincrónicas, como la supervisión del [estado](../../../ado/reference/ado-api/state-property-ado.md) propiedad de un objeto con un bucle.  
  
> [!NOTE]
>  Para controlar los eventos, ADO debe tener un bombeo de mensajes o utilizarse en un modelo de contenedor uniproceso (STA). Eventos de ADO internamente se controlan mediante la creación de una ventana oculta. ADO envía mensajes a esta ventana cuando los eventos se deben activarse. Esto se hace para garantizar que los eventos se envían al subproceso que llama **IConnectionPoint:: Advise** en el punto de conexión. Esta arquitectura puede causar problemas cuando el subproceso que debe recibir las notificaciones no extrae los mensajes de ventana. Posibles problemas incluyen eventos de ADO no se entregan a los subprocesos y las difusiones de tiempo de espera y, posiblemente, lo que ralentizaría todo el sistema porque windows ocultos no procesan los mensajes de ventana global. Subprocesos STA suelen tengan un bombeo de mensajes que se ejecuta, por lo que este problema no manifestarse en subprocesos STA. Subprocesos MTA, sin embargo, no suelen tener un bombeo de mensajes por lo que el problema se manifiesta por lo general en subprocesos MTA.  
  
 Esta sección contiene los temas siguientes.  
  
-   [Conexión ADO y los eventos de conjunto de registros](../../../ado/guide/data/ado-event-handler-summary.md)  
  
-   [Tipos de eventos](../../../ado/guide/data/types-of-events.md)  
  
-   [Parámetros de eventos](../../../ado/guide/data/event-parameters.md)  
  
-   [Cómo funcionan conjuntamente los controladores de eventos](../../../ado/guide/data/how-event-handlers-work-together.md)  
  
-   [Creación de instancias de eventos de ADO según el lenguaje](../../../ado/guide/data/ado-event-instantiation-by-language.md)  
  
## <a name="see-also"></a>Vea también  
 [Resumen del controlador de eventos de ADO](../../../ado/guide/data/ado-event-handler-summary.md)   
 [Creación de instancias de eventos de ADO por idioma](../../../ado/guide/data/ado-event-instantiation-by-language.md)   
 [Eventos de ADO](../../../ado/reference/ado-api/ado-events.md)   
 [Parámetros de evento](../../../ado/guide/data/event-parameters.md)   
 [Tipos de eventos](../../../ado/guide/data/types-of-events.md)
