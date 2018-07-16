---
title: Agent XPs (opción de configuración del servidor) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Agent XPs option
- extended stored procedures [SQL Server], SQL Server Agent
ms.assetid: 2e1c6c64-5ce7-4357-98c7-ac7763a9f9de
caps.latest.revision: 22
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 841722b555a4f031263cf966d9f833cfd6f54c8f
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37279571"
---
# <a name="agent-xps-server-configuration-option"></a>Agent XPs (opción de configuración del servidor)
  La opción **Agent XPs** habilita los procedimientos almacenados extendidos del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en este servidor. Cuando no está habilitada, el nodo del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no está disponible en el Explorador de objetos de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] .  
  
 Cuando utilice la herramienta [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para iniciar el servicio del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , estos procedimientos almacenados extendidos se habilitarán automáticamente. Para obtener más información, vea [Surface Area Configuration](../../relational-databases/security/surface-area-configuration.md).  
  
> [!NOTE]  
>  El Explorador de objetos de [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] no mostrará el contenido del nodo de Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], a no ser que estos procedimientos almacenados extendidos estén habilitados, independientemente del estado del servicio del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Los valores posibles son:  
  
-   **0**, que indica que los procedimientos almacenados extendidos del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no están disponibles (valor predeterminado).  
  
-   **1**, que indica que los procedimientos almacenados extendidos del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] están disponibles.  
  
 La configuración surte efecto inmediatamente, sin necesidad de detener y reiniciar el servidor.  
  
## <a name="examples"></a>Ejemplos  
 En el siguiente ejemplo se habilitan los procedimientos almacenados extendidos del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
```  
sp_configure 'show advanced options', 1;  
GO  
RECONFIGURE;  
GO  
sp_configure 'Agent XPs', 1;  
GO  
RECONFIGURE  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [Tareas administrativas automatizadas &#40;Agente SQL Server&#41;](../../ssms/agent/sql-server-agent.md)   
 [Iniciar, detener o pausar el servicio del Agente SQL Server](../../ssms/agent/start-stop-or-pause-the-sql-server-agent-service.md)  
  
  
