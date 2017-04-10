---
title: "Crear y aplicar la instant&#225;nea inicial | Microsoft Docs"
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
  - "instantáneas [replicación de SQL Server], crear"
  - "replicación de instantáneas [SQL Server], instantáneas iniciales"
ms.assetid: 742727a1-5189-44ec-b3ae-6fd7aa1f5347
caps.latest.revision: 44
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 44
---
# Crear y aplicar la instant&#225;nea inicial
  En este tema se describe cómo crear y aplicar la instantánea inicial en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../includes/tsql-md.md)] o Replication Management Objects (RMO). Las publicaciones de mezcla que usan filtros con parámetros necesitan una instantánea de dos partes. Para más información, consulte [Create a Snapshot for a Merge Publication with Parameterized Filters](../../relational-databases/replication/create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md).  
  
 **En este tema**  
  
-   **Para crear y aplicar la instantánea inicial con:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [Replication Management Objects (RMO)](#RMOProcedure)  
  
##  <a name="SSMSProcedure"></a> Usar SQL Server Management Studio  
 De forma predeterminada, si se está ejecutando el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , el Agente de instantáneas genera una instantánea inmediatamente después de que se cree una publicación con el Asistente para nueva publicación. A continuación, el Agente de distribución (para la replicación de instantáneas y transaccional) o el Agente de mezcla (para las suscripciones de mezcla) la aplican a todas las suscripciones. Las instantáneas también se pueden generar mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] y el Monitor de replicación. Para obtener información acerca de cómo iniciar el Monitor de replicación, consulte [iniciar el Monitor de replicación](../../relational-databases/replication/monitor/start-the-replication-monitor.md).  
  
#### Para crear una instantánea en Management Studio  
  
1.  Conéctese al publicador en [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]y, a continuación, expanda el nodo del servidor.  
  
2.  Expanda la carpeta **Replicación** y, a continuación, expanda la carpeta **Publicaciones locales** .  
  
3.  Haga clic en la publicación para el que desea crear una instantánea y, a continuación, haga clic en **Ver estado del agente de instantáneas**.  
  
4.  En el **Ver estado del agente de instantáneas - \< publicación>** cuadro de diálogo, haga clic en **iniciar**.  
  
 Cuando el Agente de instantáneas termina de generar la instantánea, aparece un mensaje del tipo "[100%] Se ha generado una instantánea de 17 artículos".  
  
#### Para crear una instantánea en el Monitor de replicación  
  
1.  En el Monitor de replicación, expanda un grupo de publicador en el panel izquierdo y, a continuación, expanda un publicador.  
  
2.  Haga clic en la publicación para el que desea generar una instantánea y, a continuación, haga clic en **generar instantáneas**.  
  
3.  Para ver el estado del Agente de instantáneas, haga clic en la pestaña **Agentes** . Para obtener más información, haga clic en el agente de instantáneas en la cuadrícula y, a continuación, haga clic en **Ver detalles**.  
  
#### Para aplicar una instantánea  
  
1.  Una vez generada la instantánea, se aplica mediante la sincronización de la suscripción con el Agente de distribución o el Agente de mezcla:  
  
    -   Si el agente se ejecuta de forma continua (valor predeterminado para la replicación transaccional), la instantánea se aplica inmediatamente después de haberse generado.  
  
    -   Si el agente se ejecuta según una programación, la instantánea se aplica la siguiente vez que está programada la ejecución del agente.  
  
    -   Si el agente se ejecuta a petición, se aplica la siguiente vez que se ejecuta el agente.  
  
     Para obtener más información acerca de cómo sincronizar las suscripciones, consulte [sincronizar una suscripción de inserción](../../relational-databases/replication/synchronize-a-push-subscription.md) y [sincronizar una suscripción de extracción](../../relational-databases/replication/synchronize-a-pull-subscription.md).  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
 Las instantáneas iniciales se pueden crear mediante programación o creando y ejecutando un trabajo del Agente de instantáneas o ejecutando el archivo ejecutable Agente de instantáneas desde un archivo por lotes. Una vez generada una instantánea inicial, se transfiere y se aplica en el suscriptor cuando se sincroniza la suscripción por primera vez. Si ejecuta el Agente de instantáneas desde un símbolo del sistema o un archivo por lotes, necesitará volver a ejecutar el agente cada vez que la instantánea existente deje de ser válida.  
  
> [!IMPORTANT]  
>  Cuando sea posible, pida a los usuarios que proporcionen credenciales de seguridad en tiempo de ejecución. Si debe almacenar las credenciales en un archivo de script, proteja el archivo para evitar el acceso no autorizado.  
  
#### Para crear y ejecutar un trabajo del Agente de instantáneas que genere la instantánea inicial  
  
1.  Cree una publicación de instantáneas, transaccional o de combinación. Para obtener más información, consulte [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md).  
  
2.  Ejecutar [sp_addpublication_snapshot & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql.md). Especifique **@publication** y los siguientes parámetros:  
  
    -   **@Job_login, que especifica** las credenciales de autenticación de Windows en la que se ejecuta el agente de instantáneas en el distribuidor.  
  
    -   **@Job_password**, que es la contraseña de las credenciales de Windows proporcionadas.  
  
    -   (Opcional) Un valor de **0** para **@publisher_security_mode** Si el agente utilizará la autenticación de SQL Server al conectarse al publicador. En este caso, también debe especificar la información de inicio de sesión de autenticación de SQL Server para **@publisher_login** y **@publisher_password**.  
  
    -   (Opcional) Un programa de sincronización para el trabajo del Agente de instantáneas. Para obtener más información, consulte [Specify Synchronization Schedules](../../relational-databases/replication/specify-synchronization-schedules.md).  
  
    > [!IMPORTANT]  
    >  Al configurar un publicador con un distribuidor remoto, los valores suministrados para todos los parámetros, incluidos *job_login* y *job_password*, se envían al distribuidor como texto sin formato. Antes de ejecutar este procedimiento almacenado, se recomienda cifrar la conexión entre el publicador y su distribuidor remoto. Para obtener más información, consulte [Habilitar conexiones cifradas en el motor de base de datos & #40; SQL Server Configuration Manager y nº 41;](../../database-engine/configure-windows/enable encrypted connections to the database engine.md).  
  
3.  Agregue artículos a la publicación. Para más información, consulte [Define an Article](../../relational-databases/replication/publish/define-an-article.md).  
  
4.  En el publicador de la base de datos de publicación, ejecute [sp_startpublication_snapshot & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-startpublication-snapshot-transact-sql.md), especificando el valor de **@publication** del paso 1.  
  
#### Para ejecutar el Agente de instantáneas y generar una instantánea inicial  
  
1.  Cree una publicación de instantáneas, transaccional o de combinación. Para más información, consulte [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md).  
  
2.  Agregue artículos a la publicación. Para más información, consulte [Define an Article](../../relational-databases/replication/publish/define-an-article.md).  
  
3.  Desde el símbolo del sistema o en un archivo por lotes, inicie la [agente de instantáneas de replicación](../../relational-databases/replication/agents/replication-snapshot-agent.md) ejecutando **snapshot.exe**, especificar los argumentos de línea de comandos siguientes:  
  
    -   **-Publication**  
  
    -   **-Publisher**  
  
    -   **-Distributor**  
  
    -   **-PublisherDB**  
  
    -   **-ReplicationType**  
  
     Si está usando la autenticación de SQL Server, también debe especificar los argumentos siguientes:  
  
    -   **-DistributorLogin**  
  
    -   **-DistributorPassword**  
  
    -   **-DistributorSecurityMode** = **0**  
  
    -   **-PublisherLogin**  
  
    -   **-PublisherPassword**  
  
    -   **-PublisherSecurityMode** = **0**  
  
###  <a name="TsqlExample"></a> Ejemplos (Transact-SQL)  
 Este ejemplo muestra cómo crear una publicación transaccional y agregar un trabajo del agente de instantáneas para la nueva publicación (utilizando **sqlcmd** variables de scripting). En el ejemplo también se inicia el trabajo.  
  
 [!code-sql[HowTo#sp_trangenerate_snapshot](../../relational-databases/replication/codesnippet/tsql/create-and-apply-the-ini_1.sql)]  
  
 En este ejemplo se crea una publicación de mezcla y se agrega un trabajo del agente de instantáneas (utilizando **sqlcmd** variables) para la publicación. En este ejemplo también se inicia el trabajo.  
  
 [!code-sql[HowTo#sp_mergegenerate_snapshot](../../relational-databases/replication/codesnippet/tsql/create-and-apply-the-ini_2.sql)]  
  
 Los siguientes argumentos de la línea de comandos inician el Agente de instantáneas para que genere la instantánea para una publicación de combinación.  
  
> [!NOTE]  
>  Los saltos de línea se incluyeron para mejorar la legibilidad. En un archivo por lotes, los comandos se deben realizar en una única línea.  
  
```  
  
REM -- Declare variables  
SET Publisher=%InstanceName%  
SET PublicationDB=AdventureWorks2012   
SET Publication=AdvWorksSalesOrdersMerge   
  
REM --Start the Snapshot Agent to generate the snapshot for AdvWorksSalesOrdersMerge.  
"C:\Program Files\Microsoft SQL Server\120\COM\SNAPSHOT.EXE" -Publication %Publication%   
-Publisher %Publisher% -Distributor %Publisher% -PublisherDB %PublicationDB%   
-ReplicationType 2 -OutputVerboseLevel 1 -DistributorSecurityMode 1  
  
```  
  
##  <a name="RMOProcedure"></a> Usar Replication Management Objects (RMO)  
 El Agente de instantáneas genera instantáneas una vez creada la publicación. Puede generar estas instantáneas mediante programación utilizando Replication Management Objects (RMO) y el acceso de código administrado directo a las funcionalidades del agente de replicación. Los objetos que se usan dependen del tipo de replicación. El Agente de instantáneas se puede iniciar sincrónicamente con el objeto <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent> o de forma asincrónica con el trabajo de agente. Una vez generada la instantánea inicial, se transfiere y se aplica al suscriptor cuando se sincroniza la suscripción por primera vez. Deberá volver a ejecutar el agente cada vez que la instantánea existente no contenga datos válidos y actualizados. Para obtener más información, consulte [mantener publicaciones](../../relational-databases/replication/publish/maintain-publications.md).  
  
> [!IMPORTANT]  
>  Cuando sea posible, pida a los usuarios que proporcionen credenciales de seguridad en tiempo de ejecución. Si debe almacenar credenciales, use los [servicios de cifrado](http://go.microsoft.com/fwlink/?LinkId=34733) (en inglés) proporcionados por [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows .NET Framework.  
  
#### Para generar la instantánea inicial de una publicación transaccional o de instantáneas iniciando el trabajo del Agente de instantáneas (asincrónico)  
  
1.  Crear una conexión al publicador mediante la <xref:Microsoft.SqlServer.Management.Common.ServerConnection> clase.  
  
2.  Cree una instancia de la <xref:Microsoft.SqlServer.Replication.TransPublication> clase. Establecer el <xref:Microsoft.SqlServer.Replication.Publication.Name%2A> y <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A> Propiedades de la publicación y establezca el <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> propiedad en la conexión creada en el paso 1.  
  
3.  Llame a la <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> para cargar las propiedades restantes del objeto. Si este método devuelve **false**, significa que las propiedades de publicación del paso 2 se definieron incorrectamente, o bien que la publicación no existe.  
  
4.  Si el valor de <xref:Microsoft.SqlServer.Replication.Publication.SnapshotAgentExists%2A> es **false**, llame a <xref:Microsoft.SqlServer.Replication.Publication.CreateSnapshotAgent%2A> para crear el trabajo del agente de instantáneas para esta publicación.  
  
5.  Llame a la <xref:Microsoft.SqlServer.Replication.Publication.StartSnapshotGenerationAgentJob%2A> método para iniciar el trabajo de agente que genera la instantánea para esta publicación.  
  
6.  (Opcional) Cuando el valor de <xref:Microsoft.SqlServer.Replication.TransPublication.SnapshotAvailable%2A> es **true**, la instantánea está disponible para los suscriptores.  
  
#### Para generar la instantánea inicial de una publicación transaccional o de instantáneas ejecutando el trabajo del Agente de instantáneas (sincrónico)  
  
1.  Cree una instancia de la clase <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent> y establezca las propiedades necesarias siguientes:  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.Publisher%2A> : el nombre del publicador  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.PublisherDatabase%2A> : el nombre de la base de datos de publicación  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.Publication%2A> : el nombre de la publicación  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.Distributor%2A> : el nombre del distribuidor  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.PublisherSecurityMode%2A> -un valor de <xref:Microsoft.SqlServer.Replication.SecurityMode.Integrated> para utilizar la autenticación de Windows al conectarse al publicador o un valor de <xref:Microsoft.SqlServer.Replication.SecurityMode.Standard> y valores para <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.PublisherLogin%2A> y <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.PublisherPassword%2A> usar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticación al conectarse al publicador. Se recomienda la autenticación de Windows.  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.DistributorSecurityMode%2A> -un valor de <xref:Microsoft.SqlServer.Replication.SecurityMode.Integrated> para utilizar la autenticación de Windows al conectarse al distribuidor o un valor de <xref:Microsoft.SqlServer.Replication.SecurityMode.Standard> y valores para <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.DistributorLogin%2A> y <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.DistributorPassword%2A> usar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticación al conectarse al distribuidor. Se recomienda la autenticación de Windows.  
  
2.  Establecer un valor de <xref:Microsoft.SqlServer.Replication.ReplicationType.Transactional> o <xref:Microsoft.SqlServer.Replication.ReplicationType.Snapshot> para <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.ReplicationType%2A>.  
  
3.  Llame al método <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.GenerateSnapshot%2A> .  
  
#### Para generar la instantánea inicial de una publicación de combinación iniciando el trabajo del Agente de instantáneas (asincrónico)  
  
1.  Crear una conexión al publicador mediante la <xref:Microsoft.SqlServer.Management.Common.ServerConnection> clase.  
  
2.  Cree una instancia de la <xref:Microsoft.SqlServer.Replication.MergePublication> clase. Establecer el <xref:Microsoft.SqlServer.Replication.Publication.Name%2A> y <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A> Propiedades de la publicación y establezca el <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> propiedad en la conexión creada en el paso 1.  
  
3.  Llame a la <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> para cargar las propiedades restantes del objeto. Si este método devuelve **false**, significa que las propiedades de publicación del paso 2 se definieron incorrectamente, o bien que la publicación no existe.  
  
4.  Si el valor de <xref:Microsoft.SqlServer.Replication.Publication.SnapshotAgentExists%2A> es **false**, llame a <xref:Microsoft.SqlServer.Replication.Publication.CreateSnapshotAgent%2A> para crear el trabajo del agente de instantáneas para esta publicación.  
  
5.  Llame a la <xref:Microsoft.SqlServer.Replication.Publication.StartSnapshotGenerationAgentJob%2A> método para iniciar el trabajo de agente que genera la instantánea para esta publicación.  
  
6.  (Opcional) Cuando el valor de <xref:Microsoft.SqlServer.Replication.MergePublication.SnapshotAvailable%2A> es **true**, la instantánea está disponible para los suscriptores.  
  
#### Para generar la instantánea inicial de una publicación de combinación ejecutando el Agente de instantáneas (sincrónico)  
  
1.  Cree una instancia de la clase <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent> y establezca las propiedades necesarias siguientes:  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.Publisher%2A> : el nombre del publicador  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.PublisherDatabase%2A> : el nombre de la base de datos de publicación  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.Publication%2A> : el nombre de la publicación  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.Distributor%2A> : el nombre del distribuidor  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.PublisherSecurityMode%2A> -un valor de <xref:Microsoft.SqlServer.Replication.SecurityMode.Integrated> para utilizar la autenticación de Windows al conectarse al publicador o un valor de <xref:Microsoft.SqlServer.Replication.SecurityMode.Standard> y valores para <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.PublisherLogin%2A> y <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.PublisherPassword%2A> usar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticación al conectarse al publicador. Se recomienda la autenticación de Windows.  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.DistributorSecurityMode%2A> -un valor de <xref:Microsoft.SqlServer.Replication.SecurityMode.Integrated> para utilizar la autenticación de Windows al conectarse al distribuidor o un valor de <xref:Microsoft.SqlServer.Replication.SecurityMode.Standard> y valores para <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.DistributorLogin%2A> y <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.DistributorPassword%2A> usar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticación al conectarse al distribuidor. Se recomienda la autenticación de Windows.  
  
2.  Establecer un valor de <xref:Microsoft.SqlServer.Replication.ReplicationType.Merge> para <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.ReplicationType%2A>.  
  
3.  Llame al método <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.GenerateSnapshot%2A> .  
  
###  <a name="PShellExample"></a> Ejemplos (RMO)  
 Este ejemplo ejecuta sincrónicamente el Agente de instantáneas para generar la instantánea inicial de una publicación transaccional.  
  
 [!code-csharp[HowTo#rmo_GenerateSnapshot](../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_generatesnapshot)]  
  
 [!code-vb[HowTo#rmo_vb_GenerateSnapshot](../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_generatesnapshot)]  
  
 Este ejemplo inicia asincrónicamente el Agente de instantáneas para generar la instantánea inicial de una publicación transaccional.  
  
 [!code-csharp[HowTo#rmo_GenerateSnapshot_WithJob](../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_generatesnapshot_withjob)]  
  
 [!code-vb[HowTo#rmo_vb_GenerateSnapshot_WithJob](../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_generatesnapshot_withjob)]  
  
## Vea también  
 [Crear una publicación](../../relational-databases/replication/publish/create-a-publication.md)   
 [Crear una suscripción de extracción](../../relational-databases/replication/create-a-pull-subscription.md)   
 [Crear una suscripción de inserción](../../relational-databases/replication/create-a-push-subscription.md)   
 [Especificar programaciones de sincronización](../../relational-databases/replication/specify-synchronization-schedules.md)   
 [Crear y aplicar una instantánea](../../relational-databases/replication/create-and-apply-the-snapshot.md)   
 [Inicializar una suscripción con una instantánea](../../relational-databases/replication/initialize-a-subscription-with-a-snapshot.md)   
 [Conceptos de los Replication Management Objects (RMO)](../../relational-databases/replication/concepts/replication-management-objects-concepts.md)   
 [Prácticas recomendadas de seguridad de replicación](../../relational-databases/replication/security/replication-security-best-practices.md)   
 [Conceptos sobre los procedimientos almacenados del sistema de replicación](../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)   
 [Usar sqlcmd con variables de script](../../relational-databases/scripting/use-sqlcmd-with-scripting-variables.md)  
  
  