---
title: Tipos de eventos | Documentos de Microsoft
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- EventComplete event [ADO]
- events [ADO], types
- Will events [ADO]
- complete events [ADO]
- WillEvent event [ADO]
ms.assetid: f3327ea0-635a-43d4-bd78-c1674f62f1a2
caps.latest.revision: "9"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: f33ed98f367560da7f4b60d5a754d99937319358
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="types-of-events"></a>Tipos de eventos
Hay dos tipos básicos de eventos. "Eventos will", que se llama antes de que comience una operación, normalmente incluyen "Will" en sus nombres, por ejemplo, **WillChangeRecordset** o **WillConnect**. Los eventos que se llaman una vez completado un evento normalmente incluyen "Complete" en sus nombres, por ejemplo, **RecordChangeComplete** o **ConnectComplete**. Existen excepciones, como **InfoMessage** , pero éstas se producen una vez completada la operación asociada.  
  
## <a name="will-events"></a>Eventos Will  
 Controladores de eventos llama antes de iniciar la operación ofrecerle la oportunidad de examinar o modificar los parámetros de operación y, a continuación, cancelar la operación o permitir que se complete. Estas rutinas de controlador de eventos normalmente tienen nombres de la forma  **le*eventos***.  
  
## <a name="complete-events"></a>Eventos Complete  
 Controladores de eventos que se llama cuando se complete una operación pueden notificar a la aplicación que ha finalizado una operación. Un controlador de eventos de este tipo también recibe una notificación cuando un controlador de eventos Will cancela una operación pendiente. Estas rutinas de controlador de eventos normalmente tienen nombres de la forma  ***eventos*completar**.  
  
 Eventos Will y Complete normalmente se utilizan en pares.  
  
## <a name="other-events"></a>Otros eventos  
 Los otros controladores de eventos, es decir, los eventos cuyo nombre no tiene el formato  **le*eventos*** o  ***eventos*completar** : se denominan solo Cuando se complete una operación. Estos eventos son **desconexión**, **EndOfRecordset**, y **InfoMessage**.  
  
## <a name="see-also"></a>Vea también  
 [Resumen del controlador de eventos de ADO](../../../ado/guide/data/ado-event-handler-summary.md)   
 [Creación de instancias de eventos de ADO según el lenguaje](../../../ado/guide/data/ado-event-instantiation-by-language.md)   
 [Parámetros de eventos](../../../ado/guide/data/event-parameters.md)   
 [Cómo funcionan conjuntamente los controladores de eventos](../../../ado/guide/data/how-event-handlers-work-together.md)
