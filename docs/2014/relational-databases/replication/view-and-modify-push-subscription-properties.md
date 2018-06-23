---
title: Ver y modificar las propiedades de una suscripción de inserción | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- viewing replication properties
- push subscriptions [SQL Server replication], properties
- subscriptions [SQL Server replication], push
- push subscriptions [SQL Server replication], modifying
- modifying replication properties, push subscriptions
- modifying subscriptions, SQL Server Management Studio
ms.assetid: 801d2995-7aa5-4626-906e-c8190758ec71
caps.latest.revision: 36
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 188fbbe63303bf4de5a725b3563bf1f8f5d6db6f
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36203379"
---
# <a name="view-and-modify-push-subscription-properties"></a>Ver y modificar las propiedades de una suscripción de inserción
  En este tema se describe cómo ver y modificar las propiedades de una suscripción de inserción en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../includes/tsql-md.md)]o Replication Management Objects (RMO).  
  
 **En este tema**  
  
-   **Para ver y modificar las propiedades de una suscripción de inserción con:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [Replication Management Objects (RMO)](#RMOProcedure)  
  
##  <a name="SSMSProcedure"></a> Usar SQL Server Management Studio  
 Vea y modifique las propiedades de suscripción de inserción del publicador en:  
  
-   El cuadro de diálogo **Propiedades de suscripción - \<Publicador>: \<baseDeDatosDePublicación>**, que está disponible en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
-   La pestaña **Todas las suscripciones** en el Monitor de replicación. Para información sobre cómo iniciar el Monitor de replicación, vea [Iniciar el Monitor de replicación](monitor/start-the-replication-monitor.md).  
  
#### <a name="to-view-and-modify-push-subscription-properties-in-management-studio"></a>Ver y modificar las propiedades de suscripción de inserción en Management Studio  
  
1.  Conéctese al publicador en [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]y, a continuación, expanda el nodo del servidor.  
  
2.  Expanda la carpeta **Replicación** y, a continuación, expanda la carpeta **Publicaciones locales** .  
  
3.  Expanda la publicación apropiada, haga clic con el botón secundario en una suscripción y, a continuación, haga clic en **Propiedades**.  
  
4.  Modifique las propiedades si es necesario y, a continuación, haga clic en **Aceptar**.  
  
#### <a name="to-view-and-modify-push-subscription-properties-in-replication-monitor"></a>Para ver y modificar las propiedades de suscripción de inserción en el Monitor de replicación  
  
1.  Expanda un grupo de publicador en el panel izquierdo del Monitor de replicación, expanda un publicador y, a continuación, haga clic en una publicación.  
  
2.  Haga clic en la pestaña **Todas las suscripciones** .  
  
3.  Haga clic con el botón secundario en una suscripción y, a continuación, haga clic en **Propiedades**.  
  
4.  Modifique las propiedades si es necesario y, a continuación, haga clic en **Aceptar**.  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
 Se puede modificar las suscripciones de inserción y tener acceso a sus propiedades mediante programación utilizando procedimientos almacenados de replicación. Los procedimientos almacenados que se usen dependerán del tipo de publicación a la que corresponda la suscripción.  
  
#### <a name="to-view-the-properties-of-a-push-subscription-to-a-snapshot-or-transactional-publication"></a>Para ver las propiedades de una suscripción de inserción a una publicación transaccional o de instantáneas  
  
1.  En la base de datos de publicación del publicador, ejecute [sp_helpsubscription](/sql/relational-databases/system-stored-procedures/sp-helpsubscription-transact-sql). Especifique **@publication**, **@subscriber**y el valor **all** para **@article**.  
  
2.  En la base de datos de publicación del publicador, ejecute [sp_helpsubscriberinfo](/sql/relational-databases/system-stored-procedures/sp-helpsubscriberinfo-transact-sql), especificando **@subscriber**.  
  
#### <a name="to-change-the-properties-of-a-push-subscription-to-a-snapshot-or-transactional-publication"></a>Para modificar las propiedades de una suscripción de inserción a una publicación transaccional o de instantáneas  
  
1.  En la base de datos de publicación del publicador, ejecute [sp_changesubscriber](/sql/relational-databases/system-stored-procedures/sp-changesubscriber-transact-sql), especificando **@subscriber** y los parámetros de las propiedades del suscriptor que se vayan a cambiar.  
  
2.  En la base de datos de publicación del publicador, ejecute [sp_changesubscription](/sql/relational-databases/system-stored-procedures/sp-changesubscription-transact-sql). Especifique **@publication**, **@subscriber**, **@destination_db**, el valor **all** para **@article**, la propiedad de suscripción que se está cambiando como **@property**y el nuevo valor como **@value**. Esto cambia la configuración de seguridad para la suscripción de inserción.  
  
3.  (Opcional) Para cambiar las propiedades del paquete de Servicios de transformación de datos (DTS) de una suscripción, ejecute [sp_changesubscriptiondtsinfo](/sql/relational-databases/system-stored-procedures/sp-changesubscriptiondtsinfo-transact-sql) en la base de datos de suscripciones del suscriptor. Especifique el identificador del trabajo del Agente de distribución para **@jobid** y las siguientes propiedades del paquete DTS:  
  
    -   **@dts_package_name**  
  
    -   **@dts_package_password**  
  
    -   **@dts_package_location**  
  
     De esta forma se cambian las propiedades del paquete DTS de una suscripción.  
  
    > [!NOTE]  
    >  El Id del trabajo se puede obtener ejecutando [sp_helpsubscription](/sql/relational-databases/system-stored-procedures/sp-helpsubscription-transact-sql).  
  
#### <a name="to-view-the-properties-of-a-push-subscription-to-a-merge-publication"></a>Para ver o las propiedades de una suscripción de inserción a una publicación de combinación  
  
1.  En la base de datos de publicación del publicador, ejecute [sp_helpmergesubscription](/sql/relational-databases/system-stored-procedures/sp-helpmergesubscription-transact-sql). Especifique **@publication** y **@subscriber**.  
  
2.  En el publicador, ejecute [sp_helpsubscriberinfo](/sql/relational-databases/system-stored-procedures/sp-helpsubscriberinfo-transact-sql), especificando **@subscriber**.  
  
#### <a name="to-change-the-properties-of-a-push-subscription-to-a-merge-publication"></a>Para cambiar las propiedades de una suscripción de inserción a una publicación de combinación  
  
1.  En la base de datos de publicación del publicador, ejecute [sp_changemergesubscription](/sql/relational-databases/system-stored-procedures/sp-changemergesubscription-transact-sql). Especifique **@publication**, **@subscriber**, **@subscriber_db**, la propiedad de suscripción que se está cambiando como **@property**y el nuevo valor como **@value**.  
  
###  <a name="TsqlExample"></a> Ejemplo (Transact-SQL)  
  
##  <a name="RMOProcedure"></a> Usar Replication Management Objects (RMO)  
 Las clases RMO que usa para ver o modificar las propiedades de suscripción de inserción dependen del tipo de publicación a la que se suscribe la suscripción de inserción.  
  
#### <a name="to-view-or-modify-properties-of-a-push-subscription-to-a-snapshot-or-transactional-publication"></a>Para ver o modificar propiedades de una suscripción de inserción a una publicación transaccional o de instantáneas  
  
1.  Cree una conexión al publicador mediante la clase <xref:Microsoft.SqlServer.Management.Common.ServerConnection> .  
  
2.  Cree una instancia de la clase <xref:Microsoft.SqlServer.Replication.TransSubscription> .  
  
3.  Establezca las propiedades <xref:Microsoft.SqlServer.Replication.Subscription.PublicationName%2A>, <xref:Microsoft.SqlServer.Replication.Subscription.DatabaseName%2A>, <xref:Microsoft.SqlServer.Replication.Subscription.SubscriberName%2A>y <xref:Microsoft.SqlServer.Replication.Subscription.SubscriptionDBName%2A> .  
  
4.  Establezca la conexión <xref:Microsoft.SqlServer.Management.Common.ServerConnection> del paso 1 para la propiedad <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> .  
  
5.  Llame al método <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> para obtener las propiedades del objeto. Si este método devuelve `false`, significa que las propiedades de suscripción en el paso 3 se definieron incorrectamente o la suscripción no existe.  
  
6.  (Opcional) Para cambiar las propiedades, establezca un nuevo valor para una de las propiedades <xref:Microsoft.SqlServer.Replication.TransSubscription> que se puedan establecer y, a continuación, llame al método <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> .  
  
7.  (Opcional) Para ver los nuevos valores, llame al método <xref:Microsoft.SqlServer.Replication.ReplicationObject.Refresh%2A> para recargar las propiedades de la suscripción.  
  
#### <a name="to-view-or-modify-properties-of-a-push-subscription-to-a-merge-publication"></a>Para ver o modificar las propiedades de una suscripción de inserción a una publicación de combinación  
  
1.  Cree una conexión al suscriptor mediante la clase <xref:Microsoft.SqlServer.Management.Common.ServerConnection> .  
  
2.  Cree una instancia de la clase <xref:Microsoft.SqlServer.Replication.MergeSubscription> .  
  
3.  Establezca las propiedades <xref:Microsoft.SqlServer.Replication.Subscription.PublicationName%2A>, <xref:Microsoft.SqlServer.Replication.Subscription.DatabaseName%2A>, <xref:Microsoft.SqlServer.Replication.Subscription.SubscriberName%2A>y <xref:Microsoft.SqlServer.Replication.Subscription.SubscriptionDBName%2A> .  
  
4.  Establezca la conexión <xref:Microsoft.SqlServer.Management.Common.ServerConnection> del paso 1 para la propiedad <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> .  
  
5.  Llame al método <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> para obtener las propiedades del objeto. Si este método devuelve `false`, significa que las propiedades de suscripción en el paso 3 se definieron incorrectamente o la suscripción no existe.  
  
6.  (Opcional) Para cambiar las propiedades, establezca un nuevo valor para una de las propiedades <xref:Microsoft.SqlServer.Replication.MergeSubscription> que se puedan establecer y, a continuación, llame al método <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> .  
  
7.  (Opcional) Para ver los nuevos valores, llame al método <xref:Microsoft.SqlServer.Replication.ReplicationObject.Refresh%2A> para recargar las propiedades de la suscripción.  
  
## <a name="see-also"></a>Vea también  
 [Ver información y realizar tareas para una suscripción &#40;Monitor de replicación&#41;](monitor/view-information-and-perform-tasks-for-a-subscription-replication-monitor.md)   
 [Replication Security Best Practices](security/replication-security-best-practices.md)  (Prácticas recomendadas de seguridad de replicación)  
 [Suscribirse a publicaciones](subscribe-to-publications.md)  
  
  
