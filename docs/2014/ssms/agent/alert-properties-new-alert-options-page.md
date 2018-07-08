---
title: 'Propiedades de alerta: Nueva alerta (página Opciones) | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.ag.alert.options.f1
ms.assetid: 6e4f41aa-832d-46ba-b6b5-cf1d3b15d33f
caps.latest.revision: 18
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: b6e9cc28520099d9e3e3fad059a58e487b35859f
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37151796"
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
  
  
