---
title: "Ver y modificar par&#225;metros del s&#237;mbolo del sistema de los agentes de replicaci&#243;n (SQL Server Management Studio) | Microsoft Docs"
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
  - "agentes [replicación de SQL Server], parámetros de símbolo del sistema"
ms.assetid: 45f2e781-c21d-4b44-8992-89f60fb3d022
caps.latest.revision: 22
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
---
# Ver y modificar par&#225;metros del s&#237;mbolo del sistema de los agentes de replicaci&#243;n (SQL Server Management Studio)
  Los agentes de replicación son ejecutables que aceptan parámetros en la línea de comandos. De forma predeterminada, los agentes se ejecutan en [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] pasos de trabajo del agente, por lo que estos parámetros se pueden ver y modifican mediante el **Job Properties - \< trabajo>** cuadro de diálogo. Este cuadro de diálogo está disponible en la carpeta **Trabajos** en [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] y en la pestaña **Agentes** en el Monitor de replicación. Para obtener información acerca de cómo iniciar el Monitor de replicación, consulte [iniciar el Monitor de replicación](../../../relational-databases/replication/monitor/start-the-replication-monitor.md).  
  
> [!NOTE]  
>  Los cambios en los parámetros del agente tendrán efecto la próxima vez que se inicie el agente. Si el agente se ejecuta sin interrupción, debe detenerlo y reiniciarlo.  
  
 Aunque los parámetros se pueden modificar directamente, es más habitual modificarlos mediante un perfil de agente. Para más información, consulte [Replication Agent Profiles](../../../relational-databases/replication/agents/replication-agent-profiles.md).  
  
 Si tiene acceso a trabajos de agente en la carpeta **Trabajos** , utilice la siguiente tabla para determinar el nombre del trabajo del agente y los parámetros disponibles para cada agente.  
  
|Agente|Nombre del trabajo|Para obtener una lista de parámetros, vea…|  
|-----------|--------------|------------------------------------|  
|Agente de instantáneas|**\< publicador>-\< Basededatosdepublicaciones>-\< publicación>-\< entero>**|[Agente de instantáneas de replicación](../../../relational-databases/replication/agents/replication-snapshot-agent.md)|  
|Agente de replicación para una partición de publicación de combinación|**Dyn_ \< publicador>-\< Basededatosdepublicaciones>-\< publicación>-\< GUID>**|[Agente de instantáneas de replicación](../../../relational-databases/replication/agents/replication-snapshot-agent.md)|  
|Agente de registro del LOG|**\< publicador>-\< Basededatosdepublicaciones>-\< entero>**|[Agente de registro del LOG de replicación](../../../relational-databases/replication/agents/replication-log-reader-agent.md)|  
|Agente de mezcla para suscripciones de extracción|**\< publicador>-\< Basededatosdepublicaciones>-\< publicación>-\< suscriptor>-\< Basededatosdesuscripciones>-\< entero>**|[Agente de mezcla de replicación](../../../relational-databases/replication/agents/replication-merge-agent.md)|  
|Agente de mezcla para suscripciones de inserción|**\< publicador>-\< Basededatosdepublicaciones>-\< publicación>-\< suscriptor>-\< entero>**|[Agente de mezcla de replicación](../../../relational-databases/replication/agents/replication-merge-agent.md)|  
|Agente de distribución para suscripciones de inserción|**\< publicador>-\< Basededatosdepublicaciones>-\< publicación>-\< suscriptor>-\< entero>***|[Agente de distribución de replicación](../../../relational-databases/replication/agents/replication-distribution-agent.md)|  
|Agente de distribución para suscripciones de extracción|**\< publicador>-\< Basededatosdepublicaciones>-\< publicación>-\< suscriptor>-\< Basededatosdesuscripciones>-\< GUID>***\*|[Agente de distribución de replicación](../../../relational-databases/replication/agents/replication-distribution-agent.md)|  
|Agente de distribución para suscripciones de inserción en suscriptores que no sean de SQL Server|**\< publicador>-\< Basededatosdepublicaciones>-\< publicación>-\< suscriptor>-\< entero>**|[Agente de distribución de replicación](../../../relational-databases/replication/agents/replication-distribution-agent.md)|  
|Agente de lectura de cola|**[\< distribuidor>]. \< entero>**|[Agente de lectura de cola de replicación](../../../relational-databases/replication/agents/replication-queue-reader-agent.md)|  
  
 \*Para las suscripciones de inserción a publicaciones de Oracle, es **\< publicador>-\< publicador**> en lugar de **\< publicador>-\< Basededatosdepublicaciones>**  
  
 \*\*Para las suscripciones de extracción a publicaciones de Oracle, es **\< publicador>-\< DistributionDatabase**> en lugar de **\< publicador>-\< Basededatosdepublicaciones>**  
  
### Para ver y modificar los parámetros de la línea de comandos del agente de replicación desde Management Studio  
  
1.  Conéctese al equipo adecuado en [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)]y, a continuación, expanda el nodo de servidor:  
  
    -   En el Agente de distribución y el Agente de mezcla para suscripciones de extracción, conéctese al suscriptor.  
  
    -   Para el resto de agentes, conéctese al distribuidor.  
  
2.  Expanda la carpeta **Agente SQL Server** y a continuación la carpeta **Trabajos** .  
  
3.  Haga clic en un trabajo y, a continuación, haga clic en **propiedades**.  
  
4.  En el **pasos** página de la **Propiedades del trabajo - \< trabajo>** cuadro de diálogo, seleccione el paso **Ejecutar agente**, y, a continuación, haga clic en **Editar**.  
  
5.  En la **Propiedades de paso de trabajo - Ejecutar agente** cuadro de diálogo Editar el **comando** campo.  
  
6.  Haga clic en **Aceptar** en los dos cuadros de diálogo.  
  
### Para ver y modificar los parámetros de la línea de comandos del Agente de distribución y el Agente de mezcla desde el Monitor de replicación  
  
1.  Expanda un grupo de publicador en el panel izquierdo del Monitor de replicación, expanda un publicador y, a continuación, haga clic en una publicación.  
  
2.  Haga clic en la pestaña **Todas las suscripciones** .  
  
3.  Haga clic en una suscripción y, a continuación, haga clic en **Ver detalles**.  
  
4.  En el **suscripción \< Nombredesuscripción >** ventana, haga clic en **acción**, y, a continuación, haga clic en **\< Nombreagente> Propiedades del trabajo**.  
  
5.  En el **pasos** página de la **Propiedades del trabajo - \< trabajo>** cuadro de diálogo, seleccione el paso **Ejecutar agente**, y, a continuación, haga clic en **Editar**.  
  
6.  En la **Propiedades de paso de trabajo - Ejecutar agente** cuadro de diálogo Editar el **comando** campo.  
  
7.  Haga clic en **Aceptar** en los dos cuadros de diálogo.  
  
### Para ver y modificar los parámetros de la línea de comandos del Agente de instantáneas, Agente de registro del LOG y Agente de lectura de cola desde el Monitor de replicación  
  
1.  Expanda un grupo de publicador en el panel izquierdo del Monitor de replicación, expanda un publicador y, a continuación, haga clic en una publicación.  
  
2.  Haga clic en la pestaña **Agentes** .  
  
3.  Haga clic en un agente en la cuadrícula y, a continuación, haga clic en **propiedades**.  
  
4.  En el **pasos** página de la **Propiedades del trabajo - \< trabajo>** cuadro de diálogo, seleccione el paso **Ejecutar agente**, y, a continuación, haga clic en **Editar**.  
  
5.  En la **Propiedades de paso de trabajo - Ejecutar agente** cuadro de diálogo Editar el **comando** campo.  
  
6.  Haga clic en **Aceptar** en los dos cuadros de diálogo.  
  
## Vea también  
 [Administración del Agente de replicación](../../../relational-databases/replication/agents/replication-agent-administration.md)   
 [Conceptos de los ejecutables del Agente de replicación](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md)   
 [Información general sobre los agentes de replicación](../../../relational-databases/replication/agents/replication-agents-overview.md)  
  
  