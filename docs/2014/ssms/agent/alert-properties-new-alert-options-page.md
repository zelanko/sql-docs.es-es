---
title: 'Propiedades de alerta: Nueva alerta (página Opciones) | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
f1_keywords:
- sql12.ag.alert.options.f1
ms.assetid: 6e4f41aa-832d-46ba-b6b5-cf1d3b15d33f
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 59e5ac1f951ce897b058d224701d1a6936bfa11f
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48173315"
---
# <a name="alert-properties-new-alert-options-page"></a>Propiedades de alerta: Nueva alerta (página Opciones)
  Utilice esta página para ver y cambiar las opciones de las alertas del Agente [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="options"></a>Opciones  
 **Correo electrónico**  
 Incluye el texto de error del evento, si existe alguno, en las notificaciones de correo electrónico.  
  
 **Buscapersonas**  
 Incluye el texto de error del evento, si existe alguno, en las notificaciones de buscapersonas.  
  
 **NET SEND**  
 Incluye el texto de error del evento, si existe alguno, en las notificaciones de NET SEND.  
  
 **Mensaje adicional de notificación para enviar**  
 Escriba el texto adicional que se va a incluir en los mensajes de notificación.  
  
 **Retardo entre respuestas**  
 Especifique un retardo para las repeticiones del evento. Algunos eventos pueden producirse con frecuencia durante un breve período de tiempo. En este caso, es posible que desee saber que se ha producido el evento, pero sin necesidad de generar una respuesta para cada evento. Use esta opción para especificar un tiempo de espera. Con un retardo, después de que la alerta responde al evento, el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] espera el retardo especificado antes de responder de nuevo, independientemente de si el evento se produce durante el retardo.  
  
 **Minutos**  
 Especifique un retardo en minutos. Para responder cada vez que se produce el evento, especifique 0 minutos y 0 segundos.  
  
 **Segundos**  
 Especifique un retardo en segundos. Para responder cada vez que se produce el evento, especifique 0 minutos y 0 segundos.  
  
## <a name="see-also"></a>Vea también  
 [Alertas](alerts.md)  
  
  
