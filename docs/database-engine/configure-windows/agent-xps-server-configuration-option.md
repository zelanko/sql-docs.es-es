---
title: Agent XPs (opción de configuración del servidor) | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.suite: sql
ms.technology: configuration
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Agent XPs option
- extended stored procedures [SQL Server], SQL Server Agent
ms.assetid: 2e1c6c64-5ce7-4357-98c7-ac7763a9f9de
caps.latest.revision: 24
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 42ebfa153ab481531ff0641ff0ab960114b9d1ac
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="agent-xps-server-configuration-option"></a>Agent XPs (opción de configuración del servidor)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  La opción **Agent XPs** habilita los procedimientos almacenados extendidos del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en este servidor. Cuando no está habilitada, el nodo del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no está disponible en el Explorador de objetos de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] .  
  
 Cuando utilice la herramienta [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para iniciar el servicio del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , estos procedimientos almacenados extendidos se habilitarán automáticamente. Para obtener más información, vea [Surface Area Configuration](../../relational-databases/security/surface-area-configuration.md).  
  
> [!NOTE]  
>  El Explorador de objetos de [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] no mostrará el contenido del nodo de Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], a no ser que estos procedimientos almacenados extendidos estén habilitados, independientemente del estado del servicio del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Los valores posibles son:  
  
-   **0**, que indica que los procedimientos almacenados extendidos del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no están disponibles (valor predeterminado).  
  
-   **1**, que indica que los procedimientos almacenados extendidos del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] están disponibles.  
  
 La configuración surte efecto inmediatamente, sin necesidad de detener y reiniciar el servidor.  
  
## <a name="example"></a>Ejemplo
 En el siguiente ejemplo se habilitan los procedimientos almacenados extendidos del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  

1. Conéctese al motor de base de datos desde Microsoft SQL Server Management Studio.

2.  En la barra Estándar, haga clic en **Nueva consulta**.

3.  Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**. 
  
```sql 
sp_configure 'show advanced options', 1;  
GO  
RECONFIGURE;  
GO  
sp_configure 'Agent XPs', 1;  
GO  
RECONFIGURE  
GO  
```  
  
## <a name="see-also"></a>Ver también  
 [Tareas administrativas automatizadas &#40;Agente SQL Server&#41;](http://msdn.microsoft.com/library/541ee5ac-2c9f-4b74-b4f0-13b7bd5920b0)   
 [Iniciar, detener o pausar el servicio del Agente SQL Server](http://msdn.microsoft.com/library/c95a9759-dd30-4ab6-9ab0-087bb3bfb97c)  
  
  
