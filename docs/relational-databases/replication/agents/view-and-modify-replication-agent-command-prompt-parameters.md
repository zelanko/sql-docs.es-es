---
title: Consulta y modificación de los parámetros del símbolo del sistema del agente
description: Obtenga información sobre cómo ver y modificar los parámetros del símbolo del sistema usados por los diferentes agentes de replicación en SQL Server.
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- agents [SQL Server replication], command prompt parameters
ms.assetid: 45f2e781-c21d-4b44-8992-89f60fb3d022
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 6c72c58b0a23f8215d303addfbb2ec9fb65c4489
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "75321642"
---
# <a name="view-and-modify-replication-agent-command-prompt-parameters"></a>Ver y modificar parámetros del símbolo del sistema de los agentes de replicación
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Los agentes de replicación son ejecutables que aceptan parámetros en la línea de comandos. De forma predeterminada, los agentes se ejecutan en los pasos de trabajo del Agente [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], de modo que estos parámetros se pueden ver y modificar mediante el cuadro de diálogo **Propiedades del trabajo: \<trabajo>** . Este cuadro de diálogo está disponible en la carpeta **Trabajos** en [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] y en la pestaña **Agentes** en el Monitor de replicación. Para información sobre cómo iniciar el Monitor de replicación, vea [Iniciar el Monitor de replicación](../../../relational-databases/replication/monitor/start-the-replication-monitor.md).  
  
> [!NOTE]  
>  Los cambios en los parámetros del agente tendrán efecto la próxima vez que se inicie el agente. Si el agente se ejecuta sin interrupción, debe detenerlo y reiniciarlo.  
  
 Aunque los parámetros se pueden modificar directamente, es más habitual modificarlos mediante un perfil de agente. Para obtener más información, consulte [Replication Agent Profiles](../../../relational-databases/replication/agents/replication-agent-profiles.md).  
  
 Si tiene acceso a trabajos de agente en la carpeta **Trabajos** , utilice la siguiente tabla para determinar el nombre del trabajo del agente y los parámetros disponibles para cada agente.  
  
|Agente|Nombre del trabajo|Para obtener una lista de parámetros, vea…|  
|-----------|--------------|------------------------------------|  
|Agente de instantáneas|**\<publicador>-\<baseDeDatosDePublicación>-\<publicación>-\<entero>**|[Replication Snapshot Agent](../../../relational-databases/replication/agents/replication-snapshot-agent.md)|  
|Agente de replicación para una partición de publicación de combinación|**Dyn_\<publicador>-\<baseDeDatosDePublicación>-\<publicación>-\<GUID>**|[Replication Snapshot Agent](../../../relational-databases/replication/agents/replication-snapshot-agent.md)|  
|Agente de registro del LOG|**\<publicador>-\<baseDeDatosDePublicación>-\<entero>**|[Agente de registro del LOG de replicación](../../../relational-databases/replication/agents/replication-log-reader-agent.md)|  
|Agente de mezcla para suscripciones de extracción|**\<publicador>-\<baseDeDatosDePublicación>-\<publicación>-\<suscriptor>-\<baseDeDatosDeSuscripciones>-\<entero>**|[Replication Merge Agent](../../../relational-databases/replication/agents/replication-merge-agent.md)|  
|Agente de mezcla para suscripciones de inserción|**\<publicador>-\<baseDeDatosDePublicación>-\<publicación>-\<suscriptor>-\<entero>**|[Replication Merge Agent](../../../relational-databases/replication/agents/replication-merge-agent.md)|  
|Agente de distribución para suscripciones de inserción|**\<publicador>-\<baseDeDatosDePublicación>-\<publicación>-\<suscriptor>-\<entero>**|[Replication Distribution Agent](../../../relational-databases/replication/agents/replication-distribution-agent.md)|  
|Agente de distribución para suscripciones de extracción|**\<Publicador>-\<BaseDeDatosDePublicación>-\<Publicación>-\<Suscriptor>-\<BaseDeDatosDeSuscripción>-\<GUID>**|[Replication Distribution Agent](../../../relational-databases/replication/agents/replication-distribution-agent.md)|  
|Agente de distribución para suscripciones de inserción en suscriptores que no sean de SQL Server|**\<publicador>-\<baseDeDatosDePublicación>-\<publicación>-\<suscriptor>-\<entero>**|[Replication Distribution Agent](../../../relational-databases/replication/agents/replication-distribution-agent.md)|  
|Agente de lectura de cola|**[\<distribuidor>].\<entero>**|[Agente de lectura de cola de replicación](../../../relational-databases/replication/agents/replication-queue-reader-agent.md)|  
  
 \*Para suscripciones de inserción a publicaciones de Oracle, es **\<Publicador>-\<Publicador**> en lugar de **\<Publicador>-\<baseDeDatosDePublicación>**  
  
 \*\*Para suscripciones de extracción a publicaciones de Oracle, es **\<Publicador>-\<baseDeDatosDeDistribución**> en lugar de **\<Publicador>-\<baseDeDatosDePublicación>**  
  
### <a name="to-view-and-modify-replication-agent-command-line-parameters-from-management-studio"></a>Para ver y modificar los parámetros de la línea de comandos del agente de replicación desde Management Studio  
  
1.  Conéctese al equipo adecuado en [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)]y, a continuación, expanda el nodo de servidor:  
  
    -   En el Agente de distribución y el Agente de mezcla para suscripciones de extracción, conéctese al suscriptor.  
  
    -   Para el resto de agentes, conéctese al distribuidor.  
  
2.  Expanda la carpeta **Agente SQL Server** y a continuación la carpeta **Trabajos** .  
  
3.  Haga clic con el botón derecho en un trabajo y, a continuación, haga clic en **Propiedades**.  
  
4.  En la página **Pasos** del cuadro de diálogo **Propiedades del trabajo: \<Trabajo>** , seleccione el paso **Ejecutar agente** y luego haga clic en **Editar**.  
  
5.  En el cuadro de diálogo **Propiedades de paso de trabajo - Ejecutar agente** , edite el campo **Comando** .  
  
6.  Haga clic en **Aceptar** en los dos cuadros de diálogo.  
  
### <a name="to-view-and-modify-distribution-agent-and-merge-agent-command-line-parameters-from-replication-monitor"></a>Para ver y modificar los parámetros de la línea de comandos del Agente de distribución y el Agente de mezcla desde el Monitor de replicación  
  
1.  Expanda un grupo de publicador en el panel izquierdo del Monitor de replicación, expanda un publicador y, a continuación, haga clic en una publicación.  
  
2.  Haga clic en la pestaña **Todas las suscripciones** .  
  
3.  Haga clic con el botón secundario en una suscripción y, a continuación, haga clic en **Ver detalles**.  
  
4.  En la ventana **Suscripción <nombreDeSuscripción>** , haga clic en **Acción** y, después, haga clic en **Propiedades del trabajo del \<nombreDeAgente>** .  
  
5.  En la página **Pasos** del cuadro de diálogo **Propiedades del trabajo: \<Trabajo>** , seleccione el paso **Ejecutar agente** y luego haga clic en **Editar**.  
  
6.  En el cuadro de diálogo **Propiedades de paso de trabajo - Ejecutar agente** , edite el campo **Comando** .  
  
7.  Haga clic en **Aceptar** en los dos cuadros de diálogo.  
  
### <a name="to-view-and-modify-snapshot-agent-log-reader-agent-and-queue-reader-agent-command-line-parameters-from-replication-monitor"></a>Para ver y modificar los parámetros de la línea de comandos del Agente de instantáneas, Agente de registro del LOG y Agente de lectura de cola desde el Monitor de replicación  
  
1.  Expanda un grupo de publicador en el panel izquierdo del Monitor de replicación, expanda un publicador y, a continuación, haga clic en una publicación.  
  
2.  Haga clic en la pestaña **Agentes** .  
  
3.  Haga clic con el botón secundario en un agente en la cuadrícula y, a continuación, haga clic en **Propiedades**.  
  
4.  En la página **Pasos** del cuadro de diálogo **Propiedades del trabajo: \<Trabajo>** , seleccione el paso **Ejecutar agente** y luego haga clic en **Editar**.  
  
5.  En el cuadro de diálogo **Propiedades de paso de trabajo - Ejecutar agente** , edite el campo **Comando** .  
  
6.  Haga clic en **Aceptar** en los dos cuadros de diálogo.  
  
## <a name="see-also"></a>Consulte también  
 [Administración del Agente de replicación](../../../relational-databases/replication/agents/replication-agent-administration.md)   
 [Conceptos de los ejecutables del Agente de replicación](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md)   
 [Información general sobre los agentes de replicación](../../../relational-databases/replication/agents/replication-agents-overview.md)  
  
  
