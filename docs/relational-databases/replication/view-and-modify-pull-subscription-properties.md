---
title: "Ver y modificar las propiedades de una suscripci&#243;n de extracci&#243;n | Microsoft Docs"
ms.custom: ""
ms.date: "03/16/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "modificar suscripciones"
  - "ver propiedades de replicación"
  - "modificar propiedades de replicación, suscripciones de extracción"
  - "suscripciones de extracción [replicación de SQL Server], modificar"
  - "suscripciones [replicación de SQL Server], extraer"
  - "suscripciones de extracción [replicación de SQL Server], propiedades"
  - "modificar suscripciones, SQL Server Management Studio"
ms.assetid: 1601e54f-86f0-49e8-b023-87a5d1def033
caps.latest.revision: 37
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 37
---
# Ver y modificar las propiedades de una suscripci&#243;n de extracci&#243;n
  En este tema se describe cómo ver y modificar las propiedades de una suscripción de extracción en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../includes/tsql-md.md)] o Replication Management Objects (RMO).  
  
 **En este tema**  
  
-   **Para ver y modificar las propiedades de una suscripción de extracción con:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [Replication Management Objects (RMO)](#RMOProcedure)  
  
##  <a name="SSMSProcedure"></a> Usar SQL Server Management Studio  
 Ver las propiedades de suscripción de extracción desde el publicador o el suscriptor en la **Propiedades de suscripción - \< publicador>: \< Basededatosdepublicaciones>** cuadro de diálogo, que está disponible en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. En el suscriptor se pueden ver más propiedades y éstas se pueden modificar. También se pueden ver propiedades del publicador en la pestaña **Todas las suscripciones** , que está disponible en el Monitor de replicación. Para obtener información acerca de cómo iniciar el Monitor de replicación, consulte [iniciar el Monitor de replicación](../../relational-databases/replication/monitor/start-the-replication-monitor.md).  
  
#### Para ver las propiedades de las suscripciones de extracción en el publicador en Management Studio  
  
1.  Conéctese al publicador en [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]y, a continuación, expanda el nodo del servidor.  
  
2.  Expanda la carpeta **Replicación** y, a continuación, expanda la carpeta **Publicaciones locales** .  
  
3.  Expanda la publicación apropiada, haga clic en una suscripción y, a continuación, haga clic en **propiedades**.  
  
4.  Vea las propiedades y, a continuación, haga clic en **Aceptar**.  
  
#### Para ver y modificar las propiedades de las suscripciones de extracción en el publicador en Management Studio  
  
1.  Conéctese al suscriptor en [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]y expanda el nodo de servidor.  
  
2.  Expanda la carpeta **Replicación** y, a continuación, expanda la carpeta **Suscripciones locales** .  
  
3.  Haga clic en una suscripción y, a continuación, haga clic en **propiedades**.  
  
4.  Modifique las propiedades si es necesario y, a continuación, haga clic en **Aceptar**.  
  
#### Para ver las propiedades de las suscripciones de extracción en el publicador en el Monitor de replicación  
  
1.  Expanda un grupo de publicador en el panel izquierdo del Monitor de replicación, expanda un publicador y, a continuación, haga clic en una publicación.  
  
2.  Haga clic en la pestaña **Todas las suscripciones** .  
  
3.  Haga clic en una suscripción y, a continuación, haga clic en **propiedades**.  
  
4.  Vea las propiedades y, a continuación, haga clic en **Aceptar**.  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
 Se pueden modificar las suscripciones de extracción y tener acceso a sus propiedades mediante programación usando procedimientos almacenados de replicación. Los procedimientos almacenados que se usen dependerán del tipo de publicación a la que corresponda la suscripción.  
  
#### Para ver las propiedades de una suscripción de extracción a una publicación transaccional o de instantáneas  
  
1.  En el suscriptor, ejecute [sp_helppullsubscription](../../relational-databases/system-stored-procedures/sp-helppullsubscription-transact-sql.md). Especifique **@publisher**, **@publisher_db**, y **@publication**. Esto devuelve información sobre la suscripción que está almacenada en tablas del sistema en el Suscriptor.  
  
2.  En el suscriptor, ejecute [sp_helpsubscription_properties](../../relational-databases/system-stored-procedures/sp-helpsubscription-properties-transact-sql.md). Especifique **@publisher**, **@publisher_db**, **@publication**, y uno de los siguientes valores para **@publication_type**:  
  
    -   **0** -suscripción pertenece a una publicación transaccional.  
  
    -   **1** -suscripción pertenece a una publicación de instantáneas.  
  
3.  En el publicador, ejecute [sp_helpsubscription](../../relational-databases/system-stored-procedures/sp-helpsubscription-transact-sql.md). Especifique **@publication** y **@subscriber**.  
  
4.  En el publicador, ejecute [sp_helpsubscriberinfo](../../relational-databases/system-stored-procedures/sp-helpsubscriberinfo-transact-sql.md), especificando **@subscriber**. Presenta información acerca del suscriptor.  
  
#### Para modificar las propiedades de una suscripción de extracción a una publicación transaccional o de instantáneas  
  
1.  En el suscriptor, ejecute [sp_change_subscription_properties](../../relational-databases/system-stored-procedures/sp-change-subscription-properties-transact-sql.md), especificando **@publisher**, **@publisher_db**, **@publication**, valor **0** (transaccional) o **1** (instantánea) para **@publication_type**, la propiedad que se está cambiando como **@property**, y el nuevo valor como **@value**.  
  
2.  (Opcional) En el suscriptor en la base de datos de suscripción, ejecute [sp_changesubscriptiondtsinfo](../../relational-databases/system-stored-procedures/sp-changesubscriptiondtsinfo-transact-sql.md). Especifique el identificador del trabajo del agente de distribución **@jobid**, y propiedades del paquete de servicios de transformación de datos (DTS) siguiente:  
  
    -   **@dts_package_name**  
  
    -   **@dts_package_password**  
  
    -   **@dts_package_location**  
  
     De esta forma se cambian las propiedades del paquete DTS de una suscripción.  
  
    > [!NOTE]  
    >  El identificador puede obtenerse mediante la ejecución de trabajo [sp_helpsubscription](../../relational-databases/system-stored-procedures/sp-helpsubscription-transact-sql.md).  
  
#### Para ver o las propiedades de una suscripción de extracción a una publicación de combinación  
  
1.  En el suscriptor, ejecute [sp_helpmergepullsubscription](../../relational-databases/system-stored-procedures/sp-helpmergepullsubscription-transact-sql.md). Especifique **@publisher**, **@publisher_db**, y **@publication**.  
  
2.  En el suscriptor, ejecute [sp_helpsubscription_properties](../../relational-databases/system-stored-procedures/sp-helpsubscription-properties-transact-sql.md). Especifique **@publisher**, **@publisher_db**, **@publication**, y un valor de 2 para **@publication_type**.  
  
3.  En el publicador, ejecute [sp_helpmergesubscription](../../relational-databases/system-stored-procedures/sp-helpmergesubscription-transact-sql.md) para mostrar información de suscripción. Para obtener información acerca de una suscripción específica, debe especificar **@publication**, **@subscriber**, y un valor de **extracción** para **@subscription_type**.  
  
4.  En el publicador, ejecute [sp_helpsubscriberinfo](../../relational-databases/system-stored-procedures/sp-helpsubscriberinfo-transact-sql.md), especificando **@subscriber**. Presenta información acerca del suscriptor.  
  
#### Para cambiar las propiedades de una suscripción de extracción a una publicación de combinación  
  
1.  En el suscriptor, ejecute [sp_changemergepullsubscription](../../relational-databases/system-stored-procedures/sp-changemergepullsubscription-transact-sql.md). Especifique **@publication**, **@publisher**, **@publisher_db**, la propiedad que se está cambiando como **@property**, y el nuevo valor como **@value**.  
  
##  <a name="RMOProcedure"></a> Usar Replication Management Objects (RMO)  
 Las clases RMO que usa para ver o modificar las propiedades de suscripción de extracción dependen del tipo de publicación a la que se suscribe la suscripción de extracción.  
  
#### Para ver o modificar propiedades de una suscripción de extracción a una publicación transaccional o de instantáneas  
  
1.  Crear una conexión al suscriptor mediante la <xref:Microsoft.SqlServer.Management.Common.ServerConnection> clase.  
  
2.  Cree una instancia de la <xref:Microsoft.SqlServer.Replication.TransPullSubscription> clase.  
  
3.  Establecer el <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationName%2A>, <xref:Microsoft.SqlServer.Replication.PullSubscription.DatabaseName%2A>, <xref:Microsoft.SqlServer.Replication.PullSubscription.PublisherName%2A>, y <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationDBName%2A> Propiedades.  
  
4.  Establezca la conexión del paso 1 para el <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> propiedad.  
  
5.  Llame a la <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> método para obtener las propiedades del objeto. Si este método devuelve **false**, se definieron incorrectamente las propiedades de suscripción en el paso 3, o bien la suscripción no existe en el servidor.  
  
6.  (Opcional) Para cambiar las propiedades, establezca un nuevo valor para uno de los <xref:Microsoft.SqlServer.Replication.TransPullSubscription> propiedades que se pueden establecer y, a continuación, llame a la <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> (método).  
  
7.  (Opcional) Para ver la nueva configuración, llame el <xref:Microsoft.SqlServer.Replication.ReplicationObject.Refresh%2A> método para volver a cargar las propiedades del artículo.  
  
8.  Cierre todas las conexiones.  
  
#### Para ver o modificar las propiedades de una suscripción de extracción a una publicación de combinación  
  
1.  Crear una conexión al suscriptor mediante la <xref:Microsoft.SqlServer.Management.Common.ServerConnection> clase.  
  
2.  Cree una instancia de la <xref:Microsoft.SqlServer.Replication.MergePullSubscription> clase.  
  
3.  Establecer el <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationName%2A>, <xref:Microsoft.SqlServer.Replication.PullSubscription.DatabaseName%2A>, <xref:Microsoft.SqlServer.Replication.PullSubscription.PublisherName%2A>, y <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationDBName%2A> Propiedades.  
  
4.  Establezca la conexión del paso 1 para el <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> propiedad.  
  
5.  Llame a la <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> método para obtener las propiedades del objeto. Si este método devuelve **false**, se definieron incorrectamente las propiedades de suscripción en el paso 3, o bien la suscripción no existe en el servidor.  
  
6.  (Opcional) Para cambiar las propiedades, establezca un nuevo valor para uno de los <xref:Microsoft.SqlServer.Replication.MergePullSubscription> propiedades que se pueden establecer y, a continuación, llame a la <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> (método).  
  
7.  (Opcional) Para ver la nueva configuración, llame el <xref:Microsoft.SqlServer.Replication.ReplicationObject.Refresh%2A> método para volver a cargar las propiedades del artículo.  
  
8.  Cierre todas las conexiones.  
  
## Vea también  
 [Ver la información y realizar tareas para una suscripción & #40; Monitor de replicación & #41;](../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-a-subscription-replication-monitor.md)   
 [Prácticas recomendadas de seguridad de replicación](../../relational-databases/replication/security/replication-security-best-practices.md)   
 [Suscribirse a publicaciones](../../relational-databases/replication/subscribe-to-publications.md)  
  
  