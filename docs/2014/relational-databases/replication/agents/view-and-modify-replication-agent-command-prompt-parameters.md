---
title: Ver y modificar los parámetros de línea de comandos del agente de replicación (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- agents [SQL Server replication], command prompt parameters
ms.assetid: 45f2e781-c21d-4b44-8992-89f60fb3d022
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 6e4327de10dd03b3ff8cf034ade64391d18d2a86
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63192899"
---
# <a name="view-and-modify-replication-agent-command-prompt-parameters-sql-server-management-studio"></a>Ver y modificar parámetros del símbolo del sistema de los agentes de replicación (SQL Server Management Studio)
  Los agentes de replicación son ejecutables que aceptan parámetros en la línea de comandos. De forma predeterminada, los agentes se ejecutan en los pasos de trabajo del Agente [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], de modo que estos parámetros se pueden ver y modificar mediante el cuadro de diálogo **Propiedades del trabajo: \<trabajo>** . Este cuadro de diálogo está disponible en la carpeta **Trabajos** en [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] y en la pestaña **Agentes** en el Monitor de replicación. Para información sobre cómo iniciar el Monitor de replicación, vea [Iniciar el Monitor de replicación](../monitor/start-the-replication-monitor.md).  
  
> [!NOTE]  
>  Los cambios en los parámetros del agente tendrán efecto la próxima vez que se inicie el agente. Si el agente se ejecuta sin interrupción, debe detenerlo y reiniciarlo.  
  
 Aunque los parámetros se pueden modificar directamente, es más habitual modificarlos mediante un perfil de agente. Para más información, consulte [Replication Agent Profiles](replication-agent-profiles.md).  
  
 Si tiene acceso a trabajos de agente en la carpeta **Trabajos** , utilice la siguiente tabla para determinar el nombre del trabajo del agente y los parámetros disponibles para cada agente.  
  
|Agente|Nombre del trabajo|Para obtener una lista de parámetros, vea...|  
|-----------|--------------|------------------------------------|  
|Agente de instantáneas|**\<Publicador>-\<baseDeDatosDePublicación>-\<Publicación>-\<entero>**|[Replication Snapshot Agent](replication-snapshot-agent.md)|  
|Agente de replicación para una partición de publicación de combinación|**Dyn_\<Publicador>-\<baseDeDatosDePublicación>-\<Publicación>-\<GUID>**|[Replication Snapshot Agent](replication-snapshot-agent.md)|  
|Agente de registro del LOG|**\<Publicador>-\<baseDeDatosDePublicación>-\<entero>**|[Agente de registro del LOG de replicación](replication-log-reader-agent.md)|  
|Agente de mezcla para suscripciones de extracción|**\<Publicador>-\<baseDeDatosDePublicación>-\<Publicación>-\<Suscriptor>-\<baseDeDatosDeSuscripción>-\<entero>**|[Replication Merge Agent](replication-merge-agent.md)|  
|Agente de mezcla para suscripciones de inserción|**\<Publicador>-\<baseDeDatosDePublicación>-\<Publicación>-\<Suscriptor>-\<entero>**|[Replication Merge Agent](replication-merge-agent.md)|  
|Agente de distribución para suscripciones de inserción|**\<publicador>-\<baseDeDatosDePublicación>-\<publicación>-\<suscriptor>-\<entero>** <sup>1</sup>|[Replication Distribution Agent](replication-distribution-agent.md)|  
|Agente de distribución para suscripciones de extracción|**\<publicador>-\<baseDeDatosDePublicación>-\<publicación>-\<suscriptor>-\<baseDeDatosDeSuscripción>-\<GUID>** <sup>2</sup>|[Replication Distribution Agent](replication-distribution-agent.md)|  
|Agente de distribución para suscripciones de inserción en suscriptores que no sean de SQL Server|**\<publicador>-\<baseDeDatosDePublicación>-\<publicación>-\<suscriptor>-\<entero>**|[Replication Distribution Agent](replication-distribution-agent.md)|  
|Agente de lectura de cola|**[\<Distribuidor>].\<entero>**|[Agente de lectura de cola de replicación](replication-queue-reader-agent.md)|  
  
 <sup>1</sup> Para suscripciones de inserción a publicaciones de Oracle, es **\<publicador>-\<publicador**> en lugar de **\<publicador>-\<baseDeDatosDePublicación>**  
  
 <sup>2</sup> Para suscripciones de extracción a publicaciones de Oracle, es **\<publicador>-\<baseDeDatosDeDistribución**> en lugar de **\<publicador>-\<baseDeDatosDePublicación>**  
  
### <a name="to-view-and-modify-replication-agent-command-line-parameters-from-management-studio"></a>Para ver y modificar los parámetros de la línea de comandos del agente de replicación desde Management Studio  
  
1.  Conéctese al equipo adecuado en [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)]y, a continuación, expanda el nodo de servidor:  
  
    -   En el Agente de distribución y el Agente de mezcla para suscripciones de extracción, conéctese al suscriptor.  
  
    -   Para el resto de agentes, conéctese al distribuidor.  
  
2.  Expanda la carpeta **Agente SQL Server** y a continuación la carpeta **Trabajos** .  
  
3.  Haga clic con el botón secundario en un trabajo y, a continuación, haga clic en **Propiedades**.  
  
4.  En la página **Pasos** del cuadro de diálogo **Propiedades del trabajo: \<Trabajo>** , seleccione el paso **Ejecutar agente** y luego haga clic en **Editar**.  
  
5.  En el cuadro de diálogo **Propiedades de paso de trabajo - Ejecutar agente** , edite el campo **Comando** .  
  
6.  Haga clic en **Aceptar** en los dos cuadros de diálogo.  
  
### <a name="to-view-and-modify-distribution-agent-and-merge-agent-command-line-parameters-from-replication-monitor"></a>Para ver y modificar los parámetros de la línea de comandos del Agente de distribución y el Agente de mezcla desde el Monitor de replicación  
  
1.  Expanda un grupo de publicador en el panel izquierdo del Monitor de replicación, expanda un publicador y, a continuación, haga clic en una publicación.  
  
2.  Haga clic en la pestaña **Todas las suscripciones** .  
  
3.  Haga clic con el botón secundario en una suscripción y, a continuación, haga clic en **Ver detalles**.  
  
4.  En el **suscripción \< SubscriptionName >** ventana, haga clic en **acción**y, a continuación, haga clic en  **\<Nombreagente > Propiedades del trabajo**.  
  
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
  
## <a name="see-also"></a>Vea también  
 [Administración del Agente de replicación](replication-agent-administration.md)   
 [Conceptos de los ejecutables del Agente de replicación](../concepts/replication-agent-executables-concepts.md)   
 [Replication Agents Overview](replication-agents-overview.md)  
  
  
