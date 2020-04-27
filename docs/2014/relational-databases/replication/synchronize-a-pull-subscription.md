---
title: Sincronización de una suscripción de extracción | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- pull subscriptions [SQL Server replication], synchronizing
- synchronization [SQL Server replication], pull subscriptions
- subscriptions [SQL Server replication], pull
ms.assetid: 3ca24b23-fdc3-408e-8208-a2ace48fc8e3
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: c8a7a607221599d599438352eab5add1cc94e5d7
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "63186234"
---
# <a name="synchronize-a-pull-subscription"></a>Sincronización de una suscripción de extracción
  En este tema se describe cómo sincronizar una suscripción de extracción en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], [agentes de replicación](agents/replication-agents-overview.md) o Replication Management Objects (RMO).  
  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Uso de SQL Server Management Studio  
 El Agente de distribución (para las instantáneas y la replicación transaccional) o el Agente de mezcla (para la replicación de mezcla) sincronizan las suscripciones. Los agentes pueden ejecutarse continuamente, a petición o según una programación. Para más información sobre la configuración de las programaciones de sincronización, vea [Especificar programaciones de sincronización](specify-synchronization-schedules.md).  
  
 Sincronice una suscripción a petición desde la carpeta **Suscripciones locales** de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
#### <a name="to-synchronize-a-pull-subscription-on-demand-in-management-studio"></a>Para sincronizar una suscripción de extracción a petición en Management Studio  
  
1.  Conéctese al suscriptor en [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]y expanda el nodo de servidor.  
  
2.  Expanda la carpeta **Replicación** y, a continuación, la carpeta **Suscripciones locales**.  
  
3.  Haga clic con el botón derecho en la suscripción que desea sincronizar y, a continuación, haga clic en **Ver estado de sincronización**.  
  
4.  En el cuadro de diálogo **Ver estado de sincronización: \<suscriptor>:\<baseDeDatosDeSuscripción>**, haga clic en **Iniciar**. Cuando se completa la sincronización, se muestra el mensaje **Sincronización completada**.  
  
5.  Haga clic en **Cerrar**.  
  
##  <a name="replication-agents"></a><a name="ReplProg"></a>Agentes de replicación  
 Se pueden sincronizar las suscripciones de extracción mediante programación y a petición invocando el archivo ejecutable del agente de replicación adecuado del símbolo del sistema. El archivo ejecutable de agente de replicación que se invoca dependerá del tipo de publicación a la que pertenece la suscripción de extracción. Para más información, consulte [Agentes de replicación](agents/replication-agents-overview.md).  
  
> [!NOTE]  
>  Los agentes de replicación se conectan al servidor local con las credenciales de autenticación de Windows del usuario que inició el agente desde el símbolo del sistema. También se usan estas credenciales de Windows al conectarse a los servidores remotos con la autenticación integrada de Windows.  
  
#### <a name="to-start-the-distribution-agent-from-the-command-prompt-or-from-a-batch-file"></a>Para iniciar el agente de distribución desde el símbolo del sistema o desde un archivo por lotes  
  
1.  Desde el símbolo del sistema o en un archivo por lotes, inicie el [Agente de distribución de replicación](agents/replication-distribution-agent.md) ejecutando **distrib.exe** y especificando los argumentos de la línea de comandos siguientes:  
  
    -   **-Publicador**  
  
    -   **-PublisherDB**  
  
    -   **-Distribuidor**  
  
    -   **-DistributorSecurityMode** = **1**  
  
    -   **-Suscriptor**  
  
    -   **-SubscriberDB**  
  
    -   **-SubscriberSecurityMode** = **1**  
  
    -   **-SubscriptionType** = **1**  
  
     Si está usando la autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], también debe especificar los argumentos siguientes:  
  
    -   **-DistributorLogin**  
  
    -   **-DistributorPassword**  
  
    -   **-DistributorSecurityMode** = **0**  
  
    -   **-PublisherLogin**  
  
    -   **-PublisherPassword**  
  
    -   **-PublisherSecurityMode** = **0**  
  
    -   **-SubscriberLogin**  
  
    -   **-SubscriberPassword**  
  
    -   **-SubscriberSecurityMode** = **0**  
  
#### <a name="to-start-the-merge-agent-from-the-command-prompt-or-from-a-batch-file"></a>Para iniciar el agente de mezcla desde el símbolo del sistema o desde un archivo por lotes  
  
1.  Desde el símbolo del sistema o en un archivo por lotes, inicie el [Agente de mezcla de replicación](agents/replication-merge-agent.md) ejecutando **replmerg.exe** y especificando los argumentos de la línea de comandos siguientes:  
  
    -   **-Publicador**  
  
    -   **-PublisherDB**  
  
    -   **-PublisherSecurityMode** = **1**  
  
    -   **-Publicación**  
  
    -   **-Distribuidor**  
  
    -   **-DistributorSecurityMode** = **1**  
  
    -   **-Suscriptor**  
  
    -   **-SubscriberSecurityMode** = **1**  
  
    -   **-SubscriberDB**  
  
    -   **-SubscriptionType** = **1**  
  
     Si está usando la autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], también debe especificar los argumentos siguientes:  
  
    -   **-DistributorLogin**  
  
    -   **-DistributorPassword**  
  
    -   **-DistributorSecurityMode** = **0**  
  
    -   **-PublisherLogin**  
  
    -   **-PublisherPassword**  
  
    -   **-PublisherSecurityMode** = **0**  
  
    -   **-SubscriberLogin**  
  
    -   **-SubscriberPassword**  
  
    -   **-SubscriberSecurityMode** = **0**  
  
###  <a name="examples-replication-agents"></a><a name="TsqlExample"></a> Ejemplos (agentes de replicación)  
 El ejemplo siguiente inicia el Agente de distribución para sincronizar una suscripción de extracción. Todas las conexiones se realizan con la autenticación de Windows.  
  
 [!code-sql[HowTo#bat_synctranpullsub_10](../../snippets/tsql/SQL15/replication/howto/tsql/synctranpullsub_10.bat)]  
  
 El ejemplo siguiente inicia el Agente de mezcla para sincronizar una suscripción de extracción. Todas las conexiones se realizan con la autenticación de Windows.  
  
 [!code-sql[HowTo#bat_syncmergepullsub_10](../../snippets/tsql/SQL15/replication/howto/tsql/syncmergepullsub_10.bat)]  
  
##  <a name="using-replication-management-objects-rmo"></a><a name="RMOProcedure"></a> Uso de Replication Management Objects (RMO)  
 Puede sincronizar suscripciones de extracción mediante programación con Replication Management Objects (RMO) y el acceso de código administrado a las funcionalidades del agente de replicación. Las clases que se usan para crear una suscripción de extracción dependen del tipo de publicación al que pertenece la suscripción.  
  
> [!NOTE]  
>  Si desea iniciar una sincronización que se ejecute de forma autónoma sin afectar a la aplicación, inicie el agente asincrónicamente. Sin embargo, si desea supervisar el resultado de la sincronización y recibir las devoluciones de llamada del agente durante el proceso de sincronización (por ejemplo, para mostrar una barra de progreso), debe iniciar el agente sincrónicamente. Para los suscriptores de [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssExpressEd2005](../../includes/ssexpressed2005-md.md)], debe iniciar el agente sincrónicamente.  
  
#### <a name="to-synchronize-a-pull-subscription-to-a-snapshot-or-transactional-publication"></a>Para sincronizar una suscripción de extracción con una publicación transaccional o de instantáneas  
  
1.  Cree una conexión al suscriptor mediante la clase <xref:Microsoft.SqlServer.Management.Common.ServerConnection>.  
  
2.  Cree una instancia de la clase <xref:Microsoft.SqlServer.Replication.TransPullSubscription> y establezca las propiedades siguientes:  
  
    -   El nombre de la base de datos de suscripciones para <xref:Microsoft.SqlServer.Replication.PullSubscription.DatabaseName%2A>.  
  
    -   El nombre de la publicación a la que pertenece la suscripción para <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationName%2A>.  
  
    -   El nombre de la base de datos de publicación para <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationDBName%2A>.  
  
    -   El nombre del publicador para <xref:Microsoft.SqlServer.Replication.PullSubscription.PublisherName%2A>.  
  
    -   La conexión creada en el paso 1 para <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>.  
  
3.  Llame al método <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> para obtener las propiedades de suscripción restantes. Si este método devuelve `false`, compruebe que la suscripción existe.  
  
4.  Inicie el Agente de distribución en el suscriptor de una de las maneras siguientes:  
  
    -   Llame al método <xref:Microsoft.SqlServer.Replication.TransPullSubscription.SynchronizeWithJob%2A> en la instancia de <xref:Microsoft.SqlServer.Replication.TransPullSubscription> del paso 2. Este método inicia el Agente de distribución de forma asincrónica y controla inmediatamente las devoluciones a la aplicación mientras se está ejecutando el trabajo del agente. No puede llamar a este método para suscriptores de [!INCLUDE[ssExpressEd2005](../../includes/ssexpressed2005-md.md)] o si la suscripción se creó con un valor de `false` para <xref:Microsoft.SqlServer.Replication.PullSubscription.CreateSyncAgentByDefault%2A> (predeterminado).  
  
    -   Obtenga una instancia de la clase <xref:Microsoft.SqlServer.Replication.TransSynchronizationAgent> de la propiedad <xref:Microsoft.SqlServer.Replication.TransPullSubscription.SynchronizationAgent%2A> y llame al método <xref:Microsoft.SqlServer.Replication.TransSynchronizationAgent.Synchronize%2A>. Este método inicia el agente sincrónicamente y controla el resto con el trabajo del agente en ejecución. Durante la ejecución sincrónica, puede administrar el evento <xref:Microsoft.SqlServer.Replication.TransSynchronizationAgent.Status> mientras el agente se está ejecutando.  
  
        > [!NOTE]  
        >  Si especificó un valor de `false` para <xref:Microsoft.SqlServer.Replication.PullSubscription.CreateSyncAgentByDefault%2A> (predeterminado) cuando creó la suscripción de extracción, también debe especificar <xref:Microsoft.SqlServer.Replication.TransSynchronizationAgent.Distributor%2A>, y, <xref:Microsoft.SqlServer.Replication.TransSynchronizationAgent.DistributorSecurityMode%2A>opcionalmente, <xref:Microsoft.SqlServer.Replication.TransSynchronizationAgent.DistributorLogin%2A> y <xref:Microsoft.SqlServer.Replication.TransSynchronizationAgent.DistributorPassword%2A> porque los metadatos relacionados con el trabajo del agente para la suscripción no están disponibles en [MSsubscription_properties](/sql/relational-databases/system-tables/mssubscription-properties-transact-sql).  
  
#### <a name="to-synchronize-a-pull-subscription-to-a-merge-publication"></a>Para sincronizar una suscripción de extracción con una publicación de combinación  
  
1.  Cree una conexión al suscriptor mediante la clase <xref:Microsoft.SqlServer.Management.Common.ServerConnection>.  
  
2.  Cree una instancia de la clase <xref:Microsoft.SqlServer.Replication.MergePullSubscription> y establezca las propiedades siguientes:  
  
    -   El nombre de la base de datos de suscripciones para <xref:Microsoft.SqlServer.Replication.PullSubscription.DatabaseName%2A>.  
  
    -   El nombre de la publicación a la que pertenece la suscripción para <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationName%2A>.  
  
    -   El nombre de la base de datos publicada para <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationDBName%2A>.  
  
    -   El nombre del publicador para <xref:Microsoft.SqlServer.Replication.PullSubscription.PublisherName%2A>.  
  
    -   La conexión creada en el paso 1 para <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>.  
  
3.  Llame al método <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> para obtener las propiedades de suscripción restantes. Si este método devuelve `false`, compruebe que la suscripción existe.  
  
4.  Inicie el Agente de mezcla en el suscriptor de una de las maneras siguientes:  
  
    -   Llame al método <xref:Microsoft.SqlServer.Replication.MergePullSubscription.SynchronizeWithJob%2A> en la instancia de <xref:Microsoft.SqlServer.Replication.MergePullSubscription> del paso 2. Este método inicia el Agente de mezcla de forma asincrónica y controla inmediatamente las devoluciones a la aplicación mientras se está ejecutando el trabajo del agente. No puede llamar a este método para suscriptores de [!INCLUDE[ssExpressEd2005](../../includes/ssexpressed2005-md.md)] o si la suscripción se creó con un valor de `false` para <xref:Microsoft.SqlServer.Replication.PullSubscription.CreateSyncAgentByDefault%2A> (predeterminado).  
  
    -   Obtenga una instancia de la clase <xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent> de la propiedad <xref:Microsoft.SqlServer.Replication.MergePullSubscription.SynchronizationAgent%2A> y llame al método <xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent.Synchronize%2A>. Este método inicia el Agente de mezcla sincrónicamente y controla el resto con el trabajo del agente en ejecución. Durante la ejecución sincrónica, puede administrar el evento <xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent.Status> mientras el agente se está ejecutando.  
  
        > [!NOTE]  
        >  Si especificó un valor de `false` para <xref:Microsoft.SqlServer.Replication.PullSubscription.CreateSyncAgentByDefault%2A> (predeterminado) cuando creó la suscripción de extracción, también debe especificar <xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent.Distributor%2A> <xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent.DistributorSecurityMode%2A>,, <xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent.PublisherSecurityMode%2A>, <xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent.HostName%2A>, <xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent.SubscriptionType%2A>, <xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent.ExchangeType%2A>y, opcionalmente <xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent.DistributorLogin%2A>,, y, <xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent.DistributorPassword%2A> <xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent.PublisherLogin%2A> <xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent.PublisherPassword%2A> porque los metadatos relacionados con el trabajo del agente para la suscripción no están disponibles en [MSsubscription_properties](/sql/relational-databases/system-tables/mssubscription-properties-transact-sql).  
  
###  <a name="examples-rmo"></a><a name="PShellExample"></a>Ejemplos (RMO)  
 Este ejemplo sincroniza una suscripción de extracción con una publicación transaccional, en la que el agente se inicia de forma asincrónica con el trabajo del agente.  
  
 [!code-csharp[HowTo#rmo_SyncTranPullSub_WithJob](../../snippets/csharp/SQL15/replication/howto/cs/rmotestevelope.cs#rmo_synctranpullsub_withjob)]  
  
 [!code-vb[HowTo#rmo_vb_SyncTranPullSub_WithJob](../../snippets/visualbasic/SQL15/replication/howto/vb/rmotestenv.vb#rmo_vb_synctranpullsub_withjob)]  
  
 Este ejemplo sincroniza una suscripción de extracción con una publicación transaccional, en la que el agente se inicia sincrónicamente.  
  
 [!code-csharp[HowTo#rmo_SyncTranPullSub](../../snippets/csharp/SQL15/replication/howto/cs/rmotestevelope.cs#rmo_synctranpullsub)]  
  
 [!code-vb[HowTo#rmo_vb_SyncTranPullSub](../../snippets/visualbasic/SQL15/replication/howto/vb/rmotestenv.vb#rmo_vb_synctranpullsub)]  
  
 Este ejemplo sincroniza una suscripción de extracción con una publicación de combinación, en la que el agente se inicia de forma asincrónica con el trabajo del agente.  
  
 [!code-csharp[HowTo#rmo_SyncMergePullSub_WithJob](../../snippets/csharp/SQL15/replication/howto/cs/rmotestevelope.cs#rmo_syncmergepullsub_withjob)]  
  
 [!code-vb[HowTo#rmo_vb_SyncMergePullSub_WithJob](../../snippets/visualbasic/SQL15/replication/howto/vb/rmotestenv.vb#rmo_vb_syncmergepullsub_withjob)]  
  
 Este ejemplo sincroniza una suscripción de extracción con una publicación de combinación, en la que el agente se inicia sincrónicamente.  
  
 [!code-csharp[HowTo#rmo_SyncMergePullSub](../../snippets/csharp/SQL15/replication/howto/cs/rmotestevelope.cs#rmo_syncmergepullsub)]  
  
 [!code-vb[HowTo#rmo_vb_SyncMergePullSub](../../snippets/visualbasic/SQL15/replication/howto/vb/rmotestenv.vb#rmo_vb_syncmergepullsub)]  
  
 Este ejemplo sincroniza una suscripción de extracción con una publicación de combinación mediante la sincronización web. La suscripción se creó sin el trabajo del agente y los metadatos de suscripción relacionados, por lo que se debe iniciar el agente sincrónicamente y se proporciona información adicional acerca de la suscripción.  
  
 [!code-csharp[HowTo#rmo_SyncMergePullSub_NoJobWebSync](../../snippets/csharp/SQL15/replication/howto/cs/rmotestevelope.cs#rmo_syncmergepullsub_nojobwebsync)]  
  
 [!code-vb[HowTo#rmo_vb_SyncMergePullSub_NoJobWebSync](../../snippets/visualbasic/SQL15/replication/howto/vb/rmotestenv.vb#rmo_vb_syncmergepullsub_nojobwebsync)]  
  
## <a name="see-also"></a>Consulte también  
 [Sincronizar datos](synchronize-data.md)   
 [Create a Pull Subscription](create-a-pull-subscription.md)   
 [Prácticas recomendadas de seguridad de replicación](security/replication-security-best-practices.md)  
  
  
