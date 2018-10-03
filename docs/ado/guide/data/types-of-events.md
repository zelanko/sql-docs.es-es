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
ms.openlocfilehash: b324857816df774486716978425d1332a695952a
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47708473"
---
# <a name="types-of-events"></a>Tipos de eventos
Hay dos tipos básicos de eventos. "Eventos will", que se llama antes de iniciarse una operación, normalmente incluyen "Le" en sus nombres, por ejemplo, **WillChangeRecordset** o **WillConnect**. Los eventos que se invocan después de un evento se ha completado normalmente incluyen "Completa" en sus nombres, por ejemplo, **RecordChangeComplete** o **ConnectComplete**. Existen excepciones, como **InfoMessage** , pero estas se producen una vez completada la operación asociada.  
  
## <a name="will-events"></a>Eventos Will  
 Controladores de eventos se llama antes de que se inicie la operación ofrece la oportunidad de examinar o modificar los parámetros de operación y, a continuación, cancelar la operación o permitir que se complete. Estas rutinas de controlador de eventos suelen tienen nombres de la forma **le*evento ***.  
  
## <a name="complete-events"></a>Eventos de finalización  
 Se llama después de completarse una operación de controladores de eventos pueden notificar a la aplicación que una operación ha concluido. Estos controladores de eventos también es una notificación cuando un controlador de eventos Will cancela una operación pendiente. Estas rutinas de controlador de eventos suelen tienen nombres de la forma ***eventos * completar**.  
  
 La usará y eventos de finalización normalmente se usan en pares.  
  
## <a name="other-events"></a>Otros eventos  
 Otros controladores de eventos, es decir, los eventos cuyos nombres no tienen el formato **le * eventos*** o ***eventos * completar** : se invocan después de que se completa una operación. Estos eventos son **desconexión**, **EndOfRecordset**, y **InfoMessage**.  
  
## <a name="see-also"></a>Vea también  
 [Resumen del controlador de eventos de ADO](../../../ado/guide/data/ado-event-handler-summary.md)   
 [Creación de instancias de eventos de ADO por idioma](../../../ado/guide/data/ado-event-instantiation-by-language.md)   
 [Parámetros de evento](../../../ado/guide/data/event-parameters.md)   
 [Cómo funcionan conjuntamente los controladores de eventos](../../../ado/guide/data/how-event-handlers-work-together.md)
