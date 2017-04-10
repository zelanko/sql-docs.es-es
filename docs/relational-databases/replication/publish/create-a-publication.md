---
title: "Crear una publicaci&#243;n | Microsoft Docs"
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
  - "publicaciones [replicación de SQL Server], crear"
  - "artículos [replicación de SQL Server], definir"
  - "agregar artículos"
  - "artículos [replicación de SQL Server], agregar"
ms.assetid: 52ee6de9-1d58-4cb9-8711-372bddbe7154
caps.latest.revision: 44
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 44
---
# Crear una publicaci&#243;n
  En este tema se describe cómo crear una publicación en [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../../includes/tsql-md.md)] o Replication Management Objects (RMO).  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Limitaciones y restricciones](#Restrictions)  
  
     [Seguridad](#Security)  
  
-   **Para crear una publicación y definir artículos con:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [Replication Management Objects (RMO)](#RMOProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="Restrictions"></a> Limitaciones y restricciones  
  
-   Nombres de publicaciones y artículos no pueden incluir ninguno de los caracteres siguientes: %, \* , [,], |,:, "¿,? , ' , \ , / , \< , >. Si los objetos de la base de datos incluyen cualquiera de estos caracteres y desea replicarlos, debe especificar un nombre de artículo que es diferente del nombre del objeto en la **Propiedades del artículo: \< artículo>** cuadro de diálogo, que está disponible en la **artículos** página del asistente.  
  
###  <a name="Security"></a> Seguridad  
 Cuando sea posible, pida a los usuarios que proporcionen credenciales de seguridad en tiempo de ejecución. Si debe almacenar credenciales, use los [servicios de cifrado](http://go.microsoft.com/fwlink/?LinkId=34733) (en inglés) proporcionados por [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows .NET Framework.  
  
##  <a name="SSMSProcedure"></a> Usar SQL Server Management Studio  
 Cree publicaciones y defina artículos con el Asistente para nueva publicación. Después de crea una publicación, ver y modificar propiedades de la publicación en la **Propiedades de la publicación - \< publicación>** cuadro de diálogo. Para obtener información acerca de cómo crear una publicación de una base de datos de Oracle, vea [crear una publicación de una base de datos de Oracle](../../../relational-databases/replication/publish/create-a-publication-from-an-oracle-database.md).  
  
#### Para crear publicaciones y definir artículos  
  
1.  Conéctese al publicador en [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]y, a continuación, expanda el nodo del servidor.  
  
2.  Expanda el **replicación** carpeta y, a continuación, con el botón secundario del **publicaciones locales** carpeta.  
  
3.  Haga clic en **Nueva publicación**.  
  
4.  Siga las indicaciones de las páginas del Asistente para nueva publicación para:  
  
    -   Especificar un distribuidor si la distribución no se ha configurado en el servidor. Para obtener más información acerca de cómo configurar la distribución, consulte [Configurar publicación y distribución](../../../relational-databases/replication/configure-publishing-and-distribution.md).  
  
         Si se especifica en el **distribuidor** página que el servidor del publicador actuará como su propio distribuidor (distribuidor local) y el servidor no está configurado como distribuidor, el Asistente para nueva publicación configurará el servidor. Especifique una carpeta de instantáneas predeterminada para el distribuidor en la página **Carpeta de instantáneas** . La carpeta de instantáneas es simplemente un directorio designado como recurso compartido; los agentes que leen y escriben en esta carpeta deben tener permisos de acceso suficientes a ella. Para obtener más información acerca de cómo proteger la carpeta adecuadamente, consulte [proteger la carpeta de instantáneas](../../../relational-databases/replication/security/secure-the-snapshot-folder.md).  
  
         Si especifica que otro servidor actúe como distribuidor, deberá escribir una contraseña en la página **Contraseña administrativa** para las conexiones que se realicen desde el publicador al distribuidor. Esta contraseña debe coincidir con la especificada cuando se habilitó el publicador en el distribuidor remoto.  
  
         Para obtener más información, consulte [Configurar distribución](../../../relational-databases/replication/configure-distribution.md).  
  
    -   Elegir una base de datos de publicación.  
  
    -   Seleccionar un tipo de publicación. Para obtener más información, consulte [tipos de replicación](../../../relational-databases/replication/types-of-replication.md).  
  
    -   Especificar los datos y los objetos de base de datos que se van a publicar; de forma opcional, filtrar columnas de artículos de tablas y establecer las propiedades de los artículos.  
  
    -   De forma opcional, filtrar filas de artículos de tablas. Para obtener más información, consulte [filtrar datos publicados](../../../relational-databases/replication/publish/filter-published-data.md).  
  
    -   Establecer la programación del Agente de instantáneas.  
  
    -   Especificar las credenciales con las que los siguientes agentes de replicación se ejecutan y efectúan conexiones:  
  
         \- Agente de instantáneas para todas las publicaciones.  
  
         \- Agente de lector del registro para todas las publicaciones transaccionales.  
  
         \- Agente de lectura de cola para publicaciones transaccionales que permiten suscripciones de actualización.  
  
         Para obtener más información, consulte [Replication Agent Security Model](../../../relational-databases/replication/security/replication-agent-security-model.md) y [Replication Security Best Practices](../../../relational-databases/replication/security/replication-security-best-practices.md).  
  
    -   De forma opcional, incluir la publicación. Para más información, consulte [Scripting Replication](../../../relational-databases/replication/scripting-replication.md).  
  
    -   Especificar un nombre para la publicación.  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
 Las publicaciones pueden crearse mediante programación con procedimientos almacenados de replicación. Los procedimientos almacenados que se usen dependerán del tipo de publicación creado.  
  
#### Para crear una publicación transaccional o de instantáneas  
  
1.  En el publicador de la base de datos de publicación, ejecute [sp_replicationdboption & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-replicationdboption-transact-sql.md) Para habilitar la publicación de la base de datos actual utilizando la replicación transaccional o instantáneas.  
  
2.  En el caso de una publicación transaccional, determine si existe un trabajo de Agente de registro del LOG para la base de datos de publicación. Este paso no es necesario para las publicaciones de instantáneas.  
  
    -   Si existe un trabajo de Agente de registro del LOG para la base de datos de publicación, continúe en el paso 3.  
  
    -   Si no está seguro de si existe un trabajo del agente de lector del registro para una base de datos publicada, ejecute [sp_helplogreader_agent & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-helplogreader-agent-transact-sql.md) en el publicador de la base de datos de publicación.  
  
    -   Si el conjunto de resultados está vacío, cree un trabajo de Agente de registro del LOG. En el publicador, ejecute [sp_addlogreader_agent & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addlogreader-agent-transact-sql.md). Especifique el [!INCLUDE[msCoName](../../../includes/msconame-md.md)] las credenciales de Windows en la que se ejecuta el agente de **@job_name** y **@password**. Si el agente utilizará la autenticación de SQL Server al conectarse al publicador, también debe especificar un valor de **0** para **@publisher_security_mode** y [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] información de inicio de sesión de **@publisher_login** y **@publisher_password**. Continúe en el paso 3.  
  
3.  En el publicador, ejecute [sp_addpublication & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md). Especifique un nombre de publicación para **@publication**, y para el **@repl_freq** parámetro, especifique un valor de **instantánea** para una publicación de instantáneas o un valor de **continua** para una publicación transaccional. Especifique cualquier otra opción de publicación. Esto define la publicación.  
  
    > [!NOTE]  
    >  Los nombres de publicación no pueden incluir los caracteres siguientes:  
    >   
    >  % * [ ] | : " ? \ / \< >  
  
4.  En el publicador, ejecute [sp_addpublication_snapshot & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql.md). Especifique el nombre de publicación usado en el paso 3 para **@publication** y las credenciales de Windows en la que se ejecuta el agente de instantáneas para **@snapshot_job_name** y **@password**. Si el agente utilizará la autenticación de SQL Server al conectarse al publicador, también debe especificar un valor de **0** para **@publisher_security_mode** y la [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] información de inicio de sesión de **@publisher_login** y **@publisher_password**. Esto crea un trabajo de Agente de instantáneas para la publicación.  
  
    > [!IMPORTANT]  
    >  Al configurar un publicador con un distribuidor remoto, los valores suministrados para todos los parámetros, incluidos *job_login* y *job_password*, se envían al distribuidor como texto sin formato. Antes de ejecutar este procedimiento almacenado, se recomienda cifrar la conexión entre el publicador y su distribuidor remoto. Para obtener más información, consulte [Habilitar conexiones cifradas en el motor de base de datos & #40; SQL Server Configuration Manager y nº 41;](../../../database-engine/configure-windows/enable encrypted connections to the database engine.md).  
  
5.  Agregue artículos a la publicación. Para más información, consulte [Define an Article](../../../relational-databases/replication/publish/define-an-article.md).  
  
6.  Inicie el trabajo del Agente de instantáneas para generar la instantánea inicial de esta publicación. Para más información, consulte [Create and Apply the Initial Snapshot](../../../relational-databases/replication/create-and-apply-the-initial-snapshot.md).  
  
#### Para crear una publicación de combinación  
  
1.  En el publicador, ejecute [sp_replicationdboption & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-replicationdboption-transact-sql.md) Para habilitar la publicación de la base de datos actual mediante la replicación de mezcla.  
  
2.  En el publicador de la base de datos de publicación, ejecute [sp_addmergepublication & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md). Especifique un nombre de publicación para **@publication** y cualquier otra opción de publicación. Esto define la publicación.  
  
    > [!NOTE]  
    >  Los nombres de publicación no pueden incluir los caracteres siguientes:  
    >   
    >  % * [ ] | : " ? \ / \< >  
  
3.  En el publicador, ejecute [sp_addpublication_snapshot & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql.md). Especifique el nombre de publicación usado en el paso 2 para **@publication** y las credenciales de Windows en la que se ejecuta el agente de instantáneas para **@snapshot_job_name** y **@password**. Si el agente utilizará la autenticación de SQL Server al conectarse al publicador, también debe especificar un valor de **0** para **@publisher_security_mode** y la [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] información de inicio de sesión de **@publisher_login** y **@publisher_password**. Esto crea un trabajo de Agente de instantáneas para la publicación.  
  
    > [!IMPORTANT]  
    >  Al configurar un publicador con un distribuidor remoto, los valores suministrados para todos los parámetros, incluidos *job_login* y *job_password*, se envían al distribuidor como texto sin formato. Antes de ejecutar este procedimiento almacenado, se recomienda cifrar la conexión entre el publicador y su distribuidor remoto. Para obtener más información, consulte [Habilitar conexiones cifradas en el motor de base de datos & #40; SQL Server Configuration Manager y nº 41;](../../../database-engine/configure-windows/enable encrypted connections to the database engine.md).  
  
4.  Agregue artículos a la publicación. Para más información, consulte [Define an Article](../../../relational-databases/replication/publish/define-an-article.md).  
  
5.  Inicie el trabajo del Agente de instantáneas para generar la instantánea inicial de esta publicación. Para obtener más información, consulte [Create and Apply the Initial Snapshot](../../../relational-databases/replication/create-and-apply-the-initial-snapshot.md).  
  
###  <a name="TsqlExample"></a> Ejemplo (Transact-SQL)  
 Este ejemplo crea una publicación transaccional. Las variables de scripting se usan para pasar las credenciales de Windows necesarias para crear los trabajos del Agente de instantáneas y del Agente de registro del LOG.  
  
 [!code-sql[HowTo#sp_AddTranPub](../../../relational-databases/replication/codesnippet/tsql/create-a-publication_1.sql)]  
  
 Este ejemplo crea una publicación de combinación. Las variables de scripting se usan para pasar las credenciales de Windows necesarias para crear el trabajo del Agente de instantáneas.  
  
 [!code-sql[HowTo#sp_AddMergePub](../../../relational-databases/replication/codesnippet/tsql/create-a-publication_2.sql)]  
  
##  <a name="RMOProcedure"></a> Usar Replication Management Objects (RMO)  
 Puede crear publicaciones mediante programación utilizando Replication Management Objects (RMO). Las clases RMO que usa para crear una publicación dependen del tipo de publicación que crea.  
  
#### Para crear una publicación transaccional o de instantáneas  
  
1.  Crear una conexión al publicador mediante la <xref:Microsoft.SqlServer.Management.Common.ServerConnection> clase.  
  
2.  Cree una instancia de la <xref:Microsoft.SqlServer.Replication.ReplicationDatabase> de clases para la base de datos de publicación, establezca el <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> propiedad a la instancia de <xref:Microsoft.SqlServer.Management.Common.ServerConnection> del paso 1 y la llamada la <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> (método). Si <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> devuelve **false**, compruebe que existe la base de datos.  
  
3.  Si el <xref:Microsoft.SqlServer.Replication.ReplicationDatabase.EnabledTransPublishing%2A> propiedad es **false**, establézcalo en **true**.  
  
4.  Para una publicación transaccional, compruebe el valor de la <xref:Microsoft.SqlServer.Replication.ReplicationDatabase.LogReaderAgentExists%2A> propiedad. Si esta propiedad es **true**, un trabajo del Agente de registro del LOG ya existe para esta base de datos. Si esta propiedad es **false**, haga lo siguiente:  
  
    -   Establecer el <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Login%2A> y <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Password%2A> o <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.SecurePassword%2A> campos de <xref:Microsoft.SqlServer.Replication.ReplicationDatabase.LogReaderAgentProcessSecurity%2A> para proporcionar las credenciales para el [!INCLUDE[msCoName](../../../includes/msconame-md.md)] de cuenta de Windows en la que se ejecuta el agente de lector del registro.  
  
        > [!NOTE]  
        >  Configuración de <xref:Microsoft.SqlServer.Replication.ReplicationDatabase.LogReaderAgentProcessSecurity%2A> no es obligatorio cuando se crea la publicación por un miembro de la **sysadmin** rol fijo de servidor. En este caso, el agente suplantará a la cuenta del Agente SQL Server. Para más información, consulte [Replication Agent Security Model](../../../relational-databases/replication/security/replication-agent-security-model.md).  
  
    -   (Opcional) Establecer el <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardLogin%2A> y <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardPassword%2A> o <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SecureSqlStandardPassword%2A> campos de <xref:Microsoft.SqlServer.Replication.ReplicationDatabase.LogReaderAgentPublisherSecurity%2A> cuando se utiliza la autenticación de SQL Server para conectarse al publicador.  
  
    -   Llame a la <xref:Microsoft.SqlServer.Replication.ReplicationDatabase.CreateLogReaderAgent%2A> método para crear el trabajo del agente de lector del registro para la base de datos.  
  
5.  Cree una instancia de la <xref:Microsoft.SqlServer.Replication.TransPublication> clase y establezca las siguientes propiedades para este objeto:  
  
    -   El <xref:Microsoft.SqlServer.Management.Common.ServerConnection> del paso 1 para <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>.  
  
    -   El nombre de la base de datos publicada <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A>.  
  
    -   Un nombre para la publicación para <xref:Microsoft.SqlServer.Replication.Publication.Name%2A>.  
  
    -   Un <xref:Microsoft.SqlServer.Replication.PublicationType> del <xref:Microsoft.SqlServer.Replication.PublicationType.Transactional> o <xref:Microsoft.SqlServer.Replication.PublicationType.Snapshot>.  
  
    -   La <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Login%2A> y <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Password%2A> campos de <xref:Microsoft.SqlServer.Replication.Publication.SnapshotGenerationAgentProcessSecurity%2A> para proporcionar las credenciales de la cuenta de Windows bajo la que se ejecuta el agente de instantáneas. Se usa esta cuenta también cuando el Agente de instantáneas realiza las conexiones al Distribuidor local y para cualquier conexión remota cuando se usa Autenticación de Windows.  
  
        > [!NOTE]  
        >  Configuración de <xref:Microsoft.SqlServer.Replication.Publication.SnapshotGenerationAgentProcessSecurity%2A> no es obligatorio cuando se crea la publicación por un miembro de la **sysadmin** rol fijo de servidor. En este caso, el agente suplantará a la cuenta del Agente SQL Server. Para más información, consulte [Replication Agent Security Model](../../../relational-databases/replication/security/replication-agent-security-model.md).  
  
    -   (Opcional) El <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardLogin%2A> y <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardPassword%2A> o <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SecureSqlStandardPassword%2A> campos de <xref:Microsoft.SqlServer.Replication.Publication.SnapshotGenerationAgentPublisherSecurity%2A> cuando se utiliza la autenticación de SQL Server para conectarse al publicador.  
  
    -   (Opcional) Utilice el operador lógico OR inclusivo (**|** en Visual C# y **o** en Visual Basic) y el operador lógico OR exclusivo (**^** en Visual C# y **Xor** en Visual Basic) para establecer el <xref:Microsoft.SqlServer.Replication.PublicationAttributes> los valores para el <xref:Microsoft.SqlServer.Replication.Publication.Attributes%2A> propiedad.  
  
    -   (Opcional) El nombre del publicador para <xref:Microsoft.SqlServer.Replication.TransPublication.PublisherName%2A> cuando el publicador es un no publicador de SQL Server.  
  
6.  Llame a la <xref:Microsoft.SqlServer.Replication.Publication.Create%2A> método para crear la publicación.  
  
    > [!IMPORTANT]  
    >  Al configurar un publicador con un distribuidor remoto, los valores suministrados para todas las propiedades, incluyendo <xref:Microsoft.SqlServer.Replication.Publication.SnapshotGenerationAgentProcessSecurity%2A>, se envían al distribuidor como texto sin formato. Debe cifrar la conexión entre el publicador y el distribuidor remoto antes de llamar a la <xref:Microsoft.SqlServer.Replication.Publication.Create%2A> método. Para obtener más información, consulte [Habilitar conexiones cifradas en el motor de base de datos & #40; SQL Server Configuration Manager y nº 41;](../../../database-engine/configure-windows/enable encrypted connections to the database engine.md).  
  
7.  Llame a la <xref:Microsoft.SqlServer.Replication.Publication.CreateSnapshotAgent%2A> método para crear el trabajo del agente de instantáneas para la publicación.  
  
#### Para crear una publicación de combinación  
  
1.  Crear una conexión al publicador mediante la <xref:Microsoft.SqlServer.Management.Common.ServerConnection> clase.  
  
2.  Cree una instancia de la <xref:Microsoft.SqlServer.Replication.ReplicationDatabase> de clases para la base de datos de publicación, establezca el <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> propiedad a la instancia de <xref:Microsoft.SqlServer.Management.Common.ServerConnection> del paso 1 y la llamada la <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> (método). Si <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> devuelve **false**, compruebe que existe la base de datos.  
  
3.  Si <xref:Microsoft.SqlServer.Replication.ReplicationDatabase.EnabledMergePublishing%2A> propiedad es **false**, establézcalo en **true**, y llame a <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A>.  
  
4.  Cree una instancia de la <xref:Microsoft.SqlServer.Replication.MergePublication> clase y establezca las siguientes propiedades para este objeto:  
  
    -   El <xref:Microsoft.SqlServer.Management.Common.ServerConnection> del paso 1 para <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>.  
  
    -   El nombre de la base de datos publicada <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A>.  
  
    -   Un nombre para la publicación para <xref:Microsoft.SqlServer.Replication.Publication.Name%2A>.  
  
    -   La <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Login%2A> y <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Password%2A> campos de <xref:Microsoft.SqlServer.Replication.Publication.SnapshotGenerationAgentProcessSecurity%2A> para proporcionar las credenciales de la cuenta de Windows bajo la que se ejecuta el agente de instantáneas. Se usa esta cuenta también cuando el Agente de instantáneas realiza las conexiones al Distribuidor local y para cualquier conexión remota cuando se usa Autenticación de Windows.  
  
        > [!NOTE]  
        >  Configuración de <xref:Microsoft.SqlServer.Replication.Publication.SnapshotGenerationAgentProcessSecurity%2A> no es obligatorio cuando se crea la publicación por un miembro de la **sysadmin** rol fijo de servidor. Para más información, consulte [Replication Agent Security Model](../../../relational-databases/replication/security/replication-agent-security-model.md).  
  
    -   (Opcional) Utilice el operador lógico OR inclusivo (**|** en Visual C# y **o** en Visual Basic) y el operador lógico OR exclusivo (**^** en Visual C# y **Xor** en Visual Basic) para establecer el <xref:Microsoft.SqlServer.Replication.PublicationAttributes> los valores para el <xref:Microsoft.SqlServer.Replication.Publication.Attributes%2A> propiedad.  
  
5.  Llame a la <xref:Microsoft.SqlServer.Replication.Publication.Create%2A> método para crear la publicación.  
  
    > [!IMPORTANT]  
    >  Al configurar un publicador con un distribuidor remoto, los valores suministrados para todas las propiedades, incluyendo <xref:Microsoft.SqlServer.Replication.Publication.SnapshotGenerationAgentProcessSecurity%2A>, se envían al distribuidor como texto sin formato. Debe cifrar la conexión entre el publicador y el distribuidor remoto antes de llamar a la <xref:Microsoft.SqlServer.Replication.Publication.Create%2A> método. Para obtener más información, consulte [Habilitar conexiones cifradas en el motor de base de datos & #40; SQL Server Configuration Manager y nº 41;](../../../database-engine/configure-windows/enable encrypted connections to the database engine.md).  
  
6.  Llame a la <xref:Microsoft.SqlServer.Replication.Publication.CreateSnapshotAgent%2A> método para crear el trabajo del agente de instantáneas para la publicación.  
  
###  <a name="PShellExample"></a> Ejemplos (RMO)  
 Este ejemplo habilita la base de datos de AdventureWorks para la publicación transaccional, define un trabajo del Agente de registro del LOG y crea la publicación de AdvWorksProductTran. Se debe definir un artículo para esta publicación. Las credenciales de cuenta de Windows que se necesitan para crear el trabajo del Agente de registro del LOG y el trabajo del Agente de instantáneas se pasan en tiempo de ejecución. Para obtener información sobre cómo usar RMO para definir artículos de instantáneas y de transacciones, vea [Define an Article](../../../relational-databases/replication/publish/define-an-article.md).  
  
 [!code-csharp[HowTo#rmo_CreateTranPub](../../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_createtranpub)]  
  
 [!code-vb[HowTo#rmo_vb_CreateTranPub](../../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_createtranpub)]  
  
 Este ejemplo habilita la base de datos de AdventureWorks para la publicación de combinación y crea la publicación de AdvWorksSalesOrdersMerge. Todavía se deben definir artículos para esta publicación. Las credenciales de cuenta de Windows que se necesitan para crear el trabajo del Agente de registro del LOG se pasan en tiempo de ejecución. Para obtener información sobre cómo usar RMO para definir artículos de mezcla, vea [Define an Article](../../../relational-databases/replication/publish/define-an-article.md).  
  
 [!code-csharp[HowTo#rmo_CreateMergePub](../../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_createmergepub)]  
  
 [!code-vb[HowTo#rmo_vb_CreateMergePub](../../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_createmergepub)]  
  
## Vea también  
 [Usar sqlcmd con variables de script](../../../relational-databases/scripting/use-sqlcmd-with-scripting-variables.md)   
 [Publicar datos y objetos de base de datos](../../../relational-databases/replication/publish/publish-data-and-database-objects.md)   
 [Conceptos de los Replication Management Objects (RMO)](../../../relational-databases/replication/concepts/replication-management-objects-concepts.md)   
 [Definir un artículo](../../../relational-databases/replication/publish/define-an-article.md)   
 [Ver y modificar propiedades de publicación](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md)   
 [Configurar la distribución](../../../relational-databases/replication/configure-distribution.md)   
 [Proteger el distribuidor](../../../relational-databases/replication/security/secure-the-distributor.md)   
 [Proteger el publicador](../../../relational-databases/replication/security/secure-the-publisher.md)  
  
  