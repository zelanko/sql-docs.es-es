---
title: "Crear una suscripci&#243;n de inserci&#243;n | Microsoft Docs"
ms.custom: ""
ms.date: "08/25/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "suscripciones de inserción [replicación de SQL Server], crear"
  - "suscribir replicación de mezcla [replicación de SQL Server], suscripciones de inserción"
  - "suscripciones [replicación de SQL Server], extraer"
  - "replicación de instantáneas [SQL Server], suscribir"
  - "replicación transaccional, suscribir"
ms.assetid: adfbbc61-58d1-4330-9ad6-b14ab1142e2b
caps.latest.revision: 41
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 41
---
# Crear una suscripci&#243;n de inserci&#243;n
  En este tema se describe cómo crear una suscripción de inserción en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] utilizando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../includes/tsql-md.md)], o Replication Management Objects (RMO). Para obtener información acerca de cómo crear una suscripción de inserción para no[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] suscriptor, consulte [crear una suscripción para un suscriptor que no son de SQL Server](../../relational-databases/replication/create-a-subscription-for-a-non-sql-server-subscriber.md).  
  
 
##  <a name="SSMSProcedure"></a> Usar SQL Server Management Studio  
 Cree una suscripción de inserción en el publicador o en el suscriptor con el Asistente para nuevas suscripciones. Siga las páginas del asistente para:  
  
-   Especificar el publicador y la publicación.  
  
-   Seleccionar dónde se ejecutarán los agentes de replicación. Para una suscripción de inserción, seleccione **ejecutar todos los agentes en el distribuidor (suscripciones de inserción)** en la **ubicación del agente de distribución** página o **ubicación del agente de mezcla** página, dependiendo del tipo de publicación.  
  
-   Especificar suscriptores y bases de datos de suscripciones.  
  
-   Especifique los nombres de inicio de sesión y las contraseñas que se utilizan para las conexiones realizadas por los agentes de replicación:  
  
    -   Para las suscripciones a publicaciones de instantáneas y transaccionales, especifique las credenciales en la página **Seguridad del Agente de distribución** .  
  
    -   Para las suscripciones a publicaciones de combinación, especifique las credenciales en la página **Seguridad del Agente de mezcla** .  
  
     Para obtener información acerca de los permisos requeridos por cada agente, consulte [modelo de seguridad del agente de replicación](../../relational-databases/replication/security/replication-agent-security-model.md).  
  
-   Especifique una programación de sincronización y cuándo se debe inicializar el suscriptor.  
  
-   Especifique otras opciones para las publicaciones de combinación: el tipo de suscripción y los valores para los filtros con parámetros.  
  
-   Especifique otras opciones para las publicaciones transaccionales que permitan actualizar suscripciones: si los suscriptores deben confirmar los cambios inmediatamente en el publicador o escribirlos en una cola; las credenciales que se emplean para conectarse desde el suscriptor al publicador.  
  
-   Opcionalmente, puede crear un script para la suscripción.  
  
#### Para crear una suscripción de inserción desde el publicador  
  
1.  Conéctese al publicador en [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]y, a continuación, expanda el nodo del servidor.  
  
2.  Expanda la carpeta **Replicación** y, a continuación, expanda la carpeta **Publicaciones locales** .  
  
3.  Haga clic en la publicación para el que desea crear una o varias suscripciones y, a continuación, haga clic en **nuevas suscripciones**.  
  
4.  Complete las páginas del Asistente para nuevas suscripciones.  
  
#### Para crear una suscripción de inserción desde el suscriptor  
  
1.  Conéctese al suscriptor en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]y expanda el nodo de servidor.  
  
2.  Expanda la carpeta **Replicación** .  
  
3.  Haga clic en el **suscripciones locales** carpeta y, a continuación, haga clic en **nuevas suscripciones**.  
  
4.  En el **publicación** página del Asistente de suscripción nueva, seleccione **\< buscar publicador de SQL Server>** o **\< buscar publicador de Oracle>** desde el **Publisher** lista desplegable.  
  
5.  Conéctese al publicador en el cuadro de diálogo **Conectar al servidor** .  
  
6.  Seleccione una publicación en la página **Publicación** .  
  
7.  Complete las páginas del Asistente para nuevas suscripciones.  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
 Las suscripciones de inserción pueden crearse mediante programación con procedimientos almacenados de replicación. Los procedimientos almacenados que se usen dependerán del tipo de publicación a la que corresponda la suscripción.  
  
> **IMPORTANTE:** Cuando sea posible, pida a los usuarios que proporcionen credenciales de seguridad en tiempo de ejecución. Si debe almacenar las credenciales en un archivo de script, proteja el archivo para evitar el acceso no autorizado.  
  
#### Para crear una suscripción de inserción para una publicación de instantáneas o transaccional  
  
1.  En el publicador de la base de datos de publicación, compruebe que la publicación admite suscripciones de inserción mediante la ejecución de [sp_helppublication](../../relational-databases/system-stored-procedures/sp-helppublication-transact-sql.md).  
  
    -   Si el valor de **allow_push** es **1**, se admiten suscripciones de inserción.  
  
    -   Si el valor de **allow_push** es **0**, ejecute [sp_changepublication](../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md), especificando **allow_push** para **@property** y **true** para **@value**.  
  
2.  En el publicador de la base de datos de publicación, ejecute [sp_addsubscription](https://msdn.microsoft.com/library/ms181702.aspx). Especifique **@publication**, **@subscriber** y **@destination_db**. Especifique un valor de **inserción** para **@subscription_type**. Para obtener información acerca de cómo actualizar las suscripciones, consulte [crear una suscripción actualizable a una publicación transaccional](https://msdn.microsoft.com/library/ms152769.aspx).  
  
3.  En el publicador de la base de datos de publicación, ejecute [sp_addpushsubscription_agent](../../relational-databases/system-stored-procedures/sp-addpushsubscription-agent-transact-sql.md). Especifique lo siguiente:  
  
    -   El **@subscriber**, **@subscriber_db**, y **@publication** parámetros.  
  
    -   El [!INCLUDE[msCoName](../../includes/msconame-md.md)] las credenciales de Windows bajo la que se ejecuta el agente de distribución en el distribuidor para **@job_login** y **@job_password**.  
  
        > **Nota:** las conexiones realizadas mediante la autenticación integrada de Windows siempre utilizan las credenciales de Windows especificadas por **@job_login** y **@job_password**. El Agente de distribución siempre realiza la conexión local con el distribuidor mediante la autenticación integrada de Windows. De forma predeterminada, el agente se conectará con el suscriptor mediante la autenticación integrada de Windows.  
  
    -   (Opcional) Un valor de **0** para **@subscriber_security_mode** y [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] información de inicio de sesión de **@subscriber_login** y **@subscriber_password**. Especifique estos parámetros si necesita usar Autenticación de SQL Server al conectarse al suscriptor.  
  
    -   Una programación para el trabajo del Agente de distribución de esta suscripción. Para obtener más información, consulte [Specify Synchronization Schedules](../../relational-databases/replication/specify-synchronization-schedules.md).  
  
    > **IMPORTANTE:** Al crear una suscripción de inserción en un publicador con un distribuidor remoto, los valores suministrados para todos los parámetros, incluidos *job_login* y *job_password*, se envían al distribuidor como texto sin formato. Antes de ejecutar este procedimiento almacenado, se recomienda cifrar la conexión entre el publicador y su distribuidor remoto. Para obtener más información, vea [Habilitar conexiones cifradas en el motor de base de datos &#40;Administrador de configuración de SQL Server&#41;](../../database-engine/configure-windows/enable encrypted connections to the database engine.md).  
  
#### Para crear una suscripción de inserción para una publicación de combinación  
  
1.  En el publicador de la base de datos de publicación, compruebe que la publicación admite suscripciones de inserción mediante la ejecución de [sp_helpmergepublication](../../relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql.md).  
  
    -   Si el valor de **allow_push** es **1**, la publicación admite suscripciones de inserción.  
  
    -   Si el valor de **allow_push** no **1**, ejecute [sp_changemergepublication](../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md), especificando **allow_push** para **@property** y **true** para **@value**.  
  
2.  En el publicador de la base de datos de publicación, ejecute [sp_addmergesubscription](../../relational-databases/system-stored-procedures/sp-addmergesubscription-transact-sql.md), especifique los siguientes parámetros:  
  
    -   **@publication**. Éste es el nombre de la publicación.  
  
    -   **@subscriber_type**. Para una suscripción de cliente, especifique **local** y para una suscripción de servidor, especifique **global**.  
  
    -   **@subscription_priority**. Para una suscripción de servidor, especifique una prioridad para la suscripción (**0,00** a **99,99**).  
  
         Para obtener más información, consulte [Advanced Merge Replication Conflict Detection and Resolution](../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md).  
  
3.  En el publicador de la base de datos de publicación, ejecute [sp_addmergepushsubscription_agent](../../relational-databases/system-stored-procedures/sp-addmergepushsubscription-agent-transact-sql.md). Especifique lo siguiente:  
  
    -   El **@subscriber**, **@subscriber_db**, y **@publication** parámetros.  
  
    -   Las credenciales de Windows en la que se ejecuta el agente de mezcla en el distribuidor para **@job_login** y **@job_password**.  
  
        > **Nota:**  las conexiones realizadas mediante la autenticación integrada de Windows siempre utilizan las credenciales de Windows especificadas por **@job_login** y **@job_password**. El Agente de mezcla siempre realiza la conexión local con el distribuidor mediante la Autenticación integrada de Windows. De forma predeterminada, el agente se conectará con el suscriptor mediante la autenticación integrada de Windows.  
  
    -   (Opcional) Un valor de **0** para **@subscriber_security_mode** y la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] información de inicio de sesión de **@subscriber_login** y **@subscriber_password**. Especifique estos parámetros si necesita usar Autenticación de SQL Server al conectarse al suscriptor.  
  
    -   (Opcional) Un valor de **0** para **@publisher_security_mode** y la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] información de inicio de sesión de **@publisher_login** y **@publisher_password**. Especifique estos valores si necesita usar Autenticación de SQL Server al conectarse al publicador.  
  
    -   Una programación para el Agente de mezcla para la suscripción. Para obtener más información, consulte [Specify Synchronization Schedules](../../relational-databases/replication/specify-synchronization-schedules.md).  
  
    > **IMPORTANTE:** Al crear una suscripción de inserción en un publicador con un distribuidor remoto, los valores suministrados para todos los parámetros, incluidos *job_login* y *job_password*, se envían al distribuidor como texto sin formato. Antes de ejecutar este procedimiento almacenado, se recomienda cifrar la conexión entre el publicador y su distribuidor remoto. Para obtener más información, vea [Habilitar conexiones cifradas en el motor de base de datos &#40;Administrador de configuración de SQL Server&#41;](../../database-engine/configure-windows/enable encrypted connections to the database engine.md).  
  
###  <a name="TsqlExample"></a> Ejemplos (Transact-SQL)  
 El siguiente ejemplo crea una suscripción de inserción en una publicación transaccional. Los valores de inicio de sesión y contraseña se proporcionan en tiempo de ejecución mediante variables de scripting de **sqlcmd** .  
  
 [!code-sql[HowTo#sp_addtranpushsubscription_agent](../../relational-databases/replication/codesnippet/tsql/create-a-push-subscription_1.sql)]  
  
 El siguiente ejemplo crea una suscripción de inserción en una publicación de combinación. Los valores de inicio de sesión y contraseña se proporcionan en tiempo de ejecución mediante variables de scripting de **sqlcmd** .  
  
 [!code-sql[HowTo#sp_addmergepushsubscriptionagent](../../relational-databases/replication/codesnippet/tsql/create-a-push-subscription_2.sql)]  
  
##  <a name="RMOProcedure"></a> Usar Replication Management Objects (RMO)  
 Las suscripciones de inserción se pueden crear mediante programación usando Replication Management Objects (RMO). Las clases RMO que se utilizan para crear una suscripción de inserción dependen del tipo de publicación para el que se crea la suscripción.  
  
> **IMPORTANTE:** Cuando sea posible, pida a los usuarios que proporcionen credenciales de seguridad en tiempo de ejecución. Si debe almacenar credenciales, use los [servicios de cifrado](http://go.microsoft.com/fwlink/?LinkId=34733) (en inglés) proporcionados por [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows .NET Framework.  
  
#### Para crear una suscripción de inserción para una publicación de instantáneas o transaccional  
  
1.  Crear una conexión al publicador mediante la <xref:Microsoft.SqlServer.Management.Common.ServerConnection> clase.  
  
2.  Cree una instancia de la <xref:Microsoft.SqlServer.Replication.TransPublication> clase mediante la conexión de publicador del paso 1. Especifique <xref:Microsoft.SqlServer.Replication.Publication.Name%2A>, <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A>, y <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>.  
  
3.  Llame a la <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> método. Si este método devuelve **false**, las propiedades especificadas en el paso 2 son incorrectas o la publicación no existe en el servidor.  
  
4.  Realizar una operación AND lógica bit a bit (**&** en Visual C# y **y** en Visual Basic) entre el <xref:Microsoft.SqlServer.Replication.Publication.Attributes%2A> propiedad y <xref:Microsoft.SqlServer.Replication.PublicationAttributes.AllowPush>. Si el resultado es <xref:Microsoft.SqlServer.Replication.PublicationAttributes.None>, establezca <xref:Microsoft.SqlServer.Replication.Publication.Attributes%2A> al resultado de una operación lógica OR bit a bit (**|** en Visual C# y **o** en Visual Basic) entre <xref:Microsoft.SqlServer.Replication.Publication.Attributes%2A> y <xref:Microsoft.SqlServer.Replication.PublicationAttributes.AllowPush>. A continuación, llame a <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> para habilitar las suscripciones de inserción.  
  
5.  Si la base de datos de suscripción no existe, se crea mediante la <xref:Microsoft.SqlServer.Management.Smo.Database> clase. Para obtener más información, consulte [creación, modificación y eliminación de bases de datos](../../relational-databases/server-management-objects-smo/tasks/creating-altering-and-removing-databases.md).  
  
6.  Cree una instancia de la <xref:Microsoft.SqlServer.Replication.TransSubscription> clase.  
  
7.  Establezca las siguientes propiedades de la suscripción:  
  
    -   El <xref:Microsoft.SqlServer.Management.Common.ServerConnection> en el publicador que creó en el paso 1 para <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>.  
  
    -   Nombre de la base de datos de suscripción para <xref:Microsoft.SqlServer.Replication.Subscription.SubscriptionDBName%2A>.  
  
    -   Nombre del suscriptor para <xref:Microsoft.SqlServer.Replication.Subscription.SubscriberName%2A>.  
  
    -   Nombre de la base de datos de publicación para <xref:Microsoft.SqlServer.Replication.Subscription.DatabaseName%2A>.  
  
    -   Nombre de la publicación de <xref:Microsoft.SqlServer.Replication.Subscription.PublicationName%2A>.  
  
    -   La <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Login%2A> y <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Password%2A> o <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.SecurePassword%2A> campos de <xref:Microsoft.SqlServer.Replication.Subscription.SynchronizationAgentProcessSecurity%2A> para proporcionar las credenciales para la [!INCLUDE[msCoName](../../includes/msconame-md.md)] cuenta de Windows bajo la que se ejecuta el agente de distribución en el distribuidor. Esta cuenta se utiliza para realizar conexiones locales al distribuidor y conexiones remotas con la autenticación de Windows.  
  
        > **Nota:** configuración <xref:Microsoft.SqlServer.Replication.Subscription.SynchronizationAgentProcessSecurity%2A> no es obligatorio cuando se crea la suscripción por un miembro de la **sysadmin** rol fijo de servidor, pero se recomienda. En este caso, el agente suplantará a la cuenta del Agente SQL Server. Para obtener más información, consulte [Replication Agent Security Model](../../relational-databases/replication/security/replication-agent-security-model.md).  
  
    -   (Opcional) Un valor de **true** (predeterminado) para <xref:Microsoft.SqlServer.Replication.Subscription.CreateSyncAgentByDefault%2A> para crear un trabajo de agente que se utiliza para sincronizar la suscripción. Si especifica **false**, la suscripción solo puede sincronizarse mediante programación.  
  
    -   (Opcional) Establecer el <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardLogin%2A> y <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardPassword%2A> o <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SecureSqlStandardPassword%2A> campos de <xref:Microsoft.SqlServer.Replication.Subscription.SubscriberSecurity%2A> cuando se utiliza autenticación de SQL Server para conectarse al suscriptor.  
  
8.  Llame a la <xref:Microsoft.SqlServer.Replication.Subscription.Create%2A> método.  
  
    > **IMPORTANTE!!**Al crear una suscripción de inserción en un publicador con un distribuidor remoto, los valores suministrados para todas las propiedades, incluyendo <xref:Microsoft.SqlServer.Replication.Subscription.SynchronizationAgentProcessSecurity%2A>, se envían al distribuidor como texto sin formato. Debe cifrar la conexión entre el publicador y el distribuidor remoto antes de llamar a la <xref:Microsoft.SqlServer.Replication.Subscription.Create%2A> método. Para obtener más información, vea [Habilitar conexiones cifradas en el motor de base de datos &#40;Administrador de configuración de SQL Server&#41;](../../database-engine/configure-windows/enable encrypted connections to the database engine.md).  
  
#### Para crear una suscripción de inserción para una publicación de combinación  
  
1.  Crear una conexión al publicador mediante la <xref:Microsoft.SqlServer.Management.Common.ServerConnection> clase.  
  
2.  Cree una instancia de la <xref:Microsoft.SqlServer.Replication.MergePublication> clase mediante la conexión de publicador del paso 1. Especifique <xref:Microsoft.SqlServer.Replication.Publication.Name%2A>, <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A>, y <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>.  
  
3.  Llame a la <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> método. Si este método devuelve **false**, las propiedades especificadas en el paso 2 son incorrectas o la publicación no existe en el servidor.  
  
4.  Realizar una operación AND lógica bit a bit (**&** en Visual C# y **y** en Visual Basic) entre el <xref:Microsoft.SqlServer.Replication.Publication.Attributes%2A> propiedad y <xref:Microsoft.SqlServer.Replication.PublicationAttributes.AllowPush>. Si el resultado es <xref:Microsoft.SqlServer.Replication.PublicationAttributes.None>, establezca <xref:Microsoft.SqlServer.Replication.Publication.Attributes%2A> al resultado de una operación lógica OR bit a bit (**|** en Visual C# y **o** en Visual Basic) entre <xref:Microsoft.SqlServer.Replication.Publication.Attributes%2A> y <xref:Microsoft.SqlServer.Replication.PublicationAttributes.AllowPush>. A continuación, llame a <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> para habilitar las suscripciones de inserción.  
  
5.  Si la base de datos de suscripción no existe, se crea mediante la <xref:Microsoft.SqlServer.Management.Smo.Database> clase. Para obtener más información, consulte [creación, modificación y eliminación de bases de datos](../../relational-databases/server-management-objects-smo/tasks/creating-altering-and-removing-databases.md).  
  
6.  Cree una instancia de la <xref:Microsoft.SqlServer.Replication.MergeSubscription> clase.  
  
7.  Establezca las siguientes propiedades de la suscripción:  
  
    -   El <xref:Microsoft.SqlServer.Management.Common.ServerConnection> en el publicador que creó en el paso 1 para <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>.  
  
    -   Nombre de la base de datos de suscripción para <xref:Microsoft.SqlServer.Replication.Subscription.SubscriptionDBName%2A>.  
  
    -   Nombre del suscriptor para <xref:Microsoft.SqlServer.Replication.Subscription.SubscriberName%2A>.  
  
    -   Nombre de la base de datos de publicación para <xref:Microsoft.SqlServer.Replication.Subscription.DatabaseName%2A>.  
  
    -   Nombre de la publicación de <xref:Microsoft.SqlServer.Replication.Subscription.PublicationName%2A>.  
  
    -   La <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Login%2A> y <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Password%2A> o <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.SecurePassword%2A> campos de <xref:Microsoft.SqlServer.Replication.Subscription.SynchronizationAgentProcessSecurity%2A> para proporcionar las credenciales para la [!INCLUDE[msCoName](../../includes/msconame-md.md)] cuenta de Windows bajo la que se ejecuta el agente de mezcla en el distribuidor. Esta cuenta se utiliza para realizar conexiones locales al distribuidor y conexiones remotas con la autenticación de Windows.  
  
        > **Nota:** configuración <xref:Microsoft.SqlServer.Replication.Subscription.SynchronizationAgentProcessSecurity%2A> no es obligatorio cuando se crea la suscripción por un miembro de la **sysadmin** rol fijo de servidor, pero se recomienda. En este caso, el agente suplantará a la cuenta del Agente SQL Server. Para obtener más información, consulte [Replication Agent Security Model](../../relational-databases/replication/security/replication-agent-security-model.md).  
  
    -   (Opcional) Un valor de **true** (predeterminado) para <xref:Microsoft.SqlServer.Replication.Subscription.CreateSyncAgentByDefault%2A> para crear un trabajo de agente que se utiliza para sincronizar la suscripción. Si especifica **false**, la suscripción solo puede sincronizarse mediante programación.  
  
    -   (Opcional) Establecer el <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardLogin%2A> y <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardPassword%2A> o <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SecureSqlStandardPassword%2A> campos de <xref:Microsoft.SqlServer.Replication.Subscription.SubscriberSecurity%2A> cuando se utiliza autenticación de SQL Server para conectarse al suscriptor.  
  
    -   (Opcional) Establecer el <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardLogin%2A> y <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardPassword%2A> o <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SecureSqlStandardPassword%2A> campos de <xref:Microsoft.SqlServer.Replication.PullSubscription.PublisherSecurity%2A> cuando se utiliza la autenticación de SQL Server para conectarse al publicador.  
  
8.  Llame a la <xref:Microsoft.SqlServer.Replication.Subscription.Create%2A> método.  
  
    > **IMPORTANTE:**  Al crear una suscripción de inserción en un publicador con un distribuidor remoto, los valores suministrados para todas las propiedades, incluyendo <xref:Microsoft.SqlServer.Replication.Subscription.SynchronizationAgentProcessSecurity%2A>, se envían al distribuidor como texto sin formato. Debe cifrar la conexión entre el publicador y el distribuidor remoto antes de llamar a la <xref:Microsoft.SqlServer.Replication.Subscription.Create%2A> método. Para obtener más información, vea [Habilitar conexiones cifradas en el motor de base de datos &#40;Administrador de configuración de SQL Server&#41;](../../database-engine/configure-windows/enable encrypted connections to the database engine.md).  
  
###  <a name="PShellExample"></a> Ejemplos (RMO)  
 En este ejemplo se crea una suscripción de inserción para una publicación transaccional. Las credenciales de la cuenta de Windows utilizada para ejecutar el trabajo del Agente de distribución se pasan en tiempo de ejecución.  
  
 [!code-csharp[HowTo#rmo_CreateTranPushSub](../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_createtranpushsub)]  
  
 [!code-vb[HowTo#rmo_vb_CreateTranPushSub](../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_createtranpushsub)]  
  
 En este ejemplo se crea una suscripción de inserción para una publicación de combinación. Las credenciales de la cuenta de Windows utilizada para ejecutar el trabajo del Agente de mezcla se pasan en tiempo de ejecución.  
  
 [!code-csharp[HowTo#rmo_CreateMergePushSub](../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_createmergepushsub)]  
  
 [!code-vb[HowTo#rmo_vb_CreateMergePushSub](../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_createmergepushsub)]  
  
## Vea también  
 [Ver y modificar las propiedades de una suscripción de inserción](../../relational-databases/replication/view-and-modify-push-subscription-properties.md)   
 [Prácticas recomendadas de seguridad de replicación](../../relational-databases/replication/security/replication-security-best-practices.md)   
 [Crear una publicación](../../relational-databases/replication/publish/create-a-publication.md)   
 [Conceptos de los Replication Management Objects (RMO)](../../relational-databases/replication/concepts/replication-management-objects-concepts.md)   
 [Sincronizar una suscripción de inserción](../../relational-databases/replication/synchronize-a-push-subscription.md)   
 [Suscribirse a publicaciones](../../relational-databases/replication/subscribe-to-publications.md)   
 [Usar sqlcmd con variables de script](../../relational-databases/scripting/use-sqlcmd-with-scripting-variables.md)  
  
  