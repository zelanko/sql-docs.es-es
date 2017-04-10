---
title: "Difundir un mensaje de cierre del sistema (s&#237;mbolo del sistema) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "SQL Server, detener"
  - "instancias con nombre [SQL Server], difundir mensajes de cierre"
  - "difusión de mensaje de cierre de sistema"
  - "difundir mensaje de cierre de sistema"
  - "símbolo del sistema [SQL Server], difundir mensajes de cierre"
  - "instancias predeterminadas [SQL Server], difundir mensajes de cierre"
  - "detener SQL Server"
ms.assetid: 9f20ccd5-d952-431d-ba12-339911af9430
caps.latest.revision: 28
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 28
---
# Difundir un mensaje de cierre del sistema (s&#237;mbolo del sistema)
  En este tema se describe cómo difundir un mensaje de cierre en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante el comando **net send** . En el mensaje, incluya la hora a la que se va a detener la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para que los usuarios puedan finalizar sus tareas.  
  
##  <a name="SSMSProcedure"></a>  
  
#### Para difundir un mensaje de cierre  
  
1.  Desde el símbolo del sistema, escriba:  
  
     **net send /users "message"**  
  
     La opción **/users** especifica que el mensaje se enviará a todos los usuarios conectados al servidor  
  
> [!NOTE]  
>  El comando **net send** requiere que se esté ejecutando el servicio de mensajería tanto en el equipo emisor como en el receptor. El servicio de mensajería se deshabilita de forma predeterminada en Windows Server 2003. Para obtener información sobre **net send**, vea la documentación de Windows.  
  
 Es posible que en su red sea más conveniente ponerse en contacto con los usuarios por correo electrónico o teléfono. Para determinar qué usuarios están conectados actualmente a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], utilice el Monitor de actividad. Para obtener información sobre el Monitor de actividad, vea [Monitor de actividad](../../relational-databases/performance-monitor/activity-monitor.md) y [Abrir el Monitor de actividad &#40;SQL Server Management Studio&#41;](../../relational-databases/performance-monitor/open-activity-monitor-sql-server-management-studio.md).  
  
## Vea también  
 [Iniciar, detener, pausar, reanudar y reiniciar el motor de base de datos, Agente SQL Server o el Servicio SQL Server Browser](../../database-engine/configure-windows/start, stop, pause, resume, restart sql server services.md)  
  
  