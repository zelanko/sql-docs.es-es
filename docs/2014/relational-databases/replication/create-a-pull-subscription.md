---
title: Creación de una suscripción de extracción | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- pull subscriptions [SQL Server replication], creating
- merge replication subscribing [SQL Server replication], pull subscriptions
- subscriptions [SQL Server replication], pull
- snapshot replication [SQL Server], subscribing
- transactional replication, subscribing
ms.assetid: 41d1886d-59c9-41fc-9bd6-a59b40e0af6e
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: f8868957d7c479de3a51a599deed42c34d6676eb
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62721597"
---
# <a name="create-a-pull-subscription"></a>Crear una suscripción de extracción
  En este tema se describe cómo crear una suscripción de extracción en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../includes/tsql-md.md)]o Replication Management Objects (RMO).  
  
 Es posible configurar una suscripción de extracción para la replicación P2P mediante un script, pero no está disponible a través del asistente.  
  
  
##  <a name="SSMSProcedure"></a> Usar SQL Server Management Studio  
 Cree una suscripción de extracción en el publicador o suscriptor con el Asistente para nuevas suscripciones. Siga las páginas del asistente para:  
  
-   Especificar el publicador y la publicación.  
  
-   Seleccionar dónde se ejecutarán los agentes de replicación. En una suscripción de extracción, seleccione **Ejecutar cada agente en su suscriptor (suscripciones de extracción)** en la página **Ubicación del Agente de distribución** o en la página **Ubicación del Agente de mezcla** , dependiendo del tipo de publicación.  
  
-   Especificar suscriptores y bases de datos de suscripciones.  
  
-   Especifique los nombres de inicio de sesión y las contraseñas que se utilizan para las conexiones realizadas por los agentes de replicación:  
  
    -   Para las suscripciones a publicaciones de instantáneas y transaccionales, especifique las credenciales en la página **Seguridad del Agente de distribución** .  
  
    -   Para las suscripciones a publicaciones de combinación, especifique las credenciales en la página **Seguridad del Agente de mezcla** .  
  
     Para obtener información acerca de los permisos que necesita cada agente, vea [Modelo de seguridad del agente de replicación](security/replication-agent-security-model.md).  
  
-   Especifique una programación de sincronización y cuándo se debe inicializar el suscriptor.  
  
-   Especifique opciones adicionales para publicaciones de combinación: el tipo de suscripción, los valores para el filtro con parámetros y la información para la sincronización mediante HTTPS si la publicación está habilitada para sincronización web.  
  
-   Especifique otras opciones para las publicaciones transaccionales que permitan actualizar suscripciones: si los suscriptores deben confirmar los cambios inmediatamente en el publicador o escribirlos en una cola; las credenciales que se emplean para conectarse desde el suscriptor al publicador.  
  
-   Opcionalmente, puede crear un script para la suscripción.  
  
#### <a name="to-create-a-pull-subscription-from-the-publisher"></a>Para crear una suscripción de extracción desde el publicador  
  
1.  Conéctese al publicador en [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]y, a continuación, expanda el nodo del servidor.  
  
2.  Expanda la carpeta **Replicación** y, a continuación, expanda la carpeta **Publicaciones locales** .  
  
3.  Haga clic con el botón secundario en la publicación en la que desea crear una o varias suscripciones y, a continuación, haga clic en **Nuevas suscripciones**.  
  
4.  Complete las páginas del Asistente para nuevas suscripciones.  
  
#### <a name="to-create-a-pull-subscription-from-the-subscriber"></a>Para crear una suscripción de extracción desde el suscriptor  
  
1.  Conéctese al suscriptor en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]y expanda el nodo de servidor.  
  
2.  Expanda la carpeta **Replicación** .  
  
3.  Haga clic con el botón secundario en la carpeta **Suscripciones locales** y, a continuación, haga clic en **Nuevas suscripciones**.  
  
4.  En la página **Publicación** del Asistente para nuevas suscripciones, seleccione **\<Buscar publicador de SQL Server>** o **\<Buscar publicador de Oracle>** de la lista desplegable **Publicador**.  
  
5.  Conéctese al publicador en el cuadro de diálogo **Conectar al servidor** .  
  
6.  Seleccione una publicación en la página **Publicación** .  
  
7.  Complete las páginas del Asistente para nuevas suscripciones.  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
 Las suscripciones de extracción pueden crearse mediante programación con procedimientos almacenados de replicación. Los procedimientos almacenados que se usen dependerán del tipo de publicación a la que corresponda la suscripción.  
  
#### <a name="to-create-a-pull-subscription-to-a-snapshot-or-transactional-publication"></a>Para crear una suscripción de extracción para una publicación de instantáneas o transaccional  
  
1.  En el publicador, ejecute [sp_helppublication &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-helppublication-transact-sql) para comprobar que la publicación admite las suscripciones de extracción.  
  
    -   Si el valor de **allow_pull** del conjunto de resultados es **1**, la publicación admite las suscripciones de extracción.  
  
    -   Si el valor de **allow_pull** es **0**, ejecute [sp_changepublication &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-changepublication-transact-sql), especificando **allow_pull**para **@property** y `true` para **@value**.  
  
2.  En el suscriptor, ejecute [sp_addpullsubscription &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addpullsubscription-transact-sql). Especifique **@publisher** y **@publication**. Para obtener información sobre cómo actualizar suscripciones, vea [Crear una suscripción actualizable en una publicación transacciona](publish/create-an-updatable-subscription-to-a-transactional-publication.md).  
  
3.  En el suscriptor, ejecute [sp_addpullsubscription_agent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql). Especifique lo siguiente:  
  
    -   Los parámetros **@publisher**, **@publisher_db**y **@publication** .  
  
    -   Los parámetros [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows con las que se ejecuta el Agente de distribución en el suscriptor para **@job_login** y **@job_password**.  
  
        > [!NOTE]  
        >  Las conexiones que se realicen con la Autenticación integrada de Windows siempre usan las credenciales de Windows especificadas por **@job_login** y **@job_password**. El Agente de distribución siempre realiza la conexión local con el suscriptor mediante la autenticación integrada de Windows. De forma predeterminada, el agente se conectará con el distribuidor mediante la autenticación de Windows integrada.  
  
    -   (Opcional) Un valor de **0** para **@distributor_security_mode** y [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] información de inicio de sesión para **@distributor_login** y **@distributor_password**, si necesita usar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticación al conectarse al distribuidor.  
  
    -   Una programación para el trabajo del Agente de distribución de esta suscripción. Para obtener más información, consulte [Specify Synchronization Schedules](specify-synchronization-schedules.md).  
  
4.  En la base de datos de publicación del publicador, ejecute [sp_addsubscription &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addsubscription-transact-sql) para registrar la suscripción de extracción. Especifique **@publication**, **@subscriber**y **@destination_db**. Especifique un valor **pull** para **@subscription_type**.  
  
#### <a name="to-create-a-pull-subscription-to-a-merge-publication"></a>Para crear una suscripción de extracción para una publicación de combinación  
  
1.  En el publicador, ejecute [sp_helpmergepublication &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql) para comprobar que la publicación admite las suscripciones de extracción.  
  
    -   Si el valor de **allow_pull** del conjunto de resultados es **1**, la publicación admite las suscripciones de extracción.  
  
    -   Si el valor de **allow_pull** es **0**, ejecute [sp_changemergepublication &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql), especificando **allow_pull** para **@property** y `true` para **@value**.  
  
2.  En el suscriptor, ejecute [sp_addmergepullsubscription &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addmergepullsubscription-transact-sql). Especifique **@publisher**, **@publisher_db**, **@publication**y los parámetros siguientes:  
  
    -   **@subscriber_type**: especifique **local** para una suscripción de cliente y **global** para una suscripción de servidor.  
  
    -   **@subscription_priority**: especifique una prioridad para la suscripción (**0,00** a **99,99**). Solo es necesario para las suscripciones de servidor.  
  
         Para más información, consulte [Detección y resolución de conflictos de replicación de mezcla avanzada](merge/advanced-merge-replication-conflict-detection-and-resolution.md).  
  
3.  En el suscriptor, ejecute [sp_addmergepullsubscription_agent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql). Especifique los parámetros siguientes:  
  
    -   **@publisher**, **@publisher_db**y **@publication**.  
  
    -   Las credenciales de Windows con las que se ejecuta el Agente de mezcla en el suscriptor para **@job_login** y **@job_password**.  
  
        > [!NOTE]  
        >  Las conexiones que se realicen con la Autenticación integrada de Windows siempre usan las credenciales de Windows especificadas por **@job_login** y **@job_password**. El Agente de mezcla siempre realiza la conexión local con el suscriptor mediante la autenticación de Windows integrada. De forma predeterminada, el agente se conectará con el distribuidor mediante la autenticación de Windows integrada.  
  
    -   (Opcional) El valor **0** para **@distributor_security_mode** y la información de inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para **@distributor_login** y **@distributor_password**, si necesita utilizar la autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] al conectarse al distribuidor.  
  
    -   (Opcional) El valor **0** para **@publisher_security_mode** y la información de inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para **@publisher_login** y **@publisher_password**, si necesita utilizar la autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] al conectarse al publicador.  
  
    -   Una programación para el Agente de mezcla para la suscripción. Para más información, consulte [Crear una suscripción actualizable en una publicación transaccional](publish/create-an-updatable-subscription-to-a-transactional-publication.md).  
  
4.  En el publicador, ejecute [sp_addmergesubscription &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addmergesubscription-transact-sql). Especifique **@publication**, **@subscriber**, **@subscriber_db**y un valor de **pull** para **@subscription_type**. Esto registra la suscripción de extracción.  
  
###  <a name="TsqlExample"></a> Ejemplos (Transact-SQL)  
 El siguiente ejemplo crea una suscripción de extracción en una publicación transaccional. El primer lote se ejecuta en el suscriptor y el segundo lote se ejecuta en el publicador. Los valores de inicio de sesión y contraseña se proporcionan en tiempo de ejecución mediante variables de scripting de sqlcmd.  
  
 [!code-sql[HowTo#sp_addtranpullsubscriptionagent](../../snippets/tsql/SQL15/replication/howto/tsql/createtranpullsub.sql#sp_addtranpullsubscriptionagent)]  
  
 [!code-sql[HowTo#sp_addtranpullsubscription](../../snippets/tsql/SQL15/replication/howto/tsql/createtranpullsub.sql#sp_addtranpullsubscription)]  
  
 El siguiente ejemplo crea una suscripción de extracción en una publicación de combinación. El primer lote se ejecuta en el suscriptor y el segundo lote se ejecuta en el publicador. Los valores de inicio de sesión y contraseña se proporcionan en tiempo de ejecución mediante variables de scripting de **sqlcmd** .  
  
 [!code-sql[HowTo#sp_addmergepullsubscriptionagent](../../snippets/tsql/SQL15/replication/howto/tsql/createmergepullsub.sql#sp_addmergepullsubscriptionagent)]  
  
 [!code-sql[HowTo#sp_addmergepullsubscription](../../snippets/tsql/SQL15/replication/howto/tsql/createmergepullsub.sql#sp_addmergepullsubscription)]  
  
##  <a name="RMOProcedure"></a> Usar Replication Management Objects (RMO)  
 Las clases RMO que se utilizan para crear una suscripción de extracción dependen del tipo de publicación al que pertenece la suscripción.  
  
#### <a name="to-create-a-pull-subscription-to-a-snapshot-or-transactional-publication"></a>Para crear una suscripción de extracción para una publicación de instantáneas o transaccional  
  
1.  Cree conexiones tanto al Suscriptor como al Publicador con la clase <xref:Microsoft.SqlServer.Management.Common.ServerConnection> .  
  
2.  Cree una instancia de la clase <xref:Microsoft.SqlServer.Replication.TransPublication> con la conexión de publicador del paso 1. Especifique <xref:Microsoft.SqlServer.Replication.Publication.Name%2A>, <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A> y <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>.  
  
3.  Llame al método <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A>. Si este método devuelve `false`, las propiedades especificadas en el paso 2 son incorrectas o la publicación no existe en el servidor.  
  
4.  Ejecuta una operación lógica AND bit a bit (`&` en Visual C# y `And` en Visual Basic) entre la propiedad <xref:Microsoft.SqlServer.Replication.Publication.Attributes%2A> y <xref:Microsoft.SqlServer.Replication.PublicationAttributes.AllowPull>. Si el resultado es <xref:Microsoft.SqlServer.Replication.PublicationAttributes.None>, establezca <xref:Microsoft.SqlServer.Replication.Publication.Attributes%2A> en el resultado de una operación lógica OR bit a bit (`|` en Visual C# y `Or` en Visual Basic) entre <xref:Microsoft.SqlServer.Replication.Publication.Attributes%2A> y <xref:Microsoft.SqlServer.Replication.PublicationAttributes.AllowPull>. A continuación, llame a <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> para habilitar las suscripciones de extracción.  
  
5.  Si la base de datos de suscripciones no existe, créela con la clase <xref:Microsoft.SqlServer.Management.Smo.Database> . Para obtener más información, consulte [Crear, modificar y eliminar bases de datos](../server-management-objects-smo/tasks/creating-altering-and-removing-databases.md).  
  
6.  Cree una instancia de la clase <xref:Microsoft.SqlServer.Replication.TransPullSubscription> .  
  
7.  Establezca las siguientes propiedades de la suscripción:  
  
    -   La conexión <xref:Microsoft.SqlServer.Management.Common.ServerConnection> al Suscriptor creada en el paso 1 para <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>.  
  
    -   El nombre de la base de datos de suscripciones para <xref:Microsoft.SqlServer.Replication.PullSubscription.DatabaseName%2A>.  
  
    -   El nombre del publicador para <xref:Microsoft.SqlServer.Replication.PullSubscription.PublisherName%2A>.  
  
    -   El nombre de la base de datos de publicaciones para <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationDBName%2A>.  
  
    -   El nombre de la publicación para <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationName%2A>.  
  
    -   Los campos <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Login%2A> y <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Password%2A> o <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.SecurePassword%2A> de <xref:Microsoft.SqlServer.Replication.PullSubscription.SynchronizationAgentProcessSecurity%2A> para proporcionar las credenciales para la cuenta de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows con la que se ejecuta el Agente de distribución en el suscriptor. Esta cuenta se utiliza para realizar conexiones locales al suscriptor y conexiones remotas con la autenticación de Windows.  
  
        > [!NOTE]  
        >  No es necesario configurar <xref:Microsoft.SqlServer.Replication.PullSubscription.SynchronizationAgentProcessSecurity%2A> cuando un miembro del rol fijo de servidor `sysadmin` crea la suscripción; sin embargo, es recomendable. En este caso, el agente suplantará a la cuenta del Agente SQL Server. Para más información, consulte [Modelo de seguridad del agente de replicación](security/replication-agent-security-model.md).  
  
    -   (Opcional) El valor `true` para <xref:Microsoft.SqlServer.Replication.PullSubscription.CreateSyncAgentByDefault%2A> para crear un trabajo de agente que se utilice para sincronizar la suscripción. Si especifica `false` (el valor predeterminado), solamente se puede sincronizar la suscripción mediante programación y deberá especificar las propiedades adicionales del <xref:Microsoft.SqlServer.Replication.TransSynchronizationAgent> cuando obtenga acceso a este objeto desde la propiedad <xref:Microsoft.SqlServer.Replication.TransPullSubscription.SynchronizationAgent%2A>. Para obtener más información, consulte [Synchronize a Pull Subscription](synchronize-a-pull-subscription.md).  
  
        > [!NOTE]  
        >  Agente SQL Server no está disponible en todas las ediciones de [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obtener una lista de las características admitidas por las ediciones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vea [Features Supported by the Editions of SQL Server 2014](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md). Cuando se especifica el valor `true` para suscriptores de Express, no se crea el trabajo de agente. Sin embargo, los metadatos importantes relacionados con la suscripción se almacenan en el suscriptor.  
  
    -   (Opcional) Configure los campos <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardLogin%2A> y <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardPassword%2A> o <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SecureSqlStandardPassword%2A> de <xref:Microsoft.SqlServer.Replication.PullSubscription.DistributorSecurity%2A> si utiliza la autenticación de SQL Server para conectarse al distribuidor.  
  
8.  Llame al método <xref:Microsoft.SqlServer.Replication.PullSubscription.Create%2A> .  
  
9. Mediante la instancia de la clase <xref:Microsoft.SqlServer.Replication.TransPublication> del paso 2, llame al método <xref:Microsoft.SqlServer.Replication.TransPublication.MakePullSubscriptionWellKnown%2A> para registrar la suscripción de extracción con el publicador. Si este registro ya existe, se produce una excepción.  
  
#### <a name="to-create-a-pull-subscription-to-a-merge-publication"></a>Para crear una suscripción de extracción para una publicación de combinación  
  
1.  Cree conexiones tanto al suscriptor como al publicador con la clase <xref:Microsoft.SqlServer.Management.Common.ServerConnection> .  
  
2.  Cree una instancia de la clase <xref:Microsoft.SqlServer.Replication.MergePublication> con la conexión de publicador del paso 1. Especifique <xref:Microsoft.SqlServer.Replication.Publication.Name%2A>, <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A>y <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>.  
  
3.  Llame al método <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A>. Si este método devuelve `false`, las propiedades especificadas en el paso 2 son incorrectas o la publicación no existe en el servidor.  
  
4.  Ejecuta una operación lógica AND bit a bit (`&` en Visual C# y `And` en Visual Basic) entre la propiedad <xref:Microsoft.SqlServer.Replication.Publication.Attributes%2A> y <xref:Microsoft.SqlServer.Replication.PublicationAttributes.AllowPull>. Si el resultado es <xref:Microsoft.SqlServer.Replication.PublicationAttributes.None>, establezca <xref:Microsoft.SqlServer.Replication.Publication.Attributes%2A> en el resultado de una operación lógica OR bit a bit (`|` en Visual C# y `Or` en Visual Basic) entre <xref:Microsoft.SqlServer.Replication.Publication.Attributes%2A> y <xref:Microsoft.SqlServer.Replication.PublicationAttributes.AllowPull>. A continuación, llame a <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> para habilitar las suscripciones de extracción.  
  
5.  Si la base de datos de suscripciones no existe, créela con la clase <xref:Microsoft.SqlServer.Management.Smo.Database> . Para obtener más información, consulte [Crear, modificar y eliminar bases de datos](../server-management-objects-smo/tasks/creating-altering-and-removing-databases.md).  
  
6.  Cree una instancia de la clase <xref:Microsoft.SqlServer.Replication.MergePullSubscription> .  
  
7.  Establezca las siguientes propiedades de la suscripción:  
  
    -   La conexión <xref:Microsoft.SqlServer.Management.Common.ServerConnection> al Suscriptor creada en el paso 1 para <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>.  
  
    -   El nombre de la base de datos de suscripciones para <xref:Microsoft.SqlServer.Replication.PullSubscription.DatabaseName%2A>.  
  
    -   El nombre del publicador para <xref:Microsoft.SqlServer.Replication.PullSubscription.PublisherName%2A>.  
  
    -   El nombre de la base de datos de publicaciones para <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationDBName%2A>.  
  
    -   El nombre de la publicación para <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationName%2A>.  
  
    -   Los campos <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Login%2A> y <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Password%2A> o <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.SecurePassword%2A> de <xref:Microsoft.SqlServer.Replication.PullSubscription.SynchronizationAgentProcessSecurity%2A> para proporcionar las credenciales para la cuenta de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows con la que se ejecuta el Agente de mezcla en el suscriptor. Esta cuenta se utiliza para realizar conexiones locales al suscriptor y conexiones remotas con la autenticación de Windows.  
  
        > [!NOTE]  
        >  No es necesario configurar <xref:Microsoft.SqlServer.Replication.PullSubscription.SynchronizationAgentProcessSecurity%2A> cuando un miembro del rol fijo de servidor `sysadmin` crea la suscripción; sin embargo, es recomendable. En este caso, el agente suplantará a la cuenta del Agente SQL Server. Para más información, consulte [Modelo de seguridad del agente de replicación](security/replication-agent-security-model.md).  
  
    -   (Opcional) El valor `true` para <xref:Microsoft.SqlServer.Replication.PullSubscription.CreateSyncAgentByDefault%2A> para crear un trabajo de agente que se utilice para sincronizar la suscripción. Si especifica `false` (el valor predeterminado), solamente se puede sincronizar la suscripción mediante programación y deberá especificar las propiedades adicionales del <xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent> cuando obtenga acceso a este objeto desde la propiedad <xref:Microsoft.SqlServer.Replication.MergePullSubscription.SynchronizationAgent%2A>. Para obtener más información, consulte [Synchronize a Pull Subscription](synchronize-a-pull-subscription.md).  
  
    -   (Opcional) Configure los campos <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardLogin%2A> y <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardPassword%2A> o <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SecureSqlStandardPassword%2A> de <xref:Microsoft.SqlServer.Replication.PullSubscription.DistributorSecurity%2A> si utiliza la autenticación de SQL Server para conectarse al distribuidor.  
  
    -   (Opcional) configure los campos <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardLogin%2A> y <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardPassword%2A> o <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SecureSqlStandardPassword%2A> de <xref:Microsoft.SqlServer.Replication.PullSubscription.PublisherSecurity%2A> si utiliza la autenticación de SQL Server para conectarse al publicador.  
  
8.  Llame al método <xref:Microsoft.SqlServer.Replication.PullSubscription.Create%2A> .  
  
9. Mediante la instancia de la clase <xref:Microsoft.SqlServer.Replication.MergePublication> del paso 2, llame al método <xref:Microsoft.SqlServer.Replication.MergePublication.MakePullSubscriptionWellKnown%2A> para registrar la suscripción de extracción con el publicador. Si este registro ya existe, se produce una excepción.  
  
###  <a name="PShellExample"></a> Ejemplo (RMO)  
 En este ejemplo se crea una suscripción de extracción para una publicación transaccional. Las credenciales de la cuenta de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows utilizada para crear el trabajo del Agente de distribución se pasan en tiempo de ejecución.  
  
 [!code-csharp[HowTo#rmo_CreateTranPullSub](../../snippets/csharp/SQL15/replication/howto/cs/rmotestevelope.cs#rmo_createtranpullsub)]  
  
 [!code-vb[HowTo#rmo_vb_CreateTranPullSub](../../snippets/visualbasic/SQL15/replication/howto/vb/rmotestenv.vb#rmo_vb_createtranpullsub)]  
  
 En este ejemplo se crea una suscripción de extracción para una publicación de combinación. Las credenciales de la cuenta de Windows utilizada para crear el trabajo del Agente de mezcla se pasan en tiempo de ejecución.  
  
 [!code-csharp[HowTo#rmo_CreateMergePullSub](../../snippets/csharp/SQL15/replication/howto/cs/rmotestevelope.cs#rmo_createmergepullsub)]  
  
 [!code-vb[HowTo#rmo_vb_CreateMergePullSub](../../snippets/visualbasic/SQL15/replication/howto/vb/rmotestenv.vb#rmo_vb_createmergepullsub)]  
  
 Este ejemplo crea una suscripción de extracción a una publicación de combinación sin crear un trabajo de agente asociado ni metadatos de la suscripción en [MSsubscription_properties](/sql/relational-databases/system-tables/mssubscription-properties-transact-sql). Las credenciales de la cuenta de Windows utilizada para crear el trabajo del Agente de mezcla se pasan en tiempo de ejecución.  
  
 [!code-csharp[HowTo#rmo_CreateMergePullSub_NoJob](../../snippets/csharp/SQL15/replication/howto/cs/rmotestevelope.cs#rmo_createmergepullsub_nojob)]  
  
 [!code-vb[HowTo#rmo_vb_CreateMergePullSub_NoJob](../../snippets/visualbasic/SQL15/replication/howto/vb/rmotestenv.vb#rmo_vb_createmergepullsub_nojob)]  
  
 Este ejemplo crea una suscripción de extracción a una publicación de combinación que se puede sincronizar por Internet utilizando la sincronización web. Las credenciales de la cuenta de Windows utilizada para crear el trabajo del Agente de mezcla se pasan en tiempo de ejecución. Para más información, consulte [Configure Web Synchronization](configure-web-synchronization.md).  
  
 [!code-csharp[HowTo#rmo_CreateMergePullSub_WebSync](../../snippets/csharp/SQL15/replication/howto/cs/rmotestevelope.cs#rmo_createmergepullsub_websync)]  
  
 [!code-vb[HowTo#rmo_vb_CreateMergePullSub_WebSync](../../snippets/visualbasic/SQL15/replication/howto/vb/rmotestenv.vb#rmo_vb_createmergepullsub_websync)]  
  
## <a name="see-also"></a>Ver también  
 [Replication Management Objects Concepts](concepts/replication-management-objects-concepts.md)   
 [View and Modify Pull Subscription Properties](view-and-modify-pull-subscription-properties.md)  (Ver y modificar las propiedades de una suscripción de extracción)  
 [Configurar sincronización web](configure-web-synchronization.md)   
 [Subscribe to Publications](subscribe-to-publications.md)   
 [Prácticas recomendadas de seguridad de replicación](security/replication-security-best-practices.md)  
  
  
