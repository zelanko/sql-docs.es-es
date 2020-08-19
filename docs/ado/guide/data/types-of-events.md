---
description: Tipos de eventos
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 3fa59b0faeb5b1c74ccd4dff3f9d3c274a8f12c6
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88452687"
---
# <a name="types-of-events"></a>Tipos de eventos
Hay dos tipos básicos de eventos. "Eventos hechos", a los que se llama antes de que se inicie una operación, normalmente incluyen "va" en sus nombres, por ejemplo, **WillChangeRecordset** o **WillConnect**. Los eventos a los que se llama después de que se haya completado un evento suelen incluir "Complete" en sus nombres (por ejemplo, **RecordChangeComplete** o **ConnectComplete**). Existen excepciones, como **InfoMessage** , pero se producen una vez completada la operación asociada.  
  
## <a name="will-events"></a>Eventos de eventos  
 Los controladores de eventos a los que se llama antes de que se inicie la operación le ofrecen la oportunidad de examinar o modificar los parámetros de la operación y, a continuación, cancelar la operación o permitir que se complete. Estas rutinas de controlador de eventos suelen tener nombres del formulario <strong>*Events*</strong>.  
  
## <a name="complete-events"></a>Completar eventos  
 Los controladores de eventos a los que se llama después de que se complete una operación pueden notificar a la aplicación que ha finalizado una operación. Este controlador de eventos también recibe una notificación cuando un controlador de eventos cancela una operación pendiente. Estas rutinas de controlador de eventos suelen tener nombres con el <strong> *evento*</strong>de formulario completo.  
  
 Los eventos rellenados y completos se suelen usar en parejas.  
  
## <a name="other-events"></a>Otros eventos  
 Los otros controladores de eventos, es decir, los eventos cuyos nombres no tienen el formato <strong>serán*evento* </strong> o <strong> *evento*completado</strong> : solo se llaman después de que se complete una operación. Estos eventos son **Disconnect**, **EndOfRecordset**e **InfoMessage**.  
  
## <a name="see-also"></a>Consulte también  
 [Resumen del controlador de eventos de ADO](../../../ado/guide/data/ado-event-handler-summary.md)   
 [Creación de instancias de eventos de ADO por lenguaje](../../../ado/guide/data/ado-event-instantiation-by-language.md)   
 [Parámetros de evento](../../../ado/guide/data/event-parameters.md)   
 [Cómo funcionan conjuntamente los controladores de eventos](../../../ado/guide/data/how-event-handlers-work-together.md)
