---
title: "Configurar alertas de replicaci&#243;n predefinidas (SQL Server Management Studio) | Microsoft Docs"
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
  - "alertas [replicación de SQL Server]"
  - "alertas de replicación predefinidas [replicación de SQL Server]"
ms.assetid: c0414147-7ffe-4f9a-908c-71c1b5201584
caps.latest.revision: 24
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 24
---
# Configurar alertas de replicaci&#243;n predefinidas (SQL Server Management Studio)
  La replicación ofrece las siguientes alertas predefinidas, que se pueden configurar para que respondan a eventos de replicación:  
  
-   **Replicación: éxito de agente**  
  
-   **Replicación: error de agente**  
  
-   **Replicación: reintento de agente**  
  
-   **Replicación: suscripción expirada quitada**  
  
-   **Replicación: Suscripción reinicializada por no pasar la validación**  
  
-   **Replicación: el suscriptor no ha superado la validación de datos**  
  
-   **Replicación: El suscriptor ha pasado la validación de datos**  
  
-   **Replicación: cierre personalizado del agente**  
  
 Configure estas alertas en la carpeta **Alertas** de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] o en la pestaña **Advertencias** del Monitor de replicación. Para obtener más información sobre el acceso a esta ficha, consulte [Ver información y realizar tareas para una suscripción & #40; Monitor de replicación & #41;](../../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-a-subscription-replication-monitor.md).  
  
 Además de estas alertas, el Monitor de replicación proporciona una serie de advertencias y alertas relacionadas con el estado y el rendimiento. Para más información, consulte [Set Thresholds and Warnings in Replication Monitor](../../../relational-databases/replication/monitor/set-thresholds-and-warnings-in-replication-monitor.md). También puede definir alertas para otros eventos de replicación con la infraestructura de alertas de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Para obtener más información, consulte [crear un evento definido por el usuario](../../../ssms/agent/create-a-user-defined-event.md).  
  
### Para configurar una alerta de replicación predefinida en Management Studio  
  
1.  Conéctese al distribuidor en [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)]y expanda el nodo de servidor.  
  
2.  Expanda la carpeta **Agente SQL Server** y, a continuación, la carpeta **Alertas** .  
  
3.  Haga clic en una alerta de replicación y, a continuación, haga clic en **propiedades**.  
  
4.  Establecer opciones en el **\< NombreAlerta> Propiedades de alerta** cuadro de diálogo:  
  
    -   En la página **General** , haga clic en **Habilitar**; especifique a qué base de datos desea que se aplique la alerta.  
  
    -   En el **respuesta** página, especifique si se debe enviar un correo electrónico o se debe ejecutar un trabajo.  
  
         Si la alerta es **replicación: suscriptor no ha superado la validación de datos**, puede especificar el trabajo de respuesta que la replicación proporciona para esta alerta: seleccione **Ejecutar trabajo**, y, a continuación, haga clic en el botón Examinar (**...**). En el cuadro de diálogo **Buscar trabajo** , haga clic en **Examinar**. En el cuadro de diálogo **Buscar objetos** , seleccione **Reinicializar suscripciones con errores de validación de datos**. Haga clic en **Aceptar** en los dos cuadros de diálogo abiertos. Cuando se ejecuta el trabajo, usa una llamada a procedimiento remoto (RPC) a un procedimiento almacenado que reinicializa la suscripción. Si el publicador usa un distribuidor remoto, debe definir un inicio de sesión de servidor remoto en el publicador, de manera que se pueda llevar a cabo la RPC del distribuidor al publicador.  
  
    -   En la página **Opciones** , personalice el texto de la respuesta.  
  
5.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
### Para configurar una alerta para un umbral en el Monitor de replicación  
  
1.  En la pestaña **Advertencias** , haga clic en **Configurar alertas**.  
  
2.  En el cuadro de diálogo **Configurar alertas de replicación** , seleccione una alerta y haga clic en **Configurar**.  
  
3.  Establecer opciones en el **\< NombreAlerta> Propiedades de alerta** cuadro de diálogo:  
  
    -   En la página **General** , haga clic en **Habilitar**; especifique a qué base de datos desea que se aplique la alerta.  
  
    -   En el **respuesta** página, especifique si se debe enviar un correo electrónico o se debe ejecutar un trabajo.  
  
         Si la alerta es **replicación: suscriptor no ha superado la validación de datos**, puede especificar el trabajo de respuesta que la replicación proporciona para esta alerta: seleccione **Ejecutar trabajo**, y, a continuación, haga clic en el botón Examinar (**...**). En el cuadro de diálogo **Buscar trabajo** , haga clic en **Examinar**. En el cuadro de diálogo **Buscar objetos** , seleccione **Reinicializar suscripciones con errores de validación de datos**. Haga clic en **Aceptar** en los dos cuadros de diálogo abiertos. Cuando se ejecuta el trabajo, usa una llamada a procedimiento remoto (RPC) a un procedimiento almacenado que reinicializa la suscripción. Si el publicador usa un distribuidor remoto, debe definir un inicio de sesión de servidor remoto en el publicador, de manera que se pueda llevar a cabo la RPC del distribuidor al publicador.  
  
    -   En la página **Opciones** , personalice el texto de la respuesta.  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
5.  Haga clic en **Cerrar**.  
  
## Vea también  
 [Usar alertas para eventos del Agente de replicación](../../../relational-databases/replication/agents/use-alerts-for-replication-agent-events.md)  
  
  