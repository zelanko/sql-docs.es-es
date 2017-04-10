---
title: "Eliminar una suscripci&#243;n de extracci&#243;n | Microsoft Docs"
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
  - "quitar suscripciones"
  - "eliminar suscripciones"
  - "suscripciones de extracción [replicación de SQL Server], eliminar"
  - "suscripciones [replicación de SQL Server], extraer"
ms.assetid: 997c0b8e-d8d9-4eed-85b1-6baa1f8594ce
caps.latest.revision: 35
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 35
---
# Eliminar una suscripci&#243;n de extracci&#243;n
  En este tema se describe cómo eliminar una suscripción de extracción en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../includes/tsql-md.md)] o Replication Management Objects (RMO).  
  
 **En este tema**  
  
-   **Para eliminar una suscripción de extracción con:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [Replication Management Objects (RMO)](#RMOProcedure)  
  
##  <a name="SSMSProcedure"></a> Usar SQL Server Management Studio  
 Eliminar una suscripción de extracción en el publicador (desde el **publicaciones locales** carpeta [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]) o en el suscriptor (desde el **suscripciones locales** carpeta). Al eliminar una suscripción no se quitan los objetos ni los datos de la suscripción, y deben quitarse manualmente.  
  
#### Para eliminar una suscripción de extracción en el publicador  
  
1.  Conéctese al publicador en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]y, a continuación, expanda el nodo del servidor.  
  
2.  Expanda la carpeta **Replicación** y, a continuación, expanda la carpeta **Publicaciones locales** .  
  
3.  Expanda la publicación asociada con la suscripción que desea eliminar.  
  
4.  Haga clic en la suscripción y, a continuación, haga clic en **Eliminar**.  
  
5.  En el cuadro de diálogo de confirmación, seleccione si desea conectarse al suscriptor para eliminar la información de suscripciones. Si desactiva la casilla **Conectar a suscriptor** , deberá conectarse al suscriptor más adelante para eliminar la información.  
  
#### Para eliminar una suscripción de extracción en el suscriptor  
  
1.  Conéctese al suscriptor en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]y expanda el nodo de servidor.  
  
2.  Expanda la carpeta **Replicación** y, a continuación, expanda la carpeta **Suscripciones locales** .  
  
3.  Haga clic en la suscripción que desea eliminar y, a continuación, haga clic en **Eliminar**.  
  
4.  En el cuadro de diálogo de confirmación, seleccione si desea conectarse al publicador para eliminar la información de suscripciones. Si desactiva la casilla **Conectar al publicador** , deberá conectarse al publicador más adelante para eliminar la información.  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
 Las suscripciones de extracción pueden eliminarse mediante programación con procedimientos almacenados de replicación. Los procedimientos almacenados que se usen dependerán del tipo de publicación a la que corresponda la suscripción.  
  
#### Para eliminar una suscripción de extracción a una publicación transaccional o de instantáneas  
  
1.  En el suscriptor en la base de datos de suscripción, ejecute [sp_droppullsubscription & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-droppullsubscription-transact-sql.md). Especifique **@publication**, **@publisher**, y **@publisher_db**.  
  
2.  En el publicador de la base de datos de publicación, ejecute [sp_dropsubscription & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-dropsubscription-transact-sql.md). Especifique **@publication** y **@subscriber**. Especifique un valor de **all** para **@article**. (Opcional) Si no se puede tener acceso al distribuidor, especifique un valor de **1** para **@ignore_distributor** para eliminar la suscripción sin quitar los objetos relacionados en el distribuidor.  
  
#### Para eliminar una suscripción de extracción a una publicación de combinación  
  
1.  En el suscriptor en la base de datos de suscripción, ejecute [sp_dropmergepullsubscription & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-dropmergepullsubscription-transact-sql.md). Especifique **@publication**, **@publisher**, y **@publisher_db**.  
  
2.  En el publicador de la base de datos de publicación, ejecute [sp_dropmergesubscription & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-dropmergesubscription-transact-sql.md). Especifique **@publication**, **@subscriber**, y **@subscriber_db**. Especifique un valor de **extracción** para **@subscription_type**. (Opcional) Si no se puede tener acceso al distribuidor, especifique un valor de **1** para **@ignore_distributor** para eliminar la suscripción sin quitar los objetos relacionados en el distribuidor.  
  
###  <a name="TsqlExample"></a> Ejemplos (Transact-SQL)  
 El siguiente ejemplo elimina una suscripción de extracción en una publicación transaccional. El primer lote se ejecuta en el Suscriptor y el segundo lote se ejecuta en el Publicador.  
  
 [!code-sql[HowTo#sp_droptranpullsubscription](../../relational-databases/replication/codesnippet/tsql/delete-a-pull-subscription_1.sql)]  
  
 [!code-sql[HowTo#sp_droptransubscription](../../relational-databases/replication/codesnippet/tsql/delete-a-pull-subscription_2.sql)]  
  
 El siguiente ejemplo elimina una suscripción de extracción en una publicación de combinación. El primer lote se ejecuta en el Suscriptor y el segundo lote se ejecuta en el Publicador.  
  
 [!code-sql[HowTo#sp_dropmergepullsubscription](../../relational-databases/replication/codesnippet/tsql/delete-a-pull-subscription_3.sql)]  
  
 [!code-sql[HowTo#sp_dropmergesubscription](../../relational-databases/replication/codesnippet/tsql/delete-a-pull-subscription_4.sql)]  
  
##  <a name="RMOProcedure"></a> Usar Replication Management Objects (RMO)  
 Las suscripciones de extracción se pueden eliminar mediante programación utilizando Replication Management Objects (RMO). Las clases RMO que se usan para eliminar una suscripción de extracción dependen del tipo de publicación a la se suscribe dicha suscripción.  
  
#### Para eliminar una suscripción de extracción a una publicación transaccional o de instantáneas  
  
1.  Crear conexiones con el suscriptor y el publicador mediante la <xref:Microsoft.SqlServer.Management.Common.ServerConnection> clase.  
  
2.  Cree una instancia de la <xref:Microsoft.SqlServer.Replication.TransPullSubscription> clase y establezca la <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationName%2A>, <xref:Microsoft.SqlServer.Replication.PullSubscription.DatabaseName%2A>, <xref:Microsoft.SqlServer.Replication.PullSubscription.PublisherName%2A>, y <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationDBName%2A> Propiedades. Use la conexión de suscriptor del paso 1 para establecer el <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> propiedad.  
  
3.  Compruebe el <xref:Microsoft.SqlServer.Replication.ReplicationObject.IsExistingObject%2A> propiedad para comprobar la existencia de la suscripción. Si el valor de esta propiedad es **false**, significa que las propiedades de suscripción del paso 2 se definieron incorrectamente o bien, que la suscripción no existe.  
  
4.  Llame a la <xref:Microsoft.SqlServer.Replication.PullSubscription.Remove%2A> método.  
  
5.  Cree una instancia de la <xref:Microsoft.SqlServer.Replication.TransPublication> clase mediante la conexión de publicador del paso 1. Especifique <xref:Microsoft.SqlServer.Replication.Publication.Name%2A>, <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A> y <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>.  
  
6.  Llame a la <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> método. Si este método devuelve **false**, las propiedades especificadas en el paso 5 son incorrectas o la publicación no existe en el servidor.  
  
7.  Llame a la <xref:Microsoft.SqlServer.Replication.TransPublication.RemovePullSubscription%2A> método. Especifique el nombre del Suscriptor y la base de datos de suscripciones para los parámetros *subscriber* y *subscriberDB* .  
  
#### Para eliminar una suscripción de extracción a una publicación de combinación  
  
1.  Crear conexiones con el suscriptor y el publicador mediante la <xref:Microsoft.SqlServer.Management.Common.ServerConnection> clase.  
  
2.  Cree una instancia de la <xref:Microsoft.SqlServer.Replication.MergePullSubscription> clase y establezca la <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationName%2A>, <xref:Microsoft.SqlServer.Replication.PullSubscription.DatabaseName%2A>, <xref:Microsoft.SqlServer.Replication.PullSubscription.PublisherName%2A>, y <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationDBName%2A> Propiedades. Usar la conexión del paso 1 para establecer el <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> propiedad.  
  
3.  Compruebe el <xref:Microsoft.SqlServer.Replication.ReplicationObject.IsExistingObject%2A> propiedad para comprobar la existencia de la suscripción. Si el valor de esta propiedad es **false**, significa que las propiedades de suscripción del paso 2 se definieron incorrectamente o bien, que la suscripción no existe.  
  
4.  Llame a la <xref:Microsoft.SqlServer.Replication.PullSubscription.Remove%2A> método.  
  
5.  Cree una instancia de la <xref:Microsoft.SqlServer.Replication.MergePublication> clase mediante la conexión de publicador del paso 1. Especifique <xref:Microsoft.SqlServer.Replication.Publication.Name%2A>, <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A> y <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>.  
  
6.  Llame a la <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> método. Si este método devuelve **false**, las propiedades especificadas en el paso 5 son incorrectas o la publicación no existe en el servidor.  
  
7.  Llame a la <xref:Microsoft.SqlServer.Replication.MergePublication.RemovePullSubscription%2A> método. Especifique el nombre del Suscriptor y la base de datos de suscripciones para los parámetros *subscriber* y *subscriberDB* .  
  
###  <a name="PShellExample"></a> Ejemplos (RMO)  
 Este ejemplo elimina una suscripción de extracción a una publicación transaccional y quita el registro de suscripciones en el Publicador.  
  
 [!code-csharp[HowTo#rmo_DropTranPullSub](../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_droptranpullsub)]  
  
 [!code-vb[HowTo#rmo_vb_DropTranPullSub](../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_droptranpullsub)]  
  
 Este ejemplo elimina una suscripción de extracción a una publicación de combinación y quita el registro de suscripciones en el Publicador.  
  
 [!code-csharp[HowTo#rmo_DropMergePullSub](../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_dropmergepullsub)]  
  
 [!code-vb[HowTo#rmo_vb_DropMergePullSub](../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_dropmergepullsub)]  
  
## Vea también  
 [Suscribirse a publicaciones](../../relational-databases/replication/subscribe-to-publications.md)   
 [Prácticas recomendadas de seguridad de replicación](../../relational-databases/replication/security/replication-security-best-practices.md)  
  
  