---
title: Registro de errores del Agente SQL Server | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssms-agent
ms.reviewer: 
ms.suite: sql
ms.technology: tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- logs [SQL Server], SQL Server Agent
- messages [SQL Server], SQL Server Agent
- errors [SQL Server], logs
- SQL Server Agent, errors
ms.assetid: 0b2d6e6e-cd2d-4b8b-9fa2-2bbd2fc0da41
caps.latest.revision: "4"
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: e12dc0a4a2a301d39060d1b5e80836f970dafe0d
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="sql-server-agent-error-log"></a>Registro de errores del Agente SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] El Agente 
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] crea un registro de errores que, de manera predeterminada, registra advertencias y errores. En el registro se visualizan los siguientes errores y advertencias:  
  
-   Mensajes de advertencia que proporcionan información sobre posibles problemas, como "El trabajo \<*nombre_trabajo*> se eliminó mientras se estaba ejecutando".  
  
-   Mensajes de error que normalmente requieren la intervención de un administrador del sistema, como "No se puede iniciar la sesión de correo". Los mensajes de error se pueden enviar a un usuario o equipo específicos mediante **net send**.  
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] puede mantener hasta nueve registros de errores del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] . Cada registro archivado tiene una extensión que indica la antigüedad relativa del registro de errores. Por ejemplo, una extensión de .1 indica que es el archivo de registro de errores más reciente y una extensión de .9 indica que es el archivo de registro de errores más antiguo.  
  
De forma predeterminada, los mensajes de seguimiento de ejecución no se escriben en el registro de errores del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] porque lo pueden llenar, reduciendo así la posibilidad de seleccionar y analizar los errores más difíciles. Puesto que el registro de errores agrega una carga de proceso adicional al servidor, es importante considerar las ventajas que se obtienen al capturar los mensajes de seguimiento de ejecución en este registro de errores. Generalmente, es mejor capturar todos los mensajes solo cuando se está depurando un problema específico.  
  
Cuando se detiene el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] , se puede modificar la ubicación del registro de errores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] . Cuando el registro de errores está vacío, no se puede abrir. Se puede reciclar el registro del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] en cualquier momento, sin necesidad de detener el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] .  
  
**Para ver el registro de errores del Agente SQL Server**  
  
-   [Ver registro de errores del Agente SQL Server &#40;SQL Server Management Studio&#41;](../../ssms/agent/view-sql-server-agent-error-log-sql-server-management-studio.md)  
  
**Para cambiar el nombre del registro de errores del Agente SQL Server**  
  
-   [Cambiar el nombre del registro de errores del Agente SQL Server &#40;SQL Server Management Studio&#41;](../../ssms/agent/rename-a-sql-server-agent-error-log-sql-server-management-studio.md)  
  
**Para enviar mensajes de error del Agente SQL Server**  
  
-   [Send SQL Server Agent Error Messages](../../ssms/agent/send-sql-server-agent-error-messages.md)  
  
**Para escribir mensajes de seguimiento de ejecución en el registro de errores del Agente SQL Server**  
  
-   [Escribir mensajes de seguimiento de ejecución en el registro de errores del Agente SQL Server &#40;SQL Server Management Studio&#41;](../../ssms/agent/write-execution-trace-messages-to-sql-server-agent-log-ssms.md)  
  
