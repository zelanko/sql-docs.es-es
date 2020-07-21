---
title: 'Propiedades de alerta: nueva alerta (página Opciones) | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql12.ag.alert.options.f1
ms.assetid: 6e4f41aa-832d-46ba-b6b5-cf1d3b15d33f
author: stevestein
ms.author: sstein
ms.openlocfilehash: b84c2472c56d50fa5c0595ea7046ed3ab9a2b352
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85056596"
---
# <a name="alert-properties-new-alert-options-page"></a>Propiedades de la alerta: Nueva alerta (página Opciones)
  Utilice esta página para ver y modificar las opciones de las [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] alertas del agente.  
  
## <a name="options"></a>Opciones  
 **Por**  
 Incluye el texto de error del evento, si existe alguno, en las notificaciones de correo electrónico.  
  
 **Buscapersonas**  
 Incluye el texto de error del evento, si existe alguno, en las notificaciones de buscapersonas.  
  
 **Net send**  
 Incluye el texto de error del evento, si existe alguno, en las notificaciones de NET SEND.  
  
 **Mensaje adicional de notificación para enviar**  
 Escriba el texto adicional que se va a incluir en los mensajes de notificación.  
  
 **Retardo entre respuestas**  
 Especifique un retardo para las repeticiones del evento. Algunos eventos pueden producirse con frecuencia durante un breve período de tiempo. En este caso, es posible que desee saber que se ha producido el evento, pero sin necesidad de generar una respuesta para cada evento. Utilice esta opción para especificar un tiempo de espera. Con un retraso, después de que la alerta responda a un evento, el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] agente espera el retraso especificado antes de responder de nuevo, independientemente de si el evento se produce durante el retraso.  
  
 **Tiempo**  
 Especifique un retardo en minutos. Para responder cada vez que se produce el evento, especifique 0 minutos y 0 segundos.  
  
 **S**  
 Especifique un retardo en segundos. Para responder cada vez que se produce el evento, especifique 0 minutos y 0 segundos.  
  
## <a name="see-also"></a>Consulte también  
 [Alertas](alerts.md)  
  
  
