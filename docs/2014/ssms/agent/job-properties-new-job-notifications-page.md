---
title: 'Propiedades del trabajo: Nuevo trabajo (página notificaciones) | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql12.ag.job.notifications.f1
ms.assetid: ed393cbd-4496-4399-a177-e5baa92fb689
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 10cee6f0d5bf62178c71d25b8eb5682c22bbbe3b
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/03/2018
ms.locfileid: "52797696"
---
# <a name="job-properties-new-job-notifications-page"></a>Propiedades del trabajo: Nuevo trabajo (página notificaciones)
  Use esta página para establecer acciones que el Agente [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] debe realizar cuando finalice el trabajo.  
  
## <a name="options"></a>Opciones  
 **Correo electrónico**  
 Seleccione esta opción para enviar correo electrónico cuando el trabajo finalice. Después de seleccionar esta opción, elija el operador para notificar y la condición que activará la notificación: **Si el trabajo tiene éxito**; **Cuando se produce un error en el trabajo**; o **cuando se completa el trabajo**.  
  
 **Página**  
 Seleccione esta opción para enviar correo electrónico al buscapersonas de un operador cuando el trabajo finalice. Después de seleccionar esta opción, especifique el operador para notificar y la condición que activará la notificación: **Si el trabajo tiene éxito**; **Cuando se produce un error en el trabajo**; o **cuando se completa el trabajo**.  
  
 **NET SEND**  
 Seleccione esta opción para utilizar NET SEND para avisar a un operador cuando el trabajo finalice. Después de seleccionar esta opción, especifique el operador para notificar y la condición que activará la notificación: **Si el trabajo tiene éxito**; **Cuando se produce un error en el trabajo**; o **cuando se completa el trabajo**.  
  
 **Escribir en el registro de eventos de aplicación Windows**  
 Seleccione esta opción para escribir una entrada en el registro de eventos de la aplicación cuando el trabajo finalice. Después de seleccionar esta opción, especifique la condición que hará que la entrada que se va a escribirse: **Si el trabajo tiene éxito**; **Cuando se produce un error en el trabajo**; o **cuando se completa el trabajo**.  
  
 **Eliminar automáticamente el trabajo**  
 Seleccione esta opción para eliminar el trabajo cuando éste finalice. Después de seleccionar esta opción, especifique la condición que activará la eliminación del trabajo: **Si el trabajo tiene éxito**; **Cuando se produce un error en el trabajo**; o **cuando se completa el trabajo**.  
  
## <a name="see-also"></a>Vea también  
 [Implementar trabajos](implement-jobs.md)   
 [Configurar el Agente SQL Server para que use el Correo electrónico de base de datos](../../relational-databases/database-mail/configure-sql-server-agent-mail-to-use-database-mail.md)  
  
  
