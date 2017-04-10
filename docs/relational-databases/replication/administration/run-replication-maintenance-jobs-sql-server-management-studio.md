---
title: "Ejecutar trabajos de mantenimiento de replicaci&#243;n (SQL Server Management Studio) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "trabajos [replicación de SQL Server]"
ms.assetid: 0dc485a0-5a50-41eb-a29d-f2b2fb920174
caps.latest.revision: 38
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 38
---
# Ejecutar trabajos de mantenimiento de replicaci&#243;n (SQL Server Management Studio)
  La replicación utiliza los siguientes trabajos de mantenimiento:  
  
-   **Reinicializar suscripciones con errores de validación de datos**  
  
-   **Limpieza de historial del agente: distribución**  
  
-   **Actualizador de supervisión de replicación para distribución.**  
  
-   **Comprobación de agentes de replicación**  
  
-   **Limpieza de la distribución: distribución**  
  
-   **Limpieza de suscripciones expiradas**  
  
 Inicie y detenga estos trabajos en la carpeta **Trabajos** en [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] y en la pestaña **Agentes** del Monitor de replicación. Para obtener información acerca de cómo iniciar el Monitor de replicación, vea [iniciar el Monitor de replicación](../../../relational-databases/replication/monitor/start-the-replication-monitor.md). Ver y modificar las propiedades de cada trabajo en la **Propiedades del trabajo - \< trabajo>** cuadro de diálogo, que está disponible en la misma carpeta y pestaña.  
  
### Para iniciar o detener un mantenimiento de replicación en Management Studio  
  
1.  Conéctese al distribuidor en [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)]y expanda el nodo de servidor.  
  
2.  Expanda la carpeta **Agente SQL Server** y a continuación la carpeta **Trabajos** .  
  
3.  Haga clic en un trabajo y, a continuación, haga clic en **Iniciar trabajo** o **Detener trabajo**.  
  
### Para iniciar o detener un mantenimiento de replicación en el Monitor de replicación  
  
1.  Expanda un grupo de publicador en el Monitor de replicación y, a continuación, seleccione un publicador.  
  
2.  Haga clic en la pestaña **Agentes** .  
  
3.  Haga clic en un trabajo en la cuadrícula y, a continuación, haga clic en **Iniciar trabajo** o **Detener trabajo**.  
  
### Para ver y modificar las propiedades de un mantenimiento de replicación en Management Studio  
  
1.  Conéctese al distribuidor en [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)]y expanda el nodo de servidor.  
  
2.  Expanda la carpeta **Agente SQL Server** y a continuación la carpeta **Trabajos** .  
  
3.  Haga clic en un trabajo y, a continuación, haga clic en **propiedades**.  
  
4.  En la **Propiedades del trabajo - \< trabajo>** cuadro de diálogo, modifique las propiedades si es necesario y, a continuación, haga clic en **Aceptar**.  
  
### Para ver y modificar las propiedades de un mantenimiento de replicación en el Monitor de replicación  
  
1.  Expanda un grupo de publicador en el Monitor de replicación y, a continuación, seleccione un publicador.  
  
2.  Haga clic en la pestaña **Agentes** .  
  
3.  Haga clic en un trabajo en la cuadrícula y, a continuación, haga clic en **propiedades**.  
  
4.  En la **Propiedades del trabajo - \< trabajo>** cuadro de diálogo, modifique las propiedades si es necesario y, a continuación, haga clic en **Aceptar**.  
  
## Vea también  
 [Iniciar y detener un agente de replicación & #40; SQL Server Management Studio & #41;](../../../relational-databases/replication/agents/start-and-stop-a-replication-agent-sql-server-management-studio.md)   
 [Ver la información y realizar tareas para un publicador & #40; Monitor de replicación & #41;](../../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-a-publisher-replication-monitor.md)   
 [Administración del Agente de replicación](../../../relational-databases/replication/agents/replication-agent-administration.md)  
  
  