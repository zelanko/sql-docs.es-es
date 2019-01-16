---
title: Tipos de eventos | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- EventComplete event [ADO]
- events [ADO], types
- Will events [ADO]
- complete events [ADO]
- WillEvent event [ADO]
ms.assetid: f3327ea0-635a-43d4-bd78-c1674f62f1a2
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 78505f010706a39e5278d50219dd4504e33dd67c
ms.sourcegitcommit: bfa10c54e871700de285d7f819095d51ef70d997
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/14/2019
ms.locfileid: "54254870"
---
# <a name="types-of-events"></a>Tipos de eventos
Hay dos tipos básicos de eventos. "Eventos will", que se llama antes de iniciarse una operación, normalmente incluyen "Will" en sus nombres: por ejemplo, **WillChangeRecordset** o **WillConnect**. Los eventos que se invocan después de un evento se ha completado generalmente incluyen, por ejemplo, "Completado" en sus nombres - **RecordChangeComplete** o **ConnectComplete**. Existen excepciones - como **InfoMessage** - pero estas se producen una vez completada la operación asociada.  
  
## <a name="will-events"></a>Eventos Will  
 Controladores de eventos se llama antes de que se inicie la operación ofrece la oportunidad de examinar o modificar los parámetros de operación y, a continuación, cancelar la operación o permitir que se complete. Estas rutinas de controlador de eventos suelen tienen nombres de la forma <strong>le*eventos*</strong>.  
  
## <a name="complete-events"></a>Eventos de finalización  
 Se llama después de completarse una operación de controladores de eventos pueden notificar a la aplicación que una operación ha concluido. Estos controladores de eventos también es una notificación cuando un controlador de eventos Will cancela una operación pendiente. Estas rutinas de controlador de eventos suelen tienen nombres de la forma  <strong>*eventos*completar</strong>.  
  
 La usará y eventos de finalización normalmente se usan en pares.  
  
## <a name="other-events"></a>Otros eventos  
 Otros controladores de eventos: es decir, los eventos cuyos nombres no tienen el formato <strong>le*eventos*</strong>  o  <strong>*eventos*completar</strong> -se denominan solo después de finaliza una operación. Estos eventos son **desconexión**, **EndOfRecordset**, y **InfoMessage**.  
  
## <a name="see-also"></a>Vea también  
 [Resumen del controlador de eventos de ADO](../../../ado/guide/data/ado-event-handler-summary.md)   
 [Creación de instancias de eventos de ADO por idioma](../../../ado/guide/data/ado-event-instantiation-by-language.md)   
 [Parámetros de evento](../../../ado/guide/data/event-parameters.md)   
 [Cómo funcionan conjuntamente los controladores de eventos](../../../ado/guide/data/how-event-handlers-work-together.md)
