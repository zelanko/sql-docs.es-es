---
title: "Ver y modificar las propiedades de una suscripci&#243;n de inserci&#243;n | Microsoft Docs"
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
  - "ver propiedades de replicación"
  - "suscripciones de inserción [replicación de SQL Server], propiedades"
  - "suscripciones [replicación de SQL Server], extraer"
  - "suscripciones de inserción [replicación de SQL Server], modificar"
  - "modificar propiedades de replicación, suscripciones de inserción"
  - "modificar suscripciones, SQL Server Management Studio"
ms.assetid: 801d2995-7aa5-4626-906e-c8190758ec71
caps.latest.revision: 37
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 37
---
# Ver y modificar las propiedades de una suscripci&#243;n de inserci&#243;n
  En este tema se describe cómo ver y modificar las propiedades de una suscripción de inserción en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../includes/tsql-md.md)] o Replication Management Objects (RMO).  
  
 **En este tema**  
  
-   **Para ver y modificar las propiedades de una suscripción de inserción con:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [Replication Management Objects (RMO)](#RMOProcedure)  
  
##  <a name="SSMSProcedure"></a> Usar SQL Server Management Studio  
 Vea y modifique las propiedades de suscripción de inserción del publicador en:  
  
-   El **Propiedades de suscripción - \< publicador>: \< Basededatosdepublicaciones>** cuadro de diálogo, que está disponible en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
-   La pestaña **Todas las suscripciones** en el Monitor de replicación. Para obtener información acerca de cómo iniciar el Monitor de replicación, consulte [iniciar el Monitor de replicación](../../relational-databases/replication/monitor/start-the-replication-monitor.md).  
  
#### Ver y modificar las propiedades de suscripción de inserción en Management Studio  
  
1.  Conéctese al publicador en [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]y, a continuación, expanda el nodo del servidor.  
  
2.  Expanda la carpeta **Replicación** y, a continuación, expanda la carpeta **Publicaciones locales** .  
  
3.  Expanda la publicación apropiada, haga clic en una suscripción y, a continuación, haga clic en **propiedades**.  
  
4.  Modifique las propiedades si es necesario y, a continuación, haga clic en **Aceptar**.  
  
#### Para ver y modificar las propiedades de suscripción de inserción en el Monitor de replicación  
  
1.  Expanda un grupo de publicador en el panel izquierdo del Monitor de replicación, expanda un publicador y, a continuación, haga clic en una publicación.  
  
2.  Haga clic en la pestaña **Todas las suscripciones** .  
  
3.  Haga clic en una suscripción y, a continuación, haga clic en **propiedades**.  
  
4.  Modifique las propiedades si es necesario y, a continuación, haga clic en **Aceptar**.  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
 Se puede modificar las suscripciones de inserción y tener acceso a sus propiedades mediante programación utilizando procedimientos almacenados de replicación. Los procedimientos almacenados que se usen dependerán del tipo de publicación a la que corresponda la suscripción.  
  
#### Para ver las propiedades de una suscripción de inserción a una publicación transaccional o de instantáneas  
  
1.  En el publicador de la base de datos de publicación, ejecute [sp_helpsubscription](../../relational-databases/system-stored-procedures/sp-helpsubscription-transact-sql.md). Especifique **@publication**, **@subscriber**y el valor **all** para **@article**.  
  
2.  En el publicador de la base de datos de publicación, ejecute [sp_helpsubscriberinfo](../../relational-databases/system-stored-procedures/sp-helpsubscriberinfo-transact-sql.md), especificando **@subscriber**.  
  
#### Para modificar las propiedades de una suscripción de inserción a una publicación transaccional o de instantáneas  
  
1.  En el publicador de la base de datos de publicación, ejecute [sp_changesubscriber](../../relational-databases/system-stored-procedures/sp-changesubscriber-transact-sql.md), especificando **@subscriber** y los parámetros de las propiedades del suscriptor que se va a cambiar.  
  
2.  En el publicador de la base de datos de publicación, ejecute [sp_changesubscription](../../relational-databases/system-stored-procedures/sp-changesubscription-transact-sql.md). Especifique **@publication**, **@subscriber**, **@destination_db**, un valor de **todos los** para **@article**, la propiedad que se está cambiando como **@property**, y el nuevo valor como **@value**. Esto cambia la configuración de seguridad para la suscripción de inserción.  
  
3.  (Opcional) Para cambiar las propiedades del paquete de servicios de transformación de datos (DTS) de una suscripción, ejecute [sp_changesubscriptiondtsinfo](../../relational-databases/system-stored-procedures/sp-changesubscriptiondtsinfo-transact-sql.md) en el suscriptor de la base de datos de suscripción. Especifique el identificador del trabajo del Agente de distribución para **@jobid** y las siguientes propiedades del paquete DTS:  
  
    -   **@dts_package_name**  
  
    -   **@dts_package_password**  
  
    -   **@dts_package_location**  
  
     De esta forma se cambian las propiedades del paquete DTS de una suscripción.  
  
    > [!NOTE]  
    >  El identificador puede obtenerse mediante la ejecución de trabajo [sp_helpsubscription](../../relational-databases/system-stored-procedures/sp-helpsubscription-transact-sql.md).  
  
#### Para ver o las propiedades de una suscripción de inserción a una publicación de combinación  
  
1.  En el publicador de la base de datos de publicación, ejecute [sp_helpmergesubscription](../../relational-databases/system-stored-procedures/sp-helpmergesubscription-transact-sql.md). Especifique **@publication** y **@subscriber**.  
  
2.  En el publicador, ejecute [sp_helpsubscriberinfo](../../relational-databases/system-stored-procedures/sp-helpsubscriberinfo-transact-sql.md), especificando **@subscriber**.  
  
#### Para cambiar las propiedades de una suscripción de inserción a una publicación de combinación  
  
1.  En el publicador de la base de datos de publicación, ejecute [sp_changemergesubscription](../../relational-databases/system-stored-procedures/sp-changemergesubscription-transact-sql.md). Especifique **@publication**, **@subscriber**, **@subscriber_db**, la propiedad que se está cambiando como **@property**, y el nuevo valor como **@value**.  
  
###  <a name="TsqlExample"></a> Ejemplo (Transact-SQL)  
  
##  <a name="RMOProcedure"></a> Usar Replication Management Objects (RMO)  
 Las clases RMO que usa para ver o modificar las propiedades de suscripción de inserción dependen del tipo de publicación a la que se suscribe la suscripción de inserción.  
  
#### Para ver o modificar propiedades de una suscripción de inserción a una publicación transaccional o de instantáneas  
  
1.  Crear una conexión al publicador mediante la <xref:Microsoft.SqlServer.Management.Common.ServerConnection> clase.  
  
2.  Cree una instancia de la <xref:Microsoft.SqlServer.Replication.TransSubscription> clase.  
  
3.  Establecer el <xref:Microsoft.SqlServer.Replication.Subscription.PublicationName%2A>, <xref:Microsoft.SqlServer.Replication.Subscription.DatabaseName%2A>, <xref:Microsoft.SqlServer.Replication.Subscription.SubscriberName%2A>, y <xref:Microsoft.SqlServer.Replication.Subscription.SubscriptionDBName%2A> Propiedades.  
  
4.  Establecer el <xref:Microsoft.SqlServer.Management.Common.ServerConnection> del paso 1 para el <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> valor de la propiedad.  
  
5.  Llame a la <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> método para obtener las propiedades del objeto. Si este método devuelve **false**, significa que las propiedades de suscripción del paso 3 se definieron incorrectamente, o bien que la suscripción no existe.  
  
6.  (Opcional) Para cambiar las propiedades, establezca un nuevo valor para uno de los <xref:Microsoft.SqlServer.Replication.TransSubscription> propiedades que se pueden establecer y, a continuación, llame a la <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> (método).  
  
7.  (Opcional) Para ver la nueva configuración, llame el <xref:Microsoft.SqlServer.Replication.ReplicationObject.Refresh%2A> método para volver a cargar las propiedades de la suscripción.  
  
#### Para ver o modificar las propiedades de una suscripción de inserción a una publicación de combinación  
  
1.  Crear una conexión al suscriptor mediante la <xref:Microsoft.SqlServer.Management.Common.ServerConnection> clase.  
  
2.  Cree una instancia de la <xref:Microsoft.SqlServer.Replication.MergeSubscription> clase.  
  
3.  Establecer el <xref:Microsoft.SqlServer.Replication.Subscription.PublicationName%2A>, <xref:Microsoft.SqlServer.Replication.Subscription.DatabaseName%2A>, <xref:Microsoft.SqlServer.Replication.Subscription.SubscriberName%2A>, y <xref:Microsoft.SqlServer.Replication.Subscription.SubscriptionDBName%2A> Propiedades.  
  
4.  Establecer el <xref:Microsoft.SqlServer.Management.Common.ServerConnection> del paso 1 para el <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> valor de la propiedad.  
  
5.  Llame a la <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> método para obtener las propiedades del objeto. Si este método devuelve **false**, significa que las propiedades de suscripción del paso 3 se definieron incorrectamente, o bien que la suscripción no existe.  
  
6.  (Opcional) Para cambiar las propiedades, establezca un nuevo valor para uno de los <xref:Microsoft.SqlServer.Replication.MergeSubscription> propiedades que se pueden establecer y, a continuación, llame a la <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> (método).  
  
7.  (Opcional) Para ver la nueva configuración, llame el <xref:Microsoft.SqlServer.Replication.ReplicationObject.Refresh%2A> método para volver a cargar las propiedades de la suscripción.  
  
## Vea también  
 [Ver la información y realizar tareas para una suscripción & #40; Monitor de replicación & #41;](../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-a-subscription-replication-monitor.md)   
 [Prácticas recomendadas de seguridad de replicación](../../relational-databases/replication/security/replication-security-best-practices.md)   
 [Suscribirse a publicaciones](../../relational-databases/replication/subscribe-to-publications.md)  
  
  