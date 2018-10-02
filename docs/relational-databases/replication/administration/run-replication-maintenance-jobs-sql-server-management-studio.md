---
title: Ejecutar trabajos de mantenimiento de replicación (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- jobs [SQL Server replication]
ms.assetid: 0dc485a0-5a50-41eb-a29d-f2b2fb920174
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 980f22b1b2f6f50fb9c22effa8a96ffdc0466b69
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47604293"
---
# <a name="run-replication-maintenance-jobs-sql-server-management-studio"></a>Ejecutar trabajos de mantenimiento de replicación (SQL Server Management Studio)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  La replicación utiliza los siguientes trabajos de mantenimiento:  
  
-   **Reinicializar suscripciones con errores de validación de datos**  
  
-   **Limpieza de historial del agente: distribución**  
  
-   **Actualizador de supervisión de replicación para distribución.**  
  
-   **Comprobación de agentes de replicación**  
  
-   **Limpieza de la distribución: distribución**  
  
-   **Limpieza de suscripciones expiradas**  
  
 Inicie y detenga estos trabajos en la carpeta **Trabajos** en [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] y en la pestaña **Agentes** del Monitor de replicación. Para información sobre cómo iniciar el Monitor de replicación, vea [Iniciar el Monitor de replicación](../../../relational-databases/replication/monitor/start-the-replication-monitor.md). Vea y modifique las propiedades de cada trabajo en el cuadro de diálogo **Propiedades del trabajo: \<Trabajo>**, que está disponible en la misma carpeta y pestaña.  
  
### <a name="to-start-or-stop-a-replication-maintenance-job-in-management-studio"></a>Para iniciar o detener un mantenimiento de replicación en Management Studio  
  
1.  Conéctese al distribuidor en [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)]y expanda el nodo de servidor.  
  
2.  Expanda la carpeta **Agente SQL Server** y a continuación la carpeta **Trabajos** .  
  
3.  Haga clic con el botón secundario en un trabajo y, a continuación, haga clic en **Iniciar el trabajo** o **Detener el trabajo**.  
  
### <a name="to-start-or-stop-a-replication-maintenance-job-in-replication-monitor"></a>Para iniciar o detener un mantenimiento de replicación en el Monitor de replicación  
  
1.  Expanda un grupo de publicador en el Monitor de replicación y, a continuación, seleccione un publicador.  
  
2.  Haga clic en la pestaña **Agentes** .  
  
3.  Haga clic con el botón secundario en la cuadrícula y, a continuación, haga clic en **Iniciar el trabajo** o **Detener el trabajo**.  
  
### <a name="to-view-and-modify-properties-for-a-replication-maintenance-job-in-management-studio"></a>Para ver y modificar las propiedades de un mantenimiento de replicación en Management Studio  
  
1.  Conéctese al distribuidor en [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)]y expanda el nodo de servidor.  
  
2.  Expanda la carpeta **Agente SQL Server** y a continuación la carpeta **Trabajos** .  
  
3.  Haga clic con el botón derecho en un trabajo y, a continuación, haga clic en **Propiedades**.  
  
4.  En el cuadro de diálogo **Propiedades del trabajo: \<Trabajo>**, modifique las propiedades si es necesario y luego haga clic en **Aceptar**.  
  
### <a name="to-view-and-modify-properties-for-a-replication-maintenance-job-in-replication-monitor"></a>Para ver y modificar las propiedades de un mantenimiento de replicación en el Monitor de replicación  
  
1.  Expanda un grupo de publicador en el Monitor de replicación y, a continuación, seleccione un publicador.  
  
2.  Haga clic en la pestaña **Agentes** .  
  
3.  Haga clic con el botón secundario en un trabajo en la cuadrícula y , a continuación, haga clic en **Propiedades**.  
  
4.  En el cuadro de diálogo **Propiedades del trabajo: \<Trabajo>**, modifique las propiedades si es necesario y luego haga clic en **Aceptar**.  
  
## <a name="see-also"></a>Ver también  
 [Iniciar y detener un agente de replicación &#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/agents/start-and-stop-a-replication-agent-sql-server-management-studio.md)   
 [Ver información y realizar tareas para un publicador &#40;Monitor de replicación&#41;](../../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-a-publisher-replication-monitor.md)   
 [Administración del Agente de replicación](../../../relational-databases/replication/agents/replication-agent-administration.md)  
  
  
