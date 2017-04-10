---
title: "Ver y modificar las propiedades del distribuidor y del publicador | Microsoft Docs"
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
  - "ver propiedades de replicación"
  - "Distribuidores [replicación de SQL Server], modificar"
  - "modificar propiedades de replicación, Distribuidores"
  - "Distribuidores [replicación de SQL Server], propiedades"
ms.assetid: 5dae1d59-c377-4c6e-adc9-b68c5b328f79
caps.latest.revision: 43
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 43
---
# Ver y modificar las propiedades del distribuidor y del publicador
  En este tema se describe cómo ver y modificar las propiedades del distribuidor y del publicador en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../includes/tsql-md.md)] o Replication Management Objects (RMO).  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Recomendaciones](#Recommendations)  
  
     [Seguridad](#Security)  
  
-   **Para ver y modificar las propiedades del publicador y del distribuidor con:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [Replication Management Objects (RMO)](#RMOProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="Recommendations"></a> Recomendaciones  
  
-   Para los publicadores que ejecutan versiones anteriores a [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], un usuario del rol fijo de servidor **sysadmin** puede registrar suscriptores en la página **Suscriptores** . A partir de [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], ya no es necesario registrar explícitamente los suscriptores para la replicación.  
  
###  <a name="Security"></a> Seguridad  
 Cuando sea posible, pida a los usuarios que proporcionen credenciales de seguridad en tiempo de ejecución.  
  
##  <a name="SSMSProcedure"></a> Usar SQL Server Management Studio  
  
#### Para ver y modificar las propiedades del distribuidor  
  
1.  Conéctese al distribuidor en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]y expanda el nodo de servidor.  
  
2.  Haga clic en el **replicación** carpeta y, a continuación, haga clic en **Propiedades del distribuidor**.  
  
3.  Ver y modificar las propiedades en la **Propiedades del distribuidor: \< distribuidor>** cuadro de diálogo.  
  
    -   Para ver y modificar las propiedades de una base de datos de distribución, haga clic en el botón de propiedades (**...**) para la base de datos en el **General** página del cuadro de cuadro de diálogo.  
  
    -   Para ver y modificar las propiedades del publicador asociados al distribuidor, haga clic en el botón de propiedades (**...**) para el publicador en el **publicadores** página del cuadro de diálogo.  
  
    -   Para obtener acceso a los perfiles de los agentes de replicación, haga clic en el botón **Valores predeterminados de perfil** de la página **General** del cuadro de diálogo. Para más información, consulte [Replication Agent Profiles](../../relational-databases/replication/agents/replication-agent-profiles.md).  
  
    -   Para cambiar la contraseña de la cuenta utilizada cuando los procedimientos almacenados administrativos se ejecutan en el publicador y actualizar la información del distribuidor, escriba una contraseña nueva en los cuadros **Contraseña** y **Confirmar contraseña** de la página **Publicadores** del cuadro de diálogo. Para obtener más información, consulte [proteger el distribuidor](../../relational-databases/replication/security/secure-the-distributor.md).  
  
4.  Modifique las propiedades si es necesario y, a continuación, haga clic en **Aceptar**.  
  
#### Para ver y modificar las propiedades del Publicador  
  
1.  Conéctese al publicador en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]y, a continuación, expanda el nodo del servidor.  
  
2.  Haga clic en el **replicación** carpeta y, a continuación, haga clic en **Propiedades del publicador**.  
  
3.  Ver y modificar las propiedades en la **Propiedades del publicador: \< publicador >** cuadro de diálogo.  
  
    -   Un usuario del rol fijo de servidor **sysadmin** puede habilitar bases de datos de replicación en la página **Bases de datos de publicaciones** . Habilitar una base de datos no publica esa base de datos; en su lugar, permite que cualquier usuario de la **db_owner** rol fijo de base de datos para esa base de datos crear una o varias publicaciones en la base de datos.  
  
4.  Modifique las propiedades si es necesario y, a continuación, haga clic en **Aceptar**.  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
 Las propiedades del publicador y del distributor se pueden ver mediante programación usando procedimientos almacenados de replicación.  
  
#### Para ver las propiedades de la base de datos de distribución  
  
1.  Ejecutar [sp_helpdistributor](../../relational-databases/system-stored-procedures/sp-helpdistributor-transact-sql.md) para devolver información sobre el distribuidor, la base de datos de distribución y el directorio de trabajo.  
  
2.  Ejecutar [sp_helpdistributiondb](../../relational-databases/system-stored-procedures/sp-helpdistributiondb-transact-sql.md) para devolver propiedades de una base de datos de distribución especificada.  
  
#### Para cambiar las propiedades de la base de datos de distribución y el distribuidor  
  
1.  En el distribuidor, ejecute [sp_changedistributor_property](../../relational-databases/system-stored-procedures/sp-changedistributor-property-transact-sql.md) para modificar las propiedades del distribuidor.  
  
2.  En el distribuidor, ejecute [sp_changedistributiondb](../../relational-databases/system-stored-procedures/sp-changedistributiondb-transact-sql.md) para modificar las propiedades de la base de datos de distribución.  
  
3.  En el distribuidor, ejecute [sp_changedistributor_password](../../relational-databases/system-stored-procedures/sp-changedistributor-password-transact-sql.md) para cambiar la contraseña del distribuidor.  
  
    > [!IMPORTANT]  
    >  Cuando sea posible, pida a los usuarios que proporcionen credenciales de seguridad en tiempo de ejecución. Si debe almacenar credenciales en un archivo de script, proteja el archivo para evitar el acceso no autorizado.  
  
4.  En el distribuidor, ejecute [sp_changedistpublisher](../../relational-databases/system-stored-procedures/sp-changedistpublisher-transact-sql.md) para cambiar las propiedades de un publicador con el distribuidor.  
  
###  <a name="TsqlExample"></a> Ejemplos (Transact-SQL)  
 El siguiente script de [!INCLUDE[tsql](../../includes/tsql-md.md)] de ejemplo devuelve información acerca del Distribuidor y la base de datos de distribución.  
  
 [!code-sql[HowTo#sp_helpdistributor](../../relational-databases/replication/codesnippet/tsql/view-and-modify-distribu_1.sql)]  
  
 [!code-sql[HowTo#sp_helpdistributiondb](../../relational-databases/replication/codesnippet/tsql/view-and-modify-distribu_2.sql)]  
  
 Este ejemplo cambia los períodos de retención para el Distribuidor, la contraseña usada al conectar al Distribuidor y el intervalo en el que el Distribuidor comprueba el estado de distintos agentes de replicación (también conocido como intervalo de latidos).  
  
> [!IMPORTANT]  
>  Cuando sea posible, pida a los usuarios que proporcionen credenciales de seguridad en tiempo de ejecución. Si debe almacenar credenciales en un archivo de script, proteja el archivo para evitar el acceso no autorizado.  
  
 [!code-sql[HowTo#sp_changedistributor_property](../../relational-databases/replication/codesnippet/tsql/view-and-modify-distribu_3.sql)]  
  
 [!code-sql[HowTo#sp_changedistributiondb](../../relational-databases/replication/codesnippet/tsql/view-and-modify-distribu_4.sql)]  
  
 [!code-sql[HowTo#sp_changedistributor_password](../../relational-databases/replication/codesnippet/tsql/view-and-modify-distribu_5.sql)]  
  
##  <a name="RMOProcedure"></a> Usar Replication Management Objects (RMO)  
  
#### Para ver y modificar las propiedades del distribuidor  
  
1.  Crear una conexión al distribuidor mediante la <xref:Microsoft.SqlServer.Management.Common.ServerConnection> clase.  
  
2.  Cree una instancia de la <xref:Microsoft.SqlServer.Replication.ReplicationServer> clase. Pasar el <xref:Microsoft.SqlServer.Management.Common.ServerConnection> objeto desde el paso 1.  
  
3.  (Opcional) Compruebe el <xref:Microsoft.SqlServer.Replication.ReplicationServer.IsDistributor%2A> propiedad para comprobar que el servidor conectado actualmente es un distribuidor.  
  
4.  Llame a la <xref:Microsoft.SqlServer.Replication.ReplicationObject.Load%2A> método para obtener las propiedades del servidor.  
  
5.  (Opcional) Para cambiar las propiedades, establezca un nuevo valor para una o varias de las propiedades del distribuidor que se pueden establecer en el <xref:Microsoft.SqlServer.Replication.ReplicationServer> objeto.  
  
6.  (Opcional) Si el <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A> propiedad en el <xref:Microsoft.SqlServer.Replication.ReplicationServer> objeto se establece en **true**, llame a la <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> método para confirmar los cambios en el servidor.  
  
#### Para ver y modificar las propiedades de la base de datos de distribución  
  
1.  Crear una conexión al distribuidor mediante la <xref:Microsoft.SqlServer.Management.Common.ServerConnection> clase.  
  
2.  Cree una instancia de la <xref:Microsoft.SqlServer.Replication.DistributionDatabase> clase. Especifique la propiedad de nombre y pase el <xref:Microsoft.SqlServer.Management.Common.ServerConnection> objeto desde el paso 1.  
  
3.  Llame a la <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> método para obtener las propiedades del servidor. Si este método devuelve **false**, significa que la base de datos con el nombre especificado no existe en el servidor.  
  
4.  (Opcional) Para cambiar las propiedades, establezca un nuevo valor para uno de los <xref:Microsoft.SqlServer.Replication.DistributionDatabase> propiedades que se pueden establecer.  
  
5.  (Opcional) Si el <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A> propiedad en el <xref:Microsoft.SqlServer.Replication.DistributionDatabase> objeto se establece en **true**, llame a la <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> método para confirmar los cambios en el servidor.  
  
#### Para ver y modificar las propiedades del Publicador  
  
1.  Crear una conexión al publicador mediante la <xref:Microsoft.SqlServer.Management.Common.ServerConnection> clase.  
  
2.  Cree una instancia de la <xref:Microsoft.SqlServer.Replication.DistributionPublisher> clase. Especifique el <xref:Microsoft.SqlServer.Replication.DistributionPublisher.Name%2A> propiedad y pase el <xref:Microsoft.SqlServer.Management.Common.ServerConnection> objeto desde el paso 1.  
  
3.  (Opcional) Para cambiar las propiedades, establezca un nuevo valor para uno de los <xref:Microsoft.SqlServer.Replication.DistributionPublisher> propiedades que se pueden establecer.  
  
4.  (Opcional) Si el <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A> propiedad en el <xref:Microsoft.SqlServer.Replication.DistributionPublisher> objeto se establece en **true**, llame a la <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> método para confirmar los cambios en el servidor.  
  
#### Para cambiar la contraseña de la conexión administrativa del publicador al distribuidor  
  
1.  Crear una conexión al distribuidor mediante la <xref:Microsoft.SqlServer.Management.Common.ServerConnection> clase.  
  
2.  Cree una instancia de la <xref:Microsoft.SqlServer.Replication.ReplicationServer> clase.  
  
3.  Establecer el <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> propiedad en la conexión creada en el paso 1.  
  
4.  Llame a la <xref:Microsoft.SqlServer.Replication.ReplicationObject.Load%2A> método para obtener las propiedades del objeto.  
  
5.  Llame a la <xref:Microsoft.SqlServer.Replication.ReplicationServer.ChangeDistributorPassword%2A> método. Pase el nuevo valor de contraseña para el parámetro *password* .  
  
    > [!IMPORTANT]  
    >  Cuando sea posible, pida a los usuarios que proporcionen credenciales de seguridad en tiempo de ejecución. Si debe almacenar credenciales, use los [servicios de cifrado](http://go.microsoft.com/fwlink/?LinkId=34733) (en inglés) proporcionados por [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows .NET Framework.  
  
6.  (Opcional) Realice los pasos siguientes para cambiar la contraseña en cada publicador remoto que utilice este distribuidor:  
  
    1.  Crear una conexión al publicador mediante la <xref:Microsoft.SqlServer.Management.Common.ServerConnection> clase.  
  
    2.  Cree una instancia de la <xref:Microsoft.SqlServer.Replication.ReplicationServer> clase.  
  
    3.  Establecer el <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> propiedad en la conexión creada en el paso 6a.  
  
    4.  Llame a la <xref:Microsoft.SqlServer.Replication.ReplicationObject.Load%2A> método para obtener las propiedades del objeto.  
  
    5.  Llame a la <xref:Microsoft.SqlServer.Replication.ReplicationServer.ChangeDistributorPassword%2A> método. Pase el nuevo valor de contraseña del paso 5 para el parámetro *password* .  
  
###  <a name="PShellExample"></a> Ejemplo (RMO)  
 Este ejemplo muestra cómo cambiar las propiedades de Distribución y de la base de datos de distribución.  
  
> [!IMPORTANT]  
>  Para no almacenar las credenciales en el código, la nueva contraseña del distribuidor se proporciona en tiempo de ejecución.  
  
 [!code-csharp[HowTo#rmo_ChangeDistPub](../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_changedistpub)]  
  
 [!code-vb[HowTo#rmo_vb_ChangeDistPub](../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_changedistpub)]  
  
## Vea también  
 [Conceptos de los Replication Management Objects (RMO)](../../relational-databases/replication/concepts/replication-management-objects-concepts.md)   
 [Deshabilitar la publicación y la distribución](../../relational-databases/replication/disable-publishing-and-distribution.md)   
 [Configurar la distribución](../../relational-databases/replication/configure-distribution.md)   
 [Conceptos de los Replication Management Objects (RMO)](../../relational-databases/replication/concepts/replication-management-objects-concepts.md)   
 [Script de información del distribuidor y del publicador](../../relational-databases/replication/administration/distributor-and-publisher-information-script.md)   
 [Conceptos sobre los procedimientos almacenados del sistema de replicación](../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)   
 [Ver la información y realizar tareas para un publicador & #40; Monitor de replicación & #41;](../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-a-publisher-replication-monitor.md)  
  
  