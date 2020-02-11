---
title: Iniciar y detener un agente de replicación (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- agents [SQL Server replication], stopping
- agents [SQL Server replication], starting
ms.assetid: 97977c4a-8c7c-4a22-9480-69aa812bd1e5
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 66be53c7b4c145f361c49c0e1611fa2942005ae5
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "63192466"
---
# <a name="start-and-stop-a-replication-agent-sql-server-management-studio"></a>Iniciar y detener un agente de replicación (SQL Server Management Studio)
  Inicie y detenga agentes desde la carpeta **trabajos** y la carpeta **replicación** en [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] y desde el monitor de replicación. Inicie y detenga los siguientes agentes y trabajos:  
  
-   El Agente de instantáneas, utilizado por todas las publicaciones.  
  
-   El Agente de registro del LOG, utilizado por todas las publicaciones transaccionales.  
  
-   El Agente de lectura de cola, utilizado por las publicaciones transaccionales con suscripciones de actualización en cola habilitadas.  
  
-   El Agente de distribución, que sincroniza las suscripciones con las publicaciones transaccionales y de instantáneas.  
  
-   El Agente de mezcla, que sincroniza las suscripciones con las publicaciones de combinación.  
  
-   Trabajos de mantenimiento de la replicación.  
  
 Para más información sobre cómo iniciar el Agente de mezcla y el Agente de distribución, vea [Sincronizar una suscripción de inserción](../synchronize-a-push-subscription.md) y [Sincronizar una suscripción de extracción](../synchronize-a-pull-subscription.md). Para más información acerca de los trabajos de mantenimiento, vea [Ejecutar trabajos de mantenimiento de replicación &#40;SQL Server Management Studio&#41;](../../../ssms/sql-server-management-studio-ssms.md).  
  
 Para información sobre cómo iniciar el Monitor de replicación, vea [Iniciar el Monitor de replicación](../monitor/start-the-replication-monitor.md).  
  
### <a name="to-start-and-stop-a-snapshot-agent-or-log-reader-agent-from-management-studio"></a>Para iniciar y detener un agente de instantáneas o un agente de registro del LOG desde Management Studio  
  
1.  Conéctese al publicador en [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)]y expanda el nodo de servidor y la carpeta **Replicación** .  
  
2.  Expanda la carpeta **Publicaciones locales** y haga clic con el botón secundario en una publicación.  
  
3.  Haga clic en **Ver estado del Agente de instantáneas** o **Ver estado del Agente de registro del LOG**.  
  
4.  Haga clic en **Iniciar** o **Detener**.  
  
### <a name="to-start-and-stop-a-queue-reader-agent-from-management-studio"></a>Para iniciar y detener un Agente de lectura de cola desde Management Studio  
  
1.  Conéctese al distribuidor en [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)]y expanda el nodo de servidor.  
  
2.  Expanda la carpeta **Agente SQL Server** y a continuación la carpeta **Trabajos** .  
  
3.  Haga clic con el botón secundario en el trabajo del agente y, a continuación, haga clic en **Iniciar trabajo** o **Detener trabajo**. El nombre del trabajo para el agente de lectura de cola tiene el formato **[\<distribuidor>].\< entero>**.  
  
### <a name="to-start-and-stop-a-snapshot-agent-log-reader-agent-or-queue-reader-agent-from-replication-monitor"></a>Para iniciar y detener un agente de instantáneas, un Agente de registro del LOG o un Agente de lectura de cola desde el Monitor de replicación  
  
1.  Expanda un grupo de publicador en el panel izquierdo, expanda un publicador y, a continuación, haga clic en una publicación.  
  
2.  Haga clic en la pestaña **Agentes** .  
  
3.  Haga clic con el botón secundario en un agente y, a continuación, haga clic en **Iniciar agente** o **Detener agente**.  
  
## <a name="see-also"></a>Consulte también  
 [Supervisión de la replicación](../monitoring-replication.md)   
 [Conceptos de los ejecutables del Agente de replicación](../concepts/replication-agent-executables-concepts.md)   
 [Información general sobre los agentes de replicación](replication-agents-overview.md)  
  
  
