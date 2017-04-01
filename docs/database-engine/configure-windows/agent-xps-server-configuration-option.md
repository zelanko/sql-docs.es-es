---
title: "Agent XPs (opci&#243;n de configuraci&#243;n del servidor) | Microsoft Docs"
ms.custom: ""
ms.date: "03/02/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Agent XPs, opción"
  - "procedimientos almacenados extendidos [SQL Server], Agente SQL Server"
ms.assetid: 2e1c6c64-5ce7-4357-98c7-ac7763a9f9de
caps.latest.revision: 24
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 24
---
# Agent XPs (opci&#243;n de configuraci&#243;n del servidor)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  La opción **Agent XPs** habilita los procedimientos almacenados extendidos del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en este servidor. Cuando no está habilitada, el nodo del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no está disponible en el Explorador de objetos de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] .  
  
 Cuando utilice la herramienta [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para iniciar el servicio del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , estos procedimientos almacenados extendidos se habilitarán automáticamente. Para obtener más información, vea [Surface Area Configuration](../../relational-databases/security/surface-area-configuration.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] El Explorador de objetos no mostrará el contenido del nodo de Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a no ser que estos procedimientos almacenados extendidos estén habilitados, independientemente del estado del servicio del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Los valores posibles son:  
  
-   **0**, que indica que los procedimientos almacenados extendidos del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no están disponibles (valor predeterminado).  
  
-   **1**, que indica que los procedimientos almacenados extendidos del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] están disponibles.  
  
 La configuración surte efecto inmediatamente, sin necesidad de detener y reiniciar el servidor.  
  
## Ejemplo
 En el siguiente ejemplo se habilitan los procedimientos almacenados extendidos del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  

1. Conéctese al motor de base de datos desde Microsoft SQL Server Management Studio.

2.  En la barra Estándar, haga clic en **Nueva consulta**.

3.  Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**. 
  
```tsql 
sp_configure 'show advanced options', 1;  
GO  
RECONFIGURE;  
GO  
sp_configure 'Agent XPs', 1;  
GO  
RECONFIGURE  
GO  
```  
  
## Vea también  
 [Tareas administrativas automatizadas &#40;Agente SQL Server&#41;](../../ssms/agent/automated-administration-tasks-sql-server-agent.md)   
 [Iniciar, detener o pausar el servicio del Agente SQL Server](../../ssms/agent/start-stop-or-pause-the-sql-server-agent-service.md)  
  
  