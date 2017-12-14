---
title: "Propiedades del trabajo: Nuevo trabajo (página Notificaciones) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: ssms-agent
ms.reviewer: 
ms.suite: sql
ms.technology: tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.ag.job.notifications.f1
ms.assetid: ed393cbd-4496-4399-a177-e5baa92fb689
caps.latest.revision: "5"
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 41a11afd5d7f85c087198069311b033ad5a6116f
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/05/2017
---
# <a name="job-properties---new-job-notifications-page"></a>Propiedades del trabajo - Nuevo trabajo (página Notificaciones)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Use esta página para establecer acciones que el Agente [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] debe realizar cuando finalice el trabajo.  
  
## <a name="options"></a>Opciones  
**Correo electrónico**  
Seleccione esta opción para enviar correo electrónico cuando el trabajo finalice. Después de seleccionar esta opción, elija el operador al que se va a notificar y la condición que activará la notificación: **Si el trabajo tiene éxito**; **Si el trabajo no tiene éxito**; o **Si el trabajo termina**.  
  
**Página**  
Seleccione esta opción para enviar correo electrónico al buscapersonas de un operador cuando el trabajo finalice. Después de seleccionar esta opción, especifique el operador al que se va a notificar y la condición que activará la notificación: **Si el trabajo tiene éxito**; **Si el trabajo no tiene éxito**; o **Si el trabajo termina**.  
  
**NET SEND**  
Seleccione esta opción para utilizar NET SEND para avisar a un operador cuando el trabajo finalice. Después de seleccionar esta opción, especifique el operador al que se va a notificar y la condición que activará la notificación: **Si el trabajo tiene éxito**; **Si el trabajo no tiene éxito**; o **Si el trabajo termina**.  
  
**Escribir en el registro de eventos de aplicación Windows**  
Seleccione esta opción para escribir una entrada en el registro de eventos de la aplicación cuando el trabajo finalice. Después de seleccionar esta opción, especifique la condición que hará que se escriba la entrada: **Si el trabajo tiene éxito**; **Si el trabajo no tiene éxito**; o **Si el trabajo termina**.  
  
**Eliminar automáticamente el trabajo**  
Seleccione esta opción para eliminar el trabajo cuando éste finalice. Después de seleccionar esta opción, especifique la condición que activará la eliminación del trabajo: **Si el trabajo tiene éxito**; **Si el trabajo no tiene éxito**; o **Si el trabajo termina**.  
  
## <a name="see-also"></a>Vea también  
[Implementar trabajos](../../ssms/agent/implement-jobs.md)  
[Cómo configurar el correo del Agente SQL Server para que utilice el Correo electrónico de base de datos (SQL Server Management Studio)](http://msdn.microsoft.com/en-us/4b8b61bd-4bd1-43cd-b6e5-c6ed2e101dce)  
  
